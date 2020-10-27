# Other

## 1. AJAX
- Asynchronous非同步：客戶端 (client) 對伺服器端 (server) 送出 request 之後，不需要等待結果，仍可以持續處理其他事情，甚至繼續送出其他 request
- JavaScript：使用的程式語言
- XML：Client 與 Server 交換資料用的資料與方法，近年由於 JSON 等格式的流行，使用 Ajax 處理的資料並不限於 XML。
- 優點: 減少伺服器負擔，回應更即時、網站頁面無需刷新，使用者體驗較好
- 缺點: 只載入第一個網頁，剩下皆動態調整內容

## 2. Cookie
- Cookie 是儲存在瀏覽器的一小段文字資料
    ```
    伺服器--- Set-Cookie header --->瀏覽器(*cookie 儲存)
         <---- 請求回傳 cookie -----
    
    // *Cookie 儲存 => 由於 cookie 會被附加在每一次的 request 之中，可能會影響效能，所以如果是不需要記錄在 server 的資訊，可以改用 storage API
    ```
- 用途: 認證身份、追蹤使用者及廣告

## 3. Single Page Application
