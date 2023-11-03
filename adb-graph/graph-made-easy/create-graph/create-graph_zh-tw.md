# 建立圖表

## 簡介

在此實驗室中，您將使用 Graph Studio 和 CREATE PROPERTY GRAPH 敘述句從 `bank_accounts` 與 `bank_txns` 表格建立圖表。

預估時間：15 分鐘。

請觀看下方影片，快速瞭解實驗室的逐步解說。[在 Graph Studio 中建立特性圖表](videohub:1_cz3cwg3h)

### 目標

瞭解如何

*   使用 Graph Studio 和 PGQL DDL (亦即 CREATE PROPERTY GRAPH 敘述句) 從現有表格或視觀表建立圖表模型和建立。

### 先決條件

*   下列實驗室需要 Autonomous Database - 共用基礎架構帳戶。
*   而且，啟用圖形的使用者 (`GRAPHUSER`) 存在。亦即，具有正確角色和權限的資料庫使用者已經存在。

## 作業 1：從對應的表格建立科目與交易的圖表

1.  按一下**圖表**圖示以瀏覽建立您的圖表。  
    然後按一下**建立 (Create)** 。  
    ![顯示建立按鈕建模工具的位置](images/graph-create-button.png " ")
    
2.  然後選取 `BANK_ACCOUNTS` 與 `BANK_TXNS` 表格。  
    ![顯示如何選取 BANK_ACCOUNTS 和 BANK_TXNS](./images/select-tables.png " ")
    
3.  將它們移到右側，亦即，按一下往返控制項上的第一個圖示。
    

![顯示選取的表格](./images/selected-tables.png " ")

4.  按一下**下一步**以取得建議的模型。我們將編輯並更新此模型，以新增邊緣和頂點標籤。
    
    建議的模型具有 `BANK_ACCOUNTS` 作為頂點表格，因為 `BANK_TXNS` 上已指定外來索引鍵限制條件來參考它。
    
    而 `BANK_TXNS` 是建議的邊緣表格。
    

![顯示頂點與邊緣表格](./images/create-graph-suggested-model.png " ")

5.  現在，讓我們變更預設的 Vertex 和 Edge 標籤。
    
    按一下 `BANK_ACCOUNTS` 頂點表格。將「頂點標籤」變更為 **ACCOUNTS** 。然後在確認標籤的輸入方塊外按一下，並儲存更新。
    
    ![將頂點的標籤名稱變更為帳戶](images/edit-accounts-vertex-label.png " ")
    
    按一下 `BANK_TXNS` 邊緣表格，並將「邊緣標籤」從 `BANK_TXNS` 重新命名為 **TRANSFERS** 。  
    然後在確認標籤的輸入方塊外按一下，並儲存更新。
    
    ![已變更要傳輸的邊緣標籤名稱](images/edit-edge-label.png " ")
    
    這是**重要**，因為查詢圖表時，我們將在此研討會的下一個實驗室中使用這些邊緣標籤。
    
6.  由於這些是導向的邊緣，因此最佳做法是驗證方向是否正確。  
    在此執行處理中，我們希望**確認**方向是從 `from_acct_id` 到 `to_acct_id`。
    
    > **注意：**左側的 `Source Vertex` 和 `Destination Vertex` 資訊。
    
    ![顯示頂點的方向有多誤](images/wrong-edge-direction.png " ")
    
    **請注意**方向錯誤。來源鍵值是 `to_acct_id`，而不是我們想要的內容，也就是 `from_acct_id`。
    
    按一下右側的交換邊圖示以交換來源與目標頂點，進而反轉邊緣方向。
    
    > **注意：**`Source Vertex` 現在是正確的，亦即 `FROM_ACCT_ID`。
    
    ![顯示方向的正確性](images/reverse-edge-result.png " ")
    
7.  按一下**來源**頁籤以驗證邊緣方向，因此產生的 CREATE PROPERTY GRAPH 敘述句正確。
    
    ![驗證來源中的邊緣方向是否正確](images/generated-cpg-statement.png " ")
    

8.  按一下**下一步**，然後按一下**建立圖表**以移至流程的下一個步驟。
    
    輸入 `bank_graph` 作為圖表名稱。  
    圖形名稱主要用於下一個實驗室。  
    請勿輸入其他名稱，因為下個實驗室中的查詢和程式碼片段將會失敗。
    
    輸入模型名稱 (例如 `bank_graph_model`) 和其他選擇性資訊，然後按一下「建立」。 ![顯示您為圖形指派名稱的建立圖形視窗](./images/create-graph-dialog.png " ")
    
9.  Graph Studio 模型建立者現在會儲存描述資料並啟動工作以建立圖表。  
    「工作 (Job)」頁面會顯示此工作的狀態。
    
    ![顯示工作狀態為成功的工作頁籤](./images/jobs-create-graph.png " ")
    
    接著，您便可以在將圖表載入記憶體後，以互動方式查詢及視覺化記事本中的圖表。
    

結束此實驗室。**您現在可以開始進行下一個實驗室。**

## 確認

*   **作者** - 產品管理 Jayant Sharma
*   **貢獻者** - Jayant Sharma，產品管理
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，產品管理，2022 年 6 月