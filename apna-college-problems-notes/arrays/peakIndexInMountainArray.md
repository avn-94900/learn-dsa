Great question 👍
This refers to **LeetCode 852. Peak Index in a Mountain Array**.
We can solve it using **binary search** because the array is strictly increasing up to the peak and strictly decreasing after the peak.

---

# 📘 Problem

Given a mountain array (strictly increasing then strictly decreasing), find the index of the peak element.

Example:

```
arr = [0, 2, 4, 3, 1]
Peak = 4, index = 2
```

---

# 🔎 Idea (Binary Search)

* In a mountain array:

  * If `arr[mid] < arr[mid+1]`, the peak lies **right side**.
  * If `arr[mid] > arr[mid+1]`, the peak lies **left side (including mid)**.

Keep narrowing the range until `start == end`, which will be the **peak index**.

**Time Complexity**: O(log n)
**Space Complexity**: O(1)

---

# 💻 Java Code

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int start = 0, end = arr.length - 1;

        while (start < end) {
            int mid = start + (end - start) / 2;

            if (arr[mid] < arr[mid + 1]) {
                // Peak is on the right side
                start = mid + 1;
            } else {
                // Peak is on the left side (mid could be peak)
                end = mid;
            }
        }
        // start == end at the peak index
        return start;
    }
}
```
```java
int peakIndexInMountainArray(vector<int>& A) {
    int st = 1, end = A.size() - 2; // peak can't be first or last

    while (st <= end) {
        int mid = st + (end - st) / 2;

        if (A[mid - 1] < A[mid] && A[mid] > A[mid + 1]) {
            return mid; // peak found
        }
        else if (A[mid - 1] < A[mid]) {
            st = mid + 1; // go right
        }
        else {
            end = mid - 1; // go left
        }
    }

    return -1; // shouldn't reach here for valid mountain array
}
```

---

# 🔎 Dry Run Example

Input: `[0, 2, 4, 3, 1]`

* start=0, end=4
  mid=2 → arr[2]=4, arr[3]=3 → arr[mid] > arr[mid+1] → end=2
* start=0, end=2
  mid=1 → arr[1]=2, arr[2]=4 → arr[mid] < arr[mid+1] → start=2
* start=2, end=2 → stop.

Answer: index `2` ✅

---

Would you like me to also extend this to the **“Find Peak Element”** problem (LeetCode #162), where the array is not guaranteed to be a mountain but may have multiple peaks?
