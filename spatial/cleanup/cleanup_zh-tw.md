# 將 ADB 重設為研習前狀態

## 簡介

此實驗室會移除在先前實驗室中建立的所有內容，以便您可以視需要重新開始。

預估實驗室時間：2 分鐘

### 關於

在此實驗室中，所有先前建立的使用者自建物件都會被刪除。

### 目標

*   將 ADB 重設為研習前狀態。

### 先決條件

*   完成實驗室 3；準備空間資料

## 工作 1：移除此研討會中建立的所有項目

1.  若要移除此研討會中建立的表格與索引，請使用「SQL 工作表」中的執行指令碼按鈕執行下列作業。
    
    ![影像替代文字](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  若要刪除插入此研習中的空間中繼資料，請使用「SQL 工作表」中的執行腳本按鈕執行下列作業。
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  若要刪除此研討會中建立的功能，請執行下列作業。
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - David Lapp，2022 年 9 月