# Queue Implementations in Java

This document summarizes different ways to implement a **Queue** in Java, along with formatted code and notes.

---

## 1. Queue Using Array (Simple)

```java
public class QueueB {
   static class Queue {
       static int arr[];
       static int size;
       static int rear;

       Queue(int size) {
           this.size = size;
           arr = new int[size];
           rear = -1;
       }

       public static boolean isEmpty() {
           return rear == -1;
       }

       public static boolean isFull() {
           return rear == size - 1;
       }

       public static void add(int data) {
           if (isFull()) {
               System.out.println("Overflow");
               return;
           }
           arr[++rear] = data;
       }

       // O(n) remove due to shifting
       public static int remove() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           int front = arr[0];
           for (int i = 1; i <= rear; i++) {
               arr[i - 1] = arr[i];
           }
           rear--;
           return front;
       }

       public static int peek() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           return arr[0];
       }
   }

   public static void main(String[] args) {
       Queue q = new Queue(5);
       q.add(1);
       q.add(2);
       q.add(3);
       System.out.println(q.remove());
       System.out.println(q.peek());
   }
}
```

**Notes:**

* Simple but inefficient → `remove()` requires shifting.
* Time: `add() → O(1)`, `remove() → O(n)`.

---

## 2. Circular Queue Using Array

```java
public class QueueB {
   static class Queue {
       static int arr[];
       static int size;
       static int front = -1;
       static int rear = -1;

       Queue(int size) {
           this.size = size;
           arr = new int[size];
       }

       public static boolean isEmpty() {
           return rear == -1 && front == -1;
       }

       public static boolean isFull() {
           return (rear + 1) % size == front;
       }

       public static void add(int data) {
           if (isFull()) {
               System.out.println("Overflow");
               return;
           }
           if (front == -1) front = 0;
           rear = (rear + 1) % size;
           arr[rear] = data;
       }

       public static int remove() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           int res = arr[front];
           if (front == rear) {
               front = rear = -1;
           } else {
               front = (front + 1) % size;
           }
           return res;
       }

       public static int peek() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           return arr[front];
       }
   }

   public static void main(String[] args) {
       Queue q = new Queue(5);
       q.add(1);
       q.add(2);
       q.add(3);
       q.add(4);
       q.add(5);
       System.out.println(q.remove());
       q.add(6);
       System.out.println(q.remove());
       q.add(7);

       while (!q.isEmpty()) {
           System.out.println(q.remove());
       }
   }
}
```

**Notes:**

* Efficient (`O(1)` add/remove).
* Uses modulo (`%`) to wrap around.

---

## 3. Queue Using Linked List

```java
public class QueueB {
   static class Node {
       int data;
       Node next;
       Node(int data) {
           this.data = data;
           next = null;
       }
   }

   static class Queue {
       static Node head = null;
       static Node tail = null;

       public static boolean isEmpty() {
           return head == null && tail == null;
       }

       public static void add(int data) {
           Node newNode = new Node(data);
           if (isEmpty()) {
               tail = head = newNode;
           } else {
               tail.next = newNode;
               tail = newNode;
           }
       }

       public static int remove() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           int front = head.data;
           if (head == tail) {
               tail = null;
           }
           head = head.next;
           return front;
       }

       public static int peek() {
           if (isEmpty()) {
               System.out.println("Empty queue");
               return -1;
           }
           return head.data;
       }
   }

   public static void main(String[] args) {
       Queue q = new Queue();
       q.add(1);
       q.add(2);
       q.add(3);
       q.add(4);
       q.add(5);

       while (!q.isEmpty()) {
           System.out.println(q.peek());
           q.remove();
       }
   }
}
```

**Notes:**

* Dynamic size, no overflow (except memory).
* `add()` and `remove()` → `O(1)`.

---

## 4. Queue Using Java Collection Framework

```java
import java.util.*;

public class QueueB {
   public static void main(String[] args) {
       Queue<Integer> q = new ArrayDeque<>(); // or new LinkedList<>()
       q.add(1);
       q.add(2);
       q.add(3);
       q.add(4);
       q.add(5);

       while (!q.isEmpty()) {
           System.out.println(q.peek());
           q.remove();
       }
   }
}
```

**Notes:**

* `ArrayDeque` is preferred (faster than `LinkedList`).
* `PriorityQueue` is also available for priority-based ordering.

---

## 5. Queue Using Two Stacks

```java
import java.util.*;

public class QueueB {
   static class Queue {
       static Stack<Integer> s1 = new Stack<>();
       static Stack<Integer> s2 = new Stack<>();

       public static boolean isEmpty() {
           return s1.isEmpty();
       }

       public static void add(int data) {
           while (!s1.isEmpty()) {
               s2.push(s1.pop());
           }
           s1.push(data);
           while (!s2.isEmpty()) {
               s1.push(s2.pop());
           }
       }

       public static int remove() {
           return s1.pop();
       }

       public static int peek() {
           return s1.peek();
       }
   }

   public static void main(String[] args) {
       Queue q = new Queue();
       q.add(1);
       q.add(2);
       q.add(3);

       while (!q.isEmpty()) {
           System.out.println(q.peek());
           q.remove();
       }
   }
}
```

**Notes:**

* Interview question favorite.
* Inefficient compared to arrays/linked list.
* Demonstrates use of stacks to simulate a queue.

---

## 🔎 Comparison Table

| Implementation         | Space Complexity | `add()` | `remove()` | Dynamic Size |
| ---------------------- | ---------------- | ------- | ---------- | ------------ |
| Array (Simple)         | O(n)             | O(1)    | O(n)       | ❌ Fixed      |
| Circular Array         | O(n)             | O(1)    | O(1)       | ❌ Fixed      |
| Linked List            | O(n)             | O(1)    | O(1)       | ✅ Yes        |
| Java Collections (JCF) | O(n)             | O(1)    | O(1)       | ✅ Yes        |
| Two Stacks             | O(n)             | O(n)    | O(1)       | ✅ Yes        |

---

✅ **Summary:**

* Use **Circular Array** for fixed-size efficient queue.
* Use **Linked List / ArrayDeque** for dynamic production-ready queues.
* Learn **Two Stacks** for interviews.
