# Backend and Frontend Communication using RabbitMQ and SignalR
This repository contains two separate backend applications, appX and appY, which communicate through a [RabbitMQ](https://www.rabbitmq.com/) message broker. The applications can be installed on one or two machines. Both applications are almost identical (99%) and coded in the same backend language C# using [.NET 6](https://dotnet.microsoft.com/en-us/).

In addition, there is a server application called AppUiServer, which subscribes to messages from appX and appY. AppUiServer runs the AppUI frontend application and sends the messages to AppUI via [SignalR](https://dotnet.microsoft.com/en-us/apps/aspnet/signalr).

AppX:\
a. Implements the class Car. Each car has its own properties (type, color, plate number, creation time).\
b. Stores a data collection of cars (list).\
c. Every 500[ms], a new car is created, stored in the appX data structure, and sent to AppY.

AppY:\
a. Implements the class Motorcycle. Each motorcycle has its own properties (type, color, plate number, creation time).\
b. Stores a data collection of motorcycles (list).\
c. Every 1000[ms], a new motorcycle is created, stored in the appY data structure, and sent to AppX.\
d. appX and appY transmit the data to AppUiServer.

AppUiServer:\
a. Subscribes to messages from appX and appY.\
b. Runs the AppUI frontend application.\
c. Sends the messages to AppUI via SignalR.

AppUI:\
a. Creates a hub connection and subscribes to the car hub and motorcycle hub.\
b. Prints the data of the last car it received and the timestamp of its creation.\
c. Prints the amount of cars it received.\
d. Prints the data of the last motorcycle it received and the timestamp of its creation.\
e. Prints the amount of motorcycles it received.

The system provides real-time updates of the cars and motorcycles in the backend, and the frontend displays the data as it is received from the backend via SignalR.
