Got it 👍 Let me give you **notes + Java code** for the **Product of Array Except Self** problem (Leetcode 238).

---

## 📘 Notes

### Problem Statement

* Given an integer array `nums` of length `n`.
* Return an array `ans` where `ans[i]` = product of all elements of `nums` except `nums[i]`.
* **Constraint**: Must run in O(n) time without using division.

---

### Approaches

#### 1. **Brute Force (O(n²))**

* For every index `i`, iterate over all other indices `j ≠ i`.
* Multiply all numbers except `nums[i]`.
* Time: O(n²), Space: O(1).
* Not efficient for large arrays.

---

#### 2. **Prefix and Suffix Product (O(n) time, O(n) space)**

* Precompute **prefix[i]** = product of all elements to the left of `i`.
* Precompute **suffix[i]** = product of all elements to the right of `i`.
* Final answer: `ans[i] = prefix[i] * suffix[i]`.
* Time: O(n), Space: O(n).

---

#### 3. **Optimized (O(n) time, O(1) space extra)**

* Use `ans` array to store prefix products in the first pass.
* Maintain a running `suffixProduct` in the second pass (right to left).
* Multiply `ans[i]` with `suffixProduct` to get final result.
* Time: O(n), Space: O(1) (ignoring output).

---

## ✅ Java Code

### Brute Force

```java
class Solution {
    public int[] productExceptSelfBrute(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];

        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = 0; j < n; j++) {
                if (i != j) {
                    product *= nums[j];
                }
            }
            ans[i] = product;
        }
        return ans;
    }
}
```

---

### Prefix + Suffix (O(n) space)

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        int[] prefix = new int[n];
        int[] suffix = new int[n];

        prefix[0] = 1;
        for (int i = 1; i < n; i++) {
            prefix[i] = prefix[i - 1] * nums[i - 1];
        }

        suffix[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--) {
            suffix[i] = suffix[i + 1] * nums[i + 1];
        }

        for (int i = 0; i < n; i++) {
            ans[i] = prefix[i] * suffix[i];
        }

        return ans;
    }
}
```

---

### Optimized O(1) Space

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];

        // Step 1: Store prefix products
        ans[0] = 1;
        for (int i = 1; i < n; i++) {
            ans[i] = ans[i - 1] * nums[i - 1];
        }

        // Step 2: Multiply with suffix products
        int suffixProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            ans[i] = ans[i] * suffixProduct;
            suffixProduct *= nums[i];
        }

        return ans;
    }
}
```

---

### Example

Input:
`nums = [1, 2, 3, 4]`

Output:
`[24, 12, 8, 6]`

---

Do you want me to also **draw a dry-run step table** (prefix, suffix, result) for better visualization?
