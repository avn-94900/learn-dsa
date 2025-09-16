# Interview Questions Organized by Topic

## Java Core Concepts

### Basic Java
- What are the new features of Java 21?
- What is the difference between primitive and non-primitive data types?
- Difference between `==` and `.equals()`
- What is the output of:
  ```java
  String s1 = new String("hello");
  String s2 = new String("hello");
  s1.equals(s2);  // ?
  s1 == s2;       // ?
  ```
- Difference between `throw` and `throws`
- Difference between `final`, `finally`, `finalize`
- Difference between `HashMap` vs `Hashtable`
- Difference between `abstract class` vs `interface`

### Collections & Data Structures
- Difference between `Map`, `Set` and `List`. Tell their time complexity as well
- Arrays problem: `{1, 5, 6, 5, 5, 8, 2, 2}` - using Java Streams return unique numbers in ascending order, then descending order

### Exception Handling
- Difference between checked and unchecked exceptions
- What is exception handling and how do you implement it?
- Tell a few ways to prevent memory leaks

### Multithreading & Concurrency
- Can async programs run on main thread or separate thread?
- How can you make async calls?
- Does `CompletableFuture` work on main thread or not?
- What is `ForkJoinCommonPool`?
- How to create a thread? Write code to create a thread
- Difference between `wait()` and `notifyAll()`
- Can we write `notifyAll()` outside synchronized block?
- What is synchronized block and how it works?
- Did you use multithreading in your project? Why executor service? Why do we have a number of threads already present in Executor service?

### Garbage Collection
- What is GC (Garbage Collection)?
- Does GC get triggered automatically?
- Does GC get triggered after fixed intervals? If not, when is it triggered?
- Can we trigger GC directly?

### Java 8 Streams
- Given array `{1, 5, 6, 5, 5, 8, 2, 2}` using Java Streams return unique numbers in ascending/descending order
- Group employees by department and get average salary using Java 8 with best time complexity
- Return second highest salary from list of integers using Java 8

## Spring Boot & Spring Framework

### Core Spring Boot
- Why do we use Spring Boot for a project? Advantages of Spring Boot
- Why did you use Spring Boot in your project?
- Flow of HTTP request in a Spring Boot application
- How to return responses from DB for an HTTP request?
- If we want to disable a class from being executed in a particular environment, how could we achieve that?

### Annotations & Components
- Difference between `@Component`, `@Service` and `@Repository`
- What annotations are used to configure HTTP requests in Spring Boot?

### Dependency Injection
- What is dependency injection? How many types of dependency injections are there? Which one do you use in your project?

### Security & Authentication
- How to enable authentication for Spring Security?
- Flow of JWT based authentication
- How are you authenticating and authorizing your service?
- Explain complete flow of JWT & OAuth

## Microservices & System Design

### HTTP Methods & REST
- What HTTP methods are used in microservices?
- What are idempotent HTTP methods? (Definition)
- Which of these methods are idempotent: GET, POST, PUT, DELETE?
- Difference between PUT and PATCH methods

### Communication Patterns
- In your project, which scenario did you use synchronous communication?
- Can we set timeout in synchronous communication? If yes, how?
- What is Circuit Breaker?
- How and when do we use retry in circuit breaker?

### Transactions & Patterns
- Explain Saga Design Pattern and its types
- How do you compensate transactions in Saga with coding example?

### Scalability & Performance
- How to make DB actions and database queries more efficient?
- How to make a service scalable or more performance specific?
- How to ensure that a service receiving API requests isn't overloaded?

### System Architecture
- What is 2-tier architecture?
- Design LLD of Notification service & multiple questions around it
- What are the components involved in designing a system having only one service and one database? What AWS services will you use?

## AWS & Cloud Services

### Compute Services
- What is EC2?
- What are similar services to EC2?
- Use cases for each of them
- Why have you used EC2 instead of other computing services of AWS?
- What are the other options available that we can use besides EC2?
- Why is EC2 better than other available options?
- Difference between ECS and Lambda

### Storage Services
- What do you use for storage in EC2?
- What are the different storage offerings of AWS?
- How does each of them differ?
- Why do you use S3?
- Tell me the process for S3 connection in Spring Boot
- What are S3 bucket best practices?
- Difference between S3 and RDBMS?

### Database Services
- What are different databases provided by AWS?

### Networking & Security
- Are security groups stateless or stateful?
- What are NACLs?

### Monitoring
- What have you used for monitoring?
- How did you use Prometheus?
- How do you design a Prometheus metric in code?
- What services does AWS offer for Prometheus?
- How can you integrate it with AWS?

### Infrastructure Management
- How do you manage AWS infrastructure and technology available for it? (Terraform)

### Docker
- Why is Docker created and its advantages?

## DevOps & Deployment

### CI/CD Pipeline
- I created a new feature and want to release it. Tell the whole flow of how a pipeline would look like, from commit till deployment

## Database & SQL

### SQL Queries
- Employee table with columns: `EmployeeID INT PRIMARY KEY`, `EmployeeName VARCHAR(50)`, `ManagerID INT`
  - Write SQL query to retrieve each employee's name and their corresponding manager's name

- Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date`
  - Find the top 3 highest paid employees
  - Find departments which have more than 5 employees
  - Find second highest salary in each department

- Orders table with columns: `order_id`, `customer_id`, `product_id`, `quantity`, `amount`
  - Find all customers who have ordered all the products that customer 1 ordered

## Coding Problems

### Array Problems

#### 1. Daily Temperatures / Next Greater Element
**Problem**: Given array of temperatures, find how many days to wait for higher temperature
- **Input**: `{73, 74, 75, 71, 69, 72, 76, 73}`
- **Output**: `{1, 1, 4, 2, 1, 1, -1, -1}`
- **Follow-up**: Optimize solution, discuss time and space complexity

#### 2. Rain Water Trapping
**Problem**: Given array of non-negative integers representing elevations, determine how many units of water can be trapped
- **Example**: `{0, 1, 3, 0, 1, 2, 0, 4, 2, 0, 3, 0}` → 13 units can be trapped

#### 3. Three Sum Problem
**Problem**: Given unsorted integer array and target, return true if sum of any 3 numbers equals target
- **Input**: `arr = {3, 7, 4, 12, 8}`, `target = 19`
- **Follow-up**: Write brute force first, then optimize to O(n²), then solve using HashMap

#### 4. Count Length of Cycle
**Problem**: Given integer array, starting from `startIndex`, follow each element to index it points to until you find cycle. Return cycle length or -1
- **Test cases**:
  - `countLengthOfCycle(new int[]{1, 0}, 0) == 2`
  - `countLengthOfCycle(new int[]{1, 2, 0}, 0) == 3`

### String/Object Processing Problems

#### 5. Maximum Average Calculator
**Problem**: Given array of employees with name and marks, find maximum average marks
- **Input**: 
  ```
  {{"Alia", "-678"},
   {"Bobby", "100"}, 
   {"Alex", "223"},
   {"Alex", "-23"},
   {"Bobby", "723"}}
  ```
- **Expected**: Bobby avg = 315, Alex avg = 100, Alia avg = -678, Result: 315
- **Follow-up**: Handle negative inputs, empty arrays, invalid format using regex

### Algorithm Design Problems

#### 6. Circuit Breaker Implementation
**Problem**: If `someOtherFn()` fails 10 times consecutively, don't call it for next 10 times, just skip
```java
public Object handle() {
    // Implementation needed
    return someOtherFn();
}

private Object someOtherFn() {
    // We don't have control over this function
}
```

## Complex Scenarios

### Multi-function Coordination
**Scenario**: 3 functions where:
- f1 makes HTTP call
- f2 makes async call  
- f3 merges response of both
**Questions**: How to coordinate? Threading considerations?

### Project-Specific Questions
- Tell me about the most complex issue you faced in your previous project
- Explain your project and how you optimized large number of queries
- Instead of sharding, what other optimization techniques can you think of?
- How did you handle 2-way sync in your project?
- Any challenging task you worked on in your previous project?