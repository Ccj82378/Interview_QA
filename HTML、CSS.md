# HTML、CSS

## display:inline、block、inline-block
- `block`：塊級元素默認填滿父級元素內容區域，旁邊不能有其他元素，ex `<div>`, `<p>`, `<ul>` 
- `inline`：行內元素在一行文本內生成元素框，不打斷所在的行，ex `<span>`, `<img>`, `<a>`
- `inline-block`：屬性是行內屬性，可以設置width和height或者我們可以理解成一個塊級元素，不用換行
![image](https://github.com/Ccj82378/Interview_QA/blob/main/img/css-display-block-vs-inline-block.png)

## Pseudo classes
- 偽類: 能夠在特定動作時改變 DOM 的 CSS 樣式，ex `:hover`, `:focus`
- 偽元素: 
    - 基於原有的 DOM ，創建另一個可設定不同 CSS 的 DOM 屬性，ex `::before`,`::after` 
    - 會繼承原本元素的屬性，如果原本文字是黑色，偽元素的文字也會是黑色

## CSS Preprocessor
- 彌補 CSS 在大型專案維護性的不足，CSS 預處理器中新增了變數、混入、繼承、嵌套等寫法，讓開發者可以更有結構地撰寫簡潔、清晰且好維護的 CSS 程式碼
- 主流有Sass/SCSS、Less、Stylus
- 特性：變數（Variables）、函式（Functions）、嵌套（Nesting）、混入（Mixins）、共用（Extends）