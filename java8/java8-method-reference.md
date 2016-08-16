#Java 8 —— 方法引用
方法引用通过方法名指向方法，一个方法引用被声明使用::（双冒号）符号，一个方法引用能被使用去指向以下类型方法：
* 静态方法（Static methods）
* 实例方法（Instance methods）
* 构造方法 —— 使用new操作符（TreeSet::new）

#####Java8Tester.java
```Java
import java.util.List;
import java.util.ArrayList;

public class Java8Tester {
   public static void main(String args[]){
      List names = new ArrayList();

      names.add("Mahesh");
      names.add("Suresh");
      names.add("Ramesh");
      names.add("Naresh");
      names.add("Kalpesh");

      names.forEach(System.out::println);
   }
}
```
输出：
```
Mahesh
Suresh
Ramesh
Naresh
Kalpesh
```
在这里，我们通过System.out::println作为一个静态方法引用。
###总结
* 方法引用
