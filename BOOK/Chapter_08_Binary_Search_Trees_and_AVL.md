# 📖 Chapter 8: Binary Search Trees (BST) & Self-Balancing Trees
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. The BST Property (Invariant)

A **Binary Search Tree (BST)** is a binary tree where for every node $X$:
- All values in the **Left Subtree** are **strictly smaller** than $X.val$.
- All values in the **Right Subtree** are **strictly greater** than $X.val$.
- Both Left and Right subtrees are also BSTs.

```
Valid BST:                              Invalid BST:
         8                                       8
       /   \                                   /   \
      3     10                                3     10
     / \      \                              / \      \
    1   6      14                           1   9      14
       / \                                     ▲
      4   7                         (9 is in Left subtree of 8! INVALID)
```

> 💡 **The Golden Rule**: An **In-Order Traversal (Left ➔ Root ➔ Right)** of a BST always visits nodes in **strictly ascending sorted order**!

---

## ⚙️ 2. Core Operations & Complexities

### **1. Search ($O(h)$ where $h = \text{height}$)**
- If `target == root.val`: Found!
- If `target < root.val`: Recurse on `root.left`
- If `target > root.val`: Recurse on `root.right`

### **2. Insertion ($O(h)$)**
- Walk down the tree following the BST invariant until hitting `None`, then attach the new node.

### **3. Deletion ($O(h)$ — The 3 Cases)**
- **Case 1: Node is a Leaf (0 Children)**: Simply delete the node (set parent pointer to `None`).
- **Case 2: Node has 1 Child**: Replace the node with its only child.
- **Case 3: Node has 2 Children**:
  1. Find the **In-Order Successor** (smallest value in the Right subtree) OR **In-Order Predecessor** (largest value in the Left subtree).
  2. Copy the successor's value into the target node.
  3. Delete the in-order successor from the right subtree (which will fall into Case 1 or 2).

```
Deleting Node 3 (Has 2 Children):
         8                                 8
       /   \                             /   \
     [3]    10   ──(Successor is 4)──>  [4]   10
     / \      \                         / \      \
    1   6      14                      1   6      14
       / \                                  \
     (4)  7                                  7
```

| Operation | Average Case (Balanced) | Worst Case (Skewed) |
|---|---|---|
| Search | $O(\log n)$ | $O(n)$ |
| Insert | $O(\log n)$ | $O(n)$ |
| Delete | $O(\log n)$ | $O(n)$ |

---

## ⚖️ 3. Self-Balancing Trees: The AVL Tree

When keys are inserted in sorted order (e.g., $1, 2, 3, 4, 5$), a standard BST degenerates into a linear linked list ($O(n)$ search).

An **AVL Tree** maintains height balance by enforcing the **Balance Factor ($BF$)**:
$$BF(\text{Node}) = \text{Height}(\text{Left Subtree}) - \text{Height}(\text{Right Subtree}) \in \{-1, 0, +1\}$$

Whenever an insertion/deletion causes $|BF| > 1$, we perform **Tree Rotations**:

### **The 4 AVL Rotations:**
1. **LL Case (Left-Left)** $\implies$ Single **Right Rotation**
2. **RR Case (Right-Right)** $\implies$ Single **Left Rotation**
3. **LR Case (Left-Right)** $\implies$ **Left Rotation** on left child, then **Right Rotation** on root
4. **RL Case (Right-Left)** $\implies$ **Right Rotation** on right child, then **Left Rotation** on root

```
Right Rotation (LL Case):
        z                                y
       / \                             /   \
      y   T4    ──(Rotate Right)──>   x     z
     / \                             / \   / \
    x   T3                          T1 T2 T3 T4
   / \
  T1 T2
```

---

## ✍️ 4. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch08_bst_practice.py` to write your code:

---

### **Problem 8.1: Validate Binary Search Tree (LeetCode 98)**
- **Task**: Given the root of a binary tree, determine if it is a valid BST.
- **Hint**: Pass down valid ranges `(min_val, max_val)` recursively: for left child `(min_val, root.val)`, for right child `(root.val, max_val)`.

---

### **Problem 8.2: Kth Smallest Element in a BST (LeetCode 230)**
- **Task**: Given the root of a BST and an integer `k`, return the $k^{\text{th}}$ smallest value (1-indexed) in the tree.
- **Hint**: Perform an iterative in-order traversal with a stack; stop at the $k^{\text{th}}$ popped node.

---

### **Problem 8.3: Delete Node in a BST (LeetCode 450)**
- **Task**: Given a root node and a key, delete the node with the given key in the BST and return the new root.

---

### **Problem 8.4: Convert Sorted Array to Balanced BST (LeetCode 108)**
- **Task**: Given an integer array `nums` where the elements are sorted in ascending order, convert it to a **height-balanced** binary search tree.
- **Target Complexity**: Time $O(N)$, Space $O(\log N)$.
