# 將圖表視覺化

## 簡介

使用「圖形視覺化」功能，可以輕鬆地將先前實驗室中完成的分析結果視覺化。

估計時間：5 分鐘

下列影片提供「圖形視覺化」元件 (= GraphViz) 的簡介。

[中文版 \_ English](youtube:zfefKdNfAY4)

### 目標

*   瞭解如何執行 PGQL 圖表查詢及將結果視覺化。

### 先決條件

*   已建立並發布圖表
*   Graph Server (使用 GraphViz) 已啟動並在執行中

## 任務 1：登入 GraphViz

使用 Web 瀏覽器開啟 GraphViz，網址為 **`https://<public_ip_for_compute>:7007/ui`** 。將 **`<public_ip_for_compute>`** 取代為您的 Graph Server 運算執行處理。

由於市集映像檔是以自行簽署的 SSL 憑證散布，因此您應在生產環境中變更自己的憑證。同時，Web 瀏覽器應顯示警告，同時我們瞭解安全警告。

如果您使用 **Chrome** ，請在警告視窗中輸入 **thisisunsafe** 以移至 GraphViz 畫面。

![登入色](images/login-chrome.jpg)

使用 **Firefox** ，依序按一下 **進階**、**接受風險並繼續**。

![登入 -firefox](images/login-firefox.jpg)

您看到的畫面應該類似下方的螢幕擷取畫面。輸入使用者名稱 (**customer\_360**) 與密碼，然後按一下「提交」。 **Graph Server** 是「進階選項」中的預設值，因此您不需要變更。

![登入](images/login.jpg)

## 作業 2：修改查詢

修改查詢以取得前 5 個資料列，亦即將 **LIMIT 100** 變更為 **LIMIT 5** ，然後按一下「執行」。

您看到的圖表應該類似下方的螢幕擷取畫面。

![show-5-elements](images/show-5-elements.jpg)

## 任務 3：新增重點

現在讓我們加入一些標籤與其他視覺內容。這些稱為重點。按一下[此處](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip)以下載 zip 檔案 highlights.json.zip。解壓縮此檔案，並記下解壓縮的位置。

按一下**設定值** (位於畫面右側) 下的「載入」按鈕。瀏覽至適當的資料夾並選擇檔案，然後按一下 \[Open\] (開啟) 以載入該檔案。

![亮白 -1](images/highlights-1.png)

圖表現在看起來會像

![亮白 -2](images/highlights-2.png)

## 任務 4：模式與 PGQL 相符

1.  接下來，讓我們執行一些 PGQL 查詢。
    
    [pgql-lang.org](http://pgql-lang.org) 網站和[規格](http://pgql-lang.org/spec/1.4)是詳細資訊和範例的最佳參考。不過，在本實驗中，基本知識就是最低。
    
    PGQL 查詢的一般結構為：
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL 提供特定的建構，稱為 **MATCH** 子句來比對圖形模式。圖形樣式會比對符合指定條件和限制條件的頂點和邊緣。
    
    *   **(v)** 表示頂點變數 **v**
    *   **\-** 表示未導向的邊緣，如 (來源) - (目的地)
    *   **\->** 從來源到目標的外送邊緣
    *   **<-** 從目的地到來源的內送邊緣
    *   **\[e\]** 表示邊緣變數 **e**
    
    此外，請在此省略 **graph\_name** ，因為它已從 GraphViz UI 選取。
    
2.  讓我們找出同一天有 500 筆外送和內送傳輸的帳戶。
    
    此項目的 PGQL 查詢為：
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    在上方的第一個 **MATCH** 子句中， **(a)** 代表來源頂點， **(a1)** 代表目的地，而 **\[t1:transfer\]** 則是連線它們的邊緣。**：transfer** 指定 **t1** 邊緣有 **TRANSFER** 標籤。兩個樣式之間的逗號 (，) 為 AND 條件。
    
3.  將查詢複製並貼到 GraphViz 應用程式的「PGQL 圖表查詢」文字輸入方塊中。按一下「執行 (Run)」。
    
    結果應如下所示。在反白設定中，以 **xxx-yyy-** 開頭的帳戶會以紅色 (= 銀行的帳戶) 顯示，而 **xxx-zzz-** 則會以橘色 (= 來自其他銀行的帳戶)。
    
    ![同日轉帳](images/same-day-transfers.jpg)
    
4.  下一個查詢會尋找相同兩個帳戶 (例如，從 a1->a2 並返回 a2->a1) 的傳輸模式。
    
    此項目的 PGQL 查詢為：
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  將查詢複製並貼到 GraphViz 應用程式的「PGQL 圖表查詢」文字輸入方塊中。按一下「執行 (Run)」。
    
    結果應如下所示。
    
    ![週期 -2 躍點](images/cycle-2-hops.jpg)
    
6.  讓我們再為該查詢新增一個帳戶，以尋找 3 個帳戶之間的循環轉移模式。
    
    PGQL 查詢會變成：
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  將查詢複製並貼到 GraphViz 應用程式的「PGQL 圖表查詢」文字輸入方塊中。按一下「執行 (Run)」。
    
    結果應如下所示。
    
    ![循環 3 躍點](images/cycle-3-hops.jpg)
    

## 確認

*   **作者** - Jayant Sharma
*   **貢獻者** - Arabella Yao、Jenny Tsai
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月