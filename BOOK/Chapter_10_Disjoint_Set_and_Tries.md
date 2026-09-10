# 📖 Chapter 10: Disjoint Set Union (DSU) & Tries
> *Data Structures and Algorithms Made Easy — Python Edition*

---

# 🌐 Part I: Disjoint Set Union (DSU / Union-Find)

## 🎯 1. Intuition: Tracking Connected Components

A **Disjoint Set Union (DSU)** data structure maintains a collection of disjoint (non-overlapping) sets. It supports two primary operations:
1. **`find(x)`**: Returns the representative (or "root") of the set containing element $x$.
2. **`union(x, y)`**: Merges the set containing $x$ with the set containing $y$.

```
Initial Disjoint Sets: {0}, {1}, {2}, {3}, {4}
After Union(0, 1) and Union(1, 2):
       (0) ◄── Set Representative
      /   \
    (1)   (2)
```

---

## ⚡ 2. The Two DSU Optimizations

Without optimizations, tree structures can degenerate into long chains of depth $O(N)$ with $O(N)$ find operations.

### **Optimization 1: Path Compression**
During a `find(x)` call, make every node along the path point directly to the root:
```python
def find(self, x):
    if self.parent[x] != x:
        self.parent[x] = self.find(self.parent[x])  # Path Compression
    return self.parent[x]
```

### **Optimization 2: Union by Rank / Size**
Always attach the smaller tree under the root of the larger tree to keep depth minimal.

```
Path Compression Visual:
Before: (0) ◄── (1) ◄── (2) ◄── (3)
After find(3):
          (0)
       /   |   \
     (1)  (2)  (3)  (Flat tree! Next find is O(1))
```

> 🚀 **Time Complexity with both optimizations**:
> $O(\alpha(N))$ per operation, where $\alpha$ is the **Inverse Ackermann Function**. For all practical values of $N \le 10^{80}$, $\alpha(N) < 5$, effectively **$O(1)$ constant time**!

---

# 🌲 Part II: Tries (Prefix Trees)

## 🎯 3. Intuition: Why Tries Over Hash Maps?

A **Trie** (pronounced *"try"*) is a tree-like data structure used to efficiently store and retrieve keys in a dataset of strings.

### ⚖️ Hash Map vs Trie for Prefix Queries
- Searching for all words starting with prefix `"app"` in a Hash Table requires scanning all $N$ words $\implies O(N \cdot L)$.
- In a Trie, we simply walk down the `"a" -> "p" -> "p"` path in **$O(\text{prefix\_length})$**!

```
Trie Storing: ["app", "apple", "bat", "ball"]
                   (root)
                  /      \
                'a'      'b'
                 |        |
                'p'      'a'
                 |       / \
              [ 'p' ]  't'  'l'
                 |      |    |
                'l'   ['t'] ['l']
                 |
               ['e']
  (Bracketed nodes indicate is_end_of_word = True)
```

---

## 🏗️ 4. Trie Node Architecture

```python
class TrieNode:
    def __init__(self):
        self.children = {}  # char -> TrieNode
        self.is_end_of_word = False
```

### Operations Complexity:
- **Insert Word ($L$ characters)**: $O(L)$ time, $O(L)$ space.
- **Search Word ($L$ characters)**: $O(L)$ time, $O(1)$ space.
- **Starts With Prefix ($P$ characters)**: $O(P)$ time, $O(1)$ space.

---

## ✍️ 5. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch10_dsu_trie_practice.py` to write your code:

---

### **Problem 10.1: Number of Connected Components in Graph (LeetCode 323 / 547)**
- **Task**: Given $n$ nodes and a list of undirected edges, determine the total number of connected components using **DSU**.

---

### **Problem 10.2: Redundant Connection (LeetCode 684)**
- **Task**: In a tree with $n$ nodes labeled $1$ to $n$ and one extra edge added (forming a cycle), return the edge that can be removed so the graph is a tree.

---

### **Problem 10.3: Implement Trie (Prefix Tree) (LeetCode 208)**
- **Task**: Implement the `Trie` class with `insert(word)`, `search(word)`, and `startsWith(prefix)`.

---

### **Problem 10.4: Word Search II (LeetCode 212 - Hard)**
- **Task**: Given an $m \times n$ board of characters and a list of strings `words`, return all words on the board.
- **Hint**: Store the words dictionary inside a **Trie**, then run DFS/Backtracking on the 2D board against the Trie.
