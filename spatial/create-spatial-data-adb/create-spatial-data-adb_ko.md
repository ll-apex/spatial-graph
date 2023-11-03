# 샘플 데이터 생성

## 소개

공간 데이터는 일반적으로 좌표나 위치 이름이 있는 파일 및 데이터를 고유 공간 형식으로 저장하는 파일에서 가져옵니다. 이 실습에서는 이러한 파일에서 공간 데이터를 로드 및 구성하고 지도에서 내용을 미리 봅니다.

예상 시간: 20분

### 목표

이 실습에서는 다음을 수행합니다.

*   Oracle Database의 공간 데이터 관리에 대해 알아보기
*   공통 파일 형식에서 Oracle Database의 공간 데이터 준비

### 필요 조건

*   실습 2 완료: SQL Worksheet를 사용하여 ADB에 연결

### 공간 데이터 정보

Oracle Database는 공간 데이터(포인트, 선, 다각형)를 SDO\_GEOMETRY이라는 고유 데이터 유형에 저장합니다. Oracle Database는 또한 고성능 공간 작업을 위한 고유 공간 인덱스를 제공합니다. 이 공간 인덱스는 공간 데이터를 저장하는 각 테이블 및 형상 열에 대해 입력된 공간 메타데이터에 의존합니다. 공간 데이터가 채워지고 인덱스화되면 강력한 API를 사용하여 공간 분석, 계산 및 처리를 수행할 수 있습니다.

SDO\_GEOMETRY 유형의 일반 형식은 다음과 같습니다.

        SDO_GEOMETRY( 
            [geometry type]              -- ID for points/lines/polygons
            , [coordinate system]        -- ID of coordinate system
            , [point coordinate]         -- used for points only
            , [line/polygon info]        -- used for lines/polygons only
            , [line/polygon coordinates] -- used for lines/polygons only
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

위도 및 경도를 사용하는 경우 위도는 Y 좌표이고 경도는 X 좌표입니다. 좌표가 X,Y 쌍으로 나열되므로 SDO\_GEOMETRY 내의 값은 경도, 위도 순서여야 합니다.

다음 예는 경도, 위도 좌표가 있는 점 형상입니다.

        SDO_GEOMETRY( 
            2001                       -- 2D point
            , 4326                     -- Coordinate system
            , SDO_POINT_TYPE(
              -100.123, 20.456, NULL)  -- lon/lat values
            , NULL                     -- Not used for points
            , NULL                     -- Not used for points
        )
    

다음 예는 경도, 위도 좌표가 있는 다각형 형상입니다.

        SDO_GEOMETRY( 
            2003                     -- 2D polygon
            , 4326                   -- Coordinate system
            , NULL                   -- Only used for points
            , SDO_ELEM_INFO_ARRAY(
                      1, 1003, 1)    -- Signifies simple exterior polygon
            , SDO_ORDINATE_ARRAY(    -- lon/lat values
                  -98.789065,39.90973
                , -101.2522,39.639537
                , -99.84374,37.160316
                , -96.67987,35.460699
                , -94.21875,39.639537
                , -98.789025,39.90973
            )
        )
    

공간 데이터를 생성하기 위한 일반적인 워크플로우는 형상을 생성한 다음 최적의 성능을 위해 공간 인덱스를 생성하는 것입니다. 공간 인덱스를 생성하기 전에 공간 인덱스가 데이터 일관성을 보장하기 위해 사용하는 공간 메타 데이터 행이 삽입됩니다.

공간 메타 데이터는 다음과 같이 삽입됩니다.

        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
        [table name],
        [geometry column name],
        SDO_DIM_ARRAY(
          SDO_DIM_ELEMENT('X',[min x],[max x],[tolerance]),
          SDO_DIM_ELEMENT('Y',[min y],[max y],[tolerance])),
        [coordinate system id]   
        );
    

이 워크샵에서는 메타 데이터 삽입이 다음과 같이 되도록 경도, 위도 좌표로 작업합니다.

        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
        [table name],
        [geometry column name],
        SDO_DIM_ARRAY(
          SDO_DIM_ELEMENT('X', -180, 180, 0.005),
          SDO_DIM_ELEMENT('Y',-90, 90, 0.005)),
        4326 
        );
    

**포인트** 데이터의 경우 가장 일반적인 시나리오는 포인트 위치를 나타내는 좌표를 포함한 데이터로 시작하는 것입니다. 데이터를 구성하려면 새 형상 열(SDO\_GEOMETRY 유형의 열)을 작성 및 채우거나, 좌표에서 형상을 작성한 다음 해당 함수에 공간 색인을 작성하는 함수를 작성합니다. 두 옵션 모두 연관된 사용 사례가 있으며 이 두 가지 방법을 모두 사용하여 익숙해집니다.

**선** 및 **다각형**의 경우 일반적인 형식(예: GeoJSON)에서 로드하고 형상 열이 있는 테이블로 변환하는 것이 가장 일반적입니다. GeoJSON는 개발자 통합을 위한 가장 일반적인 형식이며 이 워크샵에 포함되거나 GeoJSON으로의 변환이 포함되어 있으므로 다음과 같은 간단한 소개를 제공합니다.

[https://geojson.org/](https://geojson.org/)에 설명된 대로 "GeoJSON는 다양한 지리적 데이터 구조를 인코딩하는 형식입니다." 지리 공간 산업은 GeoJSON를 디팩토 표준으로 받아들였으며, 거의 모든 공간 개발자 플랫폼, 라이브러리 및 툴킷에서 사용할 수 있습니다. 따라서 GeoJSON의 처리는 상호 운용성을 위해 중요합니다.

GeoJSON 문서는 일반적으로 최상위 레벨 구조가 있는 JSON 문서입니다.

      {
          "type": "FeatureCollection",
          "features": [
             ... array of GeoJSON features ... 
          ]
       }
    

GeoJSON 기능의 형식은 다음과 같습니다.

![GeoJSON](images/geojson-00.png)

Oracle Spatial에는 기본 공간 유형(SDO\_GEOMETRY)과 GeoJSON 지오메트리 형식 간에 변환하는 내장 함수가 포함되어 있습니다. GeoJSON 형상은 비공간 속성 및 배열 구조를 포함하여 더 넓은 GeoJSON 문서 형식 내에 포함됩니다.

이 실습에서는 GeoJSON 문서의 데이터를 SDO\_GEOMETRY 열이 있는 테이블로 로드합니다. 이후 실습에서는 SDO\_GEOMETRY 열이 있는 테이블에서 GeoJSON를 생성합니다.

**주:** 이 워크샵에서는 Autonomous Database 툴 및 SQL을 사용하여 GeoJSON 문서를 로드하고 구성합니다. 이는 Autonomous Database의 기본 JSON 기능을 이해하는 데 유용합니다. 그러나 코딩이 필요 없는 Oracle Spatial에 GeoJSON를 로드하는 데 사용할 수 있는 간단한 도구 및 유틸리티도 있습니다. 예: [Oracle Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html) 및 [GDAL](https://gdal.org/). 가장 적절한 방법은 시나리오에 따라 다릅니다.

### 목표

이 실습에서는 다음을 수행합니다.

*   STORES, WAREHOUSES, REGIONS 및 TORNADO\_PATHS용 파일을 다운로드합니다.
*   지도에서 콘텐츠 보기
*   데이터베이스 테이블로 파일 로드
*   공간 분석을 위한 테이블 구성

### 필요 조건

Oracle Autonomous Database 및 Database Actions

## 작업 1: 파일에서 데이터 로드

먼저 점 형상을 작성하는 데 사용할 좌표를 포함하는 CSV 파일에서 웨어하우스 및 저장소의 데이터를 로드합니다. 그런 다음 GeoJSON 문서에서 지역 및 토네이도 경로에 대한 데이터를 로드합니다. GeoJSON 파일이 로드되어 형상이 있는 테이블로 변환됩니다.

1.  **마우스 오른쪽 단추 누르기 > 다른 이름으로 링크 저장...**을 사용하여 다음 파일을 다운로드합니다.
    
    ![공간 데이터 준비](images/save-link-as.png)
    
    *   [stores.csv](files/stores.csv)
    *   [warehouses.csv](files/warehouses.csv)
    *   [regions.geojson](files/regions.geojson)
    *   [tornado\_paths.geojson](files/tornado_paths.geojson)
2.  그런 다음 파일 시스템 탐색기를 다운로드한 파일로 이동합니다.
    
    ![공간 데이터 준비](images/create-data-00.png)
    
3.  먼저 지도에서 데이터를 확인합니다.
    
    참고: Oracle Spatial Studio는 셀프 서비스(코드 없음) 공간 데이터 로드, 구성, 분석 및 맵 시각화를 위한 웹 툴입니다. Cloud Marketplace에서 배포할 수 있는 별도의 웹 애플리케이션입니다. 이 워크샵에서는 SQL 레벨에서 Spatial 작업에만 초점을 맞추고 있으므로 Spatial Studio는 사용되지 않습니다. 대신 공용 웹 사이트를 사용하여 데이터를 봅니다.
    
    [http://geojson.io](http://geojson.io)는 작은 공간 데이터 세트를 보고 수동으로 만들고 편집하기 위한 웹 사이트입니다. 이 사이트를 사용하여 경도, 위도 열을 포함하는 파일뿐 아니라 GeoJSON 파일의 데이터를 렌더링할 수 있습니다. 다운로드한 데이터를 지도에서 보려면 [여기](http://geojson.io)를 클릭하여 새 브라우저 탭에서 geojson.io를 여십시오. 그런 다음 **warehouses.csv**를 맵으로 끌어 놓습니다.
    
    ![데이터 보기](images/create-data-00a.png)
    
    CSV 데이터는 오른쪽에 표시된 대로 GeoJSON로 변환되고 맵에 렌더링됩니다.
    
    ![공간 데이터 준비](images/create-data-00b.png)
    
    상단에서 **새로 만들기**를 눌러 새 탭에서 새 맵을 엽니다. **stores.csv**을 맵으로 끌어 놓습니다.
    
    ![공간 데이터 준비](images/create-data-00c.png)
    
    ![공간 데이터 준비](images/create-data-00d.png)
    
    **regions.geojson**에 대해 이 과정을 반복합니다.
    
    ![공간 데이터 준비](images/create-data-00e.png)
    
    **tornardo\_paths.geojson**에 대해 이 과정을 반복합니다.
    
    ![공간 데이터 준비](images/create-data-00f.png)
    

공간 분석을 로드, 구성 및 수행할 데이터입니다. 지도를 검토한 후 geojson.io 탭을 닫을 수 있습니다.

1.  그런 다음 파일을 데이터베이스 테이블로 로드합니다. Database Actions에서 왼쪽 위에 있는 기본 햄버거 아이콘을 누른 후 **Data Load**를 누릅니다.

![공간 데이터 준비](images/create-data-01.png)

2.  기본값(LOAD DATA 및 LOCAL FILE)을 적용하고 **Next**를 누릅니다.

![공간 데이터 준비](images/create-data-02.png)

3.  다운로드한 파일 4개를 모두 선택한 다음 \[데이터 로드\] 페이지로 끌어 놓습니다.

![공간 데이터 준비](images/create-data-03.png)

4.  이제 로드할 4개의 파일이 나열됩니다. tornado\_paths.geojson에 대한 작업 메뉴 아이콘을 누르고 **설정**을 선택합니다.

![공간 데이터 준비](images/create-data-04.png)

5.  기본적으로 테이블은 입력 파일과 동일한 이름으로 생성됩니다. 이것은 창고와 창고에 적합합니다. 그러나 GeoJSON에서 변환하여 데이터 로드 후 REGIONS 및 TORNADO\_PATHS 테이블을 생성합니다. 따라서 기본 이름을 대체해야 합니다. 대상 테이블 이름을 **TORNADO\_PATHS\_GEOJSON**로 변경합니다.

![공간 데이터 준비](images/create-data-05.png)

6.  GeoJSON 파일의 최상위 레벨 키에 해당하는 2개의 열이 생성되는지 확인합니다. 그런 다음 **닫기**를 누릅니다.

![공간 데이터 준비](images/create-data-06.png)

7.  regions.geojson에 대해 이 과정을 반복합니다. 작업 메뉴 아이콘을 누른 다음 **설정**을 누릅니다.

![공간 데이터 준비](images/create-data-07.png)

8.  대상 테이블 이름을 **REGIONS\_GEOJSON**로 업데이트합니다. 다른 GeoJSON 파일과 동일한 구조가 생성되고 최상위 레벨 키에 대한 열이 포함된 것을 확인합니다. **닫기**를 누릅니다.

![공간 데이터 준비](images/create-data-08.png)

9.  **시작**을 눌러 데이터 로드 시작

![공간 데이터 준비](images/create-data-09.png)

10.  확인 팝업 메시지가 표시되면 **Run**을 누릅니다.

![공간 데이터 준비](images/create-data-10.png)

11.  4개 파일이 모두 로드될 때까지 기다렸다가 **완료**를 누릅니다.

![공간 데이터 준비](images/create-data-11.png)

12.  왼쪽 위에 있는 기본 햄버거 아이콘을 누른 다음 **SQL**을 선택합니다.

![공간 데이터 준비](images/create-data-12.png)

13.  네 개의 테이블이 모두 생성되었는지 확인합니다.

![공간 데이터 준비](images/create-data-17.png)

14.  GeoJSON 콘텐츠 작업을 준비하려면 JSON으로 정의하는 FEATURES 열에 check 제약 조건을 추가합니다.
    
        <copy> 
         ALTER TABLE REGIONS_GEOJSON 
             ADD CHECK (FEATURES IS JSON);
        
         ALTER TABLE TORNADO_PATHS_GEOJSON 
             ADD CHECK (FEATURES IS JSON);
         </copy>
         ```
        
        

![공간 데이터 준비](images/create-data-17b.png)

이제 공간에 대해 테이블을 구성할 준비가 되었습니다.

## 작업 2: 지오메트리 열을 사용하여 웨어하우스 테이블 구성

다음으로 좌표 열에서 형상 열을 생성하여 공간에 대한 WAREHOUSES 테이블을 구성합니다.

1.  먼저 도면 열(SDO\_GEOMETRY 유형의 열)을 추가합니다.
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
            GEOMETRY SDO_GEOMETRY
            );
        </copy>
        
    
    ![공간 데이터 준비](images/create-data-18.png)
    
2.  그런 다음 행의 형상 열을 유효한 좌표(이 경우 모든 행)로 채웁니다.
    
        <copy> 
        UPDATE WAREHOUSES
        SET GEOMETRY = SDO_GEOMETRY(
                         2001,
                         4326,
                         SDO_POINT_TYPE(LONGITUDE, LATITUDE, NULL),
                         NULL, NULL)
        WHERE LONGITUDE IS NOT NULL 
        AND LONGITUDE BETWEEN -180 AND 180
        AND LATITUDE IS NOT NULL 
        AND LATITUDE BETWEEN -90 AND 90 ;
        </copy>
        

![공간 데이터 준비](images/create-data-19.png)

3.  공간 인덱스를 생성하기 전에 공간 메타데이터 행을 삽입해야 합니다. 모든 사용자는 공간 메타데이터에 대해 USER\_SDO\_GEOM\_METADATA이라는 업데이트 가능한 뷰를 가집니다. 이 뷰는 전체 데이터베이스 Instance에 대한 공간 메타 데이터를 저장하는 중앙화된 테이블에 대한 유저 뷰입니다. 공간 메타데이터는 인덱스화할 모든 형상 열의 좌표계 식별자(경도/위도는 여러 좌표계 중 하나임) 및 치수(2D, 3D 등)를 추적합니다. 이러한 항목은 인덱스화된 형상 열의 모든 데이터에 대해 일관성이 있어야 하므로 인덱스 생성은 값을 읽고 불일치를 거부하여 인덱스 무결성을 적용합니다.
    
    다음을 실행하여 WAREHOUSES 테이블에 대한 공간 메타 데이터를 삽입합니다.
    
        <copy> 
         INSERT INTO USER_SDO_GEOM_METADATA VALUES (
          'WAREHOUSES',  -- table name
          'GEOMETRY',    -- geometry column name
          SDO_DIM_ARRAY(
            SDO_DIM_ELEMENT('X', -180, 180, 0.005),
            SDO_DIM_ELEMENT('Y', -90, 90, 0.005)),
           4326           -- indicates longitude/latitude coordinates
         );
        </copy>
        

![공간 데이터 준비](images/create-data-20.png)

4.  마지막으로 WAREHOUSES 테이블에 대한 공간 인덱스를 생성합니다.
    
        <copy> 
          CREATE INDEX WAREHOUSES_SIDX ON
              WAREHOUSES (
                  GEOMETRY
              )
                  INDEXTYPE IS MDSYS.SPATIAL_INDEX_V2;
        </copy>
        
    
    ![공간 데이터 준비](images/create-data-21.png)
    
    **참고:** 공간 인덱스 생성 명령문이 실패할 경우(예: 이전 단계가 올바르게 수행되지 않았을 경우) 재시도하기 전에 일부 인덱스 아티팩트가 생성되었을 수 있으므로 인덱스를 삭제해야 합니다. 예를 들어, 위의 공간 인덱스 생성 명령문이 실패할 경우 재시도하기 전에 "DROP INDEX WAREHOUSES\_SIDX;"을 실행해야 합니다.
    
5.  공간 인덱스를 생성한 후 테이블 목록을 새로 고칩니다. 공간 인덱스를 생성하면 이름이 **MDRT\_xxxx$**인 특수 시스템 관리 테이블이 자동으로 생성됩니다. 이러한 테이블은 공간 인덱스를 지원하기 위해 Spatial에 의해 완전히 관리되므로 수동으로 삭제해서는 안됩니다. 데이터베이스 사용자의 경우 무시해야 합니다.
    

![공간 데이터 준비](images/create-data-21a.png)

## 작업 3: 함수 기반 공간 인덱스를 사용하여 stores 테이블 구성

다음 작업은 공간에 대해 STORES 테이블을 구성하는 것입니다. 이전 단계를 반복하여 새 형상 열을 작성하고 색인화할 수 있습니다. 대신 "함수 기반 공간 인덱스"를 생성합니다. 함수 기반 공간 인덱스를 사용하면 함수에서 반환된 형상을 인덱스화합니다. 이 접근 방식의 이점은 새 형상 열을 추가할 필요가 없다는 것입니다. 열을 추가하는 것이 비실용적이거나 바람직하지 않은 시나리오의 경우 이 방법이 선호됩니다. 자세한 내용은 [여기](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/extending-spatial-indexing.html#GUID-CFB6B6DB-4B97-43D1-86A1-21C1BA853089)에서 확인할 수 있습니다.

1.  첫번째 단계는 좌표를 받아들이고 형상(즉, SDO\_GEOMETRY 값)을 반환하는 일반 함수를 생성하는 것입니다. 함수에는 유효한 입력 좌표에 대해서만 결과가 반환되도록 하는 기준이 포함됩니다.
    
        <copy>
        CREATE OR REPLACE FUNCTION GET_GEOMETRY (
              IN_LONGITUDE NUMBER,
              IN_LATITUDE  NUMBER
          ) RETURN SDO_GEOMETRY
              DETERMINISTIC PARALLEL_ENABLE
          IS
          BEGIN
           IF (IN_LONGITUDE IS NOT NULL 
              AND IN_LONGITUDE BETWEEN -180 AND 180
              AND IN_LATITUDE IS NOT NULL 
              AND IN_LATITUDE BETWEEN -90 AND 90)
           THEN
            RETURN 
              SDO_GEOMETRY(
                2001, 
                4326, 
                SDO_POINT_TYPE(IN_LONGITUDE, IN_LATITUDE, NULL), 
                NULL, NULL);
            ELSE RETURN NULL;
            END IF;
          END;
          /
        </copy>
        
    
    ![공간 데이터 준비](images/create-data-22.png)
    
2.  그런 다음 STORES 테이블을 사용하여 함수를 테스트합니다. SQL Worksheet는 질의 결과에 SDO\_GEOMETRY와 같은 객체 유형을 표시하지 않으므로 결과가 **\[object Object\]**로 표시됩니다.
    
        <copy>
          SELECT
              GET_GEOMETRY(LONGITUDE, LATITUDE)
          FROM
              STORES
          WHERE 
               ROWNUM<10;
        </copy>
        
    
    ![공간 데이터 준비](images/create-data-22b.png)
    
3.  SQL Worksheet는 query 결과에 SDO\_GEOMETRY와 같은 객체 유형을 표시하지 않으므로 내장 함수 내의 함수를 호출하여 결과를 GeoJSON 문자열로 변환합니다.
    
        <copy>
          SELECT
              SDO_UTIL.TO_GEOJSON(
                  GET_GEOMETRY(LONGITUDE, LATITUDE))
          FROM
              STORES
          WHERE 
               ROWNUM<10;
        </copy>
        
    
    ![공간 데이터 준비](images/create-data-23.png)
    

STORES 테이블에서 새 형상 열을 만들고 인덱스화하는 대신 STORES 테이블에 대해 GET\_GEOMETRY 함수에서 반환된 값에 대한 인덱스를 만듭니다.

3.  공간 인덱스를 생성하기 전에 공간 메타데이터 행이 삽입됩니다. 함수 기반 공간 인덱스의 경우 지오메트리 열 이름 대신 함수 호출을 삽입합니다. GET\_GEOMETRY 함수를 사용하여 STORES 테이블에 대한 공간 메타 데이터를 삽입합니다. 함수 앞에 소유자 이름을 추가해야 합니다(이 경우 ADMIN).
    
        <copy>
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
         'STORES',  -- table name
         'ADMIN.GET_GEOMETRY(LONGITUDE,LATITUDE)', -- function returning geometry
         SDO_DIM_ARRAY(
          SDO_DIM_ELEMENT('X', -180, 180, 0.005),
          SDO_DIM_ELEMENT('Y', -90, 90, 0.005)),
         4326  -- indicates longitude/latitude coordinates
        );
        </copy>
        

![공간 데이터 준비](images/create-data-24.png)

4.  마지막으로 공간 인덱스를 생성합니다. 함수 기반 공간 인덱스의 경우 인덱스화되는 "열"은 실제로 GET\_GEOMETRY 함수 호출입니다.
    
        <copy>
        CREATE INDEX STORES_SIDX ON
          STORES (
              GET_GEOMETRY(LONGITUDE,LATITUDE)
          )
              INDEXTYPE IS MDSYS.SPATIAL_INDEX_V2;
        </copy>
        

![공간 데이터 준비](images/create-data-25.png)

## 작업 4: GeoJSON 문서에서 영역 테이블 생성

다음으로 GeoJSON 형식의 영역을 형상 열이 있는 테이블로 변환합니다. REGIONS\_GEOJSON의 내용을 확인하여 시작합니다. 앞서 설명한 대로 SQL Worksheet에서 JSON을 로드하면 문서의 최상위 키에 대한 열이 포함된 테이블이 생성됩니다. **type** 및 **features**인 GeoJSON의 경우 **features** 값 위로 마우스를 가져가면 기능 배열의 팝업이 표시됩니다. 피쳐는 여러 좌표를 가진 다각형이므로 배열에서 첫 번째 피쳐의 일부만 표시됩니다.

     <copy>
       SELECT *
       FROM REGIONS_GEOJSON;
     </copy>
    

![공간 데이터 준비](images/create-data-26.png)

Oracle Autonomous Database는 SQL을 통해 JSON 데이터 작업을 위한 강력한 기능을 제공합니다. 예를 들어, 다음 명령문을 실행하여 피쳐 배열의 항목 수(즉, 영역 수)를 확인합니다.

     <copy>
       SELECT 
         JSON_VALUE(features, '$.size()')
       FROM 
          REGIONS_GEOJSON;
     </copy>
    

![공간 데이터 준비](images/create-data-27.png)

배열에서 첫번째 피쳐의 속성(즉, 속성)을 반환하려면 다음을 실행합니다. 결과는 키/값 쌍이며, 이 경우 하나만 발생합니다.

    <copy>
    SELECT 
       x.features.properties[0]
    FROM
       REGIONS_GEOJSON x;
    </copy>
    

![공간 데이터 준비](images/create-data-28.png)

배열에서 첫 번째 피쳐의 형상을 SDO\_GEOMETRY로 되돌리려면 다음을 실행합니다. 앞에서 설명한 것처럼 SQL Worksheet는 SDO\_GEOMETRY와 같은 객체 유형 값을 표시하지 않으므로 \[object Object\]로 결과가 표시됩니다.

     <copy>
       SELECT 
         json_value(features,'$[0].geometry' RETURNING SDO_GEOMETRY)
       FROM
           REGIONS_GEOJSON;
     </copy>
    

![공간 데이터 준비](images/create-data-29.png)

SQL Worksheet에서 형상을 표시하려면 Spatial의 기능을 사용하여 SDO\_GEOMETRY를 다른 공통 문자열 형식으로 변환합니다. 공간은 SQL 변환 함수와 SDO\_GEOMETRY 객체 유형 메소드를 모두 사용하여 형식 변환을 지원합니다. 다음을 실행하여 SDO\_GEOMETRY 메소드를 사용하여 WKT(Well Known Text) 형식의 첫 번째 피쳐 형상을 반환합니다.

     <copy>
       SELECT 
         json_value(features,'$[0].geometry' RETURNING SDO_GEOMETRY).Get_WKT()
       FROM
           REGIONS_GEOJSON;
     </copy>
    

![공간 데이터 준비](images/create-data-30.png)

JSON\_TABLE 테이블 함수는 JSON 배열의 항목을 행으로 반환합니다. 이것이 바로 피쳐 배열을 테이블로 변환하는 데 필요한 것입니다. 다음을 실행하여 피쳐 배열의 내용을 행으로 반환합니다. COLUMNS에 대한 인수는 여기서 REGION인 속성 키와 형상입니다.

     <copy>
       SELECT
           JT.*
       FROM
           REGIONS_GEOJSON A,
           JSON_TABLE ( A.FEATURES, '$[*]'
                   COLUMNS (
                       REGION VARCHAR ( 30 ) PATH '$.properties.REGION',
                       GEOMETRY SDO_GEOMETRY PATH '$.geometry'
                   )
               )
           AS JT;
     </copy>
    

![공간 데이터 준비](images/create-data-31.png)

이전 query 결과에서 REGIONS 테이블을 생성합니다.

    <copy>
    
      CREATE TABLE REGIONS AS (
          SELECT
              JT.*
          FROM
              REGIONS_GEOJSON A,
              JSON_TABLE ( A.FEATURES, '$[*]'
                  COLUMNS (
                     REGION VARCHAR ( 30 ) PATH '$.properties.REGION',
                     GEOMETRY SDO_GEOMETRY PATH '$.geometry'
              ))
                AS JT
            );
    
    </copy>
    

![공간 데이터 준비](images/create-data-32.png)

REGIONS에 대한 공간 메타데이터를 삽입합니다.

    <copy>
      INSERT INTO USER_SDO_GEOM_METADATA VALUES (
       'REGIONS',
       'GEOMETRY',
       SDO_DIM_ARRAY(
        SDO_DIM_ELEMENT('X', -180, 180, 0.005),
        SDO_DIM_ELEMENT('Y', -90, 90, 0.005)),
       4326
        );
    </copy>
    

![공간 데이터 준비](images/create-data-33.png)

REGIONS에 대한 공간 인덱스를 생성합니다.

    <copy>
      CREATE INDEX REGIONS_SIDX ON
            REGIONS (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX_V2;
    </copy>
    

![공간 데이터 준비](images/create-data-34.png)

## 작업 5: GeoJSON 문서에서 토네이도 경로 테이블 생성

이전 작업 단계를 반복하여 TORNADO\_PATHS\_GEOJSON를 변환합니다. 먼저 기능 수를 가져옵니다.

    <copy>
      SELECT
          JSON_VALUE(FEATURES, '$.size()')
      FROM
          TORNADO_PATHS_GEOJSON;
    </copy>
    

![공간 데이터 준비](images/create-data-35.png)

그런 다음 첫 번째 피쳐의 특성을 가져옵니다. 이번에는 여러 가지가 있습니다.

    <copy>
      SELECT
          x.features.properties[0]
      FROM
          TORNADO_PATHS_GEOJSON x;
    </copy>
    

![공간 데이터 준비](images/create-data-36.png)

다음 명령을 실행하여 첫 번째 피쳐의 특성 값, 형상 및 형상을 WKT로 확인합니다.

    <copy>
      SELECT 
          json_value(features,'$[0].properties.KEY'),
          json_value(features,'$[0].properties.YR'),
          json_value(features,'$[0].properties.LOSS'),
          json_value(features,'$[0].geometry' RETURNING SDO_GEOMETRY),
          json_value(features,'$[0].geometry' RETURNING SDO_GEOMETRY).Get_WKT()
        FROM
            TORNADO_PATHS_GEOJSON;
    </copy>
    

![공간 데이터 준비](images/create-data-37.png)

JSON\_TABLE 함수를 사용하여 콘텐츠를 행으로 반환합니다.

    <copy>
      SELECT
            JT.*
        FROM
            TORNADO_PATHS_GEOJSON A,
            JSON_TABLE ( A.FEATURES, '$[*]'
                    COLUMNS (
                        KEY      NUMBER PATH '$.properties.KEY',
                        YR       NUMBER PATH '$.properties.YR',
                        LOSS     NUMBER PATH '$.properties.LOSS',
                        GEOMETRY SDO_GEOMETRY PATH '$.geometry'
                    )
                )
            AS JT;
    </copy>
    

![공간 데이터 준비](images/create-data-38.png)

이전 query 결과에서 TORNADO\_PATHS 테이블을 생성합니다.

    <copy>
      CREATE TABLE TORNADO_PATHS AS
      SELECT
            JT.*
        FROM
            TORNADO_PATHS_GEOJSON A,
            JSON_TABLE ( A.FEATURES, '$[*]'
                    COLUMNS (
                        KEY      NUMBER PATH '$.properties.KEY',
                        YR       NUMBER PATH '$.properties.YR',
                        LOSS     NUMBER PATH '$.properties.LOSS',
                        GEOMETRY SDO_GEOMETRY PATH '$.geometry'
                    )
                )
            AS JT;
    </copy>
    

![공간 데이터 준비](images/create-data-39.png)

TORNADO\_PATHS에 대한 공간 메타데이터를 삽입합니다.

    <copy>
      INSERT INTO USER_SDO_GEOM_METADATA VALUES (
       'TORNADO_PATHS',
       'GEOMETRY',
       SDO_DIM_ARRAY(
        SDO_DIM_ELEMENT('X', -180, 180, 0.005),
        SDO_DIM_ELEMENT('Y', -90, 90, 0.005)),
      4326
        );
    </copy>
    

![공간 데이터 준비](images/create-data-40.png)

TORNADO\_PATHS에 대한 공간 인덱스를 생성합니다.

    <copy>
      CREATE INDEX TORNADO_PATHS_SIDX ON
            TORNADO_PATHS (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX_V2;
    </copy>
    

![공간 데이터 준비](images/create-data-41.png)

이제 GeoJSON에서 변환이 완료되었으므로 업로드된 GeoJSON 문서를 저장하는 테이블을 삭제할 수 있습니다. 그런 다음 테이블 목록을 새로 고칩니다.

    <copy>
    DROP TABLE REGIONS_GEOJSON;
    DROP TABLE TORNADO_PATHS_GEOJSON;
    </copy>
    

![공간 데이터 준비](images/create-data-42.png)

이제 모든 데이터가 로드되고 공간 분석을 위해 준비됩니다.

이제 **다음 실습을 진행하십시오**.

## 자세히 알아보기

*   [공간 제품 포털](https://oracle.com/goto/spatial)
*   [공간 문서](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Oracle Database Insider에 대한 공간 블로그 게시물](https://blogs.oracle.com/database/category/db-spatial)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **기여자** - Karin Patenge, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 3월