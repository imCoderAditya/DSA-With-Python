# Topic 04: Trees & Binary Search Trees (BST) - Practice Problems

---

## 📋 Problem List
1. [Maximum Depth of Binary Tree (LeetCode 104)](#problem-1-maximum-depth-of-binary-tree)
2. [Validate Binary Search Tree (LeetCode 98)](#problem-2-validate-binary-search-tree)
3. [Lowest Common Ancestor of a Binary Tree (LeetCode 236)](#problem-3-lowest-common-ancestor)
4. [Binary Tree Level Order Traversal (LeetCode 102)](#problem-4-binary-tree-level-order-traversal)
5. [Invert Binary Tree (LeetCode 226)](#problem-5-invert-binary-tree)
6. [Binary Tree Maximum Path Sum (LeetCode 124)](#problem-6-binary-tree-maximum-path-sum)
7. [Serialize and Deserialize Binary Tree (LeetCode 297)](#problem-7-serialize-and-deserialize-binary-tree)

---

### Node Definition
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

---

### Problem 1: Maximum Depth of Binary Tree
**Difficulty:** Easy | **Tags:** `Tree`, `DFS`, `BFS`

#### Description
Given the `root` of a binary tree, return its maximum depth.
A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$ where $H$ is the tree height.

---

### Problem 2: Validate Binary Search Tree
**Difficulty:** Medium | **Tags:** `Tree`, `DFS`, `BST`

#### Description
Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).
- The left subtree of a node contains only nodes with keys strictly less than the node's key.
- The right subtree of a node contains only nodes with keys strictly greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$

---

### Problem 3: Lowest Common Ancestor (LCA)
**Difficulty:** Medium | **Tags:** `Tree`, `DFS`

#### Description
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes `p` and `q`.
The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where a node can be a descendant of itself).

---

### Problem 4: Binary Tree Level Order Traversal (BFS)
**Difficulty:** Medium | **Tags:** `Tree`, `BFS`, `Queue`

#### Description
Given the `root` of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

---

### Problem 5: Invert Binary Tree
**Difficulty:** Easy | **Tags:** `Tree`, `DFS`, `BFS`

#### Description
Given the `root` of a binary tree, invert the tree, and return its root.

---

### Problem 6: Binary Tree Maximum Path Sum
**Difficulty:** Hard | **Tags:** `Tree`, `DFS`, `Dynamic Programming`

#### Description
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. The path does not need to pass through the root.
Return the maximum path sum of any non-empty path.
