### Run

```
docker build -t kafka .

docker run --name container-kafka --rm -it -p 9092:9092  -v $(pwd)/server.properties:/data/config/server.properties -v $(pwd)/data:/data/kafka-logs kafka /bin/bash

kafka-server-start.sh config/server.properties --override log.dirs=/data/kafka-logs --override advertised.listeners=PLAINTEXT://localhost:9092

# 检测是否启动成功
netstat -tlnup | grep 9092

docker exec -it container-kafka /bin/bash
```

### Stop Kafka

```
kafka-server-stop.sh
```

### 创建 topic
```
kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```

### 查看 topic
```
kafka-topics.sh --list --bootstrap-server localhost:9092
```

### 生产一条消息
```
kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

### 消费一条消息
```
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

## 配置说明
几个重要的 kafka 配置:

* log.dirs  : Kafka的data目录
* advertised.listeners  : docker 中特别受到影响，因为 Kafka通过zookeeper通过主机名做服务发现，所以可能客户端是 docker 的宿主机 ip，但是zk返回 docker hostname 从而发送消息失败
* broker.id : 集群的时候很重要
* zookeeper.connect : zk 的 host 配置

## todo

增加 kafka manager

### Notice

1. 修改Kafka的data目录: log.dirs可以配置多个目录，需要用逗号分隔开
1. 修改Kafka的logs目录: 在 ${KAFKA_HOME}/bin/kafka-run-class.sh 中修改 LOG_DIR
