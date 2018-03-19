Spring Boot Web 工具
===
RestTemplate
---

`Rest`风格`http`请求工具

**泛型转换**
```
Response<User> response = new RestTemplate().exchange(url, HttpMethod.GET, null, new ParameterizedTypeReference<Response<User>>() {}).getBody();
```
