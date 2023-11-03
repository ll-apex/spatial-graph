# 安裝範例對應應用程式

## 簡介

Oracle APEX 可存取強調特定功能領域的範例應用程式組合。其中「範例對應」應用程式顯示 Oracle APEX 中的對應功能。我們提供了各式各樣的範例來作為功能範例和進一步自訂的起點。在此實驗室中，您將安裝並設定「範例對應」應用程式。

預估實驗室時間：15 分鐘

### 目標

*   安裝「範例對應」應用程式
*   載入支援資料

### 先決條件

*   必須使用 Oracle APEX 21.1+. 本研討會中的螢幕擷取畫面是使用 APEX 21.2 所拍攝。由於我們通常建議使用[最新的 APEX 版本](https://www.oracle.com/tools/downloads/apex-downloads/)，因此使用者介面會偶爾產生些微的差異。

## 作業 1：安裝應用程式

1.  首先，按一下**應用程式產生器**。
    
    ![APEX Application Builder](images/install-sample-maps-00.png)
    
2.  按一下**安裝起始應用程式或範例應用程式**。
    
    ![選取起始應用程式或範例應用程式](images/install-sample-maps-01.png)
    
    **注意：**如果工作區有現有的應用程式，請按一下**建立**，然後按一下**應用程式**。
    
3.  按一下**範例**，即可開啟包含可用範例應用程式清單的新瀏覽器頁籤。
    
    ![選取樣本](images/install-sample-maps-02.png)
    
4.  向下捲動至**範例對應**，然後按一下**下載應用程式**。
    
    ![影像替代文字](images/install-sample-maps-03.png)
    
    系統會提示您將應用程式組合儲存至本機資料夾。
    
    **注意：**如果您被重新導向至 github，請瀏覽至 APEX 版本的資料夾並下載 **sample-maps.zip** 。
    
5.  返回您的 App 產生器瀏覽器頁籤。然後按一下**匯入**。
    
    ![選取匯入](images/install-sample-maps-04.png)
    
6.  拖放或瀏覽至之前下載的「範例對應」應用程式壓縮檔案。將「檔案類型」選取為「資料庫應用程式」，然後按一下**下一步**。
    
    ![選取範例對應應用程式壓縮](images/install-sample-maps-05.png)
    
7.  檔案匯入已確認。再按一下**下一步 (Next)** 。
    
    ![按一下「下一步」](images/install-sample-maps-06.png)
    
8.  保留預設功能表選項，然後按一下**安裝應用程式**。
    
    ![按一下「安裝應用程式」](images/install-sample-maps-07.png)
    
    這將會帶您前往「安裝應用程式」精靈。
    
9.  離開預設功能表選項，然後按**下一步**。
    
    ![按一下「下一步」](images/install-sample-maps-08.png)
    
10.  按一下**下一步**以驗證系統相容性。
    

![按一下「下一步」](images/install-sample-maps-09.png)

11.  已確認相容性，按一下**安裝**即可起始支援資料庫物件和 APEX 應用程式的安裝。

![按一下「安裝」](images/install-sample-maps-10.png)

12.  安裝完成後，請按一下**執行應用程式**。

![按一下「執行應用程式」](images/install-sample-maps-11.png)

13.  使用您的 APEX 工作區使用者名稱和密碼登入「範例對應」應用程式。

![登入](images/install-sample-maps-12.png)

## 作業 2：載入資料

1.  您現在位於「範例對應」應用程式中，提供 APEX 中多個地圖和空間作業範例。初次啟動時，會顯示有關資料載入的警告訊息。按一下該訊息內的**資料載入**連結。您將瀏覽至完成載入示範資料的頁面。
    
    ![按一下資料載入](images/install-sample-maps-13.png)
    
2.  「資料載入」頁面會顯示「範例對應」應用程式所使用之「狀態」和「機場」資料集的載入狀態，以及此研討會的其他部分。安裝「範例對應」應用程式時，這些資料集僅會部分載入。若要完成範例資料載入，您可以直接從 github 中儲存的檔案載入，或是先下載檔案並從本機系統載入。如果您在需要代理以存取 github 的網路中執行 APEX，則應使用後面的選項。
    
    如果您的 APEX 執行處理不需要代理主機存取 github (例如 apex.oracle.com 或 APEX wth Oracle Autonomous Database)，請按一下按鈕來載入**直接從 GitHub** ，然後按一下右上方的**載入資料集**。
    
    ![從 Github 直接點擊](images/install-sample-maps-14.png)
    
    如果您的 APEX 執行處理需要代理主機存取 github (例如，執行於您公司防火牆後方的 APEX)，或者有其他問題直接從 github 載入，請按一下**上傳檔案**按鈕來提供替代指示。
    
3.  當資料載入完成時，您會在右上方看到通知，且警告訊息已消失。範例對應應用程式已可供使用。
    
    ![資料載入確認](images/install-sample-maps-15.png)
    

## 任務 3：探索範例對應應用程式

1.  按一下任何方磚可導覽至應用程式中的相關頁面。例如，按一下**對應與報表**。
    
    ![瀏覽至「對應與報表」頁面](images/install-sample-maps-16.png)
    
2.  在此頁面中，按一下地圖中項目之正確中心報表中的項目，並開啟資訊視窗。按一下左上角的圖示可開啟導覽面板，以存取應用程式中的其他頁面。
    
    ![與地圖互動](images/install-sample-maps-17.png)
    
3.  按一下導覽面板中的項目，以存取應用程式中的其他頁面。
    
    ![導覽面板顯示其他頁面](images/install-sample-maps-18.png)
    
4.  若要關閉導覽面板，請按一下左上角的圖示。您也可以按一下左上方的**範例對應**，瀏覽至應用程式首頁。
    
    ![關閉導覽面板](images/install-sample-maps-19.png)
    

## 作業 4：探索示範資料

1.  返回 APEX，依序按一下 **SQL 工作室**和**物件瀏覽器**。
    
    ![SQL 工作室 - 物件瀏覽器](images/install-sample-maps-20.png)
    
2.  觀察先前執行之資料載入步驟所建立的表格。按一下 **EBA\_SAMPLE\_MAP\_AIRPORTS** 。請注意，資料欄包含名稱為 GEOMETRY 且類型為 SDO\_GEOMETRY (Oracle 原生空間資料類型) 的資料欄。
    
    ![具有原生幾何資料欄的表格](images/install-sample-maps-21.png)
    
3.  按一下**資料**頁籤以檢視表格內容。
    
    ![表格內容](images/install-sample-maps-22.png)
    
    然後捲動到右側以查看幾何欄。由於機場是以點數方式儲存，APEX 會顯示點幾何值的字串表示。點數一律以單一座標為基礎，因此 APEX 會以此方式顯示值。
    
    ![點幾何](images/install-sample-maps-23.png)
    
4.  按一下 **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES** 。再者，請注意，欄包含名為 GEOMETRY 的欄，其類型為 SDO\_GEOMETRY (Oracle 的原生空間資料類型)。
    
    ![具有原生幾何資料欄的表格](images/install-sample-maps-24.png)
    
5.  按一下**資料**頁籤以檢視表格內容。由於此表格儲存狀態，因此幾何圖形是多邊形。APEX 不會顯示這些值的字串表示，因為它們可能包含極長的一組座標。
    
    ![Polygon 幾何](images/install-sample-maps-25.png)
    
6.  注意含有 **MDRT\_....$** 等名稱的表格。資料庫會在背景自動建立及管理這些表格，以支援其他表格上的空間索引。您絕對不要手動建立、更新或刪除這些表格。它們僅支援空間分析作業，可以忽略。
    
    ![空間索引使用者自建物件](images/install-sample-maps-26.png)
    
7.  最後，您可以使用此資料執行基本空間查詢。按一下 **SQL 工作室**，然後按一下 **SQL 命令**。
    
    ![SQL 工作室 - SQL 命令](images/install-sample-maps-27.png)
    
8.  下列查詢傳回超過德州 1000 公里以內的 1000 英畝土地覆蓋範圍的機場數目。請注意，使用原生空間運算子 **sdo\_within\_distance** 。將查詢複製並貼到「SQL 命令 (SQL Commands)」視窗，然後按一下右上方的**執行 (Run)** 。
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![空間查詢](images/install-sample-maps-28.png)
    
9.  在 sdo\_within\_distance 運算子中，將距離更新為 300 公里並重新執行。觀察依據較大搜尋區域的結果變更。
    
    ![空間查詢](images/install-sample-maps-29.png)
    

在稍後的實驗室中，您將設定顯示此查詢結果的地圖，其中狀態與距離是由頁面中的功能表所控制。

您現在已經安裝並探索「範例對應」應用程式和資料。接下來，您要開始建立自己的申請與對應。

這包括實驗室。您現在可以繼續下一個實驗室。

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **貢獻者** - Carsten Czarski，APEX 開發，Oracle
*   **上次更新者 / 日期** - 資料庫產品管理 David Lapp - 2023 年 3 月