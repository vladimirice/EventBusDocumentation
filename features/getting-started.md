# Getting started

1. Install Docker and Docker-compose.
2. Ask for access to the GitHub repositories.
3. Clone all required repositories locally inside the same folder:
```
    mkdir EventBusDemo
    cd EventBusDemo
    git clone git@github.com:vladimirice/EventBusInfrastructure.git
    git clone git@github.com:vladimirice/EventBusPublisher.git
    git clone git@github.com:vladimirice/EventBusConsumer.git
    git clone git@github.com:vladimirice/EventBusWebsocket.git
    git clone git@github.com:vladimirice/WebsocketClient.git
```
4. Go to the EventBusInfrastructure and run the docker containers:
```
    cd EventBusInfrastructure
    make run-project
```
5. Follow the scenarios, listed in [Readme](../README.md)
