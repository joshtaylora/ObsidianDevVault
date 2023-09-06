## Definitions
- `component`: a unit of software that is independently replaceable and upgradeable
- `libraries`: components that are linked into a program and called using in-memory function calls
- `services`: out-of-process components who communicate with a mechanism such as a web service request, or remote procedure call
- `semantic monitoring`: this type of monitoring runs a subset of an application's automated tests against the live production system on a regular basis with the results being pushed to the monitoring service which then triggers alerts in case of failures
---
## Introduction
- The microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often as HTTP resource API
	- These services are built around business capabilities and independently deployable by fully automated deployment machinery
---
## When should we use Microservices?
- Benefits:
	- Strong Module Boundaries
	- Independent Deployment
		- Autonomous, simple services are easy to deploy and less likely to cause system failures when they go wrong
	- Technology Diversity
		- Different services can use different languages, frameworks, and data-storage tech
- Costs:
	- Distribution
		- Remote calls are slow and at risk of failure
	- Eventual Consistency
		- distributed systems make maintaining strong consistency difficult
	- Operational Complexity
---
## Characteristics of a Microservice Architecture

### Componentization via Services
- Microservice architecture solves componentizing software by breaking it down into services
- Services are independently deployable
- If you have an application that consists of multiple libraries in a single process mean that a change to a single component will result in having to redeploy the entire application
	- This is why we use services as components instead of libraries
- Decomposing the application into multiple services means that single service changes require only the redeployment of the changed component
- **The aim of a good microservice architecture is to provide cohesive service boundaries and evolution mechanisms in the service contracts**

### Organized around Business Capabilities

- Services are organized around business capability
	- Cross-functional teams develop services with a broad-stack implementation for their business are, including user-interface, persistent storage, and any external collaborations

### Products not Projects

- Most app dev efforts use a project model: the aim is deliver some piece of software which is then considered to be completed
	- On completion, the software is handed over to a maintenance organization and the project team that built it is disbanded
- Microservices are best built with a different kind of model: the team should own the product over its full lifetime
- Rather than looking at the software as a set of functionality to be completed, there is an on-going relationship where the question is how can software assist its users to enhance the business capability

### Smart endpoints and dumb pipes

- Applications built from microservices aim to be as decoupled and cohesive as possible
	- They own their own domain logic and act more as filters -> receiving a request, applying logic as appropriate and producing a response
- These are choreographed using simple RESTish protocols
- The two most commonly used protocols are:
	- HTTP request-response with resource APIs
	- Lightweight messaging
- Messaging is done over a lightweight message bus
	- The infrastructure chosen is dumb in the sense that it acts as a message router only

### Decentralized Data Management

- At the most abstract level, decentralization of data management means that the conceptual model of the world will differ between systems
- Domain-Driven Design divides a complex domain up into multiple bounded contexts and maps out the relationships between them
- Microservices decentralize data storage decisions
	- Monolithic apps prefer a single logical db for persistent data
	- Microservices prefer letting each service manage its own database, either different instances of the same database technology, or entirely different database systems
![[decentralised-data.png]]

### Infrastructure Automation

- We want as much confidence as possible that our software is working so we run lots of automated tests in our deployment pipelines
- Working software is promoted to a higher environment in the pipeline when the automated tests all pass and all pipeline checks are validated
	- This means that we can automate deployments to each new environment
![[xs4rzmqa.bmp]]

### Design for failure

- Using services as components means that the application needs to be designed so that it can tolerate the failure of services
- Any service call cloud fail due to the unavailibility of the supplier
	- The client has to respond to this as gracefully as possible
- Failures need to be detected quickly and, when possible, the failing service should be automatically restored
- Microservice apps require a lot of emphasis on real-time monitoring of the app with both architectural concerns ( requests per second that the database is receiving) and business relevant metrics (like how many orders per minute are received)
- Semantic monitoring can  be used as an early warning system of something going wrong and thus trigger dev teams to follow up and investigate

### Evolutionary Design

- The key property of a component is the notion of independent replacement and upgradeability
	- This implies that you look for points where you can imagine rewriting a component without affecting its collaborators
- Drive modularity through the pattern of change -> you want to keep things that change at the same time in the same module
	- Parts of a system that change rarely should be in different services to those that are currently undergoing lots of church
	- If you find yourself repeatedly changing two services together, that's a sign that they should be merged