Got it 👍 Let’s solve **LeetCode 503. Next Greater Element II** in **Java**, step by step with explanation, notes, and test cases.

---

## 🔹 Problem Recap

* We are given a **circular array**.
* For each element, find the **Next Greater Element (NGE)** to its right.
* If no greater element exists, return `-1`.
* Since the array is **circular**, after the last element we continue checking from the start.

---

## 🔹 Approach (Monotonic Stack)

1. **Stack usage**:

   * We use a stack to keep track of indices whose next greater element is not yet found.
   * It’s a **decreasing monotonic stack** (top always holds the smallest so far).
2. **Traverse twice** (simulate circular array):

   * We loop through `2 * n` times (`i % n` gives the circular index).
   * This ensures each element gets a chance to look ahead in the circular part.
3. **Filling result**:

   * For each index `i`, while stack top is smaller, pop it and set its NGE as `nums[i % n]`.
   * Push the index into the stack only in the **first pass** (`i < n`).

⏱️ **Time Complexity**: `O(n)`
📦 **Space Complexity**: `O(n)` (stack + result)

---

## 🔹 Java Code

```java
import java.util.*;

public class NextGreaterElementII {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        Arrays.fill(ans, -1);

        Stack<Integer> stack = new Stack<>();

        // Traverse from 2n-1 to 0 (simulate circular array)
        for (int i = 2 * n - 1; i >= 0; i--) {
            int idx = i % n;

            // Pop smaller or equal elements
            while (!stack.isEmpty() && nums[stack.peek()] <= nums[idx]) {
                stack.pop();
            }

            // If stack not empty, top is next greater
            if (!stack.isEmpty()) {
                ans[idx] = nums[stack.peek()];
            }

            // Push current index
            stack.push(idx);
        }

        return ans;
    }

    // Test
    public static void main(String[] args) {
        NextGreaterElementII sol = new NextGreaterElementII();

        int[] nums1 = {1, 2, 1};
        System.out.println(Arrays.toString(sol.nextGreaterElements(nums1)));
        // Expected: [2, -1, 2]

        int[] nums2 = {3, 8, 4, 1, 2};
        System.out.println(Arrays.toString(sol.nextGreaterElements(nums2)));
        // Expected: [8, -1, 8, 2, 3]

        int[] nums3 = {5, 4, 3, 2, 1};
        System.out.println(Arrays.toString(sol.nextGreaterElements(nums3)));
        // Expected: [-1, 5, 5, 5, 5]
    }
}
```

---

## 🔹 Notes / Key Points

* Use **stack of indices**, not values → helps update result array correctly.
* Traverse array **twice** → simulate circular nature.
* Default result is `-1`.
* Each element is pushed & popped at most once → `O(n)`.

---

👉 Do you want me to also give you a **step-by-step dry run example (with stack state)** for better clarity?
