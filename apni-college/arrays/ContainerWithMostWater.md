Perfect 👍 You’re describing the **Container With Most Water** problem (LeetCode #11).
Let’s carefully break it down with explanation and code.

---

## 🔹 Problem Statement

Given an array `height[]` of size `n`, each index represents the height of a vertical line on the x-axis.
We want to **choose two lines** that, together with the x-axis, form a container that holds the **maximum water**.

### Example

```
height = [1,8,6,2,5,4,8,3,7]

Max water = 49
(choosing lines at index 1 and 8, min(8,7)=7, width=8-1=7 → area=49)
```

---

## 🔹 Two-Pointer Approach (O(n))

### Intuition

* Start with **left = 0** and **right = n-1**
* Container area is:

  ```
  area = min(height[left], height[right]) * (right - left)
  ```
* To maximize area, we need **greater height and width**.
* Move the **shorter line’s pointer** inward:

  * If `height[left] < height[right]` → move `left++`
  * Else → move `right--`
* Keep track of maximum area.

---

## 🔹 Java Code (with indices also)

```java
public class ContainerWithMostWater {
    public static int[] maxArea(int[] height) {
        int left = 0, right = height.length - 1;
        int maxArea = 0;
        int bestLeft = 0, bestRight = 0;

        while (left < right) {
            int minHeight = Math.min(height[left], height[right]);
            int width = right - left;
            int area = minHeight * width;

            if (area > maxArea) {
                maxArea = area;
                bestLeft = left;
                bestRight = right;
            }

            // Move the pointer with smaller height
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        System.out.println("Max Area = " + maxArea +
                           " formed between indices: " + bestLeft + " and " + bestRight);
        return new int[]{maxArea, bestLeft, bestRight};
    }

    public static void main(String[] args) {
        int[] height = {1,8,6,2,5,4,8,3,7};
        int[] result = maxArea(height);
    }
}
```

---

## 🔹 Output

```
Max Area = 49 formed between indices: 1 and 8
```

---

✅ This prints not only the maximum water capacity but also the **indices of the lines** forming that container.

Do you also want me to extend this to return **all possible pairs that achieve the max area** (in case of multiple containers with same capacity)?
