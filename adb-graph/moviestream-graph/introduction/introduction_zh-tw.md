# 使用圖表分析建議影片

## 簡介

在此研討會中，您將使用 Graph Studio 根據影片觀賞行為偵測並建立客戶社群。建立社群後，請根據社群成員觀看的內容提出建議。

預估時間：60 分鐘

### 關於 Graph Studio

Oracle Autonomous Database 的功能可以作為可擴展的特性圖資料庫。並自動從資料庫表格建立圖表模型與記憶體內圖表。包括筆記本和開發人員 API，可用於使用 PGQL (類似 SQL 的圖形查詢語言) 執行圖表查詢，以及超過 60 種內建圖形演算法，以及許多視覺化，包括原生圖形視覺化。

觀看下列影片，瞭解特性圖及其使用案例的簡介。

使用 Autonomous Database 簡化圖表分析

[](youtube:eCd-969hrak)

在此研討會中，您將使用從 MOVIE、CUSTOMER\_PROMOTIONS 和 CUSTSALES\_PROMOTIONS 表格建立的圖表。MOVIE 和 CUSTOMER\_PROMOTIONS 是頂點表格 (這些表格中的每個資料列都變成頂點)。CUSTSALES\_PROMOTIONS 會連線兩個表格，而且是邊緣表格。每當 CUSTOMER\_PROMOTIONS 中的客戶在 MOVIE 表格中轉譯影片時，即圖表中的邊緣。已建立此圖表供您在此研討會中使用。

分析圖表時，您可以選擇超過 60 個預先建置的演算法。在此研討會中，您將使用**個人化 SALSA** 演算法，這是產品建議的最佳選擇。客戶頂點會對應至 _Hub_ ，影片會對應至_權限_。中樞分數越高表示客戶之間關係越趨緊密。較高的授權分數表示頂點 (或電影) 在建立接近度方面扮演更重要的角色。

### 目標

在此研討會中，您將使用 Autonomous Database 的 Graph Studio 功能來：

*   使用記號
*   執行幾個 PGQL 圖表查詢
*   使用 python 從演算法程式庫執行 Personalized SALSA
*   查詢並儲存建議

### 先決條件

*   Oracle Cloud 帳戶

## 確認

*   **作者** - Oracle Spatial and Graph 產品經理 Melli Annamalai
*   **貢獻者** - Jayant Sharma
*   **上次更新者 / 日期** - 2023 年 2 月 Oracle Spatial and Graph 產品經理 Ramu Murakami Gutierrez