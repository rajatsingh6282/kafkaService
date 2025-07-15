# kafkaService
I Am Trying to make application for  kafka learnign

Installation Commands
========================================================
Step 1 : 
Copy and paste kafka folder in c directory

Step 2 :
in folder goto bin -> download open in cmd and run this command (This is use for start Zookeper)
=> zookeeper-server-start.bat ..\..\config\zookeeper.properties

kafka-server-start.bat ..\..\config\server.properties

Step 3 :
create the topic for produce and consume data
kafka-topics.bat --create --topic my-topic --bootstrap-server localhost:9092 --replication-factor 1 --partitions 3

Step 4 :
Start Producer
kafka-console-producer.bat --broker-list localhost:9092 --topic my-topic

Step 5 :
Start Consumer
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic my-topic --from-beginning

Sending Message Commands
===========================================================
zookeeper-server-start.bat ..\..\config\zookeeper.properties

kafka-server-start.bat ..\..\config\server.properties

kafka-topics.bat --create --topic foods --bootstrap-server localhost:9092 --replication-factor 1 --partitions 4

kafka-console-producer.bat --broker-list localhost:9092 --topic foods --property "key.separator=-" --property "parse.key=true"

kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic foods --from-beginning -property "key.separator=-" --property "print.key=false"

for list topics
=> kafka-topics.bat --bootstrap-server localhost:9092 --list
for groups 
=> kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
describe partitioning
=> .\kafka-topics.bat --describe --topic my-topic --bootstrap-server localhost:9092

for creating groups multiple consumer start
=> kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic my-topic --group console-consumer-2682

=============================================================
Two things -> key and value,(key is optional)
we can send message with key or without key,

when sending msg with key ordering is maintain as they will be in same partition.
without key we can not gurantee the ordering of message as consumer poll the message from all the partitions at the same time.

===================================================================================================================
create topic 
=> kafka-topics.bat --create --topic gadgets --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --replication-factor 3 --partitions 3

start producer
=> kafka-console-producer.bat --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --topic gadgets

start consumer
=> kafka-console-consumer.bat --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --topic gadgets --from-beginning

describe
=> .\kafka-topics.bat --describe --topic gadgets --bootstrap-server localhost:9092,localhost:9093,localhost:9094





Apache Kafka
================================
- Apache kafka was originally developed by Linkedin.
- Apache kafka is ditributed streaming platform.
- Streams are just infinite data, data that never mind end. it just keeping arriving, and you can process it in real-time.
- Distributed means that kafka works in a cluster, each node in the cluster is called broker.
- Broker is nothing but is a physical server.


=>  Cluster : A cluster is a group of interconnected computers that work together to perform tasks as if they are a single system.
				These are commonly used for high availability, fault tolerance, and increased performance.
				
	types of Clusters : 
			1. High-Performance Computing(HPC) Cluster
				Used for computational tasks requiring high speed, such as scientific simulations.
				
			2. Load Balancing Clustors
				Distribute workloads across multiple servers to ensure no single server is overwhelmed.
				
			3. Failover Clustors
				Provide redundancy to ensure service availability during hardware or software failures.
				
				
- apache kafka is used to process real time data feeds with high throughput and low latency.
- message represent information such as line in log file, a row of stock market area or an error message from a system.
- message are grouped into categories called topics.
example : 
		product_topic
		category_topic
		
- apache kafka is act as a message broker.
- when we are working with apache kafka two parties will be available.
	one application will acts as a publisher another application will act as Subscriber.
	
=> Apache Kafka Use Cases
	- Activity Tracking
	- Gathering metrics from many different locations.
	- Application Logs Gathering
	- Netflix uses kafka to apply recommendations in real time while you are watching TV Shows.
	- Uber uses kafka to gather user, taxi, and trip data in real time to compute and forecast demand and compute pricing in real time.
	
=> Producer
	- The Producer is the creater of the message in kafka.
	- The producers place the message to a perticular topic.
	- Topics should already exists before a message is placed by the producer.
	- Topics are split in in partitions, which are the unit of parallelism in kafka.
	
=> Broker
	- Broker is nothing but a server inside cluster.
	- kafka cluster is compossed of multiple brokers(server).
	- Each broker is identified with it's Id(integer).
	- Each broker contain certain topics and partitions.
	- After connecting any broker (called a bootstrap broker) you will be connected to entire cluster.
	- A good number to get started is 3 broker but some big cluster have over 10 brokers.
	
=> Consumer
	- The consumer is the reciver of the messages in kafka.
	- Consumers read data from topic(identified by name).
	- consumers know which broker to read from.
	- Each consumer belongs to a consumer group.
	
=> Zookeeper
	- Zookeeper is a software which will provide runtime environment to run our apache kafka server.
	- Zookeeper manages the brokers (keep a list of them)
	- it sends notifications to kafka in case of changes(new topic,broker dies, broker comes up, delete topics)
	- kafka can't work without zookeeper.
	
