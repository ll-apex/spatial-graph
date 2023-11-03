# 空間問合せ

## 概要

このラボでは、Oracle Autonomous Databaseの基本的な空間問合せについて説明します。前の演習で作成したサンプル・データを使用して、近接性と封じ込めに基づいてアイテムを識別します。

見積時間: 20分

ラボのクイック・ウォークスルーについては、次のビデオをご覧ください。[空間データの準備](videohub:1_feaq2eu8)

### 目標

この演習では、次のことを行います。

*   Oracle Databaseでの空間問合せの学習と実行

### 前提条件

*   演習3の完了: 空間データの準備

### 空間問合せについて

Oracle Databaseには、空間分析用の関数と演算子の堅牢なライブラリが含まれています。これには、空間関係、測定、集計、変換などが含まれます。これらの操作は、ネイティブSQL、PL/SQL、Java API、およびPythonやNode.jsなどのOracleへの接続モジュールを持つその他の言語を介してアクセスできます。

最も一般的な操作は、空間フィルタリングおよび結合を実行する空間演算子、および計算および変換を実行する空間関数です。

空間演算子は、INSIDEやWITHIN\_DISTANCEなどの空間関係をテストし、関係が存在する場合はTRUEを返します。空間演算子は、問合せのWHERE句で使用されます。一般的に次のようになります。

    <code>
    SELECT [fields]
    FROM [tables]
    WHERE [Spatial Operator]='TRUE'
    AND [other conditions...]
    </code>
    

たとえば、MY\_REGIONSのREGION-01内にあるMY\_POINTS内のアイテムを識別するには:

    <code>
    SELECT *
    FROM MY_POINTS A, MY_REGIONS B
    WHERE SDO_INSIDE(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
    AND B.NAME='MY_REGION-01';
    </code>
    

空間関数は値を返し、SELECTリストにあるか、WHERE句で使用できます。一般的に次のようになります。

    <code>
    SELECT [Spatial Function], [other fields...]
    FROM [tables]
    WHERE [conditions]
    </code>
    

たとえば、MY\_REGIONSのREGION-01の領域を取得するには:

    <code>
    SELECT SDO_GEOM.SDO_AREA(GEOMETRY)
    FROM MY_REGIONS
    WHERE NAME='MY_REGION-01';
    </code>
    

[ここ](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl/spatial-reference-information.html)で説明されているように、数百のSpatial SQLおよびPL/SQL操作を使用できます。この演習で最も一般的なもののいくつかを確認します。

### 目標

この演習では、空間問合せを実行して、店舗、倉庫、リージョンおよび竜巻パス間の場所の関係を識別します。

### 前提条件

*   演習3: 空間データの準備の完了

## タスク1: 近接問合せ

近接性は、アイテムが互いにどの程度近いかに関連しています。2つの主なSpatial近接演算子は次のとおりです。

*   SDO\_WITH\_DISTANCE( )は、別のアイテムから指定された距離内のアイテムを返します
*   SDO\_NN( )は、別のアイテムに最も近いアイテムを返します。

1.  まず、**SDO\_WITHIN\_DISTANCE( )**を使用して、ダラス・ウェアハウスから20マイル以内の店舗を識別します。**SDO\_WITHIN\_DISTANCE( )**の最初の引数は、(ジオメトリ列ではなく) STORESのジオメトリを返す関数であることに注意してください。これは、関連するファンクションベースの空間索引を作成したため使用できます。
    
        <copy> 
         SELECT
             STORE_NAME,
             STORE_TYPE
         FROM
             STORES     A,
             WAREHOUSES B
         WHERE
              B.WAREHOUSE_NAME = 'Dallas Warehouse'
         AND SDO_WITHIN_DISTANCE(
               GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
               B.GEOMETRY,
               'distance=20 unit=mile') = 'TRUE'
        </copy>
        
    
    ![近接問合せ](images/run-queries-01.png)
    
2.  別のアイテムに最も近いアイテムを識別するには、Spatial演算子**SDO\_NN( )**を使用します。NNはNearest Neighborを表します。次の問合せを実行して、ダラス・ウェアハウスに最も近い5つのストアを識別します。ここでも、**SDO\_NN( )**の最初の引数は、関数ベースの空間索引を持つジオメトリを返す関数であることに注意してください。
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10') = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![近接問合せ](images/run-queries-02.png)
    
3.  **SDO\_NN( )**演算子を使用すると、距離を含めることができます。次の問合せを実行して、距離とともにDallas Warehouseに最も近い5店舗をマイルで返します。
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10 unit=MILE', 1) = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![近接問合せ](images/run-queries-03.png)
    
4.  次の問合せを実行して、距離とともにDallas Warehouseに最も近い5つの小売店をマイルで返します。小売店のみを検索するため、結果には前回の結果より遠い店舗が含まれることに注意してください。
    
        <copy> 
         SELECT
              STORE_NAME,
              STORE_TYPE,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE B.WAREHOUSE_NAME = 'Dallas Warehouse'
          AND A.STORE_TYPE='RETAIL'
           AND SDO_NN(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY,
                'sdo_batch_size=10 unit=MILE', 1) = 'TRUE'
         AND ROWNUM <= 5;
        </copy>
        
    
    ![近接問合せ](images/run-queries-04.png)
    
5.  SDO\_NN( )などの空間演算子を使用して結合を作成することもできます。次の問合せを実行して、最も近い倉庫の名前を持つ各店舗を返します。
    
        <copy> 
          SELECT a.store_name, b.warehouse_name
          FROM stores a,warehouses b
          WHERE SDO_NN(b.geometry,
                  get_geometry(a.longitude,a.latitude), 
                  'sdo_num_res=1') = 'TRUE';
        </copy>
        

![近接問合せ](images/run-queries-05.png)

4.  次の問合せを実行して、最も近い倉庫の名前と距離(マイル)を持つ各店舗を返します。
    
        <copy> 
          SELECT
              A.STORE_NAME,
              B.WAREHOUSE_NAME,
              ROUND( SDO_NN_DISTANCE(1) , 2) DISTANCE_MI
          FROM
              STORES     A,
              WAREHOUSES B
          WHERE
              SDO_NN(B.GEOMETRY,
                     GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                     'sdo_num_res=1 unit=MILE', 1) = 'TRUE';
        </copy>
        

![近接問合せ](images/run-queries-06.png)

4.  近接性は集計分析に役立ちます。次の問合せを実行して、Dallas Warehouseから20マイル以内の竜巻の数および最大損失を返します。
    
        <copy> 
           SELECT
               COUNT(A.KEY),
               MAX(A.LOSS)
           FROM
               TORNADO_PATHS A,
               WAREHOUSES B
           WHERE
               B.WAREHOUSE_NAME = 'Dallas Warehouse'
            AND SDO_WITHIN_DISTANCE( A.GEOMETRY,
                                     B.GEOMETRY,
                  'distance=20 unit=mile') = 'TRUE'
        </copy>
        
    
    ![近接問合せ](images/run-queries-07.png)
    
    1.  結合用のSpatial演算子の使用に戻り、次の問合せを実行して、竜巻の数と最大損失が20マイル以内の各ウェアハウスを返します。
    
        <copy> 
           SELECT
               B.WAREHOUSE_NAME,
               COUNT(A.KEY),
               MAX(A.LOSS)
           FROM
               TORNADO_PATHS A,
               WAREHOUSES B
           WHERE SDO_WITHIN_DISTANCE( A.GEOMETRY,
                                     B.GEOMETRY,
                  'distance=20 unit=mile') = 'TRUE'
           GROUP BY B.WAREHOUSE_NAME;  
        </copy>
        
    
    ![近接問合せ](images/run-queries-08.png)
    

問合せの距離値を20から50マイルに増やし、新しい結果を確認します。

## タスク2: 包含問合せ

封じ込めとは、特定の地域に含まれるアイテムを識別することであり、その逆もまた、特定のアイテムを含む地域を識別することです。空間メインの空間包含演算子は次のとおりです。

*   SDO\_INSIDE( )は、リージョン内のアイテムを返します。境界上の項目は返されません。
*   SDO\_CONTAINS( )は、アイテムを含むリージョンを返します。境界上の項目は含まれているとはみなされません。
*   SDO\_ANYINTERACT( )は、境界上の項目や領域にまたがる行など、部分的に含まれる項目など、他の項目との空間関係を持つ項目を返します。

1.  SDO\_INSIDE( )を使用して、REGION-02のストア(境界上のストアは含まない)を返します。
    
        <copy> 
          SELECT
              A.STORE_NAME,
              A.STORE_TYPE
          FROM
              STORES  A,
              REGIONS B
          WHERE REGION = 'REGION-02'
          AND SDO_INSIDE(
                 GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                 B.GEOMETRY) = 'TRUE';
         </copy>
        
    
    ![包含問合せ](images/run-queries-09.png)
    
2.  SDO\_INSIDE( )を使用して、含まれるリージョンを持つ各ストアを返します。これは、以前にSDO\_NN( )で行ったように、Spatial演算子を使用して結合を実行するもう1つの例です。リージョン境界上のストアは含まれないことに注意してください。境界にストアを含めるには、SDO\_ANYINTERACT( )を使用します。
    
        <copy> 
        SELECT
              A.STORE_NAME,
              A.STORE_TYPE,
              B.REGION
          FROM
              STORES  A,
              REGIONS B
          WHERE SDO_INSIDE(
                GET_GEOMETRY(A.LONGITUDE, A.LATITUDE),
                B.GEOMETRY) = 'TRUE';
         </copy>
        
    
    ![包含問合せ](images/run-queries-10.png)
    
3.  次に、地域ごとの竜巻の集計のためにSDO\_ANYINTERACT( )を使用します。次を実行して、竜巻の数と各地域の最大損失を返します。SDO\_ANYINTERACT( )は、領域によって完全にまたは部分的に含まれる竜巻経路などの空間関係を持つ項目を返します。
    
        <copy> 
        SELECT
            B.REGION,
            COUNT(*),
            MAX(LOSS)
        FROM
            TORNADO_PATHS A,
            REGIONS       B
        WHERE
            SDO_ANYINTERACT(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
        GROUP BY
            REGION
        ORDER BY
            REGION;
        </copy>
        
    
    ![包含問合せ](images/run-queries-11.png)
    
4.  100,000ドルを超える損失の竜巻を含むリージョンを識別します。
    
        <copy> 
          SELECT DISTINCT
              A.REGION
          FROM
              REGIONS       A,
              TORNADO_PATHS B
          WHERE
                 SDO_CONTAINS(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
          AND 
                 B.LOSS > 100000
          ORDER BY
              REGION;
        </copy>
        
    
    ![包含問合せ](images/run-queries-12.png)
    
5.  100,000ドルを超える損失の竜巻を含む地域と、竜巻の総数を特定します。
    
        <copy> 
          SELECT DISTINCT
              A.REGION,
              COUNT(B.KEY)
          FROM
              REGIONS       A,
              TORNADO_PATHS B
          WHERE
                  SDO_CONTAINS(A.GEOMETRY, B.GEOMETRY) = 'TRUE'
              AND B.LOSS > 100000
          GROUP BY
              REGION
          ORDER BY
              REGION;
        </copy>
        
    
    ![包含問合せ](images/run-queries-13.png)
    

**次の演習に進む**ことができます。

## さらに学ぶ

*   [空間製品ポータル](https://oracle.com/goto/spatial)
*   [Spatialのマニュアル](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatialのブログ記事: Oracle Database Insider](https://blogs.oracle.com/database/category/db-spatial)

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **コントリビュータ** - Karin Patenge氏、データベース製品管理、Oracle
*   **最終更新者/日付** - David Lapp、2022年9月