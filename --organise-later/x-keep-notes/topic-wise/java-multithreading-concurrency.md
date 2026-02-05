# Java Multithreading & Concurrency

### Concurrency and Parallelism

| Number | Question |
| ------ | ---------- |
| 1 | Difference between Concurrency vs Parallelism |
| 2 | What are the benefits of `volatile` keyword? |
| 3 | What is the *Happen-Before* relationship, and which concurrency concepts provide it? |

### Thread Basics

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

### Synchronization and Locks

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

### Advanced Threading Concepts

| Number | Question |
| ------ | ---------- |
| 1 | What is Compare-And-Swap (CAS) method, and where is it used? |
| 2 | Which concepts provide atomic operation features? |
| 3 | Which concepts provide visibility of values between threads? |
| 4 | What are the benefits of `AtomicReference` / `AtomicInteger` compared to synchronization? |

### Thread Pools and Executors

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

### Callable, Future, and CompletableFuture

| Number | Question |
| ------ | ---------- |
| 1 | What is the difference between Callable and Runnable? |
| 2 | What is a Future object? Where will you use it? Benefits & drawbacks? |
| 3 | What is CompletableFuture? |
| 4 | Difference between Future and CompletableFuture |
| 5 | Advantages of CompletableFuture |
| 6 | Write a code snippet for the methods of CompletableFuture |

### Synchronization Challenges

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

### Exception Handling in Multithreading

| Number | Question |
| ------ | ---------- |
| 1 | How do you handle exception when one process in multithreading failed? |

### Miscellaneous Multithreading

| Number | Question |
| ------ | ---------- |
| 1 | How to create a custom Immutable Object? Why is it important in multithreading? |
| 2 | What is the `Unsafe` class? Where is it used, and how is it useful? |
| 3 | Can async programs run on main thread or separate thread? |
| 4 | How can you make async calls? |
| 5 | Does `CompletableFuture` work on main thread or not? |
| 6 | What is `ForkJoinCommonPool`? |