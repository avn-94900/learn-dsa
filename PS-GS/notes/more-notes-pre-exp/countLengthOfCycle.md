

## 🔹 Problem Restatement

We are given an **integer array** `arr`. Each element in the array represents the **next index** to jump to.

* Start from `arr[startIndex]`.
* Keep jumping to the index specified by the current element.
* If you **find a cycle** (i.e., revisit an index already seen in this path), return the **length of the cycle**.
* If there is **no cycle** (jumps lead outside valid indices), return `-1`.

👉 Essentially:
This is like following pointers in a **linked list with random jumps**. We want to detect whether it loops back, and if yes, find **cycle length**.

---

## 🔹 Example Input & Outputs

### Pattern 1: Simple 2-cycle

```java
arr = [1, 0], startIndex = 0
```

Steps:

* Start at `index 0 → arr[0] = 1`
* Go to `index 1 → arr[1] = 0`
* Back to `index 0` → cycle formed

Cycle = `{0 → 1 → 0}` → length = **2**

✅ Output: `2`

---

### Pattern 2: Full cycle of 3

```java
arr = [1, 2, 0], startIndex = 0
```

Steps:

* Start at `index 0 → arr[0] = 1`
* Go to `index 1 → arr[1] = 2`
* Go to `index 2 → arr[2] = 0`
* Back to `index 0` → cycle formed

Cycle = `{0 → 1 → 2 → 0}` → length = **3**

✅ Output: `3`

---

### Pattern 3: No cycle (jumps out of bounds)

```java
arr = [2, 3, -1], startIndex = 0
```

Steps:

* Start at `index 0 → arr[0] = 2`
* Go to `index 2 → arr[2] = -1`
* `-1` is **invalid index** → no cycle

✅ Output: `-1`

---

## 🔹 How to Detect a Cycle?

We need to track visited indices:

* Use a **HashMap or HashSet**.
* When we visit an index for the **second time**, we found a cycle.
* To find the cycle length: difference between first visit position and current step.

---

## 🔹 Code Implementation

```java
import java.util.*;

public class Solution {

    public static int countLengthOfCycle(int[] arr, int startIndex) {
        Map<Integer, Integer> visited = new HashMap<>(); // index -> step number
        int steps = 0;
        int current = startIndex;

        while (current >= 0 && current < arr.length) {
            if (visited.containsKey(current)) {
                int cycleLength = steps - visited.get(current);

                // 🔹 Print the cycle elements
                System.out.print("Cycle found: ");
                int cycleStart = current;
                int temp = cycleStart;
                do {
                    System.out.print(temp + " ");
                    temp = arr[temp]; // move to next index in cycle
                } while (temp != cycleStart);
                System.out.println();

                return cycleLength;
            }
            visited.put(current, steps);
            steps++;
            current = arr[current]; // jump to next index
        }

        return -1; // no cycle
    }

    public static void main(String[] args) {
        System.out.println(countLengthOfCycle(new int[]{1, 0}, 0));   // Output: 2, cycle: 0 1
        System.out.println(countLengthOfCycle(new int[]{1, 2, 0}, 0)); // Output: 3, cycle: 0 1 2
        System.out.println(countLengthOfCycle(new int[]{2, 3, -1}, 0)); // Output: -1 (no cycle)
    }
}
```

---
Perfect 👍 Let’s do a **step-by-step dry run in table format** for both test cases you mentioned.
I’ll show the variables at each step:

* `current` → the index we are currently on
* `arr[current]` → where the jump goes
* `visited` → map of index → step count
* `steps` → number of moves so far
* **Checkpoints**: cycle found? out of bounds? continue?

---

## ✅ Dry Run 1: `countLengthOfCycle(new int[]{1, 2, 0}, 0)`

| Step | `current` | `arr[current]` | `visited` (index=step) | `steps` | Condition Check    | Action Taken       |
| ---- | --------- | -------------- | ---------------------- | ------- | ------------------ | ------------------ |
| 0    | 0         | 1              | {}                     | 0       | Not visited, valid | Put `0=0` in map   |
| 1    | 1         | 2              | {0=0}                  | 1       | Not visited, valid | Put `1=1` in map   |
| 2    | 2         | 0              | {0=0, 1=1}             | 2       | Not visited, valid | Put `2=2` in map   |
| 3    | 0         | 1              | {0=0, 1=1, 2=2}        | 3       | Already visited    | **Cycle detected** |

➡ Cycle length = `steps - visited.get(0)` = `3 - 0 = 3`
➡ Printed cycle = `0 → 1 → 2 → 0`

✅ Output:

```
Cycle found: 0 1 2 
3
```

---

## ✅ Dry Run 2: `countLengthOfCycle(new int[]{2, 3, -1}, 0)`

| Step | `current` | `arr[current]` | `visited` (index=step) | `steps` | Condition Check    | Action Taken        |
| ---- | --------- | -------------- | ---------------------- | ------- | ------------------ | ------------------- |
| 0    | 0         | 2              | {}                     | 0       | Not visited, valid | Put `0=0` in map    |
| 1    | 2         | -1             | {0=0}                  | 1       | Not visited, valid | Put `2=1` in map    |
| 2    | -1        | (invalid)      | {0=0, 2=1}             | 2       | Out of bounds      | **Stop → no cycle** |

➡ No cycle found → return `-1`

✅ Output:

```
-1
```

---

📌 So the **checkpoints** in both runs are:

1. Is `current` within valid range? If not → return -1.
2. Is `current` already in `visited`? If yes → cycle found → return cycle length.
3. Otherwise, mark it visited with current step, then jump to next index.

---

