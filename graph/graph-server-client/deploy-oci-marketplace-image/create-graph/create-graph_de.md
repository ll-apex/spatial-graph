# Diagramm erstellen

## Einführung

Jetzt werden die Tabellen erstellt und mit Daten gefüllt. Erstellen wir eine Diagrammdarstellung von ihnen.

Voraussichtliche Zeit: 5 Minuten

### Ziele

Erfahren Sie, wie Sie ein Diagramm aus relationalen Datenquellen erstellen, indem Sie:

*   Starten eines Clients (Python Shell), der eine Verbindung zum Graph Server herstellt
*   Mit PGQL Data Definition Language (DDL) (z.B. CREATE PROPERTY GRAPH) ein Diagramm instanziieren

### Voraussetzungen

*   In dieser Übung wird davon ausgegangen, dass Sie die Übung "Tabellen erstellen und auffüllen" erfolgreich abgeschlossen haben.

## Aufgabe 1: Python-Client starten

Stellen Sie als **opc**\-Benutzer mit dem zuvor erstellten Private Key eine SSH-Verbindung zur Compute-Instanz her.

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

Beispiel:

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

Starten Sie eine Python-Client-Shellinstanz, die eine Verbindung zum Server herstellt.

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

Wenn die Client-Shell erfolgreich gestartet wird, sollte Folgendes angezeigt werden.

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## Aufgabe 2: Diagramm erstellen

Richten Sie die Anweisung zum Erstellen eines Eigenschaftsdiagramms ein, mit der ein Diagramm aus den vorhandenen Tabellen erstellt wird.

    <copy>
    statement = '''
    CREATE PROPERTY GRAPH "customer_360"
      VERTEX TABLES (
        customer
      , account
      , merchant
      )
      EDGE TABLES (
        account
          SOURCE KEY(id) REFERENCES account (id)
          DESTINATION KEY(customer_id) REFERENCES customer (id)
          LABEL owned_by PROPERTIES (id)
      , parent_of
          SOURCE KEY(customer_id_parent) REFERENCES customer (id)
          DESTINATION KEY(customer_id_child) REFERENCES customer (id)
      , purchased
          SOURCE KEY(account_id) REFERENCES account (id)
          DESTINATION KEY(merchant_id) REFERENCES merchant (id)
      , transfer
          SOURCE KEY(account_id_from) REFERENCES account (id)
          DESTINATION KEY(account_id_to) REFERENCES account (id)
      ) 
    '''
    </copy>
    

Weitere Informationen zur DDL-Syntax finden Sie unter [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph). Beachten Sie, dass _alle Spalten der Eingabetabellen [standardmäßig](https://pgql-lang.org/spec/1.4/#properties)_ den Eigenschaften von Scheiteln/Kanten zugeordnet sind. Für die Edge **owned\_by** wird nur die Eigenschaft **id** mit dem Schlüsselwort **PROPERTIES** zum Generieren der Edge-ID angegeben, und die anderen Eigenschaften werden nicht angegeben, da sie bereits von den Kontostandpunkten gehalten werden.

Führen Sie nun die PGQL-DDL aus, um das Diagramm zu erstellen.

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## Aufgabe 3: Neu erstelltes Diagramm prüfen

Prüfen Sie, ob das Diagramm erstellt wurde. Kopieren Sie die folgenden Anweisungen, fügen Sie sie ein, und führen Sie sie in der Python-Shell aus.

Hängen Sie das Diagramm an.

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

Prüfen Sie, ob das Diagramm erstellt wurde.

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

Führen Sie einige PGQL-Abfragen aus. z.B. die Liste der Scheitel-Etiketten:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(v) FROM MATCH (v)
    """).print()
    </copy>
    
    +----------+
    | LABEL(v) |
    +----------+
    | ACCOUNT  |
    | CUSTOMER |
    | MERCHANT |
    +----------+
    

Wie viele Scheitelpunkte mit jedem Label:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(v), LABEL(v) FROM MATCH (v) GROUP BY LABEL(v)
    """).print()
    </copy>
    
    +---------------------+
    | COUNT(v) | LABEL(v) |
    +---------------------+
    | 5        | MERCHANT |
    | 6        | ACCOUNT  |
    | 4        | CUSTOMER |
    +---------------------+
    

Die Liste der Kantenbezeichnungen:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(e) FROM MATCH ()-[e]->()
    """).print()
    </copy>
    
    +-----------+
    | LABEL(e)  |
    +-----------+
    | OWNED_BY  |
    | PARENT_OF |
    | PURCHASED |
    | TRANSFER  |
    +-----------+
    

Wie viele Kanten mit jedem Etikett:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(e), LABEL(e) FROM MATCH ()-[e]->() GROUP BY LABEL(e)
    """).print()
    </copy>
    
    +----------------------+
    | COUNT(e) | LABEL(e)  |
    +----------------------+
    | 4        | OWNED_BY  |
    | 8        | TRANSFER  |
    | 1        | PARENT_OF |
    | 11       | PURCHASED |
    +----------------------+
    

## Aufgabe 4: Diagramm veröffentlichen

Das neu erstellte Diagramm ist standardmäßig "privat" und kann nur von der aktuellen Session aus aufgerufen werden. Um zukünftig von neuen Sessions aus auf das Diagramm zuzugreifen, können Sie das Diagramm "veröffentlichen".

Erstellen Sie das Diagramm dann nach der oben beschriebenen Prozedur erneut, und veröffentlichen Sie es.

    <copy>
    graph.publish()
    </copy>
    

Wenn Sie das nächste Mal eine Verbindung herstellen, können Sie auf das Diagramm zugreifen, das im Speicher aufbewahrt wird, ohne es erneut zu laden, wenn der Graph-Server zwischen den Anmeldungen nicht heruntergefahren oder neu gestartet wurde.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Beachten Sie, dass Sie Diagramme veröffentlichen dürfen, da die Rolle **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** beim Erstellen des Benutzers erteilt wurde. Andernfalls muss er vom **ADMIN**\-Benutzer erteilt und erneut mit der Python-Shell verbunden werden, um die aktualisierten Berechtigungen abzurufen.

Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - Jayant Sharma
*   **Mitwirkende** - Arabella Yao, Jenny Tsai
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023