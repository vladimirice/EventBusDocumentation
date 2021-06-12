# Queue error handling

## Test-case

1. Run the browser tab with user subscribed to order events, following the link -
[login as admin](http://127.0.0.1:3002/?admin).

2. Run the script that will publish malformed message and then opens the Websocket logs:
```
    make publish-malformed-message --dir ../EventBusInfrastructure && make tail-logs --dir ../EventBusWebsocket
```

3. Right after it in a second console run the script that publishes a valid order event to the EventBus:
```
   make send-order-1-request --dir ../EventBusPublisher
```

**Result**: 
1. You'll see that, message is successfully delivered to the user, and republishing is still in process (no queue head blocking).
2. In logs, you'll see 20 attempts to republish and process. After the last attempt message will be logged and dropped from the queue.
   
Notes:
* A number of 20 attempts is too much and set in order to simplify testing. On production, setting will be up to 5-10 attempts.
* Message is just logged before dropping (acknowledged) from the queue. On production, it will be saved into 
the dedicated database for further investigation. 
