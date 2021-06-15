# EventBusDocumentation

Table of contents:
* [Getting started](./features/getting-started.md)
* [EventBus consumers](./features/event-bus-consumers.md)
* [Websockets microservice](./features/websocket-microservice.md)
* [Queue error handling](./features/queue-error-handling.md)

## EventBus workflow

![EventBus workflow](https://raw.githubusercontent.com/vladimirice/EventBusDocumentation/main/diagrams/event-bus-workflow.png)

**Reference:**
* [EventBus consumers](./features/event-bus-consumers.md)
* [Websockets microservice](./features/websocket-microservice.md)


## EventBus message republishing
![EventBusRepublishing](https://raw.githubusercontent.com/vladimirice/EventBusDocumentation/main/diagrams/event-bus-republishing.png)

**X-dead-letter republishing workflow example provided by Utils:**
1. Order.Updated message came before Order.Created message (due to microservice architecture).
2. An error occurred, consumer rejects the message.
3. The message is pushed to x-dead-letter exchange by RabbitMQ.
4. RabbitMQ republishes the message to the tail of the queue.

**Result:** order of messages resolved automatically. [More details](./features/queue-error-handling.md)

## EventBus message dropping
![EventBusDropping](https://raw.githubusercontent.com/vladimirice/EventBusDocumentation/main/diagrams/event-bus-dropping.png)

**Publish-consume x-dead-letter too many redeliveries workflow provided by Utils:**
1. Order.Updated message came but Order.Created message somewhere dropped.
2. For every redelivery consumer checks redeliveries count.
3. The count exceeds the maxRedeliveriesCount settings set by the consumer application based on business logic requirements.
4. Consumer drops the message, and it is logged using a logger or saved to the database (easy to implement if required).

**Result:** later, it is possible to observe dropped messages manually and decide what to do with them. [More details](./features/queue-error-handling.md)
