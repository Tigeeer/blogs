#Java 8 —— 默认方法
`Java 8`介绍了一种新的概念，接口实现默认方法。此功能增加了向后兼容性，因此旧的接口也可以使用`Java 8`的`Lambda`表达式。比如，`List`和`Collection`接口没有声明`foreach`方法，因此，添加这样的方法会简单地打破集合框架的实现。`Java 8`引入了默认的方法使`List/Collection`接口可以拥有的`forEach`方法的默认实现，以及实现这些接口的类不需要实现相同。
###语法
```Java
public interface vehicle {
   default void print(){
      System.out.println("I am a vehicle!");
   }
}
```
