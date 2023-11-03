# 在 Graph Studio 中使用 RDF 圖形

## 簡介

Oracle Autonomous Database 中的 Graph Studio 可讓使用者建立、查詢及分析圖表資料。它包括記事本、使用 PGQL 執行圖表查詢的開發人員 API、60 個以上的內建圖形演算法，以及提供包括原生圖形視覺化在內的數十種視覺化呈現。除了屬性圖之外，Graph Studio 現在還根據資源描述架構 (RDF) 和 Web Ontology Language (OWL)，擴充了語意技術支援，包括資料和待辦事項的儲存、推論和查詢功能。您現在可以將 Graph Studio 用於下列支援的 RDF 功能：

*   建立 RDF 圖形
*   在記事本段落中對 RDF 圖形執行 SPARQL 查詢
*   分析和視覺化 RDF 圖表

RDF 是代表連結資料的 W3C 標準資料模型。RDF 會使用統一資源識別碼 (URI) 作為資源與 URI 的全域唯一識別碼，以命名兩個資源之間的關係。除了 URI 之外，RDF 還使用文字來代表純量值，例如數字、字串以及時戳。RDF 模型會將資料連結為有指示標籤的圖表，其中每個邊緣通常稱為三重。邊緣的來源頂點稱為三重的主體。邊緣的標籤或名稱稱為三重的述詞，而邊緣的目的地頂點稱為三重的物件。RDF 圖表特別適合知識圖形和資料整合應用程式，因為 URI 提供全域唯一的識別碼，而且簡單、無綱要的三重結構，可將來自數個不同 RDF 圖表的資料輕鬆結合成單一圖表。此外，RDFS 和 OWL 提供標準方法來定義可重複使用的字彙 (一組語意有意義的邊緣標籤和資源類型)，以提供更具互通性和機器可處理的圖形資料。如需有關 W3C RDF 1.1 標準的詳細資訊，請參閱[這個網頁](https://www.w3.org/TR/rdf11-primer/)。

「SPARQL 通訊協定」與「RDF 查詢語言 (SPARQL)」是 W3C 標準化以查詢「資源描述架構 (RDF)」資料的其中一項技術。若要深入瞭解 W3C SPARQL 1.1 標準，請參閱[這裡](https://www.w3.org/TR/sparql11-overview/)。

SPARQL 使用 **SELECT 某些元素 WHERE 某些條件**結構來指定查詢。SPARQL 查詢的 WHERE 子句中的條件是使用三重樣式建立的，這基本上是 RDF 三重元素，其中三重元素可以用查詢變數取代 (以 ？前置碼表示)。三重模式中的查詢變數會當作萬用字元。考慮三重模式 **？movie ms:genre ms:genre\_Comedy** 。對 RDF 圖表評估此三重圖樣時，將會傳回含述詞 **ms:genre** 和 **object ms:genre\_Comedy** 之三重圖的所有**主旨**。SPARQL SELECT 子句指定從查詢建立專案的查詢變數清單。在 SPARQL 語法中，URI 會以角括號 (例如 [http://www.example.com/moviestream/actor](http://www.example.com/moviestream/actor)) 括住，而文字則以雙引號括住 (例如 "Kevin Bacon") . 文字後面可以接著 ^^ 和資料類型 URI (例如 "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer))，或後面接著 @ 和語言標記 (例如 「Jalapeño」@es)。SPARQL 中支援大多數 XML 綱要資料類型，而沒有資料類型 URI 的純文字則被視為具有資料類型 [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string) 。

以下是此示範範例，使用將會在此實驗室中使用的相似資料集。本影片強調使用 RDF 影片結構的本體結構。此示範的 RDF Graph 搭配 SQL Developer 使用暫存表格，與此 Autonomous Database 版本的實驗室不同。不過，用來查詢和視覺化資料的 SPARQL 語言與環境定義非常相似。

[使用 RDF 的示範範例](youtube:e_EQjInas50)

在此實驗室中，將會使用 SPARQL 建立語意圖表，這是整合不同資料來源的標準化方法。此程序將教導您如何使用圖形式查詢與視覺化來分析資料。

預估時間：25 分鐘

### 目標

*   開始使用 RDF 圖表
*   查詢 RDF 圖形並將其視覺化

### 先決條件

*   下列實驗室需要 Autonomous Database - 共用基礎架構帳戶。
*   且啟用圖形的使用者 (GRAPHUSER) 存在。亦即，具有正確角色和權限的資料庫使用者已經存在。

結束此實驗室。您現在可以**繼續進行下一個實驗室。**

## 確認

*   **作者** - Matthew McDaniel Solution Engineers，Ramu Murakami Gutierrez Product Manager，Nicholas Cusato
*   **技術貢獻者** - Melliyal Annamalai 傑出產品經理 Joao Paiva 技術人員諮詢成員 Lavanya Jayapalan 主要使用者協助開發人員
*   **上次更新者 / 日期** - Ramu Murakami Gutierrez，2022 年 6 月