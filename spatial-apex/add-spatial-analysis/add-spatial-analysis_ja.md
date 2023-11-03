# 空間分析の組込み

## 概要

この演習では、空間分析を組み込むことで、前の演習のマップを拡張します。選択した状態のユーザー定義の距離内にある空港の検索を設定します。

推定ラボ時間: 30分

### 目標

*   基本的な空間分析操作の理解
*   APEXマップ・リージョンへの空間分析の統合の理解

### 前提条件

*   演習3: マップを最初から作成

## タスク1: フィルタのリージョンの追加

1.  左側のツリーの上部にある**ページ3: 空港と州マップ**をクリックします。次に、右側の「ページ」プロパティ・パネルの「外観」で、ページ・テンプレートを**「左側の列」**に変更します。
    
    ![ページ・テンプレートの更新](images/add-spatial-analysis-01a.png)
    
    次に、レイアウトに**LEFT COLUMN**が表示されます。
    
    ![ページ・テンプレートの更新](images/add-spatial-analysis-01b.png)
    
2.  「静的コンテンツ」リージョンを左の列にドラッグします。
    
    ![静的コンテンツ・リージョンの追加](images/add-spatial-analysis-01c.png)
    
3.  **「自分のフィルタ」リージョン**または選択した名前に変更します。
    
    ![リージョン名の変更](images/add-spatial-analysis-02.png)
    

## タスク2: 状態選択用の項目の追加

1.  「選択リスト」項目をフィルタ・リージョンにドラッグし、名前を**P3\_STATE**に更新します。
    
    ![選択リスト・アイテムの追加](images/add-spatial-analysis-03.png)
    
2.  右側の「Page Item(ページ項目)」プロパティで、「List of Values(値リスト)」のセクションまで下にスクロールします。スイッチを使用して**「必要な値」**を有効にし、「タイプ」を**「SQL問合せ」**に設定して、次の問合せを入力します。
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT問合せ](images/add-spatial-analysis-04.png)
    
3.  右側の「ページ・アイテム」プロパティで、「デフォルト」のセクションまで下にスクロールします。「タイプ」を**「静的」**に、値を**「テキサス」**または選択した別の状態(一重引用符)に設定します。
    
    ![選択リストの構成](images/add-spatial-analysis-05.png)
    

## タスク3: 距離入力用のアイテムの追加

1.  「Number Field(数値フィールド)」をフィルタ・リージョンにドラッグします。名前を **P3\_DISTANCE**に、ラベルを **Proximity (km)**に更新します。
    
    ![数値フィールド・アイテムを追加](images/add-spatial-analysis-06.png)
    
2.  右側の「ページ・アイテム」プロパティで、「検証」セクションまで下にスクロールし、**「必要な値」**を有効にします。
    
    ![検証を値必須に設定](images/add-spatial-analysis-07.png)
    
3.  「Default(デフォルト)」セクションまで下にスクロールします。「タイプ」を**「静的」**に設定し、値を**100**に設定します。
    
    ![デフォルト値の設定](images/add-spatial-analysis-08.png)
    
    これで、州に近接して空港をフィルタリングするための入力ができました。次に、動的アクションを使用してフィルタを適用します。
    

## タスク4: 動的アクションを使用したフィルタの適用

次に、ユーザーが状態または距離の値(あるいはその両方)を変更したときに起動されるアクションを作成します。

1.  P3\_STATEまたはP3\_DISTANCEアイテムを右クリックし、**「動的アクションの作成」**を選択します(作成したアクションは両方のアイテムに適用されます)。
    
    ![動的アクションの作成](images/add-spatial-analysis-09.png)
    
2.  右側の「動的アクション」プロパティで、「名前」を**「検証およびリフレッシュ」**に設定します。「時期」セクションで、「イベント」を**「変更」**、「選択タイプ」を**「項目」**に設定し、項目をカンマ区切りリスト**P3\_DISTANCE、P3\_STATE**に設定します。「品目」テキスト・ボックスの右側にあるボタンを使用すると、リストから品目を選択できます。距離に負の値を送信しないようにするには、「クライアント側条件」セクションで、「タイプ」を**「アイテム>= 値」**、「アイテム」を**P3\_DISTANCE**、「値」を**0**に設定します。
    
    ![動的アクションの構成](images/add-spatial-analysis-10.png)
    
3.  動的アクションは、構成済の条件に基づいて起動されるTRUEアクションおよびFALSEアクションで構成されます。この場合、クライアント側の条件(P3\_DISTANCE >= 0)は、TRUEアクション(条件が満たされる)またはFALSEアクション(条件が満たされない)のどちらを起動するかを決定します。これにより、負の距離入力をトラップできます。
    
    クライアント側の条件がTRUEの場合、アクションは入力パラメータを発行してページをリフレッシュする必要があります。「TRUE」の下のアクションをクリックします。右側の「アクション」プロパティの「識別」で、「アクション」を**「リフレッシュ」**に設定します。「影響を受ける要素」で、「選択タイプ」を**「リージョン」**に設定し、「リージョン」を**「マイ・マップ・リージョン」**(または、異なる場合は使用した名前)に設定します。左側のページ・ツリーで、「TRUE」アクションが「リフレッシュ」に変わることを確認します。
    
    ![動的アクションの構成](images/add-spatial-analysis-11.png)
    
4.  次に、クライアント側の条件が満たされない(負の距離値が入力された)場合に起動するアクションを構成します。いずれかの項目の「動的アクション」で、「FALSE」を右クリックし、**「FALSEアクションの作成」**を選択します。
    
    ![動的アクションの構成](images/add-spatial-analysis-12.png)
    
5.  距離が負の場合に起動されるFALSEアクションは、ユーザーへのポップアップ・メッセージになります。「FALSE」アクションをクリックします。右側の「アクション」プロパティの「識別」で、「アクション」を**「アラート」**に設定します。「設定」で、「タイトル」を**「無効な距離」**(これはアラート・バナーになります)に設定し、「メッセージ」を**「距離」を0以上にする必要があります**(これはアラート本文になります)。左側のページ・ツリーで、「FALSE」アクションが「アラート」に変わることを確認します。
    
    ![動的アクションの構成](images/add-spatial-analysis-13.png)
    
6.  マップ・リージョンには現在、すべての状態を表示する状態レイヤーが含まれています。ここで、このレイヤーを調整して、P3\_STATEメニューから選択した状態のみを表示します。左側のページ・ツリーで、「レイヤー」の下の「状態」をクリックします。右側の「レイヤー」プロパティの「識別」で、「名前」を**「選択した状態」**に変更します。「ソース」で、Where句を**state\_code = :P3\_STATE**に設定します。左側のページ・ツリーで、レイヤー名が「Selected State」に変わることを確認します。
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![WHERE句の構成](images/add-spatial-analysis-14.png)
    
7.  最後に、Airportsレイヤーを更新して、ユーザーが指定した状態および近接度でフィルタされたアイテムを返します。左側の「ページ」ツリーで、「空港」レイヤーをクリックします。右側の「レイヤー」プロパティの「ソース」で、「タイプ」を**「SQL問合せ」**に変更します。SQL問合せの場合、Oracle DatabaseのネイティブSQLの"within distance"演算子を使用する次のように入力します。
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    「発行するページ・アイテム」に、カンマ区切りリスト**P3\_STATE、P3\_DISTANCE**を入力します。
    
    ![空間SQL問合せ](images/add-spatial-analysis-15.png)
    
8.  ページを表示する準備ができました。**「保存」**をクリックし、右上にある緑色の**「実行」**ボタンをクリックします。ページがレンダリングされたら、状態に対して**「Alabama」**を選択します。マップには、選択した州と空港が100km (デフォルトの距離)以内で表示されます。
    
    ![ページの保存と実行](images/add-spatial-analysis-16.png)
    
9.  選択した状態を**「カンザス」**に変更します。マップに、選択した州と100kmの空港が表示されるようになったことを確認します。
    
    ![カンザスの選択](images/add-spatial-analysis-17.png)
    
10.  距離を600kmに増やし、\[Enter\]または\[Tab\]をクリックして送信します。マップに、より大きな距離内に追加の空港が表示されるようになったことを確認します。
    
    ![距離を600kmに増やす](images/add-spatial-analysis-18.png)
    
11.  最後に、負の距離を送信すると、前に構成した「エラー」ポップアップになることを確認します。
    
    ![マイナスの距離アラート](images/add-spatial-analysis-19.png)
    
    このワークショップの最初にインストールしたサンプル・マップ・アプリケーションに示すように、Map RegionsおよびSpatialで実現できる、非常に多くの機能が追加されています。このワークショップでは基本を紹介し、関心が寄せられ、APEXアプリケーションでマップと空間分析の力を活用できることを期待しています。
    

## さらに学ぶ

*   [『Oracle Spatial』](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## 確認

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - Database Product Management、David Lapp、2023年3月