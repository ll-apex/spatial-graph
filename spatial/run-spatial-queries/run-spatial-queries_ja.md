# 空間問合せ

## 概要

このラボでは、Oracle Databaseの基本的な空間問合せについて説明します。前の演習で作成したサンプル・データを使用して、近接性と封じ込めに基づいてアイテムを識別します。

推定ラボ時間: 15分

### 空間問合せについて

Oracle Databaseには、空間分析用の関数と演算子の堅牢なライブラリが含まれています。これには、空間関係、測定、集計、変換などが含まれます。これらの操作には、ネイティブSQL、PL/SQL、Java API、およびOracle Databaseと通信するその他の言語を介してアクセスできます。

### 目標

この演習では、次のことを行います。

*   WAREHOUSEとの近接関係を持つBRANCHESの識別
*   COASTAL\_ZONEへの包含関係および近接関係を持つBRANCHESの識別

### 前提条件

*   前の演習の完了: サンプル空間データの作成

## 空間問合せ

Oracle Databaseの空間問合せは、慣れ親しんだ他の従来の問合せと同じです。唯一の違いは、おそらく初めての空間関数と演算子のセットです。

**ダラス倉庫に最も近い5つの支店を識別します。**

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
    

![空間問合せの実行](images/query1.png) ノート:

*   `SDO_NN`演算子は、最も近いn個のブランチをダラス・ウェアハウスに返します。ここで、nは`SDO_NUM_RES`に固有の値です。`SDO_NN`の最初の引数(前述の例では`B.GEOMETRY`)は、検索する列です。2番目の引数(前述の例では`W.GEOMETRY`)は、最も近いネイバーを検索する場所です。返される結果の順序については、想定しないでください。たとえば、返される最初の行が最も近いことは保証されません。2つ以上のブランチがウェアハウスから等しい距離にある場合は、`SDO_NN`への後続のコールでいずれかが返されます。
*   `SDO_NUM_RES`パラメータを使用する場合、`WHERE`句で他の基準は使用されません。`SDO_NUM_RES`は近接のみを考慮します。たとえば、特定の郵便番号を持つ最も近い5つの支店が必要で、最も近い5つの支店の4つの郵便番号が異なるため、`WHERE`句に基準を追加した場合、前述の問合せでは1行が返されます。この動作は、`SDO_NUM_RES`パラメータに固有です。次の問合せでは、追加の問合せ基準のシナリオに代替パラメータを使用します。

**ダラス倉庫に最も近い5つの支店を距離で識別します。**

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
    

![空間問合せの実行](images/query2.png) ノート:

*   `SDO_NN_DISTANCE`演算子は、`SDO_NN`演算子の補助演算子であり、`SDO_NN`演算子内でのみ使用できます。この演算子の引数は、`SDO_NN`の最後の引数として指定された数値と一致する数値です。この例では1です。この引数には隠された意味はなく、単なるタグです。`SDO_NN_DISTANCE()`が指定されている場合は、距離によって結果を順序付けし、返される最初の行が最も近いことを保証できます。問合せするデータが経度および緯度として格納されている場合、`SDO_NN_DISTANCE`のデフォルト単位はメートルです。
*   `SDO_NN`演算子には、`SDO_NN_DISTANCE`によって返される単位を決定する`UNIT`パラメータもあります。
*   `ORDER BY DISTANCE`句を使用すると、距離が最短距離から順に返されます。

**ダラス倉庫に最も近い5つの卸売支店を距離で識別します。**

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
    

![空間問合せの実行](images/query3.png) ノート:

*   `SDO_BATCH_SIZE`は、問合せのパフォーマンスに影響を与える可能性のあるチューニング可能なパラメータです。`SDO_NN`は、一度にその距離数を内部的に計算します。返される行の初期バッチは、WHERE句の制約を満たさない場合があるため、WHERE句のすべての制約が満たされるまで、`SDO_BATCH_SIZE`で指定された行数は継続的に返されます。最初に、WHERE句の制約を満たす可能性のある行数を返す`SDO_BATCH_SIZE`を選択する必要があります。
*   `SDO_NN`演算子内で使用される`UNIT`パラメータは、`SDO_NN_DISTANCE`パラメータの単位を指定します。デフォルトの単位は、データに関連付けられている単位です。経度および緯度データの場合、デフォルトはmです。
*   `B.BRANCH_TYPE = 'WHOLESALE' AND ROWNUM <= 5`は、`WHERE`句の追加制約です。rownum句は、返される結果の数を5に制限するために必要です。
*   `ORDER BY DISTANCE_KM`句を使用すると、距離が順番に返され、最短距離が先に、距離がマイル単位で測定されます。

**ヒューストン倉庫から50km以内の支店を特定:**

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
    

![空間問合せの実行](images/query4.png) ノート:

*   `SDO_WITHIN_DISTANCE`の最初の引数は、検索する列です。2番目の引数は、距離を決定する場所です。返される結果の順序については、想定しないでください。たとえば、返される最初の行は、倉庫3に最も近い顧客である保証されません。
*   `SDO_WITHIN_DISTANCE`演算子内で使用されるDISTANCEパラメータは距離値を指定します。この例では100です。
*   `SDO_WITHIN_DISTANCE`演算子内で使用されるUNITパラメータは、DISTANCEパラメータの単位を指定します。デフォルトの単位は、データに関連付けられている単位です。経度および緯度データの場合、デフォルトはメートルで、この例ではマイルです。

**距離のヒューストン倉庫の50km以内の枝を特定して下さい:**

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
    

![空間問合せの実行](images/query5.png) ノート:

*   `SDO_GEOM.SDO_DISTANCE`関数は、ブランチの場所とヒューストン・ウェアハウス間の距離を計算します。
*   `SDO_GEOM.SDO_DISTANCE`の最初の2つの引数は、距離計算用のBRANCHおよびWAREHOUSEの場所です。
*   `SDO_GEOM.SDO_DISTANCE` の3番目の引数は許容値です。許容範囲は、Oracle Spatialで使用されるラウンドオフ・エラー値です。許容範囲は、経度および緯度データのメートル単位です。この例では、許容差は50 mmです。
*   `SDO_GEOM.SDO_DISTANCE`パラメータ内で使用されるUNITパラメータは、`SDO_GEOM`.`SDO_DISTANCE`関数で計算される距離の単位を指定します。デフォルトの単位は、データに関連付けられている単位です。経度および緯度データの場合、デフォルトはmです。この例ではマイルです。
*   `ORDER BY DISTANCE_IN_MILES`句を使用すると、距離が順番に返され、最短距離が先に、距離がマイル単位で測定されます。

**沿岸ゾーンのブランチを識別します。**

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
    

![空間問合せの実行](images/query6.png) ノート:

*   `SDO_ANYINTERACT`演算子は、2つの引数、geometry1およびgeometry2を受け入れます。この演算子は、geometry1がgeometry2の内部または境界にある行に対して`TRUE`を返します。
*   この例では、geometry1は`B.GEOMETRY`、ブランチ・ジオメトリ、geometry2は`C.GEOMETRY`、沿岸ゾーン・ジオメトリです。COASTAL\_ZONE表には1行しかないため、追加の基準は必要ありません。

**沿岸地帯の外および10km以内の枝を特定して下さい:**

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
    

![空間問合せの実行](images/query7.png) ノート:

*   この問合せの最初の部分では、`SDO_WITHIN_DISTANCE`演算子はCOASTAL\_ZONEから10km以内にBRANCHESを識別します。これには、COASTAL\_ZONE内のBRANCHESが含まれます。
*   問合せでは、`MINUS`を使用してCOASTAL\_ZONE内のBRANCHESを削除し、10km以内およびCOASTAL\_ZONE外のBRACNCHESのみを残します。

## さらに学ぶ

*   \[空間プロダクトポータル\] (https://oracle.com/goto/spatial)
*   [空間文書化](https://docs.oracle.com/en/database/oracle/oracle-database/19/spatl)
*   [Spatialのブログ](https://blogs.oracle.com/oraclespatial/)

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - Kamryn Vinson、2020年11月