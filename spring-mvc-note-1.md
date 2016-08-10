#Spring MVC笔记——注解篇
参考文档：http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html
###@RequestMapping
用@GetMapping、@PostMapping、@PutMapping、@DeleteMapping、@PatchMapping代替@RequestMapping的method属性
```Java
@Controller
@RequestMapping("/appointments")
public class AppointmentsController {

    @GetMapping
    public Map<String, Appointment> get() {
        // ...
    }

    @GetMapping("/new")
    public AppointmentForm getNewForm() {
        // ...
    }

    @PostMapping
    public String add(@Valid AppointmentForm appointment, BindingResult result) {
        // ...
    }
}
```
###@PathVariable
用@PathVariable注解将URI上的值映射到方法参数
```Java
@GetMapping("/owners/{ownerId}")
public String findOwner(@PathVariable String ownerId, Model model) {
    // ...
}
```
多个@PathVariable注解
```Java
@GetMapping("/owners/{ownerId}/pets/{petId}")
public String findPet(@PathVariable String ownerId, @PathVariable String petId, Model model) {
    // ...
}
```
在URI上使用正则{varName:regex}
```Java
@RequestMapping("/spring-web/{symbolicName:[a-z-]+}-{version:\\d\\.\\d\\.\\d}{extension:\\.[a-z]+}")
public void handle(@PathVariable String version, @PathVariable String extension) {
    // ...
}
```
###@RequestBody
@RequestBody注解表示将请求的主体映射到方法参数上
```Java
@PutMapping("/something")
public void handle(@RequestBody String body, Writer writer) throws IOException {
    // ...
}
```
###@ResponseBody
@ResponseBody注解类似于@RequestBody，表示将返回值直接写入HTTP响应主体，而不会被解释为视图名称（view name）或模型（Model）
```Java
@GetMapping("/something")
@ResponseBody
public String helloWorld() {
    return "Hello World";
}
```
###@SessionAttributes
将Model中key为@SessionAttributes值的属性放到session中，以便全局使用
```Java
@Controller
@RequestMapping("/user")
@SessionAttributes("user")
public class UserForm {

    @RequestMapping("/login")
    public String login(Model model) {
        // create user object
        model.addAttribute("user",user);
        // return
    }
}
```
```Java
@RequestMapping("/")
public String handle(@SessionAttribute User user) {
    // ...
}
```
###@CookieValue
映射cookie值到方法参数
```Java
@RequestMapping("/displayHeaderInfo.do")
public void displayHeaderInfo(@CookieValue("JSESSIONID") String cookie) {
    //...
}
```
###@RequestHeader
映射header属性到方法参数
```Java
@RequestMapping("/displayHeaderInfo.do")
public void displayHeaderInfo(@RequestHeader("Accept-Encoding") String encoding,
        @RequestHeader("Keep-Alive") long keepAlive) {
    //...
}
```


