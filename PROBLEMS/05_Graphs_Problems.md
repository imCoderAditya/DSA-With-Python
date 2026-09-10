# Topic 05: Graphs & Graph Algorithms - Practice Problems

---

## 📋 Problem List
1. [Number of Islands (LeetCode 200)](#problem-1-number-of-islands)
2. [Clone Graph (LeetCode 133)](#problem-2-clone-graph)
3. [Course Schedule (Cycle Detection / Topological Sort - LeetCode 207)](#problem-3-course-schedule)
4. [Word Ladder (Shortest Path BFS - LeetCode 127)](#problem-4-word-ladder)
5. [Network Delay Time (Dijkstra's Algorithm - LeetCode 743)](#problem-5-network-delay-time)
6. [Cheapest Flights Within K Stops (Bellman-Ford / BFS - LeetCode 787)](#problem-6-cheapest-flights-within-k-stops)

---

### Problem 1: Number of Islands
**Difficulty:** Medium | **Tags:** `Array`, `DFS`, `BFS`, `Union Find`

#### Description
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.
An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

#### Target Complexity
- **Time Complexity:** $O(M \times N)$
- **Space Complexity:** $O(M \times N)$

---

### Problem 2: Clone Graph
**Difficulty:** Medium | **Tags:** `Hash Table`, `DFS`, `BFS`, `Graph`

#### Description
Given a reference of a node in a connected undirected graph. Return a deep copy (clone) of the graph.

---

### Problem 3: Course Schedule (Topological Sort / Kahn's Algorithm)
**Difficulty:** Medium | **Tags:** `DFS`, `BFS`, `Graph`, `Topological Sort`

#### Description
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a_i, b_i]` indicates that you must take course $b_i$ first if you want to take course $a_i$.

Return `true` if you can finish all courses. Otherwise, return `false`.

---

### Problem 4: Word Ladder
**Difficulty:** Hard | **Tags:** `Hash Table`, `String`, `BFS`

#### Description
A transformation sequence from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words $beginWord \to s_1 \to s_2 \to \dots \to s_k$ such that every adjacent pair of words differs by a single letter.
Return the number of words in the shortest transformation sequence from `beginWord` to `endWord`, or `0` if no such sequence exists.

---

### Problem 5: Network Delay Time (Dijkstra's Algorithm)
**Difficulty:** Medium | **Tags:** `DFS`, `BFS`, `Graph`, `Heap (Priority Queue)`, `Shortest Path`

#### Description
You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (u_i, v_i, w_i)`.
We send a signal from a given node `k`. Return the minimum time it takes for all the `n` nodes to receive the signal. If it is impossible, return `-1`.
