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
  
  每次瀏覽器請求網頁時，會一併將Cookie的資訊傳送到Server端
  ![Dashboard](https://github.com/YiHsuanLi0113/DailyNote/blob/master/Images/requestCookie.JPG)
  
  當Server端將網頁回傳給瀏覽器時，透過`Set-Cookie`這個Header來告訴Client端需要在瀏覽器中加入一或多個Cookie，並且記錄該Cookie的隸屬網域(Domain)、存放目錄(Path)、過期時間(Expires)等資訊
  ![Dashboard](https://github.com/YiHsuanLi0113/DailyNote/blob/master/Images/responseCookie.JPG)
  假設瀏覽器取得某網頁，且包含了5個CSS及2個JavaScript檔案，在這一次的Request中就會將相同的Cookie送出7次。
  
- Cookie限制
  基於RFC2965規範，定義了瀏覽器對於Cookie的最低儲存量
  1. 每個Cookie所能存放的大小為 4096 Bytes
  2. 每個網域至少可以儲存20個Cookie，若儲存超過限制大小，瀏覽器會捨棄最舊的Cookie
  3. 至少能儲存300個Cookie

- Cookie可選參數
  - `Path` : 限制該Cookie僅能由某個資料夾或應用程式存取
  
    Ex. 點部落網址為 www.dotblogs.com.tw ，若我們將`Path`設定為`/Web1`，則代表僅在 www.dotblogs.com.tw/Web1 這個網站底下的網頁才能使用該Cookie；若無設定則預設為`/`根目錄，代表該網域底下的所有網站都能取得該Cookie
  - `Domain` : 限制Cookie的網域範圍
  
    PS. 一般SSO(Single Sign-On)機制也會利用設定網域的方式來讓不同子網域的網站也能存取到同一個Cookie，以達到跨網域登入
    
    PS. 不能設定和自己不同的網域，ex. www.dotblogs.com.tw 的網站在設定Cookie時不能指定 facebook.com的Cookie
  - `Expires`及`maxAge` : 告訴瀏覽器Cookie何時過期。expires為UTC格式時間，maxAge為Cookie多久後過期的相對時間。若無設定這兩個參數，會產生Session Cookie，Session Cookie為短暫的，當用戶關閉瀏覽器就會被清除，一般用來保存Session ID 
  - `Secure` : 當`Secure`為`true`，Cookie在HTTP無效，在HTTPS中才有效
  - `HttpOnly` : 瀏覽器不允許腳本操作`document.cookie`去更改Cookie。一般狀況下都應設置為`true`以避免被XSS攻擊取得Cookie
  
- 利用ASP.NET來操作Cookie
  1. 新增Cookie，並設定值
     ```C#
     HttpCookie TheCookie = new HttpCookie("UserInfo"); //新增Cookie名稱為UserInfo
     TheCookie.Value = "Ellen"; //設定Cookie值
     Response.Cookies.Add(TheCookie);
     ```
  2. 取得從瀏覽器送過來的Cookie
     ```C#
     if (Request.Cookies["UserInfo"] != null)
     {
      var UserName = Request.Cookies["UserInfo"].Value;
     }
     ```
  3. 更新Cookie的到期時間
     ```C#
     if (Request.Cookies["UserInfo"] != null)
     {
      Request.Cookies["UserInfo"].Expires = DateTime.Now.AddHours(1);
     }
     ```
  4. 刪除瀏覽器的Cookie
     ```C#
     // 1. 將Cookie的到期時間設定為昨天即可移除
     Request.Cookies["UserInfo"].Expires = DateTime.Now.AddDays(-1);
     // 2. 利用Remove方法移除Cookie
     Request.Cookies.Remove("UserInfo");
     ```
  5. 建立一個含有多個值的Cookie
     ```C#
     HttpCookie TheCookie = new HttpCookie("UserInfo");
     TheCookie.Values["Name"] = "Ellen";
     TheCookie.Values["Language"] = "zh-TW";
     Response.Cookies.Add(TheCookie);
     ```

# Session

1. `Session`主要儲存於Server端，安全性高
2. 主要紀錄在Web Server上的使用者訊息
3. `Session`於伺服器端不會自動失效，除非已超過設置的失效時間
4. `Session`機制會在一個用戶完成身分認證後，存下所需的用戶資料，, 接著產生一組對應的ID，存入`Cookie`後傳回Client端
5. 多應用於網站計數器、登入驗證、使用者上次到訪日期

- Session Store
1. 內存 : Memory Store，有Memory Leak的風險。適合用於開發環境
2. Cookie : 配合Signed Cookie，但這個方法會讓Request傳輸量變大
   
   假設現在的Cookie資料為
   ```C#
   { _dotcom_user: 'jcc'}
   ```
   搭配一段秘密字串`this_is_the_secret_hash`來做SHA1
   ```C#
   var r = SHA1('this_is_the_secret_hash' + 'jcc');
   ```
   最後回傳至Client端的Cookie為
   ```C#
   {
    dotcom_user: 'jcc',
    'dotcom_user.sig': 'd01a3d595af33625be4159de07a20b79a1540e54'
   }
   ```
   這時候Client端異動了Cookie資料，但因為不知道秘密字串為何，故無法產生正確的hash值。如此一來就避免了被竄改Cookie的可能
3. 緩存 : 常見的有redis、memcache
4. 資料庫 : 不適用

