# RegisterClientScriptBlock

將JavaScript註冊到Client端的`<form>`之下

# RegisterStartupScript

將JavaScript註冊到Client端的`</form>`之上

# Response.Write

註冊於`<html>`之上
 - 不建議使用，會使WebForm的CSS失去作用，有UpdatePanel時會有js error


```C#
protected void Page_Load(object sender, EventArgs e)
{
  Page.ClientScript.RegisterClientScriptBlock(this.GetType(), "ScriptBlock", "alert('RegisterClientScriptBlock OK')", true);
  Page.ClientScript.RegisterStartupScript(this.GetType(), "StartupScript", "alert('RegisterStartupScript OK')", true);
  Response.Write("<script>alert('Response.Write OK')</script>");
}
```

執行後結果：

1. Response.Write OK
2. RegisterClientScriptBlock OK
3. RegisterStartupScript OK

![Dashboard](https://github.com/YiHsuanLi0113/DailyNote/blob/master/Images/registerscript.JPG)
