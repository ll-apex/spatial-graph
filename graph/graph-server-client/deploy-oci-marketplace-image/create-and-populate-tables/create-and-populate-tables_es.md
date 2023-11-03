# Crear y rellenar tablas

## Introducción

En este laboratorio, se conectará como usuario `CUSTOMER_360`. Aprenderá a borrar las tablas anteriores, crear nuevas tablas y rellenar las tablas con los datos.

Creará 7 tablas (cliente, cuenta, comerciante, comprado, transferencia, parent\_of). A continuación se muestra el diagrama de relación de entidad para estas tablas.

![er-diagrama](images/er-diagram.jpg)

Tiempo estimado: 7 minutos

### Objetivos

*   Descubra cómo conectarse a su nueva instancia de Autonomous Database mediante Database Actions
*   Aprender a crear tablas e insertar datos mediante SQL

### Requisitos

*   En esta práctica de laboratorio se asume que ha completado correctamente la práctica de laboratorio - Crear y activar un usuario en Database Actions.

## Tarea 1: Conexión a Database Actions

Conéctese como `CUSTOMER_360` con la contraseña introducida al crear el usuario. La URL correcta para Database Actions debe contener `/customer_360/`

![inicio de sesión-c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## Tarea 2: Borrar tablas existentes si las hay

Para garantizar una pizarra limpia, suelte las tablas existentes. Copie, pegue y ejecute los siguientes comandos en la hoja de trabajo de SQL.

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![tabla de entrega](images/drop-table.jpg)

## Tarea 3: Crear y rellenar la tabla `ACCOUNT`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

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
    

![tabla de creación](images/create-table.jpg)

## Tarea 4: Crear y rellenar la tabla `CUSTOMER`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

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
    

## Tarea 5: Crear y rellenar la tabla `MERCHANT`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

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
    

## Tarea 7: Crear y rellenar la tabla `PARENT_OF`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## Tarea 8: Crear y rellenar la tabla `PURCHASED`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

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
    

## Tarea 9: Crear y rellenar la tabla `TRANSFER`

Borre la hoja de trabajo de SQL. Copie, pegue y ejecute el siguiente script SQL.

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
    

Ahora puede pasar a la siguiente práctica de laboratorio.

## Reconocimientos

*   **Autor**: Jayant Sharma, mánager de productos, Spatial and Graph
*   **Contribuyentes** - Jenny Tsai, Arabella Yao
*   **Última actualización por/fecha**: Ryota Yamanaka, marzo de 2023