# Docker compose

```yml
services:
    zookeeper:
        image: zookeeper
        container_name: zookeeper
        ports:
            - "2181:2181"

    kafka:
        image: confluentinc/cp-kafka
        depends_on:
            - zookeeper
        ports:
            - "9092:9092"
        expose:
            - "29092"
        environment:
            KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
            KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
            KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
            KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:29092,PLAINTEXT_HOST://localhost:9092
            KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: "1"
            KAFKA_MIN_INSYNC_REPLICAS: "1"

    kafka-ui:
        container_name: kafka-ui
        image: provectuslabs/kafka-ui
        ports:
            - 8080:8080
        environment:
            DYNAMIC_CONFIG_ENABLED: true
```

# Code (Nodejs):

> *client.js*
---
```js
const { Kafka } = require("kafkajs");

exports.kafka = new Kafka({
  clientId: "my-app",
  brokers: ["<PRIVATE_IP>:9092"],
});
```


> *admin.js*
---
```js
const { kafka } = require("./client");

async function init() {
  const admin = kafka.admin();
  console.log("Admin connecting...");
  admin.connect();
  console.log("Adming Connection Success...");

  console.log("Creating Topic [rider-updates]");
  await admin.createTopics({
    topics: [
      {
        topic: "rider-updates",
        numPartitions: 2,
      },
    ],
  });
  console.log("Topic Created Success [rider-updates]");

  console.log("Disconnecting Admin..");
  await admin.disconnect();
}

init();
```


> *producer.js*
---
```js
const { kafka } = require("./client");
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

async function init() {
  const producer = kafka.producer();

  console.log("Connecting Producer");
  await producer.connect();
  console.log("Producer Connected Successfully");

  rl.setPrompt("> ");
  rl.prompt();

  rl.on("line", async function (line) {
    const [riderName, location] = line.split(" ");
    await producer.send({
      topic: "rider-updates",
      messages: [
        {
          partition: location.toLowerCase() === "north" ? 0 : 1,
          key: "location-update",
          value: JSON.stringify({ name: riderName, location }),
        },
      ],
    });
  }).on("close", async () => {
    await producer.disconnect();
  });
}

init();
```


> *consumer.js*
---
```js
const { kafka } = require("./client");
const group = process.argv[2];

async function init() {
  const consumer = kafka.consumer({ groupId: group });
  await consumer.connect();

  await consumer.subscribe({ topics: ["rider-updates"], fromBeginning: true });

  await consumer.run({
    eachMessage: async ({ topic, partition, message, heartbeat, pause }) => {
      console.log(
        `${group}: [${topic}]: PART:${partition}:`,
        message.value.toString()
      );
    },
  });
}

init();
```

# How to run

> **Step 1:**
> 	*Run the docker containers*
```bash
docker-compose up
```

> **Step 2:**
> 	*Run the admin to create topic*
```bash
node admin.js
```

> **Step 3:**
> 	*Run consumer within a predefined group*
```bash
node consumer.js grp-1
```

> **Step 4:**
> 	*Run the producer to produce messages*
```bash
node producer.js

> thor south
> tony north
> wanda south
```

