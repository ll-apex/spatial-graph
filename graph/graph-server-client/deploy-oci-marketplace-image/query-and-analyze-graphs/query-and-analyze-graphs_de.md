# Diagramm abfragen und analysieren

## Einführung

Dieses Beispiel zeigt, wie die Integration mehrerer Datensets und die Verwendung eines Diagramms zusätzliche Analysen ermöglichen und zu neuen Erkenntnissen führen kann. Wir werden drei kleine Datensätze für illustrative Zwecke verwenden. Die erste enthält Accounts und Accounteigentümer. Der zweite ist der Kauf durch die Leute, die diese Konten besitzen. Das dritte sind Transaktionen zwischen diesen Konten.

Das kombinierte Dataset wird dann verwendet, um die folgenden allgemeinen Diagrammabfragen und -analysen durchzuführen: Musterabgleich, Erkennung von Zyklen, Suchen wichtiger Knoten, Community-Erkennung.

Das folgende ER-Diagramm zeigt die Beziehungen zwischen den Datensätzen.

![er-Diagramm](images/er-diagram.jpg)

Geschätzte Laborzeit: 10 Minuten

### Ziele

*   Erfahren Sie, wie Sie das Diagramm abfragen und analysieren

### Voraussetzungen

*   Der Python-Client wird ausgeführt

## Aufgabe 1: Diagramm auf Speicher abrufen

Wenn das Diagramm **customer\_360** in der vorherigen Übung bereits in den Speicher geladen wurde, kann es mit diesem Befehl angehängt werden. Wenn das Diagramm veröffentlicht ist, können Sie auch von den neuen Sessions aus auf das Diagramm zugreifen.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Jetzt können wir dieses Diagramm abfragen und einige Analysen darauf ausführen.

## Aufgabe 2: Musterabgleich

PGQL Query ist praktisch, um bestimmte Muster zu erkennen.

Suchen Sie Konten mit einem eingehenden und einem ausgehenden Transfer von über 500 am selben Tag. Die PGQL-Abfrage hierfür lautet:

    <copy>
    graph.query_pgql("""
        SELECT a.account_no
             , a.balance
             , t1.amount AS t1_amount
             , t2.amount AS t2_amount
             , t1.transfer_date
        FROM MATCH (a)<-[t1:transfer]-(a1)
           , MATCH (a)-[t2:transfer]->(a2)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
    """).print()
    </copy>
    
    +---------------------------------------------------------------+
    | account_no  | balance | t1_amount | t2_amount | transfer_date |
    +---------------------------------------------------------------+
    | xxx-yyy-202 | 200.0   | 900.0     | 850.0     | 2018-10-06    |
    +---------------------------------------------------------------+
    

## Aufgabe 3: Erkennen von Zyklen

Als Nächstes verwenden wir PGQL, um eine Reihe von Überweisungen zu finden, die auf demselben Konto beginnen und enden, wie A bis B bis A oder A bis B bis C bis A.

Die erste Abfrage könnte folgendermaßen ausgedrückt werden:

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no    AS a1_account
             , t1.transfer_date AS t1_date
             , t1.amount        AS t1_amount
             , a2.account_no    AS a2_account
             , t2.transfer_date AS t2_date
             , t2.amount        AS t2_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_date    | t1_amount | a2_account  | t2_date    | t2_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 2018-10-05 | 200.0     | xxx-yyy-202 | 2018-10-10 | 300.0     |
    +-----------------------------------------------------------------------------+
    

Dieses Ergebnis wird im nächsten Abschnitt visualisiert:

![Erkennung](images/detection.jpg)

Die zweite Abfrage fügt dem Muster (Liste) nur eine weitere Übertragung hinzu und könnte folgendermaßen ausgedrückt werden:

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no AS a1_account
             , t1.amount     AS t1_amount
             , a2.account_no AS a2_account
             , t2.amount     AS t2_amount
             , a3.account_no AS a3_account
             , t3.amount     AS t3_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_amount | a2_account  | t2_amount | a3_account  | t3_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 500.0     | xxx-yyy-203 | 450.0     | xxx-yyy-204 | 400.0     |
    +-----------------------------------------------------------------------------+
    

Dieses Ergebnis wird im nächsten Abschnitt visualisiert:

![detection2](images/detection2.jpg)

## Aufgabe 4: Einflussreiche Konten

Finden wir heraus, welche Konten im Netzwerk einflussreich sind. Es gibt verschiedene Algorithmen, um die Wichtigkeit und Zentralität der Scheitelpunkte zu bewerten. Wir verwenden den integrierten PageRank-Algorithmus als Beispiel.

1.  Filtern Sie Kunden aus dem Diagramm. (vgl. [Filterausdrücke](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  Führen Sie den [PageRank-Algorithmus](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html) aus. PageRank Der Algorithmus weist jedem Scheitel eine numerische Gewichtung zu und misst die relative Wichtigkeit im Diagramm.
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  Zeigen Sie das Ergebnis an.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no, a.pagerank
            FROM MATCH (a)
            ORDER BY a.pagerank DESC
        """).print()
        </copy>
        
        +-------------------------------------+
        | a.account_no | a.pagerank           |
        +-------------------------------------+
        | xxx-yyy-201  | 0.18012007557258927  |
        | xxx-yyy-204  | 0.1412461615467829   |
        | xxx-yyy-203  | 0.1365633635065475   |
        | xxx-yyy-202  | 0.12293884324085073  |
        | xxx-zzz-212  | 0.05987452026569676  |
        | xxx-zzz-211  | 0.025000000000000005 |
        +-------------------------------------+
        

## Aufgabe 5: Community-Erkennung

Lassen Sie uns herausfinden, welche Untergruppen von Konten Communitys bilden. Das heißt, es gibt mehr Transfers zwischen Konten in derselben Untergruppe als zwischen diesen und Konten in einer anderen Untergruppe. Wir verwenden den integrierten Algorithmus für schwach/stark verbundene Komponenten.

1.  Der erste Schritt besteht darin, ein Unterdiagramm zu erstellen, das nur die Konten und die Transfers enthält. Dies geschieht durch Erstellen und Anwenden eines Kantenfilters (für Kanten mit dem Lable "Transfer") auf das Diagramm.
    
    Filtern Sie Kunden aus dem Diagramm.
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  Der Algorithmus [Weakly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) erkennt nur eine Partition.
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    Der Komponentenwert wird in einer Eigenschaft mit dem Namen **wcc** gespeichert.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.wcc AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.wcc
            ORDER BY a.wcc
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 6     |
        +----------------------+
        
    
    In diesem Fall bilden alle sechs Konten eine Komponente des ÖRK-Algorithmus.
    
3.  Führen Sie stattdessen den [Strongly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html)\-Algorithmus SCC Kosaraju aus. Er erkennt drei Komponenten.
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  Listen Sie Komponenten und die Anzahl der Scheitel jeweils auf.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.scc_kosaraju AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.scc_kosaraju
            ORDER BY a.scc_kosaraju
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 1     |
        | 1            | 4     |
        | 2            | 1     |
        +----------------------+
        
5.  Listen Sie die anderen Konten in derselben verbundenen Komponente auf wie Johns Konto (= **xxx-yyy-201**). Die Komponenten-ID wird als Eigenschaft mit dem Namen **SCC\_KOSARAJ** zur Verwendung in PGQL-Abfragen hinzugefügt.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no
            FROM MATCH (a)
               , MATCH (a1)
            WHERE a1.account_no = 'xxx-yyy-201'
            AND a.scc_kosaraju = a1.scc_kosaraju
            ORDER BY a.account_no
        """).print()
        </copy>
        
        +-------------+
        | account_no  |
        +-------------+
        | xxx-yyy-201 |
        | xxx-yyy-202 |
        | xxx-yyy-203 |
        | xxx-yyy-204 |
        +-------------+
        
    
    ![Community](images/community.jpg)
    
    In diesem Fall ist das Konto **xxx-yyy-201** (Konto von John), **xxx-yyy-202**, **xxx-yyy-203** und **xxx-yyy-204** eine Partition, das Konto **xxx-zzz-211** eine Parition und das Konto **xxx-zzz-212** eine Partition des SCC-Kosaraju-Algorithmus.
    

Sie können jetzt mit der nächsten Übung fortfahren.

## Danksagungen

*   **Autor** - Jayant Sharma
*   **Mitwirkende** - Arabella Yao, Jenny Tsai
*   **Zuletzt aktualisiert am/um** - Ryota Yamanaka, März 2023