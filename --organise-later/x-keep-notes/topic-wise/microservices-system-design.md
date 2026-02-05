# Microservices & System Design Interview Notes

## HTTP Methods & REST Concepts

| Number | Question |
| ------ | ---------- |
| 1 | What HTTP methods are used in microservices? |
| 2 | What are idempotent HTTP methods? (Definition) |
| 3 | Which of these methods are idempotent: GET, POST, PUT, DELETE? |
| 4 | Difference between PUT and PATCH methods |

## Communication Patterns

| Number | Question |
| ------ | ---------- |
| 1 | In your project, which scenario did you use synchronous communication? |
| 2 | Can we set timeout in synchronous communication? If yes, how? |
| 3 | What is Circuit Breaker? |
| 4 | How and when do we use retry in circuit breaker? |

## Distributed Transaction Patterns

| Number | Question |
| ------ | ---------- |
| 1 | Explain Saga Design Pattern and its types |
| 2 | How do you compensate transactions in Saga with coding example? |

## Scalability & Performance

| Number | Question |
| ------ | ---------- |
| 1 | How to make DB actions and database queries more efficient? |
| 2 | How to make a service scalable or more performance specific? |
| 3 | How to ensure that a service receiving API requests isn't overloaded? |

## System Architecture Design

| Number | Question |
| ------ | ---------- |
| 1 | What is 2-tier architecture? |
| 2 | Design LLD of Notification service & multiple questions around it |
| 3 | What are the components involved in designing a system having only one service and one database? |
| 4 | What AWS services will you use? |

## Browser Tab Management System (Design Problem)

| Number | Scenario |
| ------ | ---------- |
| - | Design a browser tab management system with following scenarios: 1. When closing active tab, switch to previous tab 2. When closing non-active tab, keep current tab active 3. Handle edge case when first tab is active. Suggested Data Structure: LinkedHashSet for maintaining insertion order, Variables: currentActiveTab, index, Methods: openTab(), movement(), removeTab() |

## Load Balancing & Distributed Systems

| Number | Problem |
| ------ | ---------- |
| 1 | Trade Version Processing - Handle millions of trades (Trade1_v1, Trade1_v2, etc.) with 3 processors. Ensure all versions of same trade processed by same processor. Achieve load balancing and fast lookup. Suggested Solutions: Consistent Hashing, Kafka partitioning based on trade ID, Redis for persistent trade-to-processor mapping |
| 2 | Video Processing Server Calculation - Calculate exact number of servers needed if: One video takes 30 seconds to process, All videos should be processed within 60 seconds, Daily load: 1 million video uploads |
| 3 | DDOS Prevention - How to prevent multiple same requests from clogging/breaking system |
| 4 | API Parameter Validation - How to validate parameters being sent on API calls |
| 5 | File Processing with Multithreading - Process file with millions of transaction records (sorted by time). Design solution using multithreading |
| 6 | Database Insertion Optimization - File with 1000s of records. Insert only rows not present in SQL database |

## Algorithm Design

| Number | Problem |
| ------ | ---------- |
| 1 | Circuit Breaker Implementation - If someOtherFn() fails 10 times consecutively, don't call it for next 10 times, just skip. Implementation needed for handle() method |