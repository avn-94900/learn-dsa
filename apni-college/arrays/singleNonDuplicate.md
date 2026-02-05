Ah! You are talking about the **“Single Element in a Sorted Array”** problem (LeetCode 540). But note: **binary search only works efficiently if the array is sorted**, not fully unsorted.

Here’s how you can approach it with **binary search** in a **sorted array** where every element appears twice except one:

---

# 📘 Problem

* Input: Sorted array `nums` where every element appears **twice** except **one element**.
* Output: The single element.

Example:

```
nums = [1,1,2,3,3,4,4,8,8]
Output: 2
```

---

# 🔎 Binary Search Idea

* Pairs appear in the array as `(even_index, odd_index)`.
* **Before** the single element: first of pair at **even index**, second at **odd index**.
* **After** the single element: first of pair at **odd index**, second at **even index**.
* Use this pattern to **narrow down** the search.

---

# 💻 Java Code

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0, high = nums.length - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;

            // Ensure mid is even
            if (mid % 2 == 1) mid--;

            // Check if pair is correct
            if (nums[mid] == nums[mid + 1]) {
                // Single element is after this pair
                low = mid + 2;
            } else {
                // Single element is before or at mid
                high = mid;
            }
        }

        return nums[low]; // low == high points to single element
    }
}
```

---

# 🔎 Dry Run Example

Input: `[1,1,2,3,3,4,4,8,8]`

* low=0, high=8
* mid=4 → even → nums[4]=3, nums[5]=4 → not equal → high=4
* mid=2 → even → nums[2]=2, nums[3]=3 → not equal → high=2
* mid=0 → even → nums[0]=1, nums[1]=1 → equal → low=2
* low=high=2 → stop

✅ Single element = `2`

---

⚠️ **Important**:

* If the array is **unsorted**, binary search **cannot** be used reliably. You would need a **linear scan or XOR trick**:

```java
int single = 0;
for (int num : nums) single ^= num;
```

This works in **O(n)** and finds the single number even in an unsorted array.

---

I can provide a **visual diagram of the binary search steps** to make it easier to understand the pattern of pairs and single element.

Do you want me to do that?
