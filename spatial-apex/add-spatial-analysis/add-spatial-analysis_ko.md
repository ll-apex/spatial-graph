# 공간 분석 통합

## 소개

이 실습에서는 공간 분석을 통합하여 이전 실습의 지도를 향상시킵니다. 선택한 상태의 사용자 정의 거리 내에 있는 공항 검색을 구성합니다.

예상 실험 시간: 30분

### 목표

*   기본 공간 분석 작업 이해
*   APEX Map Region에 공간 분석 통합 이해

### 필요 조건

*   실습 3: 처음부터 맵 만들기

## 작업 1: 필터에 대한 영역 추가

1.  왼쪽 트리 맨 위에 있는 **3페이지: 공항 및 주 맵**을 누릅니다. 그런 다음 오른쪽의 \[페이지\] 속성 패널에서 \[모양\] 아래의 \[페이지 템플리트\]를 **왼쪽 열**로 변경합니다.
    
    ![페이지 템플리트 업데이트](images/add-spatial-analysis-01a.png)
    
    그러면 레이아웃에 **LEFT COLUMN**이 표시되어야 합니다.
    
    ![페이지 템플리트 업데이트](images/add-spatial-analysis-01b.png)
    
2.  정적 콘텐츠 영역을 왼쪽 열로 끌어옵니다.
    
    ![정적 콘텐츠 영역 추가](images/add-spatial-analysis-01c.png)
    
3.  **내 필터 영역** 또는 선택한 이름으로 이름을 바꿉니다.
    
    ![영역 이름 바꾸기](images/add-spatial-analysis-02.png)
    

## 작업 2: 상태 선택에 대한 항목 추가

1.  목록 선택 항목을 필터 영역으로 끌어와서 이름을 **P3\_STATE**로 업데이트합니다.
    
    ![선택 목록 항목 추가](images/add-spatial-analysis-03.png)
    
2.  오른쪽의 Page Item 속성에서 List of Values 섹션으로 스크롤합니다. 스위치를 사용하여 **필요한 값**을 사용으로 설정하고 유형을 **SQL 질의**로 설정하고 다음 질의를 입력합니다.
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT 질의](images/add-spatial-analysis-04.png)
    
3.  오른쪽의 Page Item 속성에서 Default 섹션으로 아래로 스크롤합니다. 유형을 **정적**으로 설정하고 값을 **'텍사스'** 또는 선택한 다른 상태(작은 따옴표)로 설정합니다.
    
    ![선택 목록 구성](images/add-spatial-analysis-05.png)
    

## 태스크 3: 거리 입력 항목 추가

1.  Number Field를 필터 영역으로 끌어옵니다. **P3\_DISTANCE**로 이름을 업데이트하고 레이블을 **Proximity (km)**로 업데이트합니다.
    
    ![숫자 필드 항목 추가](images/add-spatial-analysis-06.png)
    
2.  오른쪽의 \[페이지 항목\] 속성에서 \[검증\] 섹션을 찾아 **필요한 값**을 사용으로 설정합니다.
    
    ![검증을 값 필수로 설정](images/add-spatial-analysis-07.png)
    
3.  Default 섹션으로 스크롤합니다. Type을 **Static**으로 설정하고 값을 **100**으로 설정합니다.
    
    ![기본값 세트](images/add-spatial-analysis-08.png)
    
    이제 상태에 근접하여 공항을 필터링하기 위한 입력이 생겼습니다. 다음 작업은 동적 작업을 사용하여 필터를 적용하는 것입니다.
    

## 작업 4: 동적 작업을 사용하여 필터 적용

그런 다음 사용자가 상태 및/또는 거리 값을 변경할 때 호출되는 작업을 생성합니다.

1.  P3\_STATE 또는 P3\_DISTANCE 항목을 마우스 오른쪽 단추로 누르고 **동적 작업 생성**을 선택합니다. 생성하는 작업은 두 항목에 모두 적용됩니다.
    
    ![동적 작업 생성](images/add-spatial-analysis-09.png)
    
2.  오른쪽의 동적 작업 속성에서 이름을 **검증 및 새로고침**으로 설정합니다. When 섹션에서 Event를 **Change**로, Selection Type을 **Items**로, Items를 쉼표로 구분된 목록 **P3\_DISTANCE,P3\_STATE**로 설정합니다. 항목 텍스트 상자 오른쪽에 있는 단추를 사용하여 목록에서 항목을 선택할 수 있습니다. 거리에 대한 음수 값 제출을 방지하려면 클라이언트측 조건 섹션에서 유형을 **항목 >= 값**으로 설정하고 항목을 **P3\_DISTANCE**로, 값을 **0**으로 설정합니다.
    
    ![동적 작업 구성](images/add-spatial-analysis-10.png)
    
3.  동적 작업은 구성된 조건에 따라 호출되는 TRUE 작업 및 FALSE 작업으로 구성됩니다. 이 경우 클라이언트측 조건(P3\_DISTANCE >= 0)은 TRUE 작업을 호출할지(조건이 충족됨) 아니면 FALSE 작업을 호출할지(조건이 충족되지 않음)를 결정합니다. 그러면 음수 거리 입력을 트랩할 수 있습니다.
    
    클라이언트측 조건이 TRUE인 경우 작업이 입력 값을 제출하고 페이지를 refresh해야 합니다. TRUE 아래의 작업을 클릭합니다. 오른쪽의 \[작업\] 속성에서 \[식별\]에서 \[작업\]을 **새로고침**으로 설정합니다. \[영향을 받는 요소\]에서 \[선택 유형\]을 **영역**으로 설정하고 \[지역\]을 **내 맵 영역**(또는 다른 경우 사용한 이름)으로 설정합니다. 왼쪽의 페이지 트리에서 TRUE 작업이 \[새로고침\]으로 변경됩니다.
    
    ![동적 작업 구성](images/add-spatial-analysis-11.png)
    
4.  다음 작업은 클라이언트측 조건이 충족되지 않아 음수 거리 값이 입력된 경우 호출할 작업을 구성하는 것입니다. 두 항목의 동적 작업에서 False를 마우스 오른쪽 버튼으로 누르고 **FALSE 작업 생성**을 선택합니다.
    
    ![동적 작업 구성](images/add-spatial-analysis-12.png)
    
5.  거리가 음수일 때 호출되는 FALSE 작업은 사용자에게 팝업 메시지가 됩니다. False 동작을 클릭합니다. 오른쪽의 \[동작\] 등록정보에서 \[식별\]에서 \[동작\]을 **경보**로 설정합니다. 설정에서 제목을 **부적합한 거리**(경보 배너가 됨)로 설정하고 메시지를 **거리 >= 0**(경보 본문이 됨)으로 설정합니다. 왼쪽의 페이지 트리에서 False 작업이 Alert로 변경되는 것을 확인합니다.
    
    ![동적 작업 구성](images/add-spatial-analysis-13.png)
    
6.  맵 영역에는 현재 모든 상태를 표시하는 상태 레이어가 포함되어 있습니다. 이제 P3\_STATE 메뉴에서 선택한 상태만 표시하도록 이 계층을 조정합니다. 왼쪽의 페이지 트리에서 레이어 아래의 상태를 클릭합니다. 오른쪽의 도면층 특성에서 식별에서 이름을 **선택된 상태**로 변경합니다. Source에서 Where 절을 **state\_code = :P3\_STATE**로 설정합니다. 왼쪽의 페이지 트리에서 레이어 이름이 Selected State로 변경되는지 확인합니다.
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![WHERE 절 구성](images/add-spatial-analysis-14.png)
    
7.  마지막으로 Airports 레이어를 업데이트하여 사용자 지정 상태 및 근접도로 필터링된 항목을 반환합니다. 왼쪽의 페이지 트리에서 공항 레이어를 클릭합니다. 오른쪽의 \[레이어\] 속성에서 \[소스\] 아래에서 \[유형\]을 **SQL 질의**로 변경합니다. SQL Query에 대해 Oracle Database의 Native SQL "within distance" 연산자를 사용하는 다음을 입력합니다.
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    제출할 페이지 항목에 쉼표로 구분된 목록 **P3\_STATE,P3\_DISTANCE**를 입력합니다.
    
    ![공간 SQL 질의](images/add-spatial-analysis-15.png)
    
8.  이제 페이지를 볼 수 있습니다. **저장**을 누른 다음 오른쪽 위에 있는 녹색 **실행** 단추를 누릅니다. 페이지가 렌더링되면 상태에 대해 **알라바마**를 선택합니다. 지도에는 선택한 상태 및 공항이 100km(기본 거리) 내에 표시됩니다.
    
    ![페이지 저장 및 실행](images/add-spatial-analysis-16.png)
    
9.  선택한 상태를 **Kansas**로 변경합니다. 이제 선택한 상태와 공항이 100km로 표시되는지 확인합니다.
    
    ![캔자스 선택](images/add-spatial-analysis-17.png)
    
10.  거리를 600km로 늘린 다음 Enter 또는 Tab을 눌러 제출합니다. 이제 지도에 더 큰 거리 내에 추가 공항이 표시되는지 확인합니다.
    
    ![600km에 거리 증가](images/add-spatial-analysis-18.png)
    
11.  마지막으로 음수 거리를 제출하면 이전에 구성한 오류 팝업이 나타납니다.
    
    ![음수 거리 경보](images/add-spatial-analysis-19.png)
    
    이 워크샵의 시작 부분에 설치한 Sample Maps 응용 프로그램에 표시된 것처럼 Map Regions and Spatial을 사용하여 기능적으로 수행할 수 있는 추가 작업이 엄청납니다. 이 워크샵에서는 기본 사항을 소개했으며 APEX 애플리케이션에서 관심이 많아지고 맵 및 공간 분석 기능을 활용할 수 있기를 바랍니다.
    

## 자세히 알아보기

*   [Oracle Spatial](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2023년 3월