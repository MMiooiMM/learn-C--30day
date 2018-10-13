  ### 運算子

  程式在進行運算時，需要依賴運算子來處理，例如加減乘除就是本文所說的運算子。

  運算子在進行運算時，是有優先順序的，就好比數學上的先加減後乘除，程式碼會依照優先順序進行運算，所以在使用時如果結果不是滿意的話，也可以像數學式子那樣加個括弧```()```來強調優先權。

  這邊介紹幾個實務上比較常出現的，若想了解全部運算子可以看文末連結。

  * 具有最高優先的運算子有

    * x.y 成員存取，可以呼叫 x 裡面的 y 屬性或方法。

    * x?. y 這也是成員存取，差別在於如果 x 是 null 則回傳 null，這很重要，如果在程式執行階段，沒有判斷 x 是否為 null 而強行取值，C# 可不會像 JS 一樣給你 undefined 這麼好心，這會使你的程式掛掉。

    這邊簡單說一下 null，我都這樣念 null，你也可以聽到很多種念法，這好比資訊界的 IKEA，還是只有我有這種困擾嗎XD。

    null 表示為無，該屬性為空值，像是```string str = null```，但通常不會在宣告時這樣使用，往往是處理資料時才會遇到的。還有像是 int 等的 value type 通常不能為空，但若需處理 null 情況，則需要在型別後方加一個問號(?)，像是```int? number = null```。

    * x[y] 索引存取，會在後面的 array 提到。

    * x?[y] 同上，只是多一個 null 判斷。

    * x++ 與 x-- 會在之後的 ++x 一起講解。

  * 一元運算子

    此後的每一個區段都具有的優先順序高於下一個區段且低於前一個區段。

    * ++x 與 --x 與上面的 x++ 和 x--，x++ 可以想成先取 x 後 +1，++x 則為先 +1 後取 x，而```--```只是替換成 -1，如
      ```
      int a = 6;
      int b = a++; // b 值為 6，a 值為 7。
      int c = ++a; // c 值為 8，a 值為 8。
      // 為 C# 的註解，告知程式 // 後面不需要執行。
      /*
      若要多行註解則用 /* 開頭與 */ 結尾
      */
      ```
      實務上不常用到，除了之後會講到的 for 迴圈。
    
    * -x 數值否定，如
      ```
      int a = 6;
      int b = -a; // b 值為 -6  
      ```

    * !x 邏輯否定，如
      ```
      bool a = true;
      bool b = !a; // b 值為 false
      ```

    * (T)x 型別轉換，有特別標註欲轉換的型別我們稱為顯性轉型，在轉換時需注意型別的大小是否能夠轉型，通常是小型別轉大型別，也可以不加則稱為隱性轉型，一樣文末有附上文章，如
      ```
      int a = 6;
      double b = (double)a;
      double c = a;
      ```

  * 乘法類運算子

    * x * y 乘法。

    * x / y 除法。

    * x % y 餘數，大致介紹一下，就是 5 除 4 餘 1 來說就是```5 % 4 = 1```。

  * 加法類運算子

    * x + y 加法。

    * x - y 減法。

  * 關係運算子

    * x > y 大於，x 與 y 可比較的話，若 x 大於 y 則回傳 ture 反之為 false。

    * x < y 小於，同上。

    * x >= y 大於等於，同上。

    * x <= y 小於等於，同上。

  * 等號比較運算子

    * x == y 等於，同上。

    * x != y 不等於，同上。

  * 條件 AND 運算子

    * x && y 邏輯 AND。如果 x 與 y 都是 true 則為 true，但如果其中一個為 false 則為 false。當 x 為 false，C# 就不會看 y。

  * 條件 OR 運算子

    * x || y 邏輯 OR。x 與 y 其中一個為 true 則為 true，如果 x 為 true，C# 就不會看 y。

  * Null 聯合運算子

    * x ?? y 如果 x 為 null 則回傳 y 反之為 x。

  * 指派運算子

    * x = y 指派，請不要與```==```搞混。

參考連結
[C# 運算子 | Microsoft Docs]
[轉型和類型轉換 (C# 程式設計手冊) | Microsoft Docs]

[C# 運算子 | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/operators/
[轉型和類型轉換 (C# 程式設計手冊) | Microsoft Docs]: https://docs.microsoft.com/zh-tw/dotnet/csharp/programming-guide/types/casting-and-type-conversions