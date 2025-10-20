# Serverless Event-Driven Architectures on Azure

## 1. Event-Driven Architecture

- Event-Driven (EDA) is an architecture pattern that allows us to build highly scalable software and cloud systems. 
- The key advantage of the Event-Driven systems is having loosely coupled components and services.

Let’s have a look at a basic Event-Driven system design below.

### Basic Event-Driven Architecture

<img width="1645" height="818" alt="image" src="https://github.com/user-attachments/assets/52eda7e2-f89e-49f6-b1f1-e2177f9e7979" />

### 2. EDA with Mediator

- In this architecture, all events are orchestrated by the Event Mediator. 
- It decides which subscriber can handle what event. 
- It can be represented as a Serverless application(Azure function or AWS Lambda), a different web application, components in the system, or any other microservice. 
- In a simple scenario, the Event Mediator does not contain any state, neither persistent nor in-memory. 
- In complex solutions, it may contain its own database.

## 3. Event-Driven Architecture with Mediator

<img width="1842" height="822" alt="image" src="https://github.com/user-attachments/assets/a66b6669-19ce-4556-bcbf-2b444fd7626d" />

## 4. EDA with Event Bus

This is similar to the Event Mediator but the Event Bus does not serve as a mediator and does not contain any other complex logic. 
It is the same as a Message Broker Cluster. 
It serves as event storage that is implemented as a queue based on the First-In-First-Out principle.

Event-driven Architecture with Event-Bus

<img width="1522" height="688" alt="image" src="https://github.com/user-attachments/assets/f7836b41-580e-42c5-9d8a-f6e5eae851f9" />


The Event Bus can be based on the following components:

1. Azure Queue
2. Azure Service Bus
3. Apache Kafka
4. RabbitMQ
   
The choice of these components depends on how many events it should handle, the overall system, and architecture complexity. 
We will use some of these components in our architecture.

## 5. Real-world examples of the EDA

Let’s have a look at a few real-world examples.

### Image recognition web portal

This is a system that contains a Single Page App (SPA) that uses cognitive services to recognize and resize images, and store metadata in the NoSql database.

Event-Driven Architecture with Cognitive Services

<img width="1705" height="775" alt="image" src="https://github.com/user-attachments/assets/cdfa83a0-e079-42f3-9d2b-d2b901023668" />

It also uses a serverless Azure function as a microservice and the Azure EventGrid to generate events between them..

### Ocean observation data API

The NOAA Climate Data API is a project (or initiative) that gathers data from weather stations, satellites, and ocean sensors and exposes it with a public API. 
This project allows anyone to build custom applications intended to predict the weather or use data in scientific projects.

This solution uses the Event-Driven approach at its core. You can find the rough architecture diagram of the NOAA Climate Data API below.

#### The architecture contains the following components:

- Weather stations, sensors, satellites that gather data about tsunamis, water streams, hurricanes, and temperatures.
- A satellite that is used as middleware. Sensors and weather stations send data messages to the satellite. The satellite redirects these messages to a message broker cluster.
- Data centers retrieve, process, and store messages.
- The API that exposes these stored messages publicly.

Ocean observation data API structure

<img width="801" height="706" alt="image" src="https://github.com/user-attachments/assets/1503299f-89a6-475b-96a0-97f8d64337dd" />

> Important: This is an extremely simplified view of how this project works. The real project may be bigger and complex. The main idea here is to demonstrate the benefits of the Event-Driven-Architecture.

