# 📖 Chapter 15: Greedy Algorithms
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Intuition: The Greedy Philosophy

A **Greedy Algorithm** always makes the choice that looks best at the moment (local optimum) in hopes of finding the global optimum.

---

## 📊 2. Detailed Step-by-Step Greedy Examples

---

### 🌟 Example 1: Activity Selection / Non-Overlapping Intervals
- **Intervals**: `[(1, 4), (3, 5), (0, 6), (5, 7), (3, 9), (5, 9), (6, 10), (8, 11), (8, 12), (2, 14), (12, 16)]`
- **Sort by End Time**:
  1. Pick `(1, 4)`: End time = 4.
  2. Skip `(3, 5)`, `(0, 6)` (Starts before 4).
  3. Pick `(5, 7)`: End time = 7.
  4. Skip `(3, 9)`, `(5, 9)`, `(6, 10)`.
  5. Pick `(8, 11)`: End time = 11.
  6. Skip `(8, 12)`, `(2, 14)`.
  7. Pick `(12, 16)`: End time = 16.
- **Maximum Non-Overlapping Activities = 4 `[(1, 4), (5, 7), (8, 11), (12, 16)]`!**

---

### 🌟 Example 2: Fractional Knapsack
- **Items**: 
  - Item A: Val 60, Wt 10 $\implies \text{Ratio} = 6.0$
  - Item B: Val 100, Wt 20 $\implies \text{Ratio} = 5.0$
  - Item C: Val 120, Wt 30 $\implies \text{Ratio} = 4.0$
- **Capacity**: $W = 50$
  1. Pick 100% of Item A: Wt 10, Val 60 $\implies$ Remaining capacity = 40.
  2. Pick 100% of Item B: Wt 20, Val 100 $\implies$ Remaining capacity = 20.
  3. Pick $\frac{20}{30} = \frac{2}{3}$ of Item C: Wt 20, Val $\frac{2}{3} \times 120 = 80$.
- **Max Value = $60 + 100 + 80 = \mathbf{240}$!**

---

### 🌟 Example 3: Gas Station Circular Tour
- **Gas**: `[1, 2, 3, 4, 5]`, **Cost**: `[3, 4, 5, 1, 2]`
- Net gain at each station $= \text{Gas} - \text{Cost} = [-2, -2, -2, +3, +3]$.
- Total Net Sum $= (-2) + (-2) + (-2) + 3 + 3 = 0 \ge 0 \implies$ Solution exists!
- Starting from station 3 (net $+3$), running tank remains $\ge 0$ throughout the loop. **Start Index = 3!**

---

### 🌟 Example 4: Jump Game (Can Reach the End?)
- **Array**: `[2, 3, 1, 1, 4]`
- Maintain `max_reachable` index:
  - $i=0 (\text{val } 2) \implies \text{max\_reachable} = \max(0, 0 + 2) = 2$
  - $i=1 (\text{val } 3) \implies \text{max\_reachable} = \max(2, 1 + 3) = \mathbf{4}$
  - Since $4 \ge \text{last\_index } (4) \implies$ **True (Can reach end!)**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch15_greedy_practice.py` to write your code:

- **Problem 15.1**: Non-overlapping Intervals (LeetCode 435)
- **Problem 15.2**: Gas Station (LeetCode 134)
- **Problem 15.3**: Jump Game II (LeetCode 45)
