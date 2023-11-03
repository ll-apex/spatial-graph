# 安裝 Spatial Studio

## 簡介

本實驗室將逐步介紹使用 Oracle Cloud Marketplace 佈建 Oracle Spatial Studio (Spatial Studio) 的流程。Oracle Cloud Marketplace 提供了 Oracle 和第三方提供的應用軟體與服務。如需詳細資訊，請參閱[這個網頁](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html)。

預估實驗室時間：30 分鐘

### 目標

在此實驗室中，您將：

*   瞭解如何從 Oracle Cloud Marketplace 安裝 Spatial Studio
*   瞭解如何在初始啟動時設定 Spatial Studio 儲存庫綱要

### 先決條件

*   一個 Oracle Free Tier，Always Free，Paid 或 LiveLabs Cloud 帳戶
*   已建立儲存區域綱要 (實驗室 3)。

## 工作 1：從 Marketplace 選取 Spatial Studio

1.  按一下左上方的**導覽功能表**，然後選取**市集**。

![Oracle Cloud Marketplace ](https://oracle-livelabs.github.io/common/images/console/marketplace.png "Marketplace")

2.  搜尋 Spatial Studio，然後按一下 Oracle Spatial Studio 應用程式

![Oracle Cloud Marketplace 中的 Oracle Spatial Studio](images/env-marketplace-2.png "Oracle Spatial Studio 市集映像檔")

3.  複查「使用說明」，然後接受條款與條件並按一下「啟動堆疊」

![啟動用於部署 Oracle Spatial Studio 的堆疊](images/env-marketplace-3.png "啟動堆疊")

## 作業 2：建立堆疊精靈

1.  選擇性地輸入部署堆疊的自訂名稱和描述。然後選取要用於部署的區間，然後按一下「下一步」

![建立堆疊精靈](images/env-marketplace-4.png "使用精靈建立堆疊")

2.  選取運算執行處理的可用性網域和資源配置。

如需運算型態的詳細資訊，請參閱[這個網頁](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm)。檢查可用性網域中所需資源配置的配額可用性。使用永遠免費資源配置時，尤其重要：\* 在 OCI 主控台中，瀏覽至「治理」>「限制、配額」以及「用量」\* 若為「服務」，請選取「運算」，若為「範圍」，請選取「可用性網域」\* 確認所需資源配置的可用性 \* 視需要變更可用性網域選項，以識別可用的配額

![Oracle Cloud 資源的限制、配額和使用量](images/env-marketplace-4-1.png "計算資源的限制")

已確認配額，請在「建立堆疊」精靈中選取項目。

![設定堆疊參數](images/env-marketplace-5.png "選取運算執行處理")

然後向下捲動。

3.  視需要從預設值變更 HTTPS 連接埠和 Spatial Studio 管理使用者名稱。若要認證 Spatial Studio 管理員使用者，您可以選擇使用 OCI 保存庫加密密碼或密碼。下圖顯示使用密碼的範例。對於生產環境部署，建議您使用 OCI 保存庫加密密碼。向下捲動至網路配置的區段。

注意：依預設，Spatial Studio 管理使用者名稱為 **admin** 。這是與儲存在資料庫中之儲存區域綱要在實驗室 3 中建立之資料庫使用者名稱 (studio\_repo) 不同的 Spatial Studio 應用程式使用者。

![設定其他參數，例如連接埠和密碼](images/env-marketplace-6.png "Spatial Studio 進階組態 - Spatial Studio 管理員使用者密碼")

4.  針對網路，您可以選擇自動建立新的 VCN 或現有的 VCN。選取要建立新 VCN 或搜尋現有 VCN 的區間。

下圖顯示使用「建立新 VCN」的範例。若要使用現有的 VCN，它必須與上述步驟 2 中所選取的可用性網域相同。如果您沒有其他現有的 VCN，則剩餘的預設值可以原樣保留。如果您有其他現有的 VCN，請更新 CIDR 值以避免衝突。

![設定網路](images/env-marketplace-7.png "Spatial Studio 進階組態 - 網路組態")

瀏覽至「SSH Keys (SSH 金鑰)」區段。

5.  載入 SSH 公開金鑰可針對管理目的，存取 Spatial Studio 的檔案系統。此對話方塊包含一般 SSH 連線文件的連結。瀏覽至金鑰檔案或複製貼上金鑰字串以送出您的 SSH 公開金鑰。如果您從檔案載入 SSH 公用金鑰，則金鑰檔案名稱將會如下圖所示。按 \[Next\] (下一步)。

![新增 SSH 金鑰](images/env-marketplace-8.png "Spatial Studio 進階組態 - 公用 SSH 金鑰")

6.  檢閱項目的摘要。如果需要更正，請按一下「上一步」。否則，請按一下「建立」以開始部署處理。系統會將您重新導向至部署的「工作詳細資訊」頁面。

![建立堆疊](images/env-marketplace-9.png "複查堆疊定義並建立堆疊")

## 作業 3：監督部署進度

1.  「工作詳細資訊」頁面底端的「日誌」區段會顯示進度。它一開始會在設定部署時顯示旋轉器。

![監督堆疊部署工作 - Terraform 套用](images/env-marketplace-10.png "監督堆疊部署進度")

在數分鐘後，您將看到日誌資訊。

![部署工作的日誌資訊](images/env-marketplace-11.png "堆疊部署日誌")

2.  向下捲動至日誌區段底端。完成後，您將會見到「套用完成」！後面接著執行處理詳細資訊。列出的最後一個項目是 Spatial Studio 公用 URL。複製此 URL 並貼至瀏覽器。

![部署工作已順利完成](images/env-marketplace-12.png "已部署堆疊的輸出變數")

## 作業 4：首次登入

1.  第一次開啟 Spatial Studio 公用 URL 將會顯示與隱私權和安全性相關的瀏覽器警告。特定的警告取決於您的平台與瀏覽器。

![開啟 Spatial Studio URL 時發出警告](images/env-marketplace-13.png "瀏覽器連線警告")

這不是 Spatial Studio 問題；一般來說是存取沒有已簽署 HTTPS 憑證的網站。載入和配置簽署的憑證會移除此警告。然而，在 Jetty 中載入憑證的程序超出本研討會的範圍。

按一下連結以繼續前往網站。

2.  輸入 Spatial Studio 管理員使用者名稱 (預設為管理)，以及您在步驟 2 (建立堆疊精靈，項目 3) 中輸入的密碼。然後按一下「登入」。

![提供使用者名稱和密碼以登入 Spatial Studio](images/env-marketplace-14.png "Spatial Studio 登入對話方塊")

3.  第一次登入 Spatial Studio 執行處理時，系統會提示您輸入資料庫綱要的連線資訊，以作為 Spatial Studio 的描述資料儲存區域。這是用於所有 Spatial Studio 描述資料的資料庫綱要，也可供 Spatial Studio 管理員使用者用來儲存其他資料。您將使用實驗室 3 中建立的綱要，選取 Oracle Autonomous Database 並按「下一步」。

![選擇描述資料連線類型](images/env-marketplace-15.png "選擇 Spatial Studio 描述資料儲存區域類型")

4.  瀏覽至 (或拖放) 儲存在實驗室 3 中的公事包檔案。載入之後，公事包檔案名稱將會列為選取的公事包。按一下「確定 (OK)」。

![上傳公事包](images/env-marketplace-16.png "上傳連線公事包")

5.  輸入實驗室 2 和服務中定義的使用者名稱和密碼。中等服務等級適用於此研討會。按一下「確定 (OK)」。

![輸入描述資料儲存區域的連線詳細資訊](images/env-marketplace-17.png "輸入連線詳細資訊")

6.  Spatial Studio 初始連線至綱要並建立數個描述資料表格時，請稍候。完成後，Spatial Studio 會開啟「入門」資訊。

![Spatial Studio 首頁 - 入門](images/env-marketplace-18.png "Spatial Studio 登陸頁面")

## 作業 5：載入資料與建立映射

若要驗證 Spatial Studio 是否正常運作，您將載入、準備及將小型資料範例視覺化。資料包含博物館清單，包括姓名與地址。您將會對互動式地圖上的資料進行地理編碼，並將資料視覺化。

1.  您將不會在此建立連線，因為您可以使用 Spatial Studio 儲存區域連線進行此驗證。按一下動態磚以**建立資料集**。

![啟動精靈以上傳資料](images/verify-1.png "建立資料集")

2.  從[此處](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx)下載資料範例檔案，然後儲存至方便的位置。然後將檔案拖放至檔案上傳動態磚。您也可以按一下檔案上傳動態磚並導覽至檔案。

![透過上傳資料建立資料集](images/verify-2.png "上傳現有試算表資料")

3.  在資料預覽中，將「連線」設為 SPATIAL\_STUDIO，並將 POSTAL\_CODE 的資料類型設為 STRING。然後按一下**送出 (Submit)** 。

![指定上傳詳細資訊](images/verify-3.png "指定上傳詳細資訊並檢查資料欄設定值")

4.  上傳完成時，將會列出資料集並顯示警告圖示，指出必須採取動作。按一下警告圖示，然後按一下**前往資料集資料欄**連結，以指定索引鍵資料欄。

![設定資料集的索引鍵資料欄](images/verify-4.png "解決資料集問題 - 選擇或新增索引鍵資料欄")

5.  選取 NAME 作為索引鍵，然後按一下**驗證索引鍵**。

![驗證索引鍵](images/verify-5.png "驗證選擇的索引鍵")

驗證金鑰之後，請按一下**套用**。

6.  再按一下警告圖示，然後按一下按鈕以**地理代碼地址**，將地址轉換為協調地圖視覺化的地點。

![地址](images/verify-7.png "解決資料集問題 - 地理代碼地址")

7.  請注意，系統會自動偵測 ADDRESS 和 POSTAL\_CODE 資料欄以用於地理編碼。接受預設值並按一下**套用**。

![地理區域地址對應](images/verify-8.png "將資料集與地理編碼參考資料對應")

地理編碼完成時，會返回「資料集」頁面。

8.  按一下 SF\_AREA\_MUSEUMS 資料集的動作功能表，然後選取**建立專案**。

![開始建立專案](images/verify-9.png "為資料集建立新專案")

9.  按一下並將 SF\_AREA\_MUSEUMS 資料集拖放至地圖上的任何位置。

![新增資料集並將其拖曳至地圖畫面](images/verify-10.png "將資料集新增為專案的層級")

SF\_AREA\_MUSEUMS 資料集將新增為地圖圖層，地圖將會平移並縮放至資料區域。

10.  按一下 SF\_AREA\_MUSEUMS 層的動作功能表，然後選取**設定值**

![資料層設定值](images/verify-11.png "定義資料層的樣式和其他樣式")

11.  選取您選擇的顏色與透明度來設定地圖圖層樣式 。

![樣式設定](images/verify-12.png "選擇資料層的顏色與透明度")

12.  按一下**互動**頁籤，啟用**顯示資訊視窗**，然後選取所有資料欄。然後按一下地圖中的項目，以查看具有所選項目之資料值的資訊視窗。

![地圖互動的設定](images/verify-13.png "定義與地圖互動的詳細資料")

這樣可以驗證基本的資料準備和視覺化是否正常運作。

13\. 按一下左側導覽面板按鈕以返回「資料集」頁面。選取**捨棄變更**選項，因為您不需要保留此測試。

![捨棄變更](images/verify-14.png "捨棄目前專案的變更")

14.  驗證完成後，您可以刪除測試資料集與資料庫表格。按一下 SF\_AREA\_MUSEUMS 的動作功能表，然後選取**刪除**

![刪除資料集](images/verify-15.png "刪除資料集")

15.  選取刪除資料庫表格的選項，然後按一下**確定**。

![如果勾選，即可永久刪除資料庫表格](images/verify-16.png "刪除與資料集相關的資料庫表格")

現在已佈建並測試 Oracle Spatial Studio。下列實驗室提供不再需要 Spatial Studio 的步驟。

## 工作 6：解除安裝 Spatial Studio (不再需要時)

**如果您要完全移除市集部署，請繼續下列作業。**

1.  按一下左上方的**導覽功能表**，瀏覽至**開發人員服務**，然後選取**堆疊**。

![清除所有已部署的資源](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "移除市集部署")

2.  選擇 STEP 2 中使用的區間和名稱。在下方顯示的範例中，使用了一個名為 sandbox 和名為 Oracle Spatial Studio 的堆疊。

![選擇正確的區間並選取要刪除的堆疊](images/env-marketplace-20.png "選取堆疊")

3.  選取 Terraform 動作 > 毀棄

![毀棄透過 Oracle Spatial Studio 堆疊部署的所有資源](images/env-marketplace-21.png "毀棄已部署的資源")

系統會提示您進行確認。這將會移除市集部署所建立的運算和網路使用者自建物件。

4.  移除 Spatial Studio 應用程式之後，您的儲存區域綱要會維持在原位狀態。若要移除儲存區域綱要，請以 **admin** 的身分連線至資料庫，並執行以下作業。

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## 進一步瞭解

*   [Spatial Studio 產品頁面](https://www.oracle.com/database/spatial/#rc30p2)
*   [開始使用 Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - 資料庫產品管理 David Lapp - 2023 年 3 月