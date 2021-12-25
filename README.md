# Project Description
## Real time anomaly detection.
The model is trained on a dataset generated statistically.
The model is then stored.
The transaction data form which anomalies are to be found are then 
generated and fed into a kafka topic - `transactions`.
Anomaly detection service has a kafka consumer which listens to the topic 
messages in `transactions` and then uses the model to detect anomalies.
The anomalies are fed into a kafka topic - `anomalies`.

## Steps to execute the project
1. Setup
   1. brew install kafka
   2. setup virtualenv using python3
   3. pip install requirements.txt
2. Start zookeeper and kafka services:
   1. /usr/local/opt/kafka/bin/zookeeper-server-start 
      /usr/local/etc/kafka/zookeeper.properties
   2. /usr/local/opt/kafka/bin/kafka-server-start 
      /usr/local/etc/kafka/server.properties
3. Train the model:
   1. python model/train.py
4. Start the transactions producer:
   1. python streaming/producer.py
5. Start the anomaly detector service:
   1. python streaming/anomaly_detector.py
6. See the messages from transactions and anomalies topics on console:
   1. /usr/local/opt/kafka/bin/kafka-console-consumer --bootstrap-server 
      localhost:9092 --topic transactions --from-beginning
   2. /usr/local/opt/kafka/bin/kafka-console-consumer --bootstrap-server 
      localhost:9092 --topic anomalies --from-beginning
