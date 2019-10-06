# Sketchy Data Pipelines

Requirements:

 - Python 3.x
 - Kafka 2.1.0
 - Elasticsearch 6.7.0
 - Flask
 - Client APIs and packages `pip install -r requirements.txt`

Setup:

 1. Start Zookeeper
 
        zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties

 2. Start Kafka
 
        kafka-server-start /usr/local/etc/kafka/server.properties

 3. Create topics
 
        kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic twitter2kafka
        kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic kafka2sketch

 4. Start Elasticsearch
        
        elasticsearch

 5. Create Elasticsearch index
        
        curl -XPUT "http://localhost:9200/tweets"

 6. Navigate to the 'code' directory and start the services:
        
        python streaming/twitter_to_kafka.py
        python streaming/kafka_to_elastic.py
        python app/application.py

 7. Initialize the stateful count-min sketch:
        
        curl -v http://127.0.0.1:5000/initialize

 8. Call API endpoints listed as routes in `app/application.py` to get the data
 