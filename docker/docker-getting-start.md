Docker 教程（一）—— CentOS 7.2 安装Docker
===
环境
---
```
CentOS 7.2
```
开始
---
1. 更新yum包
`$ yum update`

2. 运行docker安装脚本
`$ curl -fsSL https://get.docker.com/ | sh`

3. 启动服务
`$ systemctl enable docker`

4. 启动docker守护进程
`$ systemctl start docker`

5. 下载镜像
`$ docker pull`