## acks
生产者在把消息发送给server之后发出的确认接收信号，此项配置是指定需要多少个确认信号

## acks 的值
```
acks = 0
  设置为0表示producer不需要等待任何确认收到的信息。副本将立即加到socket  buffer并认为已经发送。没有任何保障可以保证此种情况下server已经成功接收数据，同时重试配置不会发生作用（因为客户端不知道是否失败）回馈的offset会总是设置为-1
acks = 1
  这意味着至少要等待leader已经成功将数据写入本地log，但是并没有等待所有follower是否成功写入。这种情况下，如果follower没有成功备份数据，而此时leader又挂掉，则消息会丢失。
acks = all
  这意味着leader需要等待所有备份都成功写入日志，这种策略会保证只要有一个备份存活就不会丢失数据。这是最强的保证。
acks = 其他的值
  例如acks=2也是可以的，这将需要给定的acks数量，但是这种策略一般很少用。
```