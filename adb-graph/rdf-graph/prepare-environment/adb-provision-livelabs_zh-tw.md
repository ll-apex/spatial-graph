/\* 刪除此檔案於下次發行 - 請先使用 ADB-PROVISION-CONDITIONAL.MD 檔案安裝，並且指定您所需的版本：{ "title"："Lab 1: Provisioning an ADB Instance"，"description"："Provisioning an Autonomous Database Instance"，"type"："livelabs"，"filename"："https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }，\*/

# 佈建 Autonomous Database (ADW 和 ATP)

## 簡介

這個實驗室會逐步引導您瞭解在 Oracle Cloud 上使用 Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] 和 Autonomous Transaction Processing \[ATP\]) 的入門步驟。在此實驗室中，您可以佈建新的 ADW 執行處理。

> **備註：**此實驗室使用 ADW 時，建立可承諾量資料庫的步驟是相同的。

估計時間：5 分鐘

### 目標

*   瞭解如何佈建新的 Autonomous Database

## 作業 1：從服務功能表選擇 ADW 或 ATP

1.  登入 Oracle Cloud。
    
2.  登入之後，系統會將您帶往雲端服務儀表板，供您查看所有可用的服務。按一下左上方的導覽功能表，以顯示最上層導覽選項。
    
    > **注意：**您也可以在儀表板的**快速動作**區段中，直接存取您的 Autonomous Data Warehouse 或 Autonomous Transaction Processing 服務。
    
    ![Oracle 首頁。](./images/Picture100-36.png " ")
    
3.  以下步驟適用於 Autonomous Data Warehouse 或 Autonomous Transaction Processing。這個實驗室會顯示 Autonomous Data Warehouse 資料庫的佈建，請按一下 **Autonomous Data Warehouse** 。
    
    ![按一下 Autonomous Data Warehouse。](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  確定您的工作負載類型為**資料倉儲**或**全部**，以查看您的 Autonomous Data Warehouse 執行處理。使用**清單範圍**下拉式功能表選取區間。輸入使用者名稱的第一個部分，例如「搜尋區間」欄位中的 `LL185`，以快速找到您的區間。
    
    ![檢查左側的工作負載類型。](images/livelabs-compartment.png " ")
    
5.  此主控台顯示尚無資料庫。如果資料庫清單很長，您可以依資料庫的**狀態** (可用、已停止、已終止等等) 篩選清單。您也可以依**工作負載類型**排序。此處選取了**資料倉儲**工作負載類型。
    
    ![「自治式資料庫」主控台。](./images/Compartment.png " ")
    

## 作業 2：建立 ADB 執行處理

1.  按一下**建立 Autonomous Database** 以開始執行處理建立處理作業。
    
    ![按一下「建立 Autonomous Database」。](./images/Picture100-23.png " ")
    
2.  這會帶出**建立 Autonomous Database** 畫面，您可以在其中指定執行處理的組態。
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  提供自治式資料庫的基本資訊：
    
    *   **選擇區間** - 離開預設區間。
    *   **顯示名稱** - 輸入資料庫的可重複名稱以供顯示。在這個實驗室中，請使用 **ADW Finance Mart** 。
    *   **資料庫名稱** - 只能使用字母與數字，並且以字母為開頭。長度上限為 14 個字元。(初始不支援底線。) 若為此實驗室，請使用 **ADWFINANCE** 並**附加您的使用者 ID** 。例如，如果您的使用者 ID 為 **LL-185** ，則輸入 **ADWFINANCE185**
    
    ![輸入必要的詳細資料。](./images/Picture100-26-livelabs.png " ")
    
4.  選擇工作負載類型。從選項中選取資料庫的工作負載類型：
    
    *   **資料倉儲** - 針對此實驗室，請選擇**資料倉儲**作為工作負載類型。
    *   **交易處理** - 或者，您也可以選擇「交易處理」作為工作負載類型。
    
    ![選擇工作負載類型。](./images/Picture100-26b.png " ")
    
5.  選擇部署類型。從選項中選取資料庫的部署類型：
    
    *   **共用基礎架構** - 針對此實驗室，請選擇**共用基礎架構**作為部署類型。
    *   **專屬基礎架構** - 或者，您也可以選擇專用基礎架構作為部署類型。
    
    ![選擇部署類型。](./images/Picture100-26_deployment_type.png " ")
    
6.  設定資料庫：
    
    *   **永遠免費** - 如果您的雲端帳戶是永遠免費帳戶，可以選取此選項以建立永遠免費自治式資料庫。隨時可用的資料庫隨附 1 個 CPU 和 20 GB 儲存空間。針對此實驗室，建議您不要勾選「永遠免費」。
    *   **選擇資料庫版本** - 從可用的版本選取資料庫版本。
    *   **OCPU 數目** - 您服務的 CPU 數目。在這個實驗室中，指定 **1 CPU** 。如果您選擇永遠免費資料庫，它就有 1 個 CPU。
    *   **儲存 (TB)** \- 選取您的儲存容量 (以 TB 為單位)。請為此實驗室指定 **1 TB** 的儲存體。或者，如果您選擇永遠免費資料庫，資料庫會隨附 20 GB 儲存空間。
    *   **自動調整規模** - 在這個實驗室中，保持啟用自動調整功能，讓系統可自動使用多達三倍的 CPU 和 IO 資源來滿足工作負載需求。
    *   **新資料庫預覽** - 如果核取方塊可供預覽新資料庫版本，請勿選取。
    
    > **注意：**您無法縱向擴展 / 縮減永遠免費自治式資料庫。
    
    ![選擇剩餘的參數 。](./images/Picture100-26c.png " ")
    
7.  建立管理員證明資料：
    
    *   **密碼和確認密碼** - 指定服務執行處理之 ADMIN 使用者的密碼。密碼必須符合下列需求：
    *   密碼長度必須介於 12 到 30 個字元之間，且必須至少包含一個大寫字母、一個小寫字母及一個數字字元。
    *   密碼不能包含使用者名稱。
    *   密碼不可包含雙引號 (") 字元。
    *   密碼必須與最後使用的 4 個密碼不同。
    *   密碼不得與 24 小時前設定的密碼相同。
    *   重新輸入密碼加以確認。記下此密碼。
    
    ![輸入密碼和確認密碼。](./images/Picture100-26d.png " ")
    
8.  選擇網路存取：
    
    *   在這個實驗室中，請接受「保護來自任何位置的存取安全」預設值。
    *   如果您只要允許來自您指定之 IP 位址和 VCN 的流量 - 從所有公用 IP 或 VCN 存取資料庫的位置都被封鎖，請在選擇網路存取區域中選取「僅從允許的 IP 和 VCN 存取安全」。
    *   若要限制存取 OCI VCN 內的專用端點，請在「選擇網路存取」區域中選取「僅限專用端點存取」。
    *   如果選取「需要相互 TLS (mTLS) 認證」選項，將會要求 mTLS 認證與 Autonomous Database 的連線。如果您使用 JDBC 精簡型驅動程式搭配 JDK8 或更新版本，TLS 連線即可連線至 Autonomous Database 而不使用公事包。請參閱[網路選項文件](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5)，瞭解允許 TLS 或僅需要相互 TLS (mTLS) 認證的選項。
    
    ![選擇網路存取。](./images/Picture100-26e.png " ")
    
9.  選擇授權類型。在這個實驗室中，選擇**自備授權 (BYOL)** 。兩種授權類型為：
    
    *   **自備授權 (BYOL)** \- 當您的組織有現有的資料庫授權時，請選取此類型。
    *   **包括授權** - 若要訂閱新資料庫軟體授權和資料庫雲服務，請選取此類型。
    
    ![按一下「建立 Autonomous Database」。](./images/Picture100-27-byol.png " ")
    
10.  在此實驗室中，請勿提供聯絡人電子郵件地址。「聯絡人電子郵件」欄位可讓您列出聯絡人以接收作業通知與公告，以及未計畫的維護通知。
    
    ![請勿提供聯絡人電子郵件地址。](images/contact-email-field.png)
    
11.  按一下**建立 Autonomous Database** 。
    
12.  您的執行處理將開始佈建。在幾分鐘內，狀態將從「佈建」變成「可用」。此時，您的 Autonomous Data Warehouse 資料庫已可供使用！在此查看您執行處理的詳細資訊，包括其名稱、資料庫版本、OCPU 數目以及儲存大小。
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

請_進入下一個實驗室_。

## 想要進一步瞭解嗎？

按一下[此處](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)以取得使用 Autonomous Data Warehouse 典型工作流程的文件。

## 確認

*   **作者** - Nilay Panchal、ADB 產品管理
*   **因應雲端需求** - 資料庫使用者協助主要開發者 Richard Green
*   **貢獻者** - Oracle LiveLabs QA 團隊 (Jeffrey Malcolm Jr，Intern | Arabella Yao，Product Manager Intern)
*   **上次更新者 / 日期** - Richard Green，2022 年 2 月