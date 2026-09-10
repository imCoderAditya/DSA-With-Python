# 📖 Chapter 20: Advanced Data Structures (Segment & Fenwick Trees)
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. The Range Query & Update Dilemma

---

## 🌲 2. Step-by-Step Advanced Data Structure Examples

---

### 🌟 Example 1: Fenwick Tree (BIT) Point Update & Prefix Query
- **Array**: `[3, 2, -1, 6, 5, 4, -3, 3, 7, 2, 3]` (1-indexed)
- **Query Prefix Sum up to index 7**:
  - Start at $i = 7 (0111_2)$: $\text{total} += \text{BIT}[7]$
  - $i = 7 - (7 \ \& \ -7) = 6 (0110_2)$: $\text{total} += \text{BIT}[6]$
  - $i = 6 - (6 \ \& \ -6) = 4 (0100_2)$: $\text{total} += \text{BIT}[4]$
  - $i = 4 - (4 \ \& \ -4) = 0 \implies$ **Done in 3 steps ($\le \log_2 N$)!**

---

### 🌟 Example 2: Fenwick Tree Range Sum Query $[L, R]$
- To query $\text{sum}(3, 7)$:
  $$\text{sum}(3, 7) = \text{prefix\_query}(7) - \text{prefix\_query}(2)$$
- Computed in $2 \times O(\log N) = \mathbf{O(\log N)}$ time!

---

### 🌟 Example 3: Segment Tree Range Sum Query
- Array: `[1, 3, 5, 7, 9, 11]` ($N = 6$)
- Root `[0...5]` has sum 36. Left child `[0...2]` has sum 9, Right child `[3...5]` has sum 27.
- **Query range $[1, 4]$ (`3 + 5 + 7 + 9 = 24`)**:
  - Disjoint node `[0]`: 0
  - Overlapping segment `[1...2]`: 8
  - Partial segment `[3...4]`: 16
  - Disjoint node `[5]`: 0
  - Result $= 8 + 16 = \mathbf{24}$ in $O(\log N)$!

---

### 🌟 Example 4: Lazy Propagation (Deferred Updates)
- Range update $[0, 5] += 10$:
  - Instead of updating all 6 leaf nodes ($O(N)$), update root node with $+60$ and set `lazy[root] = 10`.
  - When child nodes are queried in future, propagate the lazy value down one level on-demand!
- **Achieves $O(\log N)$ Range Updates!**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch20_advanced_structures_practice.py` to write your code:

- **Problem 20.1**: Range Sum Query - Mutable (LeetCode 307)
- **Problem 20.2**: Count of Smaller Numbers After Self (LeetCode 315 - Hard)
