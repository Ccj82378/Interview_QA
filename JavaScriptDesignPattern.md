# JavaScript Design Pattern

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
- Model View Presenter
    1. view 為"被動視圖"（Passive View），定義一個介面，並且實作出來
    2. presenter 視為在 View 與 Model 中間協調者，做出不同的反應與處理或者存取 Model 物件內的資料給 View 使用
- Model View ViewModel
    - 類似MVP
    - view 通常會需要使用到 XAML 標記宣告語言來定義，而 XAML 僅僅提供了使用者介面的宣告，並無法提供任何處理邏輯
    - viewModel 扮演這存取資料 model 的責任，並且透過了資料繫結技術將資料提供給檢視
![image](https://github.com/Ccj82378/LearningNote/blob/main/img/MVC_MPV_MVVM.png)