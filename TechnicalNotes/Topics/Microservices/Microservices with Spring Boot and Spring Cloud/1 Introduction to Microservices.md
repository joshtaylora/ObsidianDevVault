## Topics Covered
- What is a microservice-based architecture?
- Challenges with Microservices
- Design patterns for handling challenges
- Software enablers that can enable us to handle these challenges
- Other important considerations that aren't covered in this book

## Benefits of autonomous software components
- Customer can deploy parts of the platform in its own system landscape, integrating it with its existing systems using its well-defined APIs
- Another customer can choose to replace parts of the platform's functionality with implementations that already exist in the customer's system landscape, potentially requiring some adoption of the existing functionality in the platform's APIs
- Each component in the platform can be delivered and upgraded separately
- Each component in the platform can also be scaled out to multiple servers independently of the other components
## Enter microservices
- `Horizontal Scaling`: deploying a component on a number of smaller servers and placing a load balancer in front of it
## A sample microservice landscape
- This book will use a small set of cooperating microservices that we will evolve throughout the book that looks like the following illustration:
	![[Pasted image 20230907152916.png]]
## Defining a microservice
- Microservice architecture is about splitting up monolithic applications into smaller components, achieving the following goals: 
	- Faster development, enabling continuous deployments
	- Easier to scale, manually or automatically
- Microservices are essentially an autonomous software component that is independently upgradeable, replaceable, and scalable
- In order to act as an autonomous component, the service must fulfill the following criteria:
	- Must conform to a shared nothing architecture: microservices don't share data in databases with each other
	- Must only communicate through well-defined interfaces, either APIs and synchronous services or by sending messages asynchronously
	- Must be deployed as separate runtime processes
		- Each microservice runs in a separate runtime process i.e Docker container
	- Microservice instances are stateless so that incoming requests to a microservice can be handled by any of its instances
- How big should a microservice be?
	- Small enough to fit in the head of a developer
	- Big enough to not jeopardize performance (latency) and/or data consistency (SQL foreign keys between data that's stored in different microservices)
## Challenges with microservices
- Synchronous communication between many small components can cause a chain of failure problem
- Keeping configuration for many small components up to date can be challenging
- Hard to track a request that's being processed and involves many components
- Analyzing hardware resource usage on a component level can be challenging
- Manual configuration and management of many small components can become costly and error-prone
- 8 Fallacies of distributed systems
	- The network is reliable
	- Latency is zero
	- Bandwidth is infinite
	- The network is secure
	- Topology doesn't change
	- There is one administrator
	- Transport cost is zero
	- The network is homogenous
## Design patterns for microservices
- Service discovery
- Edge server
- Reactive microservices
- Central configuration
- Centralized log analysis
- Distributed tracing
- Circuit breaker
- Control loop
- Centralized monitoring and alarms
- The following approach will be used for describing design patterns:
	- The problem
	- A solution
	- Requirements for the solution
## Service Discovery
### Problem
- How can clients find microservices and their instances?
- Typically, microservice instances are assigned dynamically allocated IP addresses when they start up
- This makes it difficult for a client to make a request to a microservice that exposes a REST API over HTTP
### Solution
- Add a new component: `service discovery service` to the system landscape that keeps track of currently available microservices and the IP addresses of its instances
### Solution Requirements
- Automatically register/unregister microservices and their instances as they come and go
- The client must be able to make a request to a logical endpoint for the microservice
	- The request will be routed to one of the available microservice instances
- Requests to a microservice must be load balanced over the available instances
- We must be able to detect instances that currently are unhealthy, so that requests will not be routed to them

## Edge server
### Problem
- In a system landscape of microservices, it is in many cases desirable to expose some of the microservices to the outside of the system landscape and hide the remaining microservices from external access
	- The exposed microservices must be protected against requests from malicious clients
### Solution
- Add a new component called an `edge server` to the system landscape that all incoming requests will go through
	- The edge server behaves like a reverse proxy and can be integrated with a discovery service to provide dynamic load-balancing capabilities
### Solution requirements
- Hide internal services that should not be exposed outside their context
	- only route requests to microservices that are configured to allow external requests
- Expose external services and protect them from malicious requests
	- use standard protocols and best practices to ensure that the clients are trustworthy

## Reactive Microservices
### Problem
- Java programs traditionally implement synchronous communication using blocking I/O using RESTful JSON API over HTTP
- Using a blocking I/O requires the thread to be allocated from the operating system for the length of the request
	- this means that if the number of concurrent requests goes up, a server might run out of available threads in the operating system
- Microservice architecture can make this problem worse as a chain of cooperating microservices is used to serve a request
### Solution 
- Use non-blocking I/O to ensure that no threads are allocated while waiting for processing to occur in another service i.e a database or other microservice
### Solution requirements
- Whenever feasible, use an asynchronous programming model, sending messages without waiting for the receiver to process them
- If a synchronous programming model is preferred, use reactive frameworks that can execute synchronous requests using non-blocking I/O, without allocating a thread while waiting for a response
- Microservices must be designed to be resilient and self-healing
	- Resilient meaning capable of producing a response even if one of the services it depends on fails
	- Self-healing meaning that once the failing service is operational again, the microservice must be able to resume using it