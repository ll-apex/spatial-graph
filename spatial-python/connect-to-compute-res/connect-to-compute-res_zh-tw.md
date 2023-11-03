# 連線至運算

## 簡介

若要存取您的 Python 主機運算，您需要有 SSH 金鑰組。Oracle Cloud Infrastructure (OCI) Cloud Shell 是一個可從 Oracle Cloud 主控台存取的 Web 瀏覽器終端機，提供對 Linux Shell 的存取。您將會擷取 SSH 金鑰組，並連線至 OCI Cloud Shell 中的 Python 主機。

預估實驗室時間：5 分鐘

請觀看下方影片，快速瞭解實驗室的逐步解說。[實驗室 1](videohub:1_0tvxm2q0)

### 目標

*   擷取運算 IP 位址
*   擷取 SSH 金鑰組
*   建立運算的 SSH 連線

### 先決條件

*   您必須登入 OCI 主控台

## 作業 1：擷取運算執行處理的 IP 位址

1.  從主功能表前往 \[ 運算 \] > \[ 執行處理 \]

![開啟 Cloud Shell](images/compute-01.png)

2.  在研討會指示頁面中，按一下左上方的**檢視登入資訊**，然後複製您的區間名稱。

![開啟 Cloud Shell](images/compartment.png)

1.  在 OCI 主控台中，貼上您的區間名稱，然後從下拉式清單中選取。

![開啟 Cloud Shell](images/compute-02.png)

4.  記下運算執行處理的公用 IP。您稍後將會在此和其他實驗室中使用此方法。

![開啟 Cloud Shell](images/compute-03.png)

## 作業 2：擷取 SSH 金鑰

1.  開啟雲端 Shell。
    
    ![開啟 Cloud Shell](images/compute-04.png)
    
2.  如果提示執行教學課程，請輸入 N 並輸入。
    
    ![開啟 Cloud Shell](images/compute-05.png)
    
3.  在命令行中，執行下列每一個動作以建立並瀏覽至您的 SSH 資料夾。
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`\`

![建立金鑰](images/compute-06.png)

1.  在命令行中，執行下列動作以擷取並列出包含 SSH 金鑰的 zip 檔案。
    
        <copy>
        wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/hfpJ4-8XrB5tWBDUWvgnCmGch_1WHhihBrRpHNIzj6JSq5O5hbwp2wsqRPYbg8Gm/n/c4u04/b/livelabsfiles/o/labfiles/ocw23-keys.zip
        </copy>
        
    
        <copy>
        ls
        </copy>
        
    
    ![建立金鑰](images/compute-07.png)
    
2.  在指令行執行以下指令，以解壓縮並列出 zip 檔案內容。
    
        <copy>
        unzip ocw23-keys
        </copy>
        
    
        <copy>
        ls
        </copy>
        

![建立金鑰](images/compute-08.png)

## 任務 3：連線至運算執行處理

2.  在命令行執行下列動作以連線至您的 Python 運算執行處理，其中 IP 位址是作業 1 的運算 IP 位址。
    
        <copy>
         ssh -i ~/.ssh/ocw23-rsa opc@[IP address]
        </copy>
        
    
    如果提示新增到已知主機清單，請回答 **yes** 。
    
    ![建立金鑰](images/compute-09.png)
    
3.  按一下收合圖示即可將 Cloud Shell 降到最低。
    
    ![收合 Cloud Shell](images/compute-10.png)
    
4.  請觀察「回復」按鈕以重新開啟 Cloud Shell. 您將在接下來的實驗室中重新開啟 Cloud Shell。
    
    ![回復 Cloud Shell](images/compute-11.png)
    

您現在可以**進入下一個實驗室**。

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **貢獻者** - Rahul Tasker，Denise Myrick，Ramu Gutierrez
*   **上次更新者 / 日期** - David Lapp，2023 年 8 月