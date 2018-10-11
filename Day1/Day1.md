### 前言

因為不知道能不能用Day0來講一些開賽前想說的話，所以就塞在第一天了，請見諒。

雖然標題很聳動，但在此之前本人並沒有發過任何技術教學文章，不知道自己能不能寫出符合這個規格的文章。

所以對我來說是練習寫技術教學文章的30天，想藉由自身比較熟悉的程式語言 C# 來練習自己的表達能力，所以不懂的地方或描述不完全的地方還請各位大大指教，謝謝。

若文章有任何錯誤也請路過的大大指導，還有新手在閱讀時`請不要百分百的相信內文`，文章為我本人學習與使用時所獲得的心得，也請培養對每件事情抱有懷疑的習慣，並找出對於自己真正正確的答案，找完後不怕麻煩也可以與我分享討論，謝謝。

### C#

根據維基百科的介紹，我們可以正確地發出 [C#][C# wiki]。

> C# 的發音為「C sharp」，「#」讀作「sharp」（/ʃɑːp/），命名啟發於音樂上的音名「C♯」，在音樂中「C♯」表示 C 升半音，為比 C 高一點的音節，且「#」形似 4 個加號，微軟藉助這樣的命名，表示 C# 在一些語言特性方面對 C++ 的提升的意思。

### 環境安裝

本文會以輕量的 VSCode 來做教學環境，首先請到[VSCode安裝頁面]下載符合自己電腦規格的版本。

如果本身已有安裝任何 C# 開發環境也可以，只是專案的建立方式不太一樣，這邊只針對 VSCode 進行講解。

題外話：如果是 Windows 或 Linux 的用戶，可以下載壓縮檔來製作 VSCode 攜帶版。只要在解壓縮後的資料夾裡增加一個 data 資料夾，讓往後的 VSCode 設定放在 data 裡面就可以。切記如果直接開啟就會寫入 user 資料夾裡，那就會失去免安裝的便利了。

安裝完開發環境後，接著是安裝[.NET Core SDK]進入網頁後，選擇 Download .NET Core SDK 進行安裝，安裝完畢就可以開始建立第一份專案了。

>.NET Core 軟體開發套件 (SDK) 是一組程式庫和工具，可讓開發人員建立 .NET Core 應用程式和程式庫。 這是開發人員最可能取得的套件。

### 建立第一份專案

新增一個空資料夾，然後開啟你的 VSCode 並且 Open folder 你的專案資料夾。

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/01.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/01.png)

開啟完畢後，點選左下角的圖示後點選 TERMIANL 或者快捷鍵`ctrl + ‵`來開啟終端機，然後可以輸入`dotnet new`來查看可安裝的專案範本。

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/02.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/02.png)

本系列文只介紹 C# 基礎語法而已，所以安裝的範本是`Console Application`，輸入`dotnet new console`來安裝`console`範本，如果需要實作桌面程式或者網頁等，可再閱讀後自行建立相對應範本練習。

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/03.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/03.png)
![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/04.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/04.png)

安裝後會提醒是否要安裝 C# 擴充套件，

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/05.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/05.png)

請點選 Install，安裝完後 Reload 就完成初始設定了。

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/06.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/06.png)
![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/07.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/07.png)

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/08.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/08.png)

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/09.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/09.png)

然後不免俗的開始任何程式的第一步，讓程式印出`Hello World!`。

點選左邊檔案總管的`Program.cs`會看到他的程式碼。

對，在你建立好範本時，他已經幫你實現第一步了，這時按下 F5 就可以執行程式了，或者你也可以選取左側選單的 Debug 蟲蟲圖案後按下左上綠色箭頭(Start Debugging)，你會在 DEBUG CONSOLE 看到一堆相關訊息與`Hello World!`。

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/10.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-30days/master/Day1/pic/10.png)

這樣我們便安裝好環境與建立第一份專案。

參考連結
[C# - 維基百科，自由的百科全書][C# wiki]
[VSCode]
[VSCode免安裝步驟]
[.NET Core SDK 概觀]

[C# wiki]: https://zh.wikipedia.org/wiki/C%E2%99%AF
[VSCode]: https://code.visualstudio.com/
[VSCode安裝頁面]: https://code.visualstudio.com/#alt-downloads
[VSCode免安裝步驟]: https://code.visualstudio.com/docs/editor/portable
[.NET Core SDK 概觀]: https://docs.microsoft.com/zh-tw/dotnet/core/sdk
[.NET Core SDK]: https://www.microsoft.com/net/download