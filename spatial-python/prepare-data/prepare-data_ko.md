# 데이터 준비

## 소개

이 실습에서는 가상의 재무 트랜잭션 데이터가 Autonomous Database로 로드되고 공간 및 시간적("spatiotemporal") 분석을 위해 구성됩니다.

예상 실험 시간: 10분

### 목표

*   Autonomous Database로 재무 트랜잭션 데이터 로드
*   시간 기준 분석을 위한 데이터 구성

### 필요 조건

*   Lab 4 완료: Python에서 Autonomous Database에 연결

## 작업 1: 데이터 파일 업로드

1.  다음 링크를 사용하여 데이터 파일을 다운로드합니다.

*   [locations.csv](./data/locations.csv)
*   [transactions.csv](./data/transactions.csv)

2.  **업로드** 아이콘을 눌러 데이터 파일을 로드합니다. ![데이터 업로드](images/prepare-data-01.png)
    
3.  왼쪽 패널에서 locations.csv 및 transactions.csv을 두 번 눌러 새 탭에서 데이터 파일을 미리 봅니다.
    
    ![파일 미리보기](images/prepare-data-02.png)
    

locations.csv에는 ATM 위치당 하나의 행이 있고 트랜잭션에는 재무 트랜잭션당 하나의 행이 있습니다. 그런 다음 데이터 미리보기로 탭을 닫고 노트북으로 돌아갑니다.

## 작업 2: 테이블 생성 및 로드

1.  노트북의 다음 셀에 다음 명령문을 붙여 넣은 다음 **run** 버튼을 누릅니다. 그러면 locations 데이터에 대한 테이블이 생성됩니다.
    
        <copy>
        # Create table for locations data
        cursor.execute("""
         CREATE TABLE locations (
                   location_id INTEGER,
                   owner VARCHAR2(100),  
                   lon NUMBER,
                   lat NUMBER)""")
        </copy>
        
    
    ![데이터 로드](images/prepare-data-04.png)
    
2.  다음을 실행하여 위치 데이터를 로드합니다.
    
        <copy>
        # Load the locations data
        import csv
        BATCH_SIZE = 1000
        with connection.cursor() as cursor:
            with open('locations.csv', 'r') as csv_file:
                csv_reader = csv.reader(csv_file, delimiter=',')
                #skip header
                next(csv_reader)
                #load data
                sql = "INSERT INTO locations VALUES (:1, :2, :3, :4)"
                data = []
                for line in csv_reader:
                    data.append((line[0], line[1], line[2], line[3]))
                    if len(data) % BATCH_SIZE == 0:
                        cursor.executemany(sql, data)
                        data = []
                if data:
                    cursor.executemany(sql, data)
                connection.commit()
        </copy>
        
    
    ![데이터 로드](images/prepare-data-05.png)
    
3.  다음을 실행하여 좌표 및 고유한 위치 ID를 포함하여 각 ATM 위치에 대해 행이 하나씩 포함된 위치 데이터를 미리 봅니다.
    
        <copy>
        # Preview locations data
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM locations")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![데이터 미리보기](images/prepare-data-06.png)
    
4.  다음 셀에 다음 명령문을 붙여 넣은 다음 **run** 버튼을 누릅니다. 그러면 트랜잭션 데이터에 대한 테이블이 생성됩니다.
    
        <copy>
        # Create table for transactions data
        cursor.execute("""
           CREATE TABLE transactions (
                          trans_id INTEGER,
                          location_id INTEGER,
                          trans_date DATE,
                          cust_id INTEGER)""")
        </copy>
        
    
    ![테이블 생성](images/prepare-data-07.png)
    
5.  다음을 실행하여 트랜잭션 데이터를 로드합니다.
    
        <copy>
        # Load the transactions data
        BATCH_SIZE = 1000
        with connection.cursor() as cursor:
            with open('transactions.csv', 'r') as csv_file:
                csv_reader = csv.reader(csv_file, delimiter=',')
                #skip header
                next(csv_reader)
                #load data
                sql = "INSERT INTO transactions VALUES (:1, :2, TO_DATE(:3,'YYYY-MM-DD:HH24:MI:SS'), :4)"
                data = []
                for line in csv_reader:
                    data.append((line[0], line[1], line[2], line[3]))
                    if len(data) % BATCH_SIZE == 0:
                        cursor.executemany(sql, data)
                        data = []
                if data:
                    cursor.executemany(sql, data)
                connection.commit()
        </copy>
        
    
    ![데이터 로드](images/prepare-data-08.png)
    
6.  다음을 실행하여 데이터 및 위치 ID를 포함하여 각 트랜잭션에 대해 행이 하나씩 포함된 트랜잭션 데이터를 미리 봅니다.
    
        <copy>
        # Preview transactions data
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM transactions")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![데이터 미리보기](images/prepare-data-09.png)
    
7.  다음을 실행하여 고유 고객 ID를 나열합니다.
    
        <copy>
        # Customer ID's
        cursor = connection.cursor()
        cursor.execute("SELECT DISTINCT cust_id FROM transactions ORDER BY cust_id")
        for row in cursor.fetchall():
            print(row[0])
        </copy>
        
    
    ![목록 ID](images/prepare-data-09a.png)
    

## 태스크 3: 시대 일자 추가

임시 계산은 이 워크샵의 핵심 구성 요소이며 날짜와 시간을 정수 형식으로 표현하는 것이 가장 좋습니다. 이 정수 표현은 일반적으로 epoch 시간 또는 보다 구체적으로 UNIX 시간이라고 합니다. 이 연습에서는 모든 트랜잭션에 대한 epoch 시간을 추가합니다.

1.  다음을 실행하여 epoch 날짜에 대한 열을 추가하고 채웁니다.
    
        <copy>
        # add column for epoch date
        cursor.execute("ALTER TABLE transactions ADD (trans_epoch_date integer)")
        </copy>
        
    
        <copy>
        # add column for epoch date
        cursor.execute("""UPDATE transactions
                          SET trans_epoch_date = (trans_date - date'1970-01-01') * 86400""")
        connection.commit()
        </copy>
        
    
    ![Epoch 날짜 추가](images/prepare-data-10.png)
    
2.  다음을 실행하여 트랜잭션 데이터를 다시 미리 봅니다. epoch date 열이 추가되었는지 확인합니다.
    
        <copy>
        # Preview transactions data
        cursor.execute("SELECT * FROM transactions")
        for row in cursor.fetchmany(size=10):
            print(row)
        </copy>
        
    
    ![미리보기 Epoch 날짜](images/prepare-data-11.png)
    

## 작업 4: 공간 작업에 대한 데이터 구성

공간 계산은 이 워크샵의 추가 주요 구성 요소입니다. 이 작업에서는 Autonomous Database의 공간 기능을 활용하도록 위치 데이터를 구성합니다. locations 테이블에는 경도/위도 좌표가 포함되어 있습니다. 한 가지 옵션은 고유 공간 데이터 유형을 사용하여 새 열을 생성하고 채우는 것입니다. 완벽하게 작동하지만 "함수 기반 인덱스화"라는 주류 Oracle Database 기능을 활용하는 또 다른 옵션이 있습니다. 이 접근 방식을 사용하면 열을 만들 필요 없이 새 공간 열을 만드는 것과 관련된 모든 기능을 사용할 수 있습니다. 대신 좌표를 공간 데이터 요소로 변환하는 데이터베이스 함수를 생성한 다음 해당 함수에 인덱스를 생성합니다. 함수와 인덱스가 생성되면 모든 공간 작업은 새 공간 열이 생성된 것처럼 동작합니다. 이 워크샵에서는 작은 데이터 볼륨에 반드시 필요한 것은 아니지만, 열 추가 오버헤드가 중요한 대규모 시스템에는 이러한 접근 방법이 매우 유용합니다.

1.  다음을 실행하여 경도/위도 좌표를 Oracle의 고유 공간 데이터 유형(예: SDO\_GEOMETRY, "기하학"이라고 함)으로 변환하는 함수를 생성합니다. 함수는 좌표를 고유 공간 유형으로 변환할 뿐만 아니라 경도/위도에서 좌표를 "세계 용광자"라는 좌표계로 변환합니다. 이것은 후속 실습에서 사용되는 Python 라이브러리에서 예상되는 좌표계이므로 이 함수에서 이 변환을 수행하는 것이 편리합니다.
    
        <copy>
        # Create function to return lon/lat coordinates as a geometry.
        cursor.execute("""
         CREATE OR REPLACE FUNCTION lonlat_to_proj_geom (longitude IN NUMBER, latitude IN NUMBER)
         RETURN SDO_GEOMETRY DETERMINISTIC IS
         BEGIN
           IF latitude IS NULL OR longitude IS NULL
           OR latitude NOT BETWEEN -90 AND 90
           OR longitude NOT BETWEEN -180 AND 180
           THEN
             RETURN NULL;
           ELSE
              RETURN sdo_cs.transform(
                SDO_GEOMETRY(2001, 4326,
                             sdo_point_type(longitude, latitude, NULL),NULL, NULL),
                3857);
           END IF;
        END;""")
        </copy>
        
    
    ![기능 생성](images/prepare-data-13.png)
    
2.  문자열 표현으로 변환된 형상 및 형상 조회에는 "대형 객체" 또는 "LOB"가 포함됩니다. LOB 위치자를 패치(fetch)한 다음 두번째 라운드 트립에서 LOB 컨텐트를 패치(fetch)하는 대신 LOB가 직접 패치(fetch)되도록 다음 설정을 python-oracledb에 적용합니다.
    
        <copy>
        # return LOBs directly as strings or bytes
        oracledb.defaults.fetch_lobs = False  
        </copy>
        
    
    ![LOB 옵션 설정](images/fetch-lobs.png)
    
3.  다음 명령을 실행하여 함수를 테스트합니다.
    
        <copy>
        # test the function
        cursor.execute("""
         with x as (
            SELECT location_id, lonlat_to_proj_geom(lon,lat) as geom FROM locations)
         SELECT location_id, geom, (geom).get_wkt()
         FROM x
         """)
        for row in cursor.fetchone():
            print(row)
        </copy>
        
    
    ![함수 테스트](images/prepare-data-14.png)
    
4.  공간 질의는 최적의 성능을 위해 공간 인덱스에 의존합니다. 공간 색인은 균일한 치수(즉, 2D 또는 3D)와 좌표계가 있는 데이터에 대해서만 작성할 수 있습니다. 공간 인덱스를 생성하기 전에 인덱스화할 형상에 대해 이러한 특성을 설명하는 메타데이터 행을 삽입해야 합니다. 여기에는 테이블 이름, 형상 열 이름(또는 이 경우 형상을 반환하는 함수), 치수 및 좌표계 코드가 포함됩니다. 공간 인덱스를 생성할 때 메타데이터를 준수하도록 데이터가 먼저 확인됩니다. 데이터가 메타데이터를 준수하는 경우에만 공간 인덱스화가 성공적으로 완료됩니다. 다음을 실행하여 위치 형상에 대한 공간 메타데이터를 작성합니다.
    
        <copy>
        cursor.execute("""
         INSERT INTO user_sdo_geom_metadata VALUES (
            'LOCATIONS', 'ADMIN.LONLAT_TO_PROJ_GEOM(LON,LAT)',
             SDO_DIM_ARRAY(SDO_DIM_ELEMENT('LON', 0, 0, 0.05),
                           SDO_DIM_ELEMENT('LAT', 0, 0, 0.05)),
             3857)
                    """)
        </copy>
        
    
    ![메타데이터 삽입](images/prepare-data-15.png)
    
5.  다음을 실행하여 위치 형상에 대한 공간 색인을 작성합니다.
    
        <copy>
        cursor.execute("""
         CREATE INDEX locations_sidx
         ON locations(LONLAT_TO_PROJ_GEOM(LON,LAT))
         INDEXTYPE IS mdsys.spatial_index_v2
                    """)
        </copy>
        
    
    ![인덱스 생성](images/prepare-data-16.png)
    
6.  공간 인덱스를 확인하려면 다음 spatial query 예제를 실행합니다. 이 질의는 **위치** 테이블에서 거리와 함께 경도, 위도 좌표까지 가장 가까운 5개 항목을 반환합니다. 이를 "가장 가까운 이웃" 질의라고 하며 공간 인덱스를 사용하는 **sdo\_nn( )** 연산자를 사용합니다. 가장 가까운 이웃 쿼리에 대한 자세한 내용은 [설명서](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/spatial-operators-reference.html#GUID-41E6B1FA-1A03-480B-996F-830E8566661D)를 참조하십시오.
    
        <copy>
        cursor.execute("""
         SELECT location_id, round(sdo_nn_distance(1), 2) FROM locations
         WHERE sdo_nn(
           LONLAT_TO_PROJ_GEOM(LON,LAT),
           LONLAT_TO_PROJ_GEOM( -97.6, 30.3),
           'sdo_num_res=5 unit=mile', 1) = 'TRUE' """)
        for row in cursor.fetchmany():
            print(row)  
        </copy>
        
    
    ![공간 질의 실행](images/prepare-data-18.png)
    

이제 **다음 실습을 진행하십시오**.

## 자세히 알아보기

*   UNIX 시간에 대한 자세한 내용은 [https://en.wikipedia.org/wiki/Unix\_time](https://en.wikipedia.org/wiki/Unix_time)을 참조하십시오.
*   함수 기반 공간 인덱싱에 대한 자세한 내용은 [설명서](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/extending-spatial-indexing.html#GUID-CFB6B6DB-4B97-43D1-86A1-21C1BA853089)를 참조하십시오.

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 8월