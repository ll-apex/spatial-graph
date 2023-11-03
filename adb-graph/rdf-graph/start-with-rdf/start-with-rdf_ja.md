# RDFグラフの開始

## 概要

このラボでは、Autonomous DatabaseにリンクされるバケットにRDFデータをアップロードして開始するステップについて説明します。これには、プロファイルから正しいOCIユーザー名をコピーする必要があります。Graph Studioが(DBMS\_CLOUDパッケージを使用して)OCIオブジェクト・ストレージのRDFデータにアクセスできるようにするには、OCIアカウントを使用してアクセス・トークンを作成する必要があります。これはセカンダリ・ラボで使用されます。

見積時間: 5分

### 目標

*   OCIオブジェクト・ストレージへのRDFデータのアップロード
*   OCIユーザー名の表示
*   アクセス・トークンの生成

### 前提条件

この演習では、次を想定しています。

*   Oracle Cloudアカウント
*   この[リンク](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)を使用してMOVIESTREAMファイル(moviestream\_rdf.nt)をダウンロードします

## **タスク1:** OCIオブジェクト・ストレージへのRDFデータのアップロード

1.  Oracle Cloud資格証明を使用してOCIコンソールにサインインします。
2.  ナビゲーション・メニューを開き、「Storage」をクリックします。「Object Storage & Archive Storage」で、次に示すように「Buckets」をクリックします。 ![メニューからバケット・フォルダが選択されている場所を説明するイメージ](./images/buckets-folder.png)
3.  OCIアカウントに適用するコンパートメントを選択します。 ![「バケット」ページの「コンパートメント」ドロップダウン・メニューの場所を示す図](./images/compartment-menu.png)
4.  「Create Bucket」をクリックします。「バケットの作成」スライダが次のように開きます。 ![「バケットの作成」ページを説明するイメージ](./images/create-bucket.png)
5.  「バケット名」を入力し、それ以外はすべてデフォルトのままにして、「作成」をクリックします。バケットが作成され、「バケット」ページに次のように表示されます。 ![バケットの作成結果を示す図](./images/bucket-result.png)
6.  RDF\_DATA\_BUCKETリンクをクリックし、「バケット詳細」ページにナビゲートします。

![作成後の「バケット」ページを示す図](./images/bucket-page.png) 7.「オブジェクト」セクションの「アップロード」をクリックします。「Upload Objects(オブジェクトのアップロード)」スライダが開きます。 8.ローカル・システムでダウンロードしたRDF moviestream\_rdf.ntファイルの[リンク](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)を選択し、「アップロード」をクリックします。ファイルは正常にアップロードされます。「クローズ」をクリックして、「バケット詳細」ページに戻ります。アップロードされたファイルは、「オブジェクト」の下に次のようにリストされます。 ![バケットにアップロードされたオブジェクトを示す図](./images/image-upload.png)

1.  アップロードしたファイルの「アクション」メニューを選択し、「オブジェクト詳細の表示」をクリックして、アップロードしたファイルのプロパティにアクセスします。「オブジェクトの詳細」スライダが次のように開きます。 ![「オブジェクト詳細の表示」オプションが強調表示された「オブジェクト」メニューを示す図](./images/object-details.png)
2.  オブジェクトのURLパスを書き留めます。これは、Graph StudioのRDFインポート・ウィザードで使用されます。 ![バケット内のオブジェクトへのURLパスの検索場所を示す図](./images/url-path.png)

## **タスク2:** OCIユーザー名の表示

1.  右上隅にあるアバター・アイコンをクリックして、プロファイルを開きます。「プロファイル」の下の最初のエントリは、OCIユーザー名です。 ![OCIプロファイルへのアクセス方法を示す図](./images/oci-profile.png)
2.  OCIユーザー名を書き留めます。これは、Graph StudioのRDFインポート・ウィザードで使用されます。 ![ユーザー詳細からのOCIユーザー名を示す図](./images/oci-username.png)

## **タスク3:** OCIコンソールからのアクセス・トークンの生成

1.  Oracle Cloud資格証明を使用してOCIコンソールにサインインします。
    
2.  右上のアバター・アイコンをクリックしてプロファイルを開き、「ユーザー設定」をクリックします。 ![プロファイルからユーザー設定にアクセスする方法を示す図](./images/user-settings.png)
    
3.  次に示すように、「リソース」で認証トークンをクリックします: ![「ユーザー設定」の「リソース」メニューから認証トークンにアクセスする方法を示す図](./images/auth-tokens.png)
    
4.  「Generate Token」をクリックします。「Generate Token」ダイアログが開きます。 ![認証トークンの生成方法を示す図](./images/gen-tokens.png)
    
5.  「説明」を入力し、「トークンの生成」をクリックします。生成されたトークンの詳細が次のように表示されます: ![生成された認証トークンのコピー方法を示す図](./images/token-details.png)
    
6.  「コピー」をクリックしてトークンをコピーし、後で使用するために保存します。
    

これで、このラボは終了です。_次の演習に進むことができます。_

## 謝辞

*   **著者** - Melliyal Annamalai、Distinguished Product Manager
*   **技術貢献者** - Santa Monica Specialist Hub、Nicholas Cusato氏
*   **最終更新者/日付** - Santa Monica Specialist Hub、Nicholas Cusato氏、2022年2月25日