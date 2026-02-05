

## 🔹 Approach

1. Use two pointers: `left` (start of string) and `right` (end of string).
2. Skip non-alphanumeric characters using `Character.isLetterOrDigit()`.
3. Compare characters case-insensitively using `Character.toLowerCase()`.
4. If mismatch → return `false`.
5. If pointers cross → return `true`.

---

## ✅ Java Code

```java
public class ValidPalindrome {

    public static boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            // skip non-alphanumeric chars
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            // compare case-insensitively
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }
        return true;
    }

    // Test cases
    public static void main(String[] args) {
        String s1 = "A man, a plan, a canal: Panama";
        System.out.println(isPalindrome(s1));  // true

        String s2 = "race a car";
        System.out.println(isPalindrome(s2));  // false

        String s3 = " ";
        System.out.println(isPalindrome(s3));  // true (empty after cleaning)

        String s4 = "No 'x' in Nixon";
        System.out.println(isPalindrome(s4));  // true
    }
}
```

---

## 🔹 Sample Output

```
true
false
true
true
```

---

