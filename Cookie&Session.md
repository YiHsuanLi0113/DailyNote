# Cookie

1. 通常用以記錄對網站的個人喜好設定
2. `Cookie`以明碼方式傳送，機密資料不建議以此方式儲存
3. 資料存放於Client端，不會造成Server端過載
4. 存於Client端的`Cookie`，不會因為瀏覽器關閉而消失(直到時效失效為止)
5. 多應用於購物車的購買紀錄、記住帳號密碼

- `Cookie`是HTTP協議的一部分，處理步驟如下
  1. Server向Client端發送Cookie
  2. 瀏覽器將Cookie保存於電腦的資料夾中
  3. 每次請求，瀏覽器都會將符合的Cookie送至Server端
  
- Cookie可選參數
  - `path` : 
  - `expires`及`maxAge` : 告訴瀏覽器Cookie何時過期。expires為UTC格式時間，maxAge為Cookie多久後過期的相對時間。若無設定這兩個參數，會產生Session Cookie，Session Cookie為短暫的，當用戶關閉瀏覽器就會被清除，一般用來保存Session ID 
  - `secure` : 當`Secure`為`true`，Cookie在HTTP無效，在HTTPS中才有效
  - `httpOnly` : 瀏覽器不允許腳本操作`document.cookie`去更改Cookie。一般狀況下都應設置為`true`以避免被XSS攻擊取得Cookie

# Session

1. `Session`主要儲存於Server端，安全性高
2. 主要紀錄在Web Server上的使用者訊息
3. `Session`於伺服器端不會自動失效，除非已超過設置的失效時間
4. `Session`機制會在一個用戶完成身分認證後，存下所需的用戶資料，, 接著產生一組對應的ID，存入`Cookie`後傳回Client端
5. 多應用於網站計數器、登入驗證、使用者上次到訪日期
