# 샘플 데이터 생성

## 소개

이 실습에서는 Oracle Database에서 샘플 공간 데이터를 생성하는 단계를 안내합니다.

예상 실험 시간: 10분

### 목표

이 실습에서는 다음을 수행합니다.

*   Oracle Database의 공간 데이터 관리에 대해 알아보기
*   공통 파일 형식에서 Oracle Database의 공간 데이터 준비

### 필요 조건

*   실습 2 완료

### 공간 데이터 정보

Oracle Database는 공간 데이터(포인트, 선, 다각형)를 SDO\_GEOMETRY이라는 고유 데이터 유형에 저장합니다. Oracle Database는 또한 고성능 공간 작업을 위한 고유 공간 인덱스를 제공합니다. 이 공간 인덱스는 공간 데이터를 저장하는 각 테이블 및 형상 열에 대해 입력된 공간 메타데이터에 의존합니다. 공간 데이터가 채워지고 인덱스화되면 강력한 API를 사용하여 공간 분석, 계산 및 처리를 수행할 수 있습니다.

SDO\_GEOMETRY 유형의 일반 형식은 다음과 같습니다.

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

가장 일반적인 형상 유형은 2차원입니다.

| ID | 유형 |
| --- | --- |
| 2001년 | 지점 |
| 2002년 | 라인 |
| 2003년 | 다각형 |

가장 일반적인 좌표계는 다음과 같습니다.

| ID | 좌표 시스템 |
| --- | --- |
| 4326 | 위도 |
| 3857 | World Mercator |

위도/경도를 사용하는 경우 위도는 Y 좌표이고 경도는 X 좌표입니다. 좌표가 X,Y 쌍으로 나열되므로 값은 실제로 위도 순서로 표시됩니다.

다음은 위도/경도 좌표를 사용하는 점 형상의 예입니다.

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

다음은 위도/경도 좌표를 사용하는 다각형 형상의 예입니다.

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### 목표

이 실습에서는 다음을 수행합니다.

*   형상 열이 있는 테이블 작성
*   형상 채우기
*   공간 메타데이터 및 인덱스 생성

### 필요 조건

워크샵 소개에 설명된 대로 Oracle Database 및 SQL Client에 액세스해야 합니다. 없는 경우 Oracle Cloud 계정, Autonomous Database 및 SQL Developer Web의 섹션으로 돌아갑니다.

## 작업 1: 좌표를 사용하여 테이블 생성

먼저 위도, 경도 좌표로 테이블을 생성합니다. 이것은 GPS에서 좌표, 지오코딩 거리 주소 또는 IP 주소와 같은 공간 데이터를 생성하는 일반적인 시작점입니다.

지침 및 스크린샷은 SQL Developer Web을 참조하지만 다른 SQL 클라이언트에도 동일한 단계가 적용됩니다.

1.  [여기](files/create-sample-data.sql)에서 SQL 스크립트를 다운로드하십시오.
    
2.  SQL Developer Web에서 스크립트 복사/붙여넣기/실행 ![이미지 대체 텍스트](images/run-script-1.png)
    
3.  BRANCHES 및 WAREHOUSES 테이블을 보려면 목록을 새로 고치십시오.
    
    ![이미지 대체 텍스트](images/refresh-tables-1.png)
    

## 작업 2: 좌표에서 형상 작성

도면을 SQL로 채울 수 있습니다. 예를 들어 위도 및 경도 열에 따라 점 지오메트리의 좌표를 지정하면 됩니다.

1.  형상 열 추가:
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  형상 열을 채웁니다.
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## 작업 3: 다각형으로 테이블 작성

선과 다각형은 같은 방법으로 작성할 수 있습니다. 점 형상에는 하나의 좌표가 필요하지만 선과 다각형에는 형상을 정의하는 모든 좌표가 필요합니다. 이 경우 다각형을 저장할 테이블을 만듭니다.

1.  테이블 생성 및 행 삽입
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  테이블 목록을 새로 고쳐 COASTAL\_ZONE 테이블을 확인합니다. ![이미지 대체 텍스트](images/refresh-tables-2.png)
    

## 작업 4: 공간 메타데이터 및 인덱스 추가

Oracle Database는 고성능 공간 작업을 위한 고유 공간 인덱스를 제공합니다. 샘플 데이터가 너무 작아서 공간 인덱스가 실제로 필요하지 않습니다. 하지만 다음 단계는 일반적인 운영 데이터 볼륨에 중요하므로 수행합니다. 공간 인덱스에는 인덱스화되는 형상에 대한 메타데이터 행이 필요합니다. 이 메타데이터를 생성한 다음 공간 인덱스를 생성합니다.

1.  공간 메타데이터 추가:
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  공간 인덱스 생성:
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    인덱스가 생성된 후 테이블 리스트를 Refresh합니다. 이름이 MDRT\_로 시작하는 3개의 테이블이 표시됩니다. 공간 인덱스의 아티팩트이며 Oracle Database에서 자동으로 관리됩니다. 이러한 테이블을 수동으로 조작해서는 안됩니다. ![이미지 대체 텍스트](images/refresh-tables-3.png)
    
    우리의 샘플 데이터는 이제 공간 쿼리를 위해 준비되어 있습니다.
    
    이제 다음 실습을 진행할 수 있습니다.
    
    이 실습을 복원하고 생성된 항목을 제거해야 하는 경우 다음을 실행합니다.
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## 자세히 알아보기

*   \[공간 제품 포털\] (https://oracle.com/goto/spatial)
*   [공간 문서](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [공간 블로그](https://blogs.oracle.com/oraclespatial/)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - Kamryn Vinson, 2020년 11월