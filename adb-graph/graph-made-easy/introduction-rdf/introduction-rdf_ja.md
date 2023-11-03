# Graph StudioでのRDFグラフの操作

## 概要

Oracle Autonomous DatabaseのGraph Studioを使用すると、ユーザーはグラフ・データをモデル化、作成、問合せおよび分析できます。ノートブック、PGQLを使用したグラフ問合せを実行するための開発者API、60以上の組込みグラフ・アルゴリズムが含まれ、ネイティブのグラフ・ビジュアライゼーションを含む多数のビジュアライゼーションが提供されます。プロパティ・グラフに加えて、Graph Studioでは、リソース記述フレームワーク(RDF)およびWebオントロジー言語(OWL)に基づくデータおよびオントロジのストレージ、推論および問合せ機能など、セマンティック・テクノロジのサポートが拡張されるようになりました。サポートされている次のRDF機能にGraph Studioを使用できるようになりました。

*   RDFグラフの作成
*   ノートブック段落のRDFグラフでSPARQL問合せを実行します
*   RDFグラフの分析と可視化

RDFは、リンクされたデータを表すためのW3C標準のデータ・モデルです。RDFでは、リソースおよびURIのグローバル一意識別子としてUniform Resource Identifiers (URI)を使用して、2つのリソース間の関係に名前を付けます。URIに加えて、RDFはリテラルを使用して、数値、文字列、タイムスタンプなどのスカラー値を表します。RDFは、データを指示付きラベル付きグラフとしてモデル化し、各エッジは通常トリプルと呼ばれます。エッジのソース頂点はトリプルのサブジェクトと呼ばれます。エッジのラベルまたは名前はトリプルの述語と呼ばれ、エッジの宛先頂点はトリプルのオブジェクトと呼ばれます。RDFグラフは、特にナレッジ・グラフおよびデータ統合アプリケーションに適しています。URIはグローバルに一意の識別子を提供し、単純なスキーマレス・トリプル構造により、複数の異なるRDFグラフのデータを単一のグラフに簡単に結合できるためです。さらに、RDFSおよびOWLは、相互運用性と機械処理性に優れたグラフ・データのために、再利用可能な語彙(意味的に意味のあるエッジ・ラベルとリソース・タイプのセット)を定義する標準的な方法を提供します。W3C RDF 1.1標準の詳細は、[ここ](https://www.w3.org/TR/rdf11-primer/)を参照してください。

SPARQLプロトコルおよびRDF問合せ言語(SPARQL)は、リソース記述フレームワーク(RDF)データの問合せ用にW3Cによって標準化されたテクノロジの1つです。W3C SPARQL 1.1標準の詳細は、[ここ](https://www.w3.org/TR/sparql11-overview/)を参照してください。

SPARQLは、**SELECT some elements WHERE some conditions**構造を使用して問合せを指定します。SPARQL問合せのWHERE句の条件は、トリプル・パターンを使用して作成されます。トリプル・パターンは基本的にRDFトリプルで、トリプルの要素を問合せ変数(?接頭辞で示される)に置き換えることができます。トリプル・パターンの問合せ変数は、ワイルドカードとして機能します。トリプルパターン **?movie ms:genre ms:genre\_Comedy**について考えてみます。このトリプル・パターンがRDFグラフに対して評価されると、述語**ms:genre**および**object ms:genre\_Comedy**を持つトリプルのすべての**サブジェクト**が返されます。SPARQL SELECT句では、問合せから投影する問合せ変数のリストを指定します。SPARQL構文では、URIは山カッコ([http://www.example.com/moviestream/actor](http://www.example.com/moviestream/actor)など)で囲まれ、リテラルは二重引用符(Kevin Baconなど)で囲まれます。リテラルには、^^とデータ型URI (例: "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer))が続くか、@と言語タグ(例: "Jalapeño"@es)が続くことができます。ほとんどのXMLスキーマ・データ型はSPARQLでサポートされており、データ型URIのないプレーン・リテラルはデータ型[http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string)であるとみなされます。

下記のビデオは、このラボで利用できる同様のデータセットを使用したデモの例です。このビデオでは、RDFを使用した映画構造のオントロジーの構造を強調しています。デモでは、SQL Developerと組み合せてステージング表を使用するRDFグラフが特長で、このAutonomous Databaseバージョンのラボとは明らかに異なります。ただし、データの問合せおよびビジュアル化に使用されるSPARQL言語は、コンテキストに非常によく似ています。

[RDFの使用例](youtube:e_EQjInas50)

この演習では、様々なデータ・ソースを統合するための標準化された方法であるSPARQLを使用してセマンティック・グラフを作成します。この手順では、グラフベースの問合せとビジュアライゼーションを使用してデータを分析する方法について説明します。

所要時間: 25分

### 目標

*   RDFグラフの開始
*   RDFグラフの問合せおよびビジュアル化

### 前提条件

*   次の演習では、Autonomous Database - 共有インフラストラクチャ・アカウントが必要です。
*   グラフ対応ユーザー(GRAPHUSER)が存在すること。つまり、正しいロールおよび権限を持つデータベース・ユーザーが存在します。

これで、このラボは終了です。**次の演習に進みます。**

## 確認

*   **著者** - Nicholas Cusato氏、Ethan Shmargad氏、Matthew McDanielソリューション・エンジニア、Ramu Murakami Gutierrez製品マネージャー
*   **技術貢献者** - Melliyal Annamalai Distinguished Product Manager、Joao Paiva Consulting Member of Technical Staff、Lavanya Jayapalanプリンシパル・ユーザー・アシスタンス開発者
*   **最終更新者/日付** - 2022年6月、プログラム・マネージャー、Ramu Murakami Gutierrez氏