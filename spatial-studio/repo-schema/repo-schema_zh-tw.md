# Spatial Studio 儲存區域的資料庫使用者

## 簡介

此實驗室會逐步引導您建立用於 Spatial Studio 之描述資料儲存區域的資料庫綱要。這是將儲存您在 Spatial Studio 中所做工作的綱要，例如資料集、分析及專案的定義。

Spatial Studio 儲存區域的資料庫綱要在技術上可以具有任何名稱。為了與其他 Spatial Studio 研討會一致，我們將使用者名稱命名為 **studio\_repo** 。請注意，這是資料庫使用者名稱，與 Spatial Studio 應用程式使用者名稱不同，例如安裝 Spatial Studio 應用程式時建立的預設 Spatial Studio 管理員使用者名稱 (studio\_admin)。

預估實驗室時間：5 分鐘

### 目標

*   瞭解如何建立 Spatial Studio 描述資料儲存區域的綱要
*   瞭解如何下載資料庫連線的公事包

### 先決條件

*   一個 Oracle Free Tier，Always Free，Paid 或 LiveLabs Cloud 帳戶
*   存取資料庫 SQL Developer Web。

## 作業 1：建立儲存區域綱要

1.  在 SQL Developer Web 中，以 **admin** 使用者身分連線至用於 Spatial Studio 儲存區域的自治式資料庫
    
2.  建立 Spatial Studio 儲存區域的綱要。綱要可具有任何名稱，但為了與其他實驗室一致，我們使用名稱 **studio\_repo** 。[這裡](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F)是 Oracle Autonomous Database 的密碼需求。請記下您選取的密碼，我們將在接下來的步驟中使用。
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## 作業 2：指派表格空間配額

1.  將預設表格空間指派給 Spatial Studio 儲存區域綱要。使用 Autonomous Database 時，您可以使用表格空間名稱**資料**
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  將表格空間配額指派給 Spatial Studio 儲存區域綱要。Spatial Studio 的描述資料佔用的儲存空間非常少。因此配額主要容納儲存在儲存區域綱要中的業務資料。在這個實驗室中，配額值 **250M** 正常。如果您將實驗其他資料集，也可以將值設定為 **unlimited** 。
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## 任務 3：授予權限

1.  將下列權限授予 Spatial Studio 儲存區域綱要使用者
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

studio\_repo 綱要現在已經可以當作您的 Spatial Studio 儲存區域使用。

## 作業 4：下載公事包

Spatial Studio 必須要有公事包，才能連線至我們建立的 Autonomous Database 儲存區域綱要。我們將在下一個實驗室中使用 Wallet。

1.  瀏覽至您的 Autonomous Database 並選取「檢視詳細資訊」
    
    ![影像替代文字](images/repo-schema-1.png "影像標題")
    
2.  選取「資料庫連線」頁籤
    
    ![影像替代文字](images/repo-schema-2.png "影像標題")
    
3.  按一下下載公事包 .。 ![影像替代文字](images/repo-schema-3.png "影像標題")
    
    系統會提示您輸入 Wallet 檔案的密碼。公事包是單一壓縮檔。
    
4.  將 Wallet 檔案儲存至方便的位置。下一個實驗室中將會包含這個檔案。
    

您現在可以[進入下一個實驗室](#next)。

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - 資料庫產品管理 David Lapp - 2023 年 3 月