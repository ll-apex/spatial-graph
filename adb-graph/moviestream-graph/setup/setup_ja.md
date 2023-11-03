# 設定: スタックの実行

## 概要

この演習では、terraformスクリプトを実行してAutonomous Databaseを生成し、グラフ・ユーザーを作成し、使用するデータセットをアップロードするスタックを作成します。

見積時間: 5分。

### 目標

次の方法を学習します

*   スタックを実行して、Autonomous Database、Graphユーザーを作成し、データセットをアップロードします
*   Graph Studioにログイン

## タスク1: OCIコンパートメントの作成

[](include:iam-compartment-create-body.md)

## タスク2: スタックの実行

次の手順では、グラフ・ユーザーおよびプロパティ・グラフ問合せに必要なデータセットを含むAutonomous Databaseを自動的に作成するスタックを実行する方法を示します。

1.  Oracle Cloudにログインします。
    
2.  ログインしたら、この[リンク](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kMdD7Vnv0J1st_2cU-S5PYNWT4SKzOOA04XbhwltUVXnOQ7vec1JJBEGk1eOxPS/n/oradbclouducm/b/moviestream_livelab/o/MovieStream_live_lab_7_AnD.zip)を使用してスタックを作成および実行します。
    

> ノート: リンクは新しいタブまたはウィンドウで開きます。

3.  このページが表示されます:

![スタックの作成ページ](./images/create-stack.png)

4.  「Oracle使用条件を確認して同意しました」ボックスを選択し、**コンパートメント**を選択します。残りはデフォルトのままにします。**「次へ」**をクリックします。

![「Oracle使用条件」が選択されていることを確認し、それに同意するオプション](./images/oracle-terms.png)

5.  **コンパートメント**を選択してAutonomous Databaseを作成し、スタックを作成する**リージョン**を選択してすべてのリソースを作成します。**「次へ」**をクリックします。確認ページが表示されたら、**「作成」**をクリックします。

![スタックの作成ページ](./images/configure-variables.png)

6.  「ジョブ詳細」ページが表示され、初期ステータスがオレンジ色で表示されます。ジョブが正常に完了すると、アイコンは緑色になります。
    
    ![ジョブは正常に終了しました](./images/successful-job.png)
    

## 謝辞

*   **著者** - 製品管理、Murakami Gutierrez Ramu、Jayant Sharma氏
*   **コントリビュータ** - Rahul Tasker、Jayant Sharma、Ramu Murakami Gutierrez、製品管理
*   **最終更新者/日付** - 2023年2月、製品マネージャー、Ramu Murakami Gutierrez氏