Ah, I see what you’re trying to do! You want to **flatten a multilevel (child) linked list** where each node may have a `child` pointer pointing to another linked list, and you want a single flattened list. Let me break down your description and structure it properly in a **working function** in Java.

---

### Key idea:

1. Preserve the `next` pointer of the current node before going into the `child`.
2. Recursively flatten the `child` list.
3. Attach the flattened `child` to the current node.
4. Move to the end of the flattened child to attach the preserved `next`.
5. Repeat until the whole list is flattened.

---

### Java Implementation:

```java
class Node {
    int val;
    Node next;
    Node child;

    Node(int val) {
        this.val = val;
        this.next = null;
        this.child = null;
    }
}

public class FlattenList {

    public Node flatten(Node head) {
        if (head == null) return null;

        Node curr = head;

        while (curr != null) {
            if (curr.child != null) {
                Node nextTemp = curr.next;  // preserve the next pointer

                // Flatten the child and attach it to curr.next
                Node childHead = flatten(curr.child);
                curr.next = childHead;

                // Find the tail of the flattened child list
                Node tail = childHead;
                while (tail.next != null) {
                    tail = tail.next;
                }

                // Attach the preserved next
                tail.next = nextTemp;

                // Remove the child pointer
                curr.child = null;
            }
            curr = curr.next;  // move to next node
        }

        return head;
    }

    // Helper function to print list
    public void printList(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.val + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    // Test
    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.child = new Node(3);
        head.next.child.next = new Node(4);
        head.next.next = new Node(5);

        FlattenList fl = new FlattenList();
        Node flatHead = fl.flatten(head);
        fl.printList(flatHead);  // Expected: 1 -> 2 -> 3 -> 4 -> 5 -> null
    }
}
```

---

### How it works:

1. We loop through each node.
2. If a node has a `child`, we **flatten the child** recursively.
3. We attach the flattened child list to `curr.next`.
4. Find the **tail of the child** to reattach the preserved `next`.
5. Nullify `child` pointer.
6. Continue until the end of the list.

---

If you want, I can also give a **fully recursive version** that returns the **tail directly**, which avoids the `while(tail.next!=null)` loop and is slightly faster.

Do you want me to do that?


<br/><br/><br/>


Absolutely! Flattening a **multilevel doubly linked list** is very similar, but now we have to also **update the `prev` pointer** when attaching the child list.

Here’s a clean **recursive Java implementation** for a doubly linked list:

---

### Node definition (doubly linked list)

```java
class Node {
    int val;
    Node next;
    Node prev;
    Node child;

    Node(int val) {
        this.val = val;
        this.next = null;
        this.prev = null;
        this.child = null;
    }
}
```

---

### Flatten function (recursive)

```java
public class FlattenDoublyList {

    // Flatten and return the tail of the list
    public Node flattenRec(Node head) {
        if (head == null) return null;

        Node curr = head;
        Node tail = head;

        while (curr != null) {
            Node nextTemp = curr.next; // preserve next pointer

            // If child exists, flatten it
            if (curr.child != null) {
                Node childTail = flattenRec(curr.child);

                // Insert child between curr and nextTemp
                curr.next = curr.child;
                curr.child.prev = curr; // update prev pointer
                curr.child = null;

                if (nextTemp != null) {
                    childTail.next = nextTemp;
                    nextTemp.prev = childTail; // update prev pointer
                }

                tail = childTail; // update tail
            } else {
                tail = curr;
            }

            curr = nextTemp; // move to preserved next
        }

        return tail; // return tail of flattened list
    }

    // Flatten helper
    public Node flatten(Node head) {
        flattenRec(head);
        return head;
    }

    // Print doubly linked list
    public void printList(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.val + " <-> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    // Test
    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.prev = head;
        head.next.child = new Node(3);
        head.next.child.next = new Node(4);
        head.next.child.next.prev = head.next.child;
        head.next.next = new Node(5);
        head.next.next.prev = head.next;

        FlattenDoublyList fl = new FlattenDoublyList();
        Node flatHead = fl.flatten(head);
        fl.printList(flatHead);  // Expected: 1 <-> 2 <-> 3 <-> 4 <-> 5 <-> null
    }
}
```

---

### Key differences from singly linked list:

1. When attaching the child list:

   ```java
   curr.child.prev = curr;
   ```

   Update the `prev` pointer of the child head.

2. When reattaching the preserved `next`:

   ```java
   nextTemp.prev = childTail;
   ```

   Update the `prev` pointer of the original `next` node.

3. Everything else works recursively exactly like the singly linked list version.

---

