MySQL基本配置
===
添加远程登录授权
---
`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;`

`FLUSH PRIVILEGES;`
