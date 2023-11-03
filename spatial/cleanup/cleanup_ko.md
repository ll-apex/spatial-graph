# ADB를 사전 워크샵 상태로 재설정

## 소개

이 실습에서는 필요한 경우 처음부터 다시 시작할 수 있도록 이전 실습에서 생성한 모든 항목을 제거합니다.

예상 실험 시간: 2분

### 정보

이 연습에서는 이전에 생성한 모든 artifact가 삭제됩니다.

### 목표

*   ADB를 사전 워크샵 상태로 재설정합니다.

### 필요 조건

*   실습 3 완료, 공간 데이터 준비

## 작업 1: 이 워크샵에서 생성한 모든 항목 제거

1.  이 워크샵에서 생성한 테이블과 인덱스를 제거하려면 SQL Worksheet의 run script 버튼을 사용하여 다음을 실행합니다.
    
    ![이미지 대체 텍스트](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  이 워크샵에 삽입된 공간 메타 데이터를 삭제하려면 SQL Worksheet의 run script 버튼을 사용하여 다음을 실행합니다.
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  이 워크샵에서 생성한 함수를 삭제하려면 다음을 실행하십시오.
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - David Lapp, 2022년 9월