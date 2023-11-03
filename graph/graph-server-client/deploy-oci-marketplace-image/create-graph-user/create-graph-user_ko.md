# Database Actions에서 데이터베이스 사용자 생성 및 사용으로 설정

## 소개

이 실습에서는 Database Actions를 시작하기 위한 단계를 안내합니다. Database Actions에서 유저를 생성하고 해당 유저에게 Database Actions에 대한 액세스 권한을 제공하는 방법을 배웁니다.

추정 시간: 3분

### 목표

*   Database Actions에서 필요한 데이터베이스 롤을 설정하는 방법을 알아봅니다.
*   Database Actions에서 데이터베이스 사용자를 생성하는 방법을 알아봅니다.

### 필요 조건

*   Oracle 클라우드 계정
*   프로비저닝된 Autonomous Database

## 작업 1: Database Actions에 로그인

새로 생성된 ADB 인스턴스의 Database Actions에서 Admin 사용자로 로그인합니다.

왼쪽 위에 있는 **탐색 메뉴**를 누르고 **Oracle Database**로 이동한 다음 **Autonomous Transaction Processing**을 선택합니다.

![데이터베이스-atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

\[Autonomous Database 세부 정보\] 페이지에서 **도구** 탭을 열고 **데이터베이스 작업**을 누릅니다. 브라우저가 팝업 창을 허용하는지 확인합니다.

![adb 콘솔](images/adb-console.jpg)

사용자 이름으로 **ADMIN**을 입력하고 다음으로 이동합니다.

![로그인-1](images/login-1.jpg)

암호(Lab 2에서 설정)를 입력하고 로그인합니다.

![로그인-2](images/login-2.jpg)

**ADMIN** 사용자로 로그인한 후 **SQL** 메뉴로 이동합니다.

![데이터베이스-작업](images/database-actions.jpg)

## Taks 2: 데이터베이스 롤 생성

이제 그래프 피쳐에 필요한 역할을 작성합니다. SQL Worksheet에 다음 명령을 입력하고 Admin 유저로 연결한 상태로 실행합니다.

    <copy>
    DECLARE
      PRAGMA AUTONOMOUS_TRANSACTION;
      role_exists EXCEPTION;
      PRAGMA EXCEPTION_INIT(role_exists, -01921);
      TYPE graph_roles_table IS TABLE OF VARCHAR2(50);
      graph_roles graph_roles_table;
    BEGIN
      graph_roles := graph_roles_table(
        'GRAPH_DEVELOPER',
        'GRAPH_ADMINISTRATOR',
        'PGX_SESSION_CREATE',
        'PGX_SERVER_GET_INFO',
        'PGX_SERVER_MANAGE',
        'PGX_SESSION_READ_MODEL',
        'PGX_SESSION_MODIFY_MODEL',
        'PGX_SESSION_NEW_GRAPH',
        'PGX_SESSION_GET_PUBLISHED_GRAPH',
        'PGX_SESSION_COMPILE_ALGORITHM',
        'PGX_SESSION_ADD_PUBLISHED_GRAPH');
      FOR elem IN 1 .. graph_roles.count LOOP
      BEGIN
        dbms_output.put_line('create_graph_roles: ' || elem || ': CREATE ROLE ' || graph_roles(elem));
        EXECUTE IMMEDIATE 'CREATE ROLE ' || graph_roles(elem);
      EXCEPTION
        WHEN role_exists THEN
          dbms_output.put_line('create_graph_roles: role already exists. continue');
        WHEN OTHERS THEN
          RAISE;
        END;
      END LOOP;
    EXCEPTION
      when others then
        dbms_output.put_line('create_graph_roles: hit error ');
        raise;
    END;
    /
    </copy>
    

**GRAPH\_ADMINISTRATOR** 및 **GRAPH\_DEVELOPER** 역할에 기본 권한을 지정하여 여러 권한을 함께 그룹화합니다.

    <copy>
    GRANT PGX_SESSION_CREATE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_GET_INFO TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SERVER_MANAGE TO GRAPH_ADMINISTRATOR;
    GRANT PGX_SESSION_CREATE TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_NEW_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_GET_PUBLISHED_GRAPH TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_MODIFY_MODEL TO GRAPH_DEVELOPER;
    GRANT PGX_SESSION_READ_MODEL TO GRAPH_DEVELOPER;
    </copy>
    

## 작업 3: 데이터베이스 유저 생성

이제 **CUSTOMER\_360** 사용자를 생성하고 이 사용자에 대한 Database Actions 액세스 권한을 제공합니다.

주 메뉴를 열고 "Database Users"를 누릅니다.

![사용자-1](images/user-1.jpg)

**사용자 생성** 단추를 누르고 사용자 이름과 비밀번호를 입력합니다. **웹 액세스**를 사용으로 설정하고 할당량을 **UNLILMITED**로 설정합니다.

![사용자-2](images/user-2.png)

**Granted Roles** 탭으로 이동하고 이 사용자에게 **`GRAPH_DEVELOPER`** 역할 및 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 역할을 부여합니다. 기본적으로 두 역할 **CONNECT** 및 **RESOURCE**가 선택됩니다. 확인해 주시면 감사하겠습니다.)

![사용자-3](images/user-3.png)

**사용자 생성**을 계속하고 로그인 창을 엽니다.

![사용자-4](images/user-4.jpg)

새 사용자로 로그인할 수 있는지 확인합니다.

![사용자-5](images/user-5.jpg)

자세한 내용은 설명서의 ["데이터베이스 사용자에게 데이터베이스 작업 액세스 제공"](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA) 절을 참조하십시오.

이제 다음 실습을 진행할 수 있습니다.

## 확인

*   **작성자** - Jayant Sharma, Spatial and Graph 제품 관리자
*   **기여자** - Arabella Yao, Jenny Tsai
*   **최종 업데이트 수행자/날짜** - Ryota Yamanaka, 2023년 3월