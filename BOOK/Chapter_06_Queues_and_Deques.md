# 📖 Chapter 6: Queues & Deques (Complete Master Guide)
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Detailed Theory & Core Intuition

### **What is a Queue?**
A **Queue** is a linear data structure that operates strictly on the **First-In, First-Out (FIFO)** principle. The element that enters the queue first is always the first one to be serviced and removed.

Think of a real-world line of people at an airport boarding gate or a supermarket checkout counter:
- New passengers join at the back of the line (**Enqueue**).
- Passengers at the front of the line board first and leave (**Dequeue**).

```
Visual Architecture of a Queue:

               Dequeue (Front)                           Enqueue (Rear)
         ◄─── [ 10 | 20 | 30 | 40 | 50 ] ◄───
                ▲                    ▲
              Front                 Rear
```

---

## 🏗️ 2. Queue Abstract Data Type (ADT) & Complexities

| Operation | Mathematical Definition | Time Complexity | Space Complexity |
|---|---|---|---|
| **`enqueue(x)`** | Inserts element $x$ at the rear of the queue | **$O(1)$** | $O(1)$ |
| **`dequeue()`** | Removes and returns the frontmost element | **$O(1)$** | $O(1)$ |
| **`front()` / `peek()`** | Views the frontmost element without removing | **$O(1)$** | $O(1)$ |
| **`is_empty()`** | Checks if the queue has 0 elements | **$O(1)$** | $O(1)$ |

---

## ⚠️ 3. The Naive Array Trap & The Circular Queue Solution

### **The Naive Array Problem:**
If you implement a queue with a standard array and increment `front` on `dequeue()`, empty slots accumulate at the beginning of the array. Even if total capacity is 100, you will get an "Overflow" error when `rear` reaches the end!

### **The Circular Queue (Ring Buffer) Solution:**
A **Circular Queue** connects the end of the array back to the beginning using **Modulo Arithmetic ($\%$)**:

```
Circular Queue of Capacity N = 5:

Index:     0       1       2       3       4
Array:  [ 40   |  50   |  --   |  20   |  30   ]
                  ▲               ▲
                 Rear           Front

Formulas:
- Next Rear Position:  rear = (rear + 1) % Capacity
- Next Front Position: front = (front + 1) % Capacity
- Full Condition:      (rear + 1) % Capacity == front
- Empty Condition:     front == -1 (or size == 0)
```

---

## 🔁 4. Deque (Double-Ended Queue)

A **Deque** (pronounced *"deck"*) allows insertions and deletions in $O(1)$ time at **both ends** (Front and Rear).

```
               ┌─────────────────────────────┐
Push Front ──► │                             │ ◄── Push Back
Pop Front  ◄── │  [ 10 | 20 | 30 | 40 | 50 ] │ ──► Pop Back
               └─────────────────────────────┘
```

In Python, `collections.deque` is implemented internally as a doubly linked list of fixed-size blocks (64 elements per block), providing **true $O(1)$ append, appendleft, pop, and popleft** without dynamic array copying overhead!

---

## 💡 5. Deep Master Examples & Step-by-Step Walkthroughs

---

### 🌟 Example 1: CPU Task Scheduling & Print Queue Simulation
- **Scenario**: 3 print jobs arrive: `Job_A (3 pages)`, `Job_B (10 pages)`, `Job_C (1 page)`.
- Queue: `[Job_A, Job_B, Job_C]`.
- Printer dequeues `Job_A`, prints 3 pages. Dequeues `Job_B`, prints 10 pages. Dequeues `Job_C`.
- **FIFO ensures fairness** (no starvation).

---

### 🌟 Example 2: Implementing a FIFO Queue using Two LIFO Stacks (Amortized $O(1)$)
- **Setup**: `in_stack = []` (for `enqueue`) and `out_stack = []` (for `dequeue`).
- **Trace**:
  1. `enqueue(1)` $\implies \text{in\_stack} = [1]$
  2. `enqueue(2)` $\implies \text{in\_stack} = [1, 2]$
  3. `enqueue(3)` $\implies \text{in\_stack} = [1, 2, 3]$
  4. `dequeue()`: `out_stack` is empty $\implies$ Transfer all elements from `in_stack` to `out_stack` by popping:
     - `out_stack = [3, 2, 1]` (Reverses the order!)
     - Pop from `out_stack` $\implies$ returns **1**! (FIFO order preserved!).
  5. `dequeue()`: `out_stack` has `[3, 2]` $\implies$ returns **2** in instant **$O(1)$**!

---

### 🌟 Example 3: Circular Buffer Ring Simulation
- Capacity $= 4$.
  - Enqueue 10, 20, 30, 40 $\implies \text{Array} = [10, 20, 30, 40]$, `front=0, rear=3`.
  - Dequeue 10, 20 $\implies \text{Array} = [-, -, 30, 40]$, `front=2, rear=3`.
  - Enqueue 50: `rear = (3 + 1) % 4 = 0` $\implies \text{Array} = [50, -, 30, 40]$, `rear=0`.
  - Enqueue 60: `rear = (0 + 1) % 4 = 1` $\implies \text{Array} = [50, 60, 30, 40]$, `rear=1`.
- **Zero wasted memory!**

---

### 🌟 Example 4: Sliding Window Maximum using Monotonic Deque (LeetCode 239 - Hard)
- **Input**: `nums = [1, 3, -1, -3, 5, 3, 6, 7]`, `k = 3`
- Maintain a deque of indices with values in strictly decreasing order:
  - $i=0 (\text{val } 1)$: `deque = [0]`
  - $i=1 (\text{val } 3)$: $3 > 1 \implies$ pop 0. `deque = [1]`
  - $i=2 (\text{val } -1)$: `deque = [1, 2]` $\implies$ **Window 1 Max = `nums[1]` = 3**
  - $i=3 (\text{val } -3)$: `deque = [1, 2, 3]` $\implies$ **Window 2 Max = `nums[1]` = 3**
  - $i=4 (\text{val } 5)$: $5 > -3, -1, 3 \implies$ pop all! `deque = [4]` $\implies$ **Window 3 Max = `nums[4]` = 5**
  - $i=5 (\text{val } 3)$: `deque = [4, 5]` $\implies$ **Window 4 Max = `nums[4]` = 5**
  - $i=6 (\text{val } 6)$: $6 > 3, 5 \implies$ pop all! `deque = [6]` $\implies$ **Window 5 Max = `nums[6]` = 6**
  - $i=7 (\text{val } 7)$: $7 > 6 \implies$ pop 6! `deque = [7]` $\implies$ **Window 6 Max = `nums[7]` = 7**
- **Output = `[3, 3, 5, 5, 6, 7]` in $O(N)$ single pass!**

---

## ✍️ 6. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch06_queues_practice.py` and implement:

---

### 🟢 **Problem 6.1: Implement Queue using Stacks (LeetCode 232)**
- **Task**: Implement a FIFO queue using only two LIFO stacks in amortized $O(1)$ time.

---

### 🟡 **Problem 6.2: Design Circular Queue (LeetCode 622)**
- **Task**: Design a fixed-size Circular Queue using an array and modulo arithmetic.

---

### 🔴 **Problem 6.3: Sliding Window Maximum (LeetCode 239)**
- **Task**: Return maximum in every sliding window of size $k$ in **$O(N)$ linear time** using a **Monotonic Deque**.
