# 📖 Chapter 5: Stacks (Complete Master Guide)
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Detailed Theory & Core Intuition

### **What is a Stack?**
A **Stack** is a linear data structure that operates strictly on the **Last-In, First-Out (LIFO)** (or First-In, Last-Out — FILO) principle. This means the element added most recently is the first one to be removed.

Think of a stack of dinner plates at a buffet:
- You place a clean plate on top of the pile (**Push**).
- You take the topmost plate off the pile (**Pop**).
- You cannot pull a plate from the bottom without disturbing the whole stack.

```
Visual Architecture of a Stack:

        │               │
Push 30 │  ┌─────────┐  │
        │  │   30    │  │ ◄── TOP Pointer (index = len - 1)
Push 20 │  ├─────────┤  │
        │  │   20    │  │
Push 10 │  ├─────────┤  │
        │  │   10    │  │ ◄── BOTTOM (index = 0)
        └──┴─────────┴──┘
```

---

## 🏗️ 2. Stack Abstract Data Type (ADT) & Complexities

A standard Stack ADT provides four fundamental operations, all running in **$O(1)$ constant time**:

| Operation | Mathematical Definition | Time Complexity | Space Complexity |
|---|---|---|---|
| **`push(x)`** | Inserts element $x$ onto the top of the stack | **$O(1)$** | $O(1)$ |
| **`pop()`** | Removes and returns the topmost element | **$O(1)$** | $O(1)$ |
| **`peek()` / `top()`** | Returns the topmost element without removing it | **$O(1)$** | $O(1)$ |
| **`is_empty()`** | Returns `True` if stack has 0 elements, else `False` | **$O(1)$** | $O(1)$ |
| **`size()`** | Returns the number of elements in the stack | **$O(1)$** | $O(1)$ |

---

## ⚙️ 3. Implementation Options: Dynamic Array vs. Linked List

### **Option 1: Array-Based Stack (Python List)**
```python
class ArrayStack:
    def __init__(self):
        self._data = []

    def push(self, val):
        self._data.append(val)  # O(1) amortized

    def pop(self):
        if self.is_empty():
            raise IndexError("Pop from empty stack")
        return self._data.pop() # O(1)

    def peek(self):
        if self.is_empty():
            raise IndexError("Peek from empty stack")
        return self._data[-1]   # O(1)

    def is_empty(self):
        return len(self._data) == 0
```

### **Option 2: Linked-List-Based Stack**
Each node points to the node below it. The `top` pointer always points to the `head` node.
- `push`: Create node, `new_node.next = top`, `top = new_node` ($O(1)$).
- `pop`: Save `top.val`, `top = top.next` ($O(1)$).

---

## 🏔️ 4. The Monotonic Stack Paradigm

A **Monotonic Stack** is a stack where elements are strictly ordered either in:
1. **Monotonically Increasing Order**: Bottom to Top is increasing: `[1, 4, 7, 10]` (Smallest at bottom).
2. **Monotonically Decreasing Order**: Bottom to Top is decreasing: `[10, 7, 4, 1]` (Largest at bottom).

### **Why Is Monotonic Stack So Important in FAANG Interviews?**
Whenever a problem asks for:
- "Find the **Next Greater Element** to the left/right"
- "Find the **Nearest Smaller Element** to the left/right"
- "Find the largest span / range where element $X$ is the minimum/maximum"

A brute force nested loop takes $O(n^2)$ time. A **Monotonic Stack solves it in $O(n)$ linear time** because every element is pushed and popped **at most once**!

---

## 💡 5. Deep Master Examples & Step-by-Step Walkthroughs

---

### 🌟 Example 1: Valid Parentheses Matching (LeetCode 20)
- **Problem**: Given a string `s = "{ [ ( ) ] }"`, determine if brackets are matched and nested correctly.
- **Rules**:
  - Push open brackets `'('`, `'{'`, `'['` to stack.
  - When seeing closing bracket, stack top must match corresponding open bracket, then pop.
- **Trace**:

| Step | Char | Stack State | Action |
|---|---|---|---|
| 1 | `'{'` | `['{']` | Push |
| 2 | `'['` | `['{', '[']` | Push |
| 3 | `'('` | `['{', '[', '(']` | Push |
| 4 | `')'` | `['{', '[']` | Match with top `'('`! Pop. |
| 5 | `']'` | `['{']` | Match with top `'['`! Pop. |
| 6 | `'}'` | `[]` | Match with top `'{'`! Pop. |

Stack is empty at the end $\implies$ **Valid (`True`)!**

---

### 🌟 Example 2: Infix, Prefix, & Postfix Expression Evaluation
- **Infix**: `(3 + 4) * 5` (Requires parentheses and operator precedence)
- **Postfix (Reverse Polish Notation)**: `3 4 + 5 *`
- **Prefix**: `* + 3 4 5`

#### **Evaluating Postfix Expression `"2 3 1 * + 9 -"` Step-by-Step:**
1. Token `2`: Push $\implies [2]$
2. Token `3`: Push $\implies [2, 3]$
3. Token `1`: Push $\implies [2, 3, 1]$
4. Token `*`: Pop 1 (operand 2) and 3 (operand 1) $\implies 3 \times 1 = 3 \implies \text{Push } 3 \implies [2, 3]$
5. Token `+`: Pop 3 and 2 $\implies 2 + 3 = 5 \implies \text{Push } 5 \implies [5]$
6. Token `9`: Push $\implies [5, 9]$
7. Token `-`: Pop 9 and 5 $\implies 5 - 9 = -4 \implies \text{Push } -4 \implies [-4]$
- **Final Result = -4** in a single $O(N)$ pass!

---

### 🌟 Example 3: Next Greater Element (NGE) in $O(N)$
- **Input**: `nums = [4, 5, 2, 25]`
- **Goal**: Find next greater number to the right for each item (or `-1` if none).
- **Trace** (Scanning from right to left with Monotonic Decreasing Stack):
  - Index 3 (`val = 25`): Stack is `[]` $\implies \text{NGE} = -1$. Push 25 $\implies \text{Stack}: [25]$.
  - Index 2 (`val = 2`): Stack top is 25 ($> 2$) $\implies \text{NGE} = 25$. Push 2 $\implies \text{Stack}: [25, 2]$.
  - Index 1 (`val = 5`): Stack top is 2 ($< 5$) $\implies$ Pop 2! Stack top is now 25 ($> 5$) $\implies \text{NGE} = 25$. Push 5 $\implies \text{Stack}: [25, 5]$.
  - Index 0 (`val = 4`): Stack top is 5 ($> 4$) $\implies \text{NGE} = 5$. Push 4 $\implies \text{Stack}: [25, 5, 4]$.
- **Output**: `[5, 25, 25, -1]` in $O(N)$ time!

---

### 🌟 Example 4: Largest Rectangle in Histogram (LeetCode 84 - Hard)
- **Input Heights**: `[2, 1, 5, 6, 2, 3]`
- **Trace using Monotonic Increasing Stack of Indices**:
  - Push index 0 (height 2).
  - At index 1 (height 1): height 1 < 2 $\implies$ pop index 0 (height 2): width $= 1 \implies \text{Area} = 2 \times 1 = 2$. Push index 1.
  - Push index 2 (height 5), Push index 3 (height 6).
  - At index 4 (height 2): height 2 < 6 $\implies$ pop index 3 (height 6): width $= 4 - 2 - 1 = 1 \implies \text{Area} = 6 \times 1 = 6$.
  - Pop index 2 (height 5): width $= 4 - 1 - 1 = 2 \implies \text{Area} = 5 \times 2 = \mathbf{10}$.
  - Push index 4 (height 2), Push index 5 (height 3).
- **Maximum Area = 10!**

---

## ⚠️ 6. Top Interview Traps & Pitfalls

1. **Pop from Empty Stack**: Always check `if not stack:` before calling `stack.pop()` or accessing `stack[-1]`.
2. **Order of Operands in Non-Commutative Operations**:
   When evaluating expressions with `-` or `/`:
   `op2 = stack.pop()`
   `op1 = stack.pop()`
   `result = op1 - op2` (NOT `op2 - op1`!).
3. **Designing $O(1)$ Min Stack**:
   Do not search the stack for minimum! Store pairs `(value, current_minimum)` or maintain an auxiliary `min_stack`.

---

## ✍️ 7. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch05_stacks_practice.py` and implement:

---

### 🟢 **Problem 5.1: Valid Parentheses (LeetCode 20)**
- **Task**: Determine if a string of brackets is valid. Time $O(N)$, Space $O(N)$.

---

### 🟡 **Problem 5.2: Min Stack with $O(1)$ Minimum (LeetCode 155)**
- **Task**: Design a stack supporting `push`, `pop`, `top`, and `getMin` all in **$O(1)$ time**.

---

### 🟡 **Problem 5.3: Next Greater Element (LeetCode 496 / 503)**
- **Task**: Find next greater elements using a **Monotonic Stack** in $O(N)$ time.

---

### 🔴 **Problem 5.4: Largest Rectangle in Histogram (LeetCode 84)**
- **Task**: Return the largest rectangular area in a histogram in $O(N)$ time.
