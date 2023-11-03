# 在 Graph Studio 中建立 RDF 圖表

## 簡介

Oracle Autonomous Database 中的 Graph Studio 可讓使用者建立、查詢及分析圖表資料。它包括記事本、使用 PGQL 執行圖表查詢的開發人員 API、60 個以上的內建圖形演算法，以及提供包括原生圖形視覺化在內的數十種視覺化呈現。除了屬性圖之外，Graph Studio 現在還根據資源描述架構 (RDF) 和 Web Ontology Language (OWL)，擴充了語意技術支援，包括資料和待辦事項的儲存、推論和查詢功能。您現在可以將 Graph Studio 用於下列支援的 RDF 功能：

*   建立 RDF 圖形
*   在記事本段落中對 RDF 圖形執行 SPARQL 查詢
*   分析和視覺化 RDF 圖表

預估時間：5 分鐘

請觀看下方影片，快速瞭解實驗室的逐步解說。[在 Graph Studio 中建立 RDF 圖形](videohub:1_vvqhh26v)

### 目標

*   在 Graph Studio 中建立 RDF Graph
*   驗證 RDF 圖表
*   在播放畫面頁面上執行 SPARQL 查詢

### 先決條件

*   下列實驗室需要 Autonomous Database - 無伺服器。
*   且啟用圖形的使用者 (GRAPHUSER) 存在。亦即，具有正確角色和權限的資料庫使用者已經存在。

## 作業 1：在 Graph Studio 中建立 RDF 圖形

假設您已完成先前的實驗室並目前已登入，請執行下列步驟：

1.  按一下左側導覽功能表上的**圖表**以瀏覽「圖表」頁面。

![建立環境後的登陸頁面是工作功能表](./images/graph-studio-home.png)

2.  在「圖形類型」下拉式功能表中，選取 **RDF** ，然後按一下介面右上角的**建立**按鈕。

![Graph Studio 頁面圖表類型下拉式功能表會顯示 PG 和 RDF 圖形選項](./images/graph-studio-graphs.png)

3.  選取 **RDF 圖表**，然後按一下**確認**按鈕。

![選取 RDF 圖表選項的確認按鈕](./images/click-confirm-rdf.png)

4.  「建立 RDF 圖形精靈」會開啟，如下所示：

![「建立 RDF 圖形」頁面。](./images/create-rdf-graph.png)

5.  輸入 OCI 物件儲存 URI 路徑：
    
          <copy>https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt
        
6.  按一下**無證明資料 (No Credential)** 。
    
7.  按一下**下一步 (Next)** 。應該會顯示下列對話方塊，為「圖形名稱」輸入 "MOVIESTREAM"：
    

![「建立 RDF 圖表」第二頁](./images/create-rdf-graph-2.png)

8.  按一下**建立**。
    
    將啟動 RDF 圖表建立工作。由於 RDF 檔案包含 139461 筆記錄，因此程序可能需要 3 到 4 分鐘。您可以在 Graph Studio 的**工作**頁面上監督工作。
    

![Graph Studio 的「工作」頁面顯示仍在進行中的「建立 RDF 圖表 - MOVIESTREAM」工作](./images/graph-studio-jobs.png)

    When succeeded, the status will change from pending to succeeded and Logs can be viewed by clicking on the three dots on the right side of the job row and selecting **See Log**. The log for the job displays details as shown below:
    
    ```
    Tue, Mar 1, 2022 08:21:04 AM
    Finished execution of task Graph Creation - MOVIESTREAM.
    
    Tue, Mar 1, 2022 08:21:04 AM
    Graph MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:21:04 AM
    Optimizer Statistics Gathered successfully
    
    Tue, Mar 1, 2022 08:20:50 AM
    External table <graph-user>_TAB_EXTERNAL dropped successfully
    
    Tue, Mar 1, 2022 08:20:49 AM
    Data successfully bulk loaded from ORACLE_ORARDF_STGTAB
    
    Tue, Mar 1, 2022 08:20:39 AM
    Model MOVIESTREAM created successfully
    
    Tue, Mar 1, 2022 08:20:37 AM
    Network RDF_NETWORK created successfully
    
    Tue, Mar 1, 2022 08:20:24 AM
    Data loaded into the staging table ORACLE_ORARDF_STGTAB from <graph-user>_TAB_EXTERNAL
    
    Tue, Mar 1, 2022 08:20:19 AM
    External table <graph-user>_TAB_EXTERNAL created successfully
    
    Tue, Mar 1, 2022 08:20:19 AM
    Using the Credential MOVIES_CREDENTIALS
    
    Tue, Mar 1, 2022 08:20:19 AM
    Started execution of task Graph Creation - MOVIESTREAM.
    ```
    

## 作業 2：驗證 RDF 圖表

您可以在 Graph Studio 的**圖表**頁面上瀏覽及驗證新建立的 RDF 圖表，如下所示：

1.  瀏覽至**圖表**頁面，並使用下拉式功能表將**圖表類型**設為 RDF。從可用的 RDF 圖表選取 MOVIESTREAM 圖表資料列、範例陳述式 (應顯示三種水平點)，使用三種水平點來調整這些陳述式的大小，並將其納入檢視表中。「RDF 圖表」的範例敘述句 (三項式或四項式) 會顯示在底部面板上，如下所示：

![RDF 圖表 'MOVIESTREAM' 的範例對帳單會顯示在三重奏中](./images/graph-sample-statements.png)

2.  選取 MOVIESTREAM 圖表後，捲動至頁面底端，並驗證您已擷取 500 列 RDF 三人組。

![MOVIESTREAM RDF 圖表的範例敘述句](./images/sample-statements.png)

## 任務 3：在播放畫面頁面上執行 SPARQL 查詢

您可以從**查詢播放畫面**頁面，在 RDF 圖表上執行 SPARQL 查詢。

1.  在**圖表**頁面上，從「圖形類型」下拉式功能表選取 **RDF** ，然後按一下**查詢**按鈕以瀏覽至「查詢播放」頁面。

![已選取 RDF 圖形類型的圖形頁面，並反白顯示查詢按鈕](./images/graph-type.png)

2.  如果在圖形工作室中有多個圖形，您必須選擇要查詢的圖形。在「圖形名稱」功能表中，從下拉式功能表中選取 MOVIESTREAM。

![查詢播放畫面會顯示從下拉式功能表選取的圖表名稱 'MOVIESTREAM'](./images/query-playground.png)

3.  針對 RDF 圖表執行下列查詢。
    
        <copy>PREFIX rdf: &lthttp://www.w3.org/1999/02/22-rdf-syntax-ns#&gt
        PREFIX rdfs: &lthttp://www.w3.org/2000/01/rdf-schema#&gt
        PREFIX xsd: &lthttp://www.w3.org/2001/XMLSchema#&gt
        PREFIX ms: &lthttp://www.example.com/moviestream/&gt
        
        SELECT DISTINCT ?gname
        WHERE {
          ?movie ms:actor/ms:name "Keanu Reeves" ;
          ms:genre/ms:genreName ?gname .
        }
        ORDER BY ASC(?gname)<copy>
        
    
    順利執行查詢時，將顯示如下的查詢輸出：
    

![查詢播放台會在 MOVIESTREAM RDF 圖表上成功執行查詢，並顯示查詢結果](./images/query-playground-script.png)

結束此實驗室。**您現在可以開始進行下一個實驗室。**

## 確認

*   **作者** - 馬利亞德文、Ethan Shmargad、Matthew McDaniel 解決方案工程師、Ramu Murakami Gutierrez 產品經理
*   **技術貢獻者** - Melliyal Annamalai 傑出產品經理 Joao Paiva 技術人員諮詢成員 Lavanya Jayapalan 主要使用者協助開發人員
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，產品經理，2023 年 8 月