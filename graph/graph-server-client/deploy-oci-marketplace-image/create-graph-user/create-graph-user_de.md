# Datenbankbenutzer in Database Actions erstellen und aktivieren

## Einführung

In dieser Übung werden Sie durch die Schritte zu den ersten Schritten mit Database Actions geführt. Sie lernen, wie Sie einen Benutzer in Database Actions erstellen und diesem Benutzer den Zugriff auf Database Actions erteilen.

Geschätzte Zeit: 3 Minuten

### Ziele

*   Erfahren Sie, wie Sie die erforderlichen Datenbankrollen in Database Actions einrichten.
*   Erfahren Sie, wie Sie einen Datenbankbenutzer in Database Actions erstellen.

### Voraussetzungen

*   Oracle-Cloud-Account
*   Bereitgestellte Autonomous Database

## Aufgabe 1: Bei Database Actions anmelden

Melden Sie sich als Admin-Benutzer in Database Actions der neu erstellten ADB-Instanz an.

Klicken Sie oben links auf das **Navigationsmenü**, navigieren Sie zu **Oracle Database**, und wählen Sie **Autonomous Transaction Processing** aus.

![datenbank-atp](https://oracle-livelabs.github.io/common/images/console/database-atp.png)

Öffnen Sie auf der Seite "Autonomous Database-Details" die Registerkarte **Tools**, und klicken Sie auf **Database Actions**. Stellen Sie sicher, dass Ihr Browser Pop-up-Fenster zulässt.

![adb-Konsole](images/adb-console.jpg)

Geben Sie **ADMIN** als Benutzernamen ein, und gehen Sie als Nächstes.

![Anmeldung-1](images/login-1.jpg)

Geben Sie das Passwort ein (Sie haben es in Übung 2 eingerichtet), und melden Sie sich an.

![Anmeldung-2](images/login-2.jpg)

Gehen Sie zum Menü **SQL**, nachdem Sie sich als **ADMIN**\-Benutzer angemeldet haben.

![Datenbankaktionen](images/database-actions.jpg)

## Taks 2: Datenbankrollen erstellen

Erstellen Sie jetzt die Rollen, die für die Diagrammfunktion erforderlich sind. Geben Sie die folgenden Befehle in das SQL Worksheet ein, und führen Sie sie aus, während Sie als Admin-Benutzer angemeldet sind.

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
    

Weisen Sie den Rollen **GRAPH\_ADMINISTRATOR** und **GRAPH\_DEVELOPER** die Standardberechtigungen zu, um mehrere Berechtigungen zu gruppieren.

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
    

## Aufgabe 3: Datenbankbenutzer erstellen

Erstellen Sie jetzt den Benutzer **CUSTOMER\_360**, und erteilen Sie diesem Benutzer Database Actions-Zugriff.

Öffnen Sie das Hauptmenü und klicken Sie auf "Datenbankbenutzer".

![Benutzer-1](images/user-1.jpg)

Klicken Sie auf die Schaltfläche **Benutzer erstellen**, und geben Sie den Benutzernamen und das Kennwort ein. Aktivieren Sie den **Webzugriff**, und setzen Sie die Quota auf **UNLILMITED**.

![Benutzer-2](images/user-2.png)

Gehen Sie zur Registerkarte **Erteilte Rollen**, und erteilen Sie diesem Benutzer die Rolle **`GRAPH_DEVELOPER`** und die Rolle **`PGX_SESSION_ADD_PUBLISHED_GRAPH`**. (Zwei Rollen **CONNECT** und **RESOURCE** sind standardmäßig ausgewählt. Bitte lassen Sie sie überprüfen, damit sie auch gewährt werden.)

![Benutzer-3](images/user-3.png)

Fahren Sie mit **Benutzer erstellen** fort, und öffnen Sie das Anmeldefenster.

![Benutzer-4](images/user-4.jpg)

Bestätigen Sie, dass Sie sich beim neuen Benutzer anmelden können.

![Benutzer-5](images/user-5.jpg)

Einzelheiten finden Sie in der Dokumentation im Abschnitt ["Datenbankbenutzern Zugriff auf Database Actions erteilen"](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/sql-developer-web.html#GUID-4B404CE3-C832-4089-B37A-ADE1036C7EEA).

Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - Jayant Sharma, Produktmanager, Spatial and Graph
*   **Mitwirkende** - Arabella Yao, Jenny Tsai
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023