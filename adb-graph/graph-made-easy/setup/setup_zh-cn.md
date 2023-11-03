# 设置：运行堆栈

## 简介

在此实验室中，您将运行一个堆栈，该堆栈将生成 Autonomous Database、创建图形用户并上载将要使用的数据集。

估计时间：5 分钟。

观看下面的视频，快速浏览实验室。[设置](videohub:1_8z5ze0pe)

### 目标

了解方法

*   创建区间 (OPTIONAL)
*   运行堆栈以创建 Autonomous Database、Graph 用户和上载数据集
*   登录到 Graph Studio

## 任务 1：创建 OCI 区间 (OPTIONAL)

> **注：**_如果您已具有区间，则此实验室是可选的。_

[](include:iam-compartment-create-body.md)

## 任务 2：运行堆栈

以下说明将说明如何运行堆栈，该堆栈将自动创建包含图形用户的 Autonomous Database 以及属性图形查询所需的数据集。

1.  登录到 Oracle Cloud。
    
2.  登录后，使用此 [link](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oracle-quickstart/oci-arch-graph/releases/latest/download/orm-graph-stack.zip) 创建并运行堆栈。
    

> 注：链接将在新选项卡或窗口中打开。

3.  您将定向到此页面：

![“创建堆栈”页](./images/create-stack.png)

4.  勾选“我已查看并接受 Oracle 使用条款”框并选择您的区间。将其余部分保留为默认值。单击**下一步**。

![已选定“查看并接受 Oracle 使用条款”的选项](./images/oracle-terms.png)

5.  选择区间以创建 Autonomous Database，其余部分保留为默认值。单击**下一步**。之后，您将转到“复查”页，单击**创建**。

![“创建堆栈”页](./images/configure-variables.png)

6.  您将转到“作业详细信息”页，初始状态以橙色显示。作业成功完成后，该图标将变为绿色。
    
    ![作业已成功](./images/successful-job.png)
    
    要查看有关应用程序的信息，请单击**应用程序信息**。保存 Graph 用户名和密码，因为您将使用它登录到 Graph Studio。
    
    ![如何查看图形用户名和密码](./images/graph-username-password.png)
    

## 任务 3：登录到 Graph 工作室

1.  单击 "Application Information" 下的 **Open Graph Studio** 。这将打开一个新页面。在登录屏幕中输入应用程序信息下提供的图形用户名和密码。

![在应用程序信息下打开图形工作室](./images/login-page.png " ")

2.  然后单击**登录**按钮。您应该看到工作室主页。

![ALT 文本不可用于此图像](./images/gs-graphuser-home-page.png " ")

Graph Studio 包含一组从左侧菜单访问的页面。

“主页”图标 ![主页图标](images/home.svg) 可将您带到主页。  
“模型”图标 ![“模型”图标](images/code-fork.svg) 可转到“模型”页，在此页上可以开始将现有表和视图建模为图形，然后创建或实例化图形。  
“图形”页 !["Graphs" 图标](images/radar-chart.svg) 列出了用于记事本的现有图形。  
“记事本”页面 ![“记事本”图标](images/notebook.svg) 列出了现有记事本，并允许您创建新记事本。  
“作业”页 ![作业图标](images/server.svg) 列出后台作业的状态，并允许您查看关联的日志（如果有）。

这个实验室结束了。**现在，您可以继续下一个练习。**

## 确认

*   **作者** - 产品管理部门 Ramu Murakami Gutierrez 的 Jayant Sharma
*   **贡献者** - Rahul Tasker，Jayant Sharma，Ramu Murakami Gutierrez，产品管理
*   **上次更新者/日期** - Ramu Murakami Gutierrez，产品管理，2022 年 6 月