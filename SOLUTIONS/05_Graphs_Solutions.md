# Topic 05: Graphs & Graph Algorithms - Optimal Solutions

---

## 📌 Index of Solutions
1. [Number of Islands](#1-number-of-islands)
2. [Clone Graph](#2-clone-graph)
3. [Course Schedule (Topological Sort)](#3-course-schedule-topological-sort)
4. [Word Ladder (BFS)](#4-word-ladder-bfs)
5. [Network Delay Time (Dijkstra's Algorithm)](#5-network-delay-time-dijkstras-algorithm)

---

### 1. Number of Islands

#### 💡 Intuition & Approach
Iterate through every cell $(r, c)$. If `grid[r][c] == '1'`, increment `island_count` and launch DFS/BFS to sink the entire island by marking connected land cells to `'0'`.

#### 💻 Python Solution
```python
from typing import List

def num_islands(grid: List[List[str]]) -> int:
    if not grid:
        return 0
        
    rows, cols = len(grid), len(grid[0])
    count = 0
    
    def dfs(r: int, c: int):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
            return
        grid[r][c] = '0'  # Mark visited / sunk
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)
        
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)
                
    return count
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(M \times N)$ — Each cell is visited constant times.
- **Space Complexity:** $O(M \times N)$ — Call stack in worst case.

---

### 2. Clone Graph

#### 💡 Intuition & Approach
Use a hash map `cloned = {original_node: cloned_node}` to remember already cloned nodes and avoid infinite loops in cyclic graphs.

#### 💻 Python Solution
```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []

def clone_graph(node: 'Node') -> 'Node':
    if not node:
        return None
        
    cloned = {}
    
    def dfs(curr: 'Node') -> 'Node':
        if curr in cloned:
            return cloned[curr]
            
        copy = Node(curr.val)
        cloned[curr] = copy
        for neighbor in curr.neighbors:
            copy.neighbors.append(dfs(neighbor))
        return copy
        
    return dfs(node)
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(V + E)$
- **Space Complexity:** $O(V)$

---

### 3. Course Schedule (Kahn's Algorithm / Topological Sort)

#### 💡 Intuition & Approach
1. Build adjacency list and compute indegree for each node.
2. Push all nodes with `indegree == 0` into a queue.
3. Pop a node, decrement indegree of its neighbors. If neighbor's indegree becomes 0, enqueue it.
4. If processed count equals `numCourses`, no cycle exists ($\implies \text{True}$).

#### 💻 Python Solution
```python
from collections import deque, defaultdict
from typing import List

def can_finish(numCourses: int, prerequisites: List[List[int]]) -> bool:
    adj = defaultdict(list)
    indegree = [0] * numCourses
    
    for dest, src in prerequisites:
        adj[src].append(dest)
        indegree[dest] += 1
        
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    taken = 0
    
    while queue:
        course = queue.popleft()
        taken += 1
        for neighbor in adj[course]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
                
    return taken == numCourses
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(V + E)$
- **Space Complexity:** $O(V + E)$

---

### 4. Word Ladder (BFS)

#### 💡 Intuition & Approach
Since every edge has weight 1 (single character change), standard BFS guarantees finding the shortest transformation path. Use generic intermediate pattern matching (e.g., `*ot` for `hot`, `dot`, `lot`) or check alphabet substitution.

#### 💻 Python Solution
```python
from collections import deque
from typing import List, Set

def ladder_length(beginWord: str, endWord: str, wordList: List[str]) -> int:
    word_set: Set[str] = set(wordList)
    if endWord not in word_set:
        return 0
        
    queue = deque([(beginWord, 1)])
    visited = {beginWord}
    
    while queue:
        word, length = queue.popleft()
        if word == endWord:
            return length
            
        for i in range(len(word)):
            for ch in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + ch + word[i+1:]
                if next_word in word_set and next_word not in visited:
                    visited.add(next_word)
                    queue.append((next_word, length + 1))
                    
    return 0
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(M^2 \times N)$ where $M$ is word length and $N$ is number of words.
- **Space Complexity:** $O(M \times N)$

---

### 5. Network Delay Time (Dijkstra's Algorithm)

#### 💡 Intuition & Approach
Use a Min-Heap (priority queue) with entries `(time, node)`:
1. Always pop the unvisited node with minimum travel time.
2. Relax outgoing edges: if `time + weight < dist[neighbor]`, update distance and push to heap.
3. Maximum distance among all nodes is the answer (or `-1` if some nodes remain unreached).

#### 💻 Python Solution
```python
import heapq
from collections import defaultdict
from typing import List

def network_delay_time(times: List[List[int]], n: int, k: int) -> int:
    graph = defaultdict(list)
    for u, v, w in times:
        graph[u].append((v, w))
        
    pq = [(0, k)]  # (current_distance, node)
    distances = {}
    
    while pq:
        time, node = heapq.heappop(pq)
        if node in distances:
            continue
        distances[node] = time
        
        for neighbor, weight in graph[node]:
            if neighbor not in distances:
                heapq.heappush(pq, (time + weight, neighbor))
                
    return max(distances.values()) if len(distances) == n else -1
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(E \log V)$
- **Space Complexity:** $O(V + E)$
