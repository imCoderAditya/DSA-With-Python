# 📖 Chapter 17: Dynamic Programming (DP)
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Intuition: What is Dynamic Programming?

**Dynamic Programming (DP)** is an optimization over recursion. It solves each unique subproblem **exactly once** and stores the result in a table (cache) to eliminate duplicate calculations.

---

## 🏛️ 2. Step-by-Step Classic DP Examples

---

### 🌟 Example 1: 0/1 Knapsack Problem Walkthrough
- **Items**: 
  - Item 1: $\text{Weight} = 1, \text{Value} = 1$
  - Item 2: $\text{Weight} = 2, \text{Value} = 6$
  - Item 3: $\text{Weight} = 3, \text{Value} = 10$
- **Capacity**: $W = 5$
- **DP Table Computation**: `dp[i][w] = max(dp[i-1][w], dp[i-1][w - weight[i]] + value[i])`

| Items \ Capacity | $w=0$ | $w=1$ | $w=2$ | $w=3$ | $w=4$ | $w=5$ |
|---|---|---|---|---|---|---|
| **0 (No items)** | 0 | 0 | 0 | 0 | 0 | 0 |
| **Item 1 (wt=1, val=1)** | 0 | 1 | 1 | 1 | 1 | 1 |
| **Item 2 (wt=2, val=6)** | 0 | 1 | 6 | 7 | 7 | 7 |
| **Item 3 (wt=3, val=10)** | 0 | 1 | 6 | 10 | 11 | **16** |

- At $i=3, w=5$: $\max(\text{exclude}=7, \text{include}=dp[2][5-3] + 10 = 6 + 10 = \mathbf{16})$.
- **Maximum Value = 16 (Items 2 and 3 chosen)!**

---

### 🌟 Example 2: Longest Common Subsequence (LCS)
- **Strings**: `s1 = "ABCDE"`, `s2 = "ACE"`
- Matrix Filling:
  - When characters match: `dp[i][j] = 1 + dp[i-1][j-1]`
  - When characters differ: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`
- Trace: Matches occur at `'A'`, `'C'`, `'E'` $\implies \mathbf{\text{LCS Length} = 3}$ (`"ACE"`).

---

### 🌟 Example 3: Coin Change Problem
- **Coins**: `[1, 2, 5]`, **Amount**: `11`
- `dp[a]` = Minimum coins for amount $a$:
  - `dp[0] = 0`
  - `dp[1] = 1` (1)
  - `dp[2] = 1` (2)
  - `dp[5] = 1` (5)
  - `dp[10] = dp[5] + 1 = 2` (5 + 5)
  - `dp[11] = dp[10] + 1 = 3` (5 + 5 + 1)
- **Fewest Coins = 3!**

---

### 🌟 Example 4: Longest Increasing Subsequence (LIS) in $O(N \log N)$
- **Array**: `[10, 9, 2, 5, 3, 7, 101, 18]`
- Maintain `tails` array with Binary Search (`bisect_left`):
  - Num 10: `tails = [10]`
  - Num 9: Replace 10 $\implies \text{tails} = [9]$
  - Num 2: Replace 9 $\implies \text{tails} = [2]$
  - Num 5: Append 5 $\implies \text{tails} = [2, 5]$
  - Num 3: Replace 5 $\implies \text{tails} = [2, 3]$
  - Num 7: Append 7 $\implies \text{tails} = [2, 3, 7]$
  - Num 101: Append 101 $\implies \text{tails} = [2, 3, 7, 101]$
  - Num 18: Replace 101 $\implies \text{tails} = [2, 3, 7, 18]$
- **Length of LIS = len(tails) = 4 (Subsequence `[2, 3, 7, 18]`)!**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch17_dp_practice.py` to write your code:

- **Problem 17.1**: Coin Change (LeetCode 322)
- **Problem 17.2**: Partition Equal Subset Sum (LeetCode 416)
- **Problem 17.3**: Edit Distance (LeetCode 72 - Hard)
- **Problem 17.4**: Longest Increasing Subsequence in $O(N \log N)$ (LeetCode 300)
