# MongoDB学习总结

## MongoDB自平衡机制（版本号：3.6）

### 丢失数据现象
MongoDB自平衡机制（默认开启）可以在数据不平衡时自动平衡各个分片之间的数据，最终达到最佳平衡。这个机制在一定情况下会造成数据丢失。
该情况发生在3.6版本以下（之后的版本未进行过测试），分片+副本集模式下。不同于其他常见的数据丢失机制，由于自平衡机制丢失的数据现象
极难排查。所以如果所有常规丢失数据原因都不符合你的情况的话，你可能需要看看是否是MongoDB自平衡机制造成了数据丢失。如果是由于MongoDB
自平衡机制造成了数据丢失，可以选择关闭MongoDB自平衡机制。
#### 命令如下（该命令应该在mongos上执行）：
Sh.stopBalancer(timeout,interval)
#### 该命令包含两个参数：
timeout：超时时间，默认为1分钟
interval：轮询间隔，每隔一段时间轮询blancer是否停止

### 关闭自平衡后如何保证数据在分片之间的平衡性
可以选择开启哈希索引，开启哈希索引后，数据会按照哈希之后的规则较为均匀的分散到各个分片。
