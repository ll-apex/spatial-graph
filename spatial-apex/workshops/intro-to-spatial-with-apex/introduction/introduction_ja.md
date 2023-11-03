# 概要

## このワークショップについて

このワークショップでは、マップ・リージョン機能およびOracle Spatialを使用したOracle APEXでのマッピングを確認します。多数の便利なマッピング例を含む事前構築済のサンプル・アプリケーションをインストールして確認します。次に、ウィザードと最初から両方のマップを使用して独自のアプリケーションを作成し、マップを構成します。

マップ・リージョンは、APEX 21.1で導入されたネイティブAPEX機能であり、Oracle Spatial、GeoJSONおよび座標からの空間データを表示する対話型マップを構成する機能を提供します。このワークショップでは、Oracle Spatialを空間データ・ソースとして使用することに重点を置いており、生の空間データと空間分析結果の両方を簡単に組み込むことができます。

![サンプルマップアプリケーション](./images/intro-01.png "Oracle Application Express - サンプル・マップ・アプリケーション ")

推定ワークショップ時間:1時間15分

### Oracle Application Express (APEX)およびOracle Spatialについて

Oracle Application Express (APEX)およびOracle Spatialは、Autonomous Data Warehouse (ADW)やAutonomous Transaction Processing (ATP)サービスなど、Oracle Databaseの機能です。

Oracle Application Express (APEX)は、最高レベルの機能を備え、どこにでもデプロイできるスケーラブルでセキュアなエンタープライズ・アプリケーションを構築できるロー・コード開発プラットフォームです。詳細は、[Oracle APEX製品ホームページ](https://apex.oracle.com)を参照してください

Oracle Spatialは、Oracle Database内の地理空間データ管理、分析および処理機能のセットです。ネイティブな空間データ型と分析操作により、位置ベースの分析は主流であり、他のすべてのデータベース操作と共存します。詳細は、[Oracle Spatial製品ホームページ](https://www.oracle.com/database/spatial)を参照してください。

### 目標

*   APEXマップ・リージョンのサンプルについて
*   マップ・リージョンの作成および構成の学習
*   Oracle Spatialにロケーション分析を組み込む方法を学ぶ

### 前提条件

*   Oracle APEX 21.1以上が必要です。このワークショップのスクリーンショットは、APEX 21.2を使用して撮影されます。通常、[最新バージョンのAPEX](https://www.oracle.com/tools/downloads/apex-downloads/)を使用することをお薦めしますので、ユーザー・インタフェースにわずかな違いが生じることがあります。
*   Oracle APEXに関する基本的な経験をお薦めしますが、必須ではありません。必要に応じて、[Oracle Autonomous Cloud Serviceの既存の表に基づくアプリケーションの作成](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628)というLiveLabs APEXワークショップの概要を確認してください。
*   Oracle Spatialに関する基本的な経験をお薦めしますが、必須ではありません。必要に応じて、[Oracle Spatialの概要](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736)のLiveLabs Spatialの概要ワークショップを確認してください。

_ノート: **無料トライアル**・アカウントがある場合、無料トライアルの期限が切れると、アカウントは**Always Free**アカウントに変換されます。Always Free環境が使用可能でないかぎり、Free Tierワークショップは実行できません。**[Free TierのFAQページはここをクリックしてください。](https://www.oracle.com/cloud/free/faq.html)**_

## 謝辞

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **コントリビュータ** - Jayson Hanes、APEX製品管理、Oracle
*   **最終更新者/日付** - David Lapp、2023年3月