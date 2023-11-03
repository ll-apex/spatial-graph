# 簡介

## 關於此研討會

在此研討會中，您將從 OCI Cloud Marketplace 將 Spatial Studio 佈建至 Oracle Cloud，並在 Autonomous Database 中準備要作為 Spatial Studio 描述資料儲存區域的綱要。

預估研討會時間：60 分鐘

### 關於 Oracle Spatial Studio

Oracle Spatial Studio (Spatial Studio) 是一項 Web 應用程式，可讓您自行存取 Oracle Database 的空間功能。雖然這些功能在歷史上都需要編碼和 (或) 使用第三方工具，但 Spatial Studio 可讓業務使用者使用自助服務 UI 建立和共用空間分析和互動式 Web 地圖。

![影像替代文字](./images/spatial-studio.png "空間工作室")

Spatial Studio 會針對 Oracle Database 中的空間資料運作，這表示包含 Oracle 幾何資料類型的表格和視觀表。此資料是預先存在的空間資料，或是使用 Spatial Studio 準備的非空間資料，以根據屬性新增幾何圖形。

Spatial Studio 是一種 Java EE 應用程式，可以從 Oracle Cloud Marketplace 部署到 Oracle Cloud。Spatial Studio 也可以手動部署至 Oracle WebLogic 或 Jetty，或自行包含的預先部署快速啟動進行測試。

如需更多資訊，請造訪 \[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)

### 目標

*   瞭解如何建立及指派 Spatial Studio 之描述資料儲存區域的資料庫綱要
*   瞭解如何使用 Cloud Marketplace 來安裝 Spatial Studio
*   瞭解如何在不再需要時解除安裝 Spatial Studio

### 先決條件

*   此研討會需要 Oracle Autonomous Database。
*   SQL Developer Web 隨附於 Autonomous Database，也可用來建立 Spatial Studio 儲存庫綱要。
*   如果您已經可以存取這些項目，則請遵循此「簡介」來略過實驗室 3。
*   否則，您應該繼續實驗室 1。
*   不需要使用 Oracle Spatial 的使用經驗。
*   Oracle Cloud 帳戶 - 請檢視此研討會的 LiveLabs 登陸頁面，查看支援的環境

_注意：如果您有**免費試用**帳戶，當您的免費試用到期時，您的帳戶將會轉換為**永遠免費**帳戶。除非 Always Free 環境可供使用，否則您將無法進行 Free Tier 工作坊。**[按一下此處以取得免費層常見問題頁面。](https://www.oracle.com/cloud/free/faq.html)**_

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - Database Product Management 的 David Lapp - 2021 年 1 月