# サンプル・データの作成

## 概要

このラボでは、Oracle Databaseでサンプル空間データを作成するステップについて説明します。

推定ラボ時間: 10分

### 目標

この演習では、次のことを行います。

*   Oracle Databaseでの空間データ管理について学習
*   一般的なファイル形式からのOracle Databaseの空間データの準備

### 前提条件

*   ラボ2の完成

### 空間データについて

Oracle Databaseは、空間データ(ポイント、線、ポリゴン)をSDO\_GEOMETRYというネイティブ・データ型に格納します。Oracle Databaseは、高パフォーマンスの空間操作用のネイティブ空間索引も提供します。この空間索引は、各表に入力される空間メタデータと、空間データを格納するジオメトリ列に依存します。空間データが移入および索引付けされると、堅牢なAPIを使用して空間分析、計算および処理を実行できます。

SDO\_GEOMETRY型の一般的な形式は次のとおりです。

    SDO_GEOMETRY( 
     [geometry type],           --ID for point/line/polygon
     [coordinate system],       --ID of coordinate system
     [point coordinate],        --for points only
     [line/polygon info],       --for lines/polygons only
     [line/polygon coordinates] --for lines/polygons only
      )
    

最も一般的なジオメトリ・タイプは2次元です。

| ID | タイプ |
| --- | --- |
| 2001 | ポイント |
| 2002 | 明細 |
| 2003 | 多角形 |

最も一般的な座標系は次のとおりです。

| ID | 座標系 |
| --- | --- |
| 4326 | 緯度/経度 |
| 3857 | ワールドメルカトル |

緯度/経度を使用する場合、緯度はY座標、経度はX座標であることに注意してください。座標はX、Yペアとしてリストされるため、値は実際には経度、緯度の順序になります。

次に、緯度/経度座標を使用した点ジオメトリの例を示します。

    SDO_GEOMETRY( 
     2001,               --2D point
     4326,               --latitude/longitude
     SDO_POINT_TYPE(     
        -100.123, 20.456 --coordinate
        ),         
     NULL,               --for lines/polygons only
     NULL                --for lines/polygons only
      )
    

次に、緯度/経度座標を使用したポリゴン ジオメトリの例を示します。

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

この演習では、次のことを行います。

*   ジオメトリ列を含む表の作成
*   ジオメトリの移入
*   空間メタデータおよび索引の作成

### 前提条件

ワークショップの概要で説明されているように、Oracle DatabaseおよびSQLクライアントにアクセスする必要があります。これらがない場合は、Oracle Cloudアカウント、Autonomous DatabaseおよびSQL Developer Webのセクションに戻ります。

## タスク1: 座標を含む表の作成

まず、緯度、経度座標で表を作成します。これは、GPSからの座標、ジオコーディングの番地やIPアドレスなど、空間データを作成するための一般的な出発点です。

手順とスクリーンショットはSQL Developer Webを参照しますが、他のSQLクライアントにも同じ手順が適用されます。

1.  [ここ](files/create-sample-data.sql)でSQLスクリプトをダウンロードします。
    
2.  SQL Developer Webでのスクリプトのコピー/貼付け/実行 ![イメージ代替テキスト](images/run-script-1.png)
    
3.  表BRANCHESおよびWAREHOUSESを表示するには、リストをリフレッシュします
    
    ![イメージ代替テキスト](images/refresh-tables-1.png)
    

## タスク2: 座標からのジオメトリの作成

緯度列と経度列に基づいて点ジオメトリの座標を指定することで、例の場合はジオメトリにSQLを移入できます。

1.  ジオメトリ列を追加します。
    
        <copy> 
        ALTER TABLE WAREHOUSES ADD (
         GEOMETRY SDO_GEOMETRY
        );
        
        ALTER TABLE BRANCHES ADD (
           GEOMETRY SDO_GEOMETRY
        );
        </copy>
        
2.  ジオメトリ列を移入します。
    
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
        

## タスク3: 多角形を使用した表の作成

線分とポリゴンは同じ方法で作成できます。点ジオメトリには1つの座標が必要ですが、線とポリゴンにはジオメトリを定義するすべての座標が必要です。この場合、ポリゴンを格納するテーブルを作成します。

1.  表の作成および行の挿入
    
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
        
2.  表のリストをリフレッシュして、COASTAL\_ZONE表を表示します。 ![イメージ代替テキスト](images/refresh-tables-2.png)
    

## タスク4: 空間メタデータおよび索引の追加

Oracle Databaseは、高パフォーマンスの空間操作のためのネイティブ空間索引を提供します。サンプル・データは非常に小さいため、空間索引は必要ありません。ただし、一般的な本番データ・ボリュームでは重要なため、次のステップを実行します。空間索引には、索引付けするジオメトリのメタデータ行が必要です。このメタデータを作成し、空間索引を作成します。

1.  空間メタデータの追加:
    
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
        
2.  空間索引を作成します。
    
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
        
    
    索引が作成されたら、表のリストをリフレッシュします。名前がMDRT\_で始まる3つの表が表示されます。これらは空間索引のアーティファクトであり、Oracle Databaseによって自動的に管理されます。これらのテーブルを手動で操作しないでください。 ![イメージ代替テキスト](images/refresh-tables-3.png)
    
    サンプル・データが準備され、空間問合せの準備ができました。
    
    次の演習に進むことができます。
    
    この演習を元に戻して、作成した項目を削除する必要がある場合は、次を実行します。
    
         DROP TABLE BRANCHES;   
         DROP TABLE WAREHOUSES;
         DROP TABLE COASTAL_ZONE;
         DELETE FROM USER_SDO_GEOM_METADATA;
         COMMIT;
        

## さらに学ぶ

*   \[空間プロダクトポータル\] (https://oracle.com/goto/spatial)
*   [Spatialのマニュアル](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatialのブログ](https://blogs.oracle.com/oraclespatial/)

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - Kamryn Vinson、2020年11月