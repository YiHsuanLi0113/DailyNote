# Directive Attributes

- `<%@` Page/Control/Import/Register [directive](https://docs.microsoft.com/en-us/previous-versions/aspnet/t8syafc7(v=vs.100)?redirectedfrom=MSDN)

- `<%$` [Resource](https://docs.microsoft.com/en-us/previous-versions/ms227427(v=vs.140)?redirectedfrom=MSDN) access and [Expression](https://docs.microsoft.com/en-us/previous-versions/d5bd1tad(v=vs.140)?redirectedfrom=MSDN) building

- `<%=` Explicit output to page, equivalent to `<% Response.Write() %>`

- `<%#` [Data Binding.](https://docs.microsoft.com/en-us/previous-versions/ms178366(v=vs.140)?redirectedfrom=MSDN) It can only used where databinding is supoorted, or ar the page level if you call `Page.DataBind()` in your code-behind.

- `<%--` [Server-side comment](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/4acf8afk(v=vs.100)?redirectedfrom=MSDN) block

- `<%:` Equivalent to `<%=`, but it also [html-encodes the output](https://weblogs.asp.net/scottgu/archive/2010/04/06/new-lt-gt-syntax-for-html-encoding-output-in-asp-net-4-and-asp-net-mvc-2.aspx).
