# OnClientClick

為前台觸發事件，會搶在`OnClick`執行前優先執行。
  1. 適合在提交數據到後台之前，檢查數據是否符合提交範圍，若不符合，則後台提交事件`OnClick`不會執行
  2. 亦適用於提交前，讓按鈕無法被點選，提交到後台，待方法執行完畢，再讓按鈕恢復可點選狀態
  
若是透過JavaScript Function，則必須回傳`bool`值。當OnClientClick回傳`true`，程式會自動執行OnClick事件；反之，不執行 

# this

代表目前類別

```C#
public  class ClassA
{
  string dataA = "World";
  
  public void Test(string dataA)   //假設dataA = "Hello"
  {
      System.Console.WriteLine(dataA);       //顯示 Hello
      System.Console.WriteLine(this.dataA);  //顯示 World
  }
}
```

# base 

代表父類別

```C#
class ParentClass
{
  virtual void FunctionA() {
    System.Console.WriteLine("ParentClassFunction");
  }
  
  class ChildClass: ParentClass
  {
    public override void FunctionA() {
      System.Console.WriteLine("ChildClassFunction");
    }
    
    public void FunctionB() 
    {
      base.FunctionA(); //顯示 ParentClassFunction
      FunctionA();      //顯示 ChildClassFunction
      this.FunctionA(); //顯示 ChildClassFunction
    }
  }
}
```

- 代表父類別的建構函式

```C#
class ParentClass
{
  public ParentClass() {
    System.Console.Write("ParentClass");
  }
}

class ChildClass: ParentClass
{
  public ChildClass(): base()
  {
    System.Console.Write("ChildClass"); //顯示 ParentClass ChildClass
  }
}
```

- 代表父類別的建構函式，並帶參數

```C#
class ParentClass
{
  public ParentClass() {System.Console.Write("ParentClassA");}
  public ParentClass(string parameterA) {System.Console.Write("ParentClassB");}
}

class ChildClass: ParentClass
{
  public ChildClass(string parameterA): base(parameterA)
  {
    System.Console.Write("ChildClass"); //顯示 ChildClass ParentClassB
  }
}
```
