Got it 👍 You’re asking for **LeetCode 134 – Gas Station**. Let’s solve step by step with **notes + Java solution**.

---

## 🔹 Problem Statement

You have `n` gas stations arranged in a circle.

* `gas[i]` = amount of gas at station `i`.
* `cost[i]` = gas needed to travel from station `i` to `(i+1) % n`.

You need to find **the starting gas station index** from where you can travel around the circle once, or return `-1` if not possible.

---

## 🔹 Key Observations

1. If **total gas < total cost**, solution is impossible → return `-1`.
2. If solution exists, there is **exactly one unique starting point**.
3. Greedy Idea:

   * Traverse stations, keep track of `tank = gas[i] - cost[i]`.
   * If `tank` becomes **negative**, we cannot reach the next station → reset start to next station.
   * At the end, if `totalGas >= totalCost`, return `start`.

---

## ✅ Java Solution with Comments

```java
public class GasStation {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0, totalCost = 0;
        int tank = 0;   // current fuel in car
        int start = 0;  // candidate starting station

        for (int i = 0; i < gas.length; i++) {
            totalGas += gas[i];
            totalCost += cost[i];

            tank += gas[i] - cost[i];

            // If tank is negative, cannot start from current segment
            if (tank < 0) {
                start = i + 1; // next station might be candidate
                tank = 0;      // reset tank
            }
        }

        // If overall gas is less than overall cost, no solution
        return totalGas < totalCost ? -1 : start;
    }

    public static void main(String[] args) {
        GasStation sol = new GasStation();
        int[] gas = {1,2,3,4,5};
        int[] cost = {3,4,5,1,2};

        int startIndex = sol.canCompleteCircuit(gas, cost);
        System.out.println("Start Index = " + startIndex);
    }
}
```

---

## 🔎 Dry Run Example

```
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]

totalGas = 15, totalCost = 15 → possible.

Step by step:
- i=0: tank = 1-3 = -2 → reset start=1, tank=0
- i=1: tank = 0+(2-4) = -2 → reset start=2, tank=0
- i=2: tank = 0+(3-5) = -2 → reset start=3, tank=0
- i=3: tank = 0+(4-1) = 3
- i=4: tank = 3+(5-2) = 6

✅ End: start = 3
```

So the answer is **3**.

---

## 📌 Notes / Takeaways

* **Condition 1:** If total gas < total cost → return `-1`.
* **Condition 2:** Otherwise, the last reset point (when tank < 0) + 1 is the solution.
* **Time complexity:** `O(n)` (single pass).
* **Space complexity:** `O(1)` (just variables).

---

Would you like me to also show a **table-style dry run** (like I did for sliding window) to visualize how `tank` and `start` change step by step?
