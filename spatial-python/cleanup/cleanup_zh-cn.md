# 清除

## 简介

您可以通过将 Autonomous Database 重置为研讨会前状态来清理研讨会环境。

估计实验室时间：2 分钟

### 目标

*   将 Autonomous Database 重置为研讨会前状态

### 先备条件

*   活动 Autonomous Database 实例

## 任务 1：将 Autonomous Database 重置为研习会前状态

1.  运行以下命令以删除在此研习会中创建的所有数据库 Artifact。
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，2023 年 8 月