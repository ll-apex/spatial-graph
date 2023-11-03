# Graph Studio：将数据从 CSV 文件加载到表中

## 简介

在此实验室中，您将使用 Oracle Autonomous Data Warehouse 或 Oracle Autonomous Transaction Processing 实例的 Database Actions 接口将两个 CSV 文件加载到相应的表中。

预计时间：10 分钟。

观看下面的视频，快速浏览实验室。

[](youtube:wkKKO-RO0lA)

### 目标

了解方法

*   使用 Database Actions 将 CSV 文件加载到 Autonomous Database

### 先备条件

*   下面的练习需要一个 Oracle Autonomous Database 账户。
*   它假定存在启用图形和 Web 访问的用户。也就是说，存在具有正确角色和权限的数据库用户，该用户可以登录到 Database Actions。

## 任务 1：连接到 Autonomous Database 实例的 Database Actions

1.  在 Oracle Cloud 控制台中打开 Autonomous Database 实例的服务详细信息页面。
    
    ![ALT 文本不可用于此图像](images/open-database-actions.png " ")
    
2.  单击 **Database Actions** 以将其打开。
    

## 任务 2：以启用图形的用户身份登录

1.  以图形用户身份登录 Autonomous Database 实例（例如 `GRAPHUSER`）。
    
    ![ALT 文本不可用于此图像](./images/db-actions-graphuser-login.png " ")
    
    > **注：**_如有必要，请执行以下操作以创建具有正确角色和权限的用户_：
    
    *   以 Autonomous Database 的 **ADMIN** 用户身份登录 Database Actions
    *   从导航菜单中选择**管理**，然后选择**数据库用户**
    *   单击**创建用户**
    *   打开 **Web 访问**和**图形**按钮

## 任务 3：从 ObjectStore 下载示例数据集

1.  在浏览器中复制并粘贴 zip 档案的 URL，即
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    或者使用 `wget` 或 `curl` 将示例数据下载到计算机。  
    可以复制和粘贴的 `curl` 请求示例为：
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  将归档文件**解压缩**到本地目录中，例如 ~/downloads。
    

## 任务 4：使用 Database Actions 数据加载上载

1.  单击 **DATA LOAD** 卡。
    
    ![ALT 文本不可用于此图像](images/db-actions-dataload-card.png " ")
    
    然后指定数据的位置。也就是说，确保 **LOAD DATA** 和 **LOCAL FILE** 卡具有复选标记。单击**下一步**。
    
    ![ALT 文本不可用于此图像](./images/db-actions-dataload-location.png)
    
2.  单击**选择文件**。
    
    ![ALT 文本不可用于此图像](images/db-action-dataload-file-browser.png " ")
    
    导航到正确的文件夹（例如 ~/downloads/random-acct-data），然后选择 `bank_accounts.csv` 和 `bank_txns.csv` 文件。
    
    ![ALT 文本不可用于此图像](./images/db-actions-dataload-choose-files.png " ")
    
3.  验证是否选择了正确的文件，然后单击**运行**图标。 ![ALT 文本不可用于此图像](./images/db-actions-dataload-click-run.png " ")
    
4.  确认您希望执行数据加载作业。
    
    ![ALT 文本不可用于此图像](./images/db-actions-dataload-confirm-run.png " ")
    
5.  加载文件后
    
    ![ALT 文本不可用于此图像](./images/dbactions-dataload-files-loaded.png " ")
    
    单击**完成**以退出。
    
    ![ALT 文本不可用于此图像](images/dbactions-click-done.png " ")
    
6.  现在打开 **SQL** 工作表。 ![ALT 文本不可用于此图像](./images/db-actions-choose-sql-card.png " ")
    
7.  导航到正确的文件夹（例如 ~/downloads），然后选择 `fixup.sql` 文件并将其拖到 SQL 工作表中。
    
    ![ALT 文本不可用于此图像](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    但是，如果希望复制粘贴，则 `fixup.sql` 的内容为：
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    本文档的作用包括：
    
    *   向 `bank_accounts` 表添加主键约束条件
    *   将列 (`txn_id`) 添加到 `bank_txns` 表
    *   设置 `txn_id` 的值并提交事务处理
    *   向 `bank_txns` 表添加主键约束条件
    *   向 `bank_txns` 表添加外键约束条件，指定 `from_acct_id` 引用 `bank_accounts.acct_id`
    *   向 `bank_txns` 表添加另一个外键约束条件，指定 `to_acct_id` 引用 `bank_accounts.acct_id`
    *   帮助您验证是否已添加了 `txn_id` 列和约束条件
8.  在 SQL 工作表中执行 `fixup.sql` 脚本。  
    ![ALT 文本不可用于此图像](./images/db-actions-sql-execute-fixup.png " ")
    
9.  脚本输出应如下所示：
    
    ![ALT 文本不可用于此图像](./images/db-actions-sql-script-output.png " ")
    
    请**转到下一个练习**以从这些表创建图形。
    

## 确认

*   **作者** - 产品管理 Jayant Sharma
*   **贡献者** - 产品管理 Jayant Sharma
*   **上次更新者/日期** - Jayant Sharma，产品管理，2022 年 2 月