# 准备环境

## 简介

Oracle Autonomous Transaction Processing (ATP) 是完全托管的 Oracle 数据库服务，在 Oracle Cloud Infrastructure (OCI) 上提供“自治驱动”功能。最佳做法是创建具有使用 Graph Studio 权限的用户。

以下实验室指南介绍了如何预配 ATP 以及如何为 Graph Studio 创建具有权限的用户。

估计时间：15 分钟

### 目标

*   在 Oracle Cloud 上创建 Autonomous Database。

### 先备条件

*   Web 浏览器
*   始终确保您位于正确的区域和区间中

## **任务 1：**登录 Oracle Cloud

1.  通过浏览器登录 Oracle Cloud。

## **任务 2：**预配 ATP

使用以下步骤预配自治事务处理数据库 (Autonomous Transaction Processing Database，ATP)。此外，自治数据仓库 (Autonomous Data Warehouse，ADW) 也可以采用类似的方式。

1.  从 OCI 控制台的右上角选择分配的区域。
    
2.  从汉堡菜单（左上角）中，选择“Oracle Database”，然后选择“Autonomous Transaction Processing（自治事务处理）”。
    

![图中显示了在菜单中选择访问自治事务处理的位置](./images/atp.png)

3.  单击“Create Autonomous Database。

![图中显示了创建自治数据库的按钮](./images/create-adb.png)

4.  选择区间。
    
5.  输入显示和数据库名称的任何唯一名称（可能是您的姓名）。控制台 UI 中使用显示名称来标识数据库。
    

![图中显示了为数据库输入唯一名称的位置](./images/unique-name.png)

6.  确保选择了“事务处理”工作量类型。
    
7.  输入密码。用户名始终为 ADMIN。（注：请记住您的密码）
    

![图中显示了密码的声明位置](./images/password.png)

8.  单击底部的“Create Autonomous Database（创建自治数据库）”。
    
    您的控制台将显示 ATP 正在预配。完成此操作大约需要 2 或 3 分钟。
    
    您可以在工作请求中检查预配的状态。
    

![图中显示了检查预配数据库状态的位置](./images/status.png)

这个实验室结束了。_现在，您可以继续下一个练习。_

## 确认

*   **作者** - Nicholas Cusato（圣莫尼卡专家中心）
*   **贡献者** - Nicholas Cusato（圣莫尼卡专家中心）
*   **上次更新者/日期** - Nicholas Cusato，2022 年 2 月