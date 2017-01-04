Docker 教程（二）—— 安装MySQL
===
环境
---
```
CentOS 7.2
```
前提
---
```
1. 已安装docker
2. 开放3306端口
```
开始
---
1. 下载mysql镜像
`$ docker pull mysql`

2. 新建data文件夹
`$ sudo mkdir -p /usr/local/mysql/data`

3. 新建my.cnf文件
`$ sudo vi /usr/local/mysq;/my.cnf`

4. 运行mysql镜像
`$ docker run --name=mysql -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v /usr/local/mysql/data:/var/lib/mysql -v /usr/local/mysql/my.cnf:/etc/mysql/my.cnf mysql`

5. 查看后台是否运行

常见错误
---
#####后台没有运行的容器
1. 交互模式运行容器
`$ docker run --rm -it -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v /usr/local/mysql/data:/var/lib/mysql -v /usr/local/mysql/my.cnf:/etc/mysql/my.cnf mysql`

2. 根据日志排查错误

3. 删除多余的容器并重新运行mysql镜像