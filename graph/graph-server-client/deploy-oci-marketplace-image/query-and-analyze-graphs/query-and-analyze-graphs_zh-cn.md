# 查询和分析图形

## 简介

此示例说明集成多个数据集和使用图形如何促进其他分析，并可获得新的洞察。我们将使用三个小数据集进行说明。第一个包含帐户和帐户所有者。第二个是拥有这些帐户的人的购买。第三是这些账户之间的交易。

然后，组合数据集用于执行以下常见的图形查询和分析：模式匹配、周期检测、查找重要节点、社区检测。

下面的实体关系图描述了数据集之间的关系。

![er 图](images/er-diagram.jpg)

估计的实验室时间：10 分钟

### 目标

*   了解如何查询和分析图形

### 先备条件

*   Python 客户端启动并运行

## 任务 1：获取内存图形

假设 **customer\_360** 图形已装入上一个实验室的内存中，则可以使用此命令附加该图形。如果图形已发布，您还可以从新会话访问该图形。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

现在，我们可以查询此图形并对其运行一些分析。

## 任务 2：模式匹配

PGQL 查询可用于检测特定模式。

查找当天有超过 500 个入站和出站转账的账户。对此的 PGQL 查询如下：

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
    

## 任务 3：检测周期

接下来，我们使用 PGQL 查找在同一帐户开始和结束的一系列传输，例如 A 到 B 到 A，或 A 到 B 到 C 到 A。

第一个查询可以表示为：

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
    

此结果将在下一节中可视化：

![检测](images/detection.jpg)

第二个查询只是向模式（列表）添加了另外一个传输，可以表示为：

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
    

此结果将在下一节中可视化：

![detection2](images/detection2.jpg)

## 任务 4：影响型客户

让我们来看看哪些帐户在网络中具有影响力。有各种算法可以对顶点的重要性和中心性进行评分。我们将使用内置的 PageRank 算法作为示例。

1.  从图形中筛选客户。（参考。）[筛选表达式](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html) )
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  运行 [PageRank 算法](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html)。PageRank 算法为每个顶点分配一个数字权重，测量其在图形中的相对重要性。
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  显示结果。
    
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
        

## 任务 5：社区检测

我们来看看哪些账户子集构成了社区。也就是说，同一子集中的账户之间的转账比其他子集中的账户和账户之间的转账多。我们将使用内置的弱/强连接组件算法。

1.  第一步是创建一个子图，其中仅包含帐户及其之间的转移。这是通过创建和应用边缘筛选器（对于具有可用“转移”的边缘）来完成的。
    
    从图形中筛选客户。
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  [Weakly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html) (WCC) 算法仅检测一个分区。
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    组件值存储在名为 **wcc** 的属性中。
    
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
        
    
    在这种情况下，所有六个帐户都由 WCC 算法组成一个组件。
    
3.  而是运行 [Strongly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html) 算法 SCC Kosaraju。它检测三个组件。
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  列出每个组件和顶点数。
    
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
        
5.  列出与 John 的帐户相同的连接组件中的其他帐户 (= **xxx-yyy-201** )。组件 ID 添加为名为 **SCC\_KOSARAJ** 的属性，以用于 PGQL 查询。
    
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
        
    
    ![社区](images/community.jpg)
    
    在这种情况下，帐户 **xxx-yyy-201** （John 的帐户）、 **xxx-yyy-202** 、 **xxx-yyy-203** 和 **xxx-yyy-204** 构成一个分区，帐户 **xxx-zzz-211** 是解析，帐户 **xxx-zzz-212** 是 SCC Kosaraju 算法的分区。
    

现在，您可以进入下一个实验室。

## 确认

*   **作者** - Jayant Sharma
*   **贡献者** - Arabella Yao、Jenny Tsai
*   **上次更新者/日期** - Ryota Yamanaka，2023 年 3 月