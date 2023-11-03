# Tabellen erstellen und auffüllen

## Einführung

In dieser Übung melden Sie sich als Benutzer `CUSTOMER_360` an. Sie lernen, wie Sie vorherige Tabellen löschen, neue Tabellen erstellen und die Tabellen mit Ihren Daten füllen.

Sie erstellen 7 Tabellen (Kunde, Konto, Händler, Kauf, Überweisung, parent\_of). Das Entity-Relationship-Diagramm für diese Tabellen wird unten angezeigt.

![er-Diagramm](images/er-diagram.jpg)

Geschätzte Zeit: 7 Minuten

### Ziele

*   Sie erfahren, wie Sie mit Database Actions eine Verbindung zu Ihrer neuen Autonomous Database herstellen.
*   Erfahren Sie, wie Sie Tabellen erstellen und Daten mit SQL einfügen

### Voraussetzungen

*   In dieser Übung wird davon ausgegangen, dass Sie die Übung "Benutzer in Database Actions erstellen und aktivieren" erfolgreich abgeschlossen haben.

## Aufgabe 1: Bei Database Actions anmelden

Melden Sie sich als `CUSTOMER_360` mit dem Kennwort an, das Sie beim Erstellen des Benutzers eingegeben haben. Die korrekte URL für Database Actions muss `/customer_360/` enthalten

![Anmeldung-c360](images/login-c360.jpg)

![sdw-c360](images/sdw-c360.jpg)

## Aufgabe 2: Vorhandene Tabellen löschen, falls vorhanden

Löschen Sie vorhandene Tabellen, um einen sauberen Schiefer zu gewährleisten. Kopieren Sie die folgenden Befehle, fügen Sie sie ein, und führen Sie sie in das SQL Worksheet aus.

    <copy>
    DROP TABLE account;
    DROP TABLE customer;
    DROP TABLE merchant;
    DROP TABLE owned_by;
    DROP TABLE parent_of;
    DROP TABLE purchased;
    DROP TABLE transfer;
    </copy>
    

![Dropdown-Tabelle](images/drop-table.jpg)

## Aufgabe 3: Erstellen und füllen Sie die Tabelle `ACCOUNT`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

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
    

![Erstellen-Tabelle](images/create-table.jpg)

## Aufgabe 4: Erstellen und füllen Sie die Tabelle `CUSTOMER`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

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
    

## Aufgabe 5: Erstellen und füllen Sie die Tabelle `MERCHANT`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

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
    

## Aufgabe 7: Erstellen und füllen Sie die Tabelle `PARENT_OF`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

    <copy>
    CREATE TABLE parent_of (
      customer_id_parent NUMBER
    , customer_id_child NUMBER
    , CONSTRAINT parent_of_pk PRIMARY KEY (customer_id_parent, customer_id_child)
    );
    
    INSERT INTO parent_of VALUES (103,104);
    COMMIT;
    </copy>
    

## Aufgabe 8: Erstellen und füllen Sie die Tabelle `PURCHASED`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

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
    

## Aufgabe 9: Erstellen und füllen Sie die Tabelle `TRANSFER`

Löschen Sie das SQL-Arbeitsblatt. Kopieren Sie das folgende SQL-Skript, fügen Sie es ein, und führen Sie es aus.

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
    

Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - Jayant Sharma, Produktmanager, Spatial and Graph
*   **Mitwirkende** - Jenny Tsai, Arabella Yao
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023