# 테이블 생성 및 채우기

## 소개

이 연습에서는 `CUSTOMER_360` 유저로 로그인합니다. 이전 테이블을 지우고, 새 테이블을 생성하고, 데이터로 테이블을 채우는 방법을 배웁니다.

7개 테이블(고객, 계정, 가맹점, 구매, 이전, parent\_of)을 생성합니다. 이러한 테이블에 대한 엔티티 관계 다이어그램은 다음과 같습니다.

![ER 다이어그램](images/er-diagram.jpg)

예상 시간: 7분

### 목표

*   Database Actions를 사용하여 새 Autonomous Database에 접속하는 방법 알아보기
*   SQL을 사용하여 테이블을 생성하고 데이터를 삽입하는 방법 학습

### 필요 조건

*   이 실습에서는 Database Actions에서 Create and enable a user라는 실습을 성공적으로 완료했다고 가정합니다.

## 작업 1: Database Actions에 로그인

사용자를 생성할 때 입력한 비밀번호를 사용하여 `CUSTOMER_360`로 로그인합니다. Database Actions의 올바른 URL에 `/customer_360/`이 포함되어야 합니다.

![로그인-c360](images/login-c360.jpg)

![sdw-c360 ](images/sdw-c360.jpg)

## 작업 2: 기존 테이블 삭제(있는 경우)

슬레이트를 지우려면 기존 테이블을 삭제합니다. 다음 명령을 복사하여 SQL Worksheet에 붙여 넣은 후 실행합니다.

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![드롭 테이블](images/drop-table.jpg)

## 작업 3: `ACCOUNT` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

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
    

![테이블 생성](images/create-table.jpg)

## 작업 4: `CUSTOMER` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

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
    

## 작업 5: `MERCHANT` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

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
    

## 작업 7: `PARENT_OF` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## 작업 8: `PURCHASED` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

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
    

## 작업 9: `TRANSFER` 테이블 생성 및 채우기

SQL Worksheet를 지웁니다. 다음 SQL 스크립트를 복사, 붙여넣기 및 실행합니다.

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
    

이제 다음 실습을 진행할 수 있습니다.

## 확인

*   **작성자** - Jayant Sharma, Spatial and Graph 제품 관리자
*   **기여자** - Jenny Tsai, Arabella Yao
*   **최종 업데이트 수행자/날짜** - Ryota Yamanaka, 2023년 3월