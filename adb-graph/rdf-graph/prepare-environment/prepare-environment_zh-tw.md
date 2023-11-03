# 準備環境

## 簡介

Oracle Autonomous Transaction Processing (ATP) 是一個完全受管理的 Oracle 資料庫服務，在 Oracle Cloud Infrastructure (OCI) 上具備「自我驅動」功能。建立具有使用 Graph Studio 之權限的使用者的最佳做法。

下列實驗室指南說明如何佈建 ATP，以及建立具備 Graph Studio 權限的使用者。

預估時間：15 分鐘

### 目標

*   在 Oracle Cloud 上建立 Autonomous Database。

### 先決條件

*   Web 瀏覽器
*   請務必確定您位於正確的區域與區間中

## **任務 1：**登入 Oracle Cloud

1.  從您的瀏覽器登入 Oracle Cloud。

## **作業 2：** 供應可承諾量

依照下列步驟佈建 Autonomous Transaction Processing 資料庫 (ATP) . 或者，您也可以使用相似的 Autonomous Data Warehouse (ADW)。

1.  從 OCI 主控台右上角選取指定的區域。
    
2.  從漢堡功能表 (左上角) 選取 Oracle Database，然後選取 Autonomous Transaction Processing。
    

![此影像顯示功能表中選擇存取 Autonomous Transaction Processing 的位置](./images/atp.png)

3.  按一下「建立 Autonomous Database」。

![顯示建立自治式資料庫按鈕的影像](./images/create-adb.png)

4.  選擇您的區間。
    
5.  輸入顯示和資料庫名稱的唯一名稱 (可能是您的名稱) . 顯示名稱在主控台 UI 中用來識別您的資料庫。
    

![影像顯示輸入資料庫唯一名稱的位置](./images/unique-name.png)

6.  確定已選取「異動處理」工作負載類型。
    
7.  輸入密碼。使用者名稱一律為 ADMIN. (注意：請記住您的密碼)
    

![影像顯示宣告您密碼的位置](./images/password.png)

8.  按一下底部的建立 Autonomous Database。
    
    您的主控台將會顯示 ATP 正在佈建中。這將需要 2 或 3 分鐘的時間才能完成。
    
    您可以在「工作要求」中檢查佈建的狀態。
    

![顯示檢查已佈建資料庫狀態的位置的影像](./images/status.png)

結束此實驗室。_您現在可以開始進行下一個實驗室。_

## 確認

*   **作者** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **貢獻者** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **上次更新者 / 日期** - Nicholas Cusato，2022 年 2 月