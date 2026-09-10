# 📖 Chapter 2: Recursion & Backtracking
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Intuition: What is Recursion?

**Recursion** is a method of solving problems where the solution depends on solutions to smaller instances of the same problem.

### 🌟 Example 1: Factorial of a Number $N!$
- Base Case: if $N = 0 \implies 1$
- Recursive Step: $N! = N \times (N - 1)!$
- Call Stack for $N = 3$:
  - `fact(3)` calls `fact(2)`
  - `fact(2)` calls `fact(1)`
  - `fact(1)` calls `fact(0)` $\implies$ returns $1$
  - Unwinding: $1 \times 1 = 1 \implies 2 \times 1 = 2 \implies 3 \times 2 = 6$.

### 🌟 Example 2: Fibonacci Sequence $F(N)$
- $F(0) = 0, F(1) = 1$
- $F(N) = F(N - 1) + F(N - 2)$
- Creates a binary recursion tree of depth $N \implies O(2^N)$ time complexity!

### 🌟 Example 3: Tower of Hanoi (3 Disks)
- Transfer disks from Peg A to Peg C using Peg B.
- Steps:
  1. Move top 2 disks from A to B using C as auxiliary.
  2. Move disk 3 directly from A to C.
  3. Move top 2 disks from B to C using A as auxiliary.
- Total moves formula: $2^N - 1 = 2^3 - 1 = 7$ moves!

---

## 🌲 2. Backtracking: The State-Space Search

Backtracking incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

### 🌟 Example 1: Generating Subsets of `[1, 2]`
```
Decision Tree:
                        []
                   /          \
            Include 1        Exclude 1
               [1]              []
             /     \          /    \
        Include 2 Exclude 2 Include 2 Exclude 2
          [1,2]     [1]       [2]        []
```
- Final Subsets: `[[], [1], [2], [1, 2]]` (Total $= 2^2 = 4$).

---

### 🌟 Example 2: Generating Permutations of `[1, 2, 3]`
- Position 0: Pick 1 $\implies$ Position 1: Pick 2 $\implies$ Position 2: Pick 3 $\implies$ `[1, 2, 3]`
- Backtrack: Swap to Pick 3 at Pos 1 $\implies$ `[1, 3, 2]`
- Backtrack to Pos 0: Pick 2 $\implies$ `[2, 1, 3]`, `[2, 3, 1]`
- Backtrack to Pos 0: Pick 3 $\implies$ `[3, 1, 2]`, `[3, 2, 1]`
- Total $= 3! = 6$ permutations.

---

### 🌟 Example 3: N-Queens Problem ($4 \times 4$ Board)
- Place 4 queens so none attack each other vertically, horizontally, or diagonally.

```
Solution Walkthrough:
Row 0: Place Q at (0, 1)  [ . Q . . ]
Row 1: Try (1,0) - diagonal conflict with (0,1)!
       Try (1,1) - column conflict with (0,1)!
       Try (1,2) - diagonal conflict with (0,1)!
       Place Q at (1, 3)  [ . . . Q ]
Row 2: Place Q at (2, 0)  [ Q . . . ]
Row 3: Place Q at (3, 2)  [ . . Q . ]
==> VALID 4-QUEENS SOLUTION FOUND!
```

---

### 🌟 Example 4: Sudoku Solver (9x9 Grid)
1. Find the first empty cell `"."`.
2. Try placing digits `'1'` through `'9'`.
3. Check 3 validity rules:
   - Digit not in the same row.
   - Digit not in the same column.
   - Digit not in the same $3 \times 3$ subgrid.
4. If valid, recursively solve remainder of the board.
5. If recursion returns `False`, reset cell to `"."` (Backtrack!) and try the next digit.

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch02_recursion_practice.py` to write your code:

- **Problem 2.1**: Tower of Hanoi
- **Problem 2.2**: Combination Sum (LeetCode 39)
- **Problem 2.3**: Palindrome Partitioning (LeetCode 131)
- **Problem 2.4**: Word Search in 2D Board (LeetCode 79)
