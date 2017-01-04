Spring Security（一）—— 基础
===

依赖
---
```java
compile("org.springframework.boot:spring-boot-starter-security")
```
基本配置
---
```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .loginPage("/login")
                .permitAll()
            	.and()
            .logout()
            .permitAll();
	}
}

```