# 📚 Comprehensive Interview Notes & Question Bank

> **Last Updated**: February 2026 | **Format**: Organized by Topic with Numbered Questions

---

# 🧵 Java Multithreading & Concurrency – Interview Notes

### Concurrency and Parallelism

| Number | Question |
| ------ | ---------- |
| 1 | Difference between Concurrency vs Parallelism |
| 2 | What are the benefits of `volatile` keyword? |
| 3 | What is the *Happen-Before* relationship, and which concurrency concepts provide it? |

---

## 🔹 Thread Basics

| Number | Question |
| ------ | ---------- |
| 1 | How many ways can we create a Thread? |
| 2 | How to get the reference of the current Thread? |
| 3 | What is the purpose of `start()` method? |
| 4 | Thread lifecycle states |
| 5 | What is the purpose of `join()` and `yield()` methods? |
| 6 | Difference between `sleep()` and `wait()` |
| 7 | Where will you use `wait()`, `notify()`, and `notifyAll()`? For which use cases are they most useful? |
| 8 | When does `IllegalMonitorStateException` occur? |

---

## 🔹 Synchronization and Locks

| Number | Question |
| ------ | ---------- |
| 1 | What are Critical Sections and Race Conditions? |
| 2 | How many ways can we avoid race conditions? |
| 3 | What is the difference between `Lock` and `synchronized`? |
| 4 | What are the benefits of a synchronized block? |
| 5 | What is a ReentrantLock? |
| 6 | What are the benefits of Lock and ReentrantLock? |
| 7 | Implement a custom Lock using synchronization |
| 8 | Difference between `volatile` and `synchronized` keyword |

---

## 🔹 Advanced Threading Concepts

| Number | Question |
| ------ | ---------- |
| 1 | What is Compare-And-Swap (CAS) method, and where is it used? |
| 2 | Which concepts provide atomic operation features? |
| 3 | Which concepts provide visibility of values between threads? |
| 4 | What are the benefits of `AtomicReference` / `AtomicInteger` compared to synchronization? |

---

## 🔹 Thread Pools and Executors

| Number | Question |
| ------ | ---------- |
| 1 | What are the types of thread pools in the Executor framework? |
| 2 | For what kind of task would you choose a Fixed Thread Pool? |
| 3 | For what kind of task would you choose a Cached Thread Pool? |
| 4 | What is the thread pool size of a Fixed Thread Pool? |
| 5 | What is the thread pool size of a Cached Thread Pool? |
| 6 | What are the types of tasks that are submitted to Thread Executors? |
| 7 | List the number of ways we can create a Task and implement it |
| 8 | Implement a Custom Thread Pool |
| 9 | ExecutorService Implementation - Write code snippet for ExecutorService with 100 thread pool |

---

## 🔹 Callable, Future, and CompletableFuture

| Number | Question |
| ------ | ---------- |
| 1 | What is the difference between Callable and Runnable? |
| 2 | What is a Future object? Where will you use it? Benefits & drawbacks? |
| 3 | What is CompletableFuture? |
| 4 | Difference between Future and CompletableFuture |
| 5 | Advantages of CompletableFuture |
| 6 | Write a code snippet for the methods of CompletableFuture |

---

## 🔹 Synchronization Challenges

| Number | Question |
| ------ | ---------- |
| 1 | Difference between Block and Wait state |
| 2 | Implement Deadlock |
| 3 | What is Semaphore? |
| 4 | What is CyclicBarrier and its use case? |
| 5 | What is CountDownLatch and its use case? |
| 6 | Is CountDownLatch similar to wait() & notifyAll()? |
| 7 | What is Exchanger? |
| 8 | Implement the Producer-Consumer problem |
| 9 | Write a program to print even and odd numbers in order using 2 threads (`T1` prints Odd, `T2` prints Even) |
| 10 | Write a program to implement Read-Write Lock |
| 11 | Implement a custom Blocking Queue |
| 12 | What locks are available in Java? |
| 13 | Difference between Semaphore and CountDownLatch |

---

## 🔹 Exception Handling in Multithreading

| Number | Question |
| ------ | ---------- |
| 1 | How do you handle exception when one process in multithreading failed? |

---

## 🔹 Miscellaneous Multithreading

| Number | Question |
| ------ | ---------- |
| 1 | How to create a custom Immutable Object? Why is it important in multithreading? |
| 2 | What is the `Unsafe` class? Where is it used, and how is it useful? |
| 3 | Can async programs run on main thread or separate thread? |
| 4 | How can you make async calls? |
| 5 | Does `CompletableFuture` work on main thread or not? |
| 6 | What is `ForkJoinCommonPool`? |

---

# ☕ Java Core Concepts

## 🔹 Basic Java

| Number | Question |
| ------ | ---------- |
| 1 | What are the new features of Java 21? |
| 2 | What is the difference between primitive and non-primitive data types? |
| 3 | Difference between `==` and `.equals()` |
| 4 | What is the output of: `String s1 = new String("hello");` `String s2 = new String("hello");` `s1.equals(s2);` `s1 == s2;` |
| 5 | Difference between `throw` and `throws` |
| 6 | Difference between `final`, `finally`, `finalize` |
| 7 | Difference between `HashMap` vs `Hashtable` |
| 8 | Difference between `abstract class` vs `interface` |

---

## 🔹 Collections & Data Structures

| Number | Question |
| ------ | ---------- |
| 1 | Difference between `Map`, `Set` and `List`. Tell their time complexity as well |
| 2 | Arrays problem: `{1, 5, 6, 5, 5, 8, 2, 2}` - using Java Streams return unique numbers in ascending order, then descending order |
| 3 | Group employees by department and get average salary using Java 8 with best time complexity |
| 4 | Return second highest salary from list of integers using Java 8 |
| 5 | Do we store hashcode in bucket? (HashMap Internals) |

---

## 🔹 Exception Handling

| Number | Question |
| ------ | ---------- |
| 1 | Difference between checked and unchecked exceptions |
| 2 | What is exception handling and how do you implement it? |
| 3 | Tell a few ways to prevent memory leaks |

---

## 🔹 Garbage Collection

| Number | Question |
| ------ | ---------- |
| 1 | What is GC (Garbage Collection)? |
| 2 | Does GC get triggered automatically? |
| 3 | Does GC get triggered after fixed intervals? If not, when is it triggered? |
| 4 | Can we trigger GC directly? |

---

## 🔹 Java Fundamentals

| Number | Question |
| ------ | ---------- |
| 1 | Use of static keyword. When are static data members loaded into memory? |
| 2 | What happens when using "return;" in void method? |
| 3 | Explain JVM internal mechanisms |

---

# 🌱 Spring & Spring Boot Interview Notes

## 🔹 Spring Core

| Number | Question |
| ------ | ---------- |
| 1 | What is the role of `@Configuration` in a Spring application? |
| 2 | What is the difference between `@Component` and `@Configuration` annotations in Spring? |
| 3 | How does `@Bean` annotation work in Spring? |
| 4 | Can you explain the difference between singleton and prototype scope in Spring? |
| 5 | What is a transaction in Spring? |
| 6 | How does Spring manage transactions? |
| 7 | What are the different propagation levels available in Spring transactions? |
| 8 | How can you configure transaction management in Spring? |
| 9 | What is the role of `@Transactional` annotation in Spring? |
| 10 | What are some best practices for using transactions in Spring? |

---

## 🔹 Spring Boot Essentials

| Number | Question |
| ------ | ---------- |
| 1 | Why do we use Spring Boot for a project? Advantages of Spring Boot |
| 2 | Why did you use Spring Boot in your project? |
| 3 | Flow of HTTP request in a Spring Boot application |
| 4 | How to return responses from DB for an HTTP request? |
| 5 | If we want to disable a class from being executed in a particular environment, how could we achieve that? |

---

## 🔹 Annotations & Components

| Number | Question |
| ------ | ---------- |
| 1 | Difference between `@Component`, `@Service` and `@Repository` |
| 2 | What annotations are used to configure HTTP requests in Spring Boot? |

---

## 🔹 Dependency Injection

| Number | Question |
| ------ | ---------- |
| 1 | What is dependency injection? How many types of dependency injections are there? |
| 2 | Which type of dependency injection do you use in your project? |

---

## 🔹 Spring Security

| Number | Question |
| ------ | ---------- |
| 1 | What is Spring Security and what are its core features? |
| 2 | How does Spring Security integrate with Spring Framework? |
| 3 | What are the different authentication providers supported by Spring Security? |
| 4 | What is the difference between authentication and authorization in Spring Security? |
| 5 | How can you configure Spring Security to use a custom authentication provider? |
| 6 | What is CSRF protection and how does Spring Security provide it? |
| 7 | How does Spring Security handle password encoding and storage? |
| 8 | What is role-based access control and how is it implemented in Spring Security? |
| 9 | How does Spring Security handle session management and prevention of session fixation attacks? |
| 10 | What is OAuth2 and how does Spring Security support it? |
| 11 | How to enable authentication for Spring Security? |
| 12 | What is @AuthenticationPrincipal UserDetails? |
| 13 | Where do authenticated user details come from? |
| 14 | How to authenticate users in Spring Boot? |
| 15 | What is Security Context? |

---

## 🔹 Request Handling & Logging

| Number | Question |
| ------ | ---------- |
| 1 | How to log all requests coming to application? |

---

## 🔹 Spring Interceptors and Filters

| Number | Question |
| ------ | ---------- |
| 1 | What is the difference between Spring Interceptors and Filters? |
| 2 | How can you register an Interceptor in a Spring application? |
| 3 | What are the common use cases for using Interceptors in Spring? |
| 4 | How does Spring Interceptor chaining work? |
| 5 | What is the difference between a `preHandle` and `postHandle` method in an Interceptor? |
| 6 | How do you configure a Filter in a Spring application? |
| 7 | What is the order of execution of Filters in a Spring application? |
| 8 | How can you customize the order of execution of Filters in a Spring application? |
| 9 | How do Filters differ from Interceptors in terms of execution context? |
| 10 | What are some common use cases for using Filters in Spring? |

---

## 🔹 JPA & ORM

| Number | Question |
| ------ | ---------- |
| 1 | What is JPA and how does it work? |
| 2 | How can you use JPA in a Spring application? |
| 3 | What is lazy loading in JPA and why is it useful? |
| 4 | What is the difference between a join and a fetch in JPA? |
| 5 | How can you implement pagination in a JPA query? |
| 6 | What is a transaction in JPA and why is it important? |
| 7 | How can you optimize performance in a JPA application? |

---

## 🔹 Error Handling & API Documentation

| Number | Question |
| ------ | ---------- |
| 1 | What is error handling in Spring and how can it be implemented? |
| 2 | What is the Open API Specification? |
| 3 | How can you generate documentation for a Spring application using the Open API Specification? |

---

## 🔹 API Design & Backward Compatibility

| Number | Question |
| ------ | ---------- |
| 1 | How to handle API provider adding new attributes without breaking |
| 2 | How to handle API provider removing attributes without breaking |
| 3 | Ensure APIs are always backward compatible |

---

# 🔑 OAuth & Authentication

## 🔹 OAuth Fundamentals

| Number | Question |
| ------ | ---------- |
| 1 | What is OAuth and how does it work? |
| 2 | What are the benefits of using OAuth over traditional authentication methods? |
| 3 | What are the different OAuth grant types and how are they used? |
| 4 | How does OAuth handle user consent and authorization? |
| 5 | What security measures should be taken when implementing OAuth? |
| 6 | What are some common vulnerabilities in OAuth implementations and how can they be prevented? |
| 7 | How does OAuth integrate with Single Sign-On (SSO) systems? |
| 8 | What role do access tokens and refresh tokens play in OAuth? |
| 9 | How does OAuth handle API access and resource authorization? |
| 10 | How can OAuth be used for delegated access and user impersonation? |
| 11 | Explain complete flow of JWT & OAuth |

---

## 🔹 JWT Authentication

| Number | Question |
| ------ | ---------- |
| 1 | Flow of JWT based authentication |
| 2 | How are you authenticating and authorizing your service? |

---

# 🏗️ Microservices & System Design

## 🔹 HTTP Methods & REST Concepts

| Number | Question |
| ------ | ---------- |
| 1 | What HTTP methods are used in microservices? |
| 2 | What are idempotent HTTP methods? (Definition) |
| 3 | Which of these methods are idempotent: GET, POST, PUT, DELETE? |
| 4 | Difference between PUT and PATCH methods |

---

## 🔹 Communication Patterns

| Number | Question |
| ------ | ---------- |
| 1 | In your project, which scenario did you use synchronous communication? |
| 2 | Can we set timeout in synchronous communication? If yes, how? |
| 3 | What is Circuit Breaker? |
| 4 | How and when do we use retry in circuit breaker? |

---

## 🔹 Distributed Transaction Patterns

| Number | Question |
| ------ | ---------- |
| 1 | Explain Saga Design Pattern and its types |
| 2 | How do you compensate transactions in Saga with coding example? |

---

## 🔹 Scalability & Performance

| Number | Question |
| ------ | ---------- |
| 1 | How to make DB actions and database queries more efficient? |
| 2 | How to make a service scalable or more performance specific? |
| 3 | How to ensure that a service receiving API requests isn't overloaded? |

---

## 🔹 System Architecture Design

| Number | Question |
| ------ | ---------- |
| 1 | What is 2-tier architecture? |
| 2 | Design LLD of Notification service & multiple questions around it |
| 3 | What are the components involved in designing a system having only one service and one database? |
| 4 | What AWS services will you use? |

---

## 🔹 Browser Tab Management System (Design Problem)

| Number | Scenario |
| ------ | ---------- |
| - | **Design a browser tab management system with following scenarios:** 1. When closing active tab, switch to previous tab 2. When closing non-active tab, keep current tab active 3. Handle edge case when first tab is active **Suggested Data Structure:** LinkedHashSet for maintaining insertion order, Variables: currentActiveTab, index, Methods: openTab(), movement(), removeTab() |

---

## 🔹 Load Balancing & Distributed Systems

| Number | Problem |
| ------ | ---------- |
| 1 | **Trade Version Processing** - Handle millions of trades (Trade1_v1, Trade1_v2, etc.) with 3 processors. Ensure all versions of same trade processed by same processor. Achieve load balancing and fast lookup. **Suggested Solutions:** Consistent Hashing, Kafka partitioning based on trade ID, Redis for persistent trade-to-processor mapping |
| 2 | **Video Processing Server Calculation** - Calculate exact number of servers needed if: One video takes 30 seconds to process, All videos should be processed within 60 seconds, Daily load: 1 million video uploads |
| 3 | **DDOS Prevention** - How to prevent multiple same requests from clogging/breaking system |
| 4 | **API Parameter Validation** - How to validate parameters being sent on API calls |
| 5 | **File Processing with Multithreading** - Process file with millions of transaction records (sorted by time). Design solution using multithreading |
| 6 | **Database Insertion Optimization** - File with 1000s of records. Insert only rows not present in SQL database |

---

# 🗄️ Database & SQL

## 🔹 SQL vs NoSQL

| Number | Question |
| ------ | ---------- |
| 1 | SQL vs NoSQL comparison |
| 2 | When to use SQL over NoSQL |
| 3 | Difference between S3 and RDBMS? |

---

## 🔹 SQL Query Problems

| Number | Query Problem |
| ------ | ---------- |
| 1 | Employee table with columns: `EmployeeID INT PRIMARY KEY`, `EmployeeName VARCHAR(50)`, `ManagerID INT` - Write SQL query to retrieve each employee's name and their corresponding manager's name |
| 2 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find the top 3 highest paid employees |
| 3 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find departments which have more than 5 employees |
| 4 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find second highest salary in each department |
| 5 | Orders table with columns: `order_id`, `customer_id`, `product_id`, `quantity`, `amount` - Find all customers who have ordered all the products that customer 1 ordered |

---

## 🔹 Redis & Caching

| Number | Question |
| ------ | ---------- |
| 1 | Where to use Redis Cache |
| 2 | Redis retention policies |

---

# 💬 Message Queues & Streaming

## 🔹 Apache Kafka

| Number | Question |
| ------ | ---------- |
| 1 | How Kafka topics work with different number of consumers |
| 2 | Same consumer group handling different message types |
| 3 | How/where did you use Kafka? |

---

## 🔹 Messaging Alternatives

| Number | Question |
| ------ | ---------- |
| 1 | Alternative messaging systems to Kafka |

---

# ☁️ AWS & Cloud Services

## 🔹 Compute Services

| Number | Question |
| ------ | ---------- |
| 1 | What is EC2? |
| 2 | What are similar services to EC2? |
| 3 | Use cases for each of them |
| 4 | Why have you used EC2 instead of other computing services of AWS? |
| 5 | What are the other options available that we can use besides EC2? |
| 6 | Why is EC2 better than other available options? |
| 7 | Difference between ECS and Lambda |

---

## 🔹 Storage Services

| Number | Question |
| ------ | ---------- |
| 1 | What do you use for storage in EC2? |
| 2 | What are the different storage offerings of AWS? |
| 3 | How does each of them differ? |
| 4 | Why do you use S3? |
| 5 | Tell me the process for S3 connection in Spring Boot |
| 6 | What are S3 bucket best practices? |
| 7 | How/where did you use S3? |

---

## 🔹 Database Services

| Number | Question |
| ------ | ---------- |
| 1 | What are different databases provided by AWS? |
| 2 | How/where did you use SQL in AWS? |

---

## 🔹 Networking & Security

| Number | Question |
| ------ | ---------- |
| 1 | Are security groups stateless or stateful? |
| 2 | What are NACLs? |

---

## 🔹 Monitoring & Observability

| Number | Question |
| ------ | ---------- |
| 1 | What have you used for monitoring? |
| 2 | How did you use Prometheus? |
| 3 | How do you design a Prometheus metric in code? |
| 4 | What services does AWS offer for Prometheus? |
| 5 | How can you integrate it with AWS? |

---

## 🔹 Infrastructure Management

| Number | Question |
| ------ | ---------- |
| 1 | How do you manage AWS infrastructure and technology available for it? (Terraform) |

---

# 🐳 DevOps & Deployment

## 🔹 Docker

| Number | Question |
| ------ | ---------- |
| 1 | Why is Docker created and its advantages? |

---

## 🔹 CI/CD Pipeline

| Number | Question |
| ------ | ---------- |
| 1 | I created a new feature and want to release it. Tell the whole flow of how a pipeline would look like, from commit till deployment |

---

## 🔹 Reverse Proxy

| Number | Question |
| ------ | ---------- |
| 1 | What is reverse proxy? |
| 2 | Reverse proxy frameworks used |

---



## 🔹 Algorithm Design

| Number | Problem |
| ------ | ---------- |
| 1 | **Circuit Breaker Implementation** - If `someOtherFn()` fails 10 times consecutively, don't call it for next 10 times, just skip. Implementation needed for `handle()` method |

---



# 🤝 Project-Specific & Behavioral Questions

## 🔹 Complex Scenarios

| Number | Question |
| ------ | ---------- |
| 1 | Tell me about the most complex issue you faced in your previous project |
| 2 | Explain your project and how you optimized large number of queries |
| 3 | Instead of sharding, what other optimization techniques can you think of? |
| 4 | How did you handle 2-way sync in your project? |
| 5 | Any challenging task you worked on in your previous project? |
| 6 | Multi-function Coordination: 3 functions where f1 makes HTTP call, f2 makes async call, f3 merges response of both. How to coordinate? Threading considerations? |

---

## 🔹 Project Experience

| Number | Question |
| ------ | ---------- |
| 1 | Did you use multithreading in your project? |
| 2 | Why executor service? |
| 3 | Why do we have a number of threads already present in Executor service? |
| 4 | How to create a thread? Write code to create a thread |
| 5 | Thread Counter Optimization - Create two threads that increment counter with optimization |
| 6 | Multithreading Use Cases - Situations where multithreading is useful |
| 7 | Deadlock & Race Condition Handling - Ways to handle deadlock and racing conditions |
| 8 | Runnable Class Implementation - Create class extending Runnable. Execute logic through Executor framework |

---

# 📝 Java 8 Features & Streams

## 🔹 Streams & Functional Programming

| Number | Problem |
| ------ | ---------- |
| 1 | Given array `{1, 5, 6, 5, 5, 8, 2, 2}` using Java Streams return unique numbers in ascending/descending order |
| 2 | Group employees by department and get average salary using Java 8 with best time complexity |
| 3 | Return second highest salary from list of integers using Java 8 |

---

# 🎯 Quick Reference

## Study Tips
- Review one topic daily
- Complete at least one coding problem from each section
- Prepare short answers (1-2 sentences) for each question
- Practice implementing design problems in code
- Relate questions to your project experience

## Topics by Priority
1. **Core Java & Multithreading** - Most asked
2. **Spring Boot & Microservices** - Very important
3. **Database & SQL** - Fundamental
4. **System Design** - For senior roles
5. **AWS & DevOps** - If role requires it

---

*Document organized with consistent markdown styling and tabular format for easy revision and reference.*
