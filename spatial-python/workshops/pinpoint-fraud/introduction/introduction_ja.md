# 概要

## このワークショップについて

このワークショップでは、場所と時間(spatiotemporal)に関する分析に基づいて、疑わしい財務取引を特定します。Oracle Database (Oracle Spatial)とPythonライブラリの空間機能の両方が使用されます。Oracle Spatialは、近接性、封じ込め、距離、エリアなどの関係と測定に基づいて、バックエンドの大規模ロケーション分析およびエンリッチメントを実行します。Pythonは、Spatiotemporal分析を含む成熟した専門ライブラリの広範なエコシステムを活用して、データ分析と機械学習のための環境を提供します。python-oracledbドライバを使用すると、Oracle Databaseへの接続性と堅牢なアクセスが可能になり、OracleバックエンドとPythonクライアントの両方の長所が最適に活用されます。

推定ワークショップ時間:45分

### Oracle Spatialおよびpython-oracledbについて

Oracle Spatialは、Oracle Database内の地理空間データ管理、分析および処理機能のセットです。ネイティブな空間データ型と分析操作により、位置ベースの分析は主流であり、他のすべてのデータベース操作と共存します。詳細は、[Oracle Spatial製品ホームページ](https://www.oracle.com/database/spatial)を参照してください。

python-oracledbドライバは、プログラムがOracle Databaseにアクセスできるようにするオープン・ソースのPythonモジュールです。python-oracledbを使用すると、PythonからOracle Database (Oracle Autonomous Databaseを含む)に簡単にアクセスでき、大規模なオブジェクト・タイプ、アドバンスト・キューイング、連続問合せ通知などの機能を活用できます。詳細は、[python-oracledb on GitHub](https://oracle.github.io/python-oracledb/)を参照してください。

### 目標

*   Python環境およびAutonomous Databaseの作成
*   PythonからAutonomous Databaseへの接続の確立
*   Autonomous Databaseでの財務トランザクション・データの準備
*   Pythonで財務取引データを調査し、疑わしい取引を特定

### 前提条件

*   SQLとPythonの経験は役に立ちますが、必須ではありません

## 確認

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **コントリビュータ** - Rahul Tasker、Denise Myrick、Ramu Gutierrez
*   **最終更新者/日付** - David Lapp、2023年8月