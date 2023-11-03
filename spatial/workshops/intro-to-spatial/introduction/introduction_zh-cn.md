# 简介

## 关于 Oracle Spatial

Oracle 的使命是帮助人们以新的方式查看数据、发现洞察并释放无限可能。空间分析是关于理解基于地理关系的复杂交互 - 根据人员，资产和资源的位置回答问题。借助空间洞察，您可以提供更优质的客户服务、优化员工队伍、定位零售和配送中心、评估销售和营销活动等。借助 Oracle 空间产品，开发人员、数据库专业人员和分析人员可以使用一整套空间数据管理、分析和可视化工具，将空间分析和映射集成到企业级数据管理基础设施（Oracle Database 和 Oracle Exadata）上的应用中。Oracle Cloud 和 Oracle Autonomous Database 是业内唯一的自治驾驶、自我保护和自我修复数据库，这些创新技术可供空间应用使用。

如下所示，Oracle Database 的空间功能可为基本和高级空间数据类型提供可扩展的高性能存储、处理和分析。还提供了一系列可部署的 Java EE 组件来支持常见的中间层服务。

![图像替代文本](./images/spatial-platform.png)

有关详细信息，请访问 \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

估计研讨会时间：60 分钟

### 研讨会概览

在本研讨会中，您将创建、配置和分析空间数据。您将基于常用格式为 STORES、WAREHOUSES、REGIONS 和 TORNADO\_PATHS 创建和配置空间表，然后执行空间查询以根据邻近性和包含性来了解其关系。最后，您可以使用 ADB 中的原生 JSON 支持来转换结果，以实现开发人员集成。

基于位置关联信息的能力，例如基于空间邻近性和封闭性的相关数据，在无数情况下是非常有价值的。不存在将门店位置与仓库相关联的预先存在的关键字。但是空间使这种关系能够根据邻近性来确定。同样，门店地点与区域之间不存在预先存在的关系，例如纳税区域。但是 Spatial 使他们的关系能够根据遏制来确定。此外，Spatial 还支持基于位置的分析，例如基于邻近性汇总信息；例如，由于龙卷风在距离某个位置的距离内丢失。您可以利用 ADB 的内置空间功能，而不是在单独的系统中执行这些分析。

您将获得本研讨会中上述所有功能的经验。

### 先备条件

\- Oracle Cloud 账户 \- 本研讨会要求访问 Oracle Database 和 SQL 客户端（即 SQL Developer、SQL Developer Web、SQL\*Plus）。- 如果您已经有权访问这些客户端，则按照本“简介”部分可以跳至“创建示例数据”部分。- 否则，应继续执行 Oracle Cloud 账户、Autonomous Database 和 SQL Developer Web 部分。- 不需要以前使用 Oracle Spatial 的经验。- Oracle Cloud 账户

## 确认

*   **作者** - David Lapp，Oracle 数据库产品管理
*   **贡献者** - Oracle 数据库产品管理云平台 Karin Patenge
*   **上次更新者/日期** - David Lapp，2022 年 9 月