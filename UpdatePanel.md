# ASP.NET WebForm - UpdatePanel


引用網址：https://github.com/AhmedMah/ClinicManagement

![Dashboard]()

# UpdatePanel結構

```C#
<asp:ScriptManager ID="ScriptManager1" runat="server">
</asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server" ChildrenAsTriggers="true"
UpdateMode="Always" RenderMode="Block">
  <ContentTemplate>
  </ContentTemplate>
  <Triggers>
    <asp:AsyncPostBackTrigger />
    <asp:PostBackTrigger />
  </Trigger>
</asp:UpdatePanel>
```
- 主要屬性

1. `ChildrenAsTriggers`：內容模板內的子控制元件的回發是否更新本模板
2. `UpdateMode`：內容模板的更新模式，分為Always及Conditional
   - `Always`：每次ajax Postback或一般Postback皆能引發Panel更新。當設定為`Always`時，不能設定`ChildrenAsTriggers`屬性
   - `Conditional`：滿足如下某一條件時才更新Panel內容
      1. 當Panel中某個控制元件引發Postback
      2. 當Panel指定的某個Trigger被引發
      - 設定`UpdateMode="Conditional"` `ChildrenAsTriggers="false"`，子控制元件不能觸發更新
3. `RenderMode`：區域性更新控制元件的呈現形式
   - `Block`：區域性更新在客戶端以`div`形式呈現
   - `Inline`：區域性更新在客戶端以`span`形式呈現

- 子元素

1. `ContentTemplate`：區域性更新控制元件的內容模板，可以在其中新增任何控制元件
2. `Triggers`：區域性更新的觸發器
   - `AsyncPostBackTrigger`：非同步回發，用來實現區域性更新
   - `PostBackTrigger`：一般回發，不管是否使用了區域性更新控制元件，都會引發頁面的全部更新


- 範例

1. UpdatePanel的`UpdateMode="Always"`


```C#
<asp:ScriptManager runat="server">
</asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server" UpdateMode="Always">
  <ContentTemplate>
    <%= DateTime.Now.ToString() %>
    <asp:Button ID="Button1" runat="server" Text="UpdatePanelButton" />
  </ContentTemplate>
 </asp:UpdatePanel>
 <asp:Button ID="Button2" runat="server" Text="Button" />
```
`Button1`及`Button2`皆會觸發更新，差異只在`Button2`會頁面PostBack

2. UpdatePanel的`UpdateMode="Conditional"``ChildrenAsTriggers="false"`

```C#
<asp:ScriptManager runat="server">
</asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server" UpdateMode="Conditional" ChildrenAsTrigger="false">
  <ContentTemplate>
    <%= DateTime.Now.ToString() %>
    <asp:Button ID="Button1" runat="server" Text="UpdatePanelButton" />
  </ContentTemplate>
 </asp:UpdatePanel>
 <asp:Button ID="Button2" runat="server" Text="Button" />
```
`Button1`不觸發更新，`Button2`則會觸發。即UpdatePanel中事件不觸發更新

3. `Trigger`

  - `PostBackTrigger`

```C#
<asp:ScriptManager runat="server">
</asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server" UpdateMode="Always">
  <ContentTemplate>
    <%= DateTime.Now.ToString() %>
    <asp:Button ID="Button1" runat="server" Text="UpdatePanelButton" />
  </ContentTemplate>
  <Triggers>
    <%--<asp:PostBackTrigger ControlID="Button1" />    當子控制元件被觸發時，僅會更新UpdatePanel內資料。若需更新全域性內容，則可以透過PostBackTrigger來實現全域性PostBack--%> 
  </Triggers>
 </asp:UpdatePanel>
 </br>
 <%=DateTime.Now.ToString() %>
 <asp:Button ID="Button2" runat="server" Text="Button" />
```
`Button1`不觸發更新，`Button2`則會觸發。即UpdatePanel中事件不觸發更新


  - `AsyncPostBackTrigger`

```C#
<asp:ScriptManager runat="server">
</asp:ScriptManager>
<asp:UpdatePanel ID="UpdatePanel1" runat="server" UpdateMode="Always">
  <ContentTemplate>
    <%= DateTime.Now.ToString() %>
    <asp:Button ID="Button1" runat="server" Text="UpdatePanelButton" />
  </ContentTemplate>
  <Triggers>
    <asp:AsyncPostBackTrigger ControlID="Button2" EventName="Click" />    
  </Triggers>
 </asp:UpdatePanel>
 </br>
 <%=DateTime.Now.ToString() %>
 <asp:Button ID="Button2" runat="server" Text="Button" />
```
`Button1`及`Button2`皆觸發更新UpdatePanel中內容。
