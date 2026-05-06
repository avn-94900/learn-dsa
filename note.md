
====================================================


Find Mean and Median of Unsorted Array
MedianOfStream 
matrix-all-sln.md
2-sum
3-sum
4-sum

===================================================


import java.util.*;

public class LongestWordFinder {

    public static Set<String> longestWord(String letters, Set<String> dict) {
        Set<String> result = new HashSet<>();

        if (letters == null || dict == null) return result;

        // Step 1: Count frequency of given letters
        int[] letterCount = new int[26];
        for (char c : letters.toCharArray()) {
            letterCount[c - 'a']++;
        }

        int maxLength = 0;

        // Step 2: Check each word
        for (String word : dict) {

            if (canForm(word, letterCount)) {

                if (word.length() > maxLength) {
                    result.clear(); // found longer word
                    result.add(word);
                    maxLength = word.length();
                } else if (word.length() == maxLength) {
                    result.add(word); // same length
                }
            }
        }

        return result;
    }

    // Helper function
    private static boolean canForm(String word, int[] letterCount) {
        int[] temp = new int[26];

        for (char c : word.toCharArray()) {
            temp[c - 'a']++;

            if (temp[c - 'a'] > letterCount[c - 'a']) {
                return false;
            }
        }

        return true;
    }

    // Testing
    public static void main(String[] args) {
        Set<String> dict1 = new HashSet<>(Arrays.asList("to", "toe", "toes"));
        System.out.println(longestWord("oet", dict1)); // [toe]

        Set<String> dict2 = new HashSet<>(Arrays.asList("to", "toe", "toes", "dog", "dogs"));
        System.out.println(longestWord("ogds", dict2)); // [dogs]
    }
}
----------------------------------------------------------------------------------
public class BackspaceStringCompare {

    public static boolean backspaceCompare(String s, String t) {
        int i = s.length() - 1;
        int j = t.length() - 1;

        while (i >= 0 || j >= 0) {

            i = getNextValidCharIndex(s, i);
            j = getNextValidCharIndex(t, j);

            if (i >= 0 && j >= 0) {
                if (s.charAt(i) != t.charAt(j)) {
                    return false;
                }
            } else {
                // One string finished, other didn't
                if (i >= 0 || j >= 0) {
                    return false;
                }
            }

            i--;
            j--;
        }

        return true;
    }

    private static int getNextValidCharIndex(String str, int index) {
        int skip = 0;

        while (index >= 0) {
            if (str.charAt(index) == '#') {
                skip++;
                index--;
            } else if (skip > 0) {
                skip--;
                index--;
            } else {
                break;
            }
        }

        return index;
    }

    public static void main(String[] args) {
        System.out.println(backspaceCompare("ab#c", "ad#c")); // true
        System.out.println(backspaceCompare("ab##", "c#d#")); // true
        System.out.println(backspaceCompare("a#c", "b"));     // false
    }
}

---------
import java.util.*;

public class BackspaceStringCompare {

    // Helper method: processes the string using stack
    public static String processString(String str) {
        Stack<Character> stack = new Stack<>();

        for (char c : str.toCharArray()) {
            if (c == '#') {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                stack.push(c);
            }
        }

        // Build final string using StringBuilder
        StringBuilder sb = new StringBuilder();
        for (char c : stack) {
            sb.append(c);
        }

        return sb.toString();
    }

    // Main method: compares both processed strings
    public static boolean backspaceCompare(String s, String t) {
        return processString(s).equals(processString(t));
    }

    public static void main(String[] args) {
        System.out.println(backspaceCompare("ab#c", "ad#c")); // true
        System.out.println(backspaceCompare("ab##", "c#d#")); // true
        System.out.println(backspaceCompare("a#c", "b"));     // false
    }
}
----------------------------------------------------------------------------










public static boolean hasCycle(int[] arr, int startIndex) {
    Set<Integer> visited = new HashSet<>();
    int current = startIndex;

    while (current >= 0 && current < arr.length) {
        if (visited.contains(current)) {
            return true;
        }
        visited.add(current);
        current = arr[current];
    }

    return false;
}
// Above one for simpler understanding.. if cycle present or not.

import java.util.*;

public class Solution {

    public static int countLengthOfCycle(int[] arr, int startIndex) {
        Map<Integer, Integer> visited = new HashMap<>(); // index -> step
        int steps = 0;
        int current = startIndex;

        while (current >= 0 && current < arr.length) {

            if (visited.containsKey(current)) {
                // cycle detected → just return length
                return steps - visited.get(current);
            }

            visited.put(current, steps);
            steps++;
            current = arr[current];
        }

        return -1; // no cycle
    }

    public static void main(String[] args) {
        System.out.println(countLengthOfCycle(new int[]{1, 0}, 0));   // 2
        System.out.println(countLengthOfCycle(new int[]{1, 2, 0}, 0)); // 3
        System.out.println(countLengthOfCycle(new int[]{2, 3, -1}, 0)); // -1
    }
}

int[] arr = {1, 2, 3, 4, 2};
int startIndex = 0;

| Step | current | visited map       | action      |
| ---- | ------- | ----------------- | ----------- |
| 0    | 0       | {}                | store (0,0) |
| 1    | 1       | {0:0}             | store (1,1) |
| 2    | 2       | {0:0,1:1}         | store (2,2) |
| 3    | 3       | {0:0,1:1,2:2}     | store (3,3) |
| 4    | 4       | {0:0,1:1,2:2,3:3} | store (4,4) |
| 5    | 2       | already visited ✅ | cycle found |
