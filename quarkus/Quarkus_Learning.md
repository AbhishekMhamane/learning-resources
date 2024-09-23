# Quarkus Learning

---

## Table of Contents

- [What is Quarkus?](#what-is-quarkus)
- [Differences Between GraalVM and OpenJDK HotSpot](#differences-between-graalvm-and-openjdk-hotspot)
- [What is Reactive Architecture Style or Reactive Programming?](#what-is-reactive-architecture-style-or-reactive-programming)
- [Imperative vs Declarative Programming](#imperative-vs-declarative-programming)
- [Blocking vs Non-Blocking](#blocking-vs-non-blocking)
- [Asynchronous vs Non-Blocking](#asynchronous-vs-non-blocking)
- [CDI (Contexts and Dependency Injection) in Quarkus](#cdi-contexts-and-dependency-injection-in-quarkus)
- [MicroProfile in Quarkus](#microprofile-in-quarkus)

---

### Important Links

- [RedHat Quarkus](https://developers.redhat.com/learn/quarkus)
- [The Reactive Manifesto](https://www.reactivemanifesto.org/)
- [Quarkus Reactive Architecture](https://quarkus.io/guides/quarkus-reactive-architecture)

---

### What is Quarkus?

- Quarkus is a Kubernetes Native Java stack tailored for **OpenJDK HotSpot** and **GraalVM**, crafted from the best of breed Java libraries and standards.
- It uses **Reactive architecture style**.

---

### Differences Between GraalVM and OpenJDK HotSpot

- Polyglot Capabilities:  
    GraalVM: Supports multiple languages (Java, JavaScript, Ruby, Python, R).
    OpenJDK HotSpot: Primarily supports Java.

- Native Image Generation:  
    GraalVM: Allows ahead-of-time (AOT) compilation to native executables, reducing startup time and memory usage.
    OpenJDK HotSpot: Uses just-in-time (JIT) compilation, which compiles code at runtime.

- Performance:  
    GraalVM: Uses advanced compilation techniques for potentially better performance.
    OpenJDK HotSpot: Mature and stable performance with extensive optimizations over time.

- Tooling Support:  
    GraalVM: Provides tools for debugging, monitoring, and profiling, with a focus on polyglot applications.
    OpenJDK HotSpot: Extensive support for debugging, monitoring, and profiling tools for Java applications.

- Interoperability:
    GraalVM: Enables interoperability between different programming languages.
    OpenJDK HotSpot: Focuses on Java and its ecosystem.

---

### What is Reactive Architecture Style or Reactive Programming?

Reactive programming is programming with asynchronous data streams.Reactive Systems are more flexible, loosely-coupled and scalable. This makes them easier to develop and amenable to change. They are significantly more tolerant of failure and when failure does occur they meet it with elegance rather than disaster. Reactive Systems are highly responsive, giving users effective interactive feedback.

#### Characteristics of reactive systems

- **Responsive**: The system responds in a timely manner if at all possible. Responsiveness is the cornerstone of usability and utility, but more than that, responsiveness means that problems may be detected quickly and dealt with effectively. Responsive systems focus on providing rapid and consistent response times, establishing reliable upper bounds so they deliver a consistent quality of service. This consistent behaviour in turn simplifies error handling, builds end user confidence, and encourages further interaction.
    - Example: Consider a simple web application that fetches user data from a database. In a responsive system, the application should quickly return the user data or provide an appropriate message if the data is not available. This ensures that the system can handle other requests while waiting for the database operation to complete, thus maintaining responsiveness. Database operation will be done asynchronously. This means that the main thread is not blocked while waiting for the database operation to complete. Instead, the operation runs in a separate thread, allowing the main thread to continue handling other incoming requests. This non-blocking behavior is key to maintaining responsiveness in a reactive system.

- **Resilient**: The system stays responsive in the face of failures. This means that the system should be able to recover from failures quickly and gracefully.Following up on this notion of responsiveness, reactive systems stay responsive when parts of the system fail. As you’ll see, our system has multiple components, each of which is isolated from the others. That means any failure is confined to one component, not the entire system. When the complete application is deployed, we can start and stop different components without affecting the entire system.
    - Example : Consider a web application that fetches user data from a database. If the database is temporarily unavailable, the application should handle this gracefully by returning a cached response or an appropriate error message, rather than crashing. Designed to be resilient by handling database failures gracefully. If the database fetch operation fails, the system returns cached data or an appropriate error message, ensuring that the failure does not affect the entire system.

- **Elastic**: The system can scale up and down as needed. Because the components of a reactive system are creating and consuming events asynchronously, it’s likely that the resources needed by a particular component will change significantly over time. A reactive system scales those resources up and down as necessary.
    - Example: Consider a web application that experiences varying levels of traffic throughout the day. During peak hours, the application should be able to scale up its resources to handle the increased load, and during off-peak hours, it should scale down to save resources. This dynamic scaling ensures that the system remains responsive and cost-effective.

- **Message driven**: The final piece of the puzzle is that reactive systems use asynchronous message passing to communicate with each other. Message passing, by its very nature, promotes loose coupling between components, and doing things asynchronously protects one component from a failure in another. If a component is producing messages, it won’t know if a component that consumes those messages fails or degrades in some way. Similarly, a message consumer won’t know if any of the producers fail. 
    - Example: Consider a web application that fetches user data from a database. The application uses a message broker to send and receive messages between components. When a user requests data, the application sends a message to the database component to fetch the data. The database component processes the message and sends a response back to the application. This message-driven architecture ensures that the components are loosely coupled and can communicate asynchronously, making the system more resilient and responsive.

---

### Imperative vs Declarative Programming

- **Imperative Programming**: In imperative programming, you tell the computer what to do or how to do  step by step. You specify the exact steps that the computer must take to accomplish a task. This is similar to writing a recipe, where you list the ingredients and the steps to prepare the dish. In imperative programming, you specify the exact steps that the computer must take to accomplish a task. This approach is often used in procedural programming languages like C, where you write code that explicitly tells the computer what to do.
    - Example: Consider a simple program that calculates the sum of the first n numbers. In an imperative programming style, you would write a loop that iterates over the numbers and calculates the sum step by step.
       ```java
        public class ImperativeSum {
              public static void main(String[] args) {
              int n = 10;
              int sum = 0;
            
                    for (int i = 1; i <= n; i++) {
                        sum += i;
                    }
            
                    System.out.println("Sum of first " + n + " numbers is: " + sum);
              }
        }
      ```
- **Declarative Programming**: In declarative programming, you specify what you want to achieve without specifying how to achieve it. You describe the desired outcome, and the computer figures out how to achieve it. This is similar to writing a shopping list, where you list the items you need without specifying how to obtain them. In declarative programming, you describe the desired outcome without specifying the exact steps to achieve it. This approach is often used in functional programming languages like Haskell, where you write code that describes the desired result rather than the exact steps to achieve it.
    - Example: Consider the same program that calculates the sum of the first n numbers. In a declarative programming style, you would use a higher-order function like reduce to calculate the sum without specifying the exact steps.
       ```java
        import java.util.stream.IntStream;
        
        public class DeclarativeSum {
            public static void main(String[] args) {
                int n = 10;
                int sum = IntStream.rangeClosed(1, n).sum();
        
                System.out.println("Sum of first " + n + " numbers is: " + sum);
            }
        }
       ```
---

### Blocking vs Non-Blocking

- **Blocking:** In a blocking operation, the execution of a thread or process is halted until a certain task completes. For example, a thread might wait for a file to be read or a database query to complete before continuing. This approach is simple but inefficient for high-load systems, as resources are tied up while waiting.

- **Non-Blocking:** Non-blocking operations allow a thread to initiate a task and then move on to other work while the task completes in the background. For example, a request to a database might be sent, and instead of waiting for a response, the system handles other tasks, processing the result when it’s available. Non-blocking is crucial for high-performance, scalable systems, as it maximizes resource utilization.

---

### Asynchronous vs Non-Blocking

- **Asynchronous**: In the asynchronous example, the operation starts, and you immediately get control back as well. However, instead of checking repeatedly if the operation is done, you simply provide a callback that gets triggered when the operation completes. The flow of your program doesn’t pause to wait or check the operation; it moves on, and the result is handled when ready, making the process completely asynchronous.

- **Non-Blocking**: In the non-blocking example, the operation starts, and you immediately get control back to do other work. You might keep checking if the operation is done, but you're not waiting idly. You might still check synchronously (like in a loop) if the data is ready, which is why non-blocking can sometimes be synchronous (you are just not blocking while checking).

---

## CDI (Contexts and Dependency Injection) in Quarkus

**CDI (Contexts and Dependency Injection)** is a key component in Quarkus that provides a standardized mechanism for managing dependencies and lifecycle events in Java applications. CDI is part of the **Jakarta EE** specification (formerly Java EE), and in Quarkus, it's used for implementing **Inversion of Control (IoC)** and **Dependency Injection (DI)**, allowing developers to build loosely coupled, maintainable applications.

### Inversion of Control (IoC)
Inversion of Control (IoC) is a design principle in software engineering where the control of objects or portions of a program is transferred from the developer's code to a framework or external entity. This allows for greater flexibility, modularity, and testability by decoupling the execution flow from the logic of the components.

#### Key Concepts of IoC
- Traditional Control Flow: In traditional programming, the developer controls how and when objects are instantiated and how they interact. For example, if you want a class to use another class, you would instantiate it directly in your code.
- Inversion of Control: In IoC, the control of creating and managing the lifecycle of objects is transferred to a framework or container. The framework decides when to create objects, inject dependencies, and manage the application's lifecycle. This "inversion" refers to the transfer of responsibility from the programmer to the framework. Instead of manually creating dependencies, a framework (like Spring, CDI in Quarkus, etc.) handles that for you. The key part is that the framework injects the dependencies where needed.

#### IoC in Quarkus:
- **Dependency Injection (DI)**: The most common implementation of IoC is Dependency Injection, where the framework injects required dependencies into objects rather than objects creating dependencies themselves.
    - Constructor Injection: Dependencies are provided via constructor arguments.
    - Setter Injection: Dependencies are provided via setter methods.
    - Field Injection: Dependencies are injected directly into fields.
      ```java
        import javax.inject.Inject;
        import javax.enterprise.context.ApplicationScoped;
        
        @ApplicationScoped
        public class MyService {
        public void process() {
        System.out.println("Service is processing...");
        }
        }
        
        @ApplicationScoped
        public class MyApplication {
        
        @Inject
        MyService service;  // IoC: Service instance is injected automatically
        
        public void start() {
            service.process();
        }
        }
      ```

### How CDI Works in Quarkus

#### 1. Dependency Injection (DI)
CDI allows you to inject dependencies (objects) into your classes without needing to manage the instantiation and lifecycle of these objects manually. This makes your application modular and easily testable.

##### Example: Basic CDI Dependency Injection
```java
import javax.inject.Inject;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class GreetingService {
    public String greet(String name) {
        return "Hello, " + name;
    }
}

@ApplicationScoped
public class Greeter {
    // Inject the GreetingService dependency
    @Inject
    GreetingService greetingService;

    public void sayHello() {
        System.out.println(greetingService.greet("Quarkus"));
    }
}
```
In the example above:
- The `@Inject` annotation is used to inject an instance of `GreetingService` into the `Greeter` class.
- Quarkus (through CDI) will handle the instantiation of `GreetingService` and manage its lifecycle.

#### 2. Lifecycle and Scopes
CDI provides different lifecycle scopes, and Quarkus uses these to manage how beans are created and destroyed.

##### Common CDI Scopes in Quarkus:
- **@ApplicationScoped**: The bean is created once for the entire application and shared across all requests (singleton).
- **@RequestScoped**: A new instance is created for each HTTP request and destroyed at the end of the request.
- **@SessionScoped**: A bean tied to a user session (typically for web applications).
- **@Dependent**: The default scope where a new instance is created every time the bean is injected.

##### Example:
```java
import javax.enterprise.context.RequestScoped;

@RequestScoped
public class RequestBean {
    // This bean will have a new instance for every request
}
```

#### 3. Qualifiers
Qualifiers allow you to inject specific implementations of an interface or class when multiple beans of the same type exist.

##### Example: Using Qualifiers
```java
import javax.enterprise.inject.Default;
import javax.enterprise.inject.Alternative;
import javax.inject.Inject;

@Default
@ApplicationScoped
public class StandardGreeting implements GreetingService {
    public String greet(String name) {
        return "Hello, " + name;
    }
}

@Alternative
@ApplicationScoped
public class CasualGreeting implements GreetingService {
    public String greet(String name) {
        return "Hey, " + name;
    }
}

@Inject
@Default
GreetingService greetingService; // Injects StandardGreeting
```

In this case, the `@Default` qualifier is used to select the `StandardGreeting` implementation, and `@Alternative` is used to define an alternative, which can be activated under certain conditions.

#### 4. Producer Methods
Sometimes, you may need to create beans dynamically or configure them at runtime. In such cases, CDI provides **producer methods** that allow you to define how beans are instantiated.

##### Example: Producer Method in CDI
```java
import javax.enterprise.context.ApplicationScoped;
import javax.enterprise.inject.Produces;

@ApplicationScoped
public class ConfigProducer {
    @Produces
    @ApplicationScoped
    public Config createConfig() {
        return new Config("production");
    }
}
```
Here, the `@Produces` annotation is used to define a method that produces a bean of type `Config`. The `Config` object is then available for injection wherever needed.

#### 5. Events
CDI provides an **event system** that allows beans to interact in a decoupled manner. Components can fire events, and others can observe and respond to these events.

##### Example: Firing and Observing Events
```java
import javax.enterprise.event.Event;
import javax.enterprise.event.Observes;
import javax.inject.Inject;

public class MessageService {

    @Inject
    Event<String> messageEvent;

    public void sendMessage(String message) {
        messageEvent.fire(message); // Fire an event
    }
}

public class MessageListener {
    
    public void onMessage(@Observes String message) {
        System.out.println("Received message: " + message); // Observes the event
    }
}
```
In this example:
- The `MessageService` fires an event containing a message.
- The `MessageListener` observes the event and responds when the message is fired.

#### 6. Interceptors and Decorators
CDI allows you to use interceptors and decorators for cross-cutting concerns like logging, security, or transaction management.

##### Example: Using Interceptors
```java
import javax.interceptor.AroundInvoke;
import javax.interceptor.Interceptor;
import javax.interceptor.InvocationContext;

@Interceptor
@Logged // Custom annotation for logging
public class LoggingInterceptor {
    
    @AroundInvoke
    public Object logMethodInvocation(InvocationContext context) throws Exception {
        System.out.println("Calling method: " + context.getMethod().getName());
        return context.proceed(); // Proceed with the original method call
    }
}
```
In this example, the interceptor logs method invocations for all methods annotated with `@Logged`.

#### 7. Lazy Loading
Quarkus leverages CDI's support for lazy loading, ensuring beans are only instantiated when they are needed, improving performance and resource utilization.

#### 8. Integration with Quarkus
Quarkus optimizes CDI to work well with its **GraalVM native compilation**, which strips down unnecessary reflection and proxy overheads, resulting in faster startup times and lower memory usage.

### Conclusion
In Quarkus, CDI provides a powerful way to manage dependencies, lifecycle, and interactions between components in a cloud-native, microservices-based architecture. Its integration in Quarkus is lightweight, efficient, and highly optimized for environments like Kubernetes, helping developers focus on business logic while handling concerns such as dependency injection, event handling, and lifecycle management.

---

## MicroProfile in Quarkus

**MicroProfile** in Quarkus is a set of enterprise Java standards and specifications that focus on building cloud-native, lightweight, and optimized microservices. The MicroProfile specification is designed to work alongside the Java EE (now Jakarta EE) platform but is specifically tailored for developing microservices with features such as fault tolerance, health checks, metrics, and configuration.
Quarkus implements the MicroProfile specification, allowing developers to leverage these features to build highly scalable and resilient microservices while maintaining a lightweight runtime and fast startup times.
Eclipse MicroProfile is a framework that helps developers build microservices and cloud-native applications for enterprise Java. It's an open source project that aims to simplify the development of microservices and cloud deployment.

### Key MicroProfile Features in Quarkus

Here’s a breakdown of the key MicroProfile features available in Quarkus:

#### 1. MicroProfile Config
- **Purpose**: Simplifies externalized configuration of applications.
- **Concept**: MicroProfile Config allows you to inject configuration values into your application from different sources (environment variables, system properties, or custom properties files).
- **Quarkus Example**:
  ```java
  @Inject
  @ConfigProperty(name = "my.custom.property", defaultValue = "defaultValue")
  String myProperty;
  ```

- **Benefits**:
    - Enables flexibility by allowing configuration changes without modifying the application.
    - Supports hierarchical configurations across environments.

#### 2. MicroProfile Health
- **Purpose**: Provides endpoints to report the health status of an application.
- **Concept**: This feature allows applications to expose their health status (e.g., database connectivity, external services) through a `/health` endpoint.
- **Quarkus Example**:
  ```java
  @Readiness
  @ApplicationScoped
  public class DatabaseHealthCheck implements HealthCheck {
      @Override
      public HealthCheckResponse call() {
          return HealthCheckResponse.up("Database is up");
      }
  }
  ```

- **Benefits**:
    - Useful for Kubernetes or OpenShift environments to perform liveliness and readiness probes.
    - Ensures that applications are only exposed when they are in a healthy state.

#### 3. MicroProfile Metrics
- **Purpose**: Collects and exposes metrics about the application.
- **Concept**: It allows developers to monitor the performance and resource usage of their application by exposing data like memory usage, CPU, response times, and more via a `/metrics` endpoint.
- **Quarkus Example**:
  ```java
  @Counted(name = "requestCount", description = "How many requests have been processed")
  public String process() {
      return "Processed";
  }
  ```

- **Benefits**:
    - Integrates easily with monitoring systems such as Prometheus.
    - Helps in observing real-time performance and behavior of microservices.

#### 4. MicroProfile Fault Tolerance
- **Purpose**: Adds resilience to microservices through patterns like retries, circuit breakers, timeouts, and bulkheads.
- **Concept**: Allows developers to create resilient microservices by defining how their applications should handle failures of downstream systems or external dependencies.
- **Quarkus Example**:
  ```java
  @ApplicationScoped
  public class ExternalService {
      
      @Retry(maxRetries = 3)
      @Timeout(500)
      @Fallback(fallbackMethod = "fallbackResponse")
      public String callExternalService() {
          // External service call logic
      }
      
      public String fallbackResponse() {
          return "Fallback response";
      }
  }
  ```

- **Benefits**:
    - Reduces the risk of cascading failures in a distributed system.
    - Improves the robustness of applications by handling failures gracefully.

#### 5. MicroProfile JWT Propagation
- **Purpose**: Propagates JSON Web Tokens (JWT) between microservices for authentication and authorization.
- **Concept**: JWT tokens are used to secure microservices, and this feature ensures that tokens can be validated and propagated across services in a secure manner.
- **Quarkus Example**:
  ```java
  @RolesAllowed("user")
  @GET
  public String getSecureResource(@Context SecurityContext securityContext) {
      Principal userPrincipal = securityContext.getUserPrincipal();
      return "Hello, " + userPrincipal.getName();
  }
  ```

- **Benefits**:
    - Simplifies the implementation of security in microservices.
    - Provides a standardized way of handling identity and permissions across services.

#### 6. MicroProfile OpenAPI
- **Purpose**: Automatically generates OpenAPI documentation for RESTful endpoints.
- **Concept**: OpenAPI provides a specification for documenting RESTful APIs. MicroProfile OpenAPI helps developers generate API documentation without needing to write it manually.
- **Quarkus Example**:
  ```java
  @Path("/api")
  public class MyResource {
      
      @Operation(summary = "Get details", description = "Gets the details of an item.")
      @GET
      public String getItem() {
          return "Item";
      }
  }
  ```

    - The documentation is automatically generated and exposed via a `/openapi` endpoint.

- **Benefits**:
    - Provides clear API documentation for developers and users of the API.
    - Helps in understanding API endpoints, request/response formats, and error handling.

#### 7. MicroProfile REST Client
- **Purpose**: Simplifies the consumption of external REST services.
- **Concept**: It allows developers to create type-safe clients for consuming REST APIs, using annotated interfaces to represent the external services.
- **Quarkus Example**:
  ```java
  @RegisterRestClient
  public interface MyRestClient {
      @GET
      @Path("/items")
      List<Item> getItems();
  }

  @Inject
  @RestClient
  MyRestClient myRestClient;
  ```

- **Benefits**:
    - Makes REST API calls more manageable by abstracting boilerplate code.
    - Enables easy integration with external services and APIs.

#### 8. MicroProfile OpenTracing
- **Purpose**: Provides distributed tracing capabilities to trace requests across microservices.
- **Concept**: Allows tracing the flow of requests as they travel through multiple microservices, helping to identify bottlenecks or issues in distributed systems.
- **Quarkus Example**:
    - Quarkus automatically enables OpenTracing for tracing service calls if the appropriate dependency is included.

- **Benefits**:
    - Enhances observability in complex, distributed microservices environments.
    - Helps in troubleshooting performance issues across services.

#### 9. MicroProfile Context Propagation
- **Purpose**: Propagates context (e.g., security, transaction, etc.) across different threads in an asynchronous execution environment.
- **Concept**: Allows the current context (like security credentials or transaction boundaries) to be propagated from one thread to another, enabling asynchronous and reactive programming patterns.
- **Benefits**:
    - Simplifies asynchronous programming in microservices.
    - Ensures consistency in context when executing code across different threads.

### Why MicroProfile in Quarkus?

MicroProfile makes it easier to build **enterprise-grade microservices** by providing a set of essential features like configuration management, monitoring, security, fault tolerance, and more. In Quarkus, these features are optimized to work with minimal overhead and maximum performance.
- **Cloud-Native Ready**: MicroProfile is tailored for developing microservices that will run in cloud environments like Kubernetes, and Quarkus provides built-in integrations for deployment to Kubernetes, OpenShift, and other platforms.
- **Optimized for Microservices**: MicroProfile's features focus on the needs of microservices architectures, such as handling service failures, monitoring, health checks, and more, which are key in distributed systems.

Quarkus brings the power of **MicroProfile** to developers by implementing these standards in a lightweight, optimized framework. By using MicroProfile in Quarkus, developers can leverage a variety of specifications that are essential for building robust, scalable, and cloud-native microservices. It allows you to focus on your business logic while Quarkus manages the rest — from configuration and health checks to security, tracing, and resilience.

---