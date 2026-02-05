Good one 👍 This is **LeetCode 567: Permutation in String**.
This is a **sliding window + frequency counting** problem.

---

## 🔹 Problem Restatement

* Given `s1` and `s2`.
* Check if **any permutation of s1** is a substring of `s2`.

👉 That means, does `s2` contain a substring with the **same character frequency** as `s1`?

---

## 🔹 Approach

1. Count frequency of each character in `s1`.
2. Use a **sliding window** of size `s1.length()` over `s2`.
3. Maintain frequency count of the current window in `s2`.
4. If at any point, the two frequency arrays match → return `true`.
5. If window ends without match → return `false`.

---

## ✅ Java Code

```java
import java.util.*;

public class PermutationInString {

    public static boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) return false;

        int[] count1 = new int[26];  // frequency of s1
        int[] count2 = new int[26];  // frequency of current window in s2

        // fill frequency for s1
        for (char c : s1.toCharArray()) {
            count1[c - 'a']++;
        }

        int window = s1.length();

        for (int i = 0; i < s2.length(); i++) {
            // add current char to window
            count2[s2.charAt(i) - 'a']++;

            // remove leftmost char if window > s1.length()
            if (i >= window) {
                count2[s2.charAt(i - window) - 'a']--;
            }

            // compare arrays
            if (Arrays.equals(count1, count2)) {
                return true;
            }
        }

        return false;
    }

    // Test cases
    public static void main(String[] args) {
        String s1 = "ab", s2 = "eidbaooo";
        System.out.println(checkInclusion(s1, s2));  // true ("ba")

        String s3 = "ab", s4 = "eidboaoo";
        System.out.println(checkInclusion(s3, s4));  // false

        String s5 = "adc", s6 = "dcda";
        System.out.println(checkInclusion(s5, s6));  // true ("cda" or "dca")

        String s7 = "hello", s8 = "ooolleoooleh";
        System.out.println(checkInclusion(s7, s8));  // false
    }
}
```

---

## 🔹 Sample Output

```
true
false
true
false
```

---

### ✅ Complexity

* **Time:** O(n) where n = length of `s2` (each char processed once).
* **Space:** O(1) (only 26 letters).

---

Do you want me to also show you an **optimized version using a single count difference variable (instead of full array comparison)** so that we avoid `Arrays.equals()` each time?
