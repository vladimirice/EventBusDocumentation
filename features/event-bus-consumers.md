# EventBus consumers

An idea is to publish message (event) to the EventBus, and route it to all microservices,
interested in this message using RabbitMQ exchange routing.

## Introduction

1. There is two demo microservices-consumers (we can add any more if required):
    * [EventBusConsumer (actually an audit microservice)](https://github.com/vladimirice/EventBusConsumer)
    * [EventBusWebsocket](https://github.com/vladimirice/EventBusWebsocket)
2. There is an [EventBusPublisher](https://github.com/vladimirice/EventBusPublisher) microservice 
   that imitates publishing process (on production, publishing module will be a part of, for example, OrdersService).


## Use-case

1. Run the browser tab with user subscribed to order events, following the link -
   [login as admin](http://127.0.0.1:3002/?admin).

2. Open up logs of other consumer in the first console tab:
```
    make tail-logs --dir ../EventBusConsumer
```

3. Publish a valid order event to the EventBus:
```
    make send-order-1-request --dir ../EventBusPublisher
```

**Result**:

1. Observe the message payload in the browser tab (delivered using a websocket).
2. Observe EventBusConsumer logs - see the same message payload (also delivered, as expected).
