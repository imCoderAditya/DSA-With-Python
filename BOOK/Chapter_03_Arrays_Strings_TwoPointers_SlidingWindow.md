# 📖 Chapter 3: Arrays, Strings, Two Pointers & Sliding Window
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Fundamental Concepts: Contiguous Memory & Layout

An **Array** is a collection of items stored at **contiguous memory locations**.

### 🌟 Example 1: Address Calculation in Memory
- Base address = `2000`, integer size = 4 bytes.
- $\text{Address}(arr[3]) = 2000 + 3 \times 4 = \mathbf{2012}$.
- Instant $O(1)$ RAM access via offset calculation!

---

## 🔄 2. Pattern 1: The Two Pointers Technique

---

### 🌟 Example 1: Two Sum II (Sorted Array)
- **Input**: `nums = [2, 7, 11, 15]`, `target = 9`
- `left = 0 (val 2)`, `right = 3 (val 15)`:
  - $\text{sum} = 2 + 15 = 17 > 9 \implies$ Need smaller sum, decrement `right = 2`.
  - $\text{sum} = 2 + 11 = 13 > 9 \implies$ Decrement `right = 1`.
  - $\text{sum} = 2 + 7 = 9 == 9 \implies$ **Found at indices `[0, 1]`!**

---

### 🌟 Example 2: Container With Most Water
- **Input**: `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`
- $L = 1 (\text{height } 8), R = 8 (\text{height } 7)$:
  - $\text{Width} = 8 - 1 = 7$, $\text{Height} = \min(8, 7) = 7 \implies \text{Area} = 7 \times 7 = 49$.
  - Move the shorter bar ($R = 8 \to 7$) to search for a potentially taller bar.

---

### 🌟 Example 3: Trapping Rain Water (Two Pointers)
- **Input**: `height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`
- Maintain `left_max` and `right_max`:
  - If `left_max < right_max`: water trapped at $L = \text{left\_max} - \text{height}[L]$. Advance $L$.
  - Else: water trapped at $R = \text{right\_max} - \text{height}[R]$. Advance $R$.
- Total water trapped = **6 units** in $O(N)$ single pass and $O(1)$ extra space!

---

### 🌟 Example 4: Remove Duplicates from Sorted Array In-Place
- **Input**: `nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]`
- `slow = 0`, `fast` iterates from `1` to `len(nums) - 1`:
  - When `nums[fast] != nums[slow]`: `slow += 1`, `nums[slow] = nums[fast]`.
- Array modified in-place to `[0, 1, 2, 3, 4, ...]` in $O(N)$ time and $O(1)$ space.

---

## 🪟 3. Pattern 2: The Sliding Window Technique

---

### 🌟 Example 1: Maximum Sum Subarray of Fixed Size $K = 3$
- **Array**: `[2, 1, 5, 1, 3, 2]`
- Initial window `[2, 1, 5]`: $\text{sum} = 8$.
- Slide window: $\text{sum} = 8 - 2 + 1 = 7$ (Window `[1, 5, 1]`).
- Slide window: $\text{sum} = 7 - 1 + 3 = 9$ (Window `[5, 1, 3]`). $\implies$ **Max Sum = 9!**

---

### 🌟 Example 2: Longest Substring Without Repeating Characters
- **String**: `s = "abcabcbb"`
- Window expands with `right` and shrinks with `left` using a hash map of last seen indices:
  - `right = 0 ('a')`: Window `"a"`, max_len = 1
  - `right = 1 ('b')`: Window `"ab"`, max_len = 2
  - `right = 2 ('c')`: Window `"abc"`, max_len = 3
  - `right = 3 ('a')`: `'a'` seen at 0 $\implies$ move `left = 1`. Window `"bca"`, max_len = 3.
- **Max length = 3!**

---

## ⚡ 4. Pattern 3: Kadane's Algorithm & Dutch National Flag

---

### 🌟 Example 1: Kadane's Algorithm Walkthrough
- **Array**: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

| Element $x$ | `curr_max = max(x, curr_max + x)` | `max_so_far` | Decision |
|---|---|---|---|
| -2 | -2 | -2 | Start at -2 |
| 1 | $\max(1, -2 + 1) = \mathbf{1}$ | 1 | Discard -2, start fresh |
| -3 | $\max(-3, 1 - 3) = -2$ | 1 | Keep running |
| 4 | $\max(4, -2 + 4) = \mathbf{4}$ | 4 | Start fresh at 4 |
| -1 | $\max(-1, 4 - 1) = 3$ | 4 | Keep running |
| 2 | $\max(2, 3 + 2) = 5$ | 5 | Max increases! |
| 1 | $\max(1, 5 + 1) = 6$ | **6** | Subarray `[4, -1, 2, 1]` |
| -5 | $\max(-5, 6 - 5) = 1$ | 6 | - |
| 4 | $\max(4, 1 + 4) = 5$ | 6 | - |

**Maximum Subarray Sum = 6!**

---

### 🌟 Example 2: Dutch National Flag (Sort 0s, 1s, 2s)
- **Input**: `[2, 0, 2, 1, 1, 0]` with `low = 0, mid = 0, high = 5`
  1. `mid=0 (val 2)`: Swap with `high(5)` $\implies [0, 0, 2, 1, 1, 2]$, `high=4`
  2. `mid=0 (val 0)`: Swap with `low(0)` $\implies [0, 0, 2, 1, 1, 2]$, `low=1, mid=1`
  3. `mid=1 (val 0)`: Swap with `low(1)` $\implies [0, 0, 2, 1, 1, 2]$, `low=2, mid=2`
  4. `mid=2 (val 2)`: Swap with `high(4)` $\implies [0, 0, 1, 1, 2, 2]$, `high=3`
  5. `mid=2 (val 1)`: `mid=3`
  6. `mid=3 (val 1)`: `mid=4 > high` $\implies$ **TERMINATE! Sorted: `[0, 0, 1, 1, 2, 2]`!**

---

## ✍️ 5. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch03_arrays_strings_practice.py` to write your code:

- **Problem 3.1**: 3Sum (LeetCode 15)
- **Problem 3.2**: Container With Most Water (LeetCode 11)
- **Problem 3.3**: Minimum Window Substring (LeetCode 76 - Hard)
- **Problem 3.4**: Rotate Matrix 90° Clockwise In-Place (LeetCode 48)
