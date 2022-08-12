# Start 
dev version of kafka via 

`docker-compose -f up`

http://localhost:3030/kafka-topics-ui/#/cluster/fast-data-dev/topic/n/kafka-aggregate-fluvio/

webinar-kafka-sink-connector.yml 

Running Kafka commands:

docker run --rm -it --net=host lensesio/fast-data-dev kafka-topics --zookeeper localhost:2181 --list

docker run --rm -it --net=host lensesio/fast-data-dev kafka-console-consumer --topic kafka-fluvio-topic --bootstrap-server "192.168.1.89:9092"