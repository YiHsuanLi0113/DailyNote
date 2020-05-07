# Delegate

```C#
public partial class _Default : Page
{
  protected void Page_Load(object sender, EventArgs e)
  {
    arithmetic ari = null; //宣告委派
    
    string fun = "/";
    switch(fun)
    {
      // 將方法指派給「ari」
      // new arithmetic(this.add); 為實作委派
      case "+":
        ari = new arithmetic(this.add);
        break;
      case "-":
        ari = new arithmetic(this.substract);
        break;
      case "*":
        ari = new arithmetic(this.multiply);
        break;
      case "/":
        ari = new arithmetic(this.devide);
        break;
    }
    
    int answer = ari(6, 3); // 答案為2
    int answer1 = ari.Invoke(6, 3); //答案為2，與ari(6, 3)相同
  }
  
  // 這些方法必須要和定義委派類型相同，此例中即必須return int，有兩個int參數
  private int add(int a, int b)
  {
    return a + b;
  }
  
  private int substract(int a, int b)
  {
    return a - b;
  }
  
  private int substract(int a, int b)
  {
    return a * b;
  }
  
  private int devide(int a, int b)
  {
    return a / b;
  }
  
  delegate int arithmetic(int num1, int num2); //定義委派類型
}
```
