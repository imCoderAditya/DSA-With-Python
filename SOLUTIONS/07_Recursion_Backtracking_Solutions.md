# Topic 07: Recursion & Backtracking - Optimal Solutions

---

## 📌 Index of Solutions
1. [Subsets](#1-subsets)
2. [Permutations](#2-permutations)
3. [Combination Sum](#3-combination-sum)
4. [N-Queens](#4-n-queens)

---

### 1. Subsets

#### 💡 Intuition & Approach
At each index `i`, we have two decisions: include `nums[i]` in the current subset or exclude it.

#### 💻 Python Solution
```python
from typing import List

def subsets(nums: List[int]) -> List[List[int]]:
    res = []
    subset = []
    
    def backtrack(i: int):
        if i >= len(nums):
            res.append(subset.copy())
            return
        # Decision 1: Include nums[i]
        subset.append(nums[i])
        backtrack(i + 1)
        # Decision 2: Exclude nums[i]
        subset.pop()
        backtrack(i + 1)
        
    backtrack(0)
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N \cdot 2^N)$
- **Space Complexity:** $O(N)$ auxiliary stack.

---

### 2. Permutations

#### 💡 Intuition & Approach
Backtrack by maintaining a list of remaining numbers or a `visited` boolean set.

#### 💻 Python Solution
```python
from typing import List

def permute(nums: List[int]) -> List[List[int]]:
    res = []
    
    def backtrack(curr_perm, remaining):
        if not remaining:
            res.append(curr_perm)
            return
        for i in range(len(remaining)):
            backtrack(curr_perm + [remaining[i]], remaining[:i] + remaining[i+1:])
            
    backtrack([], nums)
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N \cdot N!)$
- **Space Complexity:** $O(N)$

---

### 3. Combination Sum

#### 💡 Intuition & Approach
Use index `i` to avoid generating duplicate permutations. Allow reusing the same candidate by recurring on the same index `i`.

#### 💻 Python Solution
```python
from typing import List

def combination_sum(candidates: List[int], target: int) -> List[List[int]]:
    res = []
    
    def backtrack(i: int, current_comb: List[int], total: int):
        if total == target:
            res.append(current_comb.copy())
            return
        if i >= len(candidates) or total > target:
            return
            
        # Include candidate[i]
        current_comb.append(candidates[i])
        backtrack(i, current_comb, total + candidates[i])
        # Skip candidate[i]
        current_comb.pop()
        backtrack(i + 1, current_comb, total)
        
    backtrack(0, [], 0)
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(2^{target / \min(candidates)})$
- **Space Complexity:** $O(target / \min(candidates))$

---

### 4. N-Queens

#### 💡 Intuition & Approach
Track occupied columns, positive diagonals $(r + c)$, and negative diagonals $(r - c)$ using sets for $O(1)$ validity checking.

#### 💻 Python Solution
```python
from typing import List

def solve_n_queens(n: int) -> List[List[str]]:
    cols = set()
    pos_diag = set()  # (r + c)
    neg_diag = set()  # (r - c)
    
    res = []
    board = [["."] * n for _ in range(n)]
    
    def backtrack(r: int):
        if r == n:
            res.append(["".join(row) for row in board])
            return
            
        for c in range(n):
            if c in cols or (r + c) in pos_diag or (r - c) in neg_diag:
                continue
                
            cols.add(c)
            pos_diag.add(r + c)
            neg_diag.add(r - c)
            board[r][c] = "Q"
            
            backtrack(r + 1)
            
            cols.remove(c)
            pos_diag.remove(r + c)
            neg_diag.remove(r - c)
            board[r][c] = "."
            
    backtrack(0)
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N!)$
- **Space Complexity:** $O(N^2)$ board state.
