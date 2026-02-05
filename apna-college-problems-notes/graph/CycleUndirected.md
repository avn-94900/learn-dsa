Got it 👍
You’re talking about **Cycle Detection in an Undirected Graph** using **DFS**.
Let me give you the **complete clean Java code + explanation notes**.

---

# 📒 Notes: Cycle Detection in Undirected Graph (DFS)

### 🔹 Concept

* In an **undirected graph**, a cycle exists if during DFS:

  1. We find a neighbor that is **already visited**.
  2. That neighbor is **not the parent** (the node we came from).
* We pass `par` (parent node) into DFS to differentiate between a **back edge** and the **edge to parent**.

---

### ✅ Java Code

```java
import java.util.*;

class CycleUndirected {
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
        // Example: Undirected edges (add both ways)
        graph[0].add(new Edge(0, 1));
        graph[1].add(new Edge(1, 0));

        graph[0].add(new Edge(0, 2));
        graph[2].add(new Edge(2, 0));

        graph[1].add(new Edge(1, 2));
        graph[2].add(new Edge(2, 1));

        graph[2].add(new Edge(2, 3));
        graph[3].add(new Edge(3, 2));
    }

    // DFS cycle detection
    public static boolean isCycleUndirected(ArrayList<Edge>[] graph, boolean[] vis, int curr, int par) {
        vis[curr] = true;

        for (int i = 0; i < graph[curr].size(); i++) {
            Edge e = graph[curr].get(i);

            // Case 1: already visited and not parent → cycle
            if (vis[e.dest] && e.dest != par) {
                return true;
            }
            // Case 2: not visited → DFS
            else if (!vis[e.dest]) {
                if (isCycleUndirected(graph, vis, e.dest, curr)) {
                    return true;
                }
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int V = 4;
        ArrayList<Edge>[] graph = new ArrayList[V];
        createGraph(graph);

        boolean[] vis = new boolean[V];
        boolean cycleExists = false;

        // Handle disconnected graph also
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                if (isCycleUndirected(graph, vis, i, -1)) {
                    cycleExists = true;
                    break;
                }
            }
        }

        if (cycleExists) {
            System.out.println("Cycle exists in the graph.");
        } else {
            System.out.println("No cycle in the graph.");
        }
    }
}
```

---

### 🔹 Key Notes

1. `par` = parent node to avoid false cycle detection.

   * Example: In `0 → 1 → 0`, revisiting `0` is fine because it’s the parent.
2. If we find a visited node that’s **not the parent**, it’s a **cycle**.
3. Loop over all nodes in `main()` to handle **disconnected graphs**.

---

👉 Do you want me to also prepare a **dry run step-by-step** (with a `vis[]` table) for this graph so you can see exactly how the cycle gets detected?
