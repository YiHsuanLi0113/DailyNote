# AutoEventWireup

若設定為`true`，則網頁會自動綁定`Page_Load()`的委派事件。即aspx被呼叫時，CodeFile中的`Page_Load()`會被執行
若設定為`false`，則需手動使`Page_Load()`執行。這時需要`override` `Page`類別的`OnInit()`，將Page中的`Load`事件處理常式委派給`Page_Load()`
```C#
public partial class _Default:System.Web.UI.Page
{
  protected void Page_Load(object sender, EventArgs e)
  {
    Label1.Text - this.IsPostBack.ToString();
  }
  
  protected override void OnInit(EventArgs e)
  {
    this.Load += new EventHandler(this.Page_Load);
  }
}
```
預設為`false`。若要改變預設值，可於`Web.config`的`<system.web>`中，加上`<pages>`設定
```C#
<configuration>
  <system.web>
    <compilation debug="false" targetFramework="4.0" />
    <pages autoEventWireup="true" />
  </system.web>
</configuration>
```

# CodeFile

ASP.NET WebForm預設Code-Seperation開啟，將視覺的`.aspx`及邏輯的`.aspx.cs`分開。用到的是class中的`partial`，即反應在`@Page`的`CodeFile`屬性中

# Language

在編譯所有內嵌轉譯`<%%>`和`<%=%>`與網頁內的程式碼宣告區塊時所使用的語言。值可為任何.NET Framework支援的語言(Visual Basic、C#、JScript)。每個網頁只能指定一種語言

# Inherits

定義網頁要繼承的程式碼後置類別

# EnableViewState

伺服器利用ViewState端儲存了網頁各個控制元件及頁面的狀態，_VIEWSTATE屬性其值為一長串字元，型別為hidden，用以記錄各個控制元件和頁面的狀態。當使用者對頁面進行相關操作，狀態值發生改變，並將改變的值傳遞給Server端。
一旦頁面的控制元件很多，這種頻繁的傳遞控制元件狀態值對網路對消耗很大，因此ASP.NET提供EnableViewState屬性，預設值為true。當設定為true，在傳遞狀態值時就包含該控制元件；反之。既然狀態值不包含該控制元件，則Client端對它進行的操作，Server端是不響應的。
好處是某些控制元件不需要接受使用者操作或只需要接受一次操作時，可以將這些控制元件的EnableViewState設為false，以優化程式，提高網路訪問速度。

# MasterPageFile

XXX

# MaintainScrollPositionOnPostback

XXX

# ValidateRequest

XXX

# HttpRequestValidationException

XXX

# Trace
