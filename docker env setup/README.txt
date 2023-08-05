1) First need to check the the defined ports in docker-compose.yml is available or not.
2) If these defined port available then hit the shared command below to run the [kafka and zookeeper] in docker environment,
	command = docker-compose -f docker-compose.yml up -d
The -d means both Zookeeper and Kafka will run in the background, so you’ll have access to the Terminal after they start.
By specifying the -f option, you can use a different filename if your Docker Compose configuration is saved under a different name, or if you have multiple configuration files for different environments.

It's important to note that if you don't explicitly specify the -f option, Docker Compose will look for the default filename docker-compose.yml in the current directory and use it as the configuration file.

3) now in you OS open command prompt and hit the shared command below,
	command : docker exec -it kafka /bin/sh
Just replace kafka with the value of container_name, if you’ve decided to name it differently in the docker-compose.yml file.

4) create a first tusing command below,

	command : kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 3 --topic first_kafka_topic

	###Explanation of the parameters:###
	--bootstrap-server: Specifies the Kafka broker(s) to connect to. In this example, we are connecting to a broker running on localhost at port 9092.
	--topic: Specifies the topic from which you want to consume messages.
	--from-beginning: Tells the consumer to read messages from the beginning of the topic. If you omit this parameter, the consumer will read only new messages that arrive after it starts.

5) consume the topic from command line using below command,

	command : kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_kafka_topic --from-beginning
	more details command : kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_kafka_topic --property print.timestamp=true --property print.headers=true --from-beginning
	deep1 details : kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic  first_kafka_topic --property print.timestamp=true --property print.offset=true  --property print.partition=true --property print.key=true --property print.headers=true  --property   print.key=true --from-beginning
	deep2 details : kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_kafka_topic  --property group.id=your_consumer_group_id --from-beginning

		When consuming messages from Kafka, you can access the topic, partition, and offset details for each message, which together form the unique identifier for that message.
		 You can use this combination to uniquely identify and process messages in your application.

6) produce data to the topic use shared command below,
	i) command :  kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_kafka_topic
	ii) key value pair poduce data command : kafka-console-producer.sh --broker-list localhost:9092 --topic first_kafka_topic --property parse.key=true --property key.separator=:


7) essential command for manage kafka,
	i)get all topics name = kafka-topics.sh --bootstrap-server localhost:9092 --list
	ii) delete a topic = kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic first_kafka_topic  //it will take some time to delete this topic.
	iii) get details about a topic  = kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic  first_kafka_topic
	iv)  




 