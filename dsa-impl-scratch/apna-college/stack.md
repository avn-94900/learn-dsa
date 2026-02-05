<!-- import java.util.ArrayList;

public class StackAL {
    static class Stack {
        ArrayList<Integer> list = new ArrayList<>();

        public void push(int data) {
            list.add(data);
        }

        public boolean isEmpty() {
            return list.size() == 0;
        }

        public int pop() {
            if(isEmpty()) {
                return -1;
            }
            int top = list.remove(list.size()-1);
            return top;
        }

        public int peek() {
            if(isEmpty()) {
                return -1;
            }
            return list.get(list.size()-1);
        }
    }
    public static void main(String args[]) {
        Stack stack = new Stack();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek());
            stack.pop();
        }
    }
}

import java.util.*;

public class StackJCF {
    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek());
            stack.pop();
        }
    }
}






//stack using Linked List
public class StackDS {
    private static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            next = null;
        }
    }

    static class Stack {
        public static Node head = null;
        public static void push(int data) {
            Node newNode = new Node(data);

            if(head == null) {
                head = newNode;
                return;
            }
            newNode.next = head;
            head = newNode;
        }

        public static boolean isEmpty() {
            return head == null;
        }

        public static int pop() {
            if(isEmpty()) {
                return -1;
            }
            Node top = head;
            head = head.next;
            return top.data;
        }

        public static int peek() {
            if(isEmpty()) {
                return -1;
            }
            Node top = head;
            return top.data;
        }
    }

    public static void main(String args[]) {
        Stack stack = new Stack();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek());
            stack.pop();
        }
    }
}





import java.util.*;
//To push an element at the bottom of a stack
public class StackProblem1 {
    public static void pushAtBottom(Stack<Integer> s, int data) {
        if(s.isEmpty()) {
            s.push(data);
            return;
        }

        int temp = s.pop();
        pushAtBottom(s, data);
        s.push(temp);
    }

    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        pushAtBottom(stack, 4);

        while(!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}



import java.util.*;
//Code to Reverse a Stack

public class StackProblem2 {
    public static void pushAtBottom(Stack<Integer> s, int data) {
        if(s.isEmpty()) {
            s.push(data);
            return;
        }

        int temp = s.pop();
        pushAtBottom(s, data);
        s.push(temp);
    }

    public static void reverse(Stack<Integer> s) {
        if(s.isEmpty()) {
            return;
        }

        int top = s.pop();
        reverse(s);
        pushAtBottom(s, top);
    }

    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);

        while(!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}
 -->


# Java - DSA: Stacks

---

## 1. Stack Using ArrayList

```java
import java.util.ArrayList;

public class StackAL {
    static class Stack {
        ArrayList<Integer> list = new ArrayList<>();

        // Push element on top of stack
        public void push(int data) {
            list.add(data);
        }

        // Check if stack is empty
        public boolean isEmpty() {
            return list.size() == 0;
        }

        // Pop element from top of stack
        public int pop() {
            if(isEmpty()) {
                return -1; // Stack underflow
            }
            int top = list.remove(list.size()-1);
            return top;
        }

        // Peek at the top element
        public int peek() {
            if(isEmpty()) {
                return -1; // Empty stack
            }
            return list.get(list.size()-1);
        }
    }
    
    public static void main(String args[]) {
        Stack stack = new Stack();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek()); // Print top element
            stack.pop();                      // Remove top element
        }
    }
}
```

**Notes:**

* Implements stack using **dynamic ArrayList**.
* Operations: `push`, `pop`, `peek`, `isEmpty`.
* Time Complexity: `O(1)` for all except dynamic resizing.

---

## 2. Stack Using Java Collection Framework (JCF)

```java
import java.util.*;

public class StackJCF {
    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>(); // Built-in stack class
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek()); // View top
            stack.pop();                      // Remove top
        }
    }
}
```

**Notes:**

* Uses `java.util.Stack` from JCF.
* Easy and reliable for most applications.
* Time Complexity: All operations `O(1)`.

---

## 3. Stack Using Linked List

```java
// Stack using Linked List
public class StackDS {
    private static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            next = null;
        }
    }

    static class Stack {
        public static Node head = null;

        // Push: Insert at head
        public static void push(int data) {
            Node newNode = new Node(data);
            if(head == null) {
                head = newNode;
                return;
            }
            newNode.next = head;
            head = newNode;
        }

        // Check if empty
        public static boolean isEmpty() {
            return head == null;
        }

        // Pop: Remove from head
        public static int pop() {
            if(isEmpty()) {
                return -1; // Underflow
            }
            Node top = head;
            head = head.next;
            return top.data;
        }

        // Peek: Return head data
        public static int peek() {
            if(isEmpty()) {
                return -1;
            }
            return head.data;
        }
    }

    public static void main(String args[]) {
        Stack stack = new Stack();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);

        while(!stack.isEmpty()) {
            System.out.println(stack.peek());
            stack.pop();
        }
    }
}
```

**Notes:**

* Stack implemented using **Linked List**.
* No fixed size limit (dynamic memory).
* Time Complexity: Push/Pop/Peek `O(1)`.

---

## 4. Stack Problem 1: Push at Bottom

```java
import java.util.*;

// Push an element at the bottom of a stack
public class StackProblem1 {
    public static void pushAtBottom(Stack<Integer> s, int data) {
        if(s.isEmpty()) {
            s.push(data);
            return;
        }

        int temp = s.pop();
        pushAtBottom(s, data);
        s.push(temp); // Restore order
    }

    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        pushAtBottom(stack, 4);

        while(!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}
```

**Notes:**

* Uses recursion to insert element **at bottom**.
* Time Complexity: `O(n)`.
* Useful in stack manipulation problems.

---

## 5. Stack Problem 2: Reverse a Stack

```java
import java.util.*;

// Reverse a Stack using recursion
public class StackProblem2 {
    public static void pushAtBottom(Stack<Integer> s, int data) {
        if(s.isEmpty()) {
            s.push(data);
            return;
        }

        int temp = s.pop();
        pushAtBottom(s, data);
        s.push(temp);
    }

    public static void reverse(Stack<Integer> s) {
        if(s.isEmpty()) {
            return;
        }

        int top = s.pop();
        reverse(s);
        pushAtBottom(s, top);
    }

    public static void main(String args[]) {
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);

        reverse(stack); // Call reverse before printing

        while(!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}
```

**Notes:**

* Recursively reverses a stack using `pushAtBottom()`.
* Time Complexity: `O(n^2)` in worst case (due to recursion).
* Classic recursion + stack problem.

---

### 🔑 Quick Summary

* **ArrayList** → Simple & dynamic array-based.
* **JCF Stack** → Easiest to use in real projects.
* **Linked List** → No size limit, efficient.
* **Push at Bottom** → Recursion-based stack manipulation.
* **Reverse Stack** → Recursion + `pushAtBottom` trick.
