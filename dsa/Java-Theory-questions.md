# Interview Theory Questions & Conceptual Topics

## Java Core Concepts & Fundamentals

### Basic Java Concepts
1. **Java Features & Versions**
   - What are the new features of Java 21?
   - What is the difference between primitive and non-primitive data types?

2. **Object Comparison & Memory**
   - Difference between `==` and `.equals()`
   - Use of static keyword
   - When are static data members loaded into memory?

3. **Exception Handling**
   - Difference between `throw` and `throws`
   - Difference between checked and unchecked exceptions
   - What is exception handling and how do you implement it?

4. **Keywords & Modifiers**
   - Difference between `final`, `finally`, `finalize`
   - What happens when using "return;" in void method?

5. **Collections & Data Structures Theory**
   - Difference between `HashMap` vs `Hashtable`
   - Difference between `Map`, `Set` and `List`. Tell their time complexity as well
   - HashMap Internals - Do we store hashcode in bucket?

6. **Object-Oriented Programming**
   - Difference between `abstract class` vs `interface`

7. **Memory Management**
   - Tell a few ways to prevent memory leaks
   - JVM Internal Working - Explain JVM internal mechanisms

### Garbage Collection
1. **GC Fundamentals**
   - What is GC (Garbage Collection)?
   - Does GC get triggered automatically?
   - Does GC get triggered after fixed intervals? If not, when is it triggered?
   - Can we trigger GC directly?

### Java Multithreading & Concurrency Theory

#### Threading Concepts
1. **Thread Basics**
   - Multithreading Use Cases - Situations where multithreading is useful
   - Can async programs run on main thread or separate thread?
   - How can you make async calls?

2. **Synchronization Mechanisms**
   - What is synchronized block and how it works?
   - Difference between `wait()` and `notifyAll()`
   - Can we write `notifyAll()` outside synchronized block?

3. **Advanced Threading**
   - Deadlock & Race Condition Handling - Ways to handle deadlock and racing conditions
   - Does `CompletableFuture` work on main thread or not?
   - What is `ForkJoinCommonPool`?

#### Java Concurrency Utilities
4. **CountDownLatch & Synchronization**
   - What is CountDownLatch?
   - Is it similar to wait() & notifyAll()?

5. **Java Locks**
   - What locks are available in Java?
   - Difference between Semaphore and CountDownLatch
   - What is ReentrantLock and its purpose?

6. **Future & Asynchronous Programming**
   - Future vs CompletableFuture - Differences between Future and CompletableFuture

7. **Project Experience**
   - Did you use multithreading in your project? Why executor service? Why do we have a number of threads already present in Executor service?

## Spring Boot & Spring Framework Theory

### Core Spring Boot Concepts
1. **Framework Fundamentals**
   - Why do we use Spring Boot for a project? Advantages of Spring Boot
   - Why did you use Spring Boot in your project?
   - Spring vs Spring Boot - Key differences
   - Dependency management with Maven

2. **Request Flow & Architecture**
   - Flow of HTTP request in a Spring Boot application
   - How to return responses from DB for an HTTP request?
   - If we want to disable a class from being executed in a particular environment, how could we achieve that?

### Spring Annotations & Components
3. **Component Architecture**
   - Difference between `@Component`, `@Service` and `@Repository`
   - What annotations are used to configure HTTP requests in Spring Boot?

4. **Dependency Injection**
   - What is dependency injection? How many types of dependency injections are there? Which one do you use in your project?

### Spring Security & Authentication
5. **Security Framework**
   - How to enable authentication for Spring Security?
   - What is @AuthenticationPrincipal UserDetails?
   - Where do authenticated user details come from?
   - How to authenticate users in Spring Boot?
   - What is Security Context?
   - Flow of JWT based authentication
   - How are you authenticating and authorizing your service?
   - Explain complete flow of JWT & OAuth

6. **Monitoring & Logging**
   - How to log all requests coming to application?

## Microservices & System Design Theory

### HTTP Methods & REST Architecture
1. **REST Fundamentals**
   - What HTTP methods are used in microservices?
   - What are idempotent HTTP methods? (Definition)
   - Which of these methods are idempotent: GET, POST, PUT, DELETE?
   - Difference between PUT and PATCH methods

### Communication Patterns
2. **Service Communication**
   - In your project, which scenario did you use synchronous communication?
   - Can we set timeout in synchronous communication? If yes, how?

3. **Resilience Patterns**
   - What is Circuit Breaker?
   - How and when do we use retry in circuit breaker?

### Transaction Management
4. **Distributed Transactions**
   - Explain Saga Design Pattern and its types

### System Architecture Concepts
5. **Architecture Patterns**
   - What is 2-tier architecture?
   - Microservices Architecture - Explain microservices architecture patterns and principles
   - Design LLD of Notification service & multiple questions around it
   - What are the components involved in designing a system having only one service and one database? What AWS services will you use?

### Performance & Scalability
6. **Optimization Strategies**
   - How to make DB actions and database queries more efficient?
   - How to make a service scalable or more performance specific?
   - How to ensure that a service receiving API requests isn't overloaded?
   - Instead of sharding, what other optimization techniques can you think of?

### API Design & Backward Compatibility
7. **API Management**
   - API Consumption Changes - Handle API provider adding new attributes without breaking
   - API Provider Backward Compatibility - Ensure APIs are always backward compatible
   - API Parameter Validation - How to validate parameters being sent on API calls
   - DDOS Prevention - How to prevent multiple same requests from clogging/breaking system

## AWS & Cloud Services Theory

### Compute Services
1. **EC2 & Computing**
   - What is EC2?
   - What are similar services to EC2?
   - Use cases for each of them
   - Why have you used EC2 instead of other computing services of AWS?
   - What are the other options available that we can use besides EC2?
   - Why is EC2 better than other available options?
   - Difference between ECS and Lambda

### Storage Services
2. **Storage Solutions**
   - What do you use for storage in EC2?
   - What are the different storage offerings of AWS?
   - How does each of them differ?
   - Why do you use S3?
   - What are S3 bucket best practices?
   - Difference between S3 and RDBMS?

### Database Services
3. **Database Options**
   - What are different databases provided by AWS?

### Networking & Security
4. **Network Architecture**
   - Are security groups stateless or stateful?
   - What are NACLs?

### Monitoring & Observability
5. **Monitoring Solutions**
   - What have you used for monitoring?
   - How did you use Prometheus?
   - What services does AWS offer for Prometheus?
   - How can you integrate it with AWS?

### Infrastructure Management
6. **Infrastructure as Code**
   - How do you manage AWS infrastructure and technology available for it? (Terraform)

7. **Containerization**
   - Why is Docker created and its advantages?

## Database & Caching Theory

### Database Fundamentals
1. **SQL vs NoSQL**
   - Database Selection - SQL vs NoSQL comparison
   - When to use SQL over NoSQL

### Caching Strategies
2. **Redis & Caching**
   - Redis Cache Usage - Where to use Redis Cache
   - Redis retention policies

## Message Queues & Streaming Theory

### Apache Kafka
1. **Kafka Fundamentals**
   - Kafka Topic Management - How Kafka topics work with different number of consumers
   - Same consumer group handling different message types
   - Kafka Alternatives - Alternative messaging systems to Kafka

2. **Project Usage**
   - How/where did you use Kafka/SQL/S3?
   - Alternatives to these services

## Infrastructure & DevOps Theory

### Reverse Proxy & Load Balancing
1. **Proxy Concepts**
   - What is reverse proxy?
   - Reverse proxy frameworks used

### CI/CD & Deployment
2. **Pipeline Management**
   - I created a new feature and want to release it. Tell the whole flow of how a pipeline would look like, from commit till deployment

## Advanced Topics & Best Practices

### Performance Optimization
- Performance Optimization strategies
- Scalability Patterns
- Data Processing best practices
- Thread Safety considerations
- Distributed Systems concepts
- Cloud Architecture patterns

### Project Experience Questions
- Tell me about the most complex issue you faced in your previous project (non-coding aspects)
- How you approached system design decisions in your previous projects
- What architecture patterns did you implement and why?