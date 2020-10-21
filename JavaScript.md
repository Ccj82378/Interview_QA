# JavaScript

## 作用域 (Scope)
一個變數的生存範圍，一旦出了這個範圍，就無法存取到這個變數

## let const var 差異
- var 是全域變數，let 與 const 是區域變數
    ``` 
    {
        var a = "hi";
    }
        console.log(a); //hi
    {
        let b = "hello";
    }
        console.log(b); //error: Uncaught ReferenceError: b is not defined
    {
        let c = "aloha";
    }
    console.log(b); //error: Uncaught ReferenceError: c is not defined
    ```

- const必須要賦值
    ``` 
    const a;//error: unknown: Unexpected token (1:9)
    ```

- let 與 const 不允許重複宣告
    ``` 
    var v1 = 1;
    var v1 = 2;
    console.log(v1); //2

    let v2 = 3;
    let v2 = 4;
    console.log(v2); //error: unknown: Identifier 'v2' has already been declared (2:4)

    const v3 = 5;
    const v3 = 6;
    console.log(v3); //error: unknown: Identifier 'v3' has already been declared (2:6)
    ```

## Hoisting(var, let, const, function)
- 對於Javascript來說，當存取一個尚未宣告的變數
    ``` 
    console.log(a);// error: Uncaught ReferenceError: a is not defined
    ```
但變數宣告卻擺到最上層(邏輯上)，這就是hoisting
    ``` 
    console.log(a) // undefined
    var a
    ```
- 只有「宣告」有 hoisting 提升，賦值不會
    ``` 
    console.log(a) // undefined, not 5
    var a = 5   
    ```
- let, const 沒有hoisting，但有暫時性死區(TDZ)
    ```
    { 
        console.log(variable);
        let variable = 20;
    }
    ```
- 影響 
    1. 解決了必須先宣告函式才能使用，提升開發者體驗
    2. 實現函式互相遞迴

## This
- 被呼叫地當下，呼叫函式的物件
- 隨者函數使用場合不同，this值會發生變化
- 有new，則指向new對象
    ```
    function callName() {
    console.log(this.name);
    }

    var auntie = {
    name: '漂亮阿姨',
    callName: callName,
    watch: {
        name: 'Magic Watch',
        callName: callName
    }
    }

    auntie.callName() // '漂亮阿姨'
    auntie.watch.callName() // 'Magic Watch'
    ```

## Event Loop
- JavaScript 是一種單線程的程式語言，簡單的說就是一次只能做一件事，而讓它做到不阻塞的背後功臣就是 Event Loop 這個機制
1. 堆疊(stack):資料結構的一種，它就像是疊盤子一樣，特性為後進先出
2. 佇列(queue):資料結構的一種，它就像排隊一樣，特性為先進先出
3. Web APIs 
![image](https://github.com/Ccj82378/Interview_QA/blob/main/img/EventLoop.png)

## function declaration(函式運算式) vs function expression(函式陳述式) 
- function declaration 最大差異就是呼叫自定函式時可在function前
    ```
    /* function declaration */
    callTest ();
    function callTest () {
        console.log(123); // 123
    }

    /* function expression */
    var callTest = function() {
    console.log(123);// error: Uncaught TypeError: callTest is not a function
    }
```
- declaration只要被定義過後就無法從記憶體中刪除並回收，而expression則是正常的跟著變數生命週期運作，可能定義完後則直接被回收或是跟著變數的參考被移除時就結束等待GC回收

## Pass by value vs by reference
- 將舊變數(x)的值(5)複製一份，放進一塊新的記憶體，讓新變數(y)指向過去，兩者皆存放獨立資料
    ```
    /* by value */
    var x = 5;
    var y = x; 
    console.log(x); // 5
    console.log(y); // 5

    x = 10;
    console.log(x); // 10
    sonsole.log(y); // 5
    ```

- 新變數會直接指向舊變數的記憶體位址，等於新舊變數共用同一個位址的資料
    ```
    /* by reference */
    var p1 = [ money: 111];
    var p2 = p1;
    console.log(p1); // {money: 111}
    console.log(p1); // {money: 111}

    p1.money = 222;
    console.log(p1); // {money: 111}
    console.log(p1); // {money: 111}
    ```

- 依照變數的資料型別，決定傳遞行為是 Pass by value 或 Pass by reference
    - 變數的值是原生型別 (Primitive) 時，行為是 Pass by value
    在 JavaScript 中，原生型別 (Primitive) 包含：
        - String
        - Number
        - Boolean
        - Undefined
        - Null 
    - 當變數的值是物件型別 (Object) 時，行為是 Pass by reference，物件型別常見的例如：
        - Array
        - Object

- Pass by Sharing ?
雖然是物件型別 (Object) 的變數，如果是對物件變數作重新賦值，只會變更自己的值，不會連另一個變數一起變更。
    ```
    /* array literals */
    var ary1 = [1, 2, 3];
    var ary2 = ary1;
    console.log(ary1); // [1, 2, 3]
    console.log(ary2); // [1, 2, 3]

    ary1 = [99, 100];
    console.log(ary1); // [99, 100]
    console.log(ary2); // [1, 2, 3]


    /* object literals */
    var person1 = { money: 111 };
    var person2 = person1;
    console.log(person1);  // {money: 111}
    console.log(person2);  // {money: 111}

    person1 = { money: 222 };
    console.log(person1);  // {money: 222}
    console.log(person2);  // {money: 111}
    ```

- Only by value ?
    ```
    var n = 123;
    var obj = { a:"abc" };
    ```
    變數 | 資料的內容 | 存放在變數記憶體位址裡的值
    --- | --- | ---
    n | `123` | `123`

    obj | {a:"abc"} | 類似 0x0001 這樣的記憶體位址
    - 如果 Value 指的是「資料的內容」：
        物件(object)間`obj1 = obj2`傳值，屬於Reference，而非 Value 
    - 如果 Value 指的是「存放在變數記憶體位址裡的值」：
        所有的傳值`x = y`都屬於 Value 的複製，因此只有 Pass by value。