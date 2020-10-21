# ReactJS

## 1. 特性
1. 基於元件（Component）化思考
2. 用 JSX ( 擴充、語法糖 )進行宣告式UI 設計
3. 使用 Virtual DOM：

    從 MVC 架構追溯起，主要都是為了解決前端頁面呈現、資料更動、使用者操作這三種狀態交互作用產生的複雜性
    註MVC
    優點：生命周期成本低、可維護性高
    缺點：內存浪費嚴重、循環依賴性，組件模型圍繞 models 和 views 進行創建

    React(View)希望在資料更新時，能夠直接重新渲染頁面，不用主動去探究是數據的哪部份發生變化，要對應去更新頁面哪一部分的 DOM。但頁面重新渲染的成本可是更高，所以才需要 Virtual DOM 作為緩衝，透過資料更新後，重新繪製 Virtual DOM，與實體 DOM 進行 Diff，最後再把差異部分 Patch 上去，這不僅修正了重新渲染的成本問題，也降低了 data 與 view 交互更新的複雜度，提高了 developer 的開發體驗。
4. 單向資料流（Unidirectional Data Flow）、一律重繪：
    - Props都是由父元素所傳進來，子元素不能更改
    - State根據使用者互動而產生的不同狀態，主要是透過 setState() 方法進行修改
    - 當 React 發現 props 或是 state 更新時，就會重繪整個 UI
5. Component PropType 防呆機制、在 JavaScript 裡寫 CSS：Inline Style

## 2. 前端庫差別

    語言| React | Angular| Vue |
    --- | --- | --- | ---|
    DOM | V | R | V
    數據綁定 | 單向 | 雙向 | 雙向
    體系結構 | M**V**C | MVC | MVVP
    語言 | JS ES6 | JS ES6 | Typescript

## 3. Life Cycle
- Mounting：組建第一次繪製階段，在這裡完成加載及初始化。
- Updating：根據狀態重新繪製該狀態的圖。
- Unmounting：組建清除階段。
![image](https://github.com/Ccj82378/Interview_QA/blob/main/img/LIfeCycle.png)

## 4. Key
- 定義在 list 中的每個最上層 React element 上
- key 值的型別必須為 string 或 number，且在 list中是唯一值
- 以定義 list 中元素 id 的方式，來提高 render list 效能

## 5. Refs
- 只有 Class Component 能設定 ref 屬性
- 當需要進行 DOM 測量或向組件添加方法時，存儲對特定的 React 元素或組件引用的屬性，它將由組件渲染配置函數返回。
- 像是要 focus 表單欄位、觸發式動畫或第三方DOM庫集成
- 儘量不用，容易破壞元件的獨立性和封裝性，在大多數的情況下，你可以透過傳遞 props 或提升共用狀態來解決你的問題

## 6. Flux & Redux
- Flux是一種強制單向數據流的架構模式，控制數據並使用具有所有數據權限的中心(store)實現多個組件之間的通信。整個應用中的數據更新只能在此處進行
- Redux主要管理 React 複雜的 state 及 action 關係，大幅簡化了 Flux 的概念
- 以一個 root component 集中管理 state ( 通常稱做 store)，需要 store 的 component 就跟 store 連結，有變化就會重繪
- 兩者比較:
    ```
    /* DATA FLOW */
    Flux
    Action -> Dispatcher -> Store -> View
    Redux
    Action -> Reducer -> Store(Redux) -> View
    ```
    Flux|Redux
    --- | ---
    store包含狀態和更改邏輯|store、更改邏輯分開
    多個store|一個store
    狀態可變|狀態不可變

- Redux:

    三大元件：
    - action: 描述發生的事件類別(type屬性)，所承載的資訊(payload)
    - reducer: 一個函式，負責將給定的 state 根據給定的 action 做變化而得到新的 state
    - store: 整個 Redux 運作的核心，負責儲存整個 state tree，每個專案只會有一個 store

    三大原則：
    - 唯一資訊來源：整個專案的 state，被儲存在一個樹狀物件放在唯一的 store 裡面，單一狀態樹可以更容易地跟踪隨時間的變化，並調試或檢查程序
    - State 是唯讀的：改變 state 的唯一的方式是發出一個 action，也就是一個描述發生什麼事的物件。
    - 變更被寫成 pure function：要指定 state tree 如何藉由 action 來轉變，你必須撰寫 pure reducer。

## 7. React Router
- React Router是React的路由解决方案，它可以讓UI可以與URL同步
- Router 用於定義多個路由，當用戶定義特定的 URL 時，如果此 URL 與 Router 內定義的任何 “路由” 的路徑匹配，則用戶將重定向到該特定路由所以基本上我們需要在自己的應用中添加一個 Router。
