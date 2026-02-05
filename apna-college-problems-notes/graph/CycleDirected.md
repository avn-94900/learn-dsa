Perfect 👌 You’re asking about **Cycle Detection in a Directed Graph** using **DFS + recursion stack (`rec[]`)**.
I’ll prepare **well-structured notes with Java code + comments**, so it’s crystal clear.

---

# 📒 Notes: Cycle Detection in Directed Graph (DFS + Recursion Stack)

### 🔹 Concept

1. In a **directed graph**, a cycle exists if during DFS traversal we revisit a node that is already in the **current recursion stack** (`rec[]`).
2. We use two arrays:

   * `vis[]`: marks if a node has been visited *at all*.
   * `rec[]`: marks if a node is in the *current recursion path*.
3. If we ever find an edge to a node that is `rec[dest] == true`, → **cycle detected**.
4. After DFS returns, we must reset `rec[curr] = false` (backtracking).

---

### 🔹 Java Code (with comments)

```java
import java.util.*;

class CycleDirected {
    static class Edge {
        int src, dest;
        Edge(int s, int d) {
            src = s;
            dest = d;
        }
    }

    // Create graph
    public static void createGraph(ArrayList<Edge>[] graph) {
        for (int i = 0; i < graph.length; i++) {
            graph[i] = new ArrayList<>();
        }
        // Example: Directed edges
        graph[0].add(new Edge(0, 1));
        graph[1].add(new Edge(1, 2));
        graph[2].add(new Edge(2, 3));
        graph[3].add(new Edge(3, 1)); // Back edge → cycle
    }

    // DFS based cycle detection
    public static boolean isCycleDirected(ArrayList<Edge>[] graph, boolean[] vis, int curr, boolean[] rec) {
        vis[curr] = true;    // Mark as visited
        rec[curr] = true;    // Mark in recursion stack

        for (Edge e : graph[curr]) {
            // Case 1: Node already in recursion stack → cycle
            if (rec[e.dest]) {
                return true;
            }
            // Case 2: Not visited yet → DFS
            else if (!vis[e.dest]) {
                if (isCycleDirected(graph, vis, e.dest, rec)) {
                    return true;
                }
            }
        }

        // Backtrack → remove from recursion stack
        rec[curr] = false;
        return false;
    }

    public static void main(String[] args) {
        int V = 4;
        ArrayList<Edge>[] graph = new ArrayList[V];
        createGraph(graph);

        boolean[] vis = new boolean[V];
        boolean[] rec = new boolean[V];

        // Check all nodes → handles **disconnected graph** also
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                if (isCycleDirected(graph, vis, i, rec)) {
                    System.out.println("Cycle exists");
                    return;
                }
            }
        }
        System.out.println("No cycle");
    }
}
```

---

### 🔹 Key Notes

* `vis[]` → ensures we don’t repeat DFS unnecessarily.
* `rec[]` → tracks the current call stack. If we revisit, → **cycle**.
* **Disconnected Graphs**:
  We loop through all vertices in `main()`.

  ```java
  for (int i = 0; i < V; i++) {
      if (!vis[i]) {
          ...
      }
  }
  ```
* Backtracking step: `rec[curr] = false;` is mandatory, otherwise recursion stack won’t shrink properly.

---

👉 Do you also want me to add a **dry run table** showing `vis[]` and `rec[]` updates step by step for the example graph (0→1→2→3→1 cycle)?
