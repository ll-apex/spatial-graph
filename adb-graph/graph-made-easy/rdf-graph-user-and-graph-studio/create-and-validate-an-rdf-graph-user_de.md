# RDF-Graph in Graph Studio erstellen

## Einführung

Mit Graph Studio in Oracle Autonomous Database können Benutzer Diagrammdaten modellieren, erstellen, abfragen und analysieren. Sie umfasst Notizbücher, Entwickler-APIs zur Ausführung von Diagrammabfragen mit PGQL, mehr als 60 integrierte Diagrammalgorithmen und bietet Dutzende von Visualisierungen, einschließlich nativer Diagrammvisualisierung. Zusätzlich zum Eigenschaftsdiagramm erweitert Graph Studio jetzt die Unterstützung für semantische Technologien, einschließlich Speicher-, Inferenz- und Abfragefunktionen für Daten und Ontologien basierend auf Resource Description Framework (RDF) und Web Ontology Language (OWL). Sie können jetzt Graph Studio für die folgenden unterstützten RDF-Features verwenden:

*   RDF-Graph erstellen
*   SPARQL-Abfragen im RDF-Diagramm in einem Notizbuchabsatz ausführen
*   RDF-Diagramme analysieren und visualisieren

Voraussichtliche Zeit: 5 Minuten

Sehen Sie sich das Video unten an, um einen schnellen Durchgang des Labors zu erhalten. [RDF-Diagramm in Graph Studio erstellen](videohub:1_vvqhh26v)

### Ziele

*   RDF-Graph in Graph Studio erstellen
*   RDF-Graph validieren
*   SPARQL-Abfragen auf der Playground-Seite ausführen

### Voraussetzungen

*   Für die folgende Übung ist eine serverlose Autonomous Database-Instanz erforderlich.
*   Und dass der Graph-fähige Benutzer (GRAPHUSER) vorhanden ist. Das heißt, es ist ein Datenbankbenutzer mit den richtigen Rollen und Berechtigungen vorhanden.

## Aufgabe 1: RDF-Graph in Graph Studio erstellen

Wenn Sie die vorherigen Übungen abgeschlossen und derzeit angemeldet sind, führen Sie die folgenden Schritte aus:

1.  Klicken Sie links im Navigationsmenü auf **Diagramme**, um zur Seite "Diagramme" zu navigieren.

![Die Landingpage nach dem Erstellen der Umgebung ist das Menü "Jobs"](./images/graph-studio-home.png)

2.  Wählen Sie im Dropdown-Menü "Diagrammtyp" die Option **RDF**, und klicken Sie in der oberen rechten Ecke der Oberfläche auf die Schaltfläche **Erstellen**.

![Das Dropdown-Menü "Diagrammtyp der Graph Studio-Seite" zeigt PG- und RDF-Diagrammoptionen an](./images/graph-studio-graphs.png)

3.  Wählen Sie **RDF-Diagramm** aus, und klicken Sie auf die Schaltfläche **Bestätigen**.

![Schaltfläche "Bestätigen" zur Auswahl der RDF-Diagrammoption](./images/click-confirm-rdf.png)

4.  Der Assistent zum Erstellen von RDF-Graphen wird wie folgt geöffnet:

![Die Seite "RDF-Graph erstellen".](./images/create-rdf-graph.png)

5.  Geben Sie den OCI Object Storage-URI-Pfad ein:
    
          <copy>https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt
        
6.  Klicken Sie auf **Keine Zugangsdaten**.
    
7.  Klicken Sie auf **Weiter**. Das folgende Dialogfeld sollte angezeigt werden, geben Sie "MOVIESTREAM" als Diagrammnamen ein:
    

![Die zweite Seite "RDF-Diagramm erstellen"](./images/create-rdf-graph-2.png)

8.  Klicken Sie auf **Erstellen**.
    
    Der Job zum Erstellen des RDF-Diagramms wird initiiert. Da die RDF-Datei 139461 Datensätze enthält, kann der Prozess 3 bis 4 Minuten dauern. Sie können den Job auf der Seite **Jobs** in Graph Studio überwachen.
    

![Auf der Seite "Jobs" von Graph Studio wird der Job "Create a RDF Graph - MOVIESTREAM" angezeigt, der noch ausgeführt wird](./images/graph-studio-jobs.png)

    When succeeded, the status will change from pending to succeeded and Logs can be viewed by clicking on the three dots on the right side of the job row and selecting **See Log**. The log for the job displays details as shown below:
    
    ```
    Tue, Mar 1, 2022 08:21:04 AM
    Finished execution of task Graph Creation - MOVIESTREAM.
    
    Tue, Mar 1, 2022 08:21:04 AM
    Graph MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:21:04 AM
    Optimizer Statistics Gathered successfully
    
    Tue, Mar 1, 2022 08:20:50 AM
    External table <graph-user>_TAB_EXTERNAL dropped successfully
    
    Tue, Mar 1, 2022 08:20:49 AM
    Data successfully bulk loaded from ORACLE_ORARDF_STGTAB
    
    Tue, Mar 1, 2022 08:20:39 AM
    Model MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:20:37 AM
    Network RDF_NETWORK created successfully
    
    Tue, Mar 1, 2022 08:20:24 AM
    Data loaded into the staging table ORACLE_ORARDF_STGTAB from <graph-user>_TAB_EXTERNAL
    
    Tue, Mar 1, 2022 08:20:19 AM
    External table <graph-user>_TAB_EXTERNAL created successfully
    
    Tue, Mar 1, 2022 08:20:19 AM
    Using the Credential MOVIES_CREDENTIALS
    
    Tue, Mar 1, 2022 08:20:19 AM
    Started execution of task Graph Creation - MOVIESTREAM.
    ```
    

## Aufgabe 2: RDF-Diagramm validieren

Sie können das neu erstellte RDF-Diagramm auf der Seite **Diagramme** in Graph Studio wie folgt untersuchen und validieren:

1.  Navigieren Sie zur Seite **Diagramme**, und legen Sie den **Diagrammtyp** über das Dropdown-Menü auf "RDF" fest. Wählen Sie die MOVIESTREAM-Diagrammzeile aus den verfügbaren RDF-Diagrammen, Beispielanweisungen (Dreier oder Quads sollten angezeigt werden), verwenden Sie die drei horizontalen Punkte, um die Größe dieser Anweisungen zu ändern und sie anzuzeigen. Beispielanweisungen (Dreier oder Quads) aus dem RDF-Graph werden im unteren Bereich wie folgt angezeigt:

![Beispielanweisungen aus dem RDF-Diagramm "MOVIESTREAM" werden in Triplets angezeigt](./images/graph-sample-statements.png)

2.  Scrollen Sie nach der Auswahl des MOVIESTREAM-Diagramms zum Ende der Seite, und stellen Sie sicher, dass 500 RDF-Dreifachzeilen abgerufen wurden.

![Beispielanweisungen aus dem Diagramm MOVIESTREAM RDF](./images/sample-statements.png)

## Aufgabe 3: SPARQL-Abfragen auf der Spielplatzseite ausführen

Sie können SPARQL-Abfragen im RDF-Diagramm auf der Seite **Abfrage-Playground** ausführen.

1.  Wählen Sie auf der Seite **Diagramme** im Dropdown-Menü "Diagrammtyp" die Option **RDF** aus, und klicken Sie auf die Schaltfläche **Abfrage**, um zur Seite "Abfragespielplatz" zu navigieren.

![Seite "Diagramme" mit ausgewähltem RDF-Diagrammtyp und hervorgehobener Schaltfläche "Abfrage"](./images/graph-type.png)

2.  Wenn Sie mehrere Diagramme in Graph Studio haben, müssen Sie das abzufragende Diagramm auswählen. Wählen Sie im Menü "Diagrammname" die Option "MOVIESTREAM" aus dem Dropdown-Menü.

![Abfragespielplatz zeigt den im Dropdown-Menü ausgewählten Diagrammnamen "MOVIESTREAM" an](./images/query-playground.png)

3.  Führen Sie die folgende Abfrage für das RDF-Diagramm aus.
    
        <copy>PREFIX rdf: &lthttp://www.w3.org/1999/02/22-rdf-syntax-ns#&gt
        PREFIX rdfs: &lthttp://www.w3.org/2000/01/rdf-schema#&gt
        PREFIX xsd: &lthttp://www.w3.org/2001/XMLSchema#&gt
        PREFIX ms: &lthttp://www.example.com/moviestream/&gt
        
        SELECT DISTINCT ?gname
        WHERE {
          ?movie ms:actor/ms:name "Keanu Reeves" ;
          ms:genre/ms:genreName ?gname .
        }
        ORDER BY ASC(?gname)<copy>
        
    
    Wenn die Abfrage erfolgreich ausgeführt wird, wird die Abfrageausgabe wie folgt angezeigt:
    

![Abfragespielplatz zeigt die erfolgreiche Ausführung einer Abfrage im Diagramm MOVIESTREAM RDF an und zeigt Abfrageergebnisse an](./images/query-playground-script.png)

Damit endet diese Übung. **Jetzt können Sie mit der nächsten Übung fortfahren.**

## Danksagungen

*   **Autor** - Malia German, Ethan Shmargad, Matthew McDaniel Solution Engineers, Ramu Murakami Gutierrez Produktmanager
*   **Technischer Mitarbeiter** - Melliyal Annamalai Distinguished Product Manager, Joao Paiva Consulting Mitglied des technischen Personals, Lavanya Jayapalan Principal User Assistance Developer
*   **Zuletzt aktualisiert am/um** - Ramu Murakami Gutierrez, Produktmanager, August 2023