Got it ✅
I’ll make you **clean notes + Java code** for both problems covered in that video:

---

# 📘 Notes

## 1. **Pow(x, n) Problem (LeetCode #50)**

**Goal**: Implement power function $x^n$.

### Approaches

1. **Naive**: Multiply `x` by itself `n` times → **O(n)** → too slow.
2. **Binary Exponentiation (Exponentiation by Squaring)**:

   * Idea: Use binary representation of `n`.
   * Example: $x^{13} = x^{1101_2} = x^{8} \cdot x^{4} \cdot x^{1}$.
   * Algorithm:

     * Start with `res = 1`.
     * While `n > 0`:

       * If `n` is odd → multiply result by `x`.
       * Square `x` (i.e. `x *= x`).
       * Divide `n` by 2 (right shift).
   * Handle negative powers: if `n < 0`, compute `1/x^(-n)`.

**Time Complexity**: $O(\log n)$
**Space Complexity**: $O(1)$

---

## 2. **Best Time to Buy and Sell Stock (LeetCode #121)**

**Goal**: Maximize profit by buying once and selling once.

### Approaches

1. **Naive**: For each day, check all future days for profit → **O(n²)** → too slow.
2. **Optimal**: Single pass.

   * Keep track of:

     * `minPrice` so far (best day to buy).
     * `maxProfit` seen so far.
   * For each price:

     * `profit = price - minPrice`.
     * Update `maxProfit`.
     * Update `minPrice` if current price is lower.

**Time Complexity**: $O(n)$
**Space Complexity**: $O(1)$

---

# 💻 Java Code

### 1. Pow(x, n)

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n; // to handle overflow when n = Integer.MIN_VALUE
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        double result = 1;
        while (N > 0) {
            if ((N & 1) == 1) { // if odd
                result *= x;
            }
            x *= x;   // square the base
            N >>= 1;  // divide n by 2
        }
        return result;
    }
}
```

---

### 2. Best Time to Buy and Sell Stock

```java
import java.util.Arrays;
public class Main{
    public static int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE; // Step 1
        int maxProfit = 0;

        for (int currentPrice : prices) { // Step 2
            // update min price so far
            minPrice = Math.min(minPrice, currentPrice);

            // calculate profit if we sell today
            int currentProfit = currentPrice - minPrice;

            // update max profit so far
            maxProfit = Math.max(maxProfit, currentProfit);
        }
        return maxProfit; // Step 3
    }


    public static int maxProfit_2(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price; // update buying point
            } else {
                maxProfit = Math.max(maxProfit, price - minPrice);
            }
        }
        return maxProfit;
    }



    
    public static void main(String[] args) {
        int[] arr= {7, 1, 5, 3, 6, 4};
        System.out.println(" " + maxProfit(arr));
        System.out.println(" " + maxProfit_2(arr));
    }
}
```

---

👉 Both codes are **LeetCode-ready**.

Do you also want me to include **step-by-step dry runs with example input/output** for each problem, so you can quickly visualize how the logic flows?


Ah, I see — your draft code has a few **syntax mistakes** (`=` instead of `==`, typos like `binFor`, `douhle`, etc.).
Let me **fix and complete** it into a clean, working Java solution using **binary exponentiation** ✅

---

# ✅ Corrected Java Code (Pow(x, n))

```java
class Solution {
    public double myPow(double x, int n) {
        // Base cases
        if (n == 0) return 1.0;
        if (x == 0) return 0.0;
        if (x == 1) return 1.0;
        if (x == -1) return (n % 2 == 0) ? 1.0 : -1.0;

        long exp = n; // use long to handle overflow for n = Integer.MIN_VALUE

        // Handle negative exponent
        if (exp < 0) {
            x = 1 / x;
            exp = -exp;
        }

        double ans = 1.0;

        // Binary exponentiation loop
        while (exp > 0) {
            if ((exp % 2) == 1) {   // if exponent is odd
                ans *= x;
            }
            x *= x;      // square the base
            exp /= 2;    // reduce exponent
        }

        return ans;
    }
}
```

---

# 🔎 Example Dry Run

Input:

```java
x = 2.0, n = 10
```

Steps:

* `exp = 10 (1010₂)`
* Iter 1: exp = 10 (even) → square base → `x = 4`, exp = 5
* Iter 2: exp = 5 (odd) → `ans = 1 * 4 = 4`, `x = 16`, exp = 2
* Iter 3: exp = 2 (even) → `x = 256`, exp = 1
* Iter 4: exp = 1 (odd) → `ans = 4 * 256 = 1024`

Output: **1024.0**

---

👉 Now your skeleton code is fully working.
Do you want me to also **optimize away** those early checks (`x == 0, x == 1, x == -1`) since the binary exponentiation loop already handles them safely?
