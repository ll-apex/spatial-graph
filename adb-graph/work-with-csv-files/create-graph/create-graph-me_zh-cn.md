# 创建图形

## 简介

在本练习中，您将使用 Graph Studio 和 CREATE PROPERTY GRAPH 语句从 `bank_accounts` 和 `bank_txns` 表创建图形。

预计时间：15 分钟。

观看下面的视频，快速浏览实验室。[演练](videohub:1_j5xjw77c)

### 目标

了解方法

*   使用 Graph Studio 和 PGQL DDL（即 CREATE PROPERTY GRAPH 语句）基于现有表或视图建模和创建图形。

### 先备条件

*   下面的练习需要一个 Autonomous Database - Shared Infrastructure 账户。
*   存在启用图形的用户 (`GRAPHUSER`)。也就是说，存在具有正确角色和权限的数据库用户。

## 任务 1：创建帐户和事务处理的图形

1.  单击**图形**图标以导航以创建图形。  
    然后单击**创建图形**。
    
    ![显示创建按钮建模器的位置](images/graph-create-button.png " ")
    
2.  输入 `bank_graph` 作为图形名称，然后单击**下一步**。说明和标记字段是可选的。  
    该图形名称在下一个练习中使用。  
    请勿输入其他名称，因为下一个练习中的查询和代码片段将失败。
    
    ![显示在其中为图形分配名称的“创建图形”窗口](./images/create-graph-dialog.png " ")
    
3.  展开 **GRAPHUSER** ，然后选择 `BANK_ACCOUNTS` 和 `BANK_TXNS` 表。
    
    ![显示如何选择 BANK_ACCOUNTS 和 BANK_TXNS](./images/select-tables.png " ")
    
4.  将它们移到右侧，即单击往返控件上的第一个图标。
    
    ![显示所选表](./images/selected-tables.png " ")
    
5.  单击**下一步**。我们将编辑和更新此图形以添加边缘和顶点标签。
    
    建议的图形将 `BANK_ACCOUNTS` 作为顶点表，因为在 `BANK_TXNS` 上指定了引用它的外键约束条件。
    
    `BANK_TXNS` 是建议的边缘表。
    
    ![显示顶点和边缘表](./images/create-graph-suggested-model.png " ")
    
6.  现在，让我们更改默认的 Vertex 和 Edge 标签。
    
    单击 `BANK_ACCOUNTS` 顶点表。将 Vertex 标签更改为 **ACCOUNTS** 。然后单击复选标记以确认标签并保存更新。
    
    ![将顶点的标签名称更改为帐户](images/edit-accounts-vertex-label.png " ")
    
    单击 `BANK_TXNS` 边缘表，并将边缘标签从 `BANK_TXNS` 重命名为 **TRANSFERS** 。然后单击复选标记以确认标签并保存更新。
    
    ![已将边缘的标签名称更改为“转移”](images/edit-edge-label.png " ")
    
    这**非常重要**，因为在查询图形时，我们将在本研讨会的下一个练习中使用这些边缘标签。单击**下一步**。
    

7.  在“汇总”步骤中，单击**创建图形**。这将打开“创建图形”选项卡，单击 \*\* 创建图形。
    
    ![显示作业状态为成功的作业选项卡](./images/jobs-create-graph.png " ")
    
    这将打开“创建图形”选项卡，单击**创建图形**。
    
    ![显示已启用内存中和创建图形按钮](./images/create-graph-in-memory.png " ")
    
    在此之后，您将转到“Jobs（作业）”页，在该页中将创建图形。
    
    这个实验室结束了。**现在，您可以继续下一个练习。**
    

## 确认

*   **作者** - 产品管理 Jayant Sharma
*   **贡献者** - 产品管理 Jayant Sharma
*   **上次更新者/日期** - Ramu Murakami Gutierrez，产品经理，2023 年 6 月