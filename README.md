# Streaming com Kafka, Spark e MinIO

Este projeto configura um pipeline de **Streaming** utilizando **Apache Kafka, Apache Spark** e **MinIO** dentro de contêineres Docker.

##  Como Rodar o Projeto

### 1. Pré-requisitos
- Docker e Docker Compose instalados.
- Git instalado.

### 2. Clonar o repositório
```sh
git clone https://github.com/mafreitas85/streaming-kafka-spark-minio.git
cd streaming-kafka-spark-minio

### 3. Subir os contêineres Docker
docker-compose up -d

### 4. Criar o tópico Kafka
docker exec -it kafka_lab kafka-topics --create --topic mbatopic --bootstrap-server kafka_lab:9092 --partitions 1 --replication-factor 1

### 5. Rodar o Spark Streaming
docker exec -it spark_lab spark-submit --master local \
  --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0,org.apache.hadoop:hadoop-aws:3.3.4 \
  /opt/bitnami/spark/spark_kafka_streaming.py

### 6. Enviar mensagens para o Kafka
docker exec -it kafka_lab kafka-console-producer --broker-list kafka_lab:9092 --topic mbatopic

{"id": 1, "nome": "Produto A", "preco": 45.99}
{"id": 2, "nome": "Produto B", "preco": 99.50}

### 7. Verificar os dados no MinIO
Acesse: http://localhost:9001/browser
Os arquivos Parquet estarão na pasta parquet/ dentro do bucket mbabucket.


### Tecnologias Utilizadas
Apache Kafka
Apache Spark Streaming
MinIO
Docker & Docker Compose
Python & PySpark

