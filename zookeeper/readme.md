# Run

```
zkServer.sh status
zkServer.sh start-foreground
```

## 启动
```
docker build -t zk .

docker run -p 2181:2181 --name container-zk -v $(pwd)/zoo.cfg:/data/conf/zoo.cfg -v $(pwd)/data:/data/zookeeper-data -d zk

docker exec -it container-zk /bin/bash
```

## 一个参考配置例子
```
在每个节点中复制一份conf/zoo_sample.cfg为zoo.cfg,其配置文件内容如下:
tickTime=2000
initLimit=5
syncLimit=2
dataDir=/data/zk-data
clientPort=2181
server.1=zookeeper-node1:2888:3888
#server.2=zookeeper-node2:2888:3888
#server.3=zookeeper-node3:2888:3888
```
