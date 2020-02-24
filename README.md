# middleware
Operator-based middlewares

# Docker-based

1. docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
2. docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter
3. docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper  & docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --env KAFKA_ADVERTISED_HOST_NAME=localhost --env KAFKA_ADVERTISED_PORT=9092 --volume /etc/localtime:/etc/localtime wurstmeister/kafka:latest (docker exec -it ${CONTAINER ID} /bin/bash;cd /opt/kafka_2.12-2.1.0/bin;kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic mykafka;bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mykafka;bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mykafka;bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning)
