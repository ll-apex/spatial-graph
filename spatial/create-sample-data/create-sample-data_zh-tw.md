# 建立樣本資料

## 簡介

這個實驗室會逐步引導您在 Oracle Database 中建立範例空間資料。

預估實驗室時間：10 分鐘

### 目標

在此實驗室中，您將：

*   瞭解 Oracle Database 中的空間資料管理
*   從一般檔案格式準備 Oracle Database 中的空間資料

### 先決條件

*   實驗室 2 完成

### 關於空間資料

Oracle Database 將空間資料 (點、線條、多邊形) 儲存在名為 SDO\_GEOMETRY 的原生資料類型中。Oracle Database 也提供原生空間索引，以進行高效能空間作業。此空間索引依賴為每個表格輸入的空間描述資料，以及儲存空間資料的幾何資料欄。在填入空間資料並建立索引之後，就會提供健全的 API 來執行空間分析、計算以及處理。

SDO\_GEOMETRY 類型的一般格式如下：

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

最常見的幾何類型為二維：

| 識別碼 | 類型 |
| --- | --- |
| 2001 年 | 點 |
| 2002 年 | 明細行 |
| 2003 年 | 多邊形 |

最常見的座標系統為：

| 識別碼 | 座標系統 |
| --- | --- |
| 4326 人 | 緯度 / 經度 |
| 3857 年 | World Mercator |

使用緯度 / 經度時，請注意緯度為 Y 座標，經度為 X 座標。由於座標列為 X，Y 組，因此值實際上是依緯度順序排列。

以下是使用緯度 / 經度座標的點幾何範例：

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

以下是使用緯度 / 經度座標的多邊形幾何範例：

    SDO_GEOMETRY( 
     2003,                  --2D polygon
     4326,                  --latitude/longitude
     NULL,                  --for points only       
     SDO_ELEM_INFO_ARRAY(
          1, 1003, 1        --indicates simple exterior polygon
            ), 
     SDO_ORDINATE_ARRAY(   
        -98.789065,39.90973, -- coordinates
        -101.2522,39.639537,
        -99.84374,37.160316,
        -96.67987,35.460699,
        -94.21875,39.639537,
        -98.789025,39.90973
          )
        )
    );
    

### 目標

在此實驗室中，您將：

*   建立含有幾何資料欄的表格
*   填入幾何
*   建立空間描述資料與索引

### 先決條件

如研討會簡介所述，您需要存取 Oracle Database 和 SQL Client。如果您沒有這些經驗，請返回 Oracle Cloud Account、Autonomous Database 和 SQL Developer Web 上的區段。

## 作業 1：建立含有座標的表格

我們從建立緯度、經度座標的表格開始。這是建立空間資料的常見起點，例如來自 GPS 的座標，或來自地理編碼街道地址或 IP 位址。

指示與螢幕擷取畫面參照 SQL Developer Web，不過，相同的步驟也適用於其他 SQL 用戶端。

1.  [在此](files/create-sample-data.sql)下載 SQL 命令檔。
    
2.  在 SQL Developer Web 中複製 / 貼上 / 執行命令檔 ![影像替代文字](images/run-script-1.png)
    
3.  重新整理清單以查看表格 BRANCHES 與 WAREHOUS
    
    ![影像替代文字](images/refresh-tables-1.png)
    

## 工作 2：從座標建立幾何

可以使用 SQL 填入幾何圖形，以便根據緯度與經度資料欄指定點幾何的座標。

1.  新增幾何資料欄：
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  產生幾何資料欄：
    
        <copy> 
        UPDATE WAREHOUSES
        SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
         UPDATE BRANCHES
         SET
            GEOMETRY = SDO_GEOMETRY(
                2001, 4326, SDO_POINT_TYPE(
                    LON, LAT, NULL
                ), NULL, NULL
            );
        </copy>
        

## 作業 3：建立具有多邊形的表格

可以使用相同的方式建立行與多邊形。雖然點幾何需要一個座標，但線和多邊形需要定義幾何的所有座標。在這種情況下，我們會建立用來儲存多邊形的表格。

1.  建立表格並插入資料列
    
        <copy>
        CREATE TABLE COASTAL_ZONE (
            ZONE_ID   NUMBER,
            GEOMETRY  SDO_GEOMETRY
        );       
        
        INSERT INTO COASTAL_ZONE VALUES (
            1,
            SDO_GEOMETRY(
                2003, 4326, NULL, SDO_ELEM_INFO_ARRAY(
                    1, 1003, 1
                ), SDO_ORDINATE_ARRAY(
                    -93.719934, 30.210638,
                    -95.422592, 29.773714, 
                    -95.059698, 29.322204, 
                    -96.013892, 28.787021, 
                    -96.660964, 28.925638, 
                    -97.528688, 28.042050, 
                    -97.858501, 27.447461, 
                    -97.497364, 25.880056, 
                    -96.977826, 25.969716, 
                    -97.211445, 27.054605, 
                    -96.870226, 27.816077, 
                    -93.794290, 29.535729, 
                    -93.719934, 30.210638
                )
            )
        );
        </copy>
        
2.  重新整理表格清單以查看 COASTAL\_ZONE 表格。 ![影像替代文字](images/refresh-tables-2.png)
    

## 作業 4：新增空間描述資料與索引

Oracle Database 為高效能空間作業提供原生空間索引。我們的範例資料非常小，因此不需要空間索引。不過，執行下列步驟對一般生產資料磁碟區而言非常重要。空間索引需要一列中繼資料，才能索引幾何。我們會先建立這個描述資料，然後再建立空間索引。

1.  新增空間中繼資料 ：
    
        <copy> 
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'WAREHOUSES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'BRANCHES',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        
        INSERT INTO USER_SDO_GEOM_METADATA VALUES (
           'COASTAL_ZONE',
           'GEOMETRY',
           SDO_DIM_ARRAY(
               SDO_DIM_ELEMENT(
                   'x', -180, 180, 0.05
               ), SDO_DIM_ELEMENT(
                   'y', -90, 90, 0.05
               )
           ),
           4326
        );
        </copy>
        
2.  建立空間索引：
    
        <copy> 
        CREATE INDEX WAREHOUSES_SIDX ON
            WAREHOUSES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX BRANCHES_SIDX ON
            BRANCHES (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
        
        CREATE INDEX COASTAL_ZONE_SIDX ON
            COASTAL_ZONE (
                GEOMETRY
            )
                INDEXTYPE IS MDSYS.SPATIAL_INDEX;
         </copy>
        
    
    建立索引之後，請重新整理表格清單。您會看到 3 個名稱開頭為 MDRT\_ 的表格。這些是空間索引的使用者自建物件，由 Oracle Database 自動管理。您永遠不應該手動操控這些表格。 ![影像替代文字](images/refresh-tables-3.png)
    
    我們現在已經準備好範例資料，並準備進行空間查詢。
    
    您現在可以繼續下一個實驗室。
    
    如果您需要回復此實驗室並移除已建立的項目，請執行下列作業：
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## 進一步瞭解

*   \[ 空間產品入口網站 \] (https://oracle.com/goto/spatial)
*   [空間文件](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [空間部落格](https://blogs.oracle.com/oraclespatial/)

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - Kamryn Vinson，2020 年 11 月