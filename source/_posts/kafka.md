---
title: hello kafka
date: 2017-07-28
tags:
- kafka
- github
- zookeeper
---

Apache Kafka是分布式发布-订阅消息系统。

<!-- more -->

## 开始吧

#### 下载
    http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/0.11.0.0/kafka_2.11-0.11.0.0.tgz

    tar -xzf kafka_2.11-0.11.0.0.tgz

    cd kafka_2.11-0.11.0.0

#### 启动服务器
* 启动一个**ZooKeeper**服务器

      bin/zookeeper-server-start.sh  config/zookeeper.properties

* 启动**kafka**服务器

      bin/kafka-server-start.sh config/server.properties

#### 创建话题(topics)

    bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

    bin/kafka-topics.sh --list --zookeeper localhost:2181

#### 生产者发送消息(producer)

    bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test

    hello, My name is zhanghang

#### 启动消费者（consumer）

    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning

    hello, My name is zhanghang

####  设置多代理群集
