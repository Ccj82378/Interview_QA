# DesignPattern Pattern


## 1. MVC, MVP, MVVM
- The difference is in way how data from model layer ends up in the view instances.
    - Model 
        模型物件用來表示與實作出應用程式內的各種資料物件，並且包含了商業處理邏輯
    - View 
        這部份表示應用程式中的使用者介面(UI)所要顯示的各個元件
- Model View Controller
    1. controller 處理使用者的互動與處理資料模型物件，並也針對 model 物件更新
    2. view 顯示資料
    3. model 取得 view 所要顯示的內容
    - 優點：生命周期成本低、可維護性高
    - 缺點：內存浪費嚴重、循環依賴性，組件模型圍繞 models 和 views 進行創建
- Model View Presenter
    1. view 為"被動視圖"（Passive View），定義一個介面，並且實作出來
    2. presenter 視為在 View 與 Model 中間協調者，做出不同的反應與處理或者存取 Model 物件內的資料給 View 使用
- Model View ViewModel
    - 類似MVP
    - view 通常會需要使用到 XAML 標記宣告語言來定義，而 XAML 僅僅提供了使用者介面的宣告，並無法提供任何處理邏輯
    - viewModel 扮演這存取資料 model 的責任，並且透過了資料繫結技術將資料提供給檢視
![image](https://github.com/Ccj82378/LearningNote/blob/main/img/MVC_MPV_MVVM.png)

## 2. Creational Patterns - 藉由控制物件創建的流程來解決問題
- Factory Pattern
    提供用於創建對象的通用接口，沒有明確要求使用構造函數
    ```
      class Factory {
        constructor() {
            this.create = function(type) {
            let vehicle;
            if (type === 'explorer' || type === 'ranger') vehicle = new Ford();
            else if (type === 'hellcat') vehicle = new Dodge();
            vehicle.roll = () => {
                return `The ${this._type} is rolling.`;
            };
            return vehicle;
            };
        }
        }
    class Ford {
        constructor() {
            this._type = 'ford';
            this.buy= () => {
            return 'You buy the ford.';
            };
        }
        }
    class Dodge {
        constructor() {
            this._type = 'dodge';
            this.sell = () => {
            return 'You sell the Dodge.';
            };
        }
        }
    // creating objects
    const factory = new Factory();
    const myFord = factory.create('explorer');
    const myDodge = factory.create('hellcat');

    console.log(myFord.roll()); // "The ford is rolling."
    console.log(myDodge.roll()); // "The dodge is rolling."
    console.log(myFord.buy()); // "You buy the ford."
    console.log(myDodge.sell()); // "You sell the Dodge."
    ```

- Singleton Pattern
    該實例的類別沒有存在任何實例化物件的話，則會創建一個新的實例並回傳它；但如果該實例已存在，則會回傳該實例的參考
    ```
    class Database {
    constructor(data) {
        if (Database.exists) {
        return Database.instance;
        }
        this._data = data;
        Database.instance = this;
        Database.exists = true;
        return this;
    }
    getData() {
        return this._data;
    }
    setData(data) {
        this._data = data;
    }
    }
    // usage
    const mongo = new Database(555);
    console.log(mongo.getData()); // 555
    
    const A = new Database(55465455);
    console.log(A.getData()); // 555
    ```

- Prototype Pattern
    基於現有對象克隆模板來創建對象
    ```
    var myCar = {
 
    name: "Ford Escort",
    
    drive: function () {
        console.log( "Weeee. I'm driving!" );
    },
        panic: function () {
            console.log( "Wait. How do you stop this thing?" );
        }
    };
    
    // Use Object.create to instantiate a new car
    var yourCar = Object.create( myCar );
    
    // Now we can see that one is a prototype of the other
    console.log( yourCar.name ); // "Ford Escort"
    ```
## 3. Structural Patterns - 改變物件與物件之間的結構，在呼叫某個功能時，沒有篡改原先功能狀況下，取得新的功能
- Adapter Pattern 
- Composite Pattern
- Decorator Pattern 
- Façade Pattern
- Flyweight Pattern 
- Proxy Pattern
## 4. Behavioral Patterns - 改變使用物件的行為，在使用某功能時所呼叫的方法不同
- Iterator Pattern
- Template Pattern
- Chain of Responsibility Pattern
- Command Pattern 
- Mediator Pattern
- Observer Pattern
- State Pattern
- Strategy Pattern