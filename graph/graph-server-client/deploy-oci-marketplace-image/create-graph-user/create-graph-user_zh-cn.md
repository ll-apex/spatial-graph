# 在 Database Actions 中创建和启用数据库用户

## 简介

此练习将指导您完成数据库操作入门的步骤。您将学习如何在 Database Actions 中创建用户并为该用户提供对 Database Actions 的访问权限。

估计时间：3 分钟

### 目标

*   了解如何在 Database Actions 中设置所需的数据库角色。
*   了解如何在 Database Actions 中创建数据库用户。

### 先备条件

*   Oracle 云帐户
*   预配的 Autonomous Database

## 任务 1：登录到 Database Actions

以管理员用户身份登录新创建的 ADB 实例的 Database Actions。

单击左上角的**导航菜单**，导航到 **Oracle Database** ，然后选择**自治事务处理**。

![数据库 -atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

在“Autonomous Database Details（自治数据库详细信息）”页面中，打开 **Tools（工具）**选项卡，然后单击 **Database Actions（数据库操作）**。确保浏览器允许弹出窗口。

![广告控制台](images/adb-console.jpg)

输入 **ADMIN** 作为用户名，然后转到。

![登录 -1](images/login-1.jpg)

输入密码（您在实验 2 中设置）并登录。

![登录 -2](images/login-2.jpg)

以 **ADMIN** 用户身份登录后，转至 **SQL** 菜单。

![数据库操作](images/database-actions.jpg)

## Taks 2：创建数据库角色

现在创建图形功能所需的角色。在 SQL 工作表中输入以下命令，并在以管理员用户身份连接时运行该命令。

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
    

将默认权限分配给角色 **GRAPH\_ADMINISTRATOR** 和 **GRAPH\_DEVELOPER** ，以便将多个权限组合在一起。

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
    

## 任务 3：创建数据库用户

现在创建 **CUSTOMER\_360** 用户并为此用户提供 Database Actions 访问权限。

打开主菜单，然后单击“Database Users（数据库用户）”。

![用户 -1](images/user-1.jpg)

单击**创建用户**按钮，输入用户名和密码。启用 **Web 访问**并将配额设置为 **UNLILMITED** 。

![用户 -2](images/user-2.png)

转到**授予的角色**选项卡，并将 **`GRAPH_DEVELOPER`** 角色和 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 角色授予此用户。（默认情况下选择两个角色 **CONNECT** 和 **RESOURCE** ）。请对其进行检查，以便还将授予他们。)

![用户 -3](images/user-3.png)

继续**创建用户**，然后打开登录窗口。

![用户 -4](images/user-4.jpg)

确认可以使用新用户登录。

![用户 -5](images/user-5.jpg)

有关详细信息，请参阅文档中的[向数据库用户提供 Database Actions 访问权限](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA)部分。

现在，您可以进入下一个实验室。

## 确认

*   **作者** - Spatial and Graph 产品经理 Jayant Sharma
*   **贡献者** - Arabella Yao、Jenny Tsai
*   **上次更新者/日期** - Ryota Yamanaka，2023 年 3 月