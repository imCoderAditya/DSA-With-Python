# Topic 04: Trees & Binary Search Trees (BST) - Optimal Solutions

---

## 📌 Index of Solutions
1. [Maximum Depth of Binary Tree](#1-maximum-depth-of-binary-tree)
2. [Validate Binary Search Tree](#2-validate-binary-search-tree)
3. [Lowest Common Ancestor of a Binary Tree](#3-lowest-common-ancestor-of-a-binary-tree)
4. [Binary Tree Level Order Traversal](#4-binary-tree-level-order-traversal)
5. [Invert Binary Tree](#5-invert-binary-tree)
6. [Binary Tree Maximum Path Sum](#6-binary-tree-maximum-path-sum)

---

### Node Definition
```python
from typing import Optional, List
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

---

### 1. Maximum Depth of Binary Tree

#### 💡 Intuition & Approach
Depth of tree rooted at `node` is $1 + \max(\text{depth(left)}, \text{depth(right)})$.

#### 💻 Python Solution
```python
def max_depth(root: Optional[TreeNode]) -> int:
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$ recursion stack.

---

### 2. Validate Binary Search Tree

#### 💡 Intuition & Approach
A node in a BST must satisfy `low < node.val < high`. Pass allowed boundaries down recursively:
- Left child constraint: `(low, node.val)`
- Right child constraint: `(node.val, high)`

#### 💻 Python Solution
```python
def is_valid_bst(root: Optional[TreeNode]) -> bool:
    def validate(node, low=float('-inf'), high=float('inf')):
        if not node:
            return True
        if not (low < node.val < high):
            return False
        return (validate(node.left, low, node.val) and 
                validate(node.right, node.val, high))
                
    return validate(root)
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$

---

### 3. Lowest Common Ancestor of a Binary Tree

#### 💡 Intuition & Approach
1. If `root` is `None`, `p`, or `q`, return `root`.
2. Search in left and right subtrees.
3. If both left and right return non-null, `root` is the split point (LCA!).
4. Otherwise, return the non-null result.

#### 💻 Python Solution
```python
def lowest_common_ancestor(root: TreeNode, p: TreeNode, q: TreeNode) -> Optional[TreeNode]:
    if not root or root == p or root == q:
        return root
        
    left = lowest_common_ancestor(root.left, p, q)
    right = lowest_common_ancestor(root.right, p, q)
    
    if left and right:
        return root
    return left if left else right
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$

---

### 4. Binary Tree Level Order Traversal (BFS)

#### 💡 Intuition & Approach
Use a FIFO queue. In each iteration, process all nodes currently in the queue (representing one level), record their values, and enqueue their children.

#### 💻 Python Solution
```python
def level_order(root: Optional[TreeNode]) -> List[List[int]]:
    if not root:
        return []
        
    result = []
    queue = deque([root])
    
    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)
        
    return result
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### 5. Invert Binary Tree

#### 💡 Intuition & Approach
Swap `root.left` and `root.right`, then recursively invert both subtrees.

#### 💻 Python Solution
```python
def invert_tree(root: Optional[TreeNode]) -> Optional[TreeNode]:
    if not root:
        return None
    root.left, root.right = invert_tree(root.right), invert_tree(root.left)
    return root
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$

---

### 6. Binary Tree Maximum Path Sum

#### 💡 Intuition & Approach
For each node, compute the max gain it can contribute to its parent: `max(0, gain)`.
The path max with current node as peak is `node.val + left_gain + right_gain`. Update global max with this value.

#### 💻 Python Solution
```python
def max_path_sum(root: Optional[TreeNode]) -> int:
    max_sum = float('-inf')
    
    def get_max_gain(node: Optional[TreeNode]) -> int:
        nonlocal max_sum
        if not node:
            return 0
            
        left_gain = max(get_max_gain(node.left), 0)
        right_gain = max(get_max_gain(node.right), 0)
        
        # Current path through node
        current_path = node.val + left_gain + right_gain
        max_sum = max(max_sum, current_path)
        
        # Max gain contributed to parent
        return node.val + max(left_gain, right_gain)
        
    get_max_gain(root)
    return int(max_sum)
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(H)$
