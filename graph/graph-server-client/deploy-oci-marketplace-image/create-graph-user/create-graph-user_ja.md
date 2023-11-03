# データベース・アクションでのデータベース・ユーザーの作成および有効化

## 概要

このラボでは、データベース・アクションを開始するステップについて説明します。データベース・アクションでユーザーを作成し、そのユーザーにデータベース・アクションへのアクセス権を付与する方法を学習します。

見積時間: 3分

### 目標

*   データベース・アクションで必要なデータベース・ロールを設定する方法を学習します。
*   データベース・アクションでデータベース・ユーザーを作成する方法を学習します。

### 前提条件

*   Oracleクラウド・アカウント
*   プロビジョニングされたAutonomous Database

## タスク1: データベース・アクションへのログイン

新しく作成したADBインスタンスのデータベース・アクションで管理ユーザーとしてログインします。

左上の**「ナビゲーション・メニュー」**をクリックし、**「Oracle Database」**に移動して**「Autonomous Transaction Processing」**を選択します。

![データベース-ATP](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

「Autonomous Databaseの詳細」ページで、**「ツール」**タブを開き、**「データベース・アクション」**をクリックします。ブラウザでポップアップウィンドウが許可されていることを確認します。

![adbコンソール](images/adb-console.jpg)

「ユーザー名」に**ADMIN**と入力して、次に進みます。

![ログイン-1](images/login-1.jpg)

パスワード(演習2で設定)を入力し、サインインします。

![ログイン-2](images/login-2.jpg)

**ADMIN**ユーザーとしてログインしたら、**「SQL」**メニューに移動します。

![データベース・アクション](images/database-actions.jpg)

## タスク2: データベース・ロールの作成

ここで、グラフ機能に必要なロールを作成します。SQLワークシートに次のコマンドを入力し、管理ユーザーとして接続しながら実行します。

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
    

ロール**GRAPH\_ADMINISTRATOR**および**GRAPH\_DEVELOPER**にデフォルト権限を割り当てて、複数の権限をグループ化します。

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
    

## タスク3: データベース・ユーザーの作成

ここで、**CUSTOMER\_360**ユーザーを作成し、このユーザーにデータベース・アクション・アクセス権を提供します。

メイン・メニューを開き、「データベース・ユーザー」をクリックします。

![ユーザー-1](images/user-1.jpg)

**「ユーザーの作成」**ボタンをクリックし、ユーザー名とパスワードを入力します。**「Webアクセス」**を有効にし、割当て制限を**「UNLILMITED」**に設定します。

![ユーザー-2](images/user-2.png)

「**Granted Roles**」タブに移動し、このユーザーに **`GRAPH_DEVELOPER`**役割と **`PGX_SESSION_ADD_PUBLISHED_GRAPH`**役割を付与します(デフォルトでは、2つの役割 **CONNECT**と **RESOURCE**が選択されています)。必ずチェックを入れておいてください(^^)

![ユーザー-3](images/user-3.png)

**「ユーザーの作成」**に進み、ログイン・ウィンドウを開きます。

![ユーザー-4](images/user-4.jpg)

新しいユーザーでログインできることを確認します。

![ユーザー-5](images/user-5.jpg)

詳細は、ドキュメントの[「データベース・ユーザーへのデータベース・アクションのアクセス権の付与」](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA)の項を参照してください。

次の演習に進むことができます。

## 謝辞

*   **著者** - Spatial and Graph、製品マネージャ、Jayant Sharma
*   **貢献者** - Arabella Yao、Jenny Tsai
*   **最終更新者/日付** - 山中亮太、2023年3月