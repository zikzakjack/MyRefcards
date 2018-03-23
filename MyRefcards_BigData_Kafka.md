# Kafka

## Configure KAFKA_HOME

	KAFKA_HOME=<your_kafka_path>

## Start ZooKeeper

	cd %KAFKA_HOME%
	%KAFKA_HOME%/bin/windows/zookeeper-server-start %KAFKA_HOME%/config/zookeeper.properties

## Open ZooKeeper Shell

	%KAFKA_HOME%/bin/windows/zookeeper-shell localhost:2181

## Start Kafka Server

	%KAFKA_HOME%/bin/windows/kafka-server-start %KAFKA_HOME%/config/server.properties

## Create Topic

	%KAFKA_HOME%/bin/windows/kafka-topics --zookeeper localhost:2181 --create --topic zikzakjack_raw_input_position --partitions 1 --replication-factor 1

## List Topic

	%KAFKA_HOME%/bin/windows/kafka-topics --zookeeper localhost:2181 --list

## Describe Topic

	%KAFKA_HOME%/bin/windows/kafka-topics --zookeeper localhost:2181 --describe --topic zikzakjack_raw_input_position

## Console Producer

	%KAFKA_HOME%/bin/windows/kafka-console-producer --broker-list localhost:9092 --topic zikzakjack_raw_input_position

## Console Consumer

	%KAFKA_HOME%/bin/windows/kafka-console-consumer --bootstrap-server localhost:9092 --topic zikzakjack_raw_input_position --from-beginning

