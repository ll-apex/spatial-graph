# 创建和填充表

## 简介

在本练习中，您将以 `CUSTOMER_360` 用户身份登录。您将学习如何清除以前的表、创建新表以及如何使用数据填充表。

您将创建 7 个表（客户、账户、商户、购买、转移、parent\_of）。下面显示了这些表的实体关系图。

![er 图](images/er-diagram.jpg)

估计时间：7 分钟

### 目标

*   了解如何使用 Database Actions 连接到新的 Autonomous Database
*   了解如何使用 SQL 创建表和插入数据

### 先备条件

*   此实验室假设您已成功完成实验 - 创建并启用 Database Actions 中的用户。

## 任务 1：登录到 Database Actions

使用您在创建用户时输入的密码以 `CUSTOMER_360` 身份登录。Database Actions 的正确 URL 应包含 `/customer_360/`

![登录 -c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## 任务 2：删除现有表（如果有）

要确保幻灯片清晰，请删除任何现有表。将以下命令复制、粘贴并执行到 SQL 工作表中。

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![删除表](images/drop-table.jpg)

## 任务 3：创建并填充 `ACCOUNT` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

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
    

![创建表](images/create-table.jpg)

## 任务 4：创建并填充 `CUSTOMER` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

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
    

## 任务 5：创建并填充 `MERCHANT` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

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
    

## 任务 7：创建并填充 `PARENT_OF` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## 任务 8：创建并填充 `PURCHASED` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

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
    

## 任务 9：创建并填充 `TRANSFER` 表

清除 SQL 工作表。复制、粘贴并运行以下 SQL 脚本。

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
    

现在，您可以进入下一个实验室。

## 确认

*   **作者** - Spatial and Graph 产品经理 Jayant Sharma
*   **贡献者** - Jenny Tsai、Arabella Yao
*   **上次更新者/日期** - Ryota Yamanaka，2023 年 3 月