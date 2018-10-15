### 陳述式

接續昨天的話題我們繼續聊。

### 反覆運算陳述式

反覆運算式就是我們俗稱的迴圈，當今天你需要反覆執行某事件，直到特地條件發生後才停止，就會推薦你使用迴圈來減少程式碼的長度，我們假設需要列印 1 ~ 5 之間所有的數字時，以下示範無迴圈的樣子

```
Console.WriteLine(1);
Console.WriteLine(2);
Console.WriteLine(3);
Console.WriteLine(4);
Console.WriteLine(5);
```

看起來很簡單，但是因為只有 5 個數字，而使用 for 迴圈則是

```
for (int i = 1; i <= 5; i++){
Console.WriteLine(i);
}
```

是不是簡化很多了？迴圈有 for, foreach, do-while 這三種。

#### for

for 迴圈由```for (initializer; condition; iterator) {body}```組成。

用以下範例做個講解

```
for (int i = 1; i <= 5; i++){
Console.WriteLine(i);
}
```

**for** 是陳述式使用，所以一定要加啦。

**initializer** 初始設定，也就是宣告一個只在這迴圈的作用域下能夠執行的變數，至於為什麼要這樣做後面可能會提到，這就比較深了，現在只介紹用法。如```int i = 1```，宣告一個 int 的 i 變數預設值為 1，因為我們要從 1 開始計算，**非必填**。

**condition** 條件判斷，也就是檢查是否要繼續執行這個迴圈，有開始總是要有結束，如```i <= 5```，當 i 值小於等於 5 時就繼續執行，**非必填**可用跳躍陳述式離開，但不結束也不會怎麼樣只是空跑效能而已(笑。

**iterator** 迭代器，這好難解釋，可以想像成是 body 結束時所做的行為，主要是對初始設定值操作，如```i++```，在結束時使 i + 1，如果不加 i 就永遠是 1，**非必填**。

**body** 就是重複的區塊，**必填**不然也不需要迴圈了XD，一樣如果只有一條也不需要括弧```{}```。

主要內容都是非必填沒錯，所以你可以這樣寫

```
int i = 1;
for (;;) {
  Console.WriteLine(i++);
  if (i > 5)
    break;
}
```

由 for 迴圈的作用域外寫一個初始值，並在 body 進行判斷與迭代，但不建議這樣做，只是說明也能這樣做，讓迴圈的開始與結束各自奔走，所以煩請寫在一起方便閱讀與修改，寫好程式的第一步就是方便閱讀與修改，本系列文可能會一直碎念吧。

個人會用到 for 迴圈時主要是使用 array，所以這邊來介紹一下 array。

array 是陣列，可以宣告一種簡單型別的陣列，當我們需要記載一連串的數字時，使用前

```
int a1 = 1;
int a2 = 2;
int a3 = 3;
```

使用後

```
int[] a = new int[3]{ 1, 2, 3 };
```

可參考下圖，好難用文字解釋

![https://raw.githubusercontent.com/MMiooiMM/learn-csharp-in-30-days/master/Day5/pic/01.png](https://raw.githubusercontent.com/MMiooiMM/learn-csharp-in-30-days/master/Day5/pic/01.png)

取值時記得陣列是從 0 開始數，所以數字 1 是 ```a[0]``` 這樣取得，所以使用 for 迴圈時

```
int[] a = new int[3]{ 1, 2, 3 };
for (int i = 0; i < 3; i++) {
  Console.WriteLine(a[i]);
}
```

可以注意到我是從 0 開始然後數到 3 時結束，另外 array 可以是多維度的

```
int[,] a = new int[5,6]; // 二維
int[,,] a = new int[5,6,7]; // 三維
```

也可以是不規則的，每一維度的大小不一樣

```
int[][] a = new int[2][]; // 二維陣列，帶有兩個不知道大小的一維陣列
a[0] = new int[5]; // 這個一維陣列，裝五個 int
a[1] = new int[6]; // 這個一維陣列，裝六個 int
```
任何陣列在使用前，都需要明確告知大小，詳細原因看之後有沒有機會說明。

#### foreach

>一個簡單且清楚的方法來逐一查看陣列、集合中的元素。

上面的 for 迴圈有 array 搭配，而這個 foreach 迴圈則是與 list 搭配，list 打算放到後面一點講，想與泛型集合類別一起講，所以把 foreach 先擱著，搭配良好也是個人觀感，不是說 array 一定要由 for 來做，你可以

```
int[] numbers = { 1, 2, 3 };
foreach (int i in numbers)
{
  Console.WriteLine(i);
}
```

純粹是個人習慣上的差別而已。

#### do-while

**do-while 迴圈** do 後一定要接 while 來作條件判斷

```
int i = 1;
do {
  Console.WriteLine(i++);
} while (i <= 5);
```

因為作用域的關係，do 的初始設定一定要寫在外面，否則會在每一次的執行刷新初始值，while 為 true 時重複執行 do 裡面的內容，do-while 迴圈**至少執行一次** do 裡面的事件。

**while 迴圈** while 的判斷若為 true 才執行，所以**可能一次都不執行**。

```
int i = 1;
while (i <= 5) {
  Console.WriteLine(i++);
}
```

今天介紹了三種迴圈，每一種迴圈都有適合的情境，所以不是哪種方式才是好的，一樣那句易讀易改才是良好的習慣，如果是初學者也不用太要求自己，等到程式碼寫得夠多時，自然會有感而發的，然後跟昨天一樣又算錯篇幅了，明天可能才講的完最後的陳述式。

參考連結
[反覆運算陳述式 (C# 參考) | Microsoft Docs]
[陣列 (C# 程式設計手冊) | Microsoft Docs]

[反覆運算陳述式 (C# 參考) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/iteration-statements 
[陣列 (C# 程式設計手冊) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/programming-guide/arrays/