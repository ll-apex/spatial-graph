# 可视化图形

## 简介

使用图形可视化功能，可以轻松地对之前实验室中分析的结果进行可视化。

估计时间：5 分钟

以下视频概述了图形可视化组件 (= GraphViz)。

[YouTube](youtube:zfefKdNfAY4)

### 目标

*   了解如何执行 PGQL 图形查询并可视化结果。

### 先备条件

*   创建并发布图形
*   Graph 服务器（带有 GraphViz）已启动且正在运行

## 任务 1：登录 GraphViz

Open the GraphViz at **`https://<public_ip_for_compute>:7007/ui`** using a web browser. Replace **`<public_ip_for_compute>`** with the one for your Graph Server compute instance.

由于市场映像是使用自签名 SSL 证书分发的，因此在生产中使用时应更改自己的证书。与此同时，Web 浏览器应该显示警告，而我们知道它是安全的。

如果使用 **Chrome** ，请在警告窗口中键入 **thisisunsafe** 以移至 GraphViz 屏幕。

![登录信息](images/login-chrome.jpg)

使用 **Firefox** ，依次单击**高级**和**接受风险并继续**。

![登录 firefox](images/login-firefox.jpg)

您应该会看到与下面的屏幕截图类似的屏幕。输入用户名 (**customer\_360** ) 和密码，然后单击 "Submit"（提交）。**图形服务器**是高级选项中的默认设置，因此您无需更改它。

![登录](images/login.jpg)

## 任务 2：修改查询

修改查询以获取前 5 行，即将 **LIMIT 100** 更改为 **LIMIT 5** ，然后单击“运行”。

您应该会看到类似于以下屏幕截图的图形。

![show-5 元素](images/show-5-elements.jpg)

## 任务 3：添加突出显示

现在让我们添加一些标签和其他视觉上下文。这些被称为亮点。单击[此处](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip)下载 zip 文件 highlights.json.zip。解压缩此文件，注意解压缩的位置。

单击**设置**下的“加载”按钮（在屏幕右侧）。浏览到相应的文件夹并选择文件，然后单击“打开”以加载该文件。

![亮点 -1](images/highlights-1.png)

图表现在看起来像

![亮点 -2](images/highlights-2.png)

## 任务 4：与 PGQL 匹配的模式

1.  接下来，让我们运行一些 PGQL 查询。
    
    [pgql-lang.org](http://pgql-lang.org) 站点和[规范](http://pgql-lang.org/spec/1.4)是详细信息和示例的最佳参考。然而，在本实验中，这里是最低限度的基础知识。
    
    PGQL 查询的一般结构为：
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL 提供了一种称为 **MATCH** 子句的特定构造，用于匹配图形模式。图形模式匹配满足给定条件和约束的顶点和边缘。
    
    *   **(v)** 指示顶点变量 **v**
    *   **\-** 指示非定向边缘，如 (source)-(dest) 中
    *   **\->** 从源到目标的传出边缘
    *   **<-** 从目标到源的传入边缘
    *   **\[e\]** 指示边缘变量 **e**
    
    此外，请在此处省略 **graph\_name** ，因为它是从 GraphViz UI 中选择的。
    
2.  让我们查找当天出站和入站转移超过 500 的账户。
    
    对此的 PGQL 查询如下：
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    在上面的第一个 **MATCH** 子句中， **(a)** 指示源顶点， **(a1)** 指示目标，而 **\[t1:transfer\]** 是连接它们的边缘。**：transfer** 指定 **t1** 边缘的标签为 **TRANSFER** 。两个模式之间的逗号 (，) 是一个 AND 条件。
    
3.  将查询复制并粘贴到 GraphViz 应用程序的 PGQL 图形查询文本输入框中。单击“Run（运行）”。
    
    结果应如下所示。在突出显示设置中，以 **xxx-yyy-** 开头的帐户以红色显示（= 银行帐户），而 **xxx-zzz-** 以橙色显示（= 来自其他银行的帐户）。
    
    ![同日转账](images/same-day-transfers.jpg)
    
4.  下一个查询查找进出同一两个帐户的传输模式，即从 a1->a2 和后退 a2->a1。
    
    对此的 PGQL 查询如下：
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  将查询复制并粘贴到 GraphViz 应用程序的 PGQL 图形查询文本输入框中。单击“Run（运行）”。
    
    结果应如下所示。
    
    ![循环 -2 次](images/cycle-2-hops.jpg)
    
6.  让我们再向该查询添加一个帐户，以查找 3 个帐户之间的循环传输模式。
    
    PGQL 查询变为：
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  将查询复制并粘贴到 GraphViz 应用程序的 PGQL 图形查询文本输入框中。单击“Run（运行）”。
    
    结果应如下所示。
    
    ![循环 -3- 跃点](images/cycle-3-hops.jpg)
    

## 确认

*   **作者** - Jayant Sharma
*   **贡献者** - Arabella Yao、Jenny Tsai
*   **上次更新者/日期** - Ryota Yamanaka，2023 年 3 月