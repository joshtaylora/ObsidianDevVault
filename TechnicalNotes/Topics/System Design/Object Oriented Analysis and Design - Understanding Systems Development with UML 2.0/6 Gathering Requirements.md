## Chapter Outline
- 6.1 Introduction
- 6.2 The Birth of a System
- 6.3 Use Cases
- 6.4 Business Perspective
- 6.5 Developer Perspective
- 6.6 Summary

## 6.1 Introduction
- Goals of the requirements phase:
	- Examine the business context: you need to clarify the reasons for wanting the software to be developed in the first place
	- Describe the system requirements: detect constraints and decide on the functionality of the system
- Before writing any software you need to investigate the business in which the software will operate
	- Without a thorough understanding of the business, how can you build anything that will enhance the business?
- Once you understand the business and document your understanding as business requirements, you can begin to think about what your software will do for the users
- System requirements can be separated into two categories:
	- `functional requirements`: the things the system must be able to do
	- `non-functional requirements`: everything else that needs to be specified

## 6.2 The Birth of a System
- Developers must be able to transform the customer's requirements document or mission statement into a complete, unambiguous description of the system to be developed, in a standard format that the customer can understand and ratify

## 6.3 Use Case
- Most nonfunctional requirements can be recorded alongside a closely-related use case
- `Use cases` are used to document your understanding of the way a business operates (business requirements modeling) and to specify what your new software system should be able to do (system requirements modeling)
- Use cases start with a participant called an `actor` and then descends into the business, or system, and eventually returns to the actor
- The effect of each use case should be of value to the actor

## 6.4 Business Perspective
- Use cases will contain the use case model as well as the following:
	- Actor list with descriptions
	- Glossary
	- Use cases with descriptions and details
	- Communication diagrams
	- Activity diagrams

### 6.4.1 Identifying Business Actors
- An actor is either a person playing some role within a business, a department, or a separate operating system
- Departments and systems interact as if they were people themselves -> we're interested in who/what initiates inter-actions and the sequence of steps

### 6.4.2 Writing the Project Glossary
- Start maintaining a glossary at this stage in order to de-mystify the jargon for anyone examining your software development artifacts
- Each entry in the glossary defines a term
- List of relationships between terms and the development phases:
	- Business actor
	- Business object
	- System actor
	- System object
	- Analysis object
	- Deployment artifact
	- Design object
	- Design node
	- Design layer
	- Design package