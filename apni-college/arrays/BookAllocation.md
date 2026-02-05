

### **Problem restatement**

* We have `N` books, each with `A[i]` pages.
* We must allocate **contiguously** to `M` students.
* Each student gets at least one book.
* Goal: minimize the **maximum number of pages** allocated to any student.
* If `M > N`, return `-1`.

---

### **Key idea**

* This is a **search on answer** problem.
* Possible minimum pages = `max(A)` (because at least one student has to take the largest book).
* Possible maximum pages = `sum(A)` (all books assigned to one student).
* Use **binary search** between `[max(A), sum(A)]`.
* Check feasibility with a **greedy validation function**.

---

```java
import java.util.*;

public class BookAllocation {

    // Validation function
    public static boolean isValid(int[] arr, int n, int m, int maxAllowedPages) {
        int students = 1;
        int pages = 0;

        for (int i = 0; i < n; i++) {
            if (arr[i] > maxAllowedPages) return false; // book itself too large

            if (pages + arr[i] <= maxAllowedPages) {
                pages += arr[i];
            } else {
                students++;
                pages = arr[i];
                if (students > m) return false;
            }
        }
        return true;
    }

    // Main function
    public static int allocateBooks(int[] arr, int n, int m) {
        if (m > n) return -1;  // impossible if students > books

        int low = Arrays.stream(arr).max().getAsInt(); // max element
        int high = Arrays.stream(arr).sum();           // sum of all
        int result = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isValid(arr, n, m, mid)) {
                result = mid;      // feasible → try smaller max
                high = mid - 1;
            } else {
                low = mid + 1;     // not feasible → increase limit
            }
        }
        return result;
    }

    // Driver with test cases
    public static void main(String[] args) {
        int[] books1 = {12, 34, 67, 90};
        int m1 = 2;
        System.out.println("Minimum pages: " + allocateBooks(books1, books1.length, m1));
        // Expected: 113

        int[] books2 = {10, 20, 30, 40};
        int m2 = 2;
        System.out.println("Minimum pages: " + allocateBooks(books2, books2.length, m2));
        // Expected: 60 (Student1: 10+20+30, Student2: 40)

        int[] books3 = {5, 17, 100, 11};
        int m3 = 4;
        System.out.println("Minimum pages: " + allocateBooks(books3, books3.length, m3));
        // Expected: 100 (each student one book, max = 100)

        int[] books4 = {5, 10, 30, 20, 15};
        int m4 = 3;
        System.out.println("Minimum pages: " + allocateBooks(books4, books4.length, m4));
        // Expected: 35 (Student1: 5+10+20, Student2: 30, Student3: 15)

        int[] books5 = {10, 20};
        int m5 = 3;
        System.out.println("Minimum pages: " + allocateBooks(books5, books5.length, m5));
        // Expected: -1 (students > books)
    }
}
```


Explanation:

* Student 1 → {12, 34, 67} = 113 pages
* Student 2 → {90} = 90 pages
  Max = 113, minimized.

---

✅ This ensures:

* Contiguous allocation
* Each student gets ≥1 book
* Minimum possible maximum pages

---

