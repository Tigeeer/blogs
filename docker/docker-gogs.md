Docker 教程（三）—— 安装Gogs
===
环境
---
```
CentOS 7.2
```
依赖
---
```
1. 已安装docker
2. 已安装mysql
3. 开放10022,10080端口
```
开始
---
1. 下载gogs镜像
`$ docker pull gogs/gogs`

2. 新建gogs文件夹
`$ sudo mkdir -p /var/gogs`

3. 运行mysql镜像
`$ $ docker run --name=gogs-mysql -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v /usr/local/mysql/data:/var/lib/mysql -v /usr/local/mysql/my.cnf:/etc/mysql/my.cnf mysql`

4. 运行gogs镜像连接mysql
`$ docker run --name=gogs -p 10022:22 -p 10080:3000 -v /var/gogs:/data --link gogs-mysql:mysql gogs/gogs`

5. 新建gogs数据库

6. 在浏览器输入 http://ip:10080 打开gogs

常见问题
---
#####运行mysql镜像出错
[Docker教程（二）—— 安装MySQL](http://example.com)