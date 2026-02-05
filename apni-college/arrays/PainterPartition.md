
---

## 🔹 Problem Restatement

* We have `N` boards, each board has length `A[i]`.
* We have `K` painters.
* Each painter paints **contiguous boards only**.
* Painting `1 unit` length takes `1 unit time`.
* Goal: **Minimize the maximum time taken by any painter**.

👉 This is exactly like the **Book Allocation Problem** where:

* **Books = Boards**
* **Pages = Length of boards**
* **Students = Painters**

---

## 🔹 Java Solution

```java
import java.util.*;

public class PainterPartition {

    // Validation function: can we paint with maxAllowedTime limit?
    public static boolean isValid(int[] boards, int n, int k, int maxAllowedTime) {
        int painters = 1;
        int time = 0;

        for (int i = 0; i < n; i++) {
            if (boards[i] > maxAllowedTime) return false; // single board too big

            if (time + boards[i] <= maxAllowedTime) {
                time += boards[i];
            } else {
                painters++;
                time = boards[i];
                if (painters > k) return false;
            }
        }
        return true;
    }

    // Main function
    public static int minTime(int[] boards, int n, int k) {
        if (k > n) return -1; // not enough boards for painters

        int low = Arrays.stream(boards).max().getAsInt(); // longest board
        int high = Arrays.stream(boards).sum();           // total length
        int result = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isValid(boards, n, k, mid)) {
                result = mid;
                high = mid - 1; // try smaller max time
            } else {
                low = mid + 1;  // increase limit
            }
        }
        return result;
    }

    // Driver with test cases
    public static void main(String[] args) {
        int[] boards1 = {10, 20, 30, 40};
        int k1 = 2;
        System.out.println("Minimum time: " + minTime(boards1, boards1.length, k1));
        // Expected: 60 (Painter1: 10+20+30, Painter2: 40)

        int[] boards2 = {5, 10, 30, 20, 15};
        int k2 = 3;
        System.out.println("Minimum time: " + minTime(boards2, boards2.length, k2));
        // Expected: 35 (Painter1: 5+10+20, Painter2: 30, Painter3: 15)

        int[] boards3 = {5, 17, 100, 11};
        int k3 = 4;
        System.out.println("Minimum time: " + minTime(boards3, boards3.length, k3));
        // Expected: 100

        int[] boards4 = {10, 20};
        int k4 = 3;
        System.out.println("Minimum time: " + minTime(boards4, boards4.length, k4));
        // Expected: -1 (more painters than boards)
    }
}
```

---

## ✅ Sample Output

```
Minimum time: 60
Minimum time: 35
Minimum time: 100
Minimum time: -1
```

---

📌 Note:

* This is exactly the same logic as **Book Allocation**.
* If painting speed is not `1 unit per time` (say `T` units per time), just multiply the final answer by `T`.

---

Would you like me to also show how to **modify this code to include painting time per unit (`T`)**?
