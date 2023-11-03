# 合併空間分析

## 簡介

在此實驗室中，您將結合空間分析，從先前的實驗室強化您的地圖。您將設定搜尋位於所選狀態之使用者定義距離內的機場。

預估實驗室時間：30 分鐘

### 目標

*   瞭解基本空間分析作業
*   瞭解空間分析與 APEX 對應區域的整合

### 先決條件

*   實驗室 3：從頭建立地圖

## 作業 1：新增篩選條件的區域

1.  按一下左側樹狀結構頂端的**第 3 頁：機場與州地圖**。然後在右側的「頁面」特性面板中，於「外觀」下將「頁面範本」變更為**左側資料欄**。
    
    ![更新頁面樣板](images/add-spatial-analysis-01a.png)
    
    接著應該會在版面配置中看到**清除資料欄**。
    
    ![更新頁面樣板](images/add-spatial-analysis-01b.png)
    
2.  將「靜態內容」區域拖曳至左欄。
    
    ![新增靜態內容區域](images/add-spatial-analysis-01c.png)
    
3.  重新命名為**我的篩選區域**或您選擇的名稱。
    
    ![重新命名區域](images/add-spatial-analysis-02.png)
    

## 作業 2：新增選取狀態的項目

1.  拖曳篩選區域的「選取清單」項目，然後將名稱更新為 **P3\_STATE** 。
    
    ![新增選取清單項目](images/add-spatial-analysis-03.png)
    
2.  在右側的「頁面項目」屬性中，向下捲動至「值清單」的區段。使用交換器啟用**需要值**，將「類型」設為 **SQL 查詢**並輸入下列查詢：
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT 查詢](images/add-spatial-analysis-04.png)
    
3.  在右側的「頁面項目」屬性中，向下捲動至「預設」區段。將「類型」設為**靜態**，並將值設為**德州**或您選擇的另一個狀態 (單引號)。
    
    ![設定選取清單](images/add-spatial-analysis-05.png)
    

## 作業 3：新增遠距項目的項目

1.  將「數字欄位」拖曳至您的篩選區域中。將名稱更新為 **P3\_DISTANCE** ，並將標籤更新為 **Proximity (km)** 。
    
    ![新增數字欄位項目](images/add-spatial-analysis-06.png)
    
2.  在右側的「頁面項目」特性中，向下捲動至「驗證」區段並啟用**需要值**。
    
    ![將驗證設為必要值](images/add-spatial-analysis-07.png)
    
3.  向下捲動至「預設」區段。將類型設定為 **Static** ，並將值設定為 **100** 。
    
    ![設定預設值](images/add-spatial-analysis-08.png)
    
    您現在有可依相鄰狀態篩選機場的輸入。接下來，您將使用「動態動作」套用篩選。
    

## 作業 4：使用動態動作套用篩選

您下一步將建立使用者變更狀態和 (或) 距離值時所呼叫的動作。

1.  在您的 P3\_STATE 或 P3\_DISTANCE 項目上按一下滑鼠右鍵，然後選取**建立動態動作** (我們建立的動作會套用至這兩個項目)。
    
    ![建立動態動作](images/add-spatial-analysis-09.png)
    
2.  在右側的「動態動作」特性中，將「名稱」設為**驗證與重新整理**。在「當」區段下，將「事件」設為**變更**、「選擇類型」設為**項目**，並將項目設為逗號分隔的清單 **P3\_DISTANCE，P3\_STATE** 。請注意，項目文字方塊右邊的按鈕可讓您從清單中選取項目。若要避免提交距離負值，請在「客戶端條件」區段下將「類型」設為 **Item >= Value** ，將項目設為 **P3\_DISTANCE** ，並將「值」設為 **0** 。
    
    ![設定動態動作](images/add-spatial-analysis-10.png)
    
3.  動態動作設定了 TRUE 動作和根據已設定的條件呼叫的 FALSE 動作。在此情況下，用戶端條件 (P3\_DISTANCE >= 0) 會決定是要呼叫「TRUE 動作」(符合條件) 或「FALSE 動作」(不符合條件)。這可讓我們陷入負距離項目。
    
    當用戶端條件為 TRUE 時，動作應該提交輸入值並重新整理頁面。按一下 True 下的動作。在右側的「動作」特性中，將「動作」設為**重新整理**。在「受影響的元素」底下，將「選擇類型」設為**區域**，將「區域」設為**我的對應區域** (或您在不同時使用的名稱)。在左側的頁面樹狀結構中，True 動作會變更為「重新整理」。
    
    ![設定動態動作](images/add-spatial-analysis-11.png)
    
4.  接下來，您將設定當用戶端條件不符合時要呼叫的動作，表示輸入了負距離值。在任一項目的「動態動作」下，在 False 上按一下滑鼠右鍵，然後選取**建立 FALSE 動作**。
    
    ![設定動態動作](images/add-spatial-analysis-12.png)
    
5.  當距離為負數時呼叫的 FALSE 動作會是向使用者顯示的蹦現訊息。按一下「偽」動作。在右側的「動作」屬性中，將「動作」設為**警示**。在「設定值」下，將「標題」設為**無效距離** (這是警示橫幅)，並將「訊息」設為**距離必須 >= 0** (這將是警示主體)。左側頁面樹狀結構中的「偽」動作變更為「警示」。
    
    ![設定動態動作](images/add-spatial-analysis-13.png)
    
6.  您的「地圖區域」目前包含顯示所有狀態的「狀態」圖層。您現在可以調整此層，只顯示從 P3\_STATE 功能表選取的狀態。在左側的頁面樹狀結構中，按一下「圖層」下的「狀態」。在右側的「圖層」屬性中，在「識別」下將「名稱」變更為**選取的狀態**。在「來源 (Source)」底下，將 Where 子句設定為 **state\_code = ：P3\_STATE** 。觀察左側頁面樹狀目錄中的圖層名稱變更為「選取的狀態」。
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![設定 WHERE 子句](images/add-spatial-analysis-14.png)
    
7.  最後更新機場層以傳回依使用者指定狀態和鄰近度篩選的項目。在左側的「頁面」樹狀結構中，按一下「機場」層。在右側的「層」屬性中，在「來源」下，將「類型」變更為 **SQL 查詢**。若為 SQL 查詢，請輸入下列項目，使用 Oracle Database 的原生 SQL 「含距離」運算子。
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    若要提交頁面項目，請輸入以逗號分隔的清單 **P3\_STATE，P3\_DISTANCE** 。
    
    ![空間 SQL 查詢](images/add-spatial-analysis-15.png)
    
8.  您的頁面已可供檢視。按一下**儲存**，然後按一下右上方的綠色**執行**按鈕。頁面呈現後，若要選取狀態，請選取 **Alabama** 。地圖會顯示 100 公里 (預設距離) 內選取的狀態與機場。
    
    ![「儲存並執行」頁面](images/add-spatial-analysis-16.png)
    
9.  將選取的狀態變更為**堪薩斯州**。觀察地圖現在以 100 公里顯示選取的州和機場。
    
    ![選取堪薩斯州](images/add-spatial-analysis-17.png)
    
10.  將距離提高至 600 公里，然後按一下 Enter 或 Tab 鍵提交。觀察地圖現在顯示距離較大的其他機場。
    
    ![距離 600 公里](images/add-spatial-analysis-18.png)
    
11.  最後確認送出負距離會造成稍早設定的「錯誤」即現式視窗。
    
    ![負距離警示](images/add-spatial-analysis-19.png)
    
    如您在本研討會開始時安裝的「範例地圖」應用程式中所示，您可以透過「地圖區域」和「空間」來取得大量額外的功能。本講座介紹了基礎知識，希望您對 APEX 應用程式中的地圖和空間分析能發揮作用。
    

## 進一步瞭解

*   [Oracle Spatial，空間](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - 資料庫產品管理 David Lapp - 2023 年 3 月