## Install Kafka on Kubernetes


```
Create the namespace

$ kubectl create namespace kafka

$ wget https://strimzi.io/install/latest?namespace=kafka > strimzi-kafka.yml

$ kubectl create -f strimzi-kafka.yml -n kafka

$ wget https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml


Provision the Apache Kafka cluster

$ kubectl create -f kafka-persistent-single.yaml -n kafka

$ kubectl wait kafka/my-cluster --for=condition=Ready --timeout=300s -n kafka

Send and receive messages

$ kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.23.0-kafka-2.8.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --broker-list my-cluster-kafka-bootstrap:9092 --topic my-topic



Receive messages

$ kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.23.0-kafka-2.8.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning

```
