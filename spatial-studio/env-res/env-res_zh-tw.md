# 存取空間工作室

## 簡介

本實驗室逐步介紹從 Oracle LiveLabs 保留存取 Oracle Spatial Studio (Spatial Studio) 的程序。您的環境包括 Spatial Studio 和 Autonomous Database。在第一次登入 Spatial Studio 時，您將提供 Autonomous Database 的連線資訊。

預估實驗室時間：10 分鐘

### 目標

在此實驗室中，您將：

*   下載適用於您 Autonomous Database 的雲端公事包
*   執行第一次登入 Spatial Studio 以提供 Autonomous Database 連線資訊

### 先決條件

*   已完成「Oracle Spatial Studio 簡介」的 LiveLabs 保留

## 工作 1：下載適用於 Autonomous Database 的雲端公事包

1.  在「研習詳細資訊」中，記下您的雲端使用者名稱、密碼、區間和 Spatial Studio IP 位址。然後啟動「雲端主控台」。

![影像替代文字](images/1-1.png "影像標題")

2.  使用您的雲端使用者名稱和初始密碼，使用 **Oracle Cloud Infrastructure 直接登入**進行登入。系統會提示您變更預設密碼。

![影像替代文字](images/1-2.png "影像標題")

3.  依序瀏覽至 **Oracle Database** 和 **Autonomous Database** 。

![影像替代文字](images/1-3.png "影像標題")

4.  在左側的「區間」表單中，輸入先前提到的區間名稱。這會動態篩選區間清單。列出之後，請選取您的區間。接著會列出您的 Autonomous Database。按一下 Autonomous Database 的連結。

![影像替代文字](images/1-4.png "影像標題")

5.  按一下**資料庫連線**，然後按一下**下載公事包**。您將會升級公事包密碼。輸入任何字串，因為將不會使用此密碼。將公事包儲存至您筆記型電腦上的方便位置，如下一步將它使用。

![影像替代文字](images/1-5.png "影像標題")

## 工作 2:Spatial Studio 首次登入

1.  您現在將使用先前記下的 Spatial Studio IP 位址。在您的瀏覽器中開啟新分頁，然後瀏覽至 **https：//\[your Spatial Studio IP address\]：4040/spatialstudio** 。例如，如果您的 Spatial Studio IP 位址為 123.123.12.123，則您會瀏覽至 https://123.123.12.123:4040/spatialstudio.，因為您的 Spatial Studio 執行處理未設定已簽署的 SSL 憑證，因此您會看到瀏覽器特定的安全警告。接受警告並繼續前往該網站。在實際執行環境中，會設定憑證，不會進行此設定。使用使用者 **admin** 和密碼 **welcome1** 登入。

![影像替代文字](images/2-1.png "影像標題")

2.  第一次登入 Spatial Studio 會提示您輸入 Spatial Studio 之描述資料儲存區域的資料庫連線資訊。依序按一下 **Autonomous Database** 和**下一步**。在下一個 Scren 上，拖放先前下載的公事包檔案，然後按一下**確定**。

![影像替代文字](images/2-2.png "影像標題")

3.  系統現在會提示您輸入「自動資料庫」連線資訊。輸入使用者 **studio\_repo** ，密碼 **Welcome1Welcome1** ，然後選取媒體服務層級。

![影像替代文字](images/2-3.png "影像標題")

Spatial Studio 現在在 Autonomous Database 中建置其描述資料表格。這大約需要 30 秒。

4.  開啟 Spatial Studio 時，第一次登入完成，您就可以進行研討會。

![影像替代文字](images/2-4.png "影像標題")

您現在可以[進入下一個實驗室](#next)。

## 進一步瞭解

*   [Spatial Studio 產品頁面](https://oracle.com/goto/spatialstudio)

## 確認

*   **作者** - Database Product Management 的 David Lapp
*   **上次更新者 / 日期** - Database Product Management 的 David Lapp - 2021 年 6 月