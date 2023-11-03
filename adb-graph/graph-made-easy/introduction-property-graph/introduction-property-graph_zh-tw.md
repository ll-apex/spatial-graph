# 使用 Graph Studio

## 關於此研討會

本研討會介紹使用 Autonomous Database 中的 Graph Studio 功能的重要圖表資料模型製作與分析概念。它會顯示如何使用圖表查詢來尋找可能表示詐欺交易的循環付款，以及圖形分析演算法來識別大量交易流程的帳戶。您將查詢包含 (人工) 帳戶和交易資訊的資料。您可以從建立圖表、查詢圖表、執行分析演算法及將結果視覺化開始。選擇性區段會介紹常用於 Knowledge Graph 的語意 (RDF) 圖形概念，並向您展示如何從標準 RDF 圖形格式 (例如 n 三個格式) 載入資料，以及如何使用 RDF 圖表的查詢語言 SPARQL 來查詢資料。

預估研討會時間：75 分鐘

若想要觀看研討會，請點選[此處](https://youtu.be/Ymk9TE9Q2K4)。

### 關於 Graph Studio

Oracle Autonomous Database 的功能可以作為可擴展的圖表資料庫。並自動從資料庫表格建立圖表模型與記憶體內圖表。包括筆記本和開發人員 API，可用於使用 PGQL (類似 SQL 的圖形查詢語言)、使用 Java 或 Python API 執行圖形查詢，以及原生圖形視覺化。

請觀看下列兩個影片以取得 Graph Studio 的詳細資訊。第一部分是產物圖及其使用案例的簡介。第二部分是 Graph Studio 介面的導覽。

[使用 Autonomous Database 簡化圖表分析](youtube:eCd-969hrak)使用 Autonomous Database 簡化圖表分析

[Autonomous Database：Graph Studio 介面導覽](youtube:S6Q-IJcBkU0) Autonomous Database：Graph Studio 介面導覽

### 目標

在此研討會中，您將：

*   使用 PGQL (圖形查詢語言) CREATE PROPERTY GRAPH 敘述句建立圖表
*   將圖表載入記憶體以進行分析
*   建立記事本
*   使用 PGQL 記事本段落查詢圖表並以視覺化方式呈現
*   執行圖形演算法並以視覺化方式呈現結果

### 先決條件

*   Oracle Cloud 帳戶
*   佈建的 Autonomous Database 無伺服器執行處理

結束此實驗室。**您現在可以開始進行下一個實驗室。**

## 確認

*   **作者** - 產品管理 Jayant Sharma
*   **貢獻者** - Jayant Sharma，產品管理
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，產品經理，2023 年 8 月