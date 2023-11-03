# 設定：執行堆疊

## 簡介

在此實驗室中，您將建立一個堆疊，用於執行地形命令檔以產生 Autonomous Database、建立「圖形使用者」，以及上傳將使用的資料集。

預估時間：5 分鐘。

### 目標

瞭解如何

*   執行堆疊以建立 Autonomous Database、Graph 使用者及上傳資料集
*   登入 Graph Studio

## 作業 1：建立 OCI 區間

[](include:iam-compartment-create-body.md)

## 作業 2：執行堆疊

以下說明將告訴您如何執行堆疊，自動建立包含圖形使用者和特性圖查詢所需資料集的 Autonomous Database。

1.  登入 Oracle Cloud。
    
2.  登入之後，請使用此[連結](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kMdD7Vnv0J1st_2cU-S5PYNWT4SKzOOA04XbhwltUVXnOQ7vec1JJBEGk1eOxPS/n/oradbclouducm/b/moviestream_livelab/o/MovieStream_live_lab_7_AnD.zip)來建立和執行堆疊。
    

> 注意：連結會在新頁籤或視窗中開啟。

3.  您將會前往此頁面：

![建立堆疊頁面](./images/create-stack.png)

4.  請勾選「我已檢閱並接受 Oracle 使用條款」方塊，然後選擇您的**區間**。維持預設值。按一下**下一步 (Next)** 。

![接受已勾選「Oracle 使用條款」的選項](./images/oracle-terms.png)

5.  選取**區間**即可建立 Autonomous Database，以及您目前正在建立堆疊以建立所有資源的**區域**。按一下**下一步 (Next)** 。將您帶到「複查 (Review)」頁面之後，請按一下**建立 (Create)** 。

![建立堆疊頁面](./images/configure-variables.png)

6.  系統會將您帶往「工作詳細資訊 (Job Details)」頁面，其初始狀態會顯示在橙色中。工作順利完成之後，圖示就會變成綠色。
    
    ![工作成功](./images/successful-job.png)
    

## 確認

*   **作者** - Jayant Sharma，Ramu Murakami Gutierrez，產品管理
*   **貢獻者** - Rahul Tasker，Jayant Sharma，Ramu Murakami Gutierrez，Product Management
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，產品經理，2023 年 2 月