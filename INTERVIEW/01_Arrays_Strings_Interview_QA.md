# 💼 Top Interview Questions & Answers: Arrays, Strings, Two Pointers & Sliding Window

---

### Q1: What is the difference between an Array and a Python List in terms of memory and performance?
**Answer**:
- In low-level languages (C/C++), an array is a contiguous block of homogeneous elements stored directly by value.
- In Python, a `list` is an array of **pointers/references** to PyObjects. This adds a level of pointer indirection (cache misses) but allows heterogeneous types (`[1, "apple", True]`).
- Python lists dynamically resize with an amortized $O(1)$ append growth pattern (allocating size $0, 4, 8, 16, 24, 32, \dots$).

---

### Q2: How do you identify whether a problem should be solved with Sliding Window vs. Two Pointers vs. Dynamic Programming?
**Answer**:
1. **Sliding Window**:
   - Problem asks for **contiguous** subarray/substring meeting a condition (e.g., "Longest substring without repeating characters", "Minimum window sum $\ge K$").
   - Monotonic property must hold: Expanding window increases/decreases property monotonically.
2. **Two Pointers**:
   - Array is usually **sorted**, or we are pairing elements from opposite ends (e.g., "Two Sum in sorted array", "Container with most water", "Trapping rainwater").
   - Can also be fast/slow pointers for in-place modifications (e.g., "Remove duplicates").
3. **Dynamic Programming**:
   - Subarray/subsequence is **non-contiguous** or requires global optimal choice with overlapping subproblems (e.g., "Longest Increasing Subsequence", "0/1 Knapsack").

---

### Q3: Explain Kadane’s Algorithm. Can it handle arrays with all negative numbers?
**Answer**:
- Kadane's algorithm computes the maximum subarray sum in $O(N)$ time and $O(1)$ space.
- At each index $i$: `current_sum = max(nums[i], current_sum + nums[i])` and `max_sum = max(max_sum, current_sum)`.
- **All-negative numbers**: Yes! If `max_sum` is initialized to `nums[0]` (or `float('-inf')`) rather than `0`, it correctly picks the single largest negative number (e.g., for `[-3, -2, -5]`, answer is `-2`).

---

### Q4: Why does the Dutch National Flag algorithm run in $O(N)$ single pass, and what are its pointers?
**Answer**:
- It partitions an array of 3 distinct values (e.g., 0, 1, 2) in-place with $O(1)$ memory.
- Uses 3 pointers: `low`, `mid`, `high`.
  - `[0 ... low-1]`: 0s
  - `[low ... mid-1]`: 1s
  - `[mid ... high]`: Unknown / Unprocessed
  - `[high+1 ... N-1]`: 2s
- Because `mid` processes one element per step and never re-visits, total operations $\le N \implies O(N)$.
