# 그래프 사용자 생성

## 소개

이 실습에서는 Autonomous Database의 그래프 기능 사용에 필요한 적합한 롤 및 권한을 가진 데이터베이스 유저를 생성합니다.

예상 시간: 5분

실습 과정을 빠르게 살펴보려면 아래 비디오를 시청하십시오.

[이 워크샵의 비디오에 연결](youtube:CQh8Q24Rboc)

### 목표

방법 알아보기

*   **Graph Studio** 액세스에 필요한 적합한 롤 및 권한으로 데이터베이스 사용자 생성

### 필요 조건

*   다음 랩에는 Autonomous Data Warehouse - Shared Infrastructure 또는 Autonomous Transaction Processing - 공유 인프라 계정이 필요합니다.

## 작업 1: Autonomous Database 인스턴스의 Database Actions에 연결

1.  OCI 콘솔에서 Autonomous Database 인스턴스에 대한 서비스 세부 정보 페이지를 엽니다.
    
    그런 다음 **데이터베이스 작업** 링크를 눌러 엽니다.
    
    ![Database Actions 버튼을 가리키는 Autonomous Database 홈 페이지](images/open-database-actions.png "Database Actions 버튼을 가리키는 Autonomous Database 홈 페이지")
    

## 작업 2: 웹 액세스 및 그래프 사용 유저 생성

1.  Autonomous Database 인스턴스의 ADMIN 사용자로 로그인합니다.
    
    ![Autonomous Database 인스턴스에 로그인합니다.](./images/login.png "Autonomous Database 인스턴스에 로그인합니다.")
    
2.  **관리** 아래의 **DATABASE USERS** 타일을 누릅니다.
    
    ![Database Actions 타일을 누릅니다.](./images/db-actions-users.png "Database Actions 타일을 누릅니다.")
    
3.  **\+ Create User** 아이콘을 누릅니다.
    
    ![Create User를 누릅니다.](./images/db-actions-create-user.png "Create User를 누릅니다. ")
    
4.  필요한 세부정보(예: 사용자 이름 및 비밀번호)를 입력합니다. **그래프 사용** 및 **웹 액세스** 라디오 단추를 설정합니다. `DATA` 테이블스페이스에 할당할 할당량(예: **UNLIMITED**)을 선택합니다.
    
    주: 암호는 다음 요구 사항을 충족해야 합니다.
    
    *   비밀번호는 12자에서 30자 사이여야 하며 대문자, 소문자 및 숫자를 하나 이상 포함해야 합니다.
    *   비밀번호에 사용자 이름을 포함할 수 없습니다.
    *   비밀번호에 대문자를 포함할 수 없습니다.
    *   비밀번호는 이 사용자에 대해 사용된 마지막 4개 비밀번호와 달라야 합니다.
    *   비밀번호는 24시간 전에 설정된 것과 동일한 비밀번호가 아니어야 합니다.
    
    ![Graph username 및 password를 설정하고 Create User를 선택합니다.](images/db-actions-create-graph-user.png "Graph username 및 password를 설정하고 Create User를 선택합니다. ")
    
    **참고: ADMIN 사용자를 그래프에 표시하지 않고 ADMIN 사용자로 Graph Studio에 로그인하지 마십시오. ADMIN 사용자는 기본적으로 추가 권한을 가집니다. 그래프 데이터 및 분석 사용에 필요한 권한만 있는 계정을 만들고 사용합니다.**
    
    패널 아래쪽에 있는 **Create User** 버튼을 눌러 지정된 자격 증명으로 사용자를 만듭니다.
    
    이제 새로 만든 사용자가 나열됩니다.
    
    ![새로 생성된 사용자가 나열됩니다.](./images/db-actions-user-created.png "새로 생성된 사용자가 나열됩니다. ")
    
    **주:** _대신 위의 UI 단계는 ADMIN으로 로그인할 때 아래 나열된 다음 SQL 명령을 실행하여 수행할 수 있습니다. 따라서 아래의 5단계는 필요하지 않습니다. GRAPHUSER를 생성하고 활성화하는 다른 방법을 보여줍니다._
    
5.  새로 생성된 유저에게 원하는 테이블스페이스 할당량을 할당합니다. SQL 페이지를 열고 alter 명령을 실행합니다.
    
    예를 들어, `ALTER USER GRAPHUSER QUOTA UNLIMITED ON DATA;`  
    는 `DATA`라는 테이블스페이스에서 사용자 `GRAPHUSER`의 할당량을 할당합니다.  
    다음 명령을 복사하여 SQL Worksheet에 붙여 넣습니다.  
    `<username>` 및 `<quota>`를 올바른 값으로 바꾼 다음 Run을 눌러 실행합니다.
    
        <copy>
        -- Optional statement to use in place of the UI of the Administration page
        ALTER USER <username> QUOTA <quota> ON DATA;
        </copy>
        
    
        <copy>
        -- Optional statements to use in place of the UI of the Administration page
        GRANT GRAPH_DEVELOPER TO <username> ;
        ALTER USER <username> GRANT CONNECT THROUGH "GRAPH$PROXY_USER";
        </copy>
        
    
    아래 스크린샷은 ALTER USER 문 실행 예를 보여줍니다.
    
    ![사용자 할당량을 10G로 변경](./images/alter-user.png "사용자 할당량을 10G로 변경")
    
    ![alter user 명령문을 실행합니다.](./images/run-sql.png "alter user 명령문을 실행합니다.")
    
    ![사용자가 스크립트 출력에서 변경된 것으로 표시됩니다.](./images/user-altered.png "사용자가 스크립트 출력에서 변경된 것으로 표시됩니다.")
    
6.  마찬가지로 SQL 문을 사용하여 GRAPHUSER가 올바르게 설정되었는지 확인할 수 있습니다.
    
    `ADMIN`로 Data Actions SQL에 로그인하여 다음 SQL 문을 입력하고 실행해야 합니다.
    
        <copy>
        select * from dba_role_privs where grantee='GRAPHUSER';
        
        select * from dba_proxies where client='GRAPHUSER';
        </copy>
        
    
    결과는 아래 스크린샷과 동일해야 합니다.
    
    ![그래프 사용자에게 롤 및 권한 부여](images/graphuser-role-privs.png "그래프 사용자에게 롤 및 권한 부여")
    
    ![그래프 사용자에게 프록시 부여](images/graphuser-proxy-grant.png "그래프 사용자에게 프록시 부여")
    

ADB에서 그래프를 생성하고 분석하는 방법을 알아보려면 **다음 실습으로 이동**하십시오.

## 확인

*   **작성자** - Jayant Sharma, 제품 관리
*   **기여자** - Korbi Schmid, Rahul Tasker
*   **최종 업데이트 수행자/날짜** - Jayant Sharma, 2023년 6월