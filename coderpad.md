# Interview Coding Problems & Practical Questions

## Java 8 Streams & Lambdas

### Stream Operations
1. **Array Processing with Streams**
   - Given array: `{1, 5, 6, 5, 5, 8, 2, 2}`
   - Using Java Streams return unique numbers in ascending order
   - Using Java Streams return unique numbers in descending order

2. **Employee Data Processing**
   - Group employees by department and get average salary using Java 8 with best time complexity
   - Return second highest salary from list of integers using Java 8

3. **Collections Comparison Output**
   - What is the output of:
     ```java
     String s1 = new String("hello");
     String s2 = new String("hello");
     s1.equals(s2);  // ?
     s1 == s2;       // ?
     ```

## SQL Queries & Database Problems

### Employee Management Queries
1. **Employee-Manager Relationship**
   - Employee table: `EmployeeID INT PRIMARY KEY`, `EmployeeName VARCHAR(50)`, `ManagerID INT`
   - Write SQL query to retrieve each employee's name and their corresponding manager's name

2. **Employee Analytics**
   - Employee table: `id`, `name`, `dept`, `salary`, `hire_date`
   - Find the top 3 highest paid employees
   - Find departments which have more than 5 employees
   - Find second highest salary in each department

3. **Customer Order Analysis**
   - Orders table: `order_id`, `customer_id`, `product_id`, `quantity`, `amount`
   - Find all customers who have ordered all the products that customer 1 ordered

4. **Database Insertion Optimization**
   - File with 1000s of records
   - Insert only rows not present in SQL database

## Data Structures & Algorithms

### Array Problems

1. **Sort Array with 0s, 1s, and 2s**
   - Sort an array containing only 0s, 1s, and 2s
   - **Algorithm**: Dutch National Flag Algorithm

2. **Three Sum Problem**
   - Given array: `int[] num = {1,7,11,4}` and `target = 16`
   - Find three numbers that sum to the target value
   - **Variation**: Given unsorted integer array and target, return true if sum of any 3 numbers equals target
   - Input: `arr = {3, 7, 4, 12, 8}`, `target = 19`
   - **Follow-up**: Write brute force first, then optimize to O(n²), then solve using HashMap

3. **Second Smallest Element**
   - Given array: `[1,1,2,3,4,5]`
   - Find second smallest number ignoring duplicates (answer should be 1)

4. **Trapping Rain Water (Snowpack Problem)**
   - Given array of building heights: `[5, 1, 3, 2, 4]`
   - Calculate amount of water/snow trapped between buildings
   - **Variation**: Given array: `{0, 1, 3, 0, 1, 2, 0, 4, 2, 0, 3, 0}` → 13 units can be trapped

5. **Daily Temperatures / Next Greater Element**
   - **Problem**: Given array of temperatures, find how many days to wait for higher temperature
   - **Input**: `{73, 74, 75, 71, 69, 72, 76, 73}`
   - **Output**: `{1, 1, 4, 2, 1, 1, -1, -1}`
   - **Follow-up**: Optimize solution, discuss time and space complexity

6. **Student Marks Maximum Average**
   - Given 2D array: `[["ABC", 80], ["DEF", 90], ["EFG", 70], ["ABC", 100]]`
   - Return maximum average among all students

7. **Maximum Average Calculator**
   - **Problem**: Given array of employees with name and marks, find maximum average marks
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

8. **Common Elements in Matrix Rows**
   - Given m x n matrix, find all common elements present in all rows in O(mn) time
   - Example input:
     ```
     mat[4][5] = {{1, 2, 1, 4, 8},
                  {3, 7, 8, 5, 1},
                  {8, 7, 7, 3, 1},
                  {8, 1, 2, 7, 9}};
     ```
   - Expected output: 1 8 (elements present in all rows)

9. **Subarray Partitioning Problem**
   - Given integer array nums of length n
   - Determine if array can be split into subarrays of length k where:
     - Each subarray contains k distinct integers in ascending order
     - Each integer used exactly as many times as it appears
     - Integers in subarray must be distinct and sorted ascending
   - Example: `[1,1,1,2,2,3,3,3,4,5,6,7,8,9,10]` with k=3
   - Should return true if possible, false otherwise

10. **Count Length of Cycle**
    - **Problem**: Given integer array, starting from `startIndex`, follow each element to index it points to until you find cycle. Return cycle length or -1
    - **Test cases**:
      - `countLengthOfCycle(new int[]{1, 0}, 0) == 2`
      - `countLengthOfCycle(new int[]{1, 2, 0}, 0) == 3`

### Stack & Queue Problems

11. **Reverse Stack**
    - Reverse a stack with or without using additional data structure

### String Problems

12. **Robot Movement Tracker**
    - Robot starts at origin (0,0) on 2D grid
    - Commands: 'u' (up), 'd' (down), 'l' (left), 'r' (right)
    - Input example: "uuuddlrl"
    - Track robot's final position

## Data Structure Design Problems

### Time Series Data Management
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

## Java Multithreading Coding Problems

### Thread Implementation
1. **ExecutorService Implementation**
   - Write code snippet for ExecutorService with 100 thread pool
   - How to create threads

2. **Thread Counter Optimization**
   - Create two threads that increment counter with optimization

3. **Runnable Class Implementation**
   - Create class extending Runnable
   - Execute logic through Executor framework

4. **How to create a thread? Write code to create a thread**

### Algorithm Design Problems

5. **Circuit Breaker Implementation**
   - **Problem**: If `someOtherFn()` fails 10 times consecutively, don't call it for next 10 times, just skip
   ```java
   public Object handle() {
       // Implementation needed
       return someOtherFn();
   }

   private Object someOtherFn() {
       // We don't have control over this function
   }
   ```

6. **File Processing with Multithreading**
   - Process file with millions of transaction records (sorted by time)
   - Design solution using multithreading

## System Design Coding Scenarios

### Load Balancing & Distributed Systems
1. **Trade Version Processing**
   - Handle millions of trades (Trade1_v1, Trade1_v2, etc.) with 3 processors
   - Ensure all versions of same trade processed by same processor
   - Achieve load balancing and fast lookup
   - **Suggested Solutions:**
     - Consistent Hashing
     - Kafka partitioning based on trade ID
     - Redis for persistent trade-to-processor mapping

2. **Video Processing Server Calculation**
   - Calculate exact number of servers needed if:
     - One video takes 30 seconds to process
     - All videos should be processed within 60 seconds
     - Daily load: 1 million video uploads

### Multi-function Coordination
**Scenario**: 3 functions where:
- f1 makes HTTP call
- f2 makes async call  
- f3 merges response of both
**Questions**: How to coordinate? Threading considerations?

## Spring Boot Practical Implementation

### Security & Authentication
1. **Tell me the process for S3 connection in Spring Boot**

2. **How do you design a Prometheus metric in code?**

3. **How to compensate transactions in Saga with coding example?**

## Complex Problem Scenarios

### Project-Specific Coding Challenges
- Tell me about the most complex issue you faced in your previous project
- Explain your project and how you optimized large number of queries
- Any challenging task you worked on in your previous project?
- How did you handle 2-way sync in your project?