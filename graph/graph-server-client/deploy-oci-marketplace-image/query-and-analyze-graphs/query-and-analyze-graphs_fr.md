# Requête et analyse du graphique

## Présentation

Cet exemple montre comment l'intégration de plusieurs jeux de données et l'utilisation d'un graphique facilitent des analyses supplémentaires et peuvent conduire à de nouvelles informations. Nous utiliserons trois petits ensembles de données à des fins d'illustration. Le premier contient les comptes et les propriétaires de compte. Le deuxième est l'achat par les personnes qui possèdent ces comptes. La troisième concerne les transactions entre ces comptes.

L'ensemble de données combiné est ensuite utilisé pour effectuer les requêtes et analyses graphiques courantes suivantes : correspondance de modèles, détection de cycles, recherche de nœuds importants, détection de communauté.

Le diagramme ER suivant illustre les relations entre les ensembles de données.

![er-diagramme](images/er-diagram.jpg)

Temps de laboratoire estimé : 10 minutes

### Objectifs

*   Apprendre à interroger et analyser le graphique

### Prérequis

*   Le client Python est opérationnel

## Tâche 1 : obtenir le graphique sur la mémoire

En supposant que le graphique **customer\_360** est déjà chargé dans la mémoire de l'exercice précédent, vous pouvez le joindre à l'aide de cette commande. Si le graphique est publié, vous pouvez également y accéder à partir des nouvelles sessions.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Nous pouvons maintenant interroger ce graphique et y exécuter des analyses.

## Tâche 2 : correspondance de modèle

PGQL Query est pratique pour détecter des modèles spécifiques.

Recherchez les comptes ayant un transfert entrant et sortant de plus de 500 le même jour. La requête PGQL est la suivante :

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
    

## Tâche 3 : détection des cycles

Ensuite, nous utilisons PGQL pour trouver une série de transferts qui commencent et se terminent sur le même compte, tels que A à B à A, ou A à B à C à A.

La première requête peut être exprimée comme suit :

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
    

Ce résultat sera affiché dans la section suivante :

![détection](images/detection.jpg)

La deuxième requête ajoute simplement un transfert supplémentaire au modèle (liste) et peut être exprimée comme suit :

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
    

Ce résultat sera affiché dans la section suivante :

![detection2](images/detection2.jpg)

## Tâche 4 : Comptes influents

Voyons quels comptes ont une influence sur le réseau. Il existe différents algorithmes pour évaluer l'importance et la centralité des sommets. Nous utiliserons l'algorithme PageRank intégré comme exemple.

1.  Filtrez les clients à partir du graphique (cf. [Expressions de filtre](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  Exécutez l'[algorithme PageRank](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html). L'algorithme PageRank affecte une pondération numérique à chaque sommet, en mesurant son importance relative dans le graphique.
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  Affichez les résultats.
    
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
        

## Tâche 5 : détection de la communauté

Voyons quels sous-ensembles de comptes forment des communautés. Autrement dit, il y a plus de transferts entre les comptes d'un même sous-ensemble qu'entre ceux-ci et les comptes d'un autre sous-ensemble. Nous utiliserons l'algorithme de composants faiblement / fortement connectés intégré.

1.  La première étape consiste à créer un sous-graphique qui ne comporte que les comptes et les transferts entre eux. Pour ce faire, créez et appliquez un filtre d'arêtes (pour les arêtes avec l'étiquette "transfert") sur le graphique.
    
    Filtrer les clients à partir du graphique.
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  L'algorithme de [composant faiblement connecté](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) détecte une seule partition.
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    La valeur du composant est stockée dans une propriété nommée **wcc**.
    
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
        
    
    Dans ce cas, les six comptes forment un seul composant par l'algorithme du COE.
    
3.  Exécutez plutôt un algorithme [Composant fortement connecté](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html), SCC Kosaraju. Il détecte trois composants.
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  Répertoriez les composants et le nombre de sommets de chacun.
    
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
        
5.  Répertoriez les autres comptes dans le même composant connecté que le compte John (= **xxx-yyy-201**). L'ID de composant est ajouté en tant que propriété nommée **SCC\_KOSARAJ** à utiliser dans les requêtes PGQL.
    
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
        
    
    ![communauté](images/community.jpg)
    
    Dans ce cas, les comptes **xxx-yyy-201** (compte de John), **xxx-yyy-202**, **xxx-yyy-203** et **xxx-yyy-204** forment une partition, le compte **xxx-zzz-211** est une parition et le compte **xxx-zzz-212** est une partition, par l'algorithme SCC Kosaraju.
    

Vous pouvez maintenant passer au laboratoire suivant.

## Accusés de réception

*   **Auteur** - Jayant Sharma
*   **Contributeurs** - Arabella Yao, Jenny Tsai
*   **Dernière mise à jour par/date** - Ryota Yamanaka, mars 2023