## Intro
- This chapter will focus on 
	- How to build a set of cooperating microservices using Spring Boot
	- How to develop functionality that delivers business value
- This chapter will discuss developing microservices that:
	- Contain business logic based on plain Spring Beans
	- Expose REST APIs using Spring WebFlux
	- Have APIs documented using springdoc-openapi
	- Spring Data will be used to store data in both SQL and NoSQL databases in order to make the data processed by the microservices persistent
	- Use Docker to run as containers
## Convention over configuration and fat JAR files
- Spring Boot is strongly opinionated about how to set up both core modules from the Spring Framework and third-party products such as libraries that are used for logging or connecting to a database
- Spring Boot accomplishes this by applying several conventions by default, thus limiting the need for configuration
- When required, each convention can be overridden by writing some configuration
	- This design pattern is known as `convention over configuration` and minimizes the need for initial configuration
- Spring Boot also favors a runtime model based on a standalone JAR file, aka a `fat JAR file` allowing us to start a service with a simple command such as `java -jar app.jar`
### The magic @SpringBootApplication annotation
- The `@SpringBootApplication` annotation, when applied to a class that contains the static main method, initiates the convention based autoconfiguration mechanism
- This annotation provides the following functionality:
	- Enables component scanning: it will look for Spring components and configuration classes in the package of the application class and all its sub-packages
	- The application itself becomes a configuration class
	- Enables autoconfiguration, meaning that Spring Boot will look for JAR files in the classpath that it can configure automatically
## Component scanning
- If you have a Spring component in the package of the application class or in one of it's sub-packages, another component in the application can get this component automatically injected (`auto-wiring`)  using the `@Autowired` annotation
- Ex:
```java
@Component 
public class MyComponentImpl implements MyComponent { ...

public class AnotherComponent {
	
	private final MyComponent myComponent;

	@Autowired
	public AnotherComponent(MyComponent myComponent) {
		this.myComponent = myComponent;
	}
}
```
