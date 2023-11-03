# 设置：运行堆栈

## 简介

在此实验室中，您将创建一个堆栈，该堆栈将运行 terraform 脚本来生成 Autonomous Database、创建 Graph 用户以及上载将要使用的数据集。

估计时间：5 分钟。

### 目标

了解方法

*   运行堆栈以创建 Autonomous Database、Graph 用户和上载数据集
*   登录到 Graph Studio

## 任务 1：创建 OCI 区间

[](include:iam-compartment-create-body.md)

## 任务 2：运行堆栈

以下说明将说明如何运行堆栈，该堆栈将自动创建包含图形用户的 Autonomous Database 以及属性图形查询所需的数据集。

1.  登录到 Oracle Cloud。
    
2.  登录后，使用此 [link](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kMdD7Vnv0J1st_2cU-S5PYNWT4SKzOOA04XbhwltUVXnOQ7vec1JJBEGk1eOxPS/n/oradbclouducm/b/moviestream_livelab/o/MovieStream_live_lab_7_AnD.zip) 创建并运行堆栈。
    

> 注：链接将在新选项卡或窗口中打开。

3.  您将定向到此页面：

![“创建堆栈”页](./images/create-stack.png)

4.  勾选“我已查看并接受 Oracle 使用条款”框，然后选择您的**区间**。将其余部分保留为默认值。单击**下一步**。

![已选定“查看并接受 Oracle 使用条款”的选项](./images/oracle-terms.png)

5.  选择**区间**以创建 Autonomous Database，以及创建堆栈时所在的**区域**以创建所有资源。单击**下一步**。之后，您将转到“复查”页，单击**创建**。

![“创建堆栈”页](./images/configure-variables.png)

6.  您将转到“作业详细信息”页，初始状态以橙色显示。作业成功完成后，该图标将变为绿色。
    
    ![作业已成功](./images/successful-job.png)
    

## 确认

*   **作者** - 产品管理部门 Ramu Murakami Gutierrez 的 Jayant Sharma
*   **贡献者** - Rahul Tasker，Jayant Sharma，Ramu Murakami Gutierrez，产品管理
*   **上次更新者/日期** - Ramu Murakami Gutierrez，产品经理，2023 年 2 月