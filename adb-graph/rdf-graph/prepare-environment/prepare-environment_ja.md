# 環境の準備

## 概要

Oracle Autonomous Transaction Processing (ATP)は、Oracle Cloud Infrastructure (OCI)に「自動運転」機能を備えたフルマネージドのOracleデータベース・サービスです。Graph Studioを使用する権限を持つユーザーを作成することをお薦めします。

次の演習ガイドでは、ATPをプロビジョニングし、Graph Studioの権限を持つユーザーを作成する方法を示します。

見積時間: 15分

### 目標

*   Oracle CloudにAutonomous Databaseを作成します。

### 前提条件

*   Webブラウザ
*   常に正しいリージョンおよびコンパートメントにあることを確認してください

## **タスク1:** Oracle Cloudへのログイン

1.  ブラウザからOracle Cloudにログインします。

## **タスク2:** ATPのプロビジョニング

次のステップでAutonomous Transaction Processingデータベース(ATP)をプロビジョニングします。または、Autonomous Data Warehouse (ADW)も同様に使用できます。

1.  OCIコンソールの右上から、割り当てられたリージョンを選択します。
    
2.  ハンバーガー・メニュー(左上)から、「Oracle Database」、「Autonomous Transaction Processing」の順に選択します。
    

![Autonomous Transaction Processingにアクセスするために選択するメニュー内の場所を示す図](./images/atp.png)

3.  「Autonomous Databaseの作成」をクリックします。

![自律型データベースを作成するためのボタンを示す図](./images/create-adb.png)

4.  コンパートメントを選択します。
    
5.  表示およびデータベース名の一意の名前(場合によっては自分の名前)を入力します。表示名は、コンソールUIでデータベースの識別に使用されます。
    

![データベースの一意の名前を入力する場所を示す図](./images/unique-name.png)

6.  「トランザクション処理」ワークロード・タイプが選択されていることを確認します。
    
7.  パスワードを入力します。ユーザー名は常にADMINです。(ノート: パスワードを覚えておいてください)
    

![パスワードを宣言する場所を示す図](./images/password.png)

8.  下部にある「Autonomous Databaseの作成」をクリックします。
    
    ATPがプロビジョニングされていることがコンソールに表示されます。完了には約2、3分かかります。
    
    作業リクエストでプロビジョニングのステータスを確認できます。
    

![プロビジョニングされたデータベースのステータスをチェックする場所を示す図](./images/status.png)

これで、このラボは終了です。_次の演習に進むことができます。_

## 確認

*   **著者** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **貢献者** - Nicholas Cusato (Santa Monica Specialist Hub)
*   **最終更新者/日付** - Nicholas Cusato、2022年2月