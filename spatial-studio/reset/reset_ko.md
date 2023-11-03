# Spatial Studio 및 ADB를 사전 워크샵 상태로 재설정

## 소개

이 실습에서는 필요한 경우 처음부터 다시 시작할 수 있도록 이전 실습에서 생성한 모든 항목을 제거합니다.

예상 실험 시간: 5분

실습 과정을 간단히 살펴보려면 아래 비디오를 시청하십시오.

[Spatial Studio 및 ADB를 사전 워크샵 상태로 재설정](videohub:1_z4mhzd51)

### 목표

이 실습에서는 다음을 수행합니다.

*   이전 실습에서 생성된 Spatial Studio 및 ADB 아티팩트를 제거합니다.

### 필요 조건

*   Oracle Cloud Marketplace에서 배포된 Spatial Studio

## 태스크 1: 프로젝트 삭제

1.  **프로젝트** 페이지로 이동합니다. 게시된 프로젝트에 대한 작업 메뉴에서 **삭제** 옵션을 선택합니다.
    
    ![게시된 프로젝트 삭제](images/reset-01.png)
    
2.  프로젝트에 대한 작업 메뉴에서 **삭제** 옵션을 선택합니다.
    
    ![프로젝트 삭제](images/reset-02.png)
    

## 작업 2: 데이터 세트 삭제

1.  **데이터 세트** 페이지로 이동합니다. **FLOOD2060의 CHOOLS** 분석 데이터 세트에 대한 작업 메뉴에서 **삭제** 옵션을 선택합니다.
    
    ![공간 분석 데이터 집합 삭제](images/reset-03.png)
    
2.  다음 순서로 다른 분석 데이터 세트에 대해 이전 단계를 반복합니다. 1) BUILDINGS FLOOD CONTACT, 2) FACILITIES NEAR FLOOD2060 DISTANCE, 3) FACILITIES NEAR FLOOD2060
    
3.  FACILITIES 데이터 세트의 작업 메뉴에서 **삭제** 옵션을 선택합니다.
    
    ![데이터 집합 삭제](images/reset-04.png)
    
4.  확인 팝업에서 연관된 데이터베이스 테이블을 삭제하는 옵션을 선택합니다.
    
    ![데이터베이스 테이블 삭제 확인](images/reset-05.png)
    
5.  나머지 모든 데이터 세트에 대해 반복합니다.
    

이제 Spatial Studio와 ADB가 사전 워크샵 상태로 재설정됩니다.

## 자세히 알아보기

*   [Oracle Spatial 제품 페이지](https://www.oracle.com/database/spatial)
*   [Spatial Studio 시작하기](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Spatial Studio 설명서](https://docs.oracle.com/en/database/oracle/spatial-studio)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Denise Myrick
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 8월