Spring Boot + Mybatis教程
===
环境及工具
---
* ######JDK 8
* ######Spring Boot
* ######Gradle

依赖
---
```
compile('mysql:mysql-connector-java:6.0.5')
compile('org.mybatis.spring.boot:mybatis-spring-boot-starter:1.1.1')
compile('org.springframework.boot:spring-boot-starter-web')
```
application.properties配置
---
```
spring.datasource.name=xxx
spring.datasource.url=jdbc:mysql://localhost:3306/xxx
spring.datasource.username=xxx
spring.datasource.password=xxx
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```
代码
---
####User.java
```java
package com.example.pojo;

/**
 * Created by tigeeer on 2016/10/12.
 */
public class User {
	private int id;
    private String name;
}
```
####UserMapper.java
```java
package com.example.mapper;

import com.example.pojo.User;
import org.apache.ibatis.annotations.*;

/**
 * Created by tigeeer on 2016/10/12.
 */
@Mapper
public interface UserMapper {
	@Insert("INSERT INTO user(id, name) VALUES(#{user.id}, #{user.name})")
    void insert(@Param("user") User user);
}
```
UserService.java
---
```java
package com.example.services;

import com.xjgex.mapper.UserMapper;
import com.xjgex.pojo.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

/**
 * Created by tigeeer on 2016/10/12.
 */
@Service
public class UserService {
	@Autowired
    private UserMapper userMapper;
    
    public void insert(User user) {
    	userMapper.insert(user);
    }
}
```
解析
---
* #####User.java
	- ######实体类
	- ######对应表结构
* #####UserMapper.java
	- ######@Mapper —— 声明Mapper,注册Bean
	- ######@Insert, @Update, @Select, @Delete —— 声明语句类型，只有一个value参数为默认参数，在里面写sql语句
	- ######@Param —— 参数别名，在#{}或${}中使用
* #####UserService.java
	- ######服务类
	- ######@Autowired —— 自动注入Bean

注解及技巧
---
* ######@Options(useGeneratedKeys = true, keyProperty = "") —— 将主键作为返回值赋值给keyProperty，与@Insert配合使用
* ######@Result —— 转换表字段与类变量，与@Select配合使用


