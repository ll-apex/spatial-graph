# Graph Studio: CSVファイルから表へのデータのロード

## 概要

この演習では、Oracle Autonomous Data WarehouseまたはOracle Autonomous Transaction Processingインスタンスのデータベース・アクション・インタフェースを使用して、2つのCSVファイルを対応する表にロードします。

見積時間: 10分。

ラボのクイック・ウォークスルーについては、次のビデオをご覧ください。

[](youtube:wkKKO-RO0lA)

### 目標

次の方法を学習します

*   データベース・アクションを使用したAutonomous DatabaseへのCSVファイルのロード

### 前提条件

*   次の演習では、Oracle Autonomous Databaseアカウントが必要です。
*   グラフおよびWebアクセスが有効なユーザーが存在することを前提としています。つまり、正しいロールおよび権限を持つデータベース・ユーザーが存在し、そのユーザーはデータベース・アクションにログインできます。

## タスク1: Autonomous Databaseインスタンスのデータベース・アクションへの接続

1.  Oracle CloudコンソールでAutonomous Databaseインスタンスのサービス詳細ページを開きます。
    
    ![このイメージではALTテキストは使用できません](images/open-database-actions.png " ")
    
2.  **「データベース・アクション」**をクリックして開きます。
    

## タスク2: グラフ対応ユーザーとしてログイン

1.  Autonomous Databaseインスタンスのグラフ・ユーザー(`GRAPHUSER`など)としてログインします。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-graphuser-login.png " ")
    
    > **ノート:** _必要に応じて、次を実行して適切なロールおよび権限を持つユーザーを作成します_:
    
    *   Autonomous Databaseの**ADMIN**ユーザーとしてデータベース・アクションにログインします
    *   ナビゲーション・メニューから**「管理」**、**「データベース・ユーザー」**の順に選択します。
    *   **「ユーザーの作成」**をクリックします
    *   **「Web-Access」**および**「グラフ」**ボタンをオンにします。

## タスク3: ObjectStoreからのサンプル・データセットのダウンロード

1.  zipアーカイブのURLをブラウザにコピー・アンド・ペーストします。
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    または、`wget`または`curl`を使用して、サンプル・データをコンピュータにダウンロードします。  
    コピー・アンド・ペーストできる`curl`リクエストの例を次に示します。
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  アーカイブを~/downloadsなどのローカル・ディレクトリに**解凍**します。
    

## タスク4: データベース・アクション・データ・ロードを使用したアップロード

1.  **「データ・ロード」**カードをクリックします。
    
    ![このイメージではALTテキストは使用できません](images/db-actions-dataload-card.png " ")
    
    次に、データの場所を指定します。つまり、**LOAD DATA**および **LOCAL FILE**カードにチェックマークが付いていることを確認します。**「次へ」**をクリックします。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-dataload-location.png)
    
2.  **「ファイルの選択」**をクリックします。
    
    ![このイメージではALTテキストは使用できません](images/db-action-dataload-file-browser.png " ")
    
    正しいフォルダ(~/downloads/random-acct-dataなど)に移動し、`bank_accounts.csv`ファイルおよび`bank_txns.csv`ファイルを選択します。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-dataload-choose-files.png " ")
    
3.  正しいファイルが選択されていることを確認して、「**Run**」アイコンをクリックします。 ![このイメージではALTテキストは使用できません](./images/db-actions-dataload-click-run.png " ")
    
4.  データ・ロード・ジョブが必要であることを確認します。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-dataload-confirm-run.png " ")
    
5.  ファイルのロード後
    
    ![このイメージではALTテキストは使用できません](./images/dbactions-dataload-files-loaded.png " ")
    
    **「完了」**をクリックして終了します。
    
    ![このイメージではALTテキストは使用できません](images/dbactions-click-done.png " ")
    
6.  次に、**SQL**ワークシートを開きます。 ![このイメージではALTテキストは使用できません](./images/db-actions-choose-sql-card.png " ")
    
7.  正しいフォルダ(~/downloadsなど)に移動し、`fixup.SQL`ファイルを選択してSQLワークシートにドラッグします。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    ただし、copy-n-pasteを使用する場合、`fixup.sql`の内容は次のとおりです。
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    次のことを行います。
    
    *   `bank_accounts`表に主キー制約を追加します。
    *   列(`txn_id`)を`bank_txns`表に追加します。
    *   `txn_id`の値を設定し、トランザクションをコミットします。
    *   `bank_txns`表に主キー制約を追加します。
    *   `from_acct_id`が`bank_accounts.acct_id`を参照するように指定する外部キー制約を`bank_txns`表に追加します。
    *   `to_acct_id`が`bank_accounts.acct_id`を参照するように指定する2番目の外部キー制約を`bank_txns`表に追加します。
    *   `txn_id`列の追加と制約の確認に役立ちます。
8.  SQLワークシートで`fixup.SQL`スクリプトを実行します。  
    ![このイメージではALTテキストは使用できません](./images/db-actions-sql-execute-fixup.png " ")
    
9.  スクリプトの出力を次に示します。
    
    ![このイメージではALTテキストは使用できません](./images/db-actions-sql-script-output.png " ")
    
    これらの表からグラフを作成するには、**次の演習に進んで**ください。
    

## 謝辞

*   **著者** - 製品管理、Jayant Sharma
*   **貢献者** - 製品管理、Jayant Sharma
*   **最終更新者/日付** - 製品管理、Jayant Sharma、2022年2月