# 使用图形分析推荐电影

## 简介

在本研讨会中，您将使用 Graph Studio 根据观看电影的行为检测和创建客户社区。一旦创建了社区，请根据社区成员所关注的内容提出建议。

估计时间：60 分钟

### 关于 Graph Studio

Oracle Autonomous Database 具有多种功能，可将其用作可扩展的属性图形数据库。它们基于数据库表自动创建图形模型和内存中图形。它们包括用于使用 PGQL（一种类似 SQL 的图形查询语言）和 60 多种内置图形算法执行图形查询的笔记本和开发人员 API，以及许多可视化（包括本机图形可视化）。

观看以下视频，了解属性图及其用例。

使用 Autonomous Database 简化图形分析

[](youtube:eCd-969hrak)

在本研习会中，您将使用从表“电影”、“CUSTOMER\_PROMOTIONS”和“CUSTSALES\_PROMOTIONS”创建的图形。MOVIE 和 CUSTOMER\_PROMOTIONS 是顶点表（这些表中的每一行都变为顶点）。CUSTSALES\_PROMOTIONS 连接两个表，是边缘表。每次 CUSTOMER\_PROMOTIONS 中的顾客在表“电影”中租赁一部电影时，都会在图形中占据边缘。已创建此图表供您用于本研习会。

在分析图形时，您可以选择 60 多种预构建算法。在本研讨会中，您将使用**个性化 SALSA** 算法，该算法是推荐产品的好选择。客户顶点映射到 _hubs_ ，电影映射到 _authorities_ 。较高的中心分数表示客户之间的关系更密切。更高的权威分数表明，顶点（或电影）在建立这种亲密关系中起着更重要的作用。

### 目标

在本研讨会中，您将使用 Autonomous Database 的 Graph Studio 功能：

*   使用笔记本
*   运行一些 PGQL 图形查询
*   使用 python 从算法库运行个性化 SALSA
*   查询并保存建议

### 先备条件

*   Oracle Cloud 帐户

## 确认

*   **作者** - Oracle Spatial and Graph 产品经理 Melli Annamalai
*   **贡献者** - Jayant Sharma
*   **上次更新者/日期** - Oracle Spatial and Graph 产品经理 Ramu Murakami Gutierrez，2023 年 2 月