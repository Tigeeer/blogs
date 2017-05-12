# RabbitMQ 部署

## 添加virtual host
`add_vhost {vhost}`

`add_vhost test`

## 添加用户
`add_user {username} {password}`

`add_user tiger password `

## 设置用户tag
`set_user_tags {username} {tag ...}`

`rabbitmqctl set_user_tags tiger administrator`

## 设置权限
`set_permissions [-p vhost] {user} {conf} {write} {read}`

`rabbitmqctl set_permissions -p test tiger ".*" ".*" ".*"`
