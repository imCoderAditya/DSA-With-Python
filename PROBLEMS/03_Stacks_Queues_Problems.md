# Topic 03: Stacks & Queues - Practice Problems

---

## 📋 Problem List
1. [Valid Parentheses (LeetCode 20)](#problem-1-valid-parentheses)
2. [Min Stack (LeetCode 155)](#problem-2-min-stack)
3. [Daily Temperatures / Next Greater Element (LeetCode 739)](#problem-3-daily-temperatures)
4. [Evaluate Reverse Polish Notation (LeetCode 150)](#problem-4-evaluate-reverse-polish-notation)
5. [Implement Queue using Stacks (LeetCode 232)](#problem-5-implement-queue-using-stacks)
6. [Sliding Window Maximum (Monotonic Deque - LeetCode 239)](#problem-6-sliding-window-maximum)

---

### Problem 1: Valid Parentheses
**Difficulty:** Easy | **Tags:** `Stack`, `String`

#### Description
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

#### Examples
- **Input:** `s = "()[]{}"` $\to$ **Output:** `True`
- **Input:** `s = "(]"` $\to$ **Output:** `False`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### Problem 2: Min Stack
**Difficulty:** Medium | **Tags:** `Stack`, `Design`

#### Description
Design a stack that supports `push`, `pop`, `top`, and retrieving the minimum element in **constant time $O(1)$**.

Implement the `MinStack` class:
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element val onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

---

### Problem 3: Daily Temperatures (Monotonic Stack)
**Difficulty:** Medium | **Tags:** `Array`, `Stack`, `Monotonic Stack`

#### Description
Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the $i^{th}$ day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0`.

#### Examples
- **Input:** `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`
- **Output:** `[1, 1, 4, 2, 1, 1, 0, 0]`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### Problem 4: Evaluate Reverse Polish Notation (Postfix)
**Difficulty:** Medium | **Tags:** `Array`, `Math`, `Stack`

#### Description
You are given an array of strings `tokens` that represents an arithmetic expression in a Reverse Polish Notation. Evaluate the expression. Return an integer that represents the value of the expression.
Valid operators are `+`, `-`, `*`, and `/`. Division truncates toward zero.

#### Examples
- **Input:** `tokens = ["2", "1", "+", "3", "*"]` $\to$ **Output:** `9` ($((2 + 1) * 3) = 9$)

---

### Problem 5: Implement Queue using Stacks
**Difficulty:** Easy | **Tags:** `Stack`, `Queue`, `Design`

#### Description
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

All operations must achieve amortized $O(1)$ time complexity.

---

### Problem 6: Sliding Window Maximum
**Difficulty:** Hard | **Tags:** `Array`, `Queue`, `Sliding Window`, `Monotonic Queue`

#### Description
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(k)$
