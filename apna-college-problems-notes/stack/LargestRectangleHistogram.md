You’re asking about **finding the largest rectangle in a histogram** in Java. This is a classic problem that can be solved efficiently using a **stack-based approach** in `O(n)` time. Let me give you a clear explanation along with working Java code.

---

### **Problem Statement**

Given an array `heights[]` representing the heights of bars in a histogram, find the area of the **largest rectangle** that can be formed using consecutive bars.

**Example:**

```text
Input: heights = [2, 1, 5, 6, 2, 3]
Output: 10
Explanation: Rectangle formed by heights[2] and heights[3] (5*2=10)
```

---

### **Approach: Stack-Based**

1. Use a stack to keep track of **indices** of bars in **increasing order**.
2. For each bar:

   * While the current bar is **smaller** than the top of the stack:

     * Pop the stack, calculate the area with the popped bar as the **height**.
     * Width = distance between the current index and the new top of the stack minus one.
3. Push the current bar index onto the stack.
4. After traversing, pop remaining bars in the stack and calculate area similarly.

---

### **Java Implementation**

```java
import java.util.Stack;

public class LargestRectangleHistogram {
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;

        for (int i = 0; i <= n; i++) {
            int currentHeight = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && currentHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }

        return maxArea;
    }

    public static void main(String[] args) {
        int[] histogram = {2, 1, 5, 6, 2, 3};
        System.out.println("Largest Rectangle Area: " + largestRectangleArea(histogram));
    }
}
```

---

### **Explanation of the Code**

* **Stack stores indices** of bars in increasing order of heights.
* When we find a smaller bar:

  * Pop the **taller bar**, calculate area using the popped bar as **height**.
  * Width = distance between the current bar and the previous smaller bar.
* We add a **sentinel bar** of height `0` at the end to pop all remaining bars.
* Complexity:

  * **Time:** O(n) → each bar pushed/popped once
  * **Space:** O(n) → stack

---

If you want, I can also give a **recursive divide-and-conquer approach** for this problem in Java, which is another common solution. It’s a bit slower for large inputs but elegant.

Do you want me to show that too?


<br/><br/><br/>
<br/><br/><br/>

Got it ✅
I’ll write the **Java solution** for **Largest Rectangle in Histogram (LeetCode 84)** using the **Nearest Smaller to Left (NSL)** and **Nearest Smaller to Right (NSR)** approach (stack based). I’ll also include **step-by-step notes** explaining the logic.

---

## 📘 Notes (Approach)

1. **Problem**:
   Given an array `heights[]` (bar heights of histogram), find the **maximum rectangular area**.

2. **Brute Force (O(n²))**:

   * For each bar, expand left & right until a smaller bar is found.
   * Too slow for large input.

3. **Optimized (O(n)) using Stacks**:

   * For each bar, we want to know:

     * **Nearest Smaller to Left (NSL)** → first smaller bar on left side.
     * **Nearest Smaller to Right (NSR)** → first smaller bar on right side.
   * If `l = NSL[i]`, `r = NSR[i]`, then:

     ```
     width = r - l - 1
     area = heights[i] * width
     ```
   * Keep track of **max area**.

4. **Why stacks?**

   * While traversing, stack helps to quickly find the previous/next smaller element.
   * Each bar is pushed and popped at most once → O(n).

---

## 💻 Java Code

```java
import java.util.*;

public class LargestRectangleHistogram {

    // Main function to calculate largest rectangle
    public static int largestRectangleArea(int[] heights) {
        int n = heights.length;
        
        // Step 1: Find Nearest Smaller to Left (NSL)
        int[] left = new int[n];
        Stack<Integer> st = new Stack<>();
        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && heights[st.peek()] >= heights[i]) {
                st.pop();
            }
            left[i] = st.isEmpty() ? -1 : st.peek();
            st.push(i);
        }

        // Step 2: Find Nearest Smaller to Right (NSR)
        int[] right = new int[n];
        st.clear();
        for (int i = n - 1; i >= 0; i--) {
            while (!st.isEmpty() && heights[st.peek()] >= heights[i]) {
                st.pop();
            }
            right[i] = st.isEmpty() ? n : st.peek();
            st.push(i);
        }

        // Step 3: Calculate max area
        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            int width = right[i] - left[i] - 1;
            int area = heights[i] * width;
            maxArea = Math.max(maxArea, area);
        }

        return maxArea;
    }

    // Test
    public static void main(String[] args) {
        int[] heights1 = {2, 1, 5, 6, 2, 3};
        int[] heights2 = {2, 4};
        
        System.out.println(largestRectangleArea(heights1)); // Output: 10
        System.out.println(largestRectangleArea(heights2)); // Output: 4
    }
}
```

---

## ✅ Dry Run Example

Input: `[2,1,5,6,2,3]`

* NSL = `[-1, -1, 1, 2, 1, 4]`
* NSR = `[1, 6, 4, 4, 6, 6]`
* Widths = `[1-(-1)-1=1, 6-(-1)-1=6, 4-1-1=2, 4-2-1=1, 6-1-1=4, 6-4-1=1]`
* Areas = `[2*1, 1*6, 5*2, 6*1, 2*4, 3*1] = [2, 6, 10, 6, 8, 3]`
* Max = `10`

---

👉 This is the **stack-based O(n) approach**, exactly as explained in the video.

Do you want me to also give you the **monotonic stack “single pass” version** (slightly cleaner, avoids storing NSL/NSR separately)?
