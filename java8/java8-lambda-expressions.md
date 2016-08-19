#Java 8 —— Lambda表达式
`Lambda`表达式被`Java 8`引入并且被认为是`Java 8`中最强大的功能。`Lambda`表达式有助于函数式编程，并且大大简化了开发。
###语法
`Lambda`表达式的语法如下：
```
parameter -> expression body
```
以下是`Lambda`表达式最重要的特征：
* 可选的类型声明 —— 不需要声明参数的类型，编译器能根据参数的值推断出类型。
* 可选的括号 —— 不需要将参数声明在括号里。如果有多个参数，括号还是必须的。
* 可选的大括号 —— 如果表达式的主体只包含一个语句则不需要使用大括号。
* 可选的`return`关键字 —— 如果表达式的主体只包含一个表达式，编译器能自动返回值；如果在大括号里则必须指定返回值。

###范例
#####Java8Tester.java
```Java
public class Java8Tester {
   public static void main(String args[]){
      Java8Tester tester = new Java8Tester();

      //with type declaration
      MathOperation addition = (int a, int b) -> a + b;

      //with out type declaration
      MathOperation subtraction = (a, b) -> a - b;

      //with return statement along with curly braces
      MathOperation multiplication = (int a, int b) -> { return a * b; };

      //without return statement and without curly braces
      MathOperation division = (int a, int b) -> a / b;

      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));

      //with parenthesis
      GreetingService greetService1 = message ->
      System.out.println("Hello " + message);

      //without parenthesis
      GreetingService greetService2 = (message) ->
      System.out.println("Hello " + message);

      greetService1.sayMessage("Mahesh");
      greetService2.sayMessage("Suresh");
   }

   interface MathOperation {
      int operation(int a, int b);
   }

   interface GreetingService {
      void sayMessage(String message);
   }

   private int operate(int a, int b, MathOperation mathOperation){
      return mathOperation.operation(a, b);
   }
}
```
输出：
```
10 + 5 = 15
10 - 5 = 5
10 x 5 = 50
10 / 5 = 2
Hello Mahesh
Hello Suresh
```
通过上面的例子需要考虑以下问题：
* `Lambda`表达式主要用于定义一个功能接口的内联实现，即只有一个方法的接口。在上面的例子中，我们使用各种类型`Lambda`表达式定义`MathOperation`接口中的`operation`方法。然后我们实现了`GreetingService`接口的`sayMessage`方法。
* `Lambda`表达式消除了匿名类的需要，并且给予了`Java`一种简单但是强大的函数式编程能力。

###作用域
使用`Lambda`表达式，你能引用`final`变量或有效的`final`变量（只被分配一次）。如果一个变量被分配两次值，`Lambda`表达式将抛出一个编译错误。
#####Java8Tester.java
```Java
public class Java8Tester {

   final static String salutation = "Hello! ";

   public static void main(String args[]){
      GreetingService greetService1 = message ->
      	System.out.println(salutation + message);
      greetService1.sayMessage("Mahesh");
   }

   interface GreetingService {
      void sayMessage(String message);
   }
}
```
输出：
```
Hello! Mahesh
```
