# Java - DSA: AVL Trees

This document summarizes **AVL Tree (Self-Balancing BST) concepts and implementations in Java** with formatted code and notes for easy understanding.

---

## 1. AVL Tree Node Structure

```java
public class AVLTree {
    static class Node {
        int data, height;
        Node left, right;

        Node(int data) {
            this.data = data;
            this.height = 1; // New node has height 1
            this.left = null;
            this.right = null;
        }
    }
}
```

---

## 2. Utility Functions

### Get Height
```java
public static int height(Node root) {
    if (root == null) {
        return 0;
    }
    return root.height;
}
```

### Get Balance Factor
```java
public static int getBalance(Node root) {
    if (root == null) {
        return 0;
    }
    return height(root.left) - height(root.right);
}
```

### Update Height
```java
public static void updateHeight(Node root) {
    if (root != null) {
        root.height = 1 + Math.max(height(root.left), height(root.right));
    }
}
```

---

## 3. Rotations

### Right Rotate
```java
public static Node rightRotate(Node y) {
    Node x = y.left;
    Node T2 = x.right;
    
    // Perform rotation
    x.right = y;
    y.left = T2;
    
    // Update heights
    updateHeight(y);
    updateHeight(x);
    
    return x; // New root
}
```

### Left Rotate
```java
public static Node leftRotate(Node x) {
    Node y = x.right;
    Node T2 = y.left;
    
    // Perform rotation
    y.left = x;
    x.right = T2;
    
    // Update heights
    updateHeight(x);
    updateHeight(y);
    
    return y; // New root
}
```

---

## 4. AVL Tree Insert

```java
public static Node insert(Node root, int key) {
    // Step 1: Normal BST insertion
    if (root == null) {
        return new Node(key);
    }
    
    if (key < root.data) {
        root.left = insert(root.left, key);
    } else if (key > root.data) {
        root.right = insert(root.right, key);
    } else {
        return root; // Duplicate keys not allowed
    }
    
    // Step 2: Update height of current node
    updateHeight(root);
    
    // Step 3: Get balance factor
    int balance = getBalance(root);
    
    // Step 4: If unbalanced, perform rotations
    // Left Left Case
    if (balance > 1 && key < root.left.data) {
        return rightRotate(root);
    }
    
    // Right Right Case
    if (balance < -1 && key > root.right.data) {
        return leftRotate(root);
    }
    
    // Left Right Case
    if (balance > 1 && key > root.left.data) {
        root.left = leftRotate(root.left);
        return rightRotate(root);
    }
    
    // Right Left Case
    if (balance < -1 && key < root.right.data) {
        root.right = rightRotate(root.right);
        return leftRotate(root);
    }
    
    return root; // Return unchanged root
}
```

---

## 5. AVL Tree Delete

```java
public static Node delete(Node root, int key) {
    // Step 1: Standard BST delete
    if (root == null) {
        return root;
    }
    
    if (key < root.data) {
        root.left = delete(root.left, key);
    } else if (key > root.data) {
        root.right = delete(root.right, key);
    } else {
        // Node to be deleted found
        // Case 1: Node with only right child or no child
        if (root.left == null) {
            return root.right;
        }
        // Case 2: Node with only left child
        else if (root.right == null) {
            return root.left;
        }
        
        // Case 3: Node with two children
        Node temp = minValueNode(root.right);
        root.data = temp.data;
        root.right = delete(root.right, temp.data);
    }
    
    // Step 2: Update height of current node
    updateHeight(root);
    
    // Step 3: Get balance factor
    int balance = getBalance(root);
    
    // Step 4: If unbalanced, perform rotations
    // Left Left Case
    if (balance > 1 && getBalance(root.left) >= 0) {
        return rightRotate(root);
    }
    
    // Left Right Case
    if (balance > 1 && getBalance(root.left) < 0) {
        root.left = leftRotate(root.left);
        return rightRotate(root);
    }
    
    // Right Right Case
    if (balance < -1 && getBalance(root.right) <= 0) {
        return leftRotate(root);
    }
    
    // Right Left Case
    if (balance < -1 && getBalance(root.right) > 0) {
        root.right = rightRotate(root.right);
        return leftRotate(root);
    }
    
    return root;
}

public static Node minValueNode(Node node) {
    Node current = node;
    while (current.left != null) {
        current = current.left;
    }
    return current;
}
```

---

## 6. Tree Traversals in AVL Tree

**Note**: All traversal methods are **same as Binary Tree**:
- **Preorder Traversal**: Same as Binary Tree
- **Inorder Traversal**: Same as Binary Tree *(gives sorted sequence)*
- **Postorder Traversal**: Same as Binary Tree  
- **Level Order Traversal**: Same as Binary Tree

---

## 7. Search in AVL Tree

**Note**: Search operation is **same as BST** since AVL tree maintains BST property:

```java
// Same as BST search - O(log N) guaranteed due to balanced nature
public static boolean search(Node root, int key) {
    // Same implementation as BST
    if (root == null) return false;
    if (root.data == key) return true;
    if (key < root.data) return search(root.left, key);
    return search(root.right, key);
}
```

---

## 8. AVL Tree Properties & Validation

### Check if Tree is AVL
```java
public static boolean isAVL(Node root) {
    if (root == null) {
        return true;
    }
    
    // Check if current node violates AVL property
    int balance = getBalance(root);
    if (Math.abs(balance) > 1) {
        return false;
    }
    
    // Check recursively for left and right subtrees
    return isAVL(root.left) && isAVL(root.right);
}
```

### Check if Heights are Correct
```java
public static boolean checkHeights(Node root) {
    if (root == null) {
        return true;
    }
    
    int leftHeight = height(root.left);
    int rightHeight = height(root.right);
    int expectedHeight = 1 + Math.max(leftHeight, rightHeight);
    
    if (root.height != expectedHeight) {
        return false;
    }
    
    return checkHeights(root.left) && checkHeights(root.right);
}
```

---

## 9. Count of Nodes, Sum, Other Utilities

**Note**: All utility methods are **same as Binary Tree**:
- **Count of Nodes**: Same as Binary Tree implementation
- **Sum of Nodes**: Same as Binary Tree implementation
- **Print in Range**: Same as BST implementation
- **Root to Leaf Paths**: Same as BST implementation

---

## 10. AVL Tree Rotations Explained

### Rotation Cases:
```java
/**
 * Four Rotation Cases:
 * 
 * 1. Left Left Case (LL): Right Rotate
 *    Balance > 1 && key < root.left.data
 * 
 * 2. Right Right Case (RR): Left Rotate  
 *    Balance < -1 && key > root.right.data
 * 
 * 3. Left Right Case (LR): Left Rotate then Right Rotate
 *    Balance > 1 && key > root.left.data
 * 
 * 4. Right Left Case (RL): Right Rotate then Left Rotate
 *    Balance < -1 && key < root.right.data
 */
```

### Visual Representation:
```java
/**
 * Right Rotation (LL Case):
 *     y                x
 *    / \              / \
 *   x   T3    =>    T1   y
 *  / \                  / \
 * T1  T2              T2  T3
 * 
 * Left Rotation (RR Case):
 *   x                  y
 *  / \                / \
 * T1  y      =>      x   T3
 *    / \            / \
 *   T2 T3          T1  T2
 */
```

---

## 11. Complete AVL Tree Implementation

```java
public class AVLTreeComplete {
    static class Node {
        int data, height;
        Node left, right;
        Node(int data) {
            this.data = data;
            this.height = 1;
        }
    }
    
    public static void main(String[] args) {
        Node root = null;
        int[] values = {10, 20, 30, 40, 50, 25};
        
        System.out.println("Inserting values...");
        for (int val : values) {
            root = insert(root, val);
            System.out.println("Inserted " + val);
            System.out.print("Inorder: ");
            inorder(root);
            System.out.println();
        }
        
        System.out.println("Final AVL Tree:");
        preorder(root);
    }
    
    // Include all methods defined above
}
```

---

## 12. AVL Tree Advantages & Applications

### Advantages:
```java
/**
 * 1. Guaranteed O(log N) operations (search, insert, delete)
 * 2. Self-balancing - no manual intervention needed
 * 3. Better worst-case performance than regular BST
 * 4. Maintains sorted order (inorder gives sorted sequence)
 */
```

### Applications:
```java
/**
 * 1. Database indexing
 * 2. Memory management in operating systems
 * 3. Applications requiring frequent searches
 * 4. Maintaining sorted data with frequent insertions/deletions
 */
```

---

## ✅ Summary

* **AVL Property**: Height difference between left and right subtrees ≤ 1
* **Rotations**: Four types - LL, RR, LR, RL for maintaining balance
* **Insert**: Standard BST insert + height update + balance check + rotations
* **Delete**: Standard BST delete + height update + balance check + rotations  
* **Search**: Same as BST - O(log N) guaranteed due to balanced nature
* **Height Storage**: Each node stores its height for efficient balance calculation
* **Self-Balancing**: Automatic rebalancing after each insert/delete operation
* **Traversals**: Same as Binary Tree (inorder gives sorted sequence)

---

### Time Complexities:
- **Search**: O(log N) - **Guaranteed**
- **Insert**: O(log N) - **Guaranteed**
- **Delete**: O(log N) - **Guaranteed**
- **Space**: O(N) for storing heights

### Key Difference from BST:
- **BST**: Can become skewed (O(N) worst case)
- **AVL**: Always balanced (O(log N) guaranteed)

---

### Balance Factor Formula:
```java
Balance Factor = height(left subtree) - height(right subtree)
Valid range: -1, 0, 1
If |Balance Factor| > 1, rotation required
```