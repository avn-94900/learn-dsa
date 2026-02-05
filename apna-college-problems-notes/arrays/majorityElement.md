Got it 👍 You’re talking about the **Majority Element problem** –
Find the element that appears more than `⌊n/2⌋` times in the array.

Let’s walk through **3 approaches**:

---

## ✅ Approach 1: Brute Force (O(n²))

Check frequency of each element by looping.

```java
public static int majorityElementBrute(int[] nums) {
    int n = nums.length;

    for (int val : nums) {
        int freq = 0;

        for (int el : nums) {
            if (el == val) {  // should be '==', not '='
                freq++;
            }
        }

        if (freq > n / 2) {
            return val;
        }
    }
    return -1; // no majority
}
```

---

## ✅ Approach 2: Sorting (O(n log n))

* Sort array
* Middle element will be the majority (since majority > n/2)

```java
import java.util.Arrays;

public static int majorityElementSort(int[] nums) {
    Arrays.sort(nums);
    return nums[nums.length / 2];
}
```

---

## ✅ Approach 3: Moore’s Voting Algorithm (O(n), O(1) space)

This is the most **optimized**.

### Idea:

* Maintain `candidate` and `count`
* Traverse array:

  * If `count == 0`, set `candidate = num`
  * If `num == candidate`, increase count
  * Else, decrease count
* At the end, `candidate` is majority element

```java
public static int majorityElementMoore(int[] nums) {
    int candidate = 0, count = 0;

    for (int num : nums) {
        if (count == 0) {
            candidate = num;
            count = 1;
        } else if (num == candidate) {
            count++;
        } else {
            count--;
        }
    }
    return candidate;
}
```

---

### ✅ Example Run

```
nums = [2, 2, 1, 1, 1, 2, 2]
Moore’s algo picks candidate = 2
Output = 2
```

---

⚡ Question for you:
Do you want me to also add **verification step** (checking if the candidate really > n/2) after Moore’s algorithm, or assume input always has a majority element (like in LeetCode)?
