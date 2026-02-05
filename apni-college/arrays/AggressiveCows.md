

---

## 🔹 Problem Statement

* You have `N` stalls at different positions (`arr[i]`).
* You need to place `C` cows in these stalls.
* The cows must be placed such that the **minimum distance between any two cows is as large as possible**.

👉 Return that **largest minimum distance**.

---

## 🔹 Key Idea

* Sort the stall positions.
* Answer lies between:

  * **low = 1** (minimum possible distance)
  * **high = max(stalls) - min(stalls)` (maximum possible distance)
* Use **binary search** to maximize `minDist`.
* At each step, check feasibility:

  * Can we place all cows with at least `mid` distance apart?

---

## 🔹 Java Code

```java
import java.util.*;

public class AggressiveCows {

    // Check if we can place cows with at least minDist between them
    public static boolean canPlace(int[] stalls, int n, int cows, int minDist) {
        int count = 1;  // first cow in first stall
        int lastPos = stalls[0];

        for (int i = 1; i < n; i++) {
            if (stalls[i] - lastPos >= minDist) {
                count++;
                lastPos = stalls[i];
                if (count == cows) return true;
            }
        }
        return false;
    }

    public static int largestMinDistance(int[] stalls, int n, int cows) {
        Arrays.sort(stalls);

        int low = 1;
        int high = stalls[n - 1] - stalls[0];
        int result = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (canPlace(stalls, n, cows, mid)) {
                result = mid;    // feasible → try for larger minDist
                low = mid + 1;
            } else {
                high = mid - 1;  // not feasible → reduce minDist
            }
        }
        return result;
    }

    // Driver
    public static void main(String[] args) {
        int[] stalls1 = {1, 2, 8, 4, 9};
        int cows1 = 3;
        System.out.println("Largest minimum distance: " + largestMinDistance(stalls1, stalls1.length, cows1));
        // Expected: 3 (Cows at positions 1, 4, 8 or 1, 4, 9)

        int[] stalls2 = {10, 1, 2, 7, 5};
        int cows2 = 3;
        System.out.println("Largest minimum distance: " + largestMinDistance(stalls2, stalls2.length, cows2));
        // Expected: 4 (Cows at positions 1, 5, 10)

        int[] stalls3 = {1, 2, 4, 8, 9};
        int cows3 = 3;
        System.out.println("Largest minimum distance: " + largestMinDistance(stalls3, stalls3.length, cows3));
        // Expected: 3
    }
}
```

---

## 🔹 Sample Output

```
Largest minimum distance: 3
Largest minimum distance: 4
Largest minimum distance: 3
```

---

### ✅ Core Intuition

* We’re maximizing the **minimum gap** between cows.
* Binary search helps us test possible `minDist` values efficiently.

---

Do you want me to also show you a **step-by-step dry run** of the first example (`stalls = {1,2,8,4,9}, cows=3`) to see how binary search converges to `3`?
