# 从 Python 连接到 Autonomous Database

## 简介

为了准备数据加载和分析，首先建立从 Python 到 Autonomous Database 的连接。python-oracledb 驱动程序支持此连接和所有后续数据库交互。您将使用直接连接到 Oracle Database 且不需要 Oracle Client 库的 python-oracledb 驱动程序的“瘦”模式。

估计的实验室时间：5 分钟

### 目标

*   从 Python 连接到 Autonomous Database

### 先备条件

*   完成实验室 3：启动 JupyterLab

## 任务 1：创建连接参数文件

1.  为了避免将数据库连接信息直接包含在记事本中，您需要使用记事本可以参考的信息创建文件。在 JupyterLab 中，单击“文本文件”磁贴创建新的文本文件。 ![连接到 ADB](images/connect-to-adb-01.png)
    
2.  输入 ADB ADMIN 用户密码。然后，从“文件”菜单中选择**保存文本**。 ![连接到 ADB](images/connect-to-adb-02.png)
    
3.  出现提示时，输入 **my-pwd.txt** 作为文件名，然后单击**重命名**。 ![连接到 ADB](images/connect-to-adb-03.png)
    
4.  关闭文本文件选项卡以返回到“启动器”页。 ![连接到 ADB](images/connect-to-adb-04.png)
    
5.  返回到 Oracle Cloud 浏览器选项卡并最小化 Cloud Shell。 ![连接到 ADB](images/connect-to-adb-05.png)
    
6.  单击**数据库连接**。 ![连接到 ADB](images/connect-to-adb-06.png)
    
7.  向下滚动到“Connection Strings（连接字符串）”部分。对于 TLS 验证，选择 **TLS** 。这是允许瘦模式连接所必需的。然后，在“连接字符串”下，单击**复制**以 \_low 结尾的 TNS 名称。 ![连接到 ADB](images/connect-to-adb-07.png)
    
8.  返回到 JupyterLab 浏览器选项卡。如前所述，单击“文本文件”磁贴可创建新的文本文件。粘贴刚从 Autonomous Database 复制的连接字符串。然后保存文件并重命名为 **my-dsn.txt** 。 ![连接到 ADB](images/connect-to-adb-08.png)
    

如前所述，关闭文本文件选项卡以返回到“启动器”页。

## 任务 2：创建记事本并连接到 Autonomous Database

1.  在启动器中，单击 **Python 3** 磁贴以创建新记事本。 ![连接到 ADB](images/connect-to-adb-09.png)
    
2.  在第一个单元格中，粘贴以下语句，然后单击**运行**按钮。这将加载处理与 Oracle Database 交互的 python-oracedb 模块。
    
        <copy>
        import oracledb
        </copy>
        
    
    ![连接到 ADB](images/connect-to-adb-10.png)
    
3.  在下一个单元格中，粘贴以下语句，然后单击**运行**按钮。这会将 ADB 密码和 DSN 加载到变量中
    
        <copy>
        # Get ADB password and DSN from file
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        </copy>
        
    
    ![连接到 ADB](images/connect-to-adb-11.png)
    
4.  在下一个单元格中，粘贴以下语句，然后单击**运行**按钮。这将创建与 ADB 的连接。
    
        <copy>
        # Create database connection and cursor
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        </copy>
        
    
    ![连接到 ADB](images/connect-to-adb-12.png)
    
5.  在下一个单元格中，粘贴以下语句，然后单击**运行**按钮。这将运行测试查询来验证与 ADB 的连接是否成功。
    
        <copy>
        # Run a test query
        cursor.execute("select object_type, count(*) from all_objects group by object_type")
        for row in cursor.fetchmany(size=10):
          print(row)
        </copy>
        
    
    ![连接到 ADB](images/connect-to-adb-13.png)
    
6.  在左侧面板中右键单击记事本文件 Untitled.ipynb，然后选择**重命名**。
    
    ![连接到 ADB](images/connect-to-adb-14.png)
    
7.  输入 **my-notebook** （或您选择的名称）。请注意，笔记本名称已更改。
    
    ![连接到 ADB](images/connect-to-adb-15.png)
    

现在，您可以**进入下一个练习**。

## 了解详细信息

*   有关到 Autonomous Database 的 python-oracledb 连接的详细信息，请参阅[文档](https://python-oracledb.readthedocs.io/en/latest/user_guide/connection_handling.html#connecting-to-oracle-cloud-autonomous-databases)。

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **贡献者** - Rahul Tasker、Denise Myrick、Ramu Gutierrez
*   **上次更新者/日期** - David Lapp，2023 年 8 月