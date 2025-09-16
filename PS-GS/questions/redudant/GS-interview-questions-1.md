# Interview Questions & Notes - Organized

## Data Structures & Algorithms (DSA)

### Array Problems
1. **Sort Array with 0s, 1s, and 2s**
   - Sort an array containing only 0s, 1s, and 2s

2. **Three Sum Problem**
   - Given array: `int[] num = {1,7,11,4}` and `target = 16`
   - Find three numbers that sum to the target value

3. **Second Smallest Element**
   - Given array: `[1,1,2,3,4,5]`
   - Find second smallest number ignoring duplicates (answer should be 1)

4. **Trapping Rain Water (Snowpack Problem)**
   - Given array of building heights: `[5, 1, 3, 2, 4]`
   - Calculate amount of water/snow trapped between buildings

5. **Student Marks Maximum Average**
   - Given 2D array: `[["ABC", 80], ["DEF", 90], ["EFG", 70], ["ABC", 100]]`
   - Return maximum average among all students

6. **Common Elements in Matrix Rows**
   - Given m x n matrix, find all common elements present in all rows in O(mn) time
   - Example input:
     ```
     mat[4][5] = {{1, 2, 1, 4, 8},
                  {3, 7, 8, 5, 1},
                  {8, 7, 7, 3, 1},
                  {8, 1, 2, 7, 9}};
     ```
   - Expected output: 1 8 (elements present in all rows)

7. **Subarray Partitioning Problem**
   - Given integer array nums of length n
   - Determine if array can be split into subarrays of length k where:
     - Each subarray contains k distinct integers in ascending order
     - Each integer used exactly as many times as it appears
     - Integers in subarray must be distinct and sorted ascending
   - Example: `[1,1,1,2,2,3,3,3,4,5,6,7,8,9,10]` with k=3
   - Should return true if possible, false otherwise

### Stack & Queue
8. **Reverse Stack**
   - Reverse a stack with or without using additional data structure

### String Problems
9. **Robot Movement Tracker**
   - Robot starts at origin (0,0) on 2D grid
   - Commands: 'u' (up), 'd' (down), 'l' (left), 'r' (right)
   - Input example: "uuuddlrl"
   - Track robot's final position

## System Design & Architecture

### Browser Tab Management System
**Scenario-Based Design Problem:**
- Design a browser tab management system with following scenarios:
  1. When closing active tab, switch to previous tab
  2. When closing non-active tab, keep current tab active
  3. Handle edge case when first tab is active

**Suggested Data Structure:**
- LinkedHashSet for maintaining insertion order
- Variables: currentActiveTab, index
- Methods: openTab(), movement(), removeTab()

### Load Balancing & Distributed Systems
10. **Trade Version Processing**
    - Handle millions of trades (Trade1_v1, Trade1_v2, etc.) with 3 processors
    - Ensure all versions of same trade processed by same processor
    - Achieve load balancing and fast lookup
    - **Suggested Solutions:**
      - Consistent Hashing
      - Kafka partitioning based on trade ID
      - Redis for persistent trade-to-processor mapping

11. **Video Processing Server Calculation**
    - Calculate exact number of servers needed if:
      - One video takes 30 seconds to process
      - All videos should be processed within 60 seconds
      - Daily load: 1 million video uploads

12. **DDOS Prevention**
    - How to prevent multiple same requests from clogging/breaking system

13. **API Parameter Validation**
    - How to validate parameters being sent on API calls

14. **File Processing with Multithreading**
    - Process file with millions of transaction records (sorted by time)
    - Design solution using multithreading

15. **Database Insertion Optimization**
    - File with 1000s of records
    - Insert only rows not present in SQL database

## Java Core & Multithreading

### Threading & Concurrency
16. **ExecutorService Implementation**
    - Write code snippet for ExecutorService with 100 thread pool
    - How to create threads

17. **Thread Counter Optimization**
    - Create two threads that increment counter with optimization

18. **Multithreading Use Cases**
    - Situations where multithreading is useful

19. **Deadlock & Race Condition Handling**
    - Ways to handle deadlock and racing conditions

20. **Runnable Class Implementation**
    - Create class extending Runnable
    - Execute logic through Executor framework

### Java Synchronization
21. **CountDownLatch**
    - What is CountDownLatch?
    - Is it similar to wait() & notifyAll()?

22. **Java Locks**
    - What locks are available in Java?
    - Difference between Semaphore and CountDownLatch
    - What is ReentrantLock and its purpose?

23. **Future vs CompletableFuture**
    - Differences between Future and CompletableFuture

### Java Fundamentals
24. **Static Keyword Usage**
    - Use of static keyword
    - When are static data members loaded into memory?

25. **Void Method Return Statement**
    - What happens when using "return;" in void method?

26. **HashMap Internals**
    - Do we store hashcode in bucket?

27. **JVM Internal Working**
    - Explain JVM internal mechanisms

## Time Series Data Management

### Data Structure Design
**Problem:** Handle time series data in format: User -> Time -> Mood
```
Amrish 1 Happy
Amrish 2 Happy  
Aditya 1 Sad
Amrish 4 Happy
```

**Requirements:**
- Implement setter: `set(String user, int time, String mood)`
- Implement getter: `get(String user, int time)`
- Return exact entry if found for user at specific time
- Otherwise return last entry for user if time < requested time
- Return "Not-Found" if no valid entry exists

**Suggested Data Structure:**
```
Amrish -> [1-> Happy, 2-> Happy, 4->Sad]
Aditya -> [1-> Sad]
```

## Spring Boot & Frameworks

### Spring Framework
28. **Spring vs Spring Boot**
    - Key differences
    - Dependency management with Maven

29. **Spring Security**
    - What is @AuthenticationPrincipal UserDetails?
    - Where do authenticated user details come from?
    - How to authenticate users in Spring Boot?
    - What is Security Context?

30. **Request Logging**
    - How to log all requests coming to application?

### API Design & Backward Compatibility
31. **API Consumption Changes**
    - Handle API provider adding new attributes without breaking
    - Handle API provider removing attributes without breaking

32. **API Provider Backward Compatibility**
    - Ensure APIs are always backward compatible

## Database & Caching

### SQL vs NoSQL
33. **Database Selection**
    - SQL vs NoSQL comparison
    - When to use SQL over NoSQL

### Redis
34. **Redis Cache Usage**
    - Where to use Redis Cache
    - Redis retention policies

## Message Queues & Streaming

### Apache Kafka
35. **Kafka Topic Management**
    - How Kafka topics work with different number of consumers
    - Same consumer group handling different message types

36. **Kafka Alternatives**
    - Alternative messaging systems to Kafka

## Infrastructure & DevOps

### Reverse Proxy
37. **Reverse Proxy Concepts**
    - What is reverse proxy?
    - Reverse proxy frameworks used

### Cloud Services
38. **AWS Services Usage**
    - How/where did you use Kafka/SQL/S3?
    - Alternatives to these services

## System Architecture

### Microservices
39. **Microservices Architecture**
    - Explain microservices architecture patterns and principles

---

## Additional Technical Areas Covered
- **Performance Optimization**
- **Scalability Patterns**
- **Data Processing**
- **Thread Safety**
- **Distributed Systems**
- **Cloud Architecture**