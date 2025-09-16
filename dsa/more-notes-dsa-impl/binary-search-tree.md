# Java - DSA: Binary Search Trees

This document summarizes **Binary Search Tree (BST) concepts and implementations in Java** with formatted code and notes for easy understanding.

---
I'll create a comprehensive Binary Search Tree (BST) document that complements your existing Binary Tree notes. I'll include the full implementation for BST-specific methods and reference your existing Binary Tree methods where they're the same.I've created a comprehensive Binary Search Tree document that complements your existing Binary Tree notes. Here are the key highlights:

**BST-Specific Methods Included:**
- BST construction using insert operation
- Search functionality with O(H) complexity
- Delete operation with all three cases
- Print nodes in range
- Root to leaf path printing
- BST validation
- Mirror BST creation
- Convert to balanced BST

**Methods Referenced from Binary Tree:**
- All traversal methods (with note that inorder gives sorted sequence in BST)
- Height calculation
- Node counting
- Sum calculation

**Key BST Properties Covered:**
- Inorder traversal gives sorted sequence
- Search/Insert/Delete complexities
- BST validation with min-max bounds
- Balancing techniques

The document maintains consistency with your existing notes' format and includes practical code examples with clear explanations. Each method includes time complexity analysis where relevant.

## 1. BST Node Structure

```java
public class BST {
    static class Node {
        int data;
        Node left, right;

        Node(int data) {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }
}
```

---

## 2. Build BST (Insert Operation)

```java
public static Node insert(Node root, int val) {
    if (root == null) {
        root = new Node(val);
        return root;
    }
    
    if (root.data > val) {
        // Insert in left subtree
        root.left = insert(root.left, val);
    } else {
        // Insert in right subtree
        root.right = insert(root.right, val);
    }
    
    return root;
}
```

### Usage Example:
```java
public static void main(String args[]) {
    int values[] = {5, 1, 3, 4, 2, 7};
    Node root = null;
    
    for (int i = 0; i < values.length; i++) {
        root = insert(root, values[i]);
    }
    
    inorder(root);
    System.out.println();
}
```

---

## 3. Tree Traversals in BST

**Note**: All traversal methods are **same as Binary Tree**:
- **Preorder Traversal**: Same as Binary Tree
- **Postorder Traversal**: Same as Binary Tree  
- **Level Order Traversal**: Same as Binary Tree
- **Inorder Traversal**: Same as Binary Tree *(but gives sorted sequence in BST)*

### Important Property:
```java
// Inorder traversal of BST gives sorted sequence
// For BST: {5, 1, 3, 4, 2, 7} → Inorder: {1, 2, 3, 4, 5, 7}
```

---

## 4. Search in BST

```java
public static boolean search(Node root, int key) {
    if (root == null) {
        return false;
    }
    
    if (root.data > key) {
        return search(root.left, key);
    } else if (root.data == key) {
        return true;
    } else {
        return search(root.right, key);
    }
}
```

**Time Complexity**: O(H) where H is height of tree
- **Best Case**: O(log N) for balanced BST
- **Worst Case**: O(N) for skewed BST

---

## 5. Delete Node in BST

```java
public static Node delete(Node root, int val) {
    if (root.data > val) {
        root.left = delete(root.left, val);
    } else if (root.data < val) {
        root.right = delete(root.right, val);
    } else { // root.data == val
        // Case 1: Leaf node
        if (root.left == null && root.right == null) {
            return null;
        }
        
        // Case 2: One child
        if (root.left == null) {
            return root.right;
        } else if (root.right == null) {
            return root.left;
        }
        
        // Case 3: Two children
        Node IS = inorderSuccessor(root.right);
        root.data = IS.data;
        root.right = delete(root.right, IS.data);
    }
    return root;
}

public static Node inorderSuccessor(Node root) {
    while (root.left != null) {
        root = root.left;
    }
    return root;
}
```

### Delete Cases:
1. **Leaf Node**: Simply remove the node
2. **One Child**: Replace node with its child
3. **Two Children**: Replace with inorder successor (or predecessor)

---

## 6. Print in Range

```java
public static void printInRange(Node root, int X, int Y) {
    if (root == null) {
        return;
    }
    
    if (root.data >= X && root.data <= Y) {
        printInRange(root.left, X, Y);
        System.out.print(root.data + " ");
        printInRange(root.right, X, Y);
    } else if (root.data >= Y) {
        printInRange(root.left, X, Y);
    } else {
        printInRange(root.right, X, Y);
    }
}
```

**Usage**: `printInRange(root, 6, 10)` prints all values between 6 and 10

---

## 7. Root to Leaf Paths

```java
public static void printRoot2Leaf(Node root, ArrayList<Integer> path) {
    if (root == null) {
        return;
    }
    
    path.add(root.data);
    
    // If leaf node
    if (root.left == null && root.right == null) {
        printPath(path);
    } else { // Non-leaf
        printRoot2Leaf(root.left, path);
        printRoot2Leaf(root.right, path);
    }
    
    path.remove(path.size() - 1);
}

public static void printPath(ArrayList<Integer> path) {
    for (int i = 0; i < path.size(); i++) {
        System.out.print(path.get(i) + " -> ");
    }
    System.out.println();
}
```

---

## 8. Validate BST

```java
public static boolean isValidBST(Node root, Node min, Node max) {
    if (root == null) {
        return true;
    }
    
    if (min != null && root.data <= min.data) {
        return false;
    }
    
    if (max != null && root.data >= max.data) {
        return false;
    }
    
    return isValidBST(root.left, min, root) && 
           isValidBST(root.right, root, max);
}

// Initial call
public static boolean isValidBST(Node root) {
    return isValidBST(root, null, null);
}
```

---

## 9. Mirror BST

```java
public static Node createMirror(Node root) {
    if (root == null) {
        return null;
    }
    
    Node leftMirror = createMirror(root.right);
    Node rightMirror = createMirror(root.left);
    
    root.left = leftMirror;
    root.right = rightMirror;
    
    return root;
}
```

---

## 10. Convert BST to Balanced BST

```java
public static void getInorder(Node root, ArrayList<Integer> inorder) {
    if (root == null) {
        return;
    }
    
    getInorder(root.left, inorder);
    inorder.add(root.data);
    getInorder(root.right, inorder);
}

public static Node createBST(ArrayList<Integer> inorder, int st, int end) {
    if (st > end) {
        return null;
    }
    
    int mid = (st + end) / 2;
    Node root = new Node(inorder.get(mid));
    root.left = createBST(inorder, st, mid - 1);
    root.right = createBST(inorder, mid + 1, end);
    
    return root;
}

public static Node balanceBST(Node root) {
    // Get inorder sequence
    ArrayList<Integer> inorder = new ArrayList<>();
    getInorder(root, inorder);
    
    // Create balanced BST from sorted array
    root = createBST(inorder, 0, inorder.size() - 1);
    return root;
}
```

---

## 11. Size, Largest, and Sum (Same as Binary Tree)

- **Count of Nodes**: Same as Binary Tree implementation
- **Sum of Nodes**: Same as Binary Tree implementation  
- **Height of Tree**: Same as Binary Tree implementation

---

## 12. BST Properties & Utilities

### Key Properties:
```java
// 1. Inorder traversal gives sorted sequence
// 2. For every node: left subtree < node < right subtree
// 3. Search, Insert, Delete: O(H) time complexity
// 4. No duplicate values allowed (in standard BST)
```

### Find Min and Max:
```java
public static int findMin(Node root) {
    while (root.left != null) {
        root = root.left;
    }
    return root.data;
}

public static int findMax(Node root) {
    while (root.right != null) {
        root = root.right;
    }
    return root.data;
}
```

---

## ✅ Summary

* **BST Construction**: Insert operation with proper positioning
* **Search**: O(H) time complexity using BST property
* **Delete**: Three cases - leaf, one child, two children  
* **Validation**: Check BST property with min-max bounds
* **Range Operations**: Print nodes in given range
* **Path Operations**: Root to leaf path printing
* **Balancing**: Convert skewed BST to balanced BST
* **Utility Methods**: Same as Binary Tree (height, count, sum)
* **Key Advantage**: Inorder traversal gives sorted sequence

---

### Time Complexities:
- **Search**: O(H) - O(log N) best, O(N) worst
- **Insert**: O(H) - O(log N) best, O(N) worst  
- **Delete**: O(H) - O(log N) best, O(N) worst
- **Inorder**: O(N) - gives sorted sequence

Where H = height of tree, N = number of nodes