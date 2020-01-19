#### 问题：

1. 如何解决消息队列的延时以及过期失效的问题？

2. 消息队列满了以后该怎么处理？

3. 有几百万的消息持续积压了几个小时，该怎么处理？


分析：

总的来说，上面的场景都是因为消费端出现了问题，不进行消费了；或者消费端的处理速度极慢，导致某些消息超时被清理掉；


如果大量的消息堆积，需要紧急处理；

那么目前需要的就是修复consumer的问题，让它恢复，对消息进行消费；对现有的consumer进行停掉。
临时对消费者端的服务器进行扩容，把积压的消息处理掉；等处理完挤压的消息后，重启旧的消费者进行消费。



MQ中的消息过期时间

可以设置每条消息的过期时间，那么实际上积压到一定时间后，会被自动清理掉，积压的消息不会过多。

如果有些消息类型是重要的，那么需要把这类型的消息不能设置过期时间；或者是要重新投递到队列中。


MQ监控

消费者进程监控。及时发现如果消费者进程异常退出，及时重启，避免过多消息积压；

服务监控

消息积压到一定数量，需要有预警机制，需要及时排查是否有问题；