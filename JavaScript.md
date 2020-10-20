# JavaScript

## 作用域 (Scope)
一個變數的生存範圍，一旦出了這個範圍，就無法存取到這個變數

## let const var 差異
- var 是全域變數，let 與 const 是區域變數
    ``` {
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
    ``` const a;//error: unknown: Unexpected token (1:9)
    ```

- let 與 const 不允許重複宣告
    ``` var v1 = 1;
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
    ``` console.log(a);// error: Uncaught ReferenceError: a is not defined
    ```
但變數宣告卻擺到最上層(邏輯上)，這就是hoisting
    ``` console.log(a) // undefined
    var a
    ```
- 只有「宣告」有 hoisting 提升，賦值不會
    ``` console.log(a) // undefined, not 5
    var a = 5   
    ```
- let, const 沒有hoisting，但有暫時性死區(TDZ)
    ```{ 
        console.log(variable);
        let variable = 20;
        }
    ```
- 影響 
    1. 解決了必須先宣告函式才能使用，提升開發者體驗
    2. 實現函式互相遞迴