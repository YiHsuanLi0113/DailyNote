# Directive Attributes

- `<%@` Page/Control/Import/Register directive

- `<%$` Resource access and Expression building

- `<%=` Explicit output to page, equivalent to `<% Response.Write() %>`

- `<%#` Data Binding. It can only used where databinding is supoorted, or ar the page level if you call `Page.DataBind()` in your code-behind.

- `<%--` Server-side comment block

- `<%:` Equivalent to `<%=`, but it also html-encodes the output.
