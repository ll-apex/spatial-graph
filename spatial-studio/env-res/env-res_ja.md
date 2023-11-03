# Spatial Studioへのアクセス

## 概要

このラボでは、Oracle LiveLabs予約からOracle Spatial Studio (Spatial Studio)にアクセスするプロセスについて説明します。環境には、Spatial StudioとAutonomous Databaseが含まれます。Spatial Studioへの初回ログイン時に、Autonomous Databaseの接続情報を指定します。

推定ラボ時間: 10分

### 目標

この演習では、次のことを行います。

*   Autonomous Database用のCloud Walletのダウンロード
*   Autonomous Database接続情報を提供するSpatial Studioへの初回ログインの実行

### 前提条件

*   「Oracle Spatial Studioの概要」のLiveLabs予約が完了しました

## タスク1: Autonomous Database用のCloud Walletのダウンロード

1.  「ワークショップの詳細」で、クラウドのユーザー名、パスワード、コンパートメントおよびSpatial StudioのIPアドレスを確認します。次に、クラウド・コンソールを起動します。

![イメージ代替テキスト](images/1-1.png "イメージ・タイトル")

2.  クラウドのユーザー名と初期パスワードを使用して、**Oracle Cloud Infrastructureダイレクト・サインイン**を使用してサインインします。デフォルトのパスワードを変更するように求められます。

![イメージ代替テキスト](images/1-2.png "イメージ・タイトル")

3.  **「Oracle Database」**、**「Autonomous Database」**の順に移動します。

![イメージ代替テキスト](images/1-3.png "イメージ・タイトル")

4.  左側の「コンパートメント」フォームで、前に示したコンパートメント名を入力します。これにより、「コンパートメント」リストが動的にフィルタされます。一覧表示されたら、コンパートメントを選択します。Autonomous Databaseがリストされます。Autonomous Databaseへのリンクをクリックします。

![イメージ代替テキスト](images/1-4.png "イメージ・タイトル")

5.  **「データベース接続」**、**「Walletのダウンロード」**の順にクリックします。ウォレット・パスワード用に昇格します。このパスワードは使用されないため、文字列を入力してください。次のステップで使用するため、ウォレットをラップトップ上の便利な場所に保存します。

![イメージ代替テキスト](images/1-5.png "イメージ・タイトル")

## タスク2: Spatial Studioの初回ログイン

1.  前に書き留めたSpatial StudioのIPアドレスを使用します。ブラウザで新しいタブを開き、**https://\[your Spatial Studio IP address\]:4040/spatialstudio**に移動します。たとえば、Spatial StudioのIPアドレスが123.123.12.123の場合、https://123.123.12.123:4040/spatialstudio.に移動します。Spatial Studioインスタンスが署名付きSSL証明書で構成されていないため、ブラウザ固有のセキュリティ警告が表示されます。警告を受け入れてサイトに進みます。本番環境では、証明書が構成され、これは発生しません。ユーザー **admin**およびパスワード **welcome1**を使用してログインします。

![イメージ代替テキスト](images/2-1.png "イメージ・タイトル")

2.  Spatial Studioへの初回ログインでは、Spatial Studioのメタデータ・リポジトリのデータベース接続情報を入力するよう求められます。**「Autonomous Database」**、**「次へ」**の順にクリックします。次の画面では、前にダウンロードしたウォレット・ファイルをドラッグ・アンド・ドロップし、**「OK」**をクリックします。

![イメージ代替テキスト](images/2-2.png "イメージ・タイトル")

3.  これで、自動データベース接続情報の入力を求められます。ユーザー**studio\_repo**、パスワード**Welcome1Welcome1**を入力し、中程度のサービス・レベルを選択します。

![イメージ代替テキスト](images/2-3.png "イメージ・タイトル")

Spatial Studioは、Autonomous Databaseでメタデータ表を構築しています。これには約30秒かかります。

4.  Spatial Studioを開くと、初回ログインが完了し、ワークショップに進む準備が整います。

![イメージ代替テキスト](images/2-4.png "イメージ・タイトル")

[次の演習に進む](#next)ことができます。

## さらに学ぶ

*   [Spatial Studio製品ページ](https://oracle.com/goto/spatialstudio)

## 確認

*   **著者** - Database Product Management、David Lapp氏
*   **最終更新者/日付** - Database Product Management、David Lapp、2021年6月