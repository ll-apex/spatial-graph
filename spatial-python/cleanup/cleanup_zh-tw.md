# 清除

## 簡介

您可以將 Autonomous Database 重設為研習前狀態，以清除研習環境。

預估實驗室時間：2 分鐘

### 目標

*   將 Autonomous Database 重設為研習前狀態

### 先決條件

*   作用中 Autonomous Database 執行處理

## 任務 1：將 Autonomous Database 重設為研習前狀態

1.  執行下列項目以移除在此研習中建立的所有資料庫使用者自建物件。
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## 確認

*   **作者** - Oracle 資料庫產品管理 David Lapp
*   **上次更新者 / 日期** - David Lapp，2023 年 8 月