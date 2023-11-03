# Criar e Preencher Tabelas

## Introdução

Neste laboratório, você fará log-in como usuário `CUSTOMER_360`. Você aprenderá a limpar tabelas anteriores, criar novas tabelas e preenchê-las com seus dados.

Você criará 7 tabelas (cliente, conta, comerciante, comprado, transferência, parent\_of). O diagrama de entidade-relacionamento dessas tabelas é mostrado abaixo.

![er-diagrama](images/er-diagram.jpg)

Tempo estimado: 7 minutos

### Objetivos

*   Saiba como estabelecer conexão com seu novo Autonomous Database usando o Database Actions
*   Aprender a criar tabelas e inserir dados usando SQL

### Pré-requisitos

*   Este laboratório pressupõe que você tenha concluído com sucesso o laboratório - Crie e ative um usuário no Database Actions.

## Tarefa 1: Fazer Log-in no Database Actions

Faça log-in como `CUSTOMER_360` usando a senha informada ao criar o usuário. O URL correto do Database Actions deve conter `/customer_360/`

![login-c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## Tarefa 2: Eliminar tabelas existentes, se houver

Para garantir uma lousa limpa, elimine as tabelas existentes. Copie, cole e execute os comandos a seguir na Planilha SQL.

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![tabela suspensa](images/drop-table.jpg)

## Tarefa 3: Criar e preencher a tabela `ACCOUNT`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

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
    

![criar tabela](images/create-table.jpg)

## Tarefa 4: Criar e preencher a tabela `CUSTOMER`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

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
    

## Tarefa 5: Criar e preencher a tabela `MERCHANT`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

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
    

## Tarefa 7: Criar e preencher a tabela `PARENT_OF`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## Tarefa 8: Criar e preencher a tabela `PURCHASED`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

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
    

## Tarefa 9: Criar e preencher a tabela `TRANSFER`

Limpe a Planilha SQL. Copie, cole e execute o seguinte script SQL.

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
    

Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - Jayant Sharma, Gerente de Produtos, Espacial e Gráfico
*   **Colaboradores** - Jenny Tsai, Arabella Yao
*   **Última Atualização em/Data** - Ryota Yamanaka, março de 2023