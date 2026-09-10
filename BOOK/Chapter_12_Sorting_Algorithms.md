# 📖 Chapter 12: Sorting Algorithms
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Classification of Sorting Algorithms

Sorting arranges elements in ascending or descending order.

---

## 📊 2. Detailed Sorting Walkthrough Examples

---

### 🌟 Example 1: Merge Sort Step-by-Step
- **Array**: `[38, 27, 43, 3, 9, 82, 10]`
  1. Divide into `[38, 27, 43, 3]` and `[9, 82, 10]`
  2. Sub-divide down to single elements: `[38]`, `[27]`, `[43]`, `[3]` ...
  3. Merge sorted pairs: `[27, 38]` and `[3, 43]` $\implies [3, 27, 38, 43]$
  4. Merge `[3, 27, 38, 43]` with `[9, 10, 82]` $\implies \mathbf{[3, 9, 10, 27, 38, 43, 82]}$ in $O(N \log N)$ stable time!

---

### 🌟 Example 2: Quick Sort with Lomuto Partition
- **Array**: `[10, 80, 30, 90, 40, 50, 70]` (Pivot = 70 at end)
  - `i = -1`
  - $j=0 (\text{val } 10 \le 70) \implies i=0$, swap `arr[0]` with `arr[0]`
  - $j=1 (\text{val } 80 > 70) \implies$ skip
  - $j=2 (\text{val } 30 \le 70) \implies i=1$, swap `arr[1]` (80) with `arr[2]` (30) $\implies [10, 30, 80, 90, 40, 50, 70]$
  - $j=4 (\text{val } 40 \le 70) \implies i=2$, swap `arr[2]` (80) with `arr[4]` (40) $\implies [10, 30, 40, 90, 80, 50, 70]$
  - Place pivot: Swap `arr[i+1]` (90) with pivot (70) $\implies [10, 30, 40, 50, \mathbf{70}, 80, 90]$ (70 is in its final sorted position!).

---

### 🌟 Example 3: Counting Sort in $O(N + K)$
- **Array**: `[4, 2, 2, 8, 3, 3, 1]` ($K = 8$)
  - Count frequency array: `{1: 1, 2: 2, 3: 2, 4: 1, 8: 1}`
  - Compute prefix positions and place into output array: `[1, 2, 2, 3, 3, 4, 8]` in linear time!

---

### 🌟 Example 4: Radix Sort (LSD)
- **Numbers**: `[170, 45, 75, 90, 802, 24, 2, 66]`
  - Sort by 1s digit: `[170, 90, 802, 2, 24, 45, 75, 66]`
  - Sort by 10s digit: `[802, 2, 24, 45, 66, 170, 75, 90]`
  - Sort by 100s digit: `[2, 24, 45, 66, 75, 90, 170, 802]` $\implies$ **Sorted!**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch12_sorting_practice.py` to write your code:

- **Problem 12.1**: Implement Merge Sort (Stable)
- **Problem 12.2**: Implement Randomized Quick Sort
- **Problem 12.3**: Sort an Array in $O(N)$ using Counting / Radix Sort (LeetCode 912)
