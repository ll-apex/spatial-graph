# Spatial Studioリポジトリのデータベース・ユーザー

## 概要

この演習では、Spatial Studioのメタデータ・リポジトリに使用されるデータベース・スキーマの作成について説明します。これは、データセット、分析およびプロジェクトの定義など、Spatial Studioで実行する作業を格納するスキーマです。

Spatial Studioのリポジトリのデータベース・スキーマには、技術的には任意の名前を指定できます。他のSpatial Studioワークショップとの一貫性を保つために、ユーザー名に**studio\_repo**という名前を付けます。これはデータベース・ユーザー名であり、Spatial Studioアプリケーション自体のインストール時に作成されるデフォルトのSpatial Studio管理者ユーザー名(studio\_admin)など、Spatial Studioアプリケーションのユーザー名とは異なります。

推定ラボ時間: 5分

### 目標

*   Spatial Studioメタデータ・リポジトリのスキーマを作成する方法を学習します
*   データベース接続用にWalletをダウンロードする方法を学びます

### 前提条件

*   Oracle Free Tier、Always Free、有料またはLiveLabsクラウド・アカウント
*   データベースSQL Developer Webへのアクセス。

## タスク1: リポジトリ・スキーマの作成

1.  SQL Developer Webで、Spatial Studioリポジトリに使用されるAutonomousデータベースに**admin**ユーザーとして接続します
    
2.  Spatial Studioリポジトリのスキーマを作成します。スキーマには任意の名前を指定できますが、他の演習との一貫性を保つために、**studio\_repo**という名前を使用します。Oracle Autonomous Databaseのパスワード要件は[こちら](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F)です。後のステップで使用するため、選択したパスワードをノートにとります。
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## タスク2: 表領域割当ての割当て

1.  Spatial Studioリポジトリ・スキーマにデフォルト表領域を割り当てます。Autonomous Databaseでは、表領域名**data**を使用できます
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Spatial Studioリポジトリ・スキーマに表領域割当て制限を割り当てます。Spatial Studioのメタデータは、非常に少量のストレージを占有します。したがって、割当て制限は、主にリポジトリ・スキーマに格納されているビジネス・データに対応します。この演習では、割当て制限値**250M**で問題ありません。他のデータセットを試す場合は、値を **unlimited**に設定することもできます。
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## タスク3: 権限の付与

1.  Spatial Studioリポジトリ・スキーマ・ユーザーに次の権限を付与します
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

これで、studio\_repoスキーマをSpatial Studioリポジトリとして使用する準備ができました。

## タスク4: Walletのダウンロード

Spatial Studioで作成したAutonomous Databaseリポジトリ・スキーマに接続するには、Walletが必要です。次の演習でWalletを使用します。

1.  Autonomous Databaseに移動し、「詳細の表示」を選択します
    
    ![イメージ代替テキスト](images/repo-schema-1.png "イメージ・タイトル")
    
2.  「DB接続」タブを選択します。
    
    ![イメージ代替テキスト](images/repo-schema-2.png "イメージ・タイトル")
    
3.  「Walletのダウンロード」をクリックします。 ![イメージ代替テキスト](images/repo-schema-3.png "イメージ・タイトル")
    
    Walletファイルのパスワードを入力するように求められます。Walletは単一のzipファイルです。
    
4.  Walletファイルを便利な場所に保存します。このファイルは、次の演習で必要になります。
    

[次の演習に進む](#next)ことができます。

## 確認

*   **著者** - Oracle、データベース製品管理、David Lapp氏
*   **最終更新者/日付** - Database Product Management、David Lapp、2023年3月