# Graph Studio: Diagramm mit der Anweisung PGQL CREATE PROPERTY GRAPH erstellen

## Einführung

In dieser Übung erstellen Sie ein Diagramm aus den Tabellen `bank_accounts` und `bank_txns` mit Graph Studio und der Anweisung CREATE PROPERTY GRAPH.

Geschätzte Zeit: 15 Minuten.

Sehen Sie sich das Video unten an, um einen schnellen Durchgang des Labors zu erhalten. [Kamerafahrt](videohub:1_jguolqf3)

### Ziele

Vorgehensweise

*   Verwenden Sie GRAPH Studio und PGQL DDL (also CREATE PROPERTY GRAPH-Anweisung), um ein Diagramm aus vorhandenen Tabellen oder Ansichten zu modellieren und zu erstellen.

### Voraussetzungen

*   Für die folgende Übung ist eine serverlose Autonomous Database-Instanz erforderlich.
*   Und dass der Graph-fähige Benutzer (`GRAPHUSER`) vorhanden ist. Das heißt, es ist ein Datenbankbenutzer mit den richtigen Rollen und Berechtigungen vorhanden.

## Aufgabe 1: Auf Autonomous Database zugreifen

1.  Klicken Sie oben links auf das **Navigationsmenü**, navigieren Sie zu **Oracle Database**, und wählen Sie **Autonomous Database** aus.
    
    ![Zu Autonomous Database navigieren.](images/navigation-menu.png " ")
    
2.  Wählen Sie das Compartment unter **Anmeldeinformationen anzeigen** aus, und klicken Sie auf den **Anzeigenamen** für **Autonomous Database**.
    
    ![Autonomous Database im Navigationsmenü auswählen](images/select-autonomous-database.png " ")
    

## Aufgabe 2: Bei Graph Studio anmelden

Graph Studio ist ein Feature von Autonomous Database. Sie ist als Option im Database Actions-Launchpad verfügbar. Sie benötigen einen grafikfähigen Benutzer, um sich bei Graph Studio anzumelden. Dieser Benutzer wurde bereits für Sie erstellt.

1.  Klicken Sie auf der Seite **Autonomous Database-Details** auf die Schaltfläche **Datenbankaktionen**, und wählen Sie **Alle Datenbankaktionen anzeigen** aus.
    
    ![Klicken Sie auf die Schaltfläche "Database Actions".](images/click-database-actions.png " ")
    
2.  Klicken Sie im Bereich "Datenbankaktionen" auf **Graph Studio**.
    
    ![Klicken Sie auf "Open Graph Studio".](images/graphstudiofixed.png " ")
    
3.  Melden Sie sich bei Graph Studio an. Verwenden Sie die Zugangsdaten für den Datenbankbenutzer GRAPHUSER.
    
    ![Zugangsdaten für Datenbankbenutzer MOVIESTREAM verwenden](images/graph-login.png " ")
    
    Graph Studio besteht aus einer Gruppe von Seiten, auf die über das Menü auf der linken Seite zugegriffen wird.
    
    Mit dem Symbol **Home** gelangen Sie zur Homepage.  
    Auf der Seite **Diagramm** werden vorhandene Diagramme zur Verwendung in Notizbüchern aufgeführt.  
    Auf der Seite **Notizbuch** werden vorhandene Notizbücher aufgeführt, und Sie können ein neues erstellen.  
    Auf der Seite **Vorlagen** können Sie Vorlagen für die Diagrammvisualisierungen erstellen.  
    Auf der Seite **Jobs** wird der Status von Hintergrundjobs aufgeführt. Sie können das zugehörige Log gegebenenfalls anzeigen.  
    

## Aufgabe 3: Erstellen eines Diagramms mit Konten und Transaktionen

1.  Klicken Sie auf das Symbol **Diagramm**. Klicken Sie dann auf **Diagramm erstellen**.
    
    ![Zeigt, wo sich der Modellierer der Schaltfläche "Erstellen" befindet](images/graph-create-button.png " ")
    
2.  Geben Sie `bank_graph` als Diagrammnamen ein, und klicken Sie auf **Weiter**. Die Felder "Beschreibung" und "Tags" sind optional.  
    Dieser Diagrammname wird in der nächsten Übung verwendet.  
    Geben Sie keinen anderen Namen ein, da die Abfragen und Code-Snippets in der nächsten Übung nicht erfolgreich verlaufen.
    
    ![Zeigt das Fenster "Diagramm erstellen" an, in dem Sie dem Diagramm einen Namen zuweisen](./images/create-graph-dialog.png " ")
    
3.  Blenden Sie **GRAPHUSER** ein, und wählen Sie die Tabellen `BANK_ACCOUNTS` und `BANK_TXNS` aus.
    
    ![Zeigt, wie Sie BANK_ACCOUNTS und BANK_TXNS auswählen](./images/select-tables.png " ")
    
4.  Verschieben Sie sie nach rechts, d.h. klicken Sie auf das erste Symbol im Shuttle-Steuerelement.
    
    ![Zeigt die ausgewählten Tabellen an](./images/selected-tables.png " ")
    
5.  Klicken Sie auf **Weiter**. Wir bearbeiten und aktualisieren dieses Diagramm, um eine Kante und ein Scheitel-Label hinzuzufügen.
    
    Das vorgeschlagene Diagramm hat `BANK_ACCOUNTS` als Scheiteltabelle, da für `BANK_TXNS` Fremdschlüssel-Constraints angegeben sind, die es referenzieren.
    
    `BANK_TXNS` ist eine empfohlene Edge-Tabelle.
    
    ![Zeigt den Scheitelpunkt und die Randtabelle an](./images/create-graph-suggested-model.png " ")
    
6.  Ändern wir nun die Standardbeschriftungen Vertex und Edge.
    
    Klicken Sie auf die Scheiteltabelle `BANK_ACCOUNTS`. Ändern Sie das Scheitellabel in **ACCOUNTS**. Klicken Sie dann auf das Häkchen, um das Label zu bestätigen und das Update zu speichern.
    
    ![Label-Name des Scheitels in "Konten" geändert](images/edit-accounts-vertex-label.png " ")
    
    Klicken Sie auf die Edge-Tabelle `BANK_TXNS`, und benennen Sie das Edge-Label von `BANK_TXNS` in **TRANSFERS** um. Klicken Sie dann auf das Häkchen, um das Label zu bestätigen und das Update zu speichern.
    
    ![Label-Name der Edge in "Transfers" geändert](images/edit-edge-label.png " ")
    
    Dies ist **wichtig**, da wir diese Edge-Labels in der nächsten Übung dieses Workshops bei der Abfrage des Diagramms verwenden werden. Klicken Sie auf **Weiter**.
    

7.  Klicken Sie im Schritt "Zusammenfassung" auf **Diagramm erstellen**.
    
    ![Zeigt die Registerkarte "Job" mit dem Jobstatus "Erfolgreich" an](./images/jobs-create-graph.png " ")
    
    Daraufhin wird die Registerkarte "Graph erstellen" geöffnet, und klicken Sie auf **Graph erstellen**.
    
    ![Zeigt In-Memory-fähige und die Schaltfläche "Diagramm erstellen" an](./images/create-graph-in-memory.png " ")
    
    Danach gelangen Sie zur Seite "Jobs", auf der das Diagramm erstellt wird.
    
    Damit endet diese Übung. **Jetzt können Sie mit der nächsten Übung fortfahren.**
    

## Danksagungen

*   **Autor** - Jayant Sharma, Produktmanagement
*   **Mitwirkende** - Jayant Sharma, Produktmanagement
*   **Zuletzt aktualisiert am/um** - Ramu Murakami Gutierrez, Produktmanager, Juni 2023