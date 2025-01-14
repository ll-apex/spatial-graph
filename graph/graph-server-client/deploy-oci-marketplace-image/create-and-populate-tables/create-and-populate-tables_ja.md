# 表の作成および移入

## 概要

この演習では、ユーザー`CUSTOMER_360`としてログインします。前の表のクリア、新しい表の作成、および表にデータを移入する方法を学習します。

7つの表(顧客、アカウント、業者、購入、転送、parent\_of)を作成します。これらの表のエンティティ関係図を次に示します。

![er- 図](images/er-diagram.jpg)

所要時間:7分

### 目標

*   データベース・アクションを使用して新しいAutonomous Databaseに接続する方法を学習します
*   SQLを使用した表の作成およびデータの挿入方法の学習

### 前提条件

*   この演習では、演習「データベース・アクション」でユーザーの作成と有効化を正常に完了していることを前提としています。

## タスク1: データベース・アクションへのログイン

ユーザーの作成時に入力したパスワードを使用して、`CUSTOMER_360`としてログインします。データベース・アクションの正しいURLには、`/customer_360/`が含まれている必要があります

![ログイン- c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## タスク2: 既存の表の削除(存在する場合)

スレートをきれいにするには、既存の表を削除します。SQLワークシートに次のコマンドをコピーして貼り付け、実行します。

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![ドロップテーブル](images/drop-table.jpg)

## タスク3: `ACCOUNT`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE account (
      id NUMBER NOT NULL
    , account_no VARCHAR2(20)
    , customer_id NUMBER
    , open_date VARCHAR2(20)
    , balance NUMBER
    , CONSTRAINT account_pk PRIMARY KEY (id)
    );
    
    INSERT INTO account VALUES (201,'xxx-yyy-201',101,'2015-10-04',1500);
    INSERT INTO account VALUES (202,'xxx-yyy-202',102,'2012-09-13',200);
    INSERT INTO account VALUES (203,'xxx-yyy-203',103,'2016-02-04',2100);
    INSERT INTO account VALUES (204,'xxx-yyy-204',104,'2018-01-05',100);
    INSERT INTO account VALUES (211,'xxx-zzz-211',NULL,NULL,NULL);
    INSERT INTO account VALUES (212,'xxx-zzz-212',NULL,NULL,NULL);
    COMMIT;
    </copy>
    

![作成テーブル](images/create-table.jpg)

## タスク4: `CUSTOMER`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE customer (
      id NUMBER NOT NULL,
      name VARCHAR2(20),
      age NUMBER,
      location VARCHAR2(20),
      gender VARCHAR2(20),
      student VARCHAR2(20)
    , CONSTRAINT customer_pk PRIMARY KEY (id)
    );
    
    INSERT INTO customer VALUES (101,'John',10,'Boston',NULL,NULL);
    INSERT INTO customer VALUES (102,'Mary',NULL,NULL,'F',NULL);
    INSERT INTO customer VALUES (103,'Jill',NULL,'Boston',NULL,NULL);
    INSERT INTO customer VALUES (104,'Todd',NULL,NULL,NULL,'true');
    COMMIT;
    </copy>
    

## タスク5: `MERCHANT`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE merchant (
      id NUMBER NOT NULL
    , name VARCHAR2(20)
    , CONSTRAINT merchant_pk PRIMARY KEY (id)
    );
    
    INSERT INTO merchant VALUES (301,'Apple Store');
    INSERT INTO merchant VALUES (302,'PC Paradise');
    INSERT INTO merchant VALUES (303,'Kindle Store');
    INSERT INTO merchant VALUES (304,'Asia Books');
    INSERT INTO merchant VALUES (305,'ABC Travel');
    COMMIT;
    </copy>
    

## タスク7: `PARENT_OF`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## タスク8: `PURCHASED`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE purchased (
      id NUMBER
    , account_id NUMBER
    , merchant_id NUMBER
    , amount NUMBER
    , CONSTRAINT purchased_pk PRIMARY KEY (id)
    );
    
    INSERT INTO purchased VALUES (1001,201,301,800);
    INSERT INTO purchased VALUES (1002,201,302,15);
    INSERT INTO purchased VALUES (1003,202,301,150);
    INSERT INTO purchased VALUES (1004,202,302,20);
    INSERT INTO purchased VALUES (1005,202,304,10);
    INSERT INTO purchased VALUES (1006,203,301,350);
    INSERT INTO purchased VALUES (1007,203,302,20);
    INSERT INTO purchased VALUES (1008,203,303,15);
    INSERT INTO purchased VALUES (1009,204,303,10);
    INSERT INTO purchased VALUES (1010,204,304,15);
    INSERT INTO purchased VALUES (1011,204,305,450);
    COMMIT;
    </copy>
    

## タスク9: `TRANSFER`表の作成および移入

SQLワークシートをクリアします。次のSQLスクリプトをコピー、貼り付け、実行します。

    <copy>
    CREATE TABLE transfer (
      id NUMBER
    , account_id_from NUMBER
    , account_id_to NUMBER
    , amount NUMBER
    , transfer_date VARCHAR2(20)
    , CONSTRAINT transfer_pk PRIMARY KEY (id)
    );
    
    INSERT INTO transfer VALUES (100001,201,202,200,'2018-10-05');
    INSERT INTO transfer VALUES (100002,211,202,900,'2018-10-06');
    INSERT INTO transfer VALUES (100003,202,212,850,'2018-10-06');
    INSERT INTO transfer VALUES (100004,201,203,500,'2018-10-07');
    INSERT INTO transfer VALUES (100005,203,204,450,'2018-10-08');
    INSERT INTO transfer VALUES (100006,204,201,400,'2018-10-09');
    INSERT INTO transfer VALUES (100007,202,203,100,'2018-10-10');
    INSERT INTO transfer VALUES (100008,202,201,300,'2018-10-10');
    COMMIT;
    </copy>
    

次の演習に進むことができます。

## 確認

*   **著者** - Spatial and Graph、製品マネージャ、Jayant Sharma
*   **貢献者** - Jenny Tsai、Arabella Yao
*   **最終更新者/日付** - 山中亮太、2023年3月