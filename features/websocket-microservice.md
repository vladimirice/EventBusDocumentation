## [Websocket microservice](https://github.com/vladimirice/EventBusWebsocket)

### Workflow

1. Clients subscribe to events using a websocket connection.
2. Services like `Orders service` publishes event about the new order to the RabbitMQ EventBus.
3. Event (message) is routed to the websocket queue and consumed.
4. Consumer service processes the event and push it to the OrdersGateway
5. Each order has a dedicated socket.io room, room subscribers receive the event and, for example, render new order state.

### Use-case - Order subscription

OrdersGateway (orders socket.io namespace) implements room-based subscription (room per order).

1. [Login as admin](http://127.0.0.1:3002/?admin).
2. [Login as ordersManager](http://127.0.0.1:3002/?ordersManager) - in different browser or incognito mode.
3. Ensure that users are subscribed to events (observe messages).
4. Publish order ID=1 event through the RabbitMQ by running:
```
    make send-order-1-request --dir ../EventBusPublisher
```
5. Observe JSON payload message. Both users should receive it.
6. Publish order ID=2 event through the RabbitMQ by running:
```
    make send-order-2-request --dir ../EventBusPublisher
```
7. Observe JSON payload message. Only admin user receives it.

### Use-case - clicks subscription

Click is a dedicated namespace without rooms.

1. [Login as admin](http://127.0.0.1:3002/?admin).
2. [Login as clicksManager](http://127.0.0.1:3002/?clicksManager)
3. Ensure that users are subscribed to events (observe messages).
4. Publish click event through the RabbitMQ by running:
```
    make send-click-request --dir ../EventBusPublisher
```
5. Observe JSON payload message. Both users should receive it. 
