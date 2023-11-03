# 创建图形

## 简介

现在，将创建表并使用数据进行填充。让我们创建一个图形表示形式。

估计时间：5 分钟

### 目标

了解如何通过以下方式从关系数据源创建图形：

*   启动连接到图形服务器的客户机 (Python shell)
*   使用 PGQL 数据定义语言 (DDL)（例如 CREATE PROPERTY GRAPH）实例化图形

### 先备条件

*   此实验假设您已成功完成实验 - 创建并填充表。

## 任务 1：启动 Python 客户端

使用您之前创建的私有密钥，以 **opc** 用户身份通过 SSH 连接到计算实例。

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

示例：

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

启动连接到服务器的 Python 客户端 shell 实例。

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

如果客户机 shell 已成功启动，则应看到以下内容。

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## 任务 2：创建图形

设置创建属性图形语句，该语句基于现有表创建图形。

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
    

有关 DDL 语法的更多信息，请参见 [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph) 。请注意，_输入表的所有列都[默认情况下](https://pgql-lang.org/spec/1.4/#properties)映射到顶点/边的属性_。对于 **owned\_by** 边缘，仅为边缘 ID 生成目的使用 **PROPERTIES** 关键字提供 **id** 属性，并且不提供其他属性，因为它们已被帐户顶点保留。

现在执行 PGQL DDL 以创建图形。

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## 任务 3：检查新创建的图形

检查是否已创建图形。在 Python shell 中复制、粘贴和运行以下语句。

附加图形。

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

检查是否已创建图形。

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

运行一些 PGQL 查询。例如，顶点标签列表：

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
    

每个标签有多少个顶点：

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
    

边缘标签的列表：

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
    

每个标签的边数：

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
    

## 任务 4：发布图形

默认情况下，新创建的图形为“专用”，只能从当前会话访问。要将来从新会话访问图形，您可以“发布”该图形。

然后按照上述过程再次创建图形，然后发布图形。

    <copy>
    graph.publish()
    </copy>
    

下次连接时，如果图形服务器未在登录之间关闭或重新启动，则可以访问保留在内存上的图形而不重新加载它。

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

请注意，允许您发布图形，因为在创建用户时已授予 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 角色。否则，它必须由 **ADMIN** 用户授予，然后重新连接到 Python shell 以获取更新的权限。

现在，您可以进入下一个实验室。

## 确认

*   **作者** - Jayant Sharma
*   **贡献者** - Arabella Yao、Jenny Tsai
*   **上次更新者/日期** - Ryota Yamanaka，2023 年 3 月