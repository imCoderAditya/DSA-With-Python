# 📖 Chapter 13: Searching Algorithms & Binary Search Space
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Linear vs. Binary Search

Searching locates a target value $K$ within a collection.

---

## 🔍 2. Step-by-Step Binary Search Examples

---

### 🌟 Example 1: Standard Binary Search
- **Array**: `[2, 5, 8, 12, 16, 23, 38, 56, 72, 91]`, **Target**: `23`
  - Step 1: `low = 0, high = 9, mid = 4 (val 16)`. $16 < 23 \implies \text{low} = 5$.
  - Step 2: `low = 5, high = 9, mid = 7 (val 56)`. $56 > 23 \implies \text{high} = 6$.
  - Step 3: `low = 5, high = 6, mid = 5 (val 23)`. $23 == 23 \implies$ **Found at index 5 in only 3 steps!**

---

### 🌟 Example 2: Lower Bound vs Upper Bound
- **Array with duplicates**: `[1, 2, 4, 4, 4, 6, 7]`, **Target**: `4`
  - **Lower Bound (`bisect_left`)**: First index where `arr[i] >= 4` $\implies$ **Index 2**.
  - **Upper Bound (`bisect_right`)**: First index where `arr[i] > 4` $\implies$ **Index 5**.
  - Number of occurrences of 4 $= \text{Upper Bound} - \text{Lower Bound} = 5 - 2 = \mathbf{3}$!

---

### 🌟 Example 3: Search in Rotated Sorted Array
- **Array**: `[4, 5, 6, 7, 0, 1, 2]`, **Target**: `0`
  - $L=0 (\text{val } 4), R=6 (\text{val } 2), M=3 (\text{val } 7)$.
  - Left half `[4, 5, 6, 7]` is sorted ($arr[L] \le arr[M]$).
  - Target 0 is NOT between 4 and 7 $\implies$ search in Right half: $L = M + 1 = 4$.
  - $L=4 (\text{val } 0), R=6 (\text{val } 2), M=5 (\text{val } 1)$.
  - $arr[L] == 0 == \text{Target} \implies$ **Found at index 4!**

---

### 🌟 Example 4: Binary Search on Answer Space (Koko Eating Bananas)
- **Piles**: `[3, 6, 7, 11]`, **Max Hours**: `H = 8`
- Search space for eating speed $K \in [1, 11]$:
  - Try $K = 6$: hours $= \lceil 3/6 \rceil + \lceil 6/6 \rceil + \lceil 7/6 \rceil + \lceil 11/6 \rceil = 1 + 1 + 2 + 2 = 6 \le 8$ (Feasible! Try smaller $K$).
  - Try $K = 3$: hours $= 1 + 2 + 3 + 4 = 10 > 8$ (Too slow, increase $K$).
  - Try $K = 4$: hours $= 1 + 2 + 2 + 3 = 8 \le 8$ (Feasible!).
- **Minimum speed $K = 4$ bananas/hour!**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch13_searching_practice.py` to write your code:

- **Problem 13.1**: Search in Rotated Sorted Array (LeetCode 33)
- **Problem 13.2**: Find First and Last Position of Element (LeetCode 34)
- **Problem 13.3**: Koko Eating Bananas (LeetCode 875)
- **Problem 13.4**: Median of Two Sorted Arrays (LeetCode 4 - Hard)
