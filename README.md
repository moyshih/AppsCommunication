# Backend and Frontend Communication using RabbitMQ and SignalR
This repository contains two separate backend applications, appX and appY, which communicate through a [RabbitMQ](https://www.rabbitmq.com/) message broker. The applications can be installed on one or two machines. Both applications are almost identical (99%) and coded in the same backend language C# using [.NET 6](https://dotnet.microsoft.com/en-us/).

In addition, there is a server application called AppUiServer, which subscribes to messages from appX and appY. AppUiServer runs the AppUI frontend application and sends the messages to AppUI via [SignalR](https://dotnet.microsoft.com/en-us/apps/aspnet/signalr).

![Architecture](Architecture.png) 

**AppX:**
1. Implements the class Car which inherits from Vehicle abstract class that has type, color, plate number and creation time.
2. Stores the cars in list.
3. Every 500[ms], a new car is created, stored in the app, and sent to AppY.
4. Subscribes for Motorcycles and send them to AppUIServer 

**AppY:**
1. Implements the class Motorcycle which inherits from Vehicle abstract class that has type, color, plate number and creation time.
2. Stores a data collection of motorcycles (list).
3. Every 1000[ms], a new motorcycle is created, stored in the app, and sent to AppX.
4. Subscribes for Cars and send them to AppUIServer 

**AppUiServer:**
1. Subscribes to messages from appX and appY.
2. Runs the AppUI frontend application.
3. Sends the messages to AppUI via SignalR.

**AppUI:**
1. Creates a hub connection and subscribes to the car hub and motorcycle hub.
2. Prints the data of the last car it received and the timestamp of its creation.
3. Prints the amount of cars it received.
4. Prints the data of the last motorcycle it received and the timestamp of its creation.
5. Prints the amount of motorcycles it received.

The system provides real-time updates of the cars and motorcycles in the backend, and the frontend displays the data as it is received from the backend via SignalR.
The apps could be configured by appsettings files.

#  Instructions for running the apps
1. Download [Erlang](https://www.erlang.org/downloads) and install it **using an administrative account**.
2. Download RabbitMQ Server from the [official releases page](https://github.com/rabbitmq/rabbitmq-server/releases/tag/v3.11.13). ([Shortcut for Windows](https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.11.13/rabbitmq-server-3.11.13.exe))
3. Install RabbitMQ Server **using an administrative account**
4. Start the RabbitMQ service:
    - On Windows: Open the start menu and search for "RabbitMQ Service - start". Click on the option to start the service.
    - On other platforms: Open a terminal and run the command rabbitmq-server.
5. Download This Repository and extract the folders.
6. **Optionally**, open the **'AppsCommunication-master/AppsBuild/AppUiServer/appsettings.json'** file and replace the HTTPS URL with other IP address.
7. **Optionally**, open the **'AppX/appsettings.json'** and **'AppY/appsettings.json'** files and modify the configurations as needed.
8. Run the **'.exe'** files in each extracted folder under **'AppsBuild'** folder (AppX.exe, AppY.exe, AppUiServer.exe).
9. Open the **'AppUiServer'** console and Ctrl + Left Click on the URL address at the top of the console, or open a web browser and navigate to the URL with the same address as the console is showing (**'https://localhost:7031'** by default).
10. The dashboard should display the current status of the system, including the last car, last motorcycle and number of cars and motorcycles received.
