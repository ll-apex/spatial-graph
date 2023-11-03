# グラフのビジュアル化

## 概要

前の演習で行った分析の結果は、グラフ・ビジュアライゼーション機能を使用して簡単に視覚化できます。

予想時間: 5分

次のビデオでは、グラフ・ビジュアライゼーション・コンポーネント(= GraphViz)の概要を示します。

[YouTube](youtube:zfefKdNfAY4)

### 目標

*   PGQLグラフ問合せを実行して結果をビジュアル化する方法を学習します。

### 前提条件

*   グラフが作成され、公開されます。
*   グラフ・サーバー(GraphVizを使用)は稼働中です

## タスク1: GraphVizへのログイン

Webブラウザを使用して、GraphVizを**`https://<public_ip_for_compute>:7007/ui`**で開きます。**`<public_ip_for_compute>`**をグラフ・サーバーのコンピュート・インスタンスのものに置き換えます。

マーケットプレイス・イメージは自己署名SSL証明書とともに配布されるため、本番環境で使用している独自の証明書用に変更する必要があります。一方、Webブラウザは警告を表示する必要がありますが、安全であることを理解しています。

**Chrome**を使用する場合は、警告ウィンドウで **thisisunsafe**と入力して GraphViz画面に移動します。

![ログイン- クロム](images/login-chrome.jpg)

**Firefox**を使用して、**「拡張」**、**「リスクの受入れと続行」**の順にクリックします。

![ログイン-firefox](images/login-firefox.jpg)

次のスクリーンショットのような画面が表示されます。ユーザー名(**customer\_360**)とパスワードを入力し、「送信」をクリックします。**「グラフ・サーバー」**は「拡張オプション」のデフォルトであるため、変更する必要はありません。

![ログイン](images/login.jpg)

## タスク2: 問合せの変更

最初の5行を取得するように問合せを変更します。つまり、**LIMIT 100**を**LIMIT 5**に変更し、「実行」をクリックします。

次のスクリーンショットのようなグラフが表示されます。

![show-5-elements](images/show-5-elements.jpg)

## タスク3: ハイライトの追加

次に、ラベルやその他のビジュアル・コンテキストを追加します。これらはハイライトと呼ばれます。zipファイルhighlights.json.zipをダウンロードするには、[ここ](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip)をクリックします。このファイルを解凍し、解凍した場所をメモします。

「**Settings**」(画面の右側)の「Load」ボタンをクリックします。適切なフォルダを参照してファイルを選択し、「開く」をクリックしてロードします。

![ハイライト-1](images/highlights-1.png)

グラフは次のようになります。

![ハイライト-2](images/highlights-2.png)

## タスク4: PGQLによるパターン一致

1.  次に、いくつかのPGQL問合せを実行します。
    
    [pgql-lang.org](http://pgql-lang.org)サイトと [Specification](http://pgql-lang.org/spec/1.4)は、詳細と例に関する最適なリファレンスです。ただし、この演習の目的では、基本は最小限です。
    
    PGQL問合せの一般的な構造は次のとおりです。
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQLは、グラフ・パターンを照合するための**MATCH**句と呼ばれる特定の構造を提供します。グラフ・パターンは、指定された条件および制約を満たす頂点およびエッジと一致します。
    
    *   **(v)**は頂点変数**vを示します**
    *   **\-**は(source)-(dest)のように、間接エッジを示します
    *   **\->**ソースから宛先への送信エッジ
    *   **<-**宛先からソースへの受信エッジ
    *   **\[e\]**はエッジ変数**を示します**
    
    また、GraphViz UIから選択されているため、ここでは**graph\_name**を省略してください。
    
2.  同日に500を超えるアウトバウンドおよびインバウンド転送があったアカウントを見つけましょう。
    
    このPGQL問合せは次のとおりです。
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    前述の最初の**MATCH**句では、**(a)**はソース頂点を示し、**(a1)**は宛先を示し、**\[t1:transfer\]**はそれらを接続するエッジです。**:transfer**は、**t1**エッジにラベル **TRANSFER**があることを指定します。2つのパターンの間のカンマ(、)はAND条件です。
    
3.  問合せをコピーして、GraphVizアプリケーションのPGQLグラフ問合せテキスト入力ボックスに貼り付けます。「実行」をクリックします。
    
    結果は次のようになります。強調表示設定では、**xxx-yyy-**で始まる口座は赤色(= 銀行の口座)で表示され、**xxx-zzz-**はオレンジ色(= 別の銀行の口座)で表示されます。
    
    ![同日転送](images/same-day-transfers.jpg)
    
4.  次の問合せでは、同じ2つのアカウント(a1->a2およびa2->a1)との間の転送パターンを検索します。
    
    このPGQL問合せは次のとおりです。
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  問合せをコピーして、GraphVizアプリケーションのPGQLグラフ問合せテキスト入力ボックスに貼り付けます。「実行」をクリックします。
    
    結果は次のようになります。
    
    ![サイクル2ホップ](images/cycle-2-hops.jpg)
    
6.  その問合せにアカウントをもう1つ追加して、3つのアカウント間の循環転送パターンを検索します。
    
    PGQL問合せは次のようになります。
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  問合せをコピーして、GraphVizアプリケーションのPGQLグラフ問合せテキスト入力ボックスに貼り付けます。「実行」をクリックします。
    
    結果は次のようになります。
    
    ![サイクル3ホップ](images/cycle-3-hops.jpg)
    

## 確認

*   **著者** - Jayant Sharma
*   **貢献者** - Arabella Yao、Jenny Tsai
*   **最終更新者/日付** - 山中亮太、2023年3月