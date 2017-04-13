Java 8 常用示例
===

###集合

**List排序**

```
List<User> user = new ArrayList<>(); // user拥有name属性,对name进行排序。
user.sort(Comparator.comparing(User.getName));
```
