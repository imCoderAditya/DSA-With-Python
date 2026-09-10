# Topic 06: Dynamic Programming - Optimal Solutions

---

## 📌 Index of Solutions
1. [Climbing Stairs](#1-climbing-stairs)
2. [Coin Change](#2-coin-change)
3. [Longest Increasing Subsequence (LIS)](#3-longest-increasing-subsequence-lis)
4. [0/1 Knapsack Problem](#4-01-knapsack-problem)
5. [Longest Common Subsequence (LCS)](#5-longest-common-subsequence-lcs)
6. [House Robber](#6-house-robber)

---

### 1. Climbing Stairs

#### 💡 Intuition & Approach
To reach step `i`, one must come from step `i-1` or `i-2`. Thus:
$$\text{dp}[i] = \text{dp}[i-1] + \text{dp}[i-2]$$
This is the Fibonacci sequence. We only need the previous two variables to achieve $O(1)$ space.

#### 💻 Python Solution
```python
def climb_stairs(n: int) -> int:
    if n <= 2:
        return n
        
    prev2, prev1 = 1, 2
    for _ in range(3, n + 1):
        curr = prev1 + prev2
        prev2 = prev1
        prev1 = curr
        
    return prev1
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### 2. Coin Change

#### 💡 Intuition & Approach
Let `dp[a]` be the minimum coins needed to make amount `a`.
$$\text{dp}[a] = \min_{c \in \text{coins}} (\text{dp}[a - c] + 1)$$
Initialize `dp` array with $\infty$ and `dp[0] = 0`.

#### 💻 Python Solution
```python
from typing import List

def coin_change(coins: List[int], amount: int) -> int:
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    
    for a in range(1, amount + 1):
        for c in coins:
            if a - c >= 0:
                dp[a] = min(dp[a], 1 + dp[a - c])
                
    return dp[amount] if dp[amount] != float('inf') else -1
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(\text{amount} \times \text{len(coins)})$
- **Space Complexity:** $O(\text{amount})$

---

### 3. Longest Increasing Subsequence (LIS)

#### 💡 Intuition & Approach
**Binary Search Method (Patience Sorting):**
Maintain a list `tails` where `tails[i]` stores the smallest tail of all increasing subsequences of length `i+1`.
- For each `x` in `nums`, find insertion index using `bisect_left`.
- If `x` is larger than all elements, append `x` (extends LIS length).
- Otherwise, replace `tails[idx] = x` (allows forming longer future sequences).

#### 💻 Python Solution
```python
import bisect
from typing import List

def length_of_lis(nums: List[int]) -> int:
    tails = []
    
    for x in nums:
        idx = bisect.bisect_left(tails, x)
        if idx == len(tails):
            tails.append(x)
        else:
            tails[idx] = x
            
    return len(tails)
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N \log N)$
- **Space Complexity:** $O(N)$

---

### 4. 0/1 Knapsack Problem

#### 💡 Intuition & Approach
1D Space Optimized DP:
Iterate backwards through capacities from `W` down to `weight` to ensure each item is used at most once.

#### 💻 Python Solution
```python
from typing import List

def knapsack(weights: List[int], values: List[int], W: int) -> int:
    dp = [0] * (W + 1)
    
    for wt, val in zip(weights, values):
        for w in range(W, wt - 1, -1):
            dp[w] = max(dp[w], dp[w - wt] + val)
            
    return dp[W]
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N \times W)$
- **Space Complexity:** $O(W)$

---

### 5. Longest Common Subsequence (LCS)

#### 💡 Intuition & Approach
- If `text1[i-1] == text2[j-1]`: `dp[i][j] = 1 + dp[i-1][j-1]`
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

#### 💻 Python Solution
```python
def longest_common_subsequence(text1: str, text2: str) -> int:
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i - 1] == text2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
                
    return dp[m][n]
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(M \times N)$
- **Space Complexity:** $O(M \times N)$ (can be optimized to $O(\min(M, N))$)

---

### 6. House Robber

#### 💡 Intuition & Approach
At each house `i`, either rob it (`nums[i] + rob1`) or skip it (`rob2`):
$$\text{curr} = \max(\text{nums}[i] + \text{rob1}, \text{rob2})$$

#### 💻 Python Solution
```python
from typing import List

def rob(nums: List[int]) -> int:
    rob1, rob2 = 0, 0
    
    for n in nums:
        temp = max(n + rob1, rob2)
        rob1 = rob2
        rob2 = temp
        
    return rob2
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
