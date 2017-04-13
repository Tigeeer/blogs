Spring Security 详解
===
基本配置
---
```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    private CustomAuthenticationProvider customAuthenticationProvider;

    @SuppressWarnings("SpringJavaAutowiringInspection")
    public WebSecurityConfig(CustomAuthenticationProvider customAuthenticationProvider) {
        this.customAuthenticationProvider = customAuthenticationProvider;
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf()
            .disable()
//            .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
            .authorizeRequests()
            .antMatchers("/", "/home").permitAll()
            .anyRequest().authenticated()
            .and()
            .formLogin()
            .loginPage("/login")
            .permitAll()
            .and()
            .logout()
            .permitAll();
    }

    @Autowired
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.authenticationProvider(customAuthenticationProvider);
    }

    @Bean
    public CustomUsernamePasswordAuthenticationFilter customUsernamePasswordAuthenticationFilter()
        throws Exception {
        CustomUsernamePasswordAuthenticationFilter customUsernamePasswordAuthenticationFilter = new CustomUsernamePasswordAuthenticationFilter();
        customUsernamePasswordAuthenticationFilter
            .setAuthenticationManager(authenticationManagerBean());
        customUsernamePasswordAuthenticationFilter.
            setAuthenticationSuccessHandler(new CustomAuthenticationSuccessHandler());
        customUsernamePasswordAuthenticationFilter.
            setAuthenticationFailureHandler(new CustomAuthenticationFailureHandler());

        return customUsernamePasswordAuthenticationFilter;
    }

    @Bean
    @Override
    public AuthenticationManager authenticationManagerBean() throws Exception {
        List<AuthenticationProvider> authenticationProviderList = new LinkedList<>();
        authenticationProviderList.add(customAuthenticationProvider);

        return new ProviderManager(authenticationProviderList);
    }
}

```
