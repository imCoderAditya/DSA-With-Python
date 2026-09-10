# Topic 02: Linked Lists - Optimal Solutions

---

## 📌 Index of Solutions
1. [Reverse Linked List](#1-reverse-linked-list)
2. [Linked List Cycle Detection](#2-linked-list-cycle-detection)
3. [Merge Two Sorted Lists](#3-merge-two-sorted-lists)
4. [Remove N-th Node From End of List](#4-remove-n-th-node-from-end-of-list)
5. [Intersection of Two Linked Lists](#5-intersection-of-two-linked-lists)
6. [Reorder List](#6-reorder-list)

---

### Node Definition
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

---

### 1. Reverse Linked List

#### 💡 Intuition & Approach
Maintain three pointers: `prev` (starts as None), `curr` (starts as head), and `next_temp`. In each step, save `curr.next`, redirect `curr.next = prev`, then shift `prev` and `curr` forward.

#### 💻 Python Solution
```python
def reverse_list(head: Optional[ListNode]) -> Optional[ListNode]:
    prev = None
    curr = head
    
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
        
    return prev
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### 2. Linked List Cycle Detection (Floyd's Tortoise & Hare)

#### 💡 Intuition & Approach
- Fast pointer advances 2 steps; slow pointer advances 1 step.
- If there is a cycle, the relative speed difference of 1 guarantees they will meet within the cycle in $O(N)$ steps.
- If fast reaches `None`, there is no cycle.

#### 💻 Python Solution
```python
def has_cycle(head: Optional[ListNode]) -> bool:
    if not head or not head.next:
        return False
        
    slow, fast = head, head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
            
    return False
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### 3. Merge Two Sorted Lists

#### 💡 Intuition & Approach
Use a `dummy` node to avoid edge-case checks for the new list head. Use a `tail` pointer to attach whichever node has the smaller value. At the end, attach any remaining elements.

#### 💻 Python Solution
```python
def merge_two_lists(list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
    dummy = ListNode(0)
    tail = dummy
    
    while list1 and list2:
        if list1.val <= list2.val:
            tail.next = list1
            list1 = list1.next
        else:
            tail.next = list2
            list2 = list2.next
        tail = tail.next
        
    tail.next = list1 if list1 else list2
    return dummy.next
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N + M)$
- **Space Complexity:** $O(1)$

---

### 4. Remove N-th Node From End of List

#### 💡 Intuition & Approach
Use a dummy node placed before `head`.
1. Move `fast` pointer forward by $n + 1$ steps.
2. Move both `fast` and `slow` together until `fast` reaches `None`.
3. Now `slow.next` is precisely the target node to delete! Skip it via `slow.next = slow.next.next`.

#### 💻 Python Solution
```python
def remove_nth_from_end(head: Optional[ListNode], n: int) -> Optional[ListNode]:
    dummy = ListNode(0, head)
    fast = dummy
    slow = dummy
    
    for _ in range(n + 1):
        fast = fast.next
        
    while fast:
        slow = slow.next
        fast = fast.next
        
    slow.next = slow.next.next
    return dummy.next
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ (One-pass)
- **Space Complexity:** $O(1)$

---

### 5. Intersection of Two Linked Lists

#### 💡 Intuition & Approach
Traverse both lists with pointer `pA` and `pB`. When `pA` reaches the end, redirect to `headB`. When `pB` reaches the end, redirect to `headA`.
- Both pointers travel $(lenA + lenB)$ total steps and meet at the intersection point or both become `None`.

#### 💻 Python Solution
```python
def get_intersection_node(headA: ListNode, headB: ListNode) -> Optional[ListNode]:
    if not headA or not headB:
        return None
        
    pA, pB = headA, headB
    
    while pA != pB:
        pA = pA.next if pA else headB
        pB = pB.next if pB else headA
        
    return pA
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N + M)$
- **Space Complexity:** $O(1)$

---

### 6. Reorder List

#### 💡 Intuition & Approach
1. **Find Middle:** Use slow and fast pointers.
2. **Reverse 2nd Half:** Reverse the sublist starting from `mid.next`.
3. **Merge Halves:** Interleave the first half and reversed second half.

#### 💻 Python Solution
```python
def reorder_list(head: Optional[ListNode]) -> None:
    if not head or not head.next:
        return
        
    # 1. Find middle
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
    # 2. Reverse second half
    prev = None
    curr = slow.next
    slow.next = None  # break the list into two halves
    while curr:
        nxt = curr.next
        curr.next = prev
        prev = curr
        curr = nxt
        
    # 3. Merge two halves (head and prev)
    first, second = head, prev
    while second:
        tmp1, tmp2 = first.next, second.next
        first.next = second
        second.next = tmp1
        first, second = tmp1, tmp2
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
