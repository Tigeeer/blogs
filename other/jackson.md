# Spring Boot 插件 —— Jackson
> 在众多`json`库中，`jackson`是我用过最好用的插件，它不仅仅完美契合`spring mvc`，而且还拥有强大的转换功能。

## 转换示例
首先，创建一个对象`User`

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
}
```

### String to Object

```

```