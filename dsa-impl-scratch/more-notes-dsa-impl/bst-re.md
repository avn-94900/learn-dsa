Perfect 👍 You want a **recursive BST implementation**, but with **one function per responsibility** (no extra public + private duplication).
That means:

* Use recursion wherever it’s natural (`insert`, `search`, `delete`, traversals, height).
* Keep a **single method for each responsibility** (not a wrapper + helper).
* Clear notes for interview prep.

Here’s the clean version:

---

```java
class Node {
    int key;
    Node left, right;

    Node(int key) {
        this.key = key;
    }
}

public class BinarySearchTree {
    Node root;

    // ---------------- INSERT ----------------
    public Node insert(Node node, int key) {
        if (node == null) return new Node(key);

        if (key < node.key) node.left = insert(node.left, key);
        else if (key > node.key) node.right = insert(node.right, key);
        // duplicates ignored
        return node;
    }

    // ---------------- SEARCH ----------------
    public boolean search(Node node, int key) {
        if (node == null) return false;
        if (node.key == key) return true;
        return key < node.key ? search(node.left, key) : search(node.right, key);
    }

    // ---------------- DELETE ----------------
    public Node delete(Node node, int key) {
        if (node == null) return null;

        if (key < node.key) {
            node.left = delete(node.left, key);
        } else if (key > node.key) {
            node.right = delete(node.right, key);
        } else {
            // Case 1: No child
            if (node.left == null && node.right == null) return null;

            // Case 2: One child
            if (node.left == null) return node.right;
            if (node.right == null) return node.left;

            // Case 3: Two children → use inorder successor
            Node succ = minNode(node.right);
            node.key = succ.key;
            node.right = delete(node.right, succ.key);
        }
        return node;
    }

    // ---------------- MIN & MAX ----------------
    public Node minNode(Node node) {
        if (node.left == null) return node;
        return minNode(node.left);
    }

    public Node maxNode(Node node) {
        if (node.right == null) return node;
        return maxNode(node.right);
    }

    // ---------------- HEIGHT ----------------
    public int height(Node node) {
        if (node == null) return 0;
        return 1 + Math.max(height(node.left), height(node.right));
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
        BinarySearchTree bst = new BinarySearchTree();

        int[] keys = {50, 30, 20, 40, 70, 60, 80};
        for (int k : keys) bst.root = bst.insert(bst.root, k);

        System.out.print("Inorder: ");
        bst.inorder(bst.root);
        System.out.println();

        System.out.print("Preorder: ");
        bst.preorder(bst.root);
        System.out.println();

        System.out.print("Postorder: ");
        bst.postorder(bst.root);
        System.out.println();

        System.out.println("Min: " + bst.minNode(bst.root).key);
        System.out.println("Max: " + bst.maxNode(bst.root).key);
        System.out.println("Height: " + bst.height(bst.root));

        System.out.println("Search 40: " + bst.search(bst.root, 40));
        System.out.println("Search 90: " + bst.search(bst.root, 90));

        bst.root = bst.delete(bst.root, 20);
        bst.inorder(bst.root); System.out.println();

        bst.root = bst.delete(bst.root, 30);
        bst.inorder(bst.root); System.out.println();

        bst.root = bst.delete(bst.root, 50);
        bst.inorder(bst.root); System.out.println();
    }
}
```

---

## 📝 Notes (for interviews & revision)

### 1. **Insert**

* Always compare `key` with current `node.key`.
* If smaller → go left, if larger → go right.
* If `null` → create new node.

### 2. **Search**

* Base case: `null` → not found.
* If `key == node.key` → found.
* Recurse left/right based on comparison.

### 3. **Delete Cases**

1. **Leaf node** → return `null`.
2. **One child** → return that child.
3. **Two children** → find **inorder successor** (smallest in right subtree), replace current node’s key with successor’s key, and recursively delete successor.

### 4. **Min & Max**

* `minNode` → keep going left until `left == null`.
* `maxNode` → keep going right until `right == null`.

### 5. **Height**

* Empty tree = 0.
* `1 + max(height(left), height(right))`.

### 6. **Traversals**

* **Inorder** (L → Root → R) → gives **sorted order** in BST.
* **Preorder** (Root → L → R).
* **Postorder** (L → R → Root).

---

👉 This design has **exactly one method per responsibility**, is **recursive**, and avoids duplicate wrappers.

Do you also want me to add a **recursive level-order (BFS using height)**, or keep it only DFS traversals (inorder/preorder/postorder)?
