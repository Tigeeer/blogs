#Java 8 —— 方法引用
方法引用通过方法名指向方法，使用`::`（双冒号）声明方法引用，方法引用能指向以下类型方法：
* 静态方法`Static methods`
* 实例方法`Instance methods`
* 构造方法`Constructor methods` —— 使用`new`操作符`TreeSet::new`

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
在这里，我们通过`System.out::println`引用了一个静态方法。