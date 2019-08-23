FROM openjdk:8-jre-slim

ARG DATA_DIR=/data
ARG SCALA_VERSION=2.12
ARG KAFKA_VERSION=2.3.0
# 配置文件 /data/config/server.properties
ENV KAFKA_CONF_DIR=/data/config

RUN set -ex ; \
    apt-get update ; \
    apt-get install -y curl procps ; \
    mkdir -p $DATA_DIR ; \
    cd $DATA_DIR ; \
    curl -o kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz \
        https://mirrors.tuna.tsinghua.edu.cn/apache/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz ; \
    tar -zxf kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz ; \
    rm -rf kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz ; \
    ln -s kafka_2.12-2.3.0/config "$KAFKA_CONF_DIR";

ENV PATH=$PATH:$DATA_DIR/kafka_$SCALA_VERSION-$KAFKA_VERSION/bin

WORKDIR $DATA_DIR

EXPOSE 9092

VOLUME ["/data/kafka-logs"]

CMD ["kafka-server-start.sh", "config/server.properties"]
