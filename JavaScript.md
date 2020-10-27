# JavaScript

## 1. Scope
一個變數的生存範圍，一旦出了這個範圍，就無法存取到這個變數

## 2. let const var 
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

## 3. Hoisting
- 對於Javascript來說，當存取一個尚未宣告的變數
    ``` 
    console.log(a); // error: Uncaught ReferenceError: a is not defined
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
        let variable = 20; // error: Uncaught ReferenceError: Cannot access 'variable' before initialization
    }
    ```
- 影響 
    1. 解決了必須先宣告函式才能使用，提升開發者體驗
    2. 實現函式互相遞迴

## 4. This
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

## 5. Function Declaration(函式運算式) vs Function Expression(函式陳述式) 
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

## 6. Pass by value vs by reference
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
    /* Shadow Copy */
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
    obj | { a:"abc" } | 類似 0x0001 這樣的記憶體位址
    - 如果 Value 指的是「資料的內容」：
        物件(object)間`obj1 = obj2`傳值，屬於Reference，而非 Value 
    - 如果 Value 指的是「存放在變數記憶體位址裡的值」：
        所有的傳值`x = y`都屬於 Value 的複製，因此只有 Pass by value。

## 7. Prototype Chain
- 發明人從C++引入`new`命令到JavaScript，後面接構造函數
    ```
    function DOG(name) {
        this.name = name;
    }
    var dogA = new DOG('來福');
    console.log(dogA.name); // 來福
    ```
- `new`的缺點，用構造函數產生實例對象，無法共享屬性和方法，資源也會浪費
    ```
    function DOG(name){
        this.name = name;
        this.species = '犬科';
    }

    var dogA = new DOG('來福');
    var dogB = new DOG('Lucky');

    dogA.species = '猫科';
    console.log(dogB.species); // 犬科
    ```
- 引入`prototype`屬性，最後`null`為原型鍊頂端
    ```
    function DOG(name) {
        this.name = name;
    }
    DOG.prototype = { species : '犬科' };

    var dogA = new DOG('來福');
    var dogB = new DOG('Lucky');

    console.log(dogA.species); // 犬科
    console.log(dogB.species); // 犬科

    DOG.prototype.species = '狗類';

    console.log(dogA.species); // 狗類
    console.log(dogB.species); // 狗類

    console.log(dogA.__proto__) // { species : '狗類' }
    console.log(DOG.prototype.__proto__ === Object.prototype)  // true
    console.log(Object.prototype.__proto__) // null，原型鍊頂端
    ```

## 8. Closure
- 當一個函數可以記住並存取到不同作用域的變數，甚至這個函數在不同 scope 被執行
- JavaScript 引擎的垃圾回收機制會釋放不再使用的記憶體，但閉包為了保留函式記得和存取其語彙範疇的能力
- 優點是能把變數隱藏在裡面讓外部存取不到
    ```
    function test () {
        var a = 10
        function inner() {
            console.log(a) // 還是 10
        }
        return inner
    }
    var inner = test(); 
    inner();
    ```

## 9. Call, Apply, Bind
- call：`fn.call(this, arg1, arg2..., argn)`，使用情境就在於要明確指定 this 的時候
- apply：`fn.apply(this, [arg1, arg2..., argn])`，陣列中每個元素為參數傳進目標函式
- bind：`fn.bind(this, arg1, arg2..., argn)`，回傳一個經過包裹後的 Function 回來，也可以把先前傳入 bind 的參數一並帶進目標函式中
    ```
    /* add 函式不需要 this，使用 null 來忽略他 */
    function add(a, b) {
        return a + b;
	}
	add.call(null, 1, 2);			// 3
	add.call(null, 1, 4);			// 5

	add.apply(null, [1, 2]);		// 3
	add.apply(null, [1, 4]);		// 5

	var add1 = add.bind(null, 1);
	console.log(add1(2));			// 3
	console.log(add1(4));			// 5
    ```

## 10. Currying 
- 將一個接受 n 個參數的 function，轉變成 n 個只接受一個參數的 function的過程
- 將傳入 function 的參數，利用 closure 特性，將它們存放在另一個 function 中並當做回傳值，而這些 function 會形成一個鏈（chain），待最後參數傳入，完成運算
- 優點是
    1. 簡化參數的處理，基本上是一次處理一個參數，藉以提高程式的彈性和可讀性
    2. 將程式碼依功能拆解成更細的片段，有助於重複利用
    ```
    multiply = (x, y) => x * y;
    multiply(3, 5) === 15 // true

    triple = (m) => multiply(3, m)
    triple(4) === 12 // true
    ```

## 11. Event Bubbling
    ```
    Window -> Document -> roots -> target(EventListener)  
    ====> 1.Capturing Phase =====>|    2.At Target    |
    <==== 3.Bubbing Phase <======= 
    ```
- 在`.addEventListener()`加上第三個參數
    - true：Capturing Phase
    - false：Bubbing Phase
    - 若不寫第三個參數，則預設為 false
- `e.stopPropagation()` 阻止事件傳遞，包含向上向下
-  Event delegation 事件代理
    ```
    /* 利用事件傳遞的機制，把 button 的 eventListener 綁定在上層的 .outer 元素上 */
    <div class="outer"> 
        <button class="btn_add" >add</button>
        <button class="btn" data-value="1">1</button>
        <button class="btn" data-value="2">2</button>
    </div>
    <script>
        document.querySelector('.outer').addEventListener('click',  function (e) {
        console.log(e.target.getAttribute('data-value'));
    })
    </script>
    ```


## 12. Synchronous vs Asynchronous
- 阻塞（blocking）代表執行時程式會卡在那一行，直到有結果為止，例如說readFileSync，要等檔案讀取完畢才能執行下一行；協調彼此的步伐，試著讓大家的腳步一致，就必須互相等待，這個就是同步
- 非阻塞（non-blocking）代表執行時不會卡住，但執行結果不會放在回傳值，而是需要透過回呼函式（callback function）來接收結果；；
- 阻塞的方法會同步地（synchronously）執行，而非阻塞的方法會非同步地（asynchronously）執行 - Node.js
- Callback Function
    - DOM事件監聽
    - 使用瀏覽器所提供的`setTimeout()`或`setInterval()`
    - 從資料庫或遠端伺服器請求資料

## 13. Promise
- 用在非同步處理，解決callback的可靠性不足，像是Callback Hell
- 只會有三種狀態
    1. `pending` - 初始狀態(進行中)
    2. `fulfilled` - 事件已完成 
    3. `rejected` - 事件已失敗
- 狀態改變只有:
    1. pending => fulfilled
    2. pending => rejected
- 狀態一改變就永久固定
    ```
    function number(num) {
        return (
            new Promise(function(resolve, reject) {
                if (num === 0) {
                    resolve("Yeah you got it, the number is 0");
                } 
                else {
                    reject(new Error('No No, your number is wrong'));
                }
           })
        )
    }

    number(1)
        .then(result => console.log("答對了！") );
        .catch(error => console.log("答錯了！") );
    ```
 - `async` 與 `await`
    ```
    function number(num){
        let result = new Promise(function(resolve, reject) {
            if (num === 0) {
                resolve("Yeah you got it, the number is 0");
            } 
            else {
                reject(new Error('No No, your number is wrong'));
            }
        })
        return result;
    }

    /* 當 function 裡有使用到 await 時，外面一定要有 async 的字眼，否則會出錯 */
    (async () => {
        const result = await number(0);
        console.log(result);
    })()
    ```
## 14. Event Loop
- JavaScript 是一種單線程的程式語言，簡單的說就是一次只能做一件事，而讓它做到不阻塞的背後功臣就是 Event Loop 這個機制
1. 堆疊(stack):資料結構的一種，它就像是疊盤子一樣，特性為後進先出
2. 佇列(queue):資料結構的一種，它就像排隊一樣，特性為先進先出
3. Web APIs 
![image](https://github.com/Ccj82378/Interview_QA/blob/main/img/EventLoop.png)

## 15. == vs ===
- `==`會自動做型別轉換
    ```
    var a = "14";
    var b = 14;
    console.log(a == b); // true
    console.log(a === b); // false
    ```
- 因為型別不同而有所差異，例如 Array、Object、 class，他們比較的方式是兩個變數是否指向同一個 reference

## 16. Higher-order Function
- 回傳函數的函數，或是接受函數作為參數的函數
    ```
    /* Curring */
    const add = x => y => z => x + y + z
    add(1)(2)(3) // 6
    ```
## 17. Pure Function
- 將相同的輸入丟入，永遠都會回傳相同的輸出
- 沒有任何顯著的副作用
- 優點: 
    - 程式碼閱讀性提高
    - 較為封閉與固定，可重覆使用性高
    - 輸出輸入單純，易於測試、除錯
    - 因為輸入->輸出結果固定，可以快取或作記憶處理，在高花費的應用中可作提高執行效率的機制
    ```
    var xs = [1, 2, 3, 4, 5];

    // pure
    xs.slice(0, 3);
    //=> [1, 2, 3]
    xs.slice(0, 3);
    //=> [1, 2, 3]
    xs.slice(0, 3);
    //=> [1, 2, 3]

    // impure
    xs.splice(0, 3);
    //=> [1, 2, 3]
    xs.splice(0, 3);
    //=> [4, 5]
    xs.splice(0, 3);
    //=> [] 被改變了
    ```

## 18. Side Effects
- 副作用是在計算結果的過程中，系統狀態的一種改變，或是外部世界可觀察的交互作用
- 透過pure function、作用域(如果副作用來自自由變數)減少副作用

## 19. slice()、splice()、split() 
- slice(): 複製開始與結束點（結束點不算）中的內容
    ```
    var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
    var fruit1 = fruits.slice(1);
    var fruit2 = fruits.slice(1, 3);
    var fruit3 = fruits.slice(-3); // 負數代表從後面開始算起，-1為倒數第一個元素

    // fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
    // fruit1 contains ['Orange', 'Lemon', 'Apple', 'Mango']
    // fruit2 contains ['Orange', 'Lemon']
    // fruit3 contains ["Lemon", "Apple", "Mango"]
    ```
- splice(): 從Array中添加/刪除項目，回傳被刪除的項目
    ```
    var myFish1 = ['angel', 'clown', 'drum', 'sturgeon'];
    var removed1 = myFish1.splice(2, 1, 'trumpet');

    // myFish1 is ["angel", "clown", "trumpet", "sturgeon"]
    // removed1 is ["drum"]

    var myFish2 = ['angel', 'clown', 'drum', 'sturgeon'];
    var removed2 = myFish2.splice(-2, 2, 'trumpet');

    // myFish2 is ["angel", "clown", "trumpet"]
    // removed2 is ["drum", "sturgeon"]
    ```
- split() 分割字串成字串組
    ```
    var str="How are you ?"
    var splits1 = str.split(" ");
    var splits2 = str.split("");
    var splits3 = str.split(" ",3);

    //splits1 contains ["How", "are", "you", "?"]
    //splits2 contains ["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "?"]
    //splits3 contains ["How", "are", "you"]
    ```

## 20. Immutable
- 基本型別如 number, string, boolean, null, undefined 具有值不可變性
- `const`常數宣告不變，但陣列值還是改變了
    ```
    const person = {player: {name: 'Messi'}};
    const person1 = person;
    console.log(person, person1); // [ { name: 'Messi' } ] [ { name: 'Messi' } ]
    person.player.name = 'Kane';
    console.log(person, person1); // [ { name: 'Kane' } ] [ { name: 'Kane' } ] 產生副作用
    ```
    運用shadow copy，在ES6中使用`object.assign`或者`...`
    ```
    const person = [{name: 'Messi'}];
    const person1 = person.map(item =>
    ({...item, name: 'Kane'})
    )
    console.log(person, person1); // [{name: 'Messi'}] [{name: 'Kane'}]
    ```
- deep copy
    透過Immutable.js等代替身拷貝來解決性能問提


