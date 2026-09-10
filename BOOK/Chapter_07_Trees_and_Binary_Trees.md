# 📖 Chapter 7: Trees & Binary Trees (Complete Master Guide)
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Detailed Theory & Core Intuition

### **What is a Tree?**
Unlike arrays, linked lists, stacks, and queues (which are linear data structures), a **Tree** is a **non-linear, hierarchical data structure** composed of a collection of **Nodes** connected by **Edges**.

A **Binary Tree** is a special type of tree in which each parent node has **at most two children**, called the **Left Child** and the **Right Child**.

```
Visual Architecture of a Binary Tree:

                      ┌───────────┐
                      │  Root (1) │  ◄── LEVEL 0 (Depth 0)
                      └─────┬─────┘
                  ┌─────────┴─────────┐
             ┌────▼──────┐       ┌────▼──────┐
             │ Node (2)  │       │ Node (3)  │  ◄── LEVEL 1 (Depth 1)
             └────┬──────┘       └────┬──────┘
         ┌────────┴────────┐          └────────┐
    ┌────▼──────┐     ┌────▼──────┐       ┌────▼──────┐
    │ Leaf (4)  │     │ Leaf (5)  │       │ Leaf (6)  │  ◄── LEVEL 2 (Leaves, Depth 2)
    └───────────┘     └───────────┘       └───────────┘
```

---

## 📐 2. Essential Tree Terminology & Properties

| Term | Mathematical Definition | Example from Diagram Above |
|---|---|---|
| **Root** | The topmost node of the tree (has no parent) | Node `1` |
| **Edge** | The link/connection between parent and child | Line connecting `1` and `2` |
| **Leaf Node** | A node with 0 children | Nodes `4`, `5`, `6` |
| **Depth of Node** | Number of edges from Root to that node | Depth of Node `4` $= 2$ |
| **Height of Node** | Number of edges from node to deepest leaf | Height of Root `1` $= 2$ |
| **Height of Tree** | Height of the Root node | $H = 2$ |
| **Degree of Node** | Number of children of that node | Degree of Node `2` $= 2$, Node `3` $= 1$ |

---

## 🌲 3. The 5 Major Classifications of Binary Trees

1. **Full Binary Tree (Strict Binary Tree)**:
   Every node has either **0 or 2 children** (no node has 1 child).
2. **Complete Binary Tree**:
   All levels are completely filled except possibly the last level, and all nodes in the last level are as far left as possible (Crucial foundation for **Binary Heaps**!).
3. **Perfect Binary Tree**:
   All internal nodes have 2 children, and all leaves are at the exact same depth level.
   - For height $h$, total nodes $N = 2^{h+1} - 1$.
   - Total leaf nodes $= 2^h$.
4. **Balanced Binary Tree (AVL / Red-Black)**:
   For every node, the height difference between Left and Right subtrees is at most 1 ($|h_L - h_R| \le 1$). Ensures search operations run in **$O(\log n)$**.
5. **Degenerate (Skewed) Tree**:
   Every parent node has only 1 child. It degenerates into a **Linked List** with worst-case $O(n)$ search.

---

## 🧭 4. The 4 Universal Traversals (Deep Explanation)

```
Sample Tree for Traversals:
            ( 1 )
           /     \
        ( 2 )   ( 3 )
        /   \       \
      ( 4 ) ( 5 )   ( 6 )
```

### **1. Pre-Order Traversal (Root ➔ Left ➔ Right) — Depth-First Search (DFS)**
- **Logic**: Process root, recursively visit left subtree, then right subtree.
- **Trace**: `1 ➔ 2 ➔ 4 ➔ 5 ➔ 3 ➔ 6`
- **Applications**: Cloning/copying trees, creating Prefix expressions (Polish notation), serializing trees.

### **2. In-Order Traversal (Left ➔ Root ➔ Right) — DFS**
- **Logic**: Recursively visit left subtree, process root, then right subtree.
- **Trace**: `4 ➔ 2 ➔ 5 ➔ 1 ➔ 3 ➔ 6`
- **Applications**: In Binary Search Trees (BST), In-order traversal always outputs nodes in **strictly sorted ascending order**!

### **3. Post-Order Traversal (Left ➔ Right ➔ Root) — DFS**
- **Logic**: Recursively visit left subtree, right subtree, and finally process root.
- **Trace**: `4 ➔ 5 ➔ 2 ➔ 6 ➔ 3 ➔ 1`
- **Applications**: Deleting a tree safely from bottom-up, evaluating postfix expressions, bottom-up tree DP (diameter, height).

### **4. Level-Order Traversal (Breadth-First Search - BFS)**
- **Logic**: Traverses level-by-level using a FIFO Queue.
- **Trace**:
  - Level 0: `[1]`
  - Level 1: `[2, 3]`
  - Level 2: `[4, 5, 6]`
- **Applications**: Shortest path in unweighted tree, finding node views, print tree by levels.

---

## 💡 5. Deep Master Examples & Step-by-Step Walkthroughs

---

### 🌟 Example 1: Lowest Common Ancestor (LCA) in Binary Tree
- **Definition**: The lowest common ancestor between nodes $p$ and $q$ is the deepest node that has both $p$ and $q$ as descendants.
- **Algorithm**:
  ```python
  def lowestCommonAncestor(root, p, q):
      if not root or root == p or root == q:
          return root
      left = lowestCommonAncestor(root.left, p, q)
      right = lowestCommonAncestor(root.right, p, q)
      
      # If p is in left and q is in right, root is the LCA!
      if left and right:
          return root
      return left if left else right
  ```
- **Trace for LCA(4, 6)** on sample tree:
  - `LCA(1, 4, 6)` calls left `LCA(2, 4, 6)` $\implies$ returns Node 4.
  - Right `LCA(3, 4, 6)` $\implies$ returns Node 6.
  - Since both `left` (4) and `right` (6) are found, **Node 1 is the LCA!**

---

### 🌟 Example 2: Tree Views using Horizontal Distance (HD)
Assign each node coordinate: Root is `(HD = 0, depth = 0)`.
- Left child is `(HD - 1, depth + 1)`.
- Right child is `(HD + 1, depth + 1)`.

```
Coordinate Grid:
      HD = -2       HD = -1        HD = 0        HD = 1        HD = 2
                    ( 2 ) ──────── ( 1 ) ─────── ( 3 )
                    /   \                                    \
                  ( 4 ) ( 5 )                                ( 6 )
```
- **Top View**: First node seen at each unique HD $\implies$ `[4, 2, 1, 3, 6]`.
- **Bottom View**: Last node seen at each unique HD $\implies$ `[4, 2, 5, 3, 6]`.
- **Left View**: First node seen at each vertical depth level $\implies$ `[1, 2, 4]`.
- **Right View**: Last node seen at each vertical depth level $\implies$ `[1, 3, 6]`.

---

### 🌟 Example 3: Diameter of a Binary Tree
- **Problem**: Longest path between any two nodes in the tree (may or may not pass through root).
- **Formula at each node**:
  $$\text{Longest path passing through node} = \text{Height}(\text{left}) + \text{Height}(\text{right})$$
- On sample tree:
  - Height of Node 2's left = 1 (Node 4), right = 1 (Node 5) $\implies$ Diameter at Node 2 $= 2$.
  - Height of Node 1's left = 2, right = 2 $\implies$ Diameter at Node 1 $= 2 + 2 = \mathbf{4}$ edges (`4 -> 2 -> 1 -> 3 -> 6`).
- **Max Diameter = 4!**

---

### 🌟 Example 4: Serialize and Deserialize Binary Tree (LeetCode 297 - Hard)
- **Serialization (Tree $\to$ String)** via Pre-Order BFS with `#` for `None`:
  - `[1, 2, 3, 4, 5, #, 6]` $\implies$ `"1,2,3,4,5,#,6,#,#,#,#,#,#"`
- **Deserialization (String $\to$ Tree)**:
  - Reconstruct nodes using a Queue, assigning left and right children sequentially!

---

## ✍️ 6. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch07_trees_practice.py` and implement:

---

### 🟢 **Problem 7.1: Binary Tree Level Order Traversal (LeetCode 102)**
- **Task**: Return level-by-level list of node values using a BFS Queue in $O(N)$ time.

---

### 🟢 **Problem 7.2: Diameter of Binary Tree (LeetCode 543)**
- **Task**: Compute the maximum diameter of a binary tree in $O(N)$ time and $O(H)$ space.

---

### 🟡 **Problem 7.3: Lowest Common Ancestor (LeetCode 236)**
- **Task**: Find the LCA of two nodes in a binary tree.

---

### 🔴 **Problem 7.4: Serialize and Deserialize Binary Tree (LeetCode 297)**
- **Task**: Design an algorithm to convert a binary tree to a string and rebuild it back to a tree.
