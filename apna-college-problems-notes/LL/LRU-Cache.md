Nice — below are compact step-by-step notes followed by a **single Java file** that implements an LRU Cache using a doubly linked list + hashmap. The code is commented heavily and includes a `main` with runnable test cases and a helper to print the cache state.

# Notes — step-by-step approach

1. **Goal**: Support `get(key)` and `put(key,value)` in **O(1)** time, with capacity-based eviction of the *least recently used* item.
2. **Core idea**: combine two data structures:

   * **HashMap** `key -> node` for O(1) lookup.
   * **Doubly linked list** to maintain usage order (most recently used at head, least recently used at tail).
3. **Node layout**: each node stores `key`, `value`, `prev`, `next`. We need `key` in the node so we can remove its entry from the map when evicting.
4. **Dummy head & tail**: use sentinel (dummy) head and tail nodes to simplify insert/delete logic and avoid many null checks.
5. **Operations**:

   * `addNode(node)`: insert node right after dummy `head` (makes it most recently used).
   * `removeNode(node)`: unlink node from the list.
   * `moveToHead(node)`: `removeNode(node)` then `addNode(node)` — used after `get` or updating an existing key.
   * `popTail()`: remove and return the node just before dummy `tail` (the least recently used).
6. **`get(key)`**:

   * If key not in map → return `-1`.
   * Else move that node to head and return its value.
7. **`put(key, value)`**:

   * If key exists: update value, move node to head.
   * Else: create node, add to head, insert into map. If size > capacity → `popTail()` and remove its key from map.
8. **Complexities**:

   * Time: `O(1)` for `get` and `put`.
   * Space: `O(capacity)` for map + nodes.
9. **Edge cases**:

   * Capacity ≤ 0 → throw `IllegalArgumentException` (or choose behavior you prefer).
   * Re-inserting same key should update value and usage order.
10. **Alternative**: Java's built-in `LinkedHashMap` can implement LRU concisely by overriding `removeEldestEntry`, but the below shows the explicit list+map design for learning and fine control.

---

# Single-file Java implementation (detailed comments)

```java
import java.util.HashMap;

/**
 * Single-file LRU Cache implementation using:
 *  - Doubly linked list (for LRU order)
 *  - HashMap<Integer, Node> (for O(1) access to nodes)
 *
 * Usage (example in main): demonstrates put/get and eviction behavior.
 */
public class LRUCache {
    // Node class: doubly linked list node storing key and value
    private static class Node {
        int key;
        int value;
        Node prev;
        Node next;

        Node(int k, int v) {
            this.key = k;
            this.value = v;
        }
    }

    private final int capacity;               // maximum number of items cache can hold
    private final HashMap<Integer, Node> map; // map from key -> node in the linked list
    private final Node head;                  // dummy head (most recently used is head.next)
    private final Node tail;                  // dummy tail (least recently used is tail.prev)

    /**
     * Constructor: initialize LRU cache with positive capacity.
     * @param capacity maximum number of entries
     * @throws IllegalArgumentException if capacity <= 0
     */
    public LRUCache(int capacity) {
        if (capacity <= 0) {
            throw new IllegalArgumentException("Capacity must be > 0");
        }
        this.capacity = capacity;
        this.map = new HashMap<>(capacity * 2);
        // create dummy head and tail to avoid null checks
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head.next = tail;
        tail.prev = head;
    }

    /**
     * Get value for key. If key exists, move node to head (mark most recently used).
     * @param key the key to lookup
     * @return value associated with key, or -1 if not present
     */
    public int get(int key) {
        Node node = map.get(key);
        if (node == null) {
            // not found
            return -1;
        }
        // Move the accessed node to head (most recently used)
        moveToHead(node);
        return node.value;
    }

    /**
     * Put key,value into cache. If key exists, update value and move to head.
     * If key does not exist, insert new node. If capacity exceeded, evict LRU node.
     * @param key the key
     * @param value the value
     */
    public void put(int key, int value) {
        Node existing = map.get(key);
        if (existing != null) {
            // update value + refresh usage order
            existing.value = value;
            moveToHead(existing);
        } else {
            // create new node
            Node newNode = new Node(key, value);
            // insert into map and add to head (most recently used)
            map.put(key, newNode);
            addNode(newNode);

            // if over capacity, remove the least recently used item
            if (map.size() > capacity) {
                Node lru = popTail();           // remove from list
                if (lru != null) {
                    map.remove(lru.key);       // remove from map
                    // (optional) help GC: disconnect lru
                    lru.prev = null;
                    lru.next = null;
                }
            }
        }
    }

    /* ------------------------ Helper linked-list operations ------------------------ */

    /**
     * Add node right after dummy head.
     * Result: node becomes the first real node (most recently used).
     * Time: O(1)
     */
    private void addNode(Node node) {
        // head <-> head.next becomes head <-> node <-> head.next
        node.prev = head;
        node.next = head.next;

        head.next.prev = node;
        head.next = node;
    }

    /**
     * Remove an arbitrary node from the linked list (fix neighbours).
     * Time: O(1)
     */
    private void removeNode(Node node) {
        Node prevNode = node.prev;
        Node nextNode = node.next;
        if (prevNode != null) {
            prevNode.next = nextNode;
        }
        if (nextNode != null) {
            nextNode.prev = prevNode;
        }
        // detach node pointers (optional, makes debugging/GC cleaner)
        node.prev = null;
        node.next = null;
    }

    /**
     * Move an existing node to head (mark most recently used).
     * Time: O(1)
     */
    private void moveToHead(Node node) {
        removeNode(node);
        addNode(node);
    }

    /**
     * Pop (remove and return) the node just before dummy tail: the least recently used node.
     * Time: O(1)
     */
    private Node popTail() {
        Node lru = tail.prev;
        if (lru == head) {
            // list empty (only dummy nodes)
            return null;
        }
        removeNode(lru);
        return lru;
    }

    /* ------------------------ Utility for demonstration / debugging ------------------------ */

    /**
     * Print current cache state from most recent to least recent.
     * Format: head -> [k:v] -> [k:v] -> tail
     */
    public void printCacheState() {
        StringBuilder sb = new StringBuilder();
        sb.append("Cache state (MRU -> LRU): ");
        Node cur = head.next;
        while (cur != null && cur != tail) {
            sb.append("[").append(cur.key).append(":").append(cur.value).append("]");
            cur = cur.next;
            if (cur != tail) sb.append(" -> ");
        }
        System.out.println(sb.toString());
    }

    /* ------------------------ Example tests ------------------------ */

    public static void main(String[] args) {
        System.out.println("LRUCache demo (capacity = 2)");
        LRUCache cache = new LRUCache(2);

        cache.put(1, 1);
        cache.printCacheState(); // expected: [1:1]
        cache.put(2, 2);
        cache.printCacheState(); // expected: [2:2] -> [1:1]

        System.out.println("get(1) -> " + cache.get(1)); // returns 1, moves key 1 to head
        cache.printCacheState(); // expected: [1:1] -> [2:2]

        cache.put(3, 3); // capacity reached, evict LRU (key 2)
        cache.printCacheState(); // expected: [3:3] -> [1:1]

        System.out.println("get(2) -> " + cache.get(2)); // returns -1 (not found)

        cache.put(4, 4); // evict LRU (key 1)
        cache.printCacheState(); // expected: [4:4] -> [3:3]

        System.out.println("get(1) -> " + cache.get(1)); // -1
        System.out.println("get(3) -> " + cache.get(3)); // 3
        System.out.println("get(4) -> " + cache.get(4)); // 4

        cache.printCacheState(); // expected: [4:4] -> [3:3] (after gets, 4 then 3)
    }
}
```

---

If you want, I can:

* Convert this to a **generic** `LRUCache<K,V>` version.
* Provide a **thread-safe** variant (with `synchronized` methods or `ReentrantLock`).
* Or show the **LinkedHashMap** one-liner alternative for production brevity.

Which one would you like next?


<br/><br/><br/><br/><br/><br/><br/><br/><br/>





Got it 👍
I’ll give you a clean **LRU Cache implementation in Java** using **HashMap + Doubly LinkedList**. This way, both `get()` and `put()` run in **O(1)**.

Here’s the code:

```java
import java.util.HashMap;

class LRUCache {

    class Node {
        int key, value;
        Node prev, next;
        Node(int k, int v) {
            key = k;
            value = v;
        }
    }

    private final int capacity;
    private HashMap<Integer, Node> map;
    private Node head, tail; // dummy head and tail

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        
        // Dummy nodes to avoid null checks
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        
        Node node = map.get(key);
        remove(node);
        insertToFront(node);
        return node.value;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            remove(map.get(key)); // remove old node
        }
        if (map.size() == capacity) {
            remove(tail.prev); // remove least recently used
        }
        Node node = new Node(key, value);
        insertToFront(node);
    }

    // --- Helpers ---
    private void remove(Node node) {
        map.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void insertToFront(Node node) {
        map.put(node.key, node);
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }
}
```

---

### ✅ Usage Example:

```java
public class Main {
    public static void main(String[] args) {
        LRUCache cache = new LRUCache(2);

        cache.put(1, 1);
        cache.put(2, 2);
        System.out.println(cache.get(1)); // returns 1
        cache.put(3, 3);                  // evicts key 2
        System.out.println(cache.get(2)); // returns -1 (not found)
        cache.put(4, 4);                  // evicts key 1
        System.out.println(cache.get(1)); // returns -1 (not found)
        System.out.println(cache.get(3)); // returns 3
        System.out.println(cache.get(4)); // returns 4
    }
}
```

---

👉 This is the **classic LeetCode 146 LRU Cache solution**.

Do you want me to also show a **simpler version using `LinkedHashMap`** (less code, but less educational)?
