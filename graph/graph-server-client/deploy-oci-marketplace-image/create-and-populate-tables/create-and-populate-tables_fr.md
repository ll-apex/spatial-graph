# Créer et alimenter des tables

## Présentation

Dans cet exercice, vous allez vous connecter en tant qu'utilisateur `CUSTOMER_360`. Vous apprendrez à effacer les tables précédentes, à en créer de nouvelles et à les alimenter avec vos données.

Vous allez créer 7 tables (client, compte, commerçant, acheté, transfert, parent\_of). Le diagramme entité-relation de ces tables est présenté ci-dessous.

![er-diagramme](images/er-diagram.jpg)

Temps estimé : 7 minutes

### Objectifs

*   Découvrez comment vous connecter à votre nouvelle instance Autonomous Database à l'aide de Database Actions
*   Apprendre à créer des tables et à insérer des données à l'aide de SQL

### Prérequis

*   Cet exercice suppose que vous avez terminé l'exercice : Créer et activer un utilisateur dans Database Actions.

## Tâche 1 : se connecter à Database Actions

Connectez-vous en tant que `CUSTOMER_360` à l'aide du mot de passe que vous avez saisi lors de la création de l'utilisateur. L'URL correcte pour Database Actions doit contenir `/customer_360/`

![connexion-c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## Tâche 2 : supprimer les tables existantes, le cas échéant

Pour garantir une ardoise propre, supprimez toutes les tables existantes. Copiez, collez et exécutez les commandes suivantes dans SQL Worksheet.

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![supprimer une table](images/drop-table.jpg)

## Tâche 3 : créer et remplir la table `ACCOUNT`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

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
    

![créer-table](images/create-table.jpg)

## Tâche 4 : créer et alimenter la table `CUSTOMER`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

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
    

## Tâche 5 : créer et remplir la table `MERCHANT`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

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
    

## Tâche 7 : créer et remplir la table `PARENT_OF`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## Tâche 8 : créer et alimenter la table `PURCHASED`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

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
    

## Tâche 9 : créer et alimenter la table `TRANSFER`

Effacez la feuille de calcul SQL. Copiez, collez et exécutez le script SQL suivant.

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
    

Vous pouvez maintenant passer à l'exercice suivant.

## Accusés de réception

*   **Auteur** - Jayant Sharma, chef de produit, Spatial and Graph
*   **Contributeurs** - Jenny Tsai, Arabella Yao
*   **Dernière mise à jour par/date** - Ryota Yamanaka, mars 2023