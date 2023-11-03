# 安装 Spatial Studio

## 简介

此实验室介绍使用 Oracle Cloud Marketplace 预配 Oracle Spatial Studio (Spatial Studio) 的过程。Oracle Cloud Marketplace 提供由 Oracle 和第三方提供的应用和服务。详细信息可在[此处](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html)找到。

估计的实验室时间：30 分钟

### 目标

在此实验室中，您将：

*   了解如何从 Oracle Cloud Marketplace 安装 Spatial Studio
*   了解如何在初始启动时设置 Spatial Studio 资料档案库方案

### 先备条件

*   Oracle Free Tier，Always Free，Paid 或 LiveLabs Cloud 账户
*   已创建资料档案库方案（练习 3）。

## 任务 1：从市场选择 Spatial Studio

1.  单击左上角的**导航菜单**，然后选择**市场**。

![Oracle Cloud Marketplace](https://oracle-livelabs.github.io/common/images/console/marketplace.png "市场")

2.  搜索 Spatial Studio，然后单击 Oracle Spatial Studio 应用程序

![Oracle Cloud Marketplace 中的 Oracle Spatial Studio](images/env-marketplace-2.png "Oracle Spatial Studio 市场映像")

3.  查看使用说明，然后接受条款和条件，然后单击“启动堆栈”

![启动堆栈以部署 Oracle Spatial Studio](images/env-marketplace-3.png "启动堆栈")

## 任务 2：创建堆栈向导

1.  （可选）输入部署堆栈的自定义名称和说明。然后选择要用于部署的区间，然后单击“Next（下一步）”

![创建堆栈向导](images/env-marketplace-4.png "使用向导创建堆栈")

2.  选择计算实例的可用性域和配置。

有关计算配置的详细信息，请参阅[此处](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm)。检查可用性域中所需配置的配额可用性。使用“Always Free（始终免费）”配置时，这一点尤其重要：\* 在 OCI 控制台中，导航到“Governance（监管）”>“Limits（限制）”、“Quota（限额）”和“Usage（使用情况）”\* 对于“Service（服务）”选择“Compute（计算）”和“Scope（范围）”选择“Availability Domain（可用性域）”\* 确认所需配置的可用性 \* 如果需要，更改“Availability Domain（可用性域）”选择以确定可用限额

![Oracle Cloud 资源的限制、配额和使用量](images/env-marketplace-4-1.png "计算资源的限制")

在确认配额后，请在“Create Stack（创建堆栈）”向导中进行选择。

![设置堆栈参数](images/env-marketplace-5.png "选择计算实例")

然后向下滚动。

3.  （可选）从默认值更改 HTTPS 端口和 Spatial Studio 管理员用户名。对于 Spatial Studio 管理员用户的身份验证，您可以选择使用 OCI Vault 密钥或密码。下图显示了使用口令的示例。对于生产部署，建议您使用 OCI Vault 密钥。向下滚动到网络配置部分。

注意：默认情况下，Spatial Studio 管理员用户名是 **admin** 。这是 Spatial Studio 应用程序用户，不同于在实验 3 中为数据库中存储的资料档案库方案创建的数据库用户名 (studio\_repo)。

![设置更多参数，如端口和密码](images/env-marketplace-6.png "Spatial Studio 高级配置 - Spatial Studio 管理员用户密码")

4.  对于网络，您可以选择自动创建新的 VCN 或现有 VCN。选择用于创建新 VCN 或搜索现有 VCN 的区间。

下图显示了使用“创建新 VCN”的示例。要使用现有 VCN，它必须位于上面在步骤 2 中选择的同一可用性域中。如果您没有其他现有 VCN，则剩余的默认值可以保持原样。如果存在其他现有 VCN，则更新 CIDR 值以避免冲突。

![配置网络](images/env-marketplace-7.png "Spatial Studio 高级配置 - 网络配置")

向下滚动到 "SSH Keys" 部分。

5.  加载 SSH 公共密钥允许出于管理目的访问 Spatial Studio 的文件系统。该对话框包含指向常规 SSH 连接文档的链接。通过浏览到密钥文件或复制粘贴密钥字符串来提交 SSH 公共密钥。如果从文件加载 SSH 公共密钥，则密钥文件名将显示如下图所示。单击“Next（下一步）”。

![添加 SSH 密钥](images/env-marketplace-8.png "Spatial Studio 高级配置 - 公共 SSH 密钥")

6.  查看条目的汇总。如果需要更正，请单击“返回”。否则，单击“Create（创建）”启动部署过程。您将重定向到部署的“作业详细信息”页。

![创建堆栈](images/env-marketplace-9.png "复查堆栈定义并创建堆栈")

## 任务 3：监控部署进度

1.  “作业详细信息”页面底部的“日志”部分将显示进度。它最初将在设置部署时显示微调器。

![监视堆栈部署作业 - Terraform 应用](images/env-marketplace-10.png "监视堆栈部署进度")

几分钟后，您将看到日志信息。

![记录有关部署作业的信息](images/env-marketplace-11.png "堆栈部署日志")

2.  向下滚动到日志部分的底部。完成后，您将看到应用完成！后跟实例详细信息。最后列出的项目是 Spatial Studio 公共 URL。复制此 URL 并粘贴到浏览器中。

![部署作业已成功完成](images/env-marketplace-12.png "已部署堆栈的输出变量")

## 任务 4：首次登录

1.  首次打开 Spatial Studio 公共 URL 将显示与隐私和安全相关的浏览器警告。具体警告取决于您的平台和浏览器。

![打开 Spatial Studio URL 时出现警告](images/env-marketplace-13.png "浏览器连接警告")

这不是 Spatial Studio 问题；访问没有签名 HTTPS 证书的网站是通用的。加载和配置签名证书将删除此警告。但是，在 Jetty 中加载证书的过程超出了本研讨会的范围。

单击该链接以继续访问网站。

2.  输入 Spatial Studio 管理员用户名（默认值为 admin）和您在步骤 2（创建堆栈向导，第 3 项）中输入的密码。然后单击“Sign In（登录）”。

![提供登录 Spatial Studio 的用户名和密码](images/env-marketplace-14.png "Spatial Studio 登录对话框")

3.  首次登录 Spatial Studio 实例时，系统会提示您输入数据库方案的连接信息，以将其用作 Spatial Studio 的元数据资料档案库。这是用于 Spatial Studio 的所有元数据的数据库方案，Spatial Studio 管理员用户也可以使用它来存储其他数据。您将使用在实验 3 中创建的方案，因此请选择 Oracle Autonomous Database，然后单击“Next（下一步）”。

![选择元数据连接类型](images/env-marketplace-15.png "选择 Spatial Studio 元数据资料档案库的类型")

4.  浏览（或拖放）在练习 3 中保存的 Wallet 文件。加载后，Wallet 文件名将列为“Selected Wallet（所选 Wallet）”。单击“OK（确定）”。

![加载 wallet](images/env-marketplace-16.png "上载连接 wallet")

5.  输入在实验 2 和服务中定义的用户名和密码。中等服务水平适合本次研讨会。单击“OK（确定）”。

![输入元数据资料档案库的连接详细资料](images/env-marketplace-17.png "输入连接详细资料")

6.  等待片刻，Spatial Studio 将其初始连接到方案并创建多个元数据表。完成后，Spatial Studio 将打开并显示入门信息。

![Spatial Studio 主页 - 入门](images/env-marketplace-18.png "Spatial Studio 登陆页面")

## 任务 5：加载数据并创建映射

要验证 Spatial Studio 是否正常运行，您将加载、准备和可视化小数据样本。数据包含博物馆列表，包括名称和地址。您将在交互式地图上对数据进行地理编码并可视化数据。

1.  您不会在此处创建连接，因为可以使用 Spatial Studio 资料档案库连接进行此验证。单击磁贴以**创建数据集**。

![启动向导以上载数据](images/verify-1.png "创建数据集")

2.  在[此处](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx)下载数据样例文件并保存到方便的位置。然后将文件拖放到文件上载磁贴中。您还可以单击文件上载磁贴并导航到文件。

![通过上载数据创建数据集](images/verify-2.png "上载现有电子表格数据")

3.  在数据预览中，将上载连接设置为 SPATIAL\_STUDIO，并将 POSTAL\_CODE 的数据类型设置为 STRING。然后单击**提交**。

![指定上载详细信息](images/verify-3.png "指定上载详细信息并检查列设置")

4.  上载完成后，将列出数据集，并显示一个警告图标，指示需要执行操作。单击警告图标，然后单击链接**转到数据集列**以分配键列。

![设置数据集的键列](images/verify-4.png "解决数据集问题 - 选择或添加键列")

5.  选择“名称”作为键，然后单击**验证键**。

![验证键](images/verify-5.png "验证所选键")

验证密钥后，单击**应用**。

6.  再次单击警告图标，然后单击 **Geocode Addresses（地理编码地址）**按钮以转换地址以协调地图可视化位置。

![地理编码地址](images/verify-7.png "解决数据集问题 - 地理编码地址")

7.  请注意，ADDRESS 和 POSTAL\_CODE 列是自动检测到的，用于地理编码。接受默认值，然后单击**应用**。

![地理编码地址映射](images/verify-8.png "使用地理编码参考数据映射数据集")

地理编码完成后，将返回到“Datasets（数据集）”页面。

8.  单击 SF\_AREA\_MUSEUMS 数据集的操作菜单，然后选择**创建项目**。

![开始创建项目](images/verify-9.png "为数据集创建新项目")

9.  单击并拖动 SF\_AREA\_MUSEUMS 数据集，然后放置在地图上的任何位置。

![添加数据集并将其拖到地图画布中](images/verify-10.png "将数据集作为层添加到项目")

SF\_AREA\_MUSEUMS 数据集将作为地图层添加，地图将平移并缩放到数据区域。

10.  单击 SF\_AREA\_MUSEUMS 层的操作菜单，然后选择**设置**

![数据层设置](images/verify-11.png "为数据层定义样式等")

11.  通过选择所选的颜色和不透明度对地图层进行样式设置。

![样式设置](images/verify-12.png "为数据层选择颜色和不透明度")

12.  单击**交互**选项卡，启用**显示信息窗口**，然后选择所有列。然后单击映射中的项以查看包含选定项的数据值的信息窗口。

![地图交互的设置](images/verify-13.png "定义与映射交互的详细信息")

这将验证基本数据准备和可视化是否正常工作。

13。单击左侧导航面板按钮可返回到“数据集”页。选择**放弃更改**选项，因为不需要保留此测试。

![放弃更改](images/verify-14.png "放弃对当前项目所做的更改")

14.  验证完成后，您可以删除测试数据集和数据库表。单击 SF\_AREA\_MUSEUMS 的操作菜单，然后选择**删除**

![删除数据集](images/verify-15.png "删除数据集")

15.  选择该选项以删除数据库表，然后单击**确定**。

![选中以永久删除数据库表](images/verify-16.png "删除与数据集相关的数据库表")

Oracle Spatial Studio 现已预配和测试。以下实验室提供了在不再需要时拆除 Spatial Studio 的步骤。

## 任务 6：卸载 Spatial Studio（不再需要时）

**如果要完全删除您的应用市场部署，请执行下列操作。**

1.  单击左上角的**导航菜单**，导航到**开发人员服务**，然后选择**堆栈**。

![清除所有部署的资源](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "删除市场部署")

2.  选择步骤 2 中使用的区间和名称。在下面所示的示例中，使用了名为沙盒的区间和名为 Oracle Spatial Studio 的堆栈。

![选择正确的区间并选择要删除的堆栈](images/env-marketplace-20.png "选择堆栈")

3.  选择 Terraform 操作 > 销毁

![销毁通过 Oracle Spatial Studio 堆栈部署的所有资源](images/env-marketplace-21.png "销毁已部署资源")

系统将提示您确认。这将删除应用市场部署创建的计算和网络构件。

4.  删除 Spatial Studio 应用程序后，资料档案库方案将保持原样。要删除系统信息库方案，请像在实验 3 中那样以 **admin** 身份连接到数据库并运行以下命令。

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## 了解详细信息

*   [Spatial Studio 产品页面](https://www.oracle.com/database/spatial/#rc30p2)
*   [开始使用 Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2023 年 3 月