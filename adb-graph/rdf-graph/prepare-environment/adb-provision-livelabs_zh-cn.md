/\* 删除下一个发行版中的此文件 - 请使用 ADB-PROVISION-CONDITIONAL.MD 文件实例并指定您手动所需的版本：{ "title"："Lab 1: Provision an ADB Instance"，"description"："Provision an Autonomous Database Instance"，"type"："livelabs"，"filename"："https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }，\*/

# 预配 Autonomous Database（ADW 和 ATP）

## 简介

此实验室将指导您逐步开始在 Oracle Cloud 上使用 Oracle Autonomous Database（Autonomous Data Warehouse \[ADW\] 和 Autonomous Transaction Processing \[ATP\]）。在此实验室中，您将预配新的 ADW 实例。

> **注：**本练习使用 ADW 时，创建 ATP 数据库的步骤相同。

估计时间：5 分钟

### 目标

*   了解如何预配新的 Autonomous Database

## 任务 1：从服务菜单中选择 ADW 或 ATP

1.  登录到 Oracle Cloud。
    
2.  登录后，您将转到云服务仪表盘，您可以在其中查看可用的所有服务。单击左上角的导航菜单以显示顶层导航选项。
    
    > **注：**您还可以在仪表盘的**快速操作**部分中直接访问 Autonomous Data Warehouse 或 Autonomous Transaction Processing 服务。
    
    ![Oracle 主页。](./images/Picture100-36.png " ")
    
3.  以下步骤与 Autonomous Data Warehouse 或 Autonomous Transaction Processing 类似。此实验室显示如何预配 Autonomous Data Warehouse 数据库，因此请单击 **Autonomous Data Warehouse** 。
    
    ![单击 Autonomous Data Warehouse。](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  确保工作负载类型为**数据仓库**或**全部**，以查看 Autonomous Data Warehouse 实例。使用**列表范围**下拉菜单选择区间。在“Search Compartments（搜索区间）”字段中输入用户名的第一部分，例如 `LL185`，以快速找到区间。
    
    ![检查左侧的工作量类型。](images/livelabs-compartment.png " ")
    
5.  此控制台显示尚不存在数据库。如果数据库列表较长，您可以按数据库的**状态**（可用、已停止、已终止等）筛选列表。您还可以按**工作量类型**排序。在此处，选择**数据仓库**工作量类型。
    
    ![Autonomous Databases console（自治数据库控制台）。](./images/Compartment.png " ")
    

## 任务 2：创建 ADB 实例

1.  单击**创建 Autonomous Database** 以启动实例创建过程。
    
    ![单击“Create Autonomous Database。](./images/Picture100-23.png " ")
    
2.  此时将显示**创建 Autonomous Database** 屏幕，您可以在其中指定实例的配置。
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  提供自治数据库的基本信息：
    
    *   **选择区间** - 保留默认区间。
    *   **Display Name（显示名称）** \- 为数据库输入可记忆的名称以供显示。对于此实验室，请使用 **ADW Finance Mart（ADW 财务市场）**。
    *   **数据库名称** - 仅使用字母和数字，以字母开头。最大长度为 14 个字符。（最初不支持下划线。）对于此实验室，请使用 **ADWFINANCE** 并**附加您的用户 ID** 。例如，如果用户 ID 为 **LL-185** ，则输入 **ADWFINANCE185**
    
    ![输入必需的详细信息。](./images/Picture100-26-livelabs.png " ")
    
4.  选择工作负载类型。从以下选项中选择数据库的工作量类型：
    
    *   **数据仓库** - 在此实验室中，选择**数据仓库**作为工作量类型。
    *   **事务处理** - 或者，您也可以选择“事务处理”作为工作量类型。
    
    ![选择工作负载类型。](./images/Picture100-26b.png " ")
    
5.  选择部署类型。从以下选项中选择数据库的部署类型：
    
    *   **共享基础结构** - 在此实验室中，选择**共享基础结构**作为部署类型。
    *   **专用基础设施** - 或者，您也可以选择专用基础设施作为部署类型。
    
    ![选择部署类型。](./images/Picture100-26_deployment_type.png " ")
    
6.  配置数据库：
    
    *   **始终免费** - 如果您的 Cloud 账户是“始终免费”账户，您可以选择此选项来创建始终免费的自治数据库。始终免费的数据库提供 1 个 CPU 和 20 GB 存储。对于此实验室，我们建议您取消选中“始终免费”。
    *   **选择数据库版本** - 从可用版本中选择数据库版本。
    *   **OCPU 计数** \- 服务的 CPU 数。对于此练习，请指定 **1 CPU** 。如果您选择“始终免费”数据库，则它具有 1 个 CPU。
    *   **存储 (TB)** - 选择存储容量 (TB)。对于此练习，请指定 **1 TB** 存储。或者，如果您选择“始终免费”数据库，则它具有 20 GB 存储空间。
    *   **自动缩放** - 在此实验室中，请始终启用自动缩放，以允许系统自动使用多达三倍的 CPU 和 IO 资源来满足负载需求。
    *   **新建数据库预览** - 如果有复选框可用于预览新数据库版本，请勿选择它。
    
    > **注：**您无法纵向扩展/收缩 Always Free 自治数据库。
    
    ![选择剩余的参数。](./images/Picture100-26c.png " ")
    
7.  创建管理员身份证明：
    
    *   **密码和确认密码** - 指定服务实例的 ADMIN 用户的密码。密码必须符合以下要求：
    *   密码的长度必须介于 12 到 30 个字符之间，并且必须至少包含一个大写字母，一个小写字母和一个数字字符。
    *   密码不能包含用户名。
    *   密码不能包含双引号 (") 字符。
    *   密码必须不同于使用的最后 4 个密码。
    *   密码不得为 24 小时内设置的同一密码。
    *   重新输入口令进行确认。记下此密码。
    
    ![输入口令并确认口令。](./images/Picture100-26d.png " ")
    
8.  选择网络访问：
    
    *   对于此实验室，接受默认值“Secure access from everywhere”。
    *   如果要仅允许来自您指定的 IP 地址和 VCN 的流量 - 所有公共 IP 或 VCN 对数据库的访问被阻止，请在“选择网络访问”区域中选择“仅允许 IP 和 VCN 的安全访问”。
    *   如果要限制对 OCI VCN 中专用端点的访问，请在“选择网络访问”区域中选择“仅限专用端点访问”。
    *   如果选择了“需要相互 TLS (mTLS) 验证”选项，则需要使用 mTLS 来验证与 Autonomous Database 的连接。如果您在 JDK8 或更高版本中使用 JDBC 瘦驱动程序，则可以通过 TLS 连接连接到 Autonomous Database，而无需 wallet。有关允许 TLS 或仅要求相互 TLS (mTLS) 验证的选项，请参见 [documentation for network options](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5) 。
    
    ![选择网络访问。](./images/Picture100-26e.png " ")
    
9.  选择许可证类型。对于此实验室，请选择**自带许可证 (BYOL)** 。两种许可证类型是：
    
    *   **自带许可证 (Bring Your Own License，BYOL)** - 当您的组织具有现有数据库许可证时，选择此类型。
    *   **包括的许可证** - 如果要订阅新的数据库软件许可证和数据库云服务，请选择此类型。
    
    ![单击“Create Autonomous Database。](./images/Picture100-27-byol.png " ")
    
10.  对于此实验室，请勿提供联系人电子邮件地址。“联系人电子邮件”字段允许您列出联系人以接收运营通知和通告以及计划外维护通知。
    
    ![请勿提供联系人电子邮件地址。](images/contact-email-field.png)
    
11.  Click **Create Autonomous Database**.
    
12.  您的实例将开始预配。几分钟后，该状态将从“预配”变为“可用”。此时，您的 Autonomous Data Warehouse 数据库已准备就绪！在此处查看实例的详细信息，包括名称、数据库版本、OCPU 计数和存储大小。
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

请_转到下一个练习_。

## 是否想要了解更多信息？

单击[此处](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)获取有关使用 Autonomous Data Warehouse 的典型工作流的文档。

## 确认

*   **作者** - ADB 产品管理平台 Nilay Panchal
*   **针对云进行了调整** - 数据库用户帮助首席开发人员 Richard Green
*   **贡献者** - Oracle LiveLabs QA 团队（Jeffrey Malcolm Jr，实习生 | Arabella Yao，产品经理实习生）
*   **上次更新者/日期** - Richard Green，2022 年 2 月