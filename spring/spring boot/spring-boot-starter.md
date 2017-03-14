# Spring Boot 基础
> `spring boot`是目前最流行的`java`框架，它改变了如何构建企业应用程序以及如何管理它们的方式。`spring boot`帮助开发者去构建应用，而不是去开发应用。在它的背后，是简化配置和部署的过程。

### 关于 Spring Boot
`spring boot`摆脱了配置构建企业应用程序的依赖性所涉及的所有困难。我们知道，`spring`配置加载了大量的`xml`配置文件；现在，所有的配置将交给`spring boot`去处理，我们只需要选择使用哪些插件。

`spring boot`的优势：
* 快速构建应用的开发环境及配置
* 创建独立的应用
* `web`应用能被打包成`FAT-JAR`，作为一个独立应用运行

### 安装说明
你能和使用`java`任何标准库一样的方式去使用`spring boot`，只需要在类路径中包含`spring-boot-*.jar`文件。`spring boot`不需要集成任何特殊工具，因此可以使用任何IDE或文本编辑器; 并且`spring boot`应用没有什么特别之处，因此你可以像任何其他`java`程序一样运行和调试。

#### Gradle安装
`spring boot`兼容`gradle` 2（2.9或更高版本）及`gradle` 3，如果你还没有安装`gradle`，你可以按照 <https://gradle.org/> 的说明进行操作。
`spring boot`依赖项可以使用`org.springframework.boot`组声明。通常，你的项目将声明一个或多个 *starter* 的依赖关系。`spring boot`提供了一个有用的`gradle`插件，可用于简化依赖声明和创建可执行文件。

这是一个典型的`build.gradle`文件

```gradle
plugins {
    id 'org.springframework.boot' version '1.5.1.RELEASE'
    id 'java'
}

jar {
    baseName = 'spring-boot-demo'
    version =  '0.0.1-SNAPSHOT'
}

repositories {
    jcenter()
}

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    testCompile("org.springframework.boot:spring-boot-starter-test")
}
```

### 示例代码
下面，我们将通过一个示例配置并运行`spring boot`

**目录结构**

![图片不见了QAQ](http://127.0.0.1:8081/upload/images/dbb3e82c-1d36-4a4f-9dec-325c8c0e36a4.png)

**build.gradle**

```gradle
group 'com.example'
version '0.1.0'

buildscript {
    repositories {
        mavenCentral()
        jcenter()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.4.2.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'
apply plugin: 'war'

jar {
    baseName = 'example'
    version =  '0.1.0'
}

war {
    baseName = 'example'
    version =  '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile('mysql:mysql-connector-java:6.0.5')
    compile('org.mybatis.spring.boot:mybatis-spring-boot-starter:1.1.1')
    compile('org.springframework.boot:spring-boot-starter-web')

    testCompile('junit:junit:4.12')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}

task wrapper(type: Wrapper) {
    gradleVersion = '3.2'
}
```

添加`mysql`、`mybatis`及`spring-boot-starter-web`依赖。其中，
* `mysql-connector-java`为`mysql`数据库驱动，用于连接`mysql`数据库。
* `mybatis-spring-boot-starter`是`mybatis`开发的基于`spring boot`的类库，这点从`:`前面的`group`可以看出来。
* `spring-boot-starter-web`是`spring boot`构建`web`应用。其中，使用`jackson-databind`构建`RESTful`、使用`hibernate-validator`、`spring-web`、`spring-webmvc`、`spring-boot-starter-tomcat`构建`web`应用及嵌入式`tomcat`，当然，最关键的还是`spring-boot-starter`库，它是`spring boot`的核心，所有的`spring-boot-starter-*`都依赖于它。

**application.properties**

```properties
# datasource
spring.datasource.name=blog
spring.datasource.url=jdbc:mysql://localhost:3306/example?serverTimezone=Asia/Shanghai&characterEncoding=utf8&useSSL=true
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

这是`spring boot`的配置文件，所有的配置都在这一个文件中。当然，你也可以使用其他的文件名，但是必须指定使用哪个文件作为配置文件。不建议这样做，如果有必要，可以自行参考官方文档。在这个文件中，我们配置了*数据源*，这个时候，我们就已经可以连接和操作数据库，而不需要配置其他的`bean`（`xml`或者`java code`）。

**Application.java**

```
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }
}
```

`spring boot`使用`main`方法里面的`SpringApplication.run`来启动应用。`@SpringBootApplication`是一个方便的注解，包括以下功能：
* `@Configuration`定义了应用上下文`bean`的源
* `@EnableAutoConfiguration`告诉`spring boot`基于该路径（该文件所在路径，所以一般放在包的根目录下面）添加`bean`
* `@ComponentScan`用于自动扫描所有的`component`、`configurations`、`service`及`controller`，由于添加了`mybatis`依赖，所以也会自动扫描`mapper`

**User.java**

```
public class User {

    private long id;
    private String name;

    public long getId() {
        return id;
    }

    public void setId(long id) {
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

**UserMapper.java**

```
@Mapper
public interface UserMapper {

    @Insert("INSERT INTO users(name) VALUES(#{user.name})")
    void insert(@Param("user") User user);
}
```

**UserService.java**

```
@Service
public class UserService {

    private UserMapper userMapper;

    public UserService(UserMapper userMapper) {
        this.userMapper = userMapper;
    }

    public void insert() {

    }
}
```

**UserController.java**

```
@RestController
@RequestMapping("/user")
public class UserController {

    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @RequestMapping(method = RequestMethod.GET)
    @ResponseBody
    public User insert(User user) {
        userService.insert(user);

        return user;
    }
}
```

**example.sql**

```
DROP DATABASE IF EXISTS example;
CREATE DATABASE example;
USE example;

DROP TABLE IF EXISTS users;
CREATE TABLE users(
  id             BIGINT                 AUTO_INCREMENT,
  name           VARCHAR(255)  NOT NULL,
  PRIMARY KEY (id)
)
  ENGINE = InnoDB
  DEFAULT CHARSET = utf8;
```

运行应用，在浏览器中打开地址 <http://localhost:8080/user?name=hello>，可以看到浏览器上打印出

```
{"id":1,"name":"hello"}
```

### 结语
其实，`spring boot`将开发者从繁琐的配置和部署中解放出来，开发者只需要少量的配置即可以使用需要的类库，大大提高了开发效率，同时，使项目更容易维护。
### 引用
参考文档 <http://docs.spring.io/spring-boot/docs/current/reference/html>

配置参考文档 <https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html>