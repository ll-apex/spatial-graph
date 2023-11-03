# 空間查詢

## 簡介

本實驗室會逐步引導您完成 Oracle Database 的基本空間查詢。您將使用先前實驗室中建立的樣本資料，根據鄰近與包含內容來識別項目。

預估實驗室時間：15 分鐘

### 關於空間查詢

Oracle Database 包含強大的函數庫和用於空間分析的運算子。這包括空間關係、測量、聚總和轉換等。透過原生 SQL、PL/SQL、Java API 以及與 Oracle Database 通訊的任何其他語言即可存取這些作業。

### 目標

在此實驗室中，您將：

*   識別與倉儲具有鄰近關係的 BRANCHES
*   識別具有與 COASTAL\_ZONE 相鄰關係的 BRANCHES

### 先決條件

*   完成上一個實驗室；建立樣本空間資料

## 空間查詢

Oracle Database 中的空間查詢就像您慣用的任何其他傳統查詢一樣。唯一的差異是空間函數和運算子的集合，這可能是您新的函數。

**識別 Dallas Warehouse 有 5 個最接近的分支：**

    <copy> 
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5'
        ) = 'TRUE';
    </copy>
    

![執行空間查詢](images/query1.png) 備註：

*   `SDO_NN` 運算子會傳回 Dallas Warehouse 的 'n nearest' 分支，其中 'n' 是 `SDO_NUM_RES` 專用的值。`SDO_NN` 的第一個引數 (上述範例中的 `B.GEOMETRY`) 是要搜尋的資料欄。第二個引數 (上述範例中的 `W.GEOMETRY`) 是您要尋找鄰近位置的位置。不應就傳回結果的順序作出任何假設。例如，傳回的第一列不保證是最接近的。如果兩個或多個分支與倉儲距離相等，則後續呼叫 `SDO_NN` 時可能會傳回任一分支。
*   使用 `SDO_NUM_RES` 參數時，不會在 `WHERE` 子句中使用其他條件。`SDO_NUM_RES` 只考量鄰近值。例如，如果您將準則新增至 `WHERE` 子句，因為您想要五個具有特定郵遞區號最接近的分支，而五個最接近的分支中有四個具有不同的郵遞區號，則上述查詢會傳回一列。此行為是 `SDO_NUM_RES` 參數的特定行為。在下方的查詢中，您將使用其他查詢準則案例的替代參數。

**識別達拉斯倉庫距離最接近的五個分支：**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_num_res=5 unit=km', 1
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![執行空間查詢](images/query2.png) 備註：

*   `SDO_NN_DISTANCE` 運算子是 `SDO_NN` 運算子的輔助運算子，只能在 `SDO_NN` 運算子中使用。此運算子的引數是符合指定為 `SDO_NN` 最後一個引數之數字的數字，在此範例中為 1。這個引數沒有隱藏意義，只是一個標記。如果指定 `SDO_NN_DISTANCE()`，您可以依距離排序結果，並保證傳回的第一列是最接近的列。如果您查詢的資料儲存為經緯度，則 `SDO_NN_DISTANCE` 的預設單位為公尺。
*   `SDO_NN` 運算子也有 `UNIT` 參數，可決定 `SDO_NN_DISTANCE` 傳回的計量單位。
*   `ORDER BY DISTANCE` 子句可確保以最短距離的順序傳回距離。

**找出距離達拉斯倉庫最接近的 5 個 WHOLESALE 分支：**

    <copy>
    SELECT
        BRANCH_NAME,
        BRANCH_TYPE,
        ROUND(
            SDO_NN_DISTANCE(
                1
            ), 2
        ) DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Dallas Warehouse'
        AND B.BRANCH_TYPE = 'WHOLESALE'
        AND SDO_NN(
            B.GEOMETRY, W.GEOMETRY, 'sdo_batch_size=5 unit=km', 1
        ) = 'TRUE'
        AND ROWNUM <= 5
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![執行空間查詢](images/query3.png) 備註：

*   `SDO_BATCH_SIZE` 是可能影響查詢效能的可調整參數。`SDO_NN` 會內部計算一次該距離數。傳回的初始資料列批次可能不符合 WHERE 子句中的限制條件，因此 `SDO_BATCH_SIZE` 指定的資料列數目會持續傳回，直到滿足 WHERE 子句中的所有限制條件為止。您應該選擇一開始會傳回可能滿足 WHERE 子句中限制之資料列數的 `SDO_BATCH_SIZE`。
*   `SDO_NN` 運算子內使用的 `UNIT` 參數指定 `SDO_NN_DISTANCE` 參數的計量單位。預設單位是與資料關聯的單位。若為經度和緯度資料，預設值為公尺。
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5` 是 `WHERE` 子句中的額外限制條件。黎明子句必須限制傳回的結果數目為 5。
*   `ORDER BY DISTANCE_KM` 子句可確保以順序傳回距離，最短距離優先，距離以英里為單位測量距離。

**在休士頓倉庫 50 公里內識別分行：**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE';
    </copy>
    

![執行空間查詢](images/query4.png) 備註：

*   `SDO_WITHIN_DISTANCE` 的第一個引數是要搜尋的資料欄。第二個引數是您要判斷距離的來源位置。不應就傳回結果的順序作出任何假設。例如，傳回的第一列不保證是最接近倉儲 3 的客戶。
*   `SDO_WITHIN_DISTANCE` 運算子內使用的 DISTANCE 參數指定距離值；在此範例中為 100。
*   `SDO_WITHIN_DISTANCE` 運算子內使用的 UNIT 參數指定 DISTANCE 參數的單位。預設單位是與資料關聯的單位。對於經度與緯度資料，預設值為公尺；在此範例中為英哩。

**在休士頓倉庫 50 公里內找到分店，距離：**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE,
        ROUND(
            SDO_GEOM.SDO_DISTANCE(
                B.GEOMETRY, W.GEOMETRY, 0.05, 'unit=km'
            ), 2
        ) AS DISTANCE_KM
    FROM
        BRANCHES    B,
        WAREHOUSES  W
    WHERE
        W.WAREHOUSE_NAME = 'Houston Warehouse'
        AND SDO_WITHIN_DISTANCE(
            B.GEOMETRY, W.GEOMETRY, 'distance=50 unit=km'
        ) = 'TRUE'
    ORDER BY
        DISTANCE_KM;
    </copy>
    

![執行空間查詢](images/query5.png) 備註：

*   `SDO_GEOM.SDO_DISTANCE` 函數會計算分支位置與 Houston Warehouse 之間的距離。
*   `SDO_GEOM.SDO_DISTANCE` 的前 2 個引數是 BRANCH 和 WAREHOUSE 位置，可用於距離計算。
*   `SDO_GEOM.SDO_DISTANCE` 的第三個引數是公差值。此允差是 Oracle Spatial 使用的捨入錯誤值。經度與緯度資料的允差單位為公尺。在此範例中，公差為 50 mm。
*   `SDO_GEOM.SDO_DISTANCE` 參數內使用的 UNIT 參數指定由 `SDO_GEOM`.`SDO_DISTANCE` 函數計算的距離單位。預設單位是與資料關聯的單位。若為經度和緯度資料，預設值為公尺。在此範例中為英里。
*   `ORDER BY DISTANCE_IN_MILES` 子句可確保以順序傳回距離，最短距離優先，距離以英里為單位測量距離。

**識別沿海區中的分支：**

    <copy>
    SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE';
    </copy>
    

![執行空間查詢](images/query6.png) 備註：

*   `SDO_ANYINTERACT` 運算子接受 2 個引數 geometry1 和 geometry2。運算子會針對 geometry1 位於 geometry2 內或位於邊界的資料列傳回 `TRUE`。
*   在此範例中，geometry1 為 `B.GEOMETRY`，分支幾何，geometry2 為 `C.GEOMETRY`，沿海區域幾何圖形。COASTAL\_ZONE 表格只有 1 個資料列，因此不需要其他條件。

**在沿海地區 10 公里內識別分支：**

    <copy>
    
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_WITHIN_DISTANCE(
            B.GEOMETRY, C.GEOMETRY, 'distance=10 unit=km'
        ) = 'TRUE'
    )
    MINUS
    ( SELECT
        B.BRANCH_NAME,
        B.BRANCH_TYPE
    FROM
        BRANCHES      B,
        COASTAL_ZONE  C
    WHERE
        SDO_ANYINTERACT(
            B.GEOMETRY, C.GEOMETRY
        ) = 'TRUE'
    );
    </copy>
    

![執行空間查詢](images/query7.png) 備註：

*   在此查詢的第一個部分中，`SDO_WITHIN_DISTANCE` 運算子會在 COASTAL\_ZONE 的 10 公里內識別 BRANCHES。這包括 COASTAL\_ZONE 中的 BRANCHES。
*   此查詢使用 `MINUS` 來移除 COASTAL\_ZONE 中的 BRANCHES，只讓 BRACNCHES 在 10 公里內與 COASTAL\_ZONE 之外。

## 進一步瞭解

*   \[ 空間產品入口網站 \] (https://oracle.com/goto/spatial)
*   [空間文件](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [空間部落格](https://blogs.oracle.com/oraclespatial/)

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - Kamryn Vinson，2020 年 11 月