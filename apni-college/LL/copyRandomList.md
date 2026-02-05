Got it 👍 — I’ll give you the **full runnable Java program** with:

* `main` method
* some **test cases** (with `random` pointers assigned manually)
* a helper method to **print the list** (showing both `val` and `random.val`).

---

## ✅ Full Java Program with `main`

```java
import java.util.HashMap;

class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;

        HashMap<Node, Node> map = new HashMap<>();

        // Step 1: Create newHead
        Node newHead = new Node(head.val);
        map.put(head, newHead);

        Node oldTemp = head.next;
        Node newTemp = newHead;

        // Step 2: Copy next pointers
        while (oldTemp != null) {
            Node copyNode = new Node(oldTemp.val);
            map.put(oldTemp, copyNode);

            newTemp.next = copyNode;
            newTemp = newTemp.next;
            oldTemp = oldTemp.next;
        }

        // Step 3: Copy random pointers
        oldTemp = head;
        newTemp = newHead;
        while (oldTemp != null) {
            if (oldTemp.random != null) {
                newTemp.random = map.get(oldTemp.random);
            }
            oldTemp = oldTemp.next;
            newTemp = newTemp.next;
        }

        return newHead;
    }
}

public class Main {
    // Helper to print list with random pointers
    static void printList(Node head) {
        Node temp = head;
        while (temp != null) {
            int randomVal = (temp.random != null) ? temp.random.val : -1;
            System.out.print("(" + temp.val + ", rand:" + randomVal + ") -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // Example Test Case
        Node n1 = new Node(7);
        Node n2 = new Node(13);
        Node n3 = new Node(11);
        Node n4 = new Node(10);
        Node n5 = new Node(1);

        // Link next pointers
        n1.next = n2;
        n2.next = n3;
        n3.next = n4;
        n4.next = n5;

        // Set random pointers
        n1.random = null;
        n2.random = n1;
        n3.random = n5;
        n4.random = n3;
        n5.random = n1;

        System.out.println("Original list:");
        printList(n1);

        Solution sol = new Solution();
        Node copiedHead = sol.copyRandomList(n1);

        System.out.println("\nCopied list:");
        printList(copiedHead);

        // Another small test
        Node a = new Node(1);
        Node b = new Node(2);
        a.next = b;
        a.random = b;
        b.random = b;

        System.out.println("\nOriginal small list:");
        printList(a);

        Node copiedSmall = sol.copyRandomList(a);
        System.out.println("Copied small list:");
        printList(copiedSmall);
    }
}
```

---

## 📝 Example Output

```
Original list:
(7, rand:-1) -> (13, rand:7) -> (11, rand:1) -> (10, rand:11) -> (1, rand:7) -> null

Copied list:
(7, rand:-1) -> (13, rand:7) -> (11, rand:1) -> (10, rand:11) -> (1, rand:7) -> null

Original small list:
(1, rand:2) -> (2, rand:2) -> null
Copied small list:
(1, rand:2) -> (2, rand:2) -> null
```

---

👉 This verifies that the **copied list is identical in structure**, but completely new (deep copy).

Do you also want me to **add a check that proves the original and copied nodes are different objects** (not just same references)?
