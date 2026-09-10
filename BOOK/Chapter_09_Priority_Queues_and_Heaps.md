# 📖 Chapter 9: Priority Queues & Binary Heaps
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Intuition: What is a Priority Queue?

A **Priority Queue** is an Abstract Data Type (ADT) similar to a standard queue, except each element has an associated **priority**. Elements with higher priority are dequeued before elements with lower priority.

A **Binary Heap** is the most efficient data structure used to implement a Priority Queue.

```
Min-Heap (Root is smallest):              Max-Heap (Root is largest):
            [ 2 ]                                     [ 90 ]
          /       \                                 /        \
       [ 5 ]     [ 8 ]                           [ 70 ]    [ 80 ]
       /   \     /                               /    \    /
     [ 9 ] [12] [15]                           [ 30 ] [40][50]
```

### 🔑 The 2 Heap Properties:
1. **Heap Order Property**:
   - In a **Min-Heap**: `Parent <= Left Child` and `Parent <= Right Child`.
   - In a **Max-Heap**: `Parent >= Left Child` and `Parent >= Right Child`.
2. **Shape Property (Complete Binary Tree)**: All levels are completely filled from left to right.

---

## 📦 2. Array Representation of Heaps

Because a binary heap is always a **Complete Binary Tree**, it can be stored directly inside a **flat 1D Array** without any pointers!

```
Tree Form:
             (10) [index 0]
            /    \
 [index 1] (20)  (15) [index 2]
          /  \
[idx 3] (30) (40) [idx 4]

Array Storage:
Index:   0    1    2    3    4
Value: [ 10 | 20 | 15 | 30 | 40 ]
```

### 📐 Index Arithmetic (0-Indexed Array):
For any node at index $i$:
- **Parent Index**: $\lfloor \frac{i - 1}{2} \rfloor$
- **Left Child Index**: $2i + 1$
- **Right Child Index**: $2i + 2$

---

## ⚡ 3. Core Operations & Complexities

| Operation | Description | Time Complexity |
|---|---|---|
| `peek()` / `find_min()` | View top element (root at index 0) | **$O(1)$** |
| `push()` / `insert()` | Append to end + **Sift-Up (Percolate Up)** | **$O(\log n)$** |
| `pop()` / `extract_min()` | Swap root with last element, pop, + **Sift-Down (Percolate Down)** | **$O(\log n)$** |
| `build_heap()` / `heapify()` | Bottom-up heap construction | **$O(n)$** |

### 🧮 Why is `heapify` $O(n)$ instead of $O(n \log n)$?
Nodes near the bottom (leaves) constitute half of the total nodes and require 0 sift-downs. The number of operations is bounded by:
$$\sum_{h=0}^{\log n} \frac{n}{2^{h+1}} \times O(h) = O\left(n \sum_{h=0}^\infty \frac{h}{2^h}\right) = O(2n) = O(n)$$

---

## 🐍 4. Python `heapq` Module Mechanics

Python has a built-in `heapq` module which implements a **Min-Heap by default**:

```python
import heapq

min_heap = []
heapq.heappush(min_heap, 10)
heapq.heappush(min_heap, 5)
heapq.heappush(min_heap, 20)
smallest = heapq.heappop(min_heap)  # Returns 5

# Max-Heap Trick: Store negative values
max_heap = []
heapq.heappush(max_heap, -10)
heapq.heappush(max_heap, -30)
largest = -heapq.heappop(max_heap)  # Returns 30
```

---

## ⚖️ 5. The Two-Heaps Pattern (Finding Stream Median)

To maintain the running median of numbers coming one-by-one:
1. **`max_heap` (stores lower half of numbers)**
2. **`min_heap` (stores upper half of numbers)**

```
             Max-Heap (Lower 50%)       Min-Heap (Upper 50%)
             [1, 3, 5, 8]               [10, 12, 15, 20]
                       ▲                 ▲
                   Max of Lower      Min of Upper
```
- Balance condition: Length difference between heaps $\le 1$.
- Median:
  - If total elements is odd: Root of the larger heap.
  - If total elements is even: Average of roots of both heaps.

---

## ✍️ 6. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch09_heaps_practice.py` to write your code:

---

### **Problem 9.1: Top K Frequent Elements (LeetCode 347)**
- **Task**: Given an integer array `nums` and an integer `k`, return the `k` most frequent elements.
- **Target Complexity**: $O(N \log K)$ using a Min-Heap of size $K$.

---

### **Problem 9.2: Merge K Sorted Lists (LeetCode 23 - Hard)**
- **Task**: You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list.
- **Target Complexity**: Time $O(N \log K)$, Space $O(K)$ where $N$ is total nodes.

---

### **Problem 9.3: Find Median from Data Stream (LeetCode 295 - Hard)**
- **Task**: Design a data structure that supports:
  1. `addNum(num)` - Adds an integer into the data structure.
  2. `findMedian()` - Returns the median of all elements so far.
- **Target Complexity**: `addNum` in $O(\log N)$, `findMedian` in $O(1)$.
