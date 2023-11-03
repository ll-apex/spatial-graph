# Autonomous Database共有Free Tierインスタンスのプロビジョニング

## 概要

このラボでは、Oracle CloudでOracle Autonomous Database (Autonomous Data Warehouse \[ADW\]およびAutonomous Transaction Processing \[ATP\])の使用を開始するステップについて説明します。クラウド・コンソールを使用して新しいATPインスタンスをプロビジョニングします。

_Note1: この演習ではATPを使用しますが、ステップはADWデータベースの作成と接続と同じです。_

_Note2: Always Free自律型データベースを作成する場合、Always Freeリソースが使用可能なリージョンに存在する必要があります。(すべてのリージョンにAlways Freeリソースがあるわけではありません)_

予想時間: 5分

Autonomous Transaction Processingでの自律型データベースのプロビジョニングに関するビデオ・デモ(Autonomous Data Warehouseでの自律型データベースのプロビジョニングには、同じステップが適用されます):

[YouTube](youtube:Q6hxMaAPghI)

### 目標

*   新しい無料層Autonomous Transaction Processingインスタンスをプロビジョニングする方法を学習します

### 前提条件

*   [Oracle Cloudアカウント](https://www.oracle.com/cloud/free/)。独自のクラウド・アカウント、トライアルで取得したクラウド・アカウント、Free Tierアカウント、またはOracleインストラクタから詳細が与えられたトレーニング・アカウントを使用できます。

## タスク1: 「サービス」メニューからのATPの選択

1.  Oracle Cloudにログインします。
    
2.  ログインすると、使用可能なすべてのサービスを表示するクラウド・サービス・ダッシュボードが表示されます。左上のナビゲーション・メニューをクリックすると、最上位レベルのナビゲーション選択肢が表示されます。
    
    **ノート:**ダッシュボードの**「クイック・アクション」**セクションで、Autonomous Data WarehouseまたはAutonomous Transaction Processingサービスに直接アクセスすることもできます。
    
    ![OCIコンソール](images/oci-console.png)
    
3.  次のステップは、Autonomous Data WarehouseまたはAutonomous Transaction Processingと同様に適用されます。このラボでは、Autonomous Transaction Processing (ATP)データベースのプロビジョニングを示します。左上の**「ナビゲーション・メニュー」**をクリックし、**「Oracle Database」**に移動して**「Autonomous Transaction Processing」**を選択します。
    
    ![ATPの選択](https://oracle-livelabs.github.io/common/images/console/database-atp.png)
    
4.  Autonomous Transaction Processingインスタンスを表示するには、ワークロード・タイプが**「トランザクション処理」**または**「すべて」**であることを確認します。**「リスト範囲」**ドロップダウン・メニューを使用して、コンパートメントを選択できます。新しいATPインスタンスを作成する**ルート・コンパートメント**または**任意の別のコンパートメント**を選択します。新しいコンパートメントを作成するか、コンパートメントについてさらに学習する場合は、[ここ](https://docs.cloud.oracle.com/iaas/Content/Identity/Tasks/managingcompartments.htm#three)をクリックしてください。
    
    _**ノート** - ManagedCompartmentforPaaSコンパートメントはOracle Platform Servicesに使用されるOracleのデフォルトであるため、使用しないでください。_
    

## タスク2: ADBインスタンスの作成

1.  **「Autonomous Databaseの作成」**をクリックして、インスタンス作成プロセスを開始します。
    
    ![ADBの作成](images/create-adb.png)
    
2.  これにより、インスタンスの構成を指定する**「Autonomous Databaseの作成」**画面が表示されます。
    
3.  Autonomous Databaseの基本情報の指定:
    
    *   **コンパートメント** - ドロップダウン・リストからデータベースのコンパートメントを選択します。
    *   **表示名** - 表示用に、覚えやすい名前を入力します。このラボでは、**ATPグラフ**を使用します。
    *   **データベース名** - 文字で始まる文字と数字のみを使用します。最大長は14文字です。(アンダースコアは当初サポートされていません。)この演習では、**ATPGRAPH**を使用します。
4.  ワークロード・タイプを選択します。選択肢からデータベースのワークロード・タイプを選択します:
    
    *   **トランザクション処理** - この演習では、ワークロード・タイプとして**「トランザクション処理」**を選択します。
    *   **データ・ウェアハウス** - または、ワークロード・タイプとしてデータ・ウェアハウスを選択することもできます。
    
    ![ワークロード・タイプ](images/workload-type.png)
    
5.  デプロイメント・タイプを選択します。選択肢からデータベースのデプロイメント・タイプを選択します。
    
    *   **共有インフラストラクチャ** - この演習では、デプロイメント・タイプとして**「共有インフラストラクチャ」**を選択します。
    *   **専用インフラストラクチャ** - または、ワークロード・タイプとして専用インフラストラクチャを選択することもできます。
    
    ![デプロイメント・タイプ](images/deployment-type.png)
    
6.  データベースを構成し、**「Always Free」**オプションを選択します:
    
    *   **Always Free** - この演習では、このオプションを選択して常に無料の自律型データベースを作成するか、このオプションを選択して有料サブスクリプションを使用してデータベースを作成しないようにできます。Always Freeデータベースには、1つのCPUと20 GBのストレージが付属しています。Always Freeを選択すると、このラボでは十分です。
    *   **データベース・バージョンの選択** - 使用可能なバージョン(`19c`または`21c`)からデータベースのバージョンを選択します。
    *   **OCPU数** - CPUの数。
    *   **自動スケーリング** - この演習では、自動スケーリングを**無効**のままにします。
    *   **ストレージ(TB)** - ストレージ容量(TB)。
    *   **新規データベース・プレビュー** - 新しいデータベース・バージョンをプレビューするためのチェック・ボックスが使用可能な場合は、選択**しない**でください。
    
    ![CPUおよびストレージの選択](images/atp-choose-cpu-storage.png)
    
7.  管理者資格証明の作成:
    
    *   **パスワードおよびパスワードの確認** - サービス・インスタンスのADMINユーザーのパスワードを指定します。パスワードは、次の要件を満たす必要があります。
    *   パスワードの長さは12から30文字とし、大文字、小文字および数字をそれぞれ1文字以上含める必要があります。
    *   パスワードにユーザー名を含めることはできません。
    *   パスワードに二重引用符(")を含めることはできません。
    *   パスワードは、過去4回に使用したパスワードとは異なる必要があります。
    *   パスワードは、設定してから24時間経過していないパスワードと同じにできません。
    *   確認用にパスワードを再入力します。このパスワードをノートにとります。
    
    ![パスワード](images/password.png)
    
8.  ネットワーク・アクセスの選択:
    
    *   この演習では、デフォルトの「Secure access from everywhere」を受け入れます。
    *   プライベート・エンドポイントで、指定したVCNからのトラフィックのみを許可する場合(すべてのパブリックIPまたはVCNからのデータベースへのアクセスがブロックされている場合)、ネットワーク・アクセスの選択領域で「仮想クラウド・ネットワーク」を選択します。
    *   ネットワーク・アクセス制御リスト(ACL)を設定することで、Autonomous Databaseへのアクセスを制御および制限できます。IPアドレス、CIDRブロック、Virtual Cloud Network、Virtual Cloud Network OCIDの4つのIP表記タイプから選択できます。
    
    ![ネットワーク・アクセス](images/network-access.png)
    
9.  ライセンス・タイプを選択します。この演習では、**「含まれるライセンス」**を選択します。次の2つのライセンス・タイプがあります。
    
    *   **Bring Your Own License (BYOL)** - 組織に既存のデータベース・ライセンスがある場合、このタイプを選択します。
    *   **含まれるライセンス** - 新しいデータベース・ソフトウェア・ライセンスおよびデータベース・クラウド・サービスにサブスクライブする場合に、このタイプを選択します。
10.  **「Autonomous Databaseの作成」**をクリックします。
    
    ![ライセンス](images/license.png)
    
11.  インスタンスのプロビジョニングが開始されます。数分後、状態は「プロビジョニング中」から「使用可能」に変わります。この時点で、Autonomous Transaction Processingデータベースを使用する準備ができました。名前、データベース・バージョン、OCPU数、ストレージ・サイズなど、インスタンスの詳細をここで確認します。![ステータス・プロビジョニング](images/atp-graph-provisioning.png) ![使用可能なステータス](images/atp-graph-available.png)
    

次の演習に進むことができます。

## 詳細

Autonomous Data Warehouseを使用するための標準的なワークフローに関するドキュメンテーションについては、[ここ](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)をクリックしてください。

## 謝辞

*   **作成者** - Nilay Panchal
*   **Adapted for Cloud by** - Richard Green
*   **最終更新者/日付** - 山中亮太、2023年3月
*   **作成者** - Nilay Panchal
*   **Adapted for Cloud by** - Richard Green
*   **最終更新者/日付** - 山中亮太、2023年3月