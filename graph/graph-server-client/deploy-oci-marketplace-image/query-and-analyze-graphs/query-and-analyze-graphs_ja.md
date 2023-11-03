# グラフの問合せおよび分析

## 概要

この例は、複数のデータセットを統合し、グラフを使用して追加の分析を促進し、新しいインサイトにつながる方法を示しています。説明のために3つの小さなデータセットを使用します。1つ目は、アカウントおよびアカウント所有者です。二つ目は、その口座を持つ人の買い物です。3つ目は、これらの勘定科目間の取引です。

次に、結合されたデータセットを使用して、パターン一致、サイクルの検出、重要なノードの検索、コミュニティ検出という共通のグラフ問合せおよび分析を実行します。

次のER図は、データセット間の関係を示しています。

![er- 図](images/er-diagram.jpg)

推定ラボ時間: 10分

### 目標

*   グラフを問い合せて分析する方法の学習

### 前提条件

*   Pythonクライアントが稼働中

## タスク1: メモリーに関するグラフの取得

前の演習のメモリーに**customer\_360**グラフがすでにロードされている場合、このコマンドでグラフをアタッチできます。グラフが公開されている場合は、新しいセッションからグラフにアクセスすることもできます。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

これで、このグラフを問い合せて、それに対していくつかの分析を実行できます。

## タスク2: パターン一致

PGQL問合せは、特定のパターンを検出するのに便利です。

同日に500を超えるインバウンドおよびアウトバウンド転送があるアカウントを検索します。このPGQL問合せは次のとおりです。

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
    

## タスク3: サイクルの検出

次に、PGQLを使用して、AからBからA、AからBからCからAなど、同じアカウントで開始および終了する一連の転送を検索します。

最初の問合せは次のように表すことができます。

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
    

この結果は、次のセクションで視覚化されます。

![検出](images/detection.jpg)

2番目の問合せは、パターン(リスト)にさらに1つの転送を追加するだけで、次のように表すことができます。

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
    

この結果は、次のセクションで視覚化されます。

![detection2](images/detection2.jpg)

## タスク4: 影響力のあるアカウント

ネットワークでどのアカウントが影響を受けますか。頂点の重要性と中心性をスコアリングする様々なアルゴリズムがあります。組込みのPageRankアルゴリズムを例として使用します。

1.  グラフから顧客をフィルタします。(cf)[フィルタ式](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  [PageRankアルゴリズム](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html)を実行します。PageRankアルゴリズムは、各頂点に数値の重みを割り当て、グラフ内の相対的な重要度を測定します。
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  結果を表示します。
    
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
        

## タスク5: コミュニティ検出

コミュニティを形成するアカウントのサブセットを見つけましょう。つまり、同じサブセット内の取引先間には、別のサブセット内の取引先間よりも多くの振替があります。組み込みの弱い/強く接続されたコンポーネントアルゴリズムを使用します。

1.  最初のステップは、勘定科目とそれらの間の転送のみを持つサブグラフを作成することです。これを行うには、エッジ・フィルタを作成して適用します(ラベルが「転送」のエッジの場合)。
    
    グラフから顧客をフィルタします。
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  [弱い接続コンポーネント](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html)(WCC)アルゴリズムは、1つのパーティションのみを検出します。
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    コンポーネント値は、**wcc**という名前のプロパティーに格納されます。
    
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
        
    
    この場合、6つの勘定科目すべてがWCCアルゴリズムによって1つのコンポーネントを形成します。
    
3.  かわりに、[厳密に接続されたコンポーネント](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html)・アルゴリズムSCC Kosarajuを実行します。3つのコンポーネントを検出します。
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  コンポーネントおよび各頂点数をリストします。
    
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
        
5.  Johnのアカウントと同じ接続コンポーネント内の他のアカウントをリストします(= **xxx-yyy-201**)。コンポーネントIDは、PGQL問合せで使用するために**SCC\_KOSARAJ**という名前のプロパティとして追加されます。
    
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
        
    
    ![コミュニティ](images/community.jpg)
    
    この場合、アカウント **xxx-yyy-201** (Johnのアカウント)、**xxx-yyy-202**、**xxx-yyy-203**、および **xxx-yyy-204**は1つのパーティション、アカウント **xxx-zzz-211**はパーティション、アカウント **xxx-zzz-212**はSCC Kosarajuアルゴリズムによるパーティションです。
    

次の演習に進むことができます。

## 謝辞

*   **著者** - Jayant Sharma
*   **貢献者** - Arabella Yao、Jenny Tsai
*   **最終更新者/日付** - 山中亮太、2023年3月