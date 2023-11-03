# 공간 질의

## 소개

이 실습에서는 Oracle Database의 기본 공간 쿼리를 안내합니다. 이전 연습에서 생성한 샘플 데이터를 사용하여 근접도와 포함을 기반으로 항목을 식별합니다.

예상 실험실 시간: 15분

### 공간 질의 정보

Oracle Database에는 공간 분석을 위한 강력한 함수 및 연산자 라이브러리가 포함되어 있습니다. 여기에는 공간 관계, 측정, 집계, 변환 등이 포함됩니다. 이러한 작업은 고유 SQL, PL/SQL, Java API 및 Oracle Database와 통신하는 기타 언어를 통해 액세스할 수 있습니다.

### 목표

이 실습에서는 다음을 수행합니다.

*   창고에 근접 관계가 있는 지점 식별
*   COASTAL\_ZONE에 대한 포함 및 근접 관계가 있는 브랜치 식별

### 필요 조건

*   이전 실습 완료, 샘플 공간 데이터 생성

## 공간 질의

Oracle Database의 공간 쿼리는 익숙한 다른 기존 쿼리와 비슷합니다. 유일한 차이점은 새로운 공간 함수와 연산자 집합입니다.

**댈러스 웨어하우스에서 가장 가까운 5개 지점 식별:**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![공간 질의 실행](images/query1.png) 노트:

*   `SDO_NN` 연산자는 Dallas Warehouse에 'n nearest' 분기를 반환합니다. 여기서 'n'은 `SDO_NUM_RES`에 지정된 값입니다. `SDO_NN`에 대한 첫번째 인수(위 예제의 경우 `B.GEOMETRY`)는 검색할 열입니다. 두번째 인수(위 예제의 `W.GEOMETRY`)는 가장 가까운 이웃을 찾을 위치입니다. 반환된 결과의 순서에 대해서는 가정할 필요가 없습니다. 예를 들어, 반환된 첫번째 행이 가장 가까운 행이 아닐 수 있습니다. 두 개 이상의 분기가 웨어하우스와 동일한 거리인 경우 이후 `SDO_NN` 호출 시 둘 중 하나가 반환될 수 있습니다.
*   `SDO_NUM_RES` 매개변수를 사용하는 경우 `WHERE` 절에 다른 조건이 사용되지 않습니다. `SDO_NUM_RES`는 근접성만 고려합니다. 예를 들어, `WHERE` 절에 기준을 추가한 경우 가장 가까운 5개 분기에 특정 우편 번호가 있고 가장 가까운 5개 분기의 4개에 다른 우편 번호가 있으면 위의 질의는 한 행을 반환합니다. 이 동작은 `SDO_NUM_RES` 매개변수에만 적용됩니다. 아래 질의에서는 추가 질의 기준 시나리오에 대한 대체 매개변수를 사용합니다.

**댈러스 웨어하우스에서 가장 가까운 5개 지점을 거리로 식별합니다.**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![공간 질의 실행](images/query2.png) 노트:

*   `SDO_NN_DISTANCE` 연산자는 `SDO_NN` 연산자에 대한 보조 연산자입니다. `SDO_NN` 연산자 내에서만 사용할 수 있습니다. 이 연산자의 인수는 `SDO_NN`의 마지막 인수로 지정된 숫자와 일치하는 숫자입니다. 이 예에서는 1입니다. 이 인수에는 숨겨진 의미가 없으며 단순히 태그입니다. `SDO_NN_DISTANCE()`를 지정할 경우 거리별로 결과를 정렬할 수 있으며 반환되는 첫번째 행이 가장 가까운 행인지 확인할 수 있습니다. 쿼리 중인 데이터가 경도와 위도로 저장되는 경우 `SDO_NN_DISTANCE`의 기본 단위는 미터입니다.
*   `SDO_NN` 연산자에는 `SDO_NN_DISTANCE`에서 반환된 측정 단위를 결정하는 `UNIT` 매개변수도 있습니다.
*   `ORDER BY DISTANCE` 절은 거리가 가장 짧은 거리를 먼저 사용하여 순서대로 반환되도록 합니다.

**댈러스 웨어하우스에 가장 가까운 5개의 WHOLESALE 지점 식별:**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![공간 질의 실행](images/query3.png) 노트:

*   `SDO_BATCH_SIZE`는 질의 성능에 영향을 줄 수 있는 조정 가능 매개변수입니다. `SDO_NN`는 한 번에 해당 거리 수를 내부적으로 계산합니다. 반환되는 초기 행 일괄 처리는 WHERE 절의 제약 조건을 충족하지 않을 수 있으므로 `SDO_BATCH_SIZE`로 지정된 행 수는 WHERE 절의 모든 제약 조건이 충족될 때까지 계속해서 반환됩니다. WHERE 절의 제약 조건을 만족할 가능성이 높은 행 수를 처음에 반환하는 `SDO_BATCH_SIZE`를 선택해야 합니다.
*   `SDO_NN` 연산자 내에서 사용되는 `UNIT` 매개변수는 `SDO_NN_DISTANCE` 매개변수의 측정 단위를 지정합니다. 기본 단위는 데이터와 연계된 측정 단위입니다. 경도 및 위도 데이터의 경우 기본값은 미터입니다.
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5`는 `WHERE` 절의 추가 제약 조건입니다. 5로 반환되는 결과 수를 제한하려면 rownum 절이 필요합니다.
*   `ORDER BY DISTANCE_KM` 절은 거리가 순서대로 반환되고 가장 짧은 거리가 먼저, 거리가 마일로 측정되도록 합니다.

**휴스턴 창고의 50km 이내 지점 식별:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![공간 질의 실행](images/query4.png) 노트:

*   `SDO_WITHIN_DISTANCE`에 대한 첫번째 인수는 검색할 열입니다. 두번째 인수는 거리를 확인할 위치입니다. 반환된 결과의 순서에 대해서는 가정할 필요가 없습니다. 예를 들어, 반환된 첫번째 행은 웨어하우스 3에 가장 가까운 고객으로 보장되지 않습니다.
*   `SDO_WITHIN_DISTANCE` 연산자 내에 사용된 DISTANCE 매개변수는 거리 값을 지정합니다. 이 예제에서는 100입니다.
*   `SDO_WITHIN_DISTANCE` 연산자 내에 사용된 UNIT 매개변수는 DISTANCE 매개변수의 측정 단위를 지정합니다. 기본 단위는 데이터와 연계된 측정 단위입니다. 경도 및 위도 데이터의 경우 기본값은 미터입니다. 이 예에서는 마일입니다.

**휴스턴 창고의 50km 이내 지점 식별:**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![공간 질의 실행](images/query5.png) 노트:

*   `SDO_GEOM.SDO_DISTANCE` 함수는 지점 위치와 휴스턴 웨어하우스 사이의 거리를 계산합니다.
*   `SDO_GEOM.SDO_DISTANCE`에 대한 처음 두 인수는 거리 계산을 위한 BRANCH 및 WAREHOUSE 위치입니다.
*   `SDO_GEOM.SDO_DISTANCE` 에 대한 세번째 인수는 허용한도 값입니다. 허용한도는 Oracle Spatial에서 사용하는 반올림 오류 값입니다. 경도 및 위도 데이터에 대한 공차는 미터 단위입니다. 이 예에서 공차는 50mm입니다.
*   `SDO_GEOM.SDO_DISTANCE` 매개변수 내에 사용된 UNIT 매개변수는 `SDO_GEOM`.`SDO_DISTANCE` 함수로 계산된 거리의 측정 단위를 지정합니다. 기본 단위는 데이터와 연계된 측정 단위입니다. 경도 및 위도 데이터의 경우 기본값은 미터입니다. 이 예제에서는 마일입니다.
*   `ORDER BY DISTANCE_IN_MILES` 절은 거리가 순서대로 반환되고 가장 짧은 거리가 먼저, 거리가 마일로 측정되도록 합니다.

**해안 지역의 지점을 식별합니다.**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![공간 질의 실행](images/query6.png) 노트:

*   `SDO_ANYINTERACT` 연산자는 2개의 인수 geometry1 및 geometry2를 받아들입니다. 연산자는 geometry1가 geometry2의 경계 내부 또는 경계에 있는 행에 대해 `TRUE`를 반환합니다.
*   이 예에서 geometry1는 `B.GEOMETRY`, 분기 형상, geometry2는 해안 영역 형상인 `C.GEOMETRY`입니다. COASTAL\_ZONE 테이블에는 행이 하나만 있으므로 추가 조건이 필요하지 않습니다.

**해안 지역 외부 및 10km 이내 지점 식별:**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![공간 질의 실행](images/query7.png) 노트:

*   이 질의의 첫번째 부분에서 `SDO_WITHIN_DISTANCE` 연산자는 COASTAL\_ZONE에서 10km 이내의 BRANCHES를 식별합니다. 여기에는 COASTAL\_ZONE 내부에 BRANCHES가 포함됩니다.
*   질의는 `MINUS`를 사용하여 COASTAL\_ZONE 내에서 BRANCHES를 제거하고 BRACNCHES만 10km 이내 및 COASTAL\_ZONE 외부로 유지합니다.

## 자세히 알아보기

*   \[공간 제품 포털\] (https://oracle.com/goto/spatial)
*   [공간 문서화](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [공간 블로그](https://blogs.oracle.com/oraclespatial/)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - Kamryn Vinson, 2020년 11월