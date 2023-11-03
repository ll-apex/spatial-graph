# 在 Graph Studio 中使用 RDF 图形

## 简介

Oracle Autonomous Database 中的 Graph Studio 支持用户对图形数据进行建模、创建、查询和分析。它包括笔记本、使用 PGQL 执行图形查询的开发人员 API、60 多个内置图形算法，并提供数十种可视化功能，包括本机图形可视化。除了属性图之外，Graph Studio 现在还扩展了对语义技术的支持，包括基于资源描述框架 (RDF) 和 Web 本体语言 (OWL) 的数据和本体的存储、推理和查询功能。您现在可以将 Graph Studio 用于以下支持的 RDF 功能：

*   创建 RDF 图形
*   对笔记本段落中的 RDF 图形执行 SPARQL 查询
*   分析和可视化 RDF 图形

RDF 是用于表示链接数据的 W3C 标准数据模型。RDF 使用统一资源标识符 (Uniform Resource Identifier，URI) 作为资源和 URI 的全局唯一标识符来命名两个资源之间的关系。除了 URI，RDF 还使用文字来表示标量值，如数字、字符串和时间戳。RDF 模型将数据链接为有指示的有标签图形，其中每个边缘通常称为三重。边缘的源顶点称为三重主题。边缘的标签或名称称为三元组的谓词，边缘的目标顶点称为三元组的对象。RDF 图形特别适合知识图和数据集成应用程序，因为 URI 提供全局唯一标识符，简单、无模式的三重结构使将数据从多个不同的 RDF 图形组合成单个图形变得非常容易。此外，RDFS 和 OWL 提供了标准方法来定义可重复使用的词汇（语义上有意义的边缘标签和资源类型集），以获得更可互操作和机器可处理的图形数据。有关 W3C RDF 1.1 标准的更多信息，请参见[此处](https://www.w3.org/TR/rdf11-primer/)。

SPARQL 协议和 RDF 查询语言 (SPARQL) 是 W3C 标准化的用于查询资源说明框架 (Resource Description Framework，RDF) 数据的技术之一。您可以在[此处](https://www.w3.org/TR/sparql11-overview/)阅读有关 W3C SPARQL 1.1 标准的更多信息。

SPARQL 使用 **SELECT 某些元素 WHERE 某些条件**结构指定查询。SPARQL 查询的 WHERE 子句中的条件是使用三重模式构建的，这本质上是 RDF 三重模式，其中三重元素可以替换为查询变量（用 ？前缀表示）。三重模式中的查询变量充当通配符。考虑三重模式 **？movie ms:genre ms:genre\_Comedy** 。根据 RDF 图形评估此三重模式时，它将返回谓词为 **ms:genre** 和 **object ms:genre\_Comedy** 的三重对象的所有 **subjects** 。SPARQL SELECT 子句指定从查询到项目的查询变量的列表。在 SPARQL 语法中，URI 用尖括号括起来，文字用双引号括起来（例如 "Kevin Bacon"）。文字后跟 ^^ 和数据类型 URI（例如 "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer) ），或者后跟 @ 和语言标记（例如 “Jalapeño”@es）。SPARQL 支持大多数 XML 模式数据类型，不带数据类型 URI 的纯文本被视为数据类型 [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string) 。

下面的视频是使用将在本实验中使用的类似数据集的演示示例。该视频强调了使用 RDF 的电影结构的本体结构。此演示使用临时表与 SQL Developer 结合使用 RDF Graph，这与 Autonomous Database 版本的实验室截然不同。但是，用于查询和可视化数据的 SPARQL 语言与上下文非常相似。

[](youtube:e_EQjInas50)

在此实验室中，将使用 SPARQL 构建语义图，SPARQL 是集成不同数据源的标准化方法。此过程将介绍如何使用基于图形的查询和可视化来分析数据。

估计时间：35 分钟

### 目标

*   准备环境
*   RDF 图形入门
*   在 Graph Studio 中创建和验证 RDF 图形用户
*   查询和可视化 RDF 图形

### 先备条件

此实验室假定您具有：

*   Oracle Cloud 账户 - 请查看本研讨会的 LiveLabs 登陆页面，了解哪些环境受支持

*   使用此[链接](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)下载 MOVIESTREAM 文件 (moviestream\_rdf.nt)

这个实验室结束了。现在，您可以_进入下一个实验室_。

## 确认

*   **作者** - Nicholas Cusato、Ethan Shmargad、Matthew McDaniel 解决方案工程师、Ramu Murakami Gutierrez 产品经理
*   **技术贡献者** - Lavanya Jayapalan 首席用户帮助开发人员 Melliyal Annamalai 杰出产品经理 Joao Paiva 技术人员咨询成员
*   **上次更新者/日期** - Ramu Murakami Gutierrez 产品经理，2023 年 6 月