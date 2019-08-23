FROM openjdk:8-jre-slim

ARG DATA_DIR=/data
ARG ZOOKEEPER_VERSION=3.5.5
# 配置文件 /data/conf/zoo.cfg
ENV ZOO_CONF_DIR=/data/conf

RUN set -ex ; \
    apt-get update ; \
    apt-get install -y curl procps ; \
    mkdir -p $DATA_DIR $ZOO_CONF_DIR; \
    cd $DATA_DIR ; \
    curl -o $DATA_DIR/apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz \
        https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/zookeeper-$ZOOKEEPER_VERSION/apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz ; \
    tar -zxf apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz ; \
    mv apache-zookeeper-$ZOOKEEPER_VERSION-bin/conf/* "$ZOO_CONF_DIR"; \
    cp $ZOO_CONF_DIR/zoo_sample.cfg $ZOO_CONF_DIR/zoo.cfg ; \
    rm -rf apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz /var/lib/apt/lists/* /tmp/* /var/tmp/* ;

# ZOOCFGDIR 是 bin/zkServer.sh 文件中的配置目录环境变量
ENV PATH=$PATH:$DATA_DIR/apache-zookeeper-$ZOOKEEPER_VERSION-bin/bin \
    ZOOCFGDIR=$ZOO_CONF_DIR

WORKDIR $DATA_DIR

# 2181：对cline端提供服务 3888：选举leader使用 2888：集群内机器通讯使用（Leader监听此端口）
EXPOSE 2181 2888 3888

CMD ["zkServer.sh", "start-foreground"]
