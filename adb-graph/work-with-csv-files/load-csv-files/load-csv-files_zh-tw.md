# Graph Studio：從 CSV 檔案將資料載入表格中

## 簡介

在此實驗室中，您將使用 Oracle Autonomous Data Warehouse 或 Oracle Autonomous Transaction Processing 執行處理的「資料庫動作」介面，將兩個 CSV 檔案載入至對應的表格。

預估時間：10 分鐘。

觀看下方影片快速瀏覽實驗室。

[](youtube:wkKKO-RO0lA)

### 目標

瞭解如何

*   使用資料庫動作將 CSV 檔案載入 Autonomous Database

### 先決條件

*   以下實驗室需要 Oracle Autonomous Database 帳戶。
*   它假設啟用「圖形」和「Web 存取」的使用者存在。也就是說，具有正確角色和權限的資料庫使用者已經存在，而且該使用者可以登入「資料庫動作」。

## 作業 1：連線至您 Autonomous Database 執行處理的資料庫動作

1.  在 Oracle Cloud 主控台中開啟您 Autonomous Database 執行處理的服務詳細資訊頁面。
    
    ![此影像無法使用 ALT 文字](images/open-database-actions.png " ")
    
2.  按一下**資料庫動作 (Database Actions)** 即可開啟該動作。
    

## 任務 2：以啟用圖形的使用者身分登入

1.  以圖形使用者 (例如 `GRAPHUSER`) 的身分登入您的 Autonomous Database 執行處理。
    
    ![此影像無法使用 ALT 文字](./images/db-actions-graphuser-login.png " ")
    
    > **備註：**_如有必要，請執行下列動作來建立具有適當角色與權限的使用者_：
    
    *   以 **ADMIN** 使用者身分登入您 Autonomous Database 資料庫動作
    *   從導覽功能表依序選取**管理**和**資料庫使用者**
    *   按一下**建立使用者 (Create User)**
    *   開啟 **Web 存取**與**圖形**按鈕

## 作業 3：從 ObjectStore 下載範例資料集

1.  在瀏覽器中複製並貼上 zip 封存檔的 URL，亦即
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    或使用 `wget` 或 `curl` 將範例資料下載至您的電腦。  
    您可以複製並貼上的 `curl` 要求範例如下：
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  **解壓縮**歸檔至本機目錄 (例如 ~/downloads)。
    

## 作業 4：使用資料庫動作資料載入上傳

1.  按一下 **DATA LOAD** 卡。
    
    ![此影像無法使用 ALT 文字](images/db-actions-dataload-card.png " ")
    
    然後指定資料的位置。也就是說，請確定 **LOAD DATA** 和 **LOCAL FILE** 卡有核取記號。按一下**下一步 (Next)** 。
    
    ![此影像無法使用 ALT 文字](./images/db-actions-dataload-location.png)
    
2.  按一下**選取檔案 (Select Files)** 。
    
    ![此影像無法使用 ALT 文字](images/db-action-dataload-file-browser.png " ")
    
    瀏覽至正確的資料夾 (例如 ~/downloads/random-acct-data)，然後選取 `bank_accounts.csv` 和 `bank_txns.csv` 檔案。
    
    ![此影像無法使用 ALT 文字](./images/db-actions-dataload-choose-files.png " ")
    
3.  確認選取的檔案正確，然後按一下**執行**圖示。 ![此影像無法使用 ALT 文字](./images/db-actions-dataload-click-run.png " ")
    
4.  確認您要資料載入工作。
    
    ![此影像無法使用 ALT 文字](./images/db-actions-dataload-confirm-run.png " ")
    
5.  檔案載入後
    
    ![此影像無法使用 ALT 文字](./images/dbactions-dataload-files-loaded.png " ")
    
    按一下**完成**結束。
    
    ![此影像無法使用 ALT 文字](images/dbactions-click-done.png " ")
    
6.  現在開啟 **SQL** 工作表。 ![此影像無法使用 ALT 文字](./images/db-actions-choose-sql-card.png " ")
    
7.  瀏覽至正確的資料夾 (例如 ~/downloads)，然後選取 `fixup.sql` 檔案並將其拖曳至 SQL 工作表。
    
    ![此影像無法使用 ALT 文字](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    不過，如果您偏好使用 copy-n-paste，則 `fixup.sql` 的內容為：
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    它是用以：
    
    *   新增主索引鍵限制條件至 `bank_accounts` 表格
    *   新增資料欄 (`txn_id`) 至 `bank_txns` 表格
    *   設定 `txn_id` 的值並確認交易
    *   新增主索引鍵限制條件至 `bank_txns` 表格
    *   將外來索引鍵限制條件新增至 `bank_txns` 表格，指定 `from_acct_id` 參照 `bank_accounts.acct_id`
    *   將第二個外來索引鍵限制條件新增至 `bank_txns` 表格，指定 `to_acct_id` 參照 `bank_accounts.acct_id`
    *   可協助您確認已新增 `txn_id` 資料欄和限制
8.  在 SQL 工作表中執行 `fixup.sql` 命令檔。  
    ![此影像無法使用 ALT 文字](./images/db-actions-sql-execute-fixup.png " ")
    
9.  程序檔輸出應如下所示：
    
    ![此影像無法使用 ALT 文字](./images/db-actions-sql-script-output.png " ")
    
    請**繼續進行下一個實驗室**，從這些表格建立圖表。
    

## 確認

*   **作者** - 產品管理 Jayant Sharma
*   **貢獻者** - Jayant Sharma，產品管理
*   **上次更新者 / 日期** - Jayant Sharma，產品管理，2022 年 2 月