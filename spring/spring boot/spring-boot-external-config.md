# Spring Boot 外部配置
> 顾名思义，外部配置的主要目的是将外部配置文件转换为`pojo`并声明成`bean`。一般，我们会使用`properties`或者`YAML`来作为配置文件，并将它们放在`resources`目录下。

### 基本功能
假设，我们正在开发微信公众号，需要使用一些微信公众号后台的参数，比如：`token`、`appid`、`secret`等。

首先，创建配置文件`wx.properties`

```
wx.token=springbootdemo
wx.appid=wx123456
wx.secret=xxxxxxxxxxx
```

然后，创建`WxConfig.java`

```
@Configuration
@EnableAutoConfiguration
@PropertySource(value = {"classpath:wx.properties"})
@ConfigurationProperties(prefix = "wx")
public class WxConfig {

    private String token;

    @Value(value = "${wx.appid}")
    private String appId;

    private String secret;

    public String getToken() {
        return token;
    }

    public void setToken(String token) {
        this.token = token;
    }

    public String getAppId() {
        return appId;
    }

    public void setAppId(String appId) {
        this.appId = appId;
    }

    public String getSecret() {
        return secret;
    }

    public void setSecret(String secret) {
        this.secret = secret;
    }
}
```

在这个文件中，使用了三个新注解：
* `@PropertySource`，指定配置文件的路径。
* `@ConfigurationProperties`，对字段的配置。`prefix`属性指定了前缀。
* `@Value`，字段映射。仔细看会发现，字段`appid`在`pojo`里面的属性名为`appId`，所以无法自动映射，需要手动指定字段。

最后，可以在其他类中使用`WxConfig`。

```
@SpringBootApplication
public class Application implements CommandLineRunner {

    private WxConfig wxConfig;

    public Application(WxConfig wxConfig) {
        this.wxConfig = wxConfig;
    }

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Override
    public void run(String... strings) throws Exception {
        System.out.println(wxConfig.getToken());
        System.out.println(wxConfig.getAppId());
        System.out.println(wxConfig.getSecret());
    }
}
```

运行程序，控制台会打印出

```
springbootdemo
wx123456
xxxxxxxxxxx
```

### 字段集合
现在，我们需要添加`ip白名单`集合。

修改`wx.properties`，添加`ip`字段

```
wx.ip[0]=192.168.1.1
wx.ip[1]=192.168.1.2
```

修改`WxConfig.java`，添加`ip`属性（`get/set`省略）

```
private List<String> ip;
```

**经过测试，集合无法使用`@Value`注解，版本`1.4.2`。**

修改`Application.java`，打印`ip`属性

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
}public class User {

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
}public class User {

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
}public class User {

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

运行程序，控制台会打印出

```
192.168.1.1
192.168.1.2
```

### 结语
使用外部配置可以更方便的管理项目，它使用的场景介于`static`变量和数据库之间。

### 引用
参考文档 <https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html>


