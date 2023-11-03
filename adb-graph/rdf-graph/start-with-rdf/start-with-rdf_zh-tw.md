# 開始使用 RDF 圖表

## 簡介

此實驗室會逐步引導您完成將 RDF 資料上傳至將連結至 Autonomous Database 之儲存桶的入門步驟。這需要從設定檔複製正確的 OCI 使用者名稱。若要允許 Graph Studio 存取 OCI 物件儲存中的 RDF 資料 (使用 DBMS\_CLOUD 套裝程式)，您必須使用您的 OCI 帳戶建立存取權杖。這將用於次要實驗室。

預估時間：5 分鐘

### 目標

*   將 RDF 資料上傳至 OCI 物件儲存
*   檢視您的 OCI 使用者名稱
*   產生存取權杖

### 先決條件

此實驗室假設您具有：

*   Oracle Cloud 帳戶
*   使用此[連結](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)下載 MOVIESTREAM 檔案 (moviestream\_rdf.nt)

## **作業 1：** 將 RDF 資料上傳至 OCI 物件儲存

1.  使用您的 Oracle Cloud 證明資料登入 OCI 主控台。
2.  開啟導覽功能表，然後按一下「儲存」。在「物件儲存與封存儲存」底下，按一下「儲存桶」，如下所示：![描述功能表中區段資料夾選取位置的影像](./images/buckets-folder.png)
3.  選取適用於您 OCI 帳戶的區間。 ![此影像顯示「儲存桶」頁面上的「區間」下拉式功能表位置](./images/compartment-menu.png)
4.  按一下「建立儲存桶」。「建立儲存桶」滑動軸便會開啟，如下所示： ![描述「建立儲存桶」頁面的影像](./images/create-bucket.png)
5.  輸入「儲存桶名稱」，將所有其他項目保留為預設值，然後按一下「建立」。儲存桶會建立並列在「儲存桶」頁面上，如下所示： ![顯示建立儲存桶結果的影像](./images/bucket-result.png)
6.  按一下 RDF\_DATA\_BUCKET 連結，然後瀏覽至「儲存桶詳細資訊」頁面。

![顯示「儲存桶」頁面建立後的影像](./images/bucket-page.png) 7.7 公里按一下「物件」區段中的「上傳」。「上傳物件」滑動軸便會開啟。 8. 選取本機系統上下載的 RDF moviestream\_rdf.nt 檔案[連結](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)，然後按一下「上傳」。檔案已順利上傳。按一下「關閉」即可返回「儲存桶詳細資訊」頁面。上傳的檔案會列在「物件」下方，如下所示： ![顯示上傳至儲存桶之物件的圖像](./images/image-upload.png)

1.  選取已上傳檔案的「動作」功能表，然後按一下「檢視物件詳細資訊」以存取已上傳檔案的特性。\[ 物件詳細資訊 \] 滑動軸會開啟，如下所示： ![此影像顯示反白顯示「檢視物件明細」選項的「物件功能表」](./images/object-details.png)
2.  記下物件的 URL 路徑。這是用於 Graph Studio 的 RDF 匯入精靈。 ![顯示在何處尋找儲存桶中物件的 URL 路徑的影像](./images/url-path.png)

## **作業 2：** 檢視您的 OCI 使用者名稱

1.  按一下右上角的頭像圖示來開啟您的設定檔。設定檔底下的第一個項目是您的 OCI 使用者名稱。 ![顯示如何存取 OCI 設定檔的影像](./images/oci-profile.png)
2.  請注意您的 OCI 使用者名稱。這是用於 Graph Studio 的 RDF 匯入精靈。 ![顯示「使用者詳細資訊」之 OCI 使用者名稱的影像](./images/oci-username.png)

## **作業 3：** 從 OCI 主控台產生存取權杖

1.  使用您的 Oracle Cloud 證明資料登入 OCI 主控台。
    
2.  按一下右上角的頭像圖示來開啟您的設定檔，然後按一下「使用者設定值」。 ![顯示如何從設定檔存取「使用者設定值」的影像](./images/user-settings.png)
    
3.  按一下資源下的認證權杖，如下所示： ![顯示如何從「使用者設定值」的「資源」功能表存取認證權杖的影像](./images/auth-tokens.png)
    
4.  按一下「產生權杖」。「產生記號」對話方塊便會開啟。 ![顯示如何產生認證權杖的影像](./images/gen-tokens.png)
    
5.  輸入描述並按一下「產生權杖」。產生的權杖詳細資訊會顯示如下： ![顯示如何複製產生之認證權杖的影像](./images/token-details.png)
    
6.  按一下「複製」以複製記號並儲存以供日後使用。
    

結束此實驗室。_您現在可以開始進行下一個實驗室。_

## 確認

*   **作者** - 傑出產品經理 Melliyal Annamalai
*   **技術貢獻者** - 聖莫尼卡專家中心 Nicholas Cusato
*   **上次更新者 / 日期** - 聖莫尼卡專家中心 Nicholas Cusato，2022 年 2 月 25 日