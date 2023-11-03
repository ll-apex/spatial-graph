# ADBをワークショップ前の状態にリセット

## 概要

この演習では、前の演習で作成したものをすべて削除して、必要に応じてやり直すことができます。

推定ラボ時間: 2分

### 情報

この演習では、以前に作成したすべてのアーティファクトが削除されます。

### 目標

*   ADBをワークショップ前の状態にリセットします。

### 前提条件

*   演習3の完了: 空間データの準備

## タスク1: このワークショップで作成されたすべての削除

1.  このワークショップで作成された表および索引を削除するには、SQLワークシートの「スクリプトの実行」ボタンを使用して次を実行します。
    
    ![イメージ代替テキスト](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  このワークショップに挿入された空間メタデータを削除するには、SQLワークシートの「スクリプトの実行」ボタンを使用して次を実行します。
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  このワークショップで作成したファンクションを削除するには、次を実行します。
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - David Lapp、2022年9月