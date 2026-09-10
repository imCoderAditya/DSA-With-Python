# 💼 Top Interview Questions & Answers: Linked Lists

---

### Q1: Why would you choose a Linked List over an Array? When is an Array better?
**Answer**:
- **Choose Linked List when**:
  - You need frequent insertions and deletions at the beginning or middle ($O(1)$ time given pointer).
  - Total number of elements is unpredictable and RAM is fragmented (no contiguous block needed).
- **Choose Array when**:
  - You need fast random access by index $O(1)$.
  - Cache locality and spatial memory performance matter (contiguous storage leverages CPU L1/L2 caches).
  - Memory overhead is critical (Linked lists spend 50-66% memory on pointers alone).

---

### Q2: How does Floyd's Tortoise & Hare Cycle Detection Algorithm work mathematically?
**Answer**:
- Uses two pointers: `slow` (advances 1 step) and `fast` (advances 2 steps).
- If there is a cycle of length $C$, the relative speed between `fast` and `slow` is $2 - 1 = 1$ step/iteration.
- Fast closes the gap by 1 node each step, guaranteeing they meet inside the cycle in at most $C$ steps.
- **Finding Entrance**: If distance from head to entrance is $L_1$ and distance from entrance to meeting point is $L_2$, then $L_1 = k \cdot C - L_2$. Resetting `slow` to head while keeping `fast` at the meeting point and moving both 1 step at a time guarantees they collide at the exact cycle entrance node.

---

### Q3: How do you reverse a singly linked list in $O(1)$ space without breaking references?
**Answer**:
- Maintain 3 pointers: `prev = None`, `curr = head`, `next_temp = None`.
- In a loop:
  1. `next_temp = curr.next` (Store next node)
  2. `curr.next = prev` (Reverse current pointer)
  3. `prev = curr` (Advance prev)
  4. `curr = next_temp` (Advance curr)
- Return `prev` as the new head.

---

### Q4: What is a Sentinel (Dummy) Node and why is it recommended in FAANG interviews?
**Answer**:
- A dummy node (`dummy = ListNode(0, head)`) sits right before the true `head`.
- **Purpose**: It eliminates special-case branching when operations (insertions, deletions, merges) affect the head node itself. At the end, simply return `dummy.next`.
