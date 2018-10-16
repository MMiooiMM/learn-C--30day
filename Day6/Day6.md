### 陳述式

### 跳躍陳述式

跳躍陳述式能在程式碼執行時跳躍語句順序執行，用途通常是離開迴圈或方法，有 break, continue, goto, return 四種。

#### break

> break 陳述式會終止其所在的最接近封閉式迴圈或 switch 陳述式。

switch 昨天有講了，那來解釋終止其所在的最接近封閉式迴圈是什麼意思，迴圈可以是巢狀的，也就是一層包一層如

```
for (int i = 1; i <= 9; i++) {
  for (int j = 1; j <= 9; j++) {
    Console.Write($"{i} * {j} = {i * j}\t");
  }
  Console.Write("\n");
}
```

這就是簡單的 99 乘法表列印，用了 string 的字串內插補點(```$```)，後面介紹方法時會提到，而```\t```的```\```是跳脫字元，```\t```等同於水平方向的 TAB，而```\n```是換行，跳脫字元可以參考文末前輩寫的文章，因為 C# 不是什麼新東西，網路上有太多的資源了，至少我學到現在還沒有找不到的答案。所以我不打算寫在系列文的內容，之後可能都會在文末附上額外補充的文章，想了解可以自行前往，但不讀也不會影響之後的內容就是了。

歪題了，這就是巢狀迴圈，雖然我不知道到底要幾層才能稱為巢狀啦。

當今天只要印 1 ~ 9 的各別乘到五時，也就是乘數是六我就將被乘數 +1，就可以加入 break 來終止迴圈。

```
for (int i = 1; i <= 9; i++) {
  for (int j = 1; j <= 9; j++) {
    if (j == 6) break;
    Console.Write($"{i} * {j} = {i * j}\t");
  }
  Console.Write("\n");
}
```

我只是舉個例子，實際上我們都知道改 j 的條件判斷就好。

我們先稱以 i 為主的迴圈為 i 迴圈 而 j 為主的迴圈為 j 迴圈，上面的程式碼可以看到雖然 i 迴圈與 j 迴圈都包住 break，但離 break 最近的是 j 迴圈，所以當 ```j == 6``` 為 true 時終止 j 迴圈。記住是要**包住 break 的迴圈**才會被正確的終止，所以放在 i 迴圈裡 j 迴圈外則是印 1 ~ 5 的各別乘到九

```
for (int i = 1; i <= 9; i++) {
  if (i == 6) break;
  for (int j = 1; j <= 9; j++) {
    Console.Write($"{i} * {j} = {i * j}\t");
  }
  Console.Write("\n");
}
```

可以看到我把條件判斷改成 ```i == 6```，因為 j 的作用域在 j 迴圈，i 迴圈無法讀取 j 值。

PS.程式碼都可以複製放進 Main 函式裡觀看結果。

#### continue

> continue 陳述式會將控制權轉移給其所在的封閉式 while、do、for 或 foreach 陳述式的下一個反覆項目。

與 break 不同，continue 不會使迴圈中斷，只是跳過這一次執行，一樣由 99 乘法表來改寫，這次我們不想要印出 5 結尾的 99乘法表

```
for (int i = 1; i <= 9; i++) {
  for (int j = 1; j <= 9; j++) {    
    if (j == 5) continue;
    Console.Write($"{i} * {j} = {i * j}\t");
  }
  Console.Write("\n");
}
```

#### goto

> goto 陳述式會將程式控制權直接轉移到標記陳述式。
> goto 的一個常見用法是將控制權轉移到特定的切換案例標籤，或 switch 陳述式中的預設標籤。
> goto 陳述式也適用於跳出深度巢狀的迴圈。

一樣來改寫 99 乘法表，並逐一解釋 goto 的用法。

第一種直接轉移控制權，就是跳到標記的陳述式位置如

```
  for (int i = 1; i <= 9; i++) {
    for (int j = 1; j <= 9; j++) {    
      if (j == 5) goto Finish;
      Console.Write($"{i} * {j} = {i * j}\t");
    }
    Console.Write("\n");
  }
Finish:
  Console.Write("跳到這之後了");
```

執行一次就會知道當 ```j == 5``` 時就跳到 ```Finish:```後面的程式碼了，所以只執行到 ```1 * 4 = 4```，也一起解釋第三種所描述的情況，他跳出了巢狀迴圈。

根據第一種方式你可以這樣撰寫

```
  int i = 0;
  goto First;
Second:
  Console.WriteLine(i);
  goto Third;
First:
  i = i + 1;
  goto Second;
Third:
  i = i + 1;
  Console.WriteLine(i);
```

我不能保證你不被打死，寫的時候還要注意不能造成無窮迴圈

```
  int i = 0;
InfiniteLoop:
  i = i + 1;
  goto InfiniteLoop;
```

第二種的 switch 裡切換預設標籤，Day 3 介紹的 switch 沒有提到這個用法，主要是本人很少使用 goto，所以寫得當下沒有意識到，那這邊就來順便補充一下，拿 Day 3 的例子來說， switch 內你想要 case 6 的事件執行完之後也執行 case 5 事件的話，那就可以用 goto 來達成

```
int a = 6;
switch (a) {
  case 5:
    Console.WriteLine("a != 5 所以不執行這邊但因為 goto 所以跑過來了");
    break;
  case 6:
    Console.WriteLine("a == 6 所以執行這邊");
    goto case 5;
}
```

透過 goto 就可以到達 case 5 事件印出```a != 5 所以不執行這邊但因為 goto 所以跑過來了```，所以我應該修正本來的話

> 在 switch 裡每一個 case 後都需要有一個 break 隔開，如果不隔開則可以判斷這兩個 case 執行相同內容

改成

> 在 switch 裡每一個 case 後都需要有一個 break 或 goto 隔開，如果不隔開則可以判斷這兩個 case 執行相同內容

還有這句

> 該 case 如果有事件存在，則一定要加 break

改成

> 該 case 如果有事件存在，則一定要加 break 或 goto

所以說我寫的內容不一定是百分百正確，請小心服用。

題外話：因為我想把文章寫給每天跟著閱讀的人，所以不修改前面的文章，而是在後面提起前面錯誤的內容。

#### return

> return 陳述式會終止執行在其中出現的方法，並且將控制權傳回給呼叫方法。

會在介紹方法時一起說明。

#### 一些小結論

break 與 continue 主要是跟著迴圈使用，使迴圈在進行時當特定條件發生時的處理，離開迴圈(break)或跳過並繼續執行下一個(continue)。因為目前只有介紹基礎，等到之後學會的內容一多，就可以看到更多的範例了。

而 goto 本人極少使用，很難說明情境。

題外話：寫到今天，系列文的走向已經跟預想的慢慢不一樣了，覺得這時候應該先介紹什麼，什麼該放在後面，不知道這樣的編排，讓讀者閱讀時方不方便。本來想把例外狀況處理陳述式(try-catch)與這篇放在一起，但考慮之後想把 try-catch 與 debug 技巧寫作一篇，並放在介紹方法完之後，所以會再看到陳述式(四)XD。

感謝您的閱讀。

參考連結
[跳躍陳述式 (C# 參考) | Microsoft Docs]
[C#常用的幾個特殊逸出Escape字元 | Jeff 隨手記 - 點部落]

[跳躍陳述式 (C# 參考) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/jump-statements
[C#常用的幾個特殊逸出Escape字元 | Jeff 隨手記 - 點部落]: https://dotblogs.com.tw/jeff-yeh/2009/03/17/7509