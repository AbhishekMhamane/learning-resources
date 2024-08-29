# Quarkus Learning

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