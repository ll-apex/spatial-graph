/\*次のリリースでこのファイルを削除してください- ADB-PROVISION-CONDITIONAL.MDファイルをインストールし、マニュアルで必要なバージョンを指定してください: { "タイトル": "ラボ1: ADBインスタンスのプロビジョニング"、 "説明": "Autonomous Databaseインスタンスのプロビジョニング"、 "タイプ": "livelabs"、 "ファイル名": "https://oracle-livelabs.github.io/ADB/shared/ADB-provision/ADB-provision-conditional.MD" }、 \*/

# Autonomous Database (ADWおよびATP)のプロビジョニング

## 概要

このラボでは、Oracle CloudでOracle Autonomous Database (Autonomous Data Warehouse \[ADW\]およびAutonomous Transaction Processing \[ATP\])の使用を開始するステップについて説明します。この演習では、新しいADWインスタンスをプロビジョニングします。

> **ノート:**この演習ではADWを使用しますが、ステップはATPデータベースの作成と同じです。

予想時間: 5分

### 目標

*   新しいAutonomous Databaseのプロビジョニング方法の学習

## タスク1: 「サービス」メニューからのADWまたはATPの選択

1.  Oracle Cloudにログインします。
    
2.  ログインすると、使用可能なすべてのサービスを表示するクラウド・サービス・ダッシュボードが表示されます。左上のナビゲーション・メニューをクリックすると、最上位レベルのナビゲーション選択肢が表示されます。
    
    > **ノート:**ダッシュボードの**「クイック・アクション」**セクションで、Autonomous Data WarehouseまたはAutonomous Transaction Processingサービスに直接アクセスすることもできます。
    
    ![Oracleホーム・ページ。](./images/Picture100-36.png " ")
    
3.  次のステップは、Autonomous Data WarehouseまたはAutonomous Transaction Processingと同様に適用されます。このラボでは、Autonomous Data Warehouseデータベースのプロビジョニングを表示するため、**「Autonomous Data Warehouse」**をクリックします。
    
    ![「Autonomous Data Warehouse」をクリックします。](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Autonomous Data Warehouseインスタンスを表示するには、ワークロード・タイプが**「データ・ウェアハウス」**または**「すべて」**であることを確認します。**「リスト範囲」**ドロップダウン・メニューを使用して、コンパートメントを選択します。ユーザー名の最初の部分(たとえば、「コンパートメントの検索」フィールドに`LL185`)を入力して、コンパートメントをすばやく検索します。
    
    ![左側のワークロード・タイプを確認します。](images/livelabs-compartment.png " ")
    
5.  このコンソールには、まだデータベースが存在しないことが示されます。データベースのリストが長い場合は、データベースの**状態**(使用可能、停止、終了など)でリストをフィルタできます。**「ワークロード・タイプ」**でソートすることもできます。ここでは、**「データ・ウェアハウス」**ワークロード・タイプが選択されています。
    
    ![Autonomous Databasesコンソール。](./images/Compartment.png " ")
    

## タスク2: ADBインスタンスの作成

1.  **「Autonomous Databaseの作成」**をクリックして、インスタンス作成プロセスを開始します。
    
    ![「Autonomous Databaseの作成」をクリックします。](./images/Picture100-23.png " ")
    
2.  これにより、インスタンスの構成を指定する**「Autonomous Databaseの作成」**画面が表示されます。
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  自律型データベースの基本情報の指定:
    
    *   **コンパートメントの選択** - デフォルトのコンパートメントのままにします。
    *   **表示名** - 表示用に、覚えやすい名前を入力します。この演習では、**ADW Finance Mart**を使用します。
    *   **データベース名** - 文字で始まる文字と数字のみを使用します。最大長は14文字です。(アンダースコアは当初サポートされていません。)この演習では、**ADWFINANCE**および**ユーザーIDを追加**します。たとえば、ユーザーIDが**LL-185**の場合は、**ADWFINANCE185と入力します。**
    
    ![必要な詳細を入力します。](./images/Picture100-26-livelabs.png " ")
    
4.  ワークロード・タイプを選択します。選択肢からデータベースのワークロード・タイプを選択します:
    
    *   **データ・ウェアハウス** - このラボでは、ワークロード・タイプとして**「データ・ウェアハウス」**を選択します。
    *   **トランザクション処理** - または、「トランザクション処理」をワークロード・タイプとして選択できます。
    
    ![ワークロード・タイプを選択します。](./images/Picture100-26b.png " ")
    
5.  デプロイメント・タイプを選択します。選択肢からデータベースのデプロイメント・タイプを選択します。
    
    *   **共有インフラストラクチャ** - この演習では、デプロイメント・タイプとして**「共有インフラストラクチャ」**を選択します。
    *   **専用インフラストラクチャ** - または、デプロイメント・タイプとして「専用インフラストラクチャ」を選択することもできます。
    
    ![デプロイメント・タイプの選択](./images/Picture100-26_deployment_type.png " ")
    
6.  データベースを構成します。
    
    *   **Always Free** - クラウド・アカウントがAlways Freeアカウントの場合は、このオプションを選択してAlways Free自律型データベースを作成できます。Always Freeデータベースには、1つのCPUと20 GBのストレージが付属しています。この演習では、Always Freeの選択を解除しておくことをお薦めします。
    *   **データベース・バージョンの選択** - 使用可能なバージョンからデータベースのバージョンを選択します。
    *   **OCPU数** - サービスのCPU数。このラボでは、**1 CPU**を指定します。Always Freeデータベースを選択した場合は、1つのCPUが付属しています。
    *   **ストレージ(TB)** - ストレージ容量をTBを選択します。このラボでは、**1TB**のストレージを指定します。または、Always Freeデータベースを選択した場合は、20 GBのストレージが付属しています。
    *   **自動スケーリング** - このラボでは、自動スケーリングを有効にしたままにして、最大3倍のCPUおよびIOリソースを自動的に使用してワークロードの要求に対応します。
    *   **新規データベース・プレビュー** - 新しいデータベース・バージョンをプレビューするためのチェック・ボックスが使用可能な場合は、選択しないでください。
    
    > **ノート:** Always Free自律型データベースはスケール・アップ/スケール・ダウンできません。
    
    ![残りのパラメータを選択します。](./images/Picture100-26c.png " ")
    
7.  管理者資格証明の作成:
    
    *   **パスワードおよびパスワードの確認** - サービス・インスタンスのADMINユーザーのパスワードを指定します。パスワードは、次の要件を満たす必要があります。
    *   パスワードの長さは12から30文字とし、大文字、小文字および数字をそれぞれ1文字以上含める必要があります。
    *   パスワードにユーザー名を含めることはできません。
    *   パスワードに二重引用符(")を含めることはできません。
    *   パスワードは、過去4回に使用したパスワードとは異なる必要があります。
    *   パスワードは、設定してから24時間経過していないパスワードと同じにできません。
    *   確認用にパスワードを再入力します。このパスワードをノートにとります。
    
    ![パスワードを入力し、パスワードを確認します。](./images/Picture100-26d.png " ")
    
8.  ネットワーク・アクセスの選択:
    
    *   この演習では、デフォルトの「Secure access from everywhere」を受け入れます。
    *   指定したIPアドレスおよびVCNからのトラフィックのみを許可する場合(すべてのパブリックIPまたはVCNからのデータベースへのアクセスがブロックされている場合)、ネットワーク・アクセスの選択領域で「許可されたIPおよびVCNからのセキュア・アクセスのみ」を選択します。
    *   OCI VCN内のプライベート・エンドポイントへのアクセスを制限する場合は、「ネットワーク・アクセスの選択」領域で「プライベート・エンドポイント・アクセスのみ」を選択します。
    *   「相互TLS (mTLS)認証が必要」オプションを選択した場合は、Autonomous Databaseへの接続を認証するためにmTLSが必要になります。JDK8以上のJDBCシン・ドライバを使用している場合、TLS接続を使用すると、ウォレットなしでAutonomous Databaseに接続できます。TLSを許可するオプション、または相互TLS (mTLS)認証のみを必要とするオプションは、[ネットワーク・オプションのドキュメント](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5)を参照してください。
    
    ![ネットワーク・アクセスを選択します。](./images/Picture100-26e.png " ")
    
9.  ライセンス・タイプを選択します。この演習では、**「Bring Your Own License (BYOL)」**を選択します。2つのライセンス・タイプは次のとおりです。
    
    *   **Bring Your Own License (BYOL)** - 組織に既存のデータベース・ライセンスがある場合、このタイプを選択します。
    *   **含まれるライセンス** - 新しいデータベース・ソフトウェア・ライセンスおよびデータベース・クラウド・サービスにサブスクライブする場合に、このタイプを選択します。
    
    ![「Autonomous Databaseの作成」をクリックします。](./images/Picture100-27-byol.png " ")
    
10.  この演習では、連絡先のEメール・アドレスを指定しないでください。「連絡先の電子メール」フィールドを使用すると、連絡先をリストして、運用上の通知やお知らせ、および計画外のメンテナンス通知を受信できます。
    
    ![連絡先電子メール・アドレスは指定しないでください。](images/contact-email-field.png)
    
11.  **「Autonomous Databaseの作成」**をクリックします。
    
12.  インスタンスのプロビジョニングが開始されます。数分後、状態は「プロビジョニング中」から「使用可能」に変わります。この時点で、Autonomous Data Warehouseデータベースを使用する準備ができました。名前、データベース・バージョン、OCPU数、ストレージ・サイズなど、インスタンスの詳細をここで確認します。
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

_次の演習に進んでください_。

## 詳細

Autonomous Data Warehouseを使用するための標準的なワークフローに関するドキュメンテーションについては、[ここ](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)をクリックしてください。

## 謝辞

*   **著者** - Nilay Panchal氏、ADB製品管理
*   **クラウドに適応** - Richard Green、データベース・ユーザー・アシスタンス担当プリンシパル開発者
*   **貢献者** - Oracle LiveLabs QAチーム(Jeffrey Malcolm Jr、Intern | Arabella Yao、Product Manager Intern)
*   **最終更新者/日付** - Richard Green、2022年2月