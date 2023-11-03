# 简介

## 关于此研讨会

在本研讨会中，您将从 OCI Cloud Marketplace 将 Spatial Studio 预配到 Oracle Cloud，并在 Autonomous Database 中准备方案以用作 Spatial Studio 的元数据存储库。

估计研讨会时间：60 分钟

### 关于 Oracle Spatial Studio

Oracle Spatial Studio (Spatial Studio) 是一个 Web 应用程序，提供对 Oracle Database 的空间功能的自助访问。尽管这些功能历来需要编码和/或使用第三方工具，但 Spatial Studio 允许业务用户使用自助 GUI 创建和共享空间分析和交互式 Web 地图。

![图像替代文本](./images/spatial-studio.png "空间工作室")

Spatial Studio 对 Oracle Database 中的空间数据进行操作，即包含 Oracle 几何数据类型的表和视图。这些数据是预先存在的空间数据或非空间数据，这些数据是使用 Spatial Studio 准备的，以根据属性添加几何图形。

Spatial Studio 是可从 Oracle Cloud Marketplace 部署到 Oracle Cloud 的 Java EE 应用程序。Spatial Studio 也可以手动部署到 Oracle WebLogic 或 Jetty，或者作为自包含的预部署快速入门进行测试。

有关详细信息，请访问 \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### 目标

*   了解如何为 Spatial Studio 的元数据资料档案库创建和分配数据库方案
*   了解如何使用云市场安装 Spatial Studio
*   了解如何在不再需要时卸载 Spatial Studio

### 先备条件

*   本研讨会需要 Oracle Autonomous Database。
*   SQL Developer Web 随 Autonomous Database 提供，还用于创建 Spatial Studio 资料档案库方案。
*   如果您已具有这些访问权限，则按照本简介，您可以跳至 Lab 3。
*   否则，您应转到 Lab 1。
*   以前不需要具备 Oracle Spatial 经验。
*   Oracle Cloud 账户 - 请查看本研讨会的 LiveLabs 登陆页面，了解哪些环境受支持

_注意：如果您有**免费试用**账户，当您的免费试用到期时，您的账户将转换为**始终免费**账户。除非“始终免费”环境可用，否则您将无法执行“免费套餐”研讨会。**[单击此处查看“免费套餐常见问题解答”页面。](https://www.oracle.com/cloud/free/faq.html)**_

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **上次更新者/日期** - David Lapp，数据库产品管理，2021 年 1 月