# Graph Studio: PGQL CREATE PROPERTY GRAPH 문을 사용하여 그래프 생성

## 소개

이 실습에서는 Graph Studio 및 CREATE PROPERTY GRAPH 문을 사용하여 `bank_accounts` 및 `bank_txns` 테이블에서 그래프를 생성합니다.

예상 시간: 15분

실습 과정을 간단히 살펴보려면 아래 비디오를 시청하십시오. [연습](videohub:1_jguolqf3)

### 목표

방법 알아보기

*   Graph Studio 및 PGQL DDL(즉, CREATE PROPERTY GRAPH 문)을 사용하여 기존 테이블 또는 뷰에서 그래프 모델링 및 생성

### 필요 조건

*   다음 실습에서는 Autonomous Database - Serverless가 필요합니다.
*   그래프 사용 사용자(`GRAPHUSER`)가 있습니다. 즉, 올바른 롤과 권한을 가진 데이터베이스 유저가 있습니다.

## 작업 1: Autonomous Database 액세스

1.  왼쪽 위에 있는 **탐색 메뉴**를 누르고 **Oracle Database**로 이동한 다음 **Autonomous Database**를 선택합니다.
    
    ![Autonomous Database로 이동합니다.](images/navigation-menu.png " ")
    
2.  **로그인 정보 보기**에 제공된 구획을 선택하고 **Autonomous Database**에 대한 **표시 이름**을 누릅니다.
    
    ![Navigation 메뉴에서 Autonomous Database를 선택합니다.](images/select-autonomous-database.png " ")
    

## 작업 2: Graph Studio에 로그인

Graph Studio는 Autonomous Database의 기능입니다. Database Actions Launchpad에서 옵션으로 제공됩니다. Graph Studio에 로그인하려면 그래프 지원 사용자가 필요합니다. 사용자가 이미 생성되어 있습니다.

1.  **Autonomous Database 세부 정보 페이지** 페이지에서 **Database Actions** 단추를 누른 다음 **모든 데이터베이스 작업 보기**를 선택합니다.
    
    ![Database Actions 버튼을 누릅니다.](images/click-database-actions.png " ")
    
2.  \[데이터베이스 작업\] 패널에서 **Graph Studio**를 누릅니다.
    
    ![Open Graph Studio를 누릅니다.](images/graphstudiofixed.png " ")
    
3.  Graph Studio에 로그인합니다. 데이터베이스 사용자 GRAPHUSER에 대한 인증서를 사용합니다.
    
    ![데이터베이스 사용자 MOVIESTREAM에 대한 인증서 사용](images/graph-login.png " ")
    
    Graph Studio는 왼쪽의 메뉴에서 액세스되는 일련의 페이지로 구성됩니다.
    
    **홈** 아이콘은 홈 페이지로 이동합니다.  
    **그래프** 페이지에는 노트북에 사용할 기존 그래프가 나열됩니다.  
    **노트북** 페이지에는 기존 노트북이 나열되며 새 노트북을 생성할 수 있습니다.  
    **템플리트** 페이지에서는 그래프 시각화에 대한 템플리트를 생성할 수 있습니다.  
    **작업** 페이지에는 백그라운드 작업의 상태가 나열되며 연관된 로그(있는 경우)를 볼 수 있습니다.  
    

## 작업 3: 계정 및 트랜잭션 그래프 생성

1.  **그래프** 아이콘을 누릅니다. 그런 다음 **그래프 생성**을 누릅니다.
    
    ![생성 버튼 모델러가 있는 위치를 표시합니다.](images/graph-create-button.png " ")
    
2.  그래프 이름으로 `bank_graph`을 입력한 다음 **다음**을 누릅니다. 설명 및 태그 필드는 선택 사항입니다.  
    이 그래프 이름은 다음 실습 전체에서 사용됩니다.  
    다른 이름을 입력하지 마십시오. 그러면 다음 연습의 query와 코드 조각이 실패합니다.
    
    ![그래프에 이름을 지정하는 그래프 생성 창을 표시합니다.](./images/create-graph-dialog.png " ")
    
3.  **GRAPHUSER**를 확장하고 `BANK_ACCOUNTS` 및 `BANK_TXNS` 테이블을 선택합니다.
    
    ![BANK_ACCOUNTS 및 BANK_TXNS 선택 방법을 보여줍니다.](./images/select-tables.png " ")
    
4.  오른쪽으로 이동합니다. 즉, 셔틀 컨트롤의 첫 번째 아이콘을 누릅니다.
    
    ![선택한 테이블을 표시합니다.](./images/selected-tables.png " ")
    
5.  **다음**을 누릅니다. 이 그래프를 편집하고 업데이트하여 모서리와 정점 레이블을 추가합니다.
    
    `BANK_TXNS`에 외래 키 제약 조건이 지정되어 있고 이를 참조하는 외래 키 제약 조건이 있으므로 권장 그래프에는 `BANK_ACCOUNTS`가 정점 테이블로 사용됩니다.
    
    그리고 `BANK_TXNS`는 권장되는 모서리 테이블입니다.
    
    ![정점 및 모서리 테이블을 표시합니다.](./images/create-graph-suggested-model.png " ")
    
6.  이제 기본 정점 및 모서리 레이블을 변경하겠습니다.
    
    `BANK_ACCOUNTS` 정점 테이블을 누릅니다. Vertex Label을 **ACCOUNTS**로 변경합니다. 그런 다음 확인 표시를 눌러 레이블을 확인하고 업데이트를 저장합니다.
    
    ![정점의 레이블 이름을 계정으로 변경](images/edit-accounts-vertex-label.png " ")
    
    `BANK_TXNS` 모서리 테이블을 누르고 모서리 레이블의 이름을 `BANK_TXNS`에서 **TRANSFERS**로 바꿉니다. 그런 다음 확인 표시를 눌러 레이블을 확인하고 업데이트를 저장합니다.
    
    ![모서리의 레이블 이름을 전송으로 변경함](images/edit-edge-label.png " ")
    
    그래프를 질의할 때 이 워크샵의 다음 실습에서 이러한 에지 레이블을 사용할 것이므로 **중요**합니다. **다음**을 누릅니다.
    

7.  요약 단계에서 **그래프 생성**을 누릅니다.
    
    ![작업 상태가 Success인 작업 탭을 표시합니다.](./images/jobs-create-graph.png " ")
    
    그러면 Create Graph 탭이 열리고 **Create Graph**를 누릅니다.
    
    ![인메모리 사용 및 그래프 생성 단추를 보여줍니다.](./images/create-graph-in-memory.png " ")
    
    그러면 그래프가 생성될 Jobs 페이지로 이동합니다.
    
    이 연습을 마칩니다. **이제 다음 실습을 진행할 수 있습니다.**
    

## 확인

*   **작성자** - Jayant Sharma, 제품 관리
*   **제공자** - Jayant Sharma, 제품 관리
*   **최종 업데이트 기한/일자** - Ramu Murakami Gutierrez, 2023년 6월 제품 관리자