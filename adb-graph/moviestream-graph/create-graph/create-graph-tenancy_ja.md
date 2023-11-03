# グラフの作成

## 概要

この演習では、Graph Studioのガイド付きユーザー・エクスペリエンスを使用して、`MOVIE, CUSTOMER\_SAMPLE`表および`WATCHED`表からグラフを作成します。

見積時間: 15分。

### 目標

次の方法を学習します

*   Graph Studioを使用して、既存の表またはビューからグラフをモデル化および作成します。

### 前提条件

*   次の演習では、Autonomous Databaseサーバーレス・インスタンスが必要です。
*   グラフ対応ユーザーが存在すること。つまり、正しいロールおよび権限を持つデータベース・ユーザーが存在します。

## タスク1: Autonomous Databaseへのアクセス

1.  左上の**「ナビゲーション・メニュー」**をクリックし、**「Oracle Database」**に移動して**「Autonomous Database」**を選択します。
    
    ![Autonomous Databaseへのナビゲート。](images/navigation-menu.png " ")
    
2.  **コンパートメント**を選択し、**Autonomous Database**の**「表示名」**をクリックします。
    
    ![ナビゲーション・メニューで「Autonomous Database」を選択します。](images/select-autonomous-database.png " ")
    

## タスク2: Graph Studioへのログイン

[](include:adb-goto-graph-studio.md)

## タスク3: ムービー推奨グラフの作成

[](include:adb-create-graph.md)

## 謝辞

*   **著者** - Oracle Spatial and Graph、製品マネージャ、Melli Annamalai
*   **貢献者** - Jayant Sharma
*   **最終更新者/日付** - Oracle Spatial and Graph、製品マネージャ、Ramu Murakami Gutierrez、2023年7月