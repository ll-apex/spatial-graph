# 查詢和分析圖表

## 簡介

此範例顯示整合多個資料集與使用圖表的方式，有助於額外的分析，並可能導致新的洞察分析。我們將使用三個小型資料集作為說明用途。第一個項目包含帳戶和帳戶擁有者。其次是由擁有這些帳戶的人購買。第三個是這些帳戶之間的交易。

接著，合併的資料集會用來執行下列通用圖表查詢與分析：模式比對、偵測週期、尋找重要節點、社群偵測。

下列 ER 圖說明資料集之間的關係。

![er-diagram - 企業資源規劃](images/er-diagram.jpg)

預估實驗室時間：10 分鐘

### 目標

*   瞭解如何查詢及分析圖表

### 先決條件

*   Python 用戶端已啟動並在執行中

## 作業 1：取得記憶體圖表

假設 **customer\_360** 圖表已經載入前一個實驗室的記憶體中，您可以使用這個指令來連接圖形。如果圖表已發布，您也可以從新階段作業存取圖表。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

現在我們可以查詢此圖表，並對其執行一些分析。

## 作業 2：模式比對

PGQL 查詢適用於偵測特定模式。

在同一天尋找內送和外送傳輸量超過 500 的帳戶。此項目的 PGQL 查詢為：

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
    

## 任務 3：偵測週期

接下來，我們使用 PGQL 來尋找從同一帳戶開始和結束的一系列轉移，例如 A 到 B 到 A，或 A 到 B 到 C 到 A。

第一個查詢可以用下列方式表示：

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
    

此結果將會在下一個區段中視覺化：

![偵測](images/detection.jpg)

第二個查詢只會將一個傳輸新增至樣式 (清單)，而且可以用下列方式表示：

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
    

此結果將會在下一個區段中視覺化：

![detection2](images/detection2.jpg)

## 作業 4：影響客戶

讓我們找出哪個帳戶在網路中受到影響。有多種演算法可對頂點的重要性和中心性進行評分。我們將使用內建的 PageRank 演算法作為範例。

1.  從圖形中篩選客戶 (cf)。[篩選表示式](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html) )
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  執行 [PageRank 演算法](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html)。PageRank 演算法會指派數值權重給每個頂點，評量其在圖形中的相對重要性。
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  顯示結果。
    
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
        

## 工作 5：社群偵測

讓我們找出哪些帳戶子集形成社群。也就是說，相同子集中的帳戶間的轉移比其他子集中的帳戶之間的轉移多。我們將使用內建的弱連接 / 強式連接元件演算法。

1.  第一步是建立只有帳戶和它們之間轉移的子圖表。這是透過建立邊緣篩選 (適用於帶有線 "transfer" 的邊緣) 並套用至圖表來完成。
    
    從圖表篩選客戶。
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  [弱連線元件](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) 演算法只會偵測一個分割區。
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    元件值儲存在名為 **wcc** 的特性中。
    
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
        
    
    在此情況下，這六個帳戶都是由 WCC 演算法組成一個元件。
    
3.  改為執行 [Strongly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html) 演算法 SCC Kosaraju。它會偵測三個元件。
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  列出各元件中的頂點數目。
    
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
        
5.  列出與 John 帳號位於相同連接元件中的其他帳號 (= **xxx-yyy-201**)。元件 ID 會新增為名為 **SCC\_KOSARAJ** 的特性，以用於 PGQL 查詢。
    
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
        
    
    ![社群](images/community.jpg)
    
    在此情況下，帳戶 **xxx-yyy-201** (John 的帳戶)、 **xxx-yyy-202** 、 **xxx-yyy-203** 及 **xxx-yyy-204** 皆為一個分割區、帳戶 **xxx-zzz-211** 為分割區，而帳戶 **xxx-zzz-212** 則為 SCC Kosaraju 演算法的分割區。
    

您現在可以繼續下一個實驗室。

## 確認

*   **作者** - Jayant Sharma
*   **貢獻者** - Arabella Yao、Jenny Tsai
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月