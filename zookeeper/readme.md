# Run

```
zkServer.sh status
zkServer.sh start-foreground
```

## 启动
```
docker run -p 2181:2181 --name container-zk -v $(pwd)/zoo.cfg:/data/conf/zoo.cfg -v $(pwd)/data:/data/zookeeper-data -d zk

docker exec -it container-zk /bin/bash
```
