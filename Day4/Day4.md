### 陳述式

由官方文件定義如下

>程式所採取的動作是在陳述式中表示。
>根據指定的條件，常見動作包括宣告變數、指派值、呼叫方法、循環執行集合，以及分支到一個或另一個程式碼區塊。
>陳述式在程式中的執行順序稱為「控制流程」或「執行流程」。
>根據程式如何反應它在執行階段收到的輸入，每次執行程式時，控制流程可能都會不同。

好比我們之前提到的宣告變數```int a;```、指派```a = 6;```。

題外話：如果有用到上一篇所提到的任何一個運算子，我們稱為運算式。

這篇一樣講解常用的陳述式，並大致介紹用法。

### 選取範圍陳述式

也就是常說的條件判斷式，有 **if-else** 與 **switch-case** 這兩個。

#### if-else

使用方式為```()```內的值如果是 **true** 則執行接著 if 的```{}```，若為 **false** 則執行接著 else 的```{}```。

```
if (true) {
  Console.WriteLine("我被執行到了");
}
else {
  Console.WriteLine("我沒被執行到");
}
```

像上述的程式碼為單行，如果是單行的話是可以省略```{}```如

```
if (true) 
  Console.WriteLine("我被執行到了");
else
  Console.WriteLine("我沒被執行到");
```

PS. 如果不想要 else 也可以只寫 if 就好。

```
if (true) {
  Console.WriteLine("我被執行到了");
}
```

但如果不只想要是或否，而是多重判斷的話，我們可以使用 **else if** 如

```
int score = 75;
if (score < 60) // 分數低於 60
  Console.WriteLine("不及格的 F");
else if (score < 70) // 分數低於 70
  Console.WriteLine("得到 D");
else if (score < 80) // 分數低於 80
  Console.WriteLine("得到 C");
else if (score < 90) // 分數低於 90
  Console.WriteLine("得到 B");
else                 // 不低於 60 70 80 90 的分數，分數不該低於 0，所以相等於 >= 90
  Console.WriteLine("得到 A");
```

可以注意到我是從小排到大，因為順序會大大影響程式流程，if-else if-else 的句子，**只會執行第一個** true 的情況，所以如果是先低於 90 的話，那本來不及格的就會變成 B 像是

```
int score = 75;
if (score < 90) // 分數低於 90
  Console.WriteLine("得到 B");
else if (score < 80) // 分數低於 80
  Console.WriteLine("得到 C");
else if (score < 70) // 分數低於 70
  Console.WriteLine("得到 D");
else if (score < 60) // 分數低於 60
  Console.WriteLine("不及格的 F");
else                 // 不低於 60 70 80 90 的分數，一樣等於 >= 90
  Console.WriteLine("得到 A");
```

本來應該是執行 **得到 C** 的事件，但因為先判斷小餘 90，所以得到了 **得到 B**事件了，所以在設計時需要考慮優先順序。

#### switch-case

類似 if-else if-else 的陳述，但我覺得閱讀性比前者好，雖然有人說效能會比前者差，但那也是在處理很大的條件判斷時才會出現些微的差距，如果路過的大大知道的話，可以幫我補充 XD。

**switch** 一般只在多條件判斷使用，但無法像前者一樣使用運算式，簡單來說就是不能在裡面比較大小，需要明確的知道內容，如果要依上面的例子來寫 switch 的話你需要

```
int score = 75;
switch (score) {
  case 0:
  case 1:
  /*
  .
  .
  .
  */
  case 59:
    Console.WriteLine("不及格的 F");
    break;
  case 60:
  /*
  .
  .
  .
  */
  case 69:
    Console.WriteLine("得到 D");
    break;
  /*
  .
  .
  .
  */
  case 89:
    Console.WriteLine("得到 B");
    break;
  default:
    Console.WriteLine("得到 A");  // 非 0 ~ 89 的數字
    break;
}
```

為了使程式碼可以運行，在 ... 加了註解，與上一個比較起來是不是複雜許多，但這是一個壞例子，所以請不要這樣模仿。

在上述的程式碼，你可以發現兩個新東西，一個是 **break** 一個是 **default**。

**break** 的用途是跳躍陳述式，在 switch 裡每一個 case 後都需要有一個 break 隔開，如果不隔開則可以判斷這兩個 case 執行相同內容，像是上面的 case 1 ~ 59 是共用 **不及格的 F** 事件，但在離開 switch 的 ```{}```也就是作用域前需要出現 break 來跳躍如

```
int a = 6;
switch (a) {
  case 6: // 這邊會出現紅字，控制項的位置不可位於最後一個 case 標籤('case 6:')的參數之外
    Console.WriteLine("a == 6 所以執行這邊");
}
```

所以必須改成以下這樣

```
int a = 6;
switch (a) {
  case 6:
    Console.WriteLine("a == 6 所以執行這邊");
    break;
}
```

還有一點就是該 case 如果有事件存在，則一定要加 break

```
int a = 6;
switch (a) {
  case 5: // 這邊會出現紅字，程式控制權無法從一個 case 標籤('case 5:')繼續到另一個
    Console.WriteLine("a != 5 所以不執行這邊");
  case 6:
    Console.WriteLine("a == 6 所以執行這邊");
    break;
}
```

你需要在結尾加上 break 如

```
int a = 6;
switch (a) {
  case 5:
    Console.WriteLine("a != 5 所以不執行這邊");
    break;
  case 6:
    Console.WriteLine("a == 6 所以執行這邊");
    break;
}
```

**default** 可以想成是 switch 版的 else，只要不屬於上面任何一個就是執行這裡，本文就不說他的預設值用法。

一個好的 switch 通常是明確知道內容物的，雖然分數也很明確沒錯，但數字是一個區間時，用 if-else 表達會更好，以下情況用 switch 就會比較好

```
string animal = "dog";
switch (animal) {
  case "cat":
    Console.WriteLine("Meow~");
    break;
  case "dog":
    Console.WriteLine("Woof!");
    break;  
}

if (animal == "cat") {
  Console.WriteLine("Meow~");
}
else if (animal == "dog") {
  Console.WriteLine("Woof!");
}
```
有注意到差異嗎？如果這時候動物種類一多，則會重複很多次的```animal ==```判斷，但這也只是使用上的習慣，沒有對錯。

除此之外，也可以發現不是一定要使用 default 的，就像 if-else 不一定要 else 一樣去處理非指定狀況，但建議使用來獲得例外狀況。在設計時可能會漏掉幾個應該考慮的點或者那些不預期的各種奇葩狀況，所以 default 往往是拋錯的好地方，後面講到例外處理時會在解釋。

本來打算把陳述式打完，但發現已經比預期的篇幅長，所以這邊就索性拆成兩篇了。

感謝閱讀。

參考連結
[陳述式 (C# 程式設計手冊) | Microsoft Docs]
[陳述式關鍵字 (C# 參考) | Microsoft Docs]

[陳述式 (C# 程式設計手冊) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/programming-guide/statements-expressions-operators/statements
[陳述式關鍵字 (C# 參考) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/statement-keywords
