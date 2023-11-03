# 概要

## このワークショップについて

このワークショップでは、OCI Cloud MarketplaceからSpatial StudioをOracle Cloudにプロビジョニングし、Spatial Studioのメタデータ・リポジトリとして使用するスキーマをAutonomous Databaseに準備します。

推定ワークショップ時間:60分

### Oracle Spatial Studioについて

Oracle Spatial Studio (Spatial Studio)は、Oracle Databaseの空間機能へのセルフサービス・アクセスを提供するWebアプリケーションです。これらの機能にはこれまでサード・パーティ・ツールのコーディングや使用が求められてきましたが、Spatial Studioを使用すると、ビジネス・ユーザーはセルフサービスGUIを使用して空間分析や対話型Webマップを作成および共有できます。

![イメージ代替テキスト](./images/spatial-studio.png "空間スタジオ")

Spatial Studioは、Oracle Databaseの空間データ(Oracleのジオメトリ・データ型を含む表およびビュー)を操作します。このデータは、既存の空間データまたは非空間データであり、Spatial Studioを使用して属性に基づいてジオメトリを追加します。

Spatial Studioは、Oracle Cloud MarketplaceからOracle CloudにデプロイできるJava EEアプリケーションです。Spatial Studioは、Oracle WebLogicまたはJettyに手動でデプロイすることも、テスト用の自己完結型の事前デプロイ済クイック・スタートとしてデプロイすることもできます。

詳細については、\[https://oracle.com/goto/spatialstudio\] (https://oracle.com/goto/spatialstudio)をご覧ください。

### 目標

*   Spatial Studioのメタデータ・リポジトリのデータベース・スキーマを作成して割り当てる方法を学習します
*   Cloud Marketplaceを使用してSpatial Studioをインストールする方法を学習します
*   必要なくなったときにSpatial Studioをアンインストールする方法を学習します

### 前提条件

*   このワークショップには、Oracle Autonomous Databaseが必要です。
*   SQL Developer WebはAutonomous Databaseで提供され、Spatial Studioリポジトリ・スキーマの作成にも使用されます。
*   これらにすでにアクセスできる場合は、この概要に従って演習3にスキップできます。
*   そうでない場合は、演習1に進む必要があります。
*   Oracle Spatialに関する経験は必要ありません。
*   Oracle Cloudアカウント- このワークショップのLiveLabsランディング・ページを参照して、サポートされている環境を確認してください

_ノート: **無料トライアル**・アカウントがある場合、無料トライアルの期限が切れると、アカウントは**Always Free**アカウントに変換されます。Always Free環境が使用可能でないかぎり、Free Tierワークショップは実行できません。**[Free TierのFAQページはここをクリックしてください。](https://www.oracle.com/cloud/free/faq.html)**_

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - Database Product Management、David Lapp、2021年1月