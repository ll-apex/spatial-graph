# 佈建 Autonomous Database 共用免費層執行處理

## 簡介

這個實驗室會逐步引導您瞭解在 Oracle Cloud 上使用 Oracle Autonomous Database (Autonomous Data Warehouse \[ADW\] 和 Autonomous Transaction Processing \[ATP\]) 的入門步驟。您將使用雲端主控台佈建新的 ATP 執行處理。

_Note1：雖然此實驗室使用 ATP，但步驟在建立和連線至 ADW 資料庫時完全相同。_

_Note2：若要建立永遠免費自治式資料庫，您必須位於提供永遠免費資源的區域。(並非所有區域都具備永遠免費資源)_

估計時間：5 分鐘

觀看示範如何在 Autonomous Transaction Processing 中佈建自治式資料庫 (在 Autonomous Data Warehouse 中佈建自治式資料庫的相同步驟)：

[中文版 \_ English](youtube:Q6hxMaAPghI)

### 目標

*   瞭解如何佈建新的免費層 Autonomous Transaction Processing 執行處理

### 先決條件

*   [Oracle Cloud 帳戶](https://www.oracle.com/cloud/free/)。您可以使用自己的雲端帳戶、透過試用取得的雲端帳戶、免費層帳戶，或是 Oracle 講師將詳細資訊提供給您的訓練帳戶。

## 作業 1：從 「服務」功能表中選擇可承諾量

1.  登入 Oracle Cloud。
    
2.  登入之後，系統會將您帶往雲端服務儀表板，供您查看所有可用的服務。按一下左上方的導覽功能表，以顯示最上層導覽選項。
    
    **注意：**您也可以在儀表板的**快速動作**區段中，直接存取您的 Autonomous Data Warehouse 或 Autonomous Transaction Processing 服務。
    
    ![OCI 主控台](images/oci-console.png)
    
3.  以下步驟適用於 Autonomous Data Warehouse 或 Autonomous Transaction Processing。這個實驗室示範 Autonomous Transaction Processing (ATP) 資料庫的佈建。按一下左上方的**導覽功能表**，瀏覽至 **Oracle Database** ，然後選取 **Autonomous Transaction Processing** 。
    
    ![選取可承諾量](https://oracle-livelabs.github.io/common/images/console/database-atp.png)
    
4.  確定您的「工作負載類型」為**交易處理**或**全部**，以查看您的 Autonomous Transaction Processing 執行處理。您可以使用**清單範圍**下拉式功能表選取區間。選取您要在其中建立新 ATP 執行處理的**根區間**或**您選擇的另一個區間**。若要建立新的區間或深入瞭解這些區間，請按一下[此處](https://docs.cloud.oracle.com/iaas/Content/Identity/Tasks/managingcompartments.htm#three)。
    
    _**注意** - 請避免使用 ManagedCompartmentforPaaS 區間，因為這是 Oracle Platform Services 所使用的 Oracle 預設值。_
    

## 作業 2：建立 ADB 執行處理

1.  按一下**建立 Autonomous Database** 以開始執行處理建立處理作業。
    
    ![建立 ADB](images/create-adb.png)
    
2.  這會帶出**建立 Autonomous Database** 畫面，您可以在其中指定執行處理的組態。
    
3.  提供 Autonomous Database 的基本資訊：
    
    *   **選擇區間** - 從下拉式清單中選取資料庫的區間。
    *   **顯示名稱** - 輸入資料庫的可重複名稱以供顯示。針對這個實驗室，請使用 **ATP 圖表**。
    *   **資料庫名稱** - 只能使用字母和數字，並且以字母為開頭。長度上限為 14 個字元。(初始不支援底線。) 若為此實驗室，請使用 **ATPGRAPH** 。
4.  選擇工作負載類型。從選項中選取資料庫的工作負載類型：
    
    *   **交易處理** - 在此實驗室中，選擇**交易處理**作為工作負載類型。
    *   **資料倉儲** - 或者，您可以選擇「資料倉儲」作為工作負載類型。
    
    ![工作負載類型](images/workload-type.png)
    
5.  選擇部署類型。從選項中選取資料庫的部署類型：
    
    *   **共用基礎架構** - 針對此實驗室，請選擇**共用基礎架構**作為部署類型。
    *   **專用基礎架構** - 或者，您也可以選擇專用基礎架構作為工作負載類型。
    
    ![部署類型](images/deployment-type.png)
    
6.  設定資料庫，選取**永遠免費**選項：
    
    *   **永遠免費** - 針對此實驗室，您可以選取此選項來建立永遠免費自治式資料庫，或者不選取此選項並使用付費訂閱建立資料庫。隨時可用的資料庫隨附 1 個 CPU 和 20 GB 儲存空間。若選取永遠免費，將會影響此實驗室。
    *   **選擇資料庫版本** - 從可用的版本 (`19c` 或 `21c`) 選取資料庫版本。
    *   **OCPU 數目** - CPU 數目。
    *   **自動調整規模** - 在此實驗室中，請維持**停用**自動調整規模。
    *   **儲存 (TB)** \- 儲存容量 (以 TB 為單位)。
    *   **新資料庫預覽** - 如果有核取方塊可用於預覽新資料庫版本，請**不要**選取它。
    
    ![選取 CPU 和儲存體](images/atp-choose-cpu-storage.png)
    
7.  建立管理員證明資料：
    
    *   **密碼和確認密碼** - 指定服務執行處理之 ADMIN 使用者的密碼。密碼必須符合下列需求：
    *   密碼長度必須介於 12 到 30 個字元之間，且必須至少包含一個大寫字母、一個小寫字母及一個數字字元。
    *   密碼不能包含使用者名稱。
    *   密碼不可包含雙引號 (") 字元。
    *   密碼必須與最後使用的 4 個密碼不同。
    *   密碼不得與 24 小時前設定的密碼相同。
    *   重新輸入密碼加以確認。記下此密碼。
    
    ![密碼](images/password.png)
    
8.  選擇網路存取：
    
    *   在這個實驗室中，接受預設值「保護無處不在的存取」。
    *   如果您想要一個專用端點，只能允許來自您指定之 VCN 的流量 - 從所有公用 IP 或 VCN 存取資料庫的位置被封鎖，請在選擇網路存取區域中選取「虛擬雲端網路」。
    *   您可以透過設定網路存取控制清單 (ACL)，控制及限制對 Autonomous Database 的存取。您可以從 4 種 IP 表示法類型中選取：IP 位址、CIDR 區塊、虛擬雲端網路、虛擬雲端網路 OCID。
    
    ![網路存取](images/network-access.png)
    
9.  選擇授權類型。對於此實驗室，請選擇**包含授權**。兩種授權類型為：
    
    *   **自備授權 (BYOL)** \- 當您的組織有現有的資料庫授權時，請選取此類型。
    *   **包括授權** - 若要訂閱新資料庫軟體授權和資料庫雲服務，請選取此類型。
10.  按一下**建立 Autonomous Database** 。
    
    ![授權](images/license.png)
    
11.  您的執行處理將開始佈建。狀態將在幾分鐘內從「佈建」變成「可用」。此時，您的 Autonomous Transaction Processing 資料庫已可供使用！在此查看您執行處理的詳細資訊，包括其名稱、資料庫版本、OCPU 計數以及儲存大小。![狀態啟動設定](images/atp-graph-provisioning.png) ![可用狀態](images/atp-graph-available.png)
    

您現在可以繼續下一個實驗室。

## 想要進一步瞭解嗎？

按一下[此處](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)以取得使用 Autonomous Data Warehouse 典型工作流程的文件。

## 確認

*   **作者** - 尼拉 Panchal
*   **因應雲端需求** - Richard Green
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月
*   **作者** - 尼拉 Panchal
*   **因應雲端需求** - Richard Green
*   **上次更新者 / 日期** - Ryota Yamanaka，2023 年 3 月