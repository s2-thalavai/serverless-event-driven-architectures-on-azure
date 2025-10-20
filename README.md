# Serverless Event-Driven Architectures on Azure

## Event-Driven Architecture

- Event-Driven (EDA) is an architecture pattern that allows us to build highly scalable software and cloud systems. 
- The key advantage of the Event-Driven systems is having loosely coupled components and services.

Let’s have a look at a basic Event-Driven system design below.

### Basic Event-Driven Architecture

<img width="1645" height="818" alt="image" src="https://github.com/user-attachments/assets/52eda7e2-f89e-49f6-b1f1-e2177f9e7979" />

### EDA with Mediator

- In this architecture, all events are orchestrated by the Event Mediator. 
- It decides which subscriber can handle what event. 
- It can be represented as a Serverless application(Azure function or AWS Lambda), a different web application, components in the system, or any other microservice. 
- In a simple scenario, the Event Mediator does not contain any state, neither persistent nor in-memory. 
- In complex solutions, it may contain its own database.

## Event-Driven Architecture with Mediator

<img width="1842" height="822" alt="image" src="https://github.com/user-attachments/assets/a66b6669-19ce-4556-bcbf-2b444fd7626d" />

