# Graph Studio: Daten aus CSV-Dateien in Tabellen laden

## Einführung

In dieser Übung laden Sie zwei CSV-Dateien mit der Database Actions-Schnittstelle Ihrer Oracle Autonomous Data Warehouse- oder Oracle Autonomous Transaction Processing-Instanz in die entsprechenden Tabellen.

Geschätzte Zeit: 10 Minuten.

Sehen Sie sich das Video unten an, um einen kurzen Spaziergang durch das Labor zu machen.

[](youtube:wkKKO-RO0lA)

### Ziele

Vorgehensweise

*   CSV-Dateien mit Database Actions in Autonomous Database laden

### Voraussetzungen

*   Für die folgende Übung ist ein Oracle Autonomous Database-Account erforderlich.
*   Es wird davon ausgegangen, dass ein Benutzer mit aktiviertem Graph und Webzugriff vorhanden ist. Das heißt, es ist ein Datenbankbenutzer mit den richtigen Rollen und Berechtigungen vorhanden, der sich bei Database Actions anmelden kann.

## Aufgabe 1: Verbindung zu Database Actions für Ihre Autonomous Database-Instanz herstellen

1.  Öffnen Sie die Detailseite des Service für Ihre Autonomous Database-Instanz in der Oracle Cloud-Konsole.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](images/open-database-actions.png " ")
    
2.  Klicken Sie auf **Database Actions**, um sie zu öffnen.
    

## Aufgabe 2: Als grafikfähiger Benutzer anmelden

1.  Melden Sie sich als Graphbenutzer (z.B. `GRAPHUSER`) für Ihre Autonomous Database-Instanz an.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-graphuser-login.png " ")
    
    > **Hinweis:** _Falls erforderlich, gehen Sie wie folgt vor, um den Benutzer mit den richtigen Rollen und Berechtigungen zu erstellen_:
    
    *   Melden Sie sich als **ADMIN**\-Benutzer für Autonomous Database bei Database Actions an.
    *   Wählen Sie im Navigationsmenü die Optionen **Administration** und **Database Users**.
    *   Klicken Sie auf **Benutzer erstellen**.
    *   Aktivieren Sie die Schaltflächen **Webzugriff** und **Diagramm**

## Aufgabe 3: Laden Sie die Beispieldatensätze aus ObjectStore herunter

1.  Kopieren Sie die URL, und fügen Sie sie in Ihren Browser für das ZIP-Archiv ein.
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    Sie können auch `wget` oder `curl` verwenden, um die Beispieldaten auf Ihren Computer herunterzuladen.  
    Sie können eine `curl`\-Beispielanforderung kopieren und einfügen:
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  **Dekomprimieren** Sie das Archiv in einem lokalen Verzeichnis wie ~/downloads.
    

## Aufgabe 4: Mit Database Actions Data Load hochladen

1.  Klicken Sie auf die Karte **DATENLADEN**.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](images/db-actions-dataload-card.png " ")
    
    Geben Sie dann den Speicherort Ihrer Daten an. Stellen Sie also sicher, dass die Karten **Daten laden** und **Lokale Datei** ein Häkchen enthalten. Klicken Sie auf **Weiter**.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-dataload-location.png)
    
2.  Klicken Sie auf **Dateien auswählen**.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](images/db-action-dataload-file-browser.png " ")
    
    Navigieren Sie zum richtigen Ordner (z.B. ~/downloads/random-acct-data), und wählen Sie die Dateien `bank_accounts.csv` und `bank_txns.csv` aus.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-dataload-choose-files.png " ")
    
3.  Prüfen Sie, ob die korrekten Dateien ausgewählt wurden, und klicken Sie auf das Symbol **Ausführen**. ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-dataload-click-run.png " ")
    
4.  Bestätigen Sie, dass der Dataload-Job gewünscht wird.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-dataload-confirm-run.png " ")
    
5.  Nachdem die Dateien geladen wurden
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/dbactions-dataload-files-loaded.png " ")
    
    Klicken Sie auf **Fertig**, um den Vorgang zu beenden.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](images/dbactions-click-done.png " ")
    
6.  Öffnen Sie jetzt das **SQL**\-Arbeitsblatt. ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-choose-sql-card.png " ")
    
7.  Navigieren Sie zum richtigen Ordner (z.B. ~/downloads), wählen Sie die Datei `fixup.SQL` aus, und ziehen Sie sie in das SQL-Arbeitsblatt.
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    Wenn Sie jedoch copy-n-paste bevorzugen, lautet der Inhalt von `fixup.sql`:
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    Es umfasst folgende Inhalte:
    
    *   Fügt der Tabelle `bank_accounts` ein Primärschlüssel-Constraint hinzu
    *   Fügt der Tabelle `bank_txns` eine Spalte (`txn_id`) hinzu
    *   Legt einen Wert für `txn_id` fest und schreibt die Transaktion fest
    *   Fügt der Tabelle `bank_txns` ein Primärschlüssel-Constraint hinzu
    *   Fügt der Tabelle `bank_txns` ein Fremdschlüssel-Constraint hinzu, das angibt, dass `from_acct_id` `bank_accounts.acct_id` referenziert
    *   Fügt der Tabelle `bank_txns` ein zweites Fremdschlüssel-Constraint hinzu, das angibt, dass `to_acct_id` `bank_accounts.acct_id` referenziert
    *   Damit können Sie prüfen, ob eine `txn_id`\-Spalte und die Constraints hinzugefügt werden
8.  Führen Sie das Skript `fixup.SQL` im SQL-Arbeitsblatt aus.  
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-sql-execute-fixup.png " ")
    
9.  Die Skriptausgabe sollte wie folgt aussehen:
    
    ![Für dieses Bild ist kein ALT-Text verfügbar](./images/db-actions-sql-script-output.png " ")
    
    **Fortfahren Sie mit der nächsten Übung**, um ein Diagramm aus diesen Tabellen zu erstellen.
    

## Danksagungen

*   **Autor** - Jayant Sharma, Produktmanagement
*   **Mitwirkende** - Jayant Sharma, Produktmanagement
*   **Zuletzt aktualisiert am/um** - Jayant Sharma, Produktmanagement, Februar 2022