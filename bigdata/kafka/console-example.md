# Kafka Console example

In this example we will see how a Kafka console-producer and
console-consumer will work.

## Pre-requisite:

Install JDK, Kafka and Zookeeper on your machine.

## Steps to run example

### Windows
1. Configure ZooKeeper-

       cd <KAFKA_HOME>\config
       notepad zookeeper.properties
   Change the `dataDir` to a local Windows path. Eg: `dataDir=D:\\tmp\\`
    
2. Start ZooKeeper-

       cd <KAFKA_HOME>
       bin\windows\zookeeper-server-start.bat config\zookeeper.properties

3. Configure Kafka-

       cd <KAFKA_HOME>\config
       notepad server.properties
       
4. Start Kafka Server-

       cd <KAFKA_HOME>
       bin\windows\kafka-server-start.bat config\server.properties
       
5. Create Kafka Topic-
      
      bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic <TopicName>
      
6. Start Kafka producer-
      kafka-console-producer.bat --broker-list localhost:9092 --topic test
      
7. Start Kafke consumer-
      bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:2181 --topic test
