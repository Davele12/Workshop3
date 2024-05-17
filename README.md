Sure, here's an updated version of the README in English, including instructions for using the provided Jupyter notebooks:

---

# Happiness Prediction Project using Kafka and Machine Learning

## Description

This project utilizes Apache Kafka for real-time data streaming and a linear regression model trained with happiness data to predict values. The data is sent to Kafka from a producer, and a consumer processes this data using the prediction model to calculate performance metrics.

## Tools Used

- **Python**: Programming language used for implementing the producer, consumer, and prediction model.
- **Apache Kafka**: Distributed streaming platform used for handling real-time data.
- **Docker and Docker Compose**: Tools used for containerizing and orchestrating Kafka and Zookeeper services.
- **scikit-learn**: Machine learning library used for training the linear regression model.
- **pandas**: Data manipulation and analysis library used for handling datasets.

## Requirements

- Docker
- Docker Compose
- Python 3.x
- Python libraries: `confluent_kafka`, `pandas`, `scikit-learn`, `pickle`

## Project Setup and Execution

### 1. Configure Docker Compose

Create a `docker-compose.yml` file with the following content:

```yaml
version: '3.8' # Docker Compose version

services: # Containers to run
  zookeeper: # First container (Service)
    image: confluentinc/cp-zookeeper:latest  # Zookeeper Docker image
    container_name: zookeeper # Container name
    environment: # Environment variables
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports: # Maps port 2181 from the host to port 2181 inside the zookeeper container
      - 2181:2181

  kafka: # Second container (Service)
    image: confluentinc/cp-kafka:latest # Latest version of Kafka Docker image
    container_name: kafka # Container name
    depends_on:
      - zookeeper # Kafka depends on Zookeeper so Kafka will not start until Zookeeper service is up and running
    environment:
      KAFKA_BROKER_ID: 1 # The unique identifier for this Kafka broker (set to 1 in this case)
      KAFKA_ZOOKEEPER_CONNECT: 'zookeeper:2181' # The connection information for ZooKeeper, which is accessible at zookeeper:2181
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_INTERNAL:PLAINTEXT # Defines the security protocols for Kafka listeners
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092,PLAINTEXT_INTERNAL://kafka:29092 # Defines the advertised endpoints for clients to connect to the Kafka broker
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 1
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 1
    ports:
      - "9092:9092" # Port to use to connect from Kafka broker to localhost port
    expose:
     - "29092" # Exposes port 29092 for internal communication

networks:
  kafka_network:
    driver: bridge
```

### 2. Start the services with Docker Compose

Run the following commands to start the Zookeeper and Kafka services:

```sh
docker-compose up -d
```

### 3. Prepare the Python environment

Create a virtual environment and activate it:

```sh
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

Install the required dependencies:

```sh
pip install confluent_kafka pandas scikit-learn
```

### 4. Train and save the model

The model is already trained and saved in the `model.ipynb` notebook located in the `notebooks` directory. Open and run the notebook to train and save the model if needed.

### 5. Run the Kafka producer

The producer code is located in the `kafka.ipynb` notebook in the `notebooks` directory. Open and run the notebook to send test data to Kafka.

### 6. Run the Kafka consumer

The consumer code is also located in the `kafka.ipynb` notebook in the `notebooks` directory. Open and run the notebook to receive the test data, make predictions, and calculate performance metrics.

## Conclusion

This project demonstrates how to use Apache Kafka for real-time data streaming and a machine learning model to predict happiness scores and calculate performance metrics. The provided Jupyter notebooks and scripts guide you through setting up the environment, training the model, and running the producer and consumer.

For any questions or further assistance, feel free to reach out.

---

Davele12
 
