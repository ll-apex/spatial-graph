# クリーンアップ

## 概要

Autonomous Databaseをワークショップ前の状態にリセットすることで、ワークショップ環境をクリーンアップできます。

推定ラボ時間: 2分

### 目標

*   Autonomous Databaseをワークショップ前の状態にリセット

### 前提条件

*   アクティブなAutonomous Databaseインスタンス

## タスク1: Autonomous Databaseのワークショップ前の状態へのリセット

1.  このワークショップで作成されたすべてのデータベース・アーティファクトを削除するには、次を実行します。
    
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

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - David Lapp、2023年8月