# Topic 03: Stacks & Queues - Optimal Solutions

---

## 📌 Index of Solutions
1. [Valid Parentheses](#1-valid-parentheses)
2. [Min Stack](#2-min-stack)
3. [Daily Temperatures](#3-daily-temperatures)
4. [Evaluate Reverse Polish Notation](#4-evaluate-reverse-polish-notation)
5. [Implement Queue using Stacks](#5-implement-queue-using-stacks)
6. [Sliding Window Maximum (Monotonic Deque)](#6-sliding-window-maximum)

---

### 1. Valid Parentheses

#### 💡 Intuition & Approach
Use a stack. For every closing parenthesis, check if the stack's top is its matching open parenthesis. If not or if stack is empty, return `False`. At the end, stack must be empty.

#### 💻 Python Solution
```python
def is_valid_parentheses(s: str) -> bool:
    stack = []
    mapping = {")": "(", "}": "{", "]": "["}
    
    for ch in s:
        if ch in mapping:
            top_element = stack.pop() if stack else '#'
            if mapping[ch] != top_element:
                return False
        else:
            stack.append(ch)
            
    return not stack
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### 2. Min Stack

#### 💡 Intuition & Approach
Maintain two parallel stacks:
- `stack`: stores regular values.
- `min_stack`: stores the minimum value seen up to that point.

#### 💻 Python Solution
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        min_val = min(val, self.min_stack[-1] if self.min_stack else val)
        self.min_stack.append(min_val)

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(1)$ for all operations.
- **Space Complexity:** $O(N)$

---

### 3. Daily Temperatures (Monotonic Decreasing Stack)

#### 💡 Intuition & Approach
Store indices in a stack. The stack will maintain temperatures in decreasing order.
When we encounter temperature `T[i]` greater than `T[stack[-1]]`, we found the next warmer day for `stack.pop()`.

#### 💻 Python Solution
```python
from typing import List

def daily_temperatures(temperatures: List[int]) -> List[int]:
    n = len(temperatures)
    ans = [0] * n
    stack = []  # indices
    
    for i, t in enumerate(temperatures):
        while stack and temperatures[stack[-1]] < t:
            prev_idx = stack.pop()
            ans[prev_idx] = i - prev_idx
        stack.append(i)
        
    return ans
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Each index pushed and popped at most once.
- **Space Complexity:** $O(N)$

---

### 4. Evaluate Reverse Polish Notation

#### 💡 Intuition & Approach
Operands go into stack. When operator is found, pop two numbers, apply operation, and push result back.
*Note:* Python division with negative numbers `int(a / b)` truncates toward zero properly.

#### 💻 Python Solution
```python
from typing import List

def eval_rpn(tokens: List[str]) -> int:
    stack = []
    
    for token in tokens:
        if token in "+-*/":
            b = stack.pop()
            a = stack.pop()
            if token == '+': stack.append(a + b)
            elif token == '-': stack.append(a - b)
            elif token == '*': stack.append(a * b)
            elif token == '/': stack.append(int(a / b))  # truncate toward zero
        else:
            stack.append(int(token))
            
    return stack[0]
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### 5. Implement Queue using Stacks

#### 💡 Intuition & Approach
Use `in_stack` for push operations and `out_stack` for pop/peek.
When `out_stack` is empty, pour all elements from `in_stack` to `out_stack` (reversing their order to FIFO).

#### 💻 Python Solution
```python
class MyQueue:
    def __init__(self):
        self.in_stack = []
        self.out_stack = []

    def push(self, x: int) -> None:
        self.in_stack.append(x)

    def pop(self) -> int:
        self._shift()
        return self.out_stack.pop()

    def peek(self) -> int:
        self._shift()
        return self.out_stack[-1]

    def empty(self) -> bool:
        return not self.in_stack and not self.out_stack

    def _shift(self) -> None:
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** Amortized $O(1)$ per operation.
- **Space Complexity:** $O(N)$

---

### 6. Sliding Window Maximum (Monotonic Deque)

#### 💡 Intuition & Approach
Use a double-ended queue `collections.deque` storing indices where values are strictly decreasing:
1. Pop indices outside window `deque[0] <= i - k`.
2. Pop smaller elements from back `nums[deque[-1]] < nums[i]`.
3. Add `i` to back. Window maximum is always `nums[deque[0]]`.

#### 💻 Python Solution
```python
from collections import deque
from typing import List

def max_sliding_window(nums: List[int], k: int) -> List[int]:
    q = deque()  # stores indices
    res = []
    
    for i, n in enumerate(nums):
        # 1. Remove indices outside window
        while q and q[0] <= i - k:
            q.popleft()
            
        # 2. Maintain decreasing order
        while q and nums[q[-1]] < n:
            q.pop()
            
        q.append(i)
        
        # 3. Add to result once first window of size k is formed
        if i >= k - 1:
            res.append(nums[q[0]])
            
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Every element is added and removed from deque at most once.
- **Space Complexity:** $O(k)$ — Deque stores at most $k$ indices.
