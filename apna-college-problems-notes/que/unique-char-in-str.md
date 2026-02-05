Got it 👍
You want to **find the first unique character in a string** using **Map** (for frequency counting) and **Queue** (to preserve order).

Here’s a **Java implementation with step-by-step comments**:

```java
import java.util.*;

public class FirstUniqueChar {
    public static char firstUniqueChar(String s) {
        // Step 1: Map to store frequency of each character
        Map<Character, Integer> freqMap = new HashMap<>();

        // Step 2: Queue to maintain the order of characters
        Queue<Character> queue = new LinkedList<>();

        // Step 3: Traverse string
        for (char c : s.toCharArray()) {
            // Update frequency
            freqMap.put(c, freqMap.getOrDefault(c, 0) + 1);

            // Add to queue if first occurrence
            if (freqMap.get(c) == 1) {
                queue.offer(c);
            }

            // Remove from queue if character is no longer unique
            while (!queue.isEmpty() && freqMap.get(queue.peek()) > 1) {
                queue.poll();
            }
        }

        // Step 4: Check result
        return queue.isEmpty() ? '_' : queue.peek(); // '_' if no unique char
    }

    public static void main(String[] args) {
        String s1 = "swiss";
        String s2 = "aabbcc";
        String s3 = "leetcode";

        System.out.println("First unique in '" + s1 + "' = " + firstUniqueChar(s1));
        System.out.println("First unique in '" + s2 + "' = " + firstUniqueChar(s2));
        System.out.println("First unique in '" + s3 + "' = " + firstUniqueChar(s3));
    }
}
```

### ✅ Explanation:

* `freqMap` keeps **counts of each character**.
* `queue` stores characters in the order they appear.
* If a char repeats, we **remove it from the front** until the front of the queue is unique again.
* At the end, `queue.peek()` is the **first unique char**.

### 🔹 Output:

```
First unique in 'swiss' = w
First unique in 'aabbcc' = _
First unique in 'leetcode' = l
```

👉 Do you want me to also extend this so it finds **all unique characters**, not just the first one?
