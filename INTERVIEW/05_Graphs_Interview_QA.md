# 💼 Top Interview Questions & Answers: Graph Algorithms

---

### Q1: How do you detect a cycle in a Directed Graph vs. an Undirected Graph?
**Answer**:
- **Undirected Graph**:
  - *Method 1 (DFS)*: If you visit an adjacent node that is already marked `visited` and is **NOT the direct parent** of the current node, a cycle exists.
  - *Method 2 (DSU)*: For each edge $(u, v)$, if `find(u) == find(v)`, adding this edge creates a cycle.
- **Directed Graph**:
  - *Method 1 (3-Color DFS / Recursion Stack)*:
    - White (0): Unvisited
    - Gray (1): Currently in recursion stack (active exploration)
    - Black (2): Completely processed
    - If DFS encounters a **Gray (active)** neighbor (Back-Edge), a cycle exists!
  - *Method 2 (Kahn's Algorithm)*: If topological sort processes fewer than $V$ vertices, a cycle exists.

---

### Q2: When does Dijkstra's Algorithm fail, and why do we use Bellman-Ford or Floyd-Warshall?
**Answer**:
- **Dijkstra's Algorithm fails with Negative Weight Edges** because it greedily assumes that once a node is popped from the min-heap, its shortest distance is finalized. A negative edge later can offer a shorter path, violating the greedy invariant.
- **Bellman-Ford**: Handles negative edges and detects negative weight cycles in $O(V \cdot E)$ by relaxing all edges $V - 1$ times.
- **Floyd-Warshall**: Finds all-pairs shortest paths using dynamic programming in $O(V^3)$ time and detects negative cycles on the diagonal (`dp[i][i] < 0`).

---

### Q3: What is Topological Sort, and can every graph be topologically sorted?
**Answer**:
- Topological Sort is a linear ordering of vertices such that for every directed edge $u \to v$, vertex $u$ appears before $v$.
- **Constraint**: It is **ONLY valid for Directed Acyclic Graphs (DAGs)**. If a graph contains a cycle or is undirected, a valid topological sort is mathematically impossible.

---

### Q4: Compare Kruskal’s vs. Prim’s Algorithm for Minimum Spanning Tree (MST).
**Answer**:
- **Kruskal's**: Edge-centric. Sorts all edges by weight ascending, adds edges one-by-one using **DSU (Union-Find)** if they don't create cycles. Runs in $O(E \log E)$. Better for **sparse graphs** ($E \ll V^2$).
- **Prim's**: Vertex-centric. Starts from a single node and greedily grows the tree by picking the minimum-weight adjacent edge using a **Min-Priority Queue**. Runs in $O(E \log V)$. Better for **dense graphs** ($E \approx V^2$).
