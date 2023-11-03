# Spatial StudioをOracle Cloudにデプロイ

## 概要

この演習では、Always Freeリソースを使用してCloud MarketplaceからSpatial Studioをデプロイします。Cloud Marketplaceは、Spatial StudioとAutonomous Databaseのインストールと構成を行います。作成されたSpatial Studioインスタンスは、このワークショップで使用するために一時的であることを意図しています。

推定ラボ時間: 15分

ラボのクイック・ウォークスルーについては、次のビデオをご覧ください。

[Spatial StudioをOracle Cloudにデプロイ](videohub:1_63orvw8q)

### 目標

この演習では、次のことを行います。

*   Always Freeリソースを使用して、Oracle Cloud MarketplaceからSpatial Studioをデプロイします。

### 前提条件

*   Oracle Cloudアカウント
*   あなたはクラウド・アカウントの管理者です。

## タスク1: コンピュート・リソースの可用性の確認

Spatial Studioデプロイメントを開始する前に、Always Freeコンピュート・シェイプの割当てがある可用性ドメインを確認する必要があります。

1.  **「ガバナンスと管理」→「制限、割当ておよび使用状況」**にナビゲートします。
    
    ![制限および割当て制限の確認](images/quota-01.png)
    
2.  The Scope menu lists availability domains. Select the first availability domain, type **micro** in the Resource menu, and select **Cores for Standard.E2.1.Micro VM Instances**.
    
    ![コンピュート・シェイプの選択](images/quota-02.png)
    
3.  結果リストには、選択した可用性ドメイン内の選択したシェイプのサービス制限(割当て制限)、使用状況および可用性が表示されます。次の例では、選択した可用性ドメインに可用性がありません。
    
    ![選択したコンピュート・シェイプの可用性のチェック](images/quota-03.png)
    
4.  選択した可用性ドメインに割当て制限がない場合は、次の可用性ドメインに変更し、「リソース」メニューに**「マイクロ」**を再度入力して、**「Cores for Standard.E2.1」を選択します。マイクロVMインスタンス**。この場合、2番目の可用性ドメインに割当て制限があります。
    
    ![代替コンピュート・シェイプの可用性をチェック](images/quota-04.png)
    

Cloud MarketplaceからSpatial Studioをインストールするときに選択する必要があるため、ターゲット・コンピュート・シェイプの割当て制限がある可用性ドメインに注意してください。

## タスク2: Cloud MarketplaceからのSpatial Studioのインストール

1.  左上のハンバーガー・アイコンをクリックして、メインのナビゲーション・メニューを開きます。**「マーケットプレイス」**を選択し、**「すべてのアプリケーション」**をクリックします。
    
    ![Oracle MarketPlaceに移動します。](images/mp-01.png)
    
2.  **spatial**を検索し、**Oracle Spatial Studio**アプリケーションをクリックします。
    
    **ノート:**「Oracle Spatial Studio for Roving Edge Infrastructure」ではなく、「Oracle Spatial Studio」を選択してください。
    
    ![アプリケーションOracle Spatial Studioの検索](images/mp-02.png)
    
3.  既存の優先コンパートメントがある場合はそれを選択し、それ以外の場合はデフォルト(ルート)のままにします。条件に同意し、**「スタックの起動」**をクリックします
    
    ![Oracle Spatial Studioのスタックの起動](images/mp-04.png)
    
4.  デフォルトを受け入れて**「次へ」**をクリックします。
    
    ![Oracle Spatial Studioのデプロイメントのパラメータの定義](images/mp-05.png)
    
5.  タスク1で指定した割当て制限を持つ可用性ドメインを選択します。Always Freeシェイプ**VMを選択します。Standard.E2.1。マイクロ**。使用可能なクラウド・クレジットまたは有料アカウントがある場合は、かわりに有料シェイプを選択できます。
    
    ![デプロイメントのその他のパラメータ](images/mp-06.png)
    
    その後、下にスクロールします。
    
6.  デフォルトでは、Spatial StudioはHTTPSアクセスのみを許可し、セキュア・アクセスに追加の構成が必要です。このワークショップでは、機密情報を含まない一時インスタンスをデプロイします。したがって、**「HTTPSのみ」**の選択を解除し、ヘルプ・テキストを読んで、意図した使用方法を理解していることを確認します。Spatial Studioの「管理ユーザー名」に、**admin** (小文字)と入力します。このユーザー名では大文字と小文字が区別されます。
    
    ![Spatial Studio拡張構成](images/mp-07.png)
    
    その後、下にスクロールします。
    
7.  Spatial Studio管理ユーザーのパスワードを入力します。これは、Spatial Studioへのログイン時に使用するパスワードです。
    
    ![Spatial Studio管理ユーザーのパスワード](images/mp-07a.png)
    
    その後、下にスクロールします。
    
8.  「ネットワーキングの構成」で、デフォルトのままにしてネットワークを作成します。次に下にスクロールします。
    
9.  SSHキーを使用すると、インスタンスの再起動やログ・ファイルのチェックなど、管理のためにSpatial Studioサーバーにアクセスできます。この場合、Spatial Studioインスタンスは一時的なもので、このワークショップの期間中に使用します。したがって、管理は必要ありません。したがって、**「SSHキーの追加」**オプションを**選択解除**します。
    

![Oracle Spatial Studioで使用されるコンピュート・インスタンスのSSHキーの追加](images/mp-09.png)

その後、下にスクロールします。

10.  Spatial Studioには、Oracle Databaseへのアクセスが必要です。Always Freeのボックスにチェックマークを入れ、他のデフォルトをそのまま使用して、Autonomous Databaseが作成および構成されるようにします。使用可能なクラウド・クレジットまたは有料アカウントがある場合は、このボックスのチェックマークを外し、かわりに有料構成を選択できます。

![Oracle Spatial Studioでリポジトリとして使用するデータベースの構成](images/mp-11.png)

その後、下にスクロールします。

11.  自律型データベース・サービス・レベルの場合は、**「中」**を選択します。次に、Spatial Studioのメタデータを格納するデータベース・ユーザーのパスワードを入力します。これは、Spatial Studioインスタンスのメタデータの自動構成で使用されます。このワークショップでは、このパスワードを再度使用する必要はありません。次に、**「次へ」**をクリックします。

![Spatial Studioのデプロイ](images/mp-12.png)

12.  ウィザードの「確認」ステップに進みます。下部にスクロールして、**「適用の実行」**が選択されていることを確認します。次に、**「作成」**をクリックします。

![Spatial Studioのデプロイ](images/mp-13.png)

13.  ステータスが「IN PROCESS」から「SUCCEEDED」に変わるまで約5分待ちます。

![Spatial Studioのデプロイ](images/mp-14.png)

ステータスが「SUCCEEDED」になったら、続行する前に、インストール後の自動ステップが完了するまで**さらに5分待ちます**。

## タスク3: Spatial Studioへのログイン

1.  **「アプリケーション情報」**タブをクリックし、**Spatial Studio HTTP URL**のリンクをクリックします。
    
    ![Spatial Studioを起動するURLのフェッチ](images/mp-15.png)
    
2.  ユーザー名 **admin**および上記の手順7で入力したパスワードを使用してログインします。
    
    ![Spatial Studioのログイン・ダイアログ](images/mp-17.png)
    
3.  ログインしたら、左側のメイン・ナビゲーション・パネルのアイコンの上にカーソルを置くと、ツールチップにページ名が表示されます。
    
    ![Spatial Studioスタート・ガイド・ページ](images/mp-19.png)
    
4.  左上にある「ハンバーガー」アイコンをクリックして、メイン・ナビゲーション・パネルを展開および縮小することもできます。
    
    ![Spatial Studioのナビゲーション・ペイン](images/mp-20.png)
    

これで、ログインし、Spatial Studioの使用を開始する準備ができました。

**次の演習に進む**ことができます。

## さらに学ぶ

*   [Oracle Spatial製品ページ](https://www.oracle.com/database/spatial)
*   [Spatial Studioの開始](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Spatial Studioのドキュメント](https://docs.oracle.com/en/database/oracle/spatial-studio)

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **貢献者** - Jesus Vizcarra
*   **最終更新者/日付** - David Lapp、2023年8月