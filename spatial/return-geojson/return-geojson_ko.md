# GeoJSON를 반환합니다.

## 소개

GeoJSON는 개발자 공간 데이터 통합에 선호되는 형식입니다. 거의 모든 공간 및 매핑 클라이언트 라이브러리는 GeoJSON를 사용합니다. 따라서 Spatial의 콘텐츠 및 결과를 GeoJSON로 반환하는 것이 중요합니다. GeoJSON에 대한 설명은 **랩 3 - 소개**를 참조하십시오. 이 실습에서는 형상이 있는 테이블에서 GeoJSON 문서를 생성합니다. 실제로 ADB에서 GeoJSON를 생성하는 값은 GeoJSON를 다양한 클라이언트에 반환한 다음 프레임워크에서 콘텐츠를 전달하는 것입니다. 예를 들어, GeoJSON를 반환하는 SQL 및 PL/SQL은 ORDS(Oracle REST Data Services)에서 GeoJSON 문서를 반환하는 위치 기반 REST API를 게시하고, Oracle Data Science는 GeoJSON를 기본적으로 지원하는 인기 있는 오픈 소스 공간 ML 라이브러리와 결합할 수 있습니다.

예상 시간: 15분

실습 과정을 간단히 살펴보려면 아래 비디오를 시청하십시오. [공간 데이터 준비](videohub:1_bj22bt29)

### 목표

이 실습에서는 다음을 수행합니다.

*   Oracle Autonomous Database에서 네이티브 JSON 핸들링 살펴보기
*   기하학이 있는 테이블을 GeoJSON 문서로 변환하여 개발자 통합 지원

### 필요 조건

*   실습 3: 공간 데이터 준비

## 작업 1: 질의 결과에서 GeoJSON 문서 생성

1.  먼저 GeoJSON 형식과 같이 토네이도 경로 형상을 반환합니다.
    
        <copy> 
        SELECT
            SDO_UTIL.TO_GEOJSON(GEOMETRY)
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON를 반환합니다.](images/return-geojson-01.png)
    
2.  그런 다음 필요에 따라 GeoJSON 문서를 작성하는 데 JSON\_ARRAYAGG( ) 함수를 사용하여 GeoJSON 형상의 행을 배열로 변환합니다. 복잡한 다각형과 같이 좌표가 많은 형상으로 인해 문자열이 매우 길어질 수 있으므로 필요한 **반복 CLOB** 인수를 확인합니다. 결과 위로 마우스를 가져가면 JSON 배열이 표시됩니다.
    
        <copy> 
        SELECT
            JSON_ARRAYAGG(
                SDO_UTIL.TO_GEOJSON(GEOMETRY) 
                FORMAT JSON RETURNING CLOB )
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON를 반환합니다.](images/return-geojson-02.png)
    
3.  피쳐 배열에는 형상과 특성이 모두 포함되어야 합니다. 다음 질의를 실행하여 피쳐 배열의 요소를 구성합니다. 결과 위로 마우스를 가져가면 이제 등록 정보가 포함된 JSON 배열이 표시됩니다.
    
        <copy> 
        SELECT
            '{"type": "Feature", "properties": {'
            || '"key":"'|| KEY
            ||'","yr":"'|| YR
            ||'","loss":"'|| LOSS
            ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
            ||'}' AS features
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON를 반환합니다.](images/return-geojson-03.png)
    
4.  JSON\_ARRAYAGG( )를 사용하여 이전 결과를 배열로 컴파일합니다. 이제 실제 피쳐 배열입니다. 결과 위로 마우스를 가져가면 결과 팝업이 표시됩니다.
    
        <copy> 
        SELECT
            JSON_ARRAYAGG( 
                '{"type": "Feature", "properties": {'
                || '"key":"'|| KEY
                ||'","yr":"'|| YR
                ||'","loss":"'|| LOSS
                ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
                ||'}' 
                FORMAT JSON RETURNING CLOB)   
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON를 반환합니다.](images/return-geojson-04.png)
    
5.  GeoJSON 문서 구성을 완료하려면 최상위 레벨 키 **유형** 및 **기능**과 닫는 중괄호를 포함합니다. 이제 완전한 GeoJSON 문서를 반환합니다. 결과 위로 마우스를 가져가면 결과 팝업이 표시됩니다.
    
        <copy> 
        SELECT
            '{"type": "FeatureCollection", "features":'
            || JSON_ARRAYAGG( 
                '{"type": "Feature", "properties": {'
                || '"key":"'|| KEY
                ||'","yr":"'|| YR
                ||'","loss":"'|| LOSS
                ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(GEOMETRY)
                ||'}' 
                FORMAT JSON RETURNING CLOB) 
            ||'}'
            AS GEOJSON
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        

![GeoJSON를 반환합니다.](images/return-geojson-05.png)

6.  결과 셀을 마우스 오른쪽 버튼으로 누르고 **복사**를 선택합니다.
    
    ![GeoJSON를 반환합니다.](images/return-geojson-06.png)
    
7.  렌더링하여 결과를 확인합니다. [여기](http://geojson.io)를 클릭하여 새 브라우저 탭에서 geojson.io를 여십시오. JSON 아래의 오른쪽 패널에서 콘텐츠를 지운 후(모두 선택 > 삭제) SQL Worksheet에서 복사된 GeoJSON에 붙여 넣습니다. 해당 등록 정보가 포함된 팝업을 보려면 토네이도 라인을 누릅니다.
    
    ![GeoJSON를 반환합니다.](images/return-geojson-07.png)
    
8.  결과를 조금 더 흥미롭게 만들려면 다음을 실행하여 토네이도 경로를 둘러싼 5마일 버퍼인 형상이 있는 GeoJSON 문서를 만듭니다. 버퍼 거리를 나타내는 새 특성 키가 추가됩니다. query를 실행한 다음 앞에서와 같이 결과를 복사합니다.
    
        <copy> 
        SELECT
           '{"type": "FeatureCollection", "features":'
           || JSON_ARRAYAGG( 
               '{"type": "Feature", "properties": {'
               || '"key":"'|| KEY
               ||'","yr":"'|| YR
               ||'","loss":"'|| LOSS
               ||'","buffer":"5 MI'
               ||'"}, "geometry":'|| SDO_UTIL.TO_GEOJSON(
                                      SDO_GEOM.SDO_BUFFER(GEOMETRY, 5, 1, 'unit=MILE'))
               ||'}' 
               FORMAT JSON RETURNING CLOB)   
           ||'}'
           AS GEOJSON
        FROM
            TORNADO_PATHS
        WHERE
            LOSS > 10000000;
        </copy>
        
    
    ![GeoJSON를 반환합니다.](images/return-geojson-08.png)
    
9.  새 geojson.io 탭을 열고 오른쪽에 있는 JSON 패널을 지운 다음 SQL Worksheet에서 복사된 결과를 붙여 넣습니다. 버퍼 형상을 관찰하고 하나를 눌러 추가된 버퍼 키를 포함한 속성이 있는 팝업을 확인합니다.
    
    ![GeoJSON를 반환합니다.](images/return-geojson-09.png)
    

실제 시나리오에서 생성한 GeoJSON는 Oracle REST Data Services와 함께 게시된 JDBC 또는 API를 통해 JavaScript 라이브러리 및 Python 노트북 매핑과 같은 클라이언트에 제공됩니다.

이제 **다음 실습을 진행하십시오**.

## 자세히 알아보기

*   [공간 제품 포털](https://oracle.com/goto/spatial)
*   [공간 문서](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Oracle Database Insider에 대한 공간 블로그 게시물](https://blogs.oracle.com/database/category/db-spatial)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - David Lapp, 2022년 9월