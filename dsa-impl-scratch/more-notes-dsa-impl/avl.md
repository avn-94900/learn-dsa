Got it 👍
You want the same style:

* **AVL Tree implementation in Java** (self-balancing BST).
* **One function per responsibility** (no wrapper/helper duplication).
* **Recursive implementation**.
* **Notes after the code** (easy for interview prep).

Here’s the clean implementation:

---

```java
class Node {
    int key, height;
    Node left, right;

    Node(int key) {
        this.key = key;
        this.height = 1; // new node is initially at height 1
    }
}

public class AVLTree {
    Node root;

    // ---------------- HEIGHT ----------------
    public int height(Node node) {
        return (node == null) ? 0 : node.height;
    }

    // ---------------- BALANCE FACTOR ----------------
    public int getBalance(Node node) {
        return (node == null) ? 0 : height(node.left) - height(node.right);
    }

    // ---------------- ROTATIONS ----------------
    private Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = 1 + Math.max(height(y.left), height(y.right));
        x.height = 1 + Math.max(height(x.left), height(x.right));

        return x; // new root
    }

    private Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = 1 + Math.max(height(x.left), height(x.right));
        y.height = 1 + Math.max(height(y.left), height(y.right));

        return y; // new root
    }

    // ---------------- INSERT ----------------
    public Node insert(Node node, int key) {
        // Normal BST insert
        if (node == null) return new Node(key);

        if (key < node.key) node.left = insert(node.left, key);
        else if (key > node.key) node.right = insert(node.right, key);
        else return node; // duplicate keys not allowed

        // Update height
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // Get balance factor
        int balance = getBalance(node);

        // Balance the tree
        // Left Left
        if (balance > 1 && key < node.left.key) return rightRotate(node);

        // Right Right
        if (balance < -1 && key > node.right.key) return leftRotate(node);

        // Left Right
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    // ---------------- MIN VALUE NODE ----------------
    public Node minNode(Node node) {
        if (node.left == null) return node;
        return minNode(node.left);
    }

    // ---------------- DELETE ----------------
    public Node delete(Node root, int key) {
        // Normal BST delete
        if (root == null) return root;

        if (key < root.key) root.left = delete(root.left, key);
        else if (key > root.key) root.right = delete(root.right, key);
        else {
            // Node with one child or no child
            if (root.left == null) return root.right;
            else if (root.right == null) return root.left;

            // Node with two children → inorder successor
            Node temp = minNode(root.right);
            root.key = temp.key;
            root.right = delete(root.right, temp.key);
        }

        // Update height
        root.height = 1 + Math.max(height(root.left), height(root.right));

        // Balance
        int balance = getBalance(root);

        // Left Left
        if (balance > 1 && getBalance(root.left) >= 0) return rightRotate(root);

        // Left Right
        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        // Right Right
        if (balance < -1 && getBalance(root.right) <= 0) return leftRotate(root);

        // Right Left
        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    // ---------------- SEARCH ----------------
    public boolean search(Node node, int key) {
        if (node == null) return false;
        if (node.key == key) return true;
        return key < node.key ? search(node.left, key) : search(node.right, key);
    }

    // ---------------- TRAVERSALS ----------------
    public void inorder(Node node) {
        if (node != null) {
            inorder(node.left);
            System.out.print(node.key + " ");
            inorder(node.right);
        }
    }

    public void preorder(Node node) {
        if (node != null) {
            System.out.print(node.key + " ");
            preorder(node.left);
            preorder(node.right);
        }
    }

    public void postorder(Node node) {
        if (node != null) {
            postorder(node.left);
            postorder(node.right);
            System.out.print(node.key + " ");
        }
    }

    // ---------------- DEMO ----------------
    public static void main(String[] args) {
        AVLTree avl = new AVLTree();

        int[] keys = {10, 20, 30, 40, 50, 25};
        for (int k : keys) avl.root = avl.insert(avl.root, k);

        System.out.print("Inorder: ");
        avl.inorder(avl.root); System.out.println();

        System.out.print("Preorder: ");
        avl.preorder(avl.root); System.out.println();

        System.out.print("Postorder: ");
        avl.postorder(avl.root); System.out.println();

        System.out.println("Search 25: " + avl.search(avl.root, 25));
        System.out.println("Search 60: " + avl.search(avl.root, 60));

        avl.root = avl.delete(avl.root, 40);
        System.out.print("After Deletion (Inorder): ");
        avl.inorder(avl.root);
    }
}
```

---

## 📝 Notes for AVL Tree

### 1. **Why AVL Tree?**

* BST can become skewed → O(n) worst-case.
* AVL Tree keeps height balanced (difference ≤ 1).
* Guarantees **O(log n)** search, insert, delete.

---

### 2. **Balance Factor**

$$
BF(node) = height(left) - height(right)
$$

* Must be in {-1, 0, 1}.
* If outside, we rebalance using rotations.

---

### 3. **Rotations**

* **LL Case** → Right Rotate.
* **RR Case** → Left Rotate.
* **LR Case** → Left Rotate (on left child) + Right Rotate.
* **RL Case** → Right Rotate (on right child) + Left Rotate.

---

### 4. **Insert**

* Do normal BST insert.
* Update `height`.
* Check `balance factor`.
* Perform rotation if needed.

---

### 5. **Delete**

* Do normal BST delete.
* Update `height`.
* Check balance factor.
* Rotate if imbalance.

---

### 6. **Traversals**

* Same as BST (`inorder`, `preorder`, `postorder`).
* Inorder traversal → **sorted order**.

---

👉 This version matches exactly the **"one method = one responsibility" recursive approach** you wanted for BST.

Do you want me to also prepare the same **notes + code style for Red-Black Tree** (another self-balancing tree), or only AVL + BST is enough?
