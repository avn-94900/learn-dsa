# Interview Questions & Coding Problems - Organized Notes

## 📚 THEORY QUESTIONS

### Java Core Concepts

#### Q1: Java Pass by Value vs Pass by Reference
**Question**: What happens when you pass primitive vs object references to methods in Java?

**Example Code**:
```java
public class Ss {
    int a = 10;
    
    void call(int a) {
        a = a + 10;  // This won't affect the instance variable
    }
    
    public static void main(String args[]) {
        Ss s = new Ss();
        System.out.println("Before" + s.a); // Before10
        s.call(50510);
        System.out.println("After" + s.a);  // After10 (unchanged)
    }
}
```

#### Q2: Java Object Reference Passing
**Question**: How does Java handle object references when passed to methods?

**Example Code**:
```java
public class Ss {
    int a = 10;
    
    void call(Ss eg) {
        eg.a = eg.a + 10;  // This modifies the original object
    }
    
    public static void main(String args[]) {
        Ss s = new Ss();
        System.out.println("Before" + s.a); // Before10
        s.call(s);
        System.out.println("After" + s.a);  // After20 (changed)
    }
}
```

#### Q3: Java Exception Handling - Catch Block Order
**Question**: What's wrong with this exception handling code?

**Problem Code**:
```java
public class Ss {
    public static void main(String args[]) {
        try {
            System.out.println(5/10);
        } catch(Exception e) {
            System.out.print("d");
        } catch (ArithmeticException r) {  // Compilation error - unreachable
            System.out.print("aa");
        }
    }
}
```
**Issue**: More specific exceptions must be caught before general Exception class.

---

## 💻 CODING PROBLEMS

### String Manipulation

#### Problem 1: Remove Duplicate Characters
**Search Terms**: "remove duplicate characters keep first occurrence", "replace duplicates with asterisk"

**Problem**: Given a string of lowercase characters, replace each duplicate character with '*', keeping only the first occurrence.

**Example**:
- Input: `"ababcababce"`
- Output: `"ab*c*e"`

---

#### Problem 1: Remove Duplicate Characters
**Search Terms**: "remove duplicate characters keep first occurrence", "replace duplicates with asterisk"

**Problem**: Given a string of lowercase characters, replace each duplicate character with '*', keeping only the first occurrence.

**Example**:
- Input: `"ababcababce"`
- Output: `"ab*c*e"`


### Problem Statement (in simple words)

You are given two strings `str1` and `str2`.
Both strings can contain:

* **Lowercase letters** (`a–z`)
* The **special character `#`**

Here, the character `#` means **backspace** → it deletes the character immediately before it.

Your task:
 After applying all the backspaces (`#`) to both strings, check whether the final processed versions of the two strings are **equal or not**.



### Example 1

```
str1 = "ab#c"
str2 = "ad#c"
```

Process:

* `"ab#c"` → `b` is removed → `"ac"`
* `"ad#c"` → `d` is removed → `"ac"`

 Both final strings = `"ac"` → Answer: **true**



### Example 2

```
str1 = "ab##"
str2 = "c#d#"
```

Process:

* `"ab##"` → `b` removed, then `a` removed → `""` (empty string)
* `"c#d#"` → `c` removed, then `d` removed → `""` (empty string)

 Both final strings = `""` → Answer: **true**

---

### Array Problems

#### Problem 3: Squares of Sorted Array
**Search Terms**: "squares of sorted array", "sorted array squares linear time", "two pointer sorted squares"

**Problem**: Given a sorted array with negative and positive integers, return sorted array of their squares in O(n) time.

**Example**:
- Input: `[-3, -2, -1, 1, 2, 4, 6]`
- Output: `[1, 1, 4, 9, 16, 36]`

**O(n log n) Solution**:
```java
public int[] getSquares(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        arr[i] = arr[i] * arr[i];
    }
    Arrays.sort(arr);
    return arr;
}
```
**Note**: Interviewer wanted O(n) solution using two pointers.

---

#### Problem 4: Three Sum
**Search Terms**: "3sum leetcode", "three sum zero", "triplets sum zero"

**Problem**: Find all unique triplets in array that sum to zero.

**Example**:
- Input: `nums = [-1,0,1,2,-1,-4]`
- Output: `[[-1,-1,2],[-1,0,1]]`

**Constraints**: 
- i ≠ j ≠ k
- nums[i] + nums[j] + nums[k] = 0
- No duplicate triplets

---

#### Problem 5: Trapping Rain Water
**Search Terms**: "trapping rain water", "water trapped between walls", "rain water harvesting algorithm"

**Problem**: Calculate amount of water trapped between walls of different heights.

**Example**:
- Input: `[1, 4, 0, 3, 4, 5, 2, 1, 9]`
- Output: `13`

**Approach**: 
- Calculate left max and right max for each position
- Water at position = min(leftMax, rightMax) - height[i]
- Time: O(n), Space: O(n)

---

#### Problem 6: Max Consecutive Ones III
**Search Terms**: "max consecutive ones with flips", "sliding window binary array", "flip zeros to ones maximum length"

**Problem**: Find maximum length of contiguous 1s after flipping at most K zeros.

**Example**:
- Input: `a = [1,0,1,0,1,0,0,0,1,1]`, `K = 2`
- Output: `6`

**Approach**: Sliding window technique
- Time: O(n), Space: O(K)

---

### Robot/Simulation Problems

#### Problem 7: Robot Position Tracking
**Search Terms**: "robot movement simulation", "track robot coordinates", "direction commands processing"

**Problem**: Simulate robot movement based on direction commands and return final position.

**Commands**:
- 'U' = up (y+1)
- 'D' = down (y-1) 
- 'L' = left (x-1)
- 'R' = right (x+1)

**Example**:
- Input: `"uuullddrrr"`
- Output: `(1, 2)`

**Solution**:
```python
def find_robot_position(directions):
    x, y = 0, 0
    for char in directions:
        if char == 'U': y += 1
        elif char == 'L': x -= 1
        elif char == 'R': x += 1
        elif char == 'D': y -= 1
    return (x, y)
```

---


## 🔍 QUICK SEARCH REFERENCE

### By Algorithm Pattern:
- **Two Pointers**: Squares of Sorted Array, Three Sum
- **Sliding Window**: Max Consecutive Ones III
- **Hash Map**: Remove Duplicates, Three Sum
- **Stack**: Backspace String Compare
- **Simulation**: Robot Position Tracking
- **Dynamic Programming**: Trapping Rain Water

### By Difficulty Level:
- **Easy**: Robot Position, Remove Duplicates, Backspace String
- **Medium**: Squares of Sorted Array (O(n)), Three Sum, Max Consecutive Ones III
- **Hard**: Trapping Rain Water

### By Company Pattern:
- **Array Manipulation**: Multiple problems
- **String Processing**: 2 problems  
- **Mathematical**: Robot simulation
- **Optimization**: Time complexity improvements (O(n log n) to O(n))