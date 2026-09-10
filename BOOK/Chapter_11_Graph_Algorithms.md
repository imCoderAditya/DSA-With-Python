# 📖 Chapter 11: Graph Algorithms
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Graph Fundamentals & Representations

A **Graph** $G = (V, E)$ consists of **Vertices (Nodes)** $V$ and **Edges** $E$.

```
Graph Example:
   (0) ───── (1)
    │  \      │
    │   \     │
    │    \    │
   (2)    ── (3)
```

---

## 🚶 2. BFS and DFS Traversals

---

### 🌟 Example 1: BFS Traversal (Shortest Path in Unweighted Graph)
- **Start Node**: 0
- Queue trace:
  - Enqueue 0: `Queue = [0]`, `Visited = {0}`
  - Dequeue 0: Neighbors 1, 2, 3 $\implies \text{Queue} = [1, 2, 3]$, `Visited = {0, 1, 2, 3}`
  - Dequeue 1: All neighbors already visited.
  - Dequeue 2, 3: Completed.
- **BFS Order**: `0 ➔ 1 ➔ 2 ➔ 3` (Level-0: `0`, Level-1: `1, 2, 3`).

---

### 🌟 Example 2: Kahn’s Algorithm for Topological Sort
- **Prerequisites DAG**: `5 -> 2`, `5 -> 0`, `4 -> 0`, `4 -> 1`, `2 -> 3`, `3 -> 1`
- In-Degrees: `{0: 2, 1: 2, 2: 1, 3: 1, 4: 0, 5: 0}`
- Queue starts with in-degree 0: `[4, 5]`
- Step 1: Pop 4 $\implies$ output `[4]`, reduce in-degrees of 0 and 1.
- Step 2: Pop 5 $\implies$ output `[4, 5]`, reduce in-degrees of 0 and 2. In-degree of 2 becomes 0 $\implies$ enqueue 2!
- Final Valid Topo Order: `[4, 5, 2, 0, 3, 1]`.

---

### 🌟 Example 3: Dijkstra’s Shortest Path Algorithm
- **Weighted Graph**:
  - $0 \xrightarrow{4} 1$, $0 \xrightarrow{1} 2$, $2 \xrightarrow{2} 1$, $1 \xrightarrow{1} 3$
- Priority Queue trace:
  - Start at 0: `dist[0] = 0`. Heap: `[(0, 0)]`
  - Pop (0, 0): Neighbors: Node 1 (dist 4), Node 2 (dist 1). Heap: `[(1, 2), (4, 1)]`
  - Pop (1, 2): Neighbor Node 1 via Node 2 has `dist = 1 + 2 = 3 < 4`! Update `dist[1] = 3`. Heap: `[(3, 1), (4, 1)]`
  - Pop (3, 1): Neighbor Node 3 has `dist = 3 + 1 = 4`.
- **Shortest Distances from Node 0**: `{0: 0, 2: 1, 1: 3, 3: 4}`!

---

### 🌟 Example 4: Kruskal’s Minimum Spanning Tree (MST)
- Edges sorted by weight:
  1. `(2, 3, weight=1)` $\implies$ Pick (No cycle).
  2. `(0, 2, weight=2)` $\implies$ Pick (No cycle).
  3. `(1, 3, weight=3)` $\implies$ Pick (No cycle).
  4. `(0, 1, weight=4)` $\implies$ Cycle detected with DSU! **Discard.**
- Selected $V - 1 = 3$ edges with total weight $= 1 + 2 + 3 = 6$!

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch11_graphs_practice.py` to write your code:

- **Problem 11.1**: Number of Islands (LeetCode 200)
- **Problem 11.2**: Course Schedule II (Topological Sort) (LeetCode 210)
- **Problem 11.3**: Network Delay Time (Dijkstra) (LeetCode 743)
- **Problem 11.4**: Critical Connections in a Network (Tarjan's) (LeetCode 1192 - Hard)
