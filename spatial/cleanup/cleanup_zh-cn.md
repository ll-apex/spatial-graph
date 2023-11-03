# 将 ADB 重置为研习会前状态

## 简介

此实验室将删除之前实验室中创建的所有内容，以便根据需要重新开始。

估计实验室时间：2 分钟

### 关于我们

在此实验室中，将删除以前创建的所有构件。

### 目标

*   将 ADB 重置为研习会前状态。

### 先备条件

*   完成实验室 3；准备空间数据

## 任务 1：删除此研习会中创建的所有内容

1.  要删除在此研习会中创建的表和索引，请使用“SQL Worksheet（SQL 工作表）”中的“run script（运行脚本）”按钮运行以下命令。
    
    ![图像替代文本](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  要删除在此研讨会中插入的空间元数据，请使用“SQL Worksheet（SQL 工作表）”中的“run script（运行脚本）”按钮运行以下命令。
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  要删除此研习会中创建的函数，请运行以下命令。
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，2022 年 9 月