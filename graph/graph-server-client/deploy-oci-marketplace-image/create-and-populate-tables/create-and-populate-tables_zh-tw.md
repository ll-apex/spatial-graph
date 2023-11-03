# 建立並植入表格

## 簡介

在此實驗室中，您將以 `CUSTOMER_360` 使用者身分登入。您將會瞭解如何清除先前的表格、建立新表格，並將資料植入表格。

您將建立 7 個表格 (客戶、帳戶、特約商店、採購、移轉、parent\_of)。下面顯示這些表格的實體關係圖。

![er-diagram - 企業資源規劃](images/er-diagram.jpg)

估計時間：7 分鐘

### 目標

*   瞭解如何使用資料庫動作連線至新的 Autonomous Database
*   瞭解如何使用 SQL 建立表格及插入資料

### 先決條件

*   此實驗室假設您已順利完成實驗室 - 建立並啟用「資料庫動作」中的使用者。

## 作業 1：登入資料庫動作

使用您在建立使用者時所輸入的密碼登入為 `CUSTOMER_360`。資料庫動作的正確 URL 應包含 `/customer_360/`

![登入 -c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## 作業 2：刪除現有表格 (若有的話)

如果要確保不會清空表格，請刪除任何現有表格。將下列命令複製、貼上並執行「SQL 工作表」。

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![下拉式表](images/drop-table.jpg)

## 作業 3：建立並填入 `ACCOUNT` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

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
    

![建立表](images/create-table.jpg)

## 作業 4：建立並填入 `CUSTOMER` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

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
    

## 作業 5：建立並填入 `MERCHANT` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

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
    

## 作業 7：建立並填入 `PARENT_OF` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## 作業 8：建立並填入 `PURCHASED` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

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
    

## 作業 9：建立並填入 `TRANSFER` 表格

清除「SQL 工作表」。複製、貼上並執行下列 SQL 命令檔。

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
    

您現在可以繼續下一個實驗室。

## 確認

*   **作者** - Spatial and Graph 產品經理 Jayant Sharma
*   **貢獻者** - Arabella Yao Jenny Tsai
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月