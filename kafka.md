# [KAFKA](http://kafka.apache.org/)

## 简单介绍
1. Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者在网站中的所有动作流数据
2. 相关术语
    * **Broker**
        Kafka集群包含一个或多个服务器，这种服务器被称为broker
    * **Topic**
       每条发布到Kafka集群的消息都有一个类别，这个类别被称为Topic。（物理上不同Topic的消息分开存储，逻辑上一个Topic的消息虽然保存于一个或多个broker上但用户只需指定消息的Topic即可生产或消费数据而不必关心数据存于何处）
    * **Partition**
        Partition是物理上的概念，每个Topic包含一个或多个Partition.
    * **Producer**
        负责发布消息到Kafka broker
    * **Consumer**
        消息消费者，向Kafka broker读取消息的客户端。
    * **Consumer Group**
        每个Consumer属于一个特定的Consumer Group（可为每个Consumer指定group name，若不指定group name则属于默认的group）。

## 安装/启动

1. [下载](https://kafka.apache.org/downloads.html) (不要下载带`src`的源文件)
```shell
    tar -xzf kafka_2.12-2.3.0.tgz
    cd kafka_2.12-2.3.0
```

1. 启动 zookeeper

```shell
    bin/zookeeper-server-start.sh config/zookeeper.properties
```

1. 启动 kafka

```shell
    bin/kafka-server-start.sh config/server.properties &
```

## node

*使用 [kafka-node](https://github.com/SOHU-Co/kafka-node) 进行连接*

* 安装
    ```node
        npm install kafka-node
    ```
* 使用
    * 引入依赖
        ```node
            let {
                Producer, // 生产者
                Consumer, // 消费者
                KafkaClient, // kafka连接
            } = require('kafka-node');
        ```

    * 创建 实例

        ```node
            const client = new KafkaClient({kafkaHost: '10.3.100.196:9092'});
        ```
    * 创建 生产者

        ```node 
            let option = {
                // Configuration for when to consider a message as acknowledged, default 1
                requireAcks: 1,
                // The amount of time in milliseconds to wait for all acks before considered, default 100ms
                ackTimeoutMs: 100,
                // Partitioner type (default = 0, random = 1, cyclic = 2, keyed = 3, custom = 4), default 0
                PartitionerrType: 2
            }
            let producer = new Producer(client,option);
        ```

    * 创建 消费者 

        ```node
            // 获取 消息 的选项
            let payloads = [{
                topic: 'topicName',
                offset: 0, //default 0
                partition: 0 // default 0
            }];
            // 创建 消费者 的选项
            let option = {
                groupId: 'kafka-node-group',// 消费者组id,默认 `kafka-node-group`
                // Auto commit config
                autoCommit: true,
                autoCommitIntervalMs: 5000,
                // The max wait time is the maximum amount of time in milliseconds to block waiting if insufficient data is available at the time the request is issued, default 100ms
                fetchMaxWaitMs: 100,
                // This is the minimum number of bytes of messages that must be available to give a response, default 1 byte
                fetchMinBytes: 1,
                // The maximum bytes to include in the message set for this partition. This helps bound the size of the response.
                fetchMaxBytes: 1024 * 1024,
                // If set true, consumer will fetch message from the given offset in the payloads
                fromOffset: false,
                // If set to 'buffer', values will be returned as raw buffer objects.
                encoding: 'utf8',
                keyEncoding: 'utf8'
            }
            let consumer = new Consumer(client,payload,option);
        ```



## 相关网站
* **kafka官方:** http://kafka.apache.org
* **kafka下载:** https://kafka.apache.org/downloads.html
* **kafka入门介绍:** https://www.orchome.com/kafka/index
* **kafka-node:** https://www.orchome.com/kafka/index
