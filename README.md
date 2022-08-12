# Start 
# Install Fluvio
* minikube start
* fluvio cluster start

# Recap of Finance Demo
* git clone https://github.com/infinyon/fluvio-demo-04-12-2022-finance-demo.git
* register on finhub.io and obtain api token 
* update API token in 
    * quote-data-input.yaml
* make 
* make gme-input
* make sm-upload
* make sm-consume
* make produce-warrants
* make sm-consume

# Write to Kafka from Fluvio topic

Clone https://github.com/infinyon/kafka_webinar_16_August_2022 
Change the value ADV_HOST in `docker-compose-webinar.yml`  'kafka_url' in `webinar-kafka-sink-connector.yml`  to local ip (`ifconfig| grep inet` for linux)
* docker-compose -f docker-compose -f docker-compose-webinar.yml up
* fluvio connector create -c ./webinar-kafka-sink-connector.yml
* fluvio connector logs -f my-kafka-sink1

# Apply Smart Module to fluvio topic before writing to Kafka 

fluvio connector create -c ./webinar-kafka-sink-connector-with-sm.yml
In https://github.com/infinyon/fluvio-demo-04-12-2022-finance-demo run

```bash
make produce-warrants
```
Watch kafka topic via Web UI
http://localhost:3030/kafka-topics-ui/#/cluster/fast-data-dev/topic/n/kafka-aggregate-fluvio/

or via command line:
docker run --rm -it --net=host landoop/fast-data-dev kafka-console-consumer --topic kafka-aggregate-fluvio --bootstrap-server "192.168.1.89:9092"


# Notes

Running Kafka commands:

docker run --rm -it --net=host lensesio/fast-data-dev kafka-topics --zookeeper localhost:2181 --list

docker run --rm -it --net=host landoop/fast-data-dev kafka-console-consumer --topic kafka-aggregate-fluvio --bootstrap-server "192.168.1.89:9092"