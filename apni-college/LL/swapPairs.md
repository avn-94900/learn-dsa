You want to **swap nodes in a linked list in pairs**. This is essentially a special case of "reverse in k-groups" with `k = 2`.

---

### Problem Explanation:

Given a linked list, swap every two adjacent nodes.

* You **cannot just swap values**; you must actually swap nodes.

Example:

```
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 2 -> 1 -> 4 -> 3 -> 5
```

---

### Approach:

1. **Recursive approach**:

   * Swap the first two nodes.
   * Call the function recursively for the rest of the list.
   * Connect the swapped pair with the result of recursion.

2. **Iterative approach**:

   * Traverse the list in pairs.
   * Swap nodes using pointer manipulation.
   * Keep track of the previous node to connect.

---

### Java Code (Recursive)

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {

    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;

        ListNode first = head;
        ListNode second = head.next;

        // Swap
        first.next = swapPairs(second.next);
        second.next = first;

        // Second becomes the new head
        return second;
    }

    // Helper function to print list
    public void printList(ListNode head) {
        while (head != null) {
            System.out.print(head.val + " -> ");
            head = head.next;
        }
        System.out.println("NULL");
    }

    public static void main(String[] args) {
        Solution sol = new Solution();

        // Example: 1->2->3->4->5
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        ListNode newHead = sol.swapPairs(head);
        sol.printList(newHead);
    }
}
```

---

✅ **Time Complexity:** O(n) — Each node is visited once.
✅ **Space Complexity:** O(n/2) — Recursion stack.

---
