# 💼 Top Interview Questions & Answers: Stacks & Queues

---

### Q1: What is a Monotonic Stack/Queue and what problems does it solve?
**Answer**:
- A **Monotonic Stack** maintains its elements in strictly increasing or strictly decreasing order.
- **Why it matters**: It reduces naive $O(N^2)$ pair/span searches to **$O(N)$ linear time** by discarding elements that can no longer serve as candidates.
- **Classic Problems**:
  - Next Greater / Smaller Element
  - Daily Temperatures (LeetCode 739)
  - Largest Rectangle in Histogram (LeetCode 84)
  - Sliding Window Maximum via Monotonic Deque (LeetCode 239)

---

### Q2: How do you design a Min-Stack with $O(1)$ `getMin()` operation?
**Answer**:
- **Method 1 (Two Stacks)**: Keep a main stack `data_stack` and an auxiliary `min_stack`. When pushing $x$, push $\min(x, \text{min\_stack.top()})$ to `min_stack`.
- **Method 2 (Single Stack of Pairs)**: Store tuples `(val, current_min)` directly on the main stack.
- **Method 3 (Mathematical Encoding with $O(1)$ extra space)**: Store $2x - \text{min\_val}$ when a new minimum is encountered to encode the previous minimum.

---

### Q3: How do you implement a Queue using Stacks, and what is the amortized complexity?
**Answer**:
- Use two stacks: `in_stack` (for `push`) and `out_stack` (for `pop`).
- `enqueue(x)`: Push directly to `in_stack` ($O(1)$).
- `dequeue()`: If `out_stack` is empty, pop all items from `in_stack` and push into `out_stack` (reversing order to FIFO), then pop from `out_stack`.
- **Amortized Analysis**: Each element is pushed to `in_stack` once, moved to `out_stack` once, and popped once $\implies$ exactly 3 operations per element $\implies$ **Amortized $O(1)$**.

---

### Q4: Why is `collections.deque` preferred over Python `list` for Queues?
**Answer**:
- `list.pop(0)` takes **$O(n)$ time** because all remaining elements must shift one memory address left in RAM.
- `collections.deque` is a doubly linked list of fixed-size blocks (64 elements per block), allowing **$O(1)$ `popleft()` and `append()`** without reallocation or shifting.
