# JavaScript Design Pattern

## 1. MVC, MVP, MVVM
- Model View Controller
    1. View 傳送指令到 Controller
    2. Controller 完成業務邏輯後，要求 Model 改變狀態
    3. Model 將新的數據發送到 View，用戶得到反饋
- Model View Presenter
    1. 各部分雙向聯繫
    2. View 與 Model 不發生聯繫，透過 Presenter 傳遞。
    3. View 非常薄，不部署任何業務邏輯，稱為"被動視圖"（Passive View），即沒有任何主動性，而 Presenter非常厚，所有邏輯都部署在那裡。

![image]()