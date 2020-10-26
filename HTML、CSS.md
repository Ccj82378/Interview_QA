# HTML、CSS

## 1. Display:inline、block、inline-block
- `block`：塊級元素，前後換行，ex `<div>`, `<p>`, `<ul>` 
- `inline`：行內元素在一行文本內生成元素框，不打斷所在的行，ex `<span>`, `<img>`, `<a>`
- `inline-block`：屬性是行內屬性，可以設置width和height或者我們可以理解成一個塊級元素，不用換行
![image](https://github.com/Ccj82378/Interview_QA/blob/main/img/css-display-block-vs-inline-block.png)

## 2. Pseudo classes
- 偽類: 能夠在特定動作時改變 DOM 的 CSS 樣式，ex `:hover`, `:focus`
- 偽元素: 
    - 基於原有的 DOM ，創建另一個可設定不同 CSS 的 DOM 屬性，ex `::before`,`::after` 
    - 會繼承原本元素的屬性，如果原本文字是黑色，偽元素的文字也會是黑色

## 3. CSS Preprocessor
- 彌補 CSS 在大型專案維護性的不足，CSS 預處理器中新增了變數、混入、繼承、嵌套等寫法，讓開發者可以更有結構地撰寫簡潔、清晰且好維護的 CSS 程式碼
- 主流有Sass/SCSS、Less、Stylus
- 特性：變數（Variables）、函式（Functions）、嵌套（Nesting）、混入（Mixins）、共用（Extends）

## 4. Position
- 指定用於元素定位的方式，`static` `relative` `fixed` `absolute` `sticky` 接著使用 `top` `bottom` `left` `right` 屬性定位元素，但除非先設置 position 屬性，否則這些元素將不起作用
- static:
    任何套用 `position: static` 的元素「不會被特別定位」在頁面上特定位置，此時 `top` `right` `bottom` `left` `z-index`皆無效
- relative:
    在一個設定為 `position: relative` 內設定 `top` `right` `bottom` `left` 屬性，會使其元素「相對地」調整其原本該出現的所在位置，而不管這些「相對定位」過的元素如何在頁面上移動位置或增加了多少空間，都不會影響到原本其他元素所在的位置
- absolute: 
    `position: absolute` 的定位是在他所處上層容器的相對位置。如果這個套用此的元素，其上層容器並沒有「可以被定位」的元素的話，那麼這個元素的定位就是相對於該網頁所有內容（也就是 `<body>` 元素）最左上角的絕對位置，看起來就是這張網頁的絕對位置一樣，所以當畫面在捲動時，該元素還是會隨著頁面捲動
- fixed: 
    `position: fixed` 會相對於瀏覽器視窗來定位，即便頁面捲動，還是會固定在相同的位置
- sticky:
    根據滾動位置從 `relative` 到 `fixed` ，註:Internet Explorer、Edge 15及更早期版本不支援

## 5. Overflow
- 處理 block box 內容溢出時的顯示狀態，顯示在 box 外的內容是否裁減，以及裁剪後是否提供滑動顯示
    - visible：內容沒有被裁切，也就是可以在 block box 外呈現
    - hidden：內容被裁切，並且不應提供捲動 UI 來查看裁切區域之外的內容
    - scroll：內容已被裁切，並且如果 UA 使用螢幕上可見的捲動機制 (例如：scroll bar 或 panner)，則無論該內容是否有內容，都應在 box 上顯示該機制被裁切。這避免了滾動條在動態環境中出現和消失的任何問題。指定此值且目標 medium 為 print 時，可能會列印出 overflow 的內容。在 table box 上使用時，此值與 visible 具有相同的含義
    - auto：此值的行為取決於 UA，但應導致為 overflow 的 box 提供捲動機制。在 table box 上使用時，此值與 visible 具有相同的含義

## 6. CSS Specificity
- 行內套用 > 內部載入 > 外部載入 > 用戶設置 > 瀏覽器預設