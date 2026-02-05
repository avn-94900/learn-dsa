# Trie Data Structure - Comprehensive Notes

## Overview
A Trie (also called Prefix Tree) is a tree-like data structure used to store strings efficiently. It's particularly useful for operations like autocomplete, spell checkers, and IP routing tables.

## Key Characteristics
- **Root Node**: Empty node that serves as the starting point
- **Path to Node**: Represents a prefix of stored strings
- **End of Word (EOW)**: Boolean flag indicating complete word endpoints
- **Time Complexity**: O(n) for insert and search operations, where n is the length of the word
- **Space Efficient**: Common prefixes are shared among words

## Basic Implementation

### Node Structure
```java
static class Node {
    Node[] children = new Node[26];  // Array for 26 lowercase letters (a-z)
    boolean eow;                     // End of word flag

    public Node() {
        for (int i = 0; i < 26; i++) {
            children[i] = null;      // Initialize all children as null
        }
    }
}
```

**Comments:**
- `children[26]` assumes only lowercase English letters
- Index mapping: 'a' → 0, 'b' → 1, ..., 'z' → 25
- `eow` flag distinguishes between intermediate nodes and word endings

### Root Declaration
```java
public static Node root = new Node();
```

**Comments:**
- Static root ensures single trie instance
- Root node is always empty and serves as entry point

## Core Operations

### 1. Insert Operation
```java
public static void insert(String word) { // Time: O(n), Space: O(n)
    Node curr = root;
    for (int level = 0; level < word.length(); level++) {
        int idx = word.charAt(level) - 'a';    // Convert char to array index
        if (curr.children[idx] == null) {
            curr.children[idx] = new Node();   // Create new node if path doesn't exist
        }
        curr = curr.children[idx];             // Move to next level
    }
    curr.eow = true;                           // Mark end of word
}
```

**Comments:**
- Creates path if it doesn't exist
- Reuses existing nodes for common prefixes
- Always marks the final node as end of word

### 2. Search Operation
```java
public static boolean search(String key) { // Time: O(n), Space: O(1)
    Node curr = root;
    for (int level = 0; level < key.length(); level++) {
        int idx = key.charAt(level) - 'a';
        if (curr.children[idx] == null) {
            return false;                      // Path doesn't exist
        }
        curr = curr.children[idx];
    }
    return curr.eow;                           // Check if it's a complete word
}
```

**Comments:**
- Returns false if any character in the path is missing
- Must check `eow` flag to ensure it's a complete word, not just a prefix
- Example: If "the" and "there" are stored, searching "the" should return true

### 3. Demo Usage
```java
public static void main(String args[]) {
    String words[] = {"the", "a", "there", "their", "any", "thee"};
    
    // Insert all words
    for (String word : words) {
        insert(word);
        System.out.println("inserted " + word);
    }

    // Search examples
    System.out.println("thee -> " + search("thee")); // true
    System.out.println("thor -> " + search("thor")); // false
    
    // Prefix search examples
    System.out.println(startsWith("the")); // true
    System.out.println(startsWith("thi")); // false
}
```

## Advanced Problems & Solutions

### Problem 1: Word Break
**Problem**: Given a string and a dictionary of words, determine if the string can be segmented into space-separated dictionary words.

```java
public static boolean wordBreak(String key) {
    int len = key.length();

    if (len == 0) {
        return true;    // Base case: empty string can always be segmented
    }

    for (int i = 1; i <= len; i++) {
        if (search(key.substring(0, i)) &&           // First part is a valid word
            wordBreak(key.substring(i))) {           // Remaining part can be segmented
            return true;
        }
    }

    return false;       // No valid segmentation found
}
```

**Comments:**
- Uses recursive approach with backtracking
- Tries all possible splits of the string
- Time Complexity: O(n³) due to substring operations
- Can be optimized using dynamic programming

### Problem 2: Prefix Search (StartsWith)
**Problem**: Check if any word in the trie starts with given prefix.

```java
public static boolean startsWith(String prefix) {
    Node curr = root;
    
    for (int i = 0; i < prefix.length(); i++) {
        int idx = prefix.charAt(i) - 'a';
        if (curr.children[idx] == null) {
            return false;           // Prefix path doesn't exist
        }
        curr = curr.children[idx];
    }
    return true;                   // Complete prefix path exists
}
```

**Comments:**
- Unlike search, doesn't need to check `eow` flag
- Returns true if prefix path exists, regardless of word completion
- Useful for autocomplete features
- Time Complexity: O(m) where m is prefix length

### Problem 3: Longest Word with All Prefixes
**Problem**: Find the longest word where all its prefixes are also valid words in the trie.

```java
public static String ans = "";    // Global variable to store result

public static void longestWord(Node root, StringBuilder curr) {
    for (int i = 0; i < 26; i++) {
        // Only traverse if child exists and represents a complete word
        if (root.children[i] != null && root.children[i].eow == true) {
            curr.append((char)(i + 'a'));      // Add current character
            
            if (curr.length() > ans.length()) {
                ans = curr.toString();          // Update longest word
            }
            
            longestWord(root.children[i], curr); // Recursive call
            curr.deleteCharAt(curr.length() - 1); // Backtrack
        }
    }
}

// Usage: Call longestWord(root, new StringBuilder()) after inserting words
```


**Comments:**
- Uses DFS with backtracking
- Only explores paths where each node represents a complete word
- StringBuilder used for efficient string manipulation
- Backtracking ensures StringBuilder is restored after each recursive call

### Problem 4: Count Unique Substrings
**Problem**: Count the number of unique substrings in a given string using suffix trie.

```java
public static void buildTrie(String str) {
    // Insert all suffixes to Trie
    root = new Node();
    for (int i = 0; i < str.length(); i++) {
        insert(str.substring(i));    // Insert suffix starting at index i
    }
}

public static int countNodes(Node root) {
    if (root == null) {
        return 0;
    }

    int count = 0;
    for (int i = 0; i < 26; i++) {
        if (root.children[i] != null) {
            count += countNodes(root.children[i]);  // Count child subtrees
        }
    }
    return 1 + count;   // +1 for current node
}
```

**Comments:**
- **Suffix Trie**: Contains all suffixes of the original string
- Each node in the trie represents a unique substring
- Number of unique substrings = Total nodes - 1 (excluding root)
- Space Complexity: O(n²) in worst case
- Alternative approach: Use rolling hash for better space efficiency

## Time & Space Complexity Summary

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Insert | O(n) | O(n) |
| Search | O(n) | O(1) |
| StartsWith | O(m) | O(1) |
| Word Break | O(n³) | O(n) |
| Longest Word | O(ALPHABET_SIZE × n) | O(n) |
| Count Substrings | O(n²) | O(n²) |

Where:
- n = length of word/string
- m = length of prefix
- ALPHABET_SIZE = 26 for lowercase English letters

## Use Cases
- **Autocomplete Systems**: Fast prefix matching
- **Spell Checkers**: Dictionary lookups and suggestions  
- **IP Routing**: Longest prefix matching in routers
- **Text Processing**: Pattern matching and string algorithms
- **Word Games**: Boggle, Scrabble word validation