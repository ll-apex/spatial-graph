# 簡介

## 關於 Oracle Spatial

Oracle 的使命是協助人們以新方式查看資料、發現洞察力，以及發揮無限可能性。空間分析是關於瞭解地理關係的複雜互動 - 根據人員、資產和資源所在位置回答問題。空間洞察力可讓您提供更佳的客戶服務、將人力最佳化、尋找零售和配銷中心、評估銷售和行銷活動等等。借助 Oracle 的空間方案，開發人員、資料庫專業人員以及分析師可以使用完整的空間資料管理、分析和視覺化工具套件，將空間分析和對應整合到企業級資料管理基礎架構上的應用系統 - Oracle Database 和 Oracle Exadata。Oracle Cloud 和 Oracle Autonomous Database 的創新技術，是業界唯一具備自我驅動、自我保護及自我修復能力的資料庫，可用於空間應用程式。

如下圖所示，Oracle Database 的空間功能為基本和進階空間資料類型提供可擴展且高效能的儲存、處理及分析。也會提供一系列可部署的 Java EE 元件，以支援常見的中間層服務。

![影像替代文字](./images/spatial-platform.png)

如需更多資訊，請造訪 \[https://oracle.com/goto/spatial\] (https://oracle.com/goto/spatial)

預估研討會時間：60 分鐘

### 工作室簡介

在此研討會中，您將建立、設定及分析空間資料。您將從通用格式建立並設定 STORES、WAREHOUSES、REGIONS 及 TORNADO\_PATHS 的空間表格，然後執行空間查詢以根據鄰近與包含內容來探索其關係。您終於使用 ADB 中的原生 JSON 支援將結果轉換為開發者整合。

以位置為基礎的資訊 (例如以空間鄰近和容器為基礎的資料) 關聯的能力，在無數的情況下非常有價值。沒有與商店地點和倉庫關聯的已預先存在金鑰。不過，「空間」可讓這類關係根據鄰近度來決定。同樣地，商店地點與區域之間沒有預先存在的關係，例如稅捐區域。但是空間可以根據容器來決定其關係。「空間」可進一步啟用以位置為基礎的分析，例如根據鄰近來彙總資訊；例如，與位置之間距離的龍捲風造成的損失。您可以在個別系統中利用 ADB 的內建空間功能，而非在個別系統中執行這些分析。

在本研討會中，您將獲得上述所有功能的經驗。

### 先決條件

\- 一個 Oracle Cloud 帳戶 \- 此研討會需要存取 Oracle Database 和 SQL 從屬端 (亦即 SQL Developer、SQL Developer Web、SQL\*Plus) . - 如果您已經可以存取這些項目，請依照此「簡介」中的指示操作，前往「建立範例資料」一節。- 否則，您應該繼續前往 Oracle Cloud 帳戶、Autonomous Database 以及 SQL Developer Web 小節。- 不需要使用 Oracle Spatial。- Oracle Cloud 帳戶

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **貢獻者** - Karin Patenge，Database Product Management，Oracle
*   **上次更新者 / 日期** - David Lapp，2022 年 9 月