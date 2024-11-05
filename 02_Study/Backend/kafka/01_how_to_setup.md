Setting up Kafka locally and using it with Node.js is a great way to learn and experiment with this powerful event streaming platform. Here’s a step-by-step guide to get you started:

### Step 1: Install Kafka Locally

1. **Download Kafka**:
    
    - Go to the Apache Kafka downloads page and download the latest version.
2. **Extract Kafka**:
    
    - Extract the downloaded file to a directory of your choice.
3. **Start ZooKeeper**:
    
    - Kafka uses ZooKeeper to manage the cluster. Start ZooKeeper with the following command:
        
        ```sh
        bin/zookeeper-server-start.sh config/zookeeper.properties
        ```
        
4. **Start Kafka Broker**:
    
    - In a new terminal window, start the Kafka broker:
        
        ```sh
        bin/kafka-server-start.sh config/server.properties
        ```
        

### Step 2: Set Up Node.js Project

1. **Initialize a Node.js Project**:
    
    - Create a new directory for your project and initialize it with npm:
        
        ```sh
        mkdir kafka-nodejs
        cd kafka-nodejs
        npm init -y
        ```
        
2. **Install KafkaJS**:
    
    - KafkaJS is a popular client library for Kafka in Node.js. Install it using npm:
        
        ```sh
        npm install kafkajs
        ```
        

### Step 3: Create Kafka Producer and Consumer

1. **Create a Producer**:
    
    - Create a file named `producer.js` and add the following code:
        
        ```js
        const { Kafka } = require('kafkajs');
        
        const kafka = new Kafka({
          clientId: 'my-app',
          brokers: ['localhost:9092']
        });
        
        const producer = kafka.producer();
        
        const run = async () => {
          await producer.connect();
          await producer.send({
            topic: 'test-topic',
            messages: [
              { value: 'Hello KafkaJS user!' },
            ],
          });
        
          await producer.disconnect();
        };
        
        run().catch(console.error);
        ```
        
2. **Create a Consumer**:
    
    - Create a file named `consumer.js` and add the following code:
        
        ```js
        const { Kafka } = require('kafkajs');
        
        const kafka = new Kafka({
          clientId: 'my-app',
          brokers: ['localhost:9092']
        });
        
        const consumer = kafka.consumer({ groupId: 'test-group' });
        
        const run = async () => {
          await consumer.connect();
          await consumer.subscribe({ topic: 'test-topic', fromBeginning: true });
        
          await consumer.run({
            eachMessage: async ({ topic, partition, message }) => {
              console.log({
                partition,
                offset: message.offset,
                value: message.value.toString(),
              });
            },
          });
        };
        
        run().catch(console.error);
        ```
        

### Step 4: Run the Producer and Consumer

1. **Start the Producer**:
    
    - Run the producer script to send a message to Kafka:
        
        ```sh
        node producer.js
        ```
        
2. **Start the Consumer**:
    
    - Run the consumer script to read messages from Kafka:
        
        ```sh
        node consumer.js
        ```
        

### Additional Resources

- [**Confluent’s Kafka and Node.js Tutorial**: A comprehensive guide to building a Node.js client application for Kafka](https://developer.confluent.io/get-started/nodejs/)[1](https://developer.confluent.io/get-started/nodejs/).
- [**Soham Kamani’s Blog**: Detailed examples of implementing Kafka producer and consumer in Node.js](https://developer.confluent.io/get-started/nodejs/)[2](https://www.sohamkamani.com/nodejs/working-with-kafka/).