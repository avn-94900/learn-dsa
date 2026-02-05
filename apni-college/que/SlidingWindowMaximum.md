Perfect 💡 You want to solve the **Sliding Window Maximum** problem using a **Queue / Deque**.

This is the classic **LeetCode 239: Sliding Window Maximum** problem.

---

## 🔹 Problem

Given an array `nums` and an integer `k`, return the maximum value in every sliding window of size `k`.

---

## ✅ Java Solution (Using Deque)

```java
import java.util.*;

public class SlidingWindowMaximum {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];
        
        int n = nums.length;
        int[] result = new int[n - k + 1];
        int ri = 0;

        // Deque stores indexes, not values
        Deque<Integer> deque = new LinkedList<>();

        for (int i = 0; i < nums.length; i++) {
            // 1. Remove indexes out of current window
            while (!deque.isEmpty() && deque.peekFirst() <= i - k) {
                deque.pollFirst();
            }

            // 2. Remove smaller numbers in k range 
            // (they will never be needed again)
            // que store only viable ans- if non vaialbe you can poll 
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }

            // 3. Add current element's index
            deque.offerLast(i);

            // 4. Add max (front of deque) to result
            if (i >= k - 1) {
                result[ri++] = nums[deque.peekFirst()];
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1,3,-1,-3,5,3,6,7};
        int k = 3;
        int[] res = maxSlidingWindow(nums, k);

        System.out.print("Sliding window maximums: ");
        for (int num : res) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔎 Explanation

We use a **Deque** to maintain indices of useful elements:

1. **Remove out-of-window elements** → if `deque.front <= i-k`.
2. **Remove smaller elements** → from the back because they can't be the max if a larger element is inside the window.
3. **Add new element’s index**.
4. **Front of deque = max of current window**.

---

## 📌 Example Walkthrough

For `nums = [1,3,-1,-3,5,3,6,7]`, `k = 3`:

* Window `[1,3,-1]` → max = `3`
* Window `[3,-1,-3]` → max = `3`
* Window `[-1,-3,5]` → max = `5`
* Window `[-3,5,3]` → max = `5`
* Window `[5,3,6]` → max = `6`
* Window `[3,6,7]` → max = `7`

✅ Output → `[3, 3, 5, 5, 6, 7]`

---

👉 Do you want me to also give you a **step-by-step dry run on paper style** for better understanding?



Absolutely! Let’s **dry run the Sliding Window Maximum algorithm** step by step using a **table format** for clarity.

We’ll use the example:

```
nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3
```

We maintain a **deque of indices** and compute the **window maximum**.

---

| i (index) | nums[i] | Deque (indices) | Deque (values) | Action / Explanation         | Window formed? | Max in window |
| --------- | ------- | --------------- | -------------- | ---------------------------- | -------------- | ------------- |
| 0         | 1       | [0]             | [1]            | Add index 0                  | ❌              | -             |
| 1         | 3       | [1]             | [3]            | Remove 0 (1<3), add 1        | ❌              | -             |
| 2         | -1      | [1,2]           | [3,-1]         | Add index 2                  | ✅              | 3             |
| 3         | -3      | [1,2,3]         | [3,-1,-3]      | Add index 3                  | ✅              | 3             |
| 4         | 5       | [4]             | [5]            | Remove 1,2,3 (all <5), add 4 | ✅              | 5             |
| 5         | 3       | [4,5]           | [5,3]          | Add index 5                  | ✅              | 5             |
| 6         | 6       | [6]             | [6]            | Remove 4,5 (all <6), add 6   | ✅              | 6             |
| 7         | 7       | [7]             | [7]            | Remove 6 (6<7), add 7        | ✅              | 7             |

---

### ✅ How the table works:

* **Deque stores indices**. Front of deque = max of current window.
* **Remove indices** that are **out of window**: `index <= i-k`.
* **Remove smaller numbers** from back; they cannot be max.
* **When i >= k-1**, we have a valid window → take deque.front as max.

---

### Final Output:

```
Sliding window maximums: [3, 3, 5, 5, 6, 7]
```

---

If you want, I can also **draw a visual sliding window diagram with the deque contents for each step**, which is really intuitive for understanding.

Do you want me to do that?
