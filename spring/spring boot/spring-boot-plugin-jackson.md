# Spring Boot 插件 —— Jackson
> 在众多`json`库中，`jackson`是我用过最好用的插件，它不仅完美契合`spring mvc`，而且还拥有强大的转换功能。

## 转换示例
首先，创建一个`User`对象

```
public class User {

    private int id;
    private String name;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
            "id=" + id +
            ", name='" + name + '\'' +
            '}';
    }
}
```

创建`Application.java`

```
@SpringBootApplication
public class Application implements CommandLineRunner {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }

   @Override
   public void run(String... strings) throws Exception {
      ObjectMapper objectMapper = new ObjectMapper();
   }
}
```

以下代码放在`run`方法下。
### Object to String

```
User user1 = new User();
user1.setId(1);
user1.setName("user1");

System.out.println(objectMapper.writeValueAsString(user1));
```

运行程序，控制台输出：

```
{"id":1,"name":"user1"}
```

### String to Object

```
String json = "{\"id\": 1, \"name\": \"Tom\"}";
User user = objectMapper.readValue(json, User.class);

System.out.println(user);
```

运行程序，控制台输出：

```
User{id=1, name='Tom'}
```

### String to T
将`string`转换为泛型对象时，需要使用`TypeReference`，例如`List`、`Map`等。

**错误示例**

```
String jsonArray = "[{\"id\": 1, \"name\": \"Tom\"}]";
LinkedList<User> users = objectMapper.readValue(jsonArray, LinkedList.class);

User user2 = users.get(0);

System.out.println(user2);
```

虽然`string`能够被转换为`List`，但是，集合里的对象并不是`User`类型，而是`LinkedHashMap`类型。所以，转换为`User`对象时会抛出异常。

**正确示例**

```
String jsonArray = "[{\"id\": 1, \"name\": \"Tom\"}]";
LinkedList<User> users = objectMapper.readValue(jsonArray, new TypeReference<LinkedList<User>>() {});
User user2 = users.get(0);

System.out.println(user2);
```

### 结语
`jackson`不仅仅能转换`string`，还能转换`File`、`I/O Stream`等。

### 引用
参考文档 <http://wiki.fasterxml.com/JacksonInFiveMinutes>