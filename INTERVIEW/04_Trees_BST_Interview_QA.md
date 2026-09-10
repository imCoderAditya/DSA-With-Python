# 💼 Top Interview Questions & Answers: Trees & Binary Search Trees (BST)

---

### Q1: What is the difference between a Binary Tree and a Binary Search Tree (BST)?
**Answer**:
- A **Binary Tree** is any tree where each node has at most 2 children with no value ordering constraint.
- A **Binary Search Tree (BST)** enforces the BST Invariant: For every node $X$, all values in the left subtree are strictly $< X.val$ and all values in the right subtree are strictly $> X.val$.
- In a BST, **In-Order Traversal (Left $\to$ Root $\to$ Right)** always yields elements in strictly ascending sorted order.

---

### Q2: How does node deletion work in a BST when the node has 2 children?
**Answer**:
- If the node has 2 children:
  1. Find the **In-Order Successor** (the smallest value in the right subtree) OR **In-Order Predecessor** (the largest value in the left subtree).
  2. Copy that successor's value into the node to be deleted.
  3. Recursively delete the successor node from the right subtree (which is guaranteed to have at most 1 child).

---

### Q3: What is the difference between BFS and DFS in trees, and when should you choose one over the other?
**Answer**:
- **BFS (Level-Order Traversal)** uses a FIFO Queue.
  - *Best for*: Finding the shortest path/distance, tree views (top, bottom, left, right), printing level by level.
  - *Space*: $O(W)$ where $W$ is maximum width of tree (up to $N/2$ nodes at leaf level).
- **DFS (Pre, In, Post-Order)** uses recursion or an explicit Stack.
  - *Best for*: Path sum queries, checking subtree validity, LCA, tree diameter, serialization.
  - *Space*: $O(H)$ where $H$ is height of the tree ($\log N$ for balanced, $N$ for skewed).

---

### Q4: What causes a BST to degrade to $O(N)$ and how do Self-Balancing Trees (AVL / Red-Black) prevent it?
**Answer**:
- Inserting sorted or reverse-sorted keys into a plain BST creates a **skewed degenerate tree** (linked list) with $O(N)$ operations.
- **AVL Trees** enforce the balance factor $BF = |h_L - h_R| \le 1$ using 4 rotation types (LL, RR, LR, RL) upon insert/delete, guaranteeing height $H \le 1.44 \log_2 N \implies \mathbf{O(\log N)}$ operations.
- **Red-Black Trees** (used in Java `TreeMap`, C++ `std::map`) enforce color invariants with at most 2 rotations per insertion.
