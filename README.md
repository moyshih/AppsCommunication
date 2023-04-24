# Backend and Frontend Communication using RabbitMQ and SignalR
This repository contains two separate backend applications, appX and appY, which communicate through a [RabbitMQ](https://www.rabbitmq.com/) message broker. The applications can be installed on one or two machines. Both applications are almost identical (99%) and coded in the same backend language C# using [.NET 6](https://dotnet.microsoft.com/en-us/).

In addition, there is a server application called AppUiServer, which subscribes to messages from appX and appY. AppUiServer runs the AppUI frontend application and sends the messages to AppUI via [SignalR](https://dotnet.microsoft.com/en-us/apps/aspnet/signalr).

**AppX:**
1. Implements the class Car. Each car has its own properties (type, color, plate number, creation time).
2. Stores a data collection of cars (list).
3. Every 500[ms], a new car is created, stored in the appX data structure, and sent to AppY.

**AppY:**
1. Implements the class Motorcycle. Each motorcycle has its own properties (type, color, plate number, creation time).\
2. Stores a data collection of motorcycles (list).\
3. Every 1000[ms], a new motorcycle is created, stored in the appY data structure, and sent to AppX.\
4. appX and appY transmit the data to AppUiServer.

**AppUiServer:**
1. Subscribes to messages from appX and appY.\
2. Runs the AppUI frontend application.\
3. Sends the messages to AppUI via SignalR.

**AppUI:**
1. Creates a hub connection and subscribes to the car hub and motorcycle hub.\
2. Prints the data of the last car it received and the timestamp of its creation.\
3. Prints the amount of cars it received.\
4. Prints the data of the last motorcycle it received and the timestamp of its creation.\
5. Prints the amount of motorcycles it received.

The system provides real-time updates of the cars and motorcycles in the backend, and the frontend displays the data as it is received from the backend via SignalR.

#  instructions for running the apps
1. Download [Erlang](https://www.erlang.org/downloads) and install it **using an administrative account**.
2. Download RabbitMQ Server from the [official releases page](https://github.com/rabbitmq/rabbitmq-server/releases/tag/v3.11.13). ([Shortcut for Windows](https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.11.13/rabbitmq-server-3.11.13.exe))
4. Install RabbitMQ Server **using an administrative account**
5. Start the RabbitMQ service:
    - On Windows: Open the start menu and search for "RabbitMQ Service - start". Click on the option to start the service.
    - On other platforms: Open a terminal and run the command rabbitmq-server.
6. Download the [Apps Builds](/AppsBuilds) and extract the folders.
7. Open the **'AppUiServer/appsettings.json'** file and replace the URLs with your IP address.
8. Optionally, open the **'AppX/appsettings.json'** and **'AppY/appsettings.json'** files and modify the configurations as needed
9. Run the **'.exe'** files in each extracted folder.
10. Open the AppUiServer console and Ctrl + Left Click on the URL address at the top of the console, or open a tab on the same address.
