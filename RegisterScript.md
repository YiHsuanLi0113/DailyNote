# RegisterClientScriptBlock

# RegisterStartupScript

# Response.Write


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
