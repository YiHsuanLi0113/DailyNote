# AutoEventWireup

若設定為`true`，則網頁會自動綁定`Page_Load()`的委派事件。即aspx被呼叫時，CodeFile中的`Page_Load()`會被執行
若設定為`false`，則需手動使`Page_Load()`執行。這時需要`override` `Page`類別的`OnInit()`，將Page中的`Load`事件處理常式委派給`Page_Load()`
```C#
public partial class _D
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
