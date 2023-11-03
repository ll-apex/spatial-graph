# Graph-Benutzer erstellen

## Einführung

In dieser Übung erstellen Sie einen Datenbankbenutzer mit den entsprechenden Rollen und Berechtigungen, die für die Verwendung der Diagrammfunktionen von Autonomous Database erforderlich sind.

Geschätzte Zeit: 5 Minuten.

Sehen Sie sich das Video unten an, um einen kurzen Spaziergang durch das Labor zu machen.

[Link zum Video dieses Workshops](youtube:CQh8Q24Rboc)

### Ziele

Vorgehensweise

*   Datenbankbenutzer mit den entsprechenden Rollen und Berechtigungen erstellen, die für den Zugriff auf **Graph Studio** erforderlich sind

### Voraussetzungen

*   Für die folgende Übung ist ein Account für Autonomous Data Warehouse - Shared Infrastructure oder Autonomous Transaction Processing - Shared Infrastructure erforderlich

## Aufgabe 1: Verbindung zu Database Actions für Ihre Autonomous Database-Instanz herstellen

1.  Öffnen Sie die Detailseite des Service für Ihre Autonomous Database-Instanz in der OCI-Konsole.
    
    Klicken Sie dann auf den Link **Database Actions**, um ihn zu öffnen.
    
    ![Autonomous Database-Homepage mit Verweis auf die Schaltfläche "Database Actions"](images/open-database-actions.png "Autonomous Database-Homepage mit Verweis auf die Schaltfläche "Database Actions"")
    

## Aufgabe 2: Webzugriff und grafisch aktivierten Benutzer erstellen

1.  Melden Sie sich als ADMIN-Benutzer für die Autonomous Database-Instanz an.
    
    ![Bei der Autonomous Database-Instanz anmelden](./images/login.png "Bei der Autonomous Database-Instanz anmelden")
    
2.  Klicken Sie unter **Administration** auf die Kachel **DATABASE USERS**.
    
    ![Klicken Sie auf die Kachel "Datenbankaktionen".](./images/db-actions-users.png "Klicken Sie auf die Kachel "Datenbankaktionen".")
    
3.  Klicken Sie auf das Symbol **\+ Benutzer erstellen**.
    
    ![Klicken Sie auf "Create User".](./images/db-actions-create-user.png "Klicken Sie auf "Create User". ")
    
4.  Geben Sie die erforderlichen Details ein, z.B. Benutzername und Kennwort. Aktivieren Sie die Optionsfelder **Diagramm aktivieren** und **Webzugriff**. Wählen Sie eine Quota, z.B. **UNLIMITED**, die im Tablespace `DATA` zugewiesen werden soll.
    
    Hinweis: Das Kennwort muss den folgenden Anforderungen entsprechen:
    
    *   Das Kennwort muss zwischen 12 und 30 Zeichen umfassen und mindestens einen Großbuchstaben, einen Kleinbuchstaben und ein numerisches Zeichen enthalten.
    *   Das Kennwort kann nicht den Benutzernamen enthalten.
    *   Das Kennwort darf keine doppelten Anführungszeichen (") enthalten.
    *   Das Kennwort muss sich von den letzten 4 Kennwörtern unterscheiden, die für diesen Benutzer verwendet wurden.
    *   Das Kennwort darf nicht mit einem Kennwort übereinstimmen, das vor weniger als 24 Stunden festgelegt wurde.
    
    ![Legen Sie den Benutzernamen und das Kennwort für Graph fest, und wählen Sie {\b Create User}.](images/db-actions-create-graph-user.png "Legen Sie den Benutzernamen und das Kennwort für Graph fest, und wählen Sie {\b Create User}. ")
    
    **Hinweis: Aktivieren Sie den ADMIN-Benutzer nicht als Diagramm, und melden Sie sich nicht als ADMIN-Benutzer bei Graph Studio an. Der ADMIN-Benutzer verfügt standardmäßig über zusätzliche Berechtigungen. Erstellen und verwenden Sie einen Account mit nur den erforderlichen Berechtigungen für die Verwendung mit Diagrammdaten und Analysen.**
    
    Klicken Sie unten im Bereich auf die Schaltfläche **Benutzer erstellen**, um den Benutzer mit den angegebenen Zugangsdaten zu erstellen.
    
    Der neu erstellte Benutzer wird jetzt aufgelistet.
    
    ![Der neu erstellte Benutzer wird aufgelistet](./images/db-actions-user-created.png "Der neu erstellte Benutzer wird aufgelistet ")
    
    **Hinweis:** _Die oben genannten UI-Schritte können stattdessen ausgeführt werden, indem die folgenden SQL-Befehle ausgeführt werden, wenn Sie als ADMIN angemeldet sind. Schritt 5 ist nicht notwendig. Es zeigt eine alternative Möglichkeit zum Erstellen und Aktivieren von GRAPHUSER._
    
5.  Weisen Sie dem neu erstellten Benutzer eine gewünschte Tablespace Quota zu. Öffnen Sie die SQL-Seite, und setzen Sie den Befehl "alter" ab.
    
    Beispiel: `ALTER USER GRAPHUSER QUOTA UNLIMITED ON DATA;`  
    weist dem Benutzer `GRAPHUSER` im Tablespace `DATA` eine Quota zu.  
    Kopieren Sie den folgenden Befehl, und fügen Sie ihn in das SQL-Arbeitsblatt ein.  
    Ersetzen Sie die korrekten Werte für `<username>` und `<quota>`, und klicken Sie auf "Ausführen", um sie auszuführen.
    
        <copy>
        -- Optional statement to use in place of the UI of the Administration page
        ALTER USER <username> QUOTA <quota> ON DATA;
        </copy>
        
    
        <copy>
        -- Optional statements to use in place of the UI of the Administration page
        GRANT GRAPH_DEVELOPER TO <username> ;
        ALTER USER <username> GRANT CONNECT THROUGH "GRAPH$PROXY_USER";
        </copy>
        
    
    Die folgenden Screenshots zeigen ein Beispiel für die Ausführung der ALTER USER-Anweisung.
    
    ![Benutzerquote in 10G ändern](./images/alter-user.png "Benutzerquote in 10G ändern")
    
    ![Anweisung "alter user" ausführen](./images/run-sql.png "Anweisung "alter user" ausführen")
    
    ![Der Benutzer wird in der Skriptausgabe als geändert angezeigt](./images/user-altered.png "Der Benutzer wird in der Skriptausgabe als geändert angezeigt")
    
6.  Auf ähnliche Weise können Sie mit SQL-Anweisungen prüfen, ob GRAPHUSER korrekt eingerichtet wurde.
    
    Sie müssen bei Data Actions SQL als `ADMIN` angemeldet sein, dann die folgenden SQL-Anweisungen eingeben und ausführen.
    
        <copy>
        select * from dba_role_privs where grantee='GRAPHUSER';
        
        select * from dba_proxies where client='GRAPHUSER';
        </copy>
        
    
    Die Ergebnisse sollten die gleichen wie in den Screenshots unten sein.
    
    ![Erteilen Sie dem Diagrammbenutzer Rollen und Berechtigungen](images/graphuser-role-privs.png "Erteilen Sie dem Diagrammbenutzer Rollen und Berechtigungen")
    
    ![Stellvertreter für den Diagrammbenutzer erteilen](images/graphuser-proxy-grant.png "Stellvertreter für den Diagrammbenutzer erteilen")
    

**Fortfahren Sie mit der nächsten Übung**, um zu erfahren, wie Sie Diagramme in ADB erstellen und analysieren.

## Danksagungen

*   **Autor** - Jayant Sharma, Produktmanagement
*   **Mitwirkende** - Korbi Schmid, Rahul Tasker
*   **Zuletzt aktualisiert am/um** - Jayant Sharma, Juni 2023