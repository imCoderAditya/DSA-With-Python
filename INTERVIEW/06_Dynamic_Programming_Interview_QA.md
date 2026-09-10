# 💼 Top Interview Questions & Answers: Dynamic Programming (DP)

---

### Q1: How do you identify if a problem can be solved using Dynamic Programming?
**Answer**:
Check for two mathematical properties:
1. **Optimal Substructure**: The global optimal solution can be constructed from optimal solutions to subproblems (e.g., shortest path from $A$ to $C$ via $B$ consists of shortest path $A \to B$ plus $B \to C$).
2. **Overlapping Subproblems**: Recursive solutions repeatedly compute identical subproblems (e.g., `fib(n-1)` and `fib(n-2)` both compute `fib(n-3)`).
- If subproblems are independent (do not overlap), it is **Divide and Conquer** (like Merge Sort), NOT DP!

---

### Q2: What is the difference between Memoization (Top-Down) and Tabulation (Bottom-Up)?
**Answer**:
- **Memoization (Top-Down)**:
  - Starts with the original large problem and breaks it down recursively.
  - Results are cached in a hash map / array (e.g., `@functools.lru_cache`).
  - *Pros*: Only computes subproblems that are strictly needed.
  - *Cons*: Call stack overhead ($O(N)$ recursion depth limit).
- **Tabulation (Bottom-Up)**:
  - Starts with base cases ($0, 1$) and iteratively fills a table up to $N$.
  - *Pros*: Pure iterative loops (no recursion overhead), enables **State Reduction / Space Optimization** (e.g., $O(N) \to O(1)$ by keeping only the last 2 variables).
  - *Cons*: Computes all table states even if some are unnecessary.

---

### Q3: What is the difference between 0/1 Knapsack and Unbounded Knapsack?
**Answer**:
- **0/1 Knapsack**: Each item can be picked **at most once** (either 0 or 1).
  - When iterating in 1D space-optimized DP table, iterate capacity **backwards ($W \to \text{weight}$)** so the same item is not reused in the same iteration!
- **Unbounded Knapsack**: Each item can be chosen **infinitely many times** (e.g., Coin Change).
  - Iterate capacity **forwards ($\text{weight} \to W$)** so the current item can be included multiple times.

---

### Q4: How does Longest Increasing Subsequence (LIS) achieve $O(N \log N)$ instead of $O(N^2)$?
**Answer**:
- Standard 2D/1D DP compares every pair $(i, j)$ with $j < i \implies O(N^2)$.
- **Patience Sorting ($O(N \log N)$)**:
  - Maintain an array `tails` where `tails[i]` stores the smallest tail value of all increasing subsequences of length $i + 1$.
  - `tails` is guaranteed to be strictly sorted!
  - For each number in the array, use **Binary Search (`bisect_left`)** to locate its position in `tails`:
    - If larger than all elements, append it (increases LIS length).
    - Otherwise, replace the smallest element $\ge x$ (lowers the bar for future candidates).
  - Final answer is `len(tails)`!
