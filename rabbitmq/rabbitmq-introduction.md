# RabbitMQ 介绍
< P = Producer, C = Consumer, Q = Queue, EX = Exchange, RK = RoutingKey

## Queue
当`P`发布消息，`Q`会将消息均分给所有的`C`。

## Exchange
`Q`可以绑定`EX`，当`EX`收到消息时，会将消息传递给`Q`。一个`Q`可以绑定多个`EX`,一个`EX`也可以拥有多个`Q`

## RoutingKey
`RK`可以理解为`Q`的标签，当`P`发布消息时，会指定`EX`和`RK`,`EX`将消息传递给所有拥有`RK`标签的`Q`。
