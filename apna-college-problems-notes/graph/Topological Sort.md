
# Notes: Topological Sort in Graphs

### 🔹 What is Topological Sort?

* **Definition**: A linear ordering of vertices of a **Directed Acyclic Graph (DAG)** such that for every directed edge `u → v`, vertex `u` appears **before** vertex `v` in the ordering.
* **Important**:

  * Works **only on DAGs** (Directed Acyclic Graphs).
  * Useful for scheduling tasks, build systems, course prerequisite problems, etc.

---

### 🔹 Two Common Approaches

1. **DFS-based** (reverse postorder of DFS traversal).
2. **BFS-based (Kahn’s Algorithm)** using **indegree**.

---

## ✅ 1. DFS-based Topological Sort

### Idea

* Run DFS, and once a node has explored all neighbors, **push it onto a stack**.
* At the end, popping from the stack gives a valid topological ordering.

### Java Code

```java
import java.util.*;

class TopoSortDFS {
    static class Edge {
        int src, dest;
        Edge(int s, int d) {
            src = s; dest = d;
        }
    }

    // Create graph
    public static void createGraph(ArrayList<Edge>[] graph) {
        for (int i = 0; i < graph.length; i++) {
            graph[i] = new ArrayList<>();
        }
        // Example DAG
        graph[0].add(new Edge(0, 2));
        graph[0].add(new Edge(0, 3));
        graph[1].add(new Edge(1, 3));
        graph[2].add(new Edge(2, 4));
        graph[3].add(new Edge(3, 4));
    }

    // DFS helper
    public static void topoSortUtil(ArrayList<Edge>[] graph, int curr, boolean[] vis, Stack<Integer> stack) {
        vis[curr] = true;
        for (Edge e : graph[curr]) {
            if (!vis[e.dest]) {
                topoSortUtil(graph, e.dest, vis, stack);
            }
        }
        stack.push(curr); // add after exploring all neighbors
    }

    // Topological sort
    public static void topoSort(ArrayList<Edge>[] graph) {
        boolean[] vis = new boolean[graph.length];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < graph.length; i++) {
            if (!vis[i]) {
                topoSortUtil(graph, i, vis, stack);
            }
        }

        // Print ordering
        while (!stack.isEmpty()) {
            System.out.print(stack.pop() + " ");
        }
    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<Edge>[] graph = new ArrayList[V];
        createGraph(graph);

        System.out.println("Topological Sort (DFS):");
        topoSort(graph);
    }
}
```

---

## ✅ 2. BFS-based (Kahn’s Algorithm)

### Idea

* Compute **indegree** of each vertex.
* Start with vertices having `indegree = 0`.
* Remove them one by one, decreasing indegree of neighbors.
* Continue until all vertices are processed.

### Java Code

```java
import java.util.*;

class TopoSortBFS {
    static class Edge {
        int src, dest;
        Edge(int s, int d) {
            src = s; dest = d;
        }
    }

    // Create graph
    public static void createGraph(ArrayList<Edge>[] graph) {
        for (int i = 0; i < graph.length; i++) {
            graph[i] = new ArrayList<>();
        }
        // Example DAG
        graph[0].add(new Edge(0, 2));
        graph[0].add(new Edge(0, 3));
        graph[1].add(new Edge(1, 3));
        graph[2].add(new Edge(2, 4));
        graph[3].add(new Edge(3, 4));
    }

    // BFS Topological Sort (Kahn’s Algorithm)
    public static void topoSortBFS(ArrayList<Edge>[] graph) {
        int V = graph.length;
        int[] indeg = new int[V];

        // Compute indegree
        for (int i = 0; i < V; i++) {
            for (Edge e : graph[i]) {
                indeg[e.dest]++;
            }
        }

        Queue<Integer> q = new LinkedList<>();
        // Add nodes with indegree 0
        for (int i = 0; i < V; i++) {
            if (indeg[i] == 0) {
                q.add(i);
            }
        }

        // Process nodes
        while (!q.isEmpty()) {
            int curr = q.remove();
            System.out.print(curr + " ");

            for (Edge e : graph[curr]) {
                indeg[e.dest]--;
                if (indeg[e.dest] == 0) {
                    q.add(e.dest);
                }
            }
        }
    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<Edge>[] graph = new ArrayList[V];
        createGraph(graph);

        System.out.println("Topological Sort (BFS - Kahn’s Algorithm):");
        topoSortBFS(graph);
    }
}
```

---

## 🔹 Key Notes

* **DFS Method**:

  * Uses recursion + stack.
  * Push node after visiting all its children.
  * Reverse of finishing time order.

* **BFS (Kahn’s Algorithm)**:

  * Works level by level using **indegree**.
  * More intuitive for scheduling tasks.

* **Applications**:

  * Job scheduling.
  * Course prerequisite ordering.
  * Build systems dependency resolution.
  * Detecting cycles in directed graphs (if topo sort is impossible → cycle exists).

---

👉 Do you want me to also add a **dry run table** comparing DFS-based vs BFS-based topo sort on the same example graph?
