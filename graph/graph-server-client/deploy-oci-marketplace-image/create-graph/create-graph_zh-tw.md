# 建立圖表

## 簡介

現在，系統會建立表格並植入資料。讓我們建立它們的圖形表示法。

估計時間：5 分鐘

### 目標

瞭解如何透過下列方式從關聯式資料來源建立圖表：

*   啟動連線至圖表伺服器的從屬端 (Python shell)
*   使用 PGQL 資料定義語言 (DDL) (例如 CREATE PROPERTY GRAPH) 建立圖表

### 先決條件

*   此實驗室假設您已成功完成實驗室 - 建立並植入表格。

## 工作 1：啟動 Python 用戶端

請使用先前建立的私密金鑰，以 **opc** 使用者身分透過 SSH 連線至運算執行處理。

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

範例：

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

啟動連線至伺服器的 Python 用戶端 Shell 實例。

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

如果用戶端 shell 成功啟動，您應該會看到以下內容。

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## 作業 2：建立圖表

設定 create property graph 敘述句，以從現有表格建立圖表。

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
    

如需 DDL 語法的詳細資訊，請參閱 [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph) 。請注意，_輸入表格的所有資料欄會[依預設對應至頂點 / 邊緣的特性](https://pgql-lang.org/spec/1.4/#properties)_。對於 **owned\_by** 邊緣，系統只會提供 **id** 特性來產生邊緣 ID 的 **PROPERTIES** 關鍵字，而不會提供其他特性，因為帳戶頂點已經保留這些特性。

現在執行 PGQL DDL 以建立圖表。

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## 作業 3：檢查新建立的圖表

檢查圖表是否已建立。在 Python Shell 中複製、貼上及執行下列敘述句。

附加圖形。

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

檢查圖表是否已建立。

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

執行一些 PGQL 查詢。例如，頂點標籤清單：

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
    

每個標籤有多少頂點 ：

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
    

邊緣標籤清單 ：

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
    

每個標籤有多少邊 ：

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
    

## 作業 4：發布圖表

依照預設，新建立的圖表是「私人」，只能從目前的階段作業存取。若要從未來的新階段作業存取圖表，您可以「發布」圖表。

然後依照上述程序再次建立圖表，然後加以發布。

    <copy>
    graph.publish()
    </copy>
    

下次連線時，如果在登入之間尚未關閉或重新啟動圖形伺服器，您可以存取保留在記憶體中的圖表而不重新載入。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

請注意，建立使用者時已授予 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 角色，因此您可以發布圖形。否則，必須由 **ADMIN** 使用者授予 Python Shell，才能提取更新的權限。

您現在可以繼續下一個實驗室。

## 確認

*   **作者** - Jayant Sharma
*   **貢獻者** - Arabella Yao、Jenny Tsai
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月