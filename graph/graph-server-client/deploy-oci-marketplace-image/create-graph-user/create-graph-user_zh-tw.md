# 在資料庫動作中建立及啟用資料庫使用者

## 簡介

這個實驗室會逐步引導您瞭解如何開始使用資料庫動作。您將會瞭解如何在「資料庫動作」中建立使用者，並提供對「資料庫動作」的存取權。

估計時間：3 分鐘

### 目標

*   瞭解如何在「資料庫動作」中設定必要的資料庫角色。
*   瞭解如何在資料庫動作中建立資料庫使用者。

### 先決條件

*   Oracle 雲端帳戶
*   佈建的 Autonomous Database

## 作業 1：登入資料庫動作

在新建立之 ADB 執行處理的資料庫動作中以管理員使用者身分登入。

按一下左上方的**導覽功能表**，瀏覽至 **Oracle Database** ，然後選取 **Autonomous Transaction Processing** 。

![資料庫組態](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

在 Autonomous Database 詳細資訊頁面中，開啟**工具**頁籤，然後按一下**資料庫動作**。請確定您的瀏覽器允許彈出視窗。

![adb- 主控台](images/adb-console.jpg)

輸入 **ADMIN** 作為使用者名稱，然後執行下一個步驟。

![登入 -1](images/login-1.jpg)

輸入密碼 (您在 Lab 2 設定) 並登入。

![登入 -2](images/login-2.jpg)

以 **ADMIN** 使用者身分登入之後，請前往 **SQL** 功能表。

![資料庫動作](images/database-actions.jpg)

## Taks 2：建立資料庫角色

現在建立圖形功能所需的角色。請在「SQL 工作表」中輸入下列命令，然後以「管理員」使用者身分連線時執行。

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
    

將預設權限指派給角色 **GRAPH\_ADMINISTRATOR** 和 **GRAPH\_DEVELOPER** ，以便將多個權限群組在一起。

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
    

## 作業 3：建立資料庫使用者

現在建立 **CUSTOMER\_360** 使用者並為此使用者提供「資料庫動作」存取權。

開啟主功能表，然後按一下「資料庫使用者」。

![使用者 -1](images/user-1.jpg)

按一下**建立使用者 (Create User)** 按鈕，輸入使用者名稱與密碼。啟用 **Web Access** ，並將配額設定為 **UNLILMITED** 。

![使用者 -2](images/user-2.png)

前往**授權的角色**頁籤，然後將 **`GRAPH_DEVELOPER`** 角色和 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 角色授予此使用者。(預設會選取兩個角色 **CONNECT** 和 **RESOURCE** 。請保留勾選，以便同時獲得許可。)

![使用者 -3](images/user-3.png)

繼續**建立使用者**，然後開啟登入視窗。

![使用者 -4](images/user-4.jpg)

確認您可以用新使用者登入。

![使用者 -5](images/user-5.jpg)

如需詳細資訊，請參閱文件中的[提供資料庫使用者的資料庫動作存取權](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA)一節。

您現在可以繼續下一個實驗室。

## 確認

*   **作者** - Spatial and Graph 產品經理 Jayant Sharma
*   **貢獻者** - Arabella Yao、Jenny Tsai
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月