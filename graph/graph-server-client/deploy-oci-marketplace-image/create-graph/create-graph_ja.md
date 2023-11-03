# グラフの作成

## 概要

これで、表が作成され、データが移入されます。これらのグラフ表現を作成します。

予想時間: 5分

### 目標

次の方法でリレーショナル・データ・ソースからグラフを作成する方法を学習します。

*   グラフ・サーバーに接続するクライアント(Pythonシェル)の起動
*   PGQLデータ定義言語(DDL)(CREATE PROPERTY GRAPHなど)を使用したグラフのインスタンス化

### 前提条件

*   この演習では、演習- 表の作成および移入を正常に完了していることを前提としています。

## タスク1: Pythonクライアントの起動

前に作成した秘密キーを使用して、SSHを介して**opc**ユーザーとしてコンピュート・インスタンスに接続します。

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

例:

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

サーバーに接続するPythonクライアント・シェル・インスタンスを起動します。

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

クライアントシェルが正常に起動した場合は、次が表示されます。

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## タスク2: グラフの作成

既存の表からグラフを作成するプロパティ・グラフ作成文を設定します。

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
    

DDL構文の詳細は、[pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph)を参照してください。_入力表のすべての列は、[デフォルトで](https://pgql-lang.org/spec/1.4/#properties)_頂点/エッジのプロパティにマップされることに注意してください。**owned\_by**エッジの場合、**ID**プロパティのみがエッジID生成の目的で**PROPERTIES**キーワードとともに指定され、他のプロパティは指定されません。これは、アカウント頂点によってすでに保持されているためです。

次に、PGQL DDLを実行してグラフを作成します。

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## タスク3: 新しく作成したグラフの確認

グラフが作成されたことを確認します。Pythonシェルで次の文をコピー、貼付けおよび実行します。

グラフを添付します。

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

グラフが作成されたことを確認します。

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

一部のPGQL問合せを実行します。たとえば、頂点ラベルのリスト:

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
    

各ラベルの頂点の数:

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
    

エッジ・ラベルのリスト:

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
    

各ラベルのエッジの数:

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
    

## タスク4: グラフの公開

新しく作成されたグラフはデフォルトで「プライベート」であり、現在のセッションからのみアクセスできます。今後、新しいセッションからグラフにアクセスするには、グラフを「公開」できます。

次に、前述の手順に従ってグラフを再度作成し、公開します。

    <copy>
    graph.publish()
    </copy>
    

次回接続時に、グラフ・サーバーがログイン間で停止または再起動されていない場合、再ロードせずにメモリーに保持されているグラフにアクセスできます。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

ユーザーの作成時に**`PGX_SESSION_ADD_PUBLISHED_GRAPH`**ロールが付与されているため、グラフの公開が許可されていることに注意してください。それ以外の場合は、**ADMIN**ユーザーによって付与され、Pythonシェルで再接続して、更新された権限を取得する必要があります。

次の演習に進むことができます。

## 謝辞

*   **著者** - Jayant Sharma
*   **貢献者** - Arabella Yao、Jenny Tsai
*   **最終更新者/日付** - 山中亮太、2023年3月