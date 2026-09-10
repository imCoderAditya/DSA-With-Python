# Topic 02: Linked Lists - Practice Problems

---

## 📋 Problem List
1. [Reverse Linked List (LeetCode 206)](#problem-1-reverse-linked-list)
2. [Linked List Cycle Detection (LeetCode 141)](#problem-2-linked-list-cycle-detection)
3. [Merge Two Sorted Lists (LeetCode 21)](#problem-3-merge-two-sorted-lists)
4. [Remove N-th Node From End of List (LeetCode 19)](#problem-4-remove-n-th-node-from-end-of-list)
5. [Intersection of Two Linked Lists (LeetCode 160)](#problem-5-intersection-of-two-linked-lists)
6. [Reorder List (LeetCode 143)](#problem-6-reorder-list)

---

### Node Definition
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

---

### Problem 1: Reverse Linked List
**Difficulty:** Easy | **Tags:** `Linked List`, `Recursion`

#### Description
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

#### Examples
- **Input:** `head = [1, 2, 3, 4, 5]`
- **Output:** `[5, 4, 3, 2, 1]`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ iterative

---

### Problem 2: Linked List Cycle Detection
**Difficulty:** Easy | **Tags:** `Linked List`, `Two Pointers (Tortoise & Hare)`

#### Description
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer.

Return `true` if there is a cycle in the linked list. Otherwise, return `false`.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 3: Merge Two Sorted Lists
**Difficulty:** Easy | **Tags:** `Linked List`, `Recursion`

#### Description
You are given the heads of two sorted linked lists `list1` and `list2`.
Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

#### Target Complexity
- **Time Complexity:** $O(N + M)$
- **Space Complexity:** $O(1)$

---

### Problem 4: Remove N-th Node From End of List
**Difficulty:** Medium | **Tags:** `Linked List`, `Two Pointers`

#### Description
Given the `head` of a linked list, remove the $n^{th}$ node from the end of the list and return its head in **one single pass**.

#### Examples
- **Input:** `head = [1, 2, 3, 4, 5], n = 2`
- **Output:** `[1, 2, 3, 5]`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 5: Intersection of Two Linked Lists
**Difficulty:** Easy | **Tags:** `Linked List`, `Two Pointers`

#### Description
Given the heads of two singly linked-lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return `null`.

#### Target Complexity
- **Time Complexity:** $O(N + M)$
- **Space Complexity:** $O(1)$

---

### Problem 6: Reorder List
**Difficulty:** Medium | **Tags:** `Linked List`, `Two Pointers`, `Stack`

#### Description
You are given the head of a singly linked-list. The list can be represented as:
$L_0 \to L_1 \to \dots \to L_{n-1} \to L_n$

Reorder the list to be on the following form:
$L_0 \to L_n \to L_1 \to L_{n-1} \to L_2 \to L_{n-2} \to \dots$

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
