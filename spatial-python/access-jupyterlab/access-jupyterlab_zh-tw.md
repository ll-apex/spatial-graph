# 存取 JupyterLab

## 簡介

筆記本是用於程式碼、描述性文字和視覺化的互動式文件。在此研討會中，您可以使用開源 JupyterLab，此開源環境內含許多容易操作的功能，例如檔案上傳。

預估實驗室時間：5 分鐘

### 目標

*   驗證 JupyterLab 的存取權
*   探索記事本功能
*   選取執行剩餘實作實驗室的選項

## 作業 1：擷取 JupyterLab 的 IP 位址

1.  從主功能表前往 \[ 運算 \] > \[ 執行處理 \]

![擷取 IP 位址](images/compute-01.png)

2.  在研討會指示頁面中，按一下左上方的**檢視登入資訊**，然後複製您的區間名稱。

![擷取 IP 位址](images/compartment.png)

1.  在 OCI 主控台中，貼上您的區間名稱，然後從下拉式清單中選取。

![擷取 IP 位址](images/compute-02.png)

4.  記下運算執行處理的公用 IP。已在此執行處理上設定 JupyerLab。您稍後將會在此和其他實驗室中使用此方法。

![擷取 IP 位址](images/compute-03.png)

## 作業 2：驗證 JupyterLab 的存取

1.  開啟新的瀏覽器頁標，並輸入 URL **http：//\[IP address\]：8001/lab** ，其中 \[IP address\] 是在任務 1 中擷取的位址。
    
    ![存取 JupyterLab](images/access-jupyter-01.png)
    
2.  輸入密碼 **livelabs** ，然後按一下**登入**。
    

## 工作 2：探索 Jupyter Notebooks

Jupyter Notebook 是互動式的網頁工具，可讓您建立並共用包含即時程式碼、方程式、視覺化和文字的文件。它被廣泛用於資料科學社群，以進行原型設計和資料分析。

在這項任務中，我們將逐步介紹如何使用 Jupyter Notebook。

1.  建立新筆記型電腦。
    
    當您的 Jupyter 環境載入時，您應該會看到開啟的啟動圖示頁籤。
    
    ![已開啟啟動程式頁籤](./images/launcher1.png)
    
    如果您沒有看到啟動圖示視窗，請選取視窗左上角的檔案，然後選取 \[New Launcher\] (新啟動圖示)。
    
    ![開啟新的啟動程式頁籤](./images/launcher2.png)
    
    從啟動圖示視窗中，選取 "Python 3" 以使用 Python 程式語言建立新的記事本。將會建立新的記事本，您可以在程式碼儲存格中輸入程式碼，或在減價儲存格中新增減價文字，以開始使用它。
    
    ![建立新的 Python 筆記本](./images/launcher3.png)
    
2.  新增一些減價文字。
    
    按一下代碼儲存格，然後使用儲存格類型下拉式清單來選取「減價」
    
    ![新增減價儲存格](./images/notebook1.png)
    
    在儲存格中貼上下列內容，然後按一下工具列上的播放按鈕，或按 Shift+Enter 來執行儲存格。
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![降價的結果](./images/notebook2.png)
    
3.  撰寫一些 Python 程式碼。將下列項目貼到下一個儲存格並加以執行。詞組 'Hello, World!' 應出現在儲存格下方。
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![哈囉，世界例子](./images/notebook3.png)
    
4.  若要儲存 Jupyter Notebook，請按一下工具列上的「儲存」圖示，或按 Ctrl+S (或 macOS 上的 Cmd+S)。此記事本將會與 .ipynb 副檔名一起儲存。
    

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **貢獻者** - Rahul Tasker，Denise Myrick，Ramu Gutierrez
*   **上次更新者 / 日期** - David Lapp，2023 年 8 月