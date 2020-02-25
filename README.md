# middleware
Containered-based middlewares

# 1 Docker-based

1. docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
2. docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter
3. docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper  & docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --env KAFKA_ADVERTISED_HOST_NAME=localhost --env KAFKA_ADVERTISED_PORT=9092 --volume /etc/localtime:/etc/localtime wurstmeister/kafka:latest (docker exec -it ${CONTAINER ID} /bin/bash;cd /opt/kafka_2.12-2.1.0/bin;kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic mykafka;bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mykafka;bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mykafka;bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning)

# 2 Operator-based

## 2.1 RabbitMQ

This solution is based on [rabbitmq-operator](https://github.com/indeedeng/rabbitmq-operator).

### 2.1.1 Create Operator

```
https://raw.githubusercontent.com/kubesys/kubeOS/master/yamls/rabbitmq/operator-rabbitmq.yaml
```

### 2.1.2 Create a instance

```
https://github.com/kubesys/kubeOS/blob/master/yamls/rabbitmq/instance-rabbitmq.yaml
```

### 2.1.3 Check the instance

```
[root@ali3 rabbitmq]# kubectl get po -o wide
NAME                                 READY   STATUS    RESTARTS   AGE     IP              NODE   NOMINATED NODE   READINESS GATES
rabbitmq-instance-0                  0/1     Running   0          5m40s   10.244.48.202   ali3   <none>           <none>
rabbitmq-operator-55d4f6545f-4m6mc   1/1     Running   0          16h     10.244.48.199   ali3   <none>           <none>
```

```
curl http://10.244.48.202:15672
```

### 2.1.4 Prometheus

Coming soon...

### 2.1.5 More parameters

Please see https://github.com/indeedeng/rabbitmq-operator


## 2.2 Kafka

This solution is based on [strimzi-kafka-operator](https://github.com/strimzi/strimzi-kafka-operator).

### 2.2.1 Create Operator

```
https://raw.githubusercontent.com/kubesys/kubeOS/master/yamls/kafka/operator-kafka.yaml
```

### 2.2.2 Create a instance

```
https://raw.githubusercontent.com/kubesys/kubeOS/master/yamls/kafka/instance-kafka.yaml
```

### 2.2.3 Check the instance

```
[root@ali3 rabbitmq]# kubectl get po -o wide
NAME                                 READY   STATUS    RESTARTS   AGE     IP              NODE   NOMINATED NODE   READINESS GATES
rabbitmq-instance-0                  1/1     Running   0          5m40s   10.244.48.202   ali3   <none>           <none>
rabbitmq-operator-55d4f6545f-4m6mc   1/1     Running   0          16h     10.244.48.199   ali3   <none>           <none>
```

```
curl http://10.244.48.202:15672
```

### 2.2.4 Prometheus

Coming soon

```
https://github.com/strimzi/strimzi-kafka-operator/tree/master/metrics/examples/prometheus/install
```

### 2.2.5 More parameters

Please see https://strimzi.io/docs/overview/latest/#configuration-points_str

# 3 Helm-based

## 3.1 RabbitMQ

https://github.com/helm/charts/tree/master/stable/rabbitmq
https://github.com/helm/charts/tree/master/stable/rabbitmq-ha

## 3.2 Kafka

https://github.com/helm/charts/tree/master/stable/kafka-manager


## 3.3 Tensorflow

https://github.com/helm/charts/tree/master/stable/distributed-tensorflow
