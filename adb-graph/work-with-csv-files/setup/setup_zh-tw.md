# 設定：執行堆疊

## 簡介

在此實驗室中，您將建立一個堆疊，執行地形指令碼以產生 Autonomous Database、建立圖形使用者，並上傳將使用的資料集。

預估時間：5 分鐘。

請觀看下方影片，快速瞭解實驗室的逐步解說。[逐步解說](videohub:1_4lr4x8eb)

### 目標

瞭解如何

*   執行堆疊以建立 Autonomous Database、Graph 使用者及上傳資料集
*   登入 Graph Studio

## 作業 1：建立 OCI 區間

[](include:iam-compartment-create-body.md)

## 作業 2：執行堆疊

以下說明將告訴您如何執行堆疊，自動建立包含圖形使用者和特性圖查詢所需資料集的 Autonomous Database。

1.  登入 Oracle Cloud。
    
2.  登入之後，請使用此[連結](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oracle-quickstart/oci-arch-graph/releases/latest/download/orm-graph-stack.zip)來建立和執行堆疊。
    
    > 注意：連結會在新頁籤或視窗中開啟。
    
3.  您將會前往此頁面：
    
    ![建立堆疊頁面](./images/create-stack.png)
    
4.  勾選「我已檢閱並接受 Oracle 使用條款」方塊並選擇您的區間。維持預設值。按一下**下一步 (Next)** 。
    
    ![接受已勾選「Oracle 使用條款」的選項](./images/oracle-terms.png)
    
5.  選取**區間**以建立 Autonomous Database 和資料庫類型。按一下**下一步 (Next)** 。將您帶到「複查 (Review)」頁面之後，請按一下**建立 (Create)** 。
    
    ![設定堆疊的設定值](./images/configure-variables.png)
    
6.  系統會將您帶往「工作詳細資訊 (Job Details)」頁面，其初始狀態會顯示在橙色中。工作順利完成之後，圖示就會變成綠色。
    
    ![工作成功](./images/successful-job.png)
    
    若要查看您應用程式的相關資訊，請按一下**應用程式資訊**。儲存圖形使用者名稱和密碼，因為您將使用此圖形使用者名稱和密碼登入 Graph Studio。
    
    ![如何查看圖表使用者名稱與密碼](./images/graph-username-password.png)
    

## 工作 3：登入 Graph Studio

1.  按一下「應用程式資訊」底下的 **Open Graph Studio** 。這會開啟新頁面 。在登入畫面中輸入「應用程式資訊」底下提供的圖形使用者名稱與密碼。
    
    ![開啟應用程式資訊下的圖形工作室](./images/login-page.png " ")
    
2.  然後按一下**登入 (Sign In)** 按鈕。您應該會看到 Studio 首頁。
    
    ![此影像無法使用 ALT 文字](./images/gs-graphuser-home-page.png " ")
    
    Graph Studio 包含一組從左側功能表存取的頁面。
    
    **首頁**圖示會將您帶往首頁。  
    **圖表**頁面列出記事本中使用的現有圖表。  
    **記事本**頁面會列出現有的記事本，並可讓您建立新的記事本。  
    **範本**頁面可讓您為圖形視覺化建立範本。  
    **工作**頁面會列出背景工作的狀態，並可讓您檢視關聯的日誌 (如果有的話)。  
    

結束此實驗室。**您現在可以開始進行下一個實驗室。**

## 確認

*   **作者** - Jayant Sharma，Ramu Murakami Gutierrez，產品管理
*   **貢獻者** - Rahul Tasker，Jayant Sharma，Ramu Murakami Gutierrez，Product Management
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，產品經理，2023 年 6 月