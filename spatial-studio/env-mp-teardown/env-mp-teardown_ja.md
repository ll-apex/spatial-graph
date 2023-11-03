# クリーンアップ

## 概要

この演習では、Cloud Marketplaceを使用して作成したSpatial Studioインスタンスをアンデプロイします。Spatial Studioデプロイメントの一部として作成されたすべてのリソースをCloud Marketplaceから完全にパージします。

推定ラボ時間: 5分

ラボのクイック・ウォークスルーについては、次のビデオをご覧ください。

[クリーンアップ・オプション2: Spatial StudioおよびADBの終了](videohub:1_1jnminp7)

### 目標

この演習では、次のことを行います。

*   Oracle Cloud Marketplaceから作成されたSpatial Studioおよび関連リソースをアンデプロイします。

### 前提条件

*   Cloud MarketplaceからデプロイされたSpatial Studio

## タスク1: デプロイ済リソースのパージ

Spatial Studioインスタンスの作成に使用するスタックに移動します。

1.  **「開発者サービス」→「スタック」**にナビゲートします。
    
    ![OCIコンソールでのスタックへのナビゲート](images/teardown-01.png)
    
2.  スタックのアクション・メニューから、**「スタック詳細の表示」**を選択します。
    
    ![スタック詳細の表示](images/teardown-02.png)
    
3.  **「破棄」**をクリックします。これにより、Spatial Studio Marketplaceデプロイメントによって作成されたリソースがパージされます。
    
    ![スタックの破棄](images/teardown-03.png)
    
4.  **「破棄」**を再度クリックして確認します。
    
    ![スタックの破棄の確認](images/teardown-04.png)
    
5.  プロセスが完了するまで約3分から4分待ちます。「ジョブ」セクションのステータスを確認します。ステータスが**「成功」**の場合、失業は完了し、Spatial Studio Marketplaceデプロイメントによってプロビジョニングされたすべてのリソースがパージされます。
    
    ![破棄ジョブのチェック](images/teardown-05.png)
    

## タスク2: スタックの削除(オプション)

スタックは、デプロイメントの手順のセットです。Cloud Marketplaceウィザードの実行時に選択した設定が取得されます。これで、スタックを実行してSpatial Studioインスタンスを作成したときに作成されたリソースをパージしたので、スタック自体を削除できます。スタックを削除した後、Spatial Studioを再度デプロイするには、Cloud Marketplaceからやり直す必要があります。また、スタックをそのまま保持して再実行したり、SSHキーの追加などのパラメータを変更して長期インスタンスを作成したりすることもできます。

1.  スタックの**「その他のアクション」**メニューから、**「スタックの削除」**を選択します。
    
    ![「Delete Stack」を選択します。](images/teardown-06.png)
    
2.  確認を求められたら、**「削除」**をクリックします
    
    ![スタックの削除を確認](images/teardown-07.png)
    
3.  クラウド・マーケットプレイス・ウィザードによって作成されたすべてのアーティファクト(リソースとスタックの両方)がなくなりました。
    

## さらに学ぶ

*   [Oracle Spatial製品ページ](https://www.oracle.com/database/spatial)
*   [Spatial Studioの開始](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Spatial Studioのドキュメント](https://docs.oracle.com/en/database/oracle/spatial-studio)

## 確認

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **貢献者** - Jesus Vizcarra
*   **最終更新者/日付** - David Lapp、2023年8月