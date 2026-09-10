# 📖 Chapter 14: Hashing & Hash Tables
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Intuition: What is a Hash Table?

A **Hash Table** maps keys to values for efficient search, insert, and delete operations in **$O(1)$ average time**.

It achieves this by converting a key into an integer array index using a mathematical function called a **Hash Function**:
$$\text{Index} = \text{hash}(\text{key}) \pmod{\text{Capacity}}$$

```
Hash Function Visual:
Key ("Apple")  ──► [ Hash Function: h("Apple") = 2049 ] ──► (2049 % 8 = 1) ──► Slot [1]
```

### 🌟 Example 1: Direct Address Table vs. Hash Table
- **Scenario**: You have 10 employees with IDs from `1` to `10`. You can just use an array of size 10 where `arr[ID]` gives employee details.
- **Problem**: What if employee IDs are 9-digit Social Security Numbers (e.g., `584-92-1049`)? You cannot allocate an array of size $1,000,000,000$ for just 10 employees!
- **Solution**: A Hash Table maps large numbers into a small array of size $M=16$ using $\text{ID} \pmod{16}$.

### 🌟 Example 2: String Hashing (Polynomial Rolling Hash)
- **Keys**: Strings `"cat"`, `"car"`, `"dog"`
- **Formula**: $h(s) = (s[0] \cdot 31^2 + s[1] \cdot 31^1 + s[2] \cdot 31^0) \pmod{100}$
  - For `"cat"` (ASCII: $c=99, a=97, t=116$):
    $$h(\text{"cat"}) = (99 \times 961 + 97 \times 31 + 116) = (95139 + 3007 + 116) = 98262 \pmod{100} = \mathbf{62}$$
  - Placed directly in slot index `62`!

---

## 💥 2. Collision Resolution Strategies

When two distinct keys produce the same array index ($h(k_1) \pmod M = h(k_2) \pmod M$), a **Collision** occurs.

---

### 🌟 Example 1: Separate Chaining (Linked Lists / Buckets)
Suppose table capacity $M = 5$. We insert keys: **12, 22, 15, 25, 37**.
- Hash function: $h(k) = k \pmod 5$

```
Calculations:
- h(12) = 12 % 5 = 2  ==> Bucket 2
- h(22) = 22 % 5 = 2  ==> Collision at Bucket 2! (Add to chain)
- h(15) = 15 % 5 = 0  ==> Bucket 0
- h(25) = 25 % 5 = 0  ==> Collision at Bucket 0! (Add to chain)
- h(37) = 37 % 5 = 2  ==> Collision at Bucket 2! (Add to chain)

Final Hash Table Memory State:
Slot 0: [ 15 ] ──► [ 25 ] ──► None
Slot 1: [ None ]
Slot 2: [ 12 ] ──► [ 22 ] ──► [ 37 ] ──► None
Slot 3: [ None ]
Slot 4: [ None ]
```

---

### 🌟 Example 2: Open Addressing — Linear Probing
- Formula: $h(k, i) = (h(k) + i) \pmod M$ where $i = 0, 1, 2, \dots$
- Let $M = 7$. Insert keys: **10, 17, 24, 31** (all have $k \pmod 7 = 3$).

```
Step-by-step probing:
1. Insert 10: h(10, 0) = 10 % 7 = 3 ==> Slot 3 is EMPTY. Place 10 in Slot [3].
2. Insert 17: h(17, 0) = 3 (COLLISION!)
             h(17, 1) = (3 + 1) % 7 = 4 ==> Slot 4 is EMPTY. Place 17 in Slot [4].
3. Insert 24: h(24, 0) = 3 (COLLISION!)
             h(24, 1) = 4 (COLLISION!)
             h(24, 2) = (3 + 2) % 7 = 5 ==> Slot 5 is EMPTY. Place 24 in Slot [5].
4. Insert 31: h(31, 0) = 3, h(31, 1) = 4, h(31, 2) = 5 (ALL OCCUPIED!)
             h(31, 3) = (3 + 3) % 7 = 6 ==> Place 31 in Slot [6].

Final Array:
Index:   0    1    2    3    4    5    6
Value: [ -  | -  | -  | 10 | 17 | 24 | 31 ]
                      ▲──────────────────▲ (Forms a Cluster!)
```

---

### 🌟 Example 3: Open Addressing — Quadratic Probing
- Formula: $h(k, i) = (h(k) + i^2) \pmod M$
- Avoids primary clustering! If $h(k) = 3$:
  - $i=0 \implies 3$
  - $i=1 \implies (3 + 1) \pmod M = 4$
  - $i=2 \implies (3 + 4) \pmod M = 7 \pmod M$
  - $i=3 \implies (3 + 9) \pmod M = 12 \pmod M$

---

### 🌟 Example 4: Double Hashing
- Formula: $h(k, i) = (h_1(k) + i \cdot h_2(k)) \pmod M$
- Let $M = 7$, $h_1(k) = k \pmod 7$, $h_2(k) = 5 - (k \pmod 5)$.
- If collision occurs at $h_1(k)$, the step size is dictated by a secondary function $h_2(k)$, guaranteeing uniform distribution!

---

## 🔄 3. Load Factor ($\alpha$) & Dynamic Rehashing

$$\text{Load Factor } \alpha = \frac{N (\text{Number of elements stored})}{M (\text{Total table capacity})}$$

### 🌟 Example 1: Rehashing Threshold Walkthrough
- Table starts with capacity $M = 4$.
- Threshold: $\alpha \ge 0.75 \implies \text{Max elements} = 4 \times 0.75 = 3$.
- Insert 1: $N=1, \alpha = 0.25$ (OK)
- Insert 2: $N=2, \alpha = 0.50$ (OK)
- Insert 3: $N=3, \alpha = 0.75$ (OK)
- Insert 4: $N=4, \alpha = 1.0 > 0.75 \implies$ **TRIGGER REHASH!**
  1. Allocate new table with $M = 8$ (doubled).
  2. Recompute $k \pmod 8$ for all existing elements and insert them.

---

## ⚡ 4. Classic Application Examples

---

### 🌟 Example 1: Two Sum with $O(1)$ Hash Map (LeetCode 1)
- **Input**: `nums = [2, 11, 7, 15]`, `target = 9`
- **Trace**:
  1. Index 0 (`num=2`): Need `complement = 9 - 2 = 7`. Map is `{}`. Store `{2: 0}`.
  2. Index 1 (`num=11`): Need `complement = 9 - 11 = -2`. Store `{2: 0, 11: 1}`.
  3. Index 2 (`num=7`): Need `complement = 9 - 7 = 2`. `2` is in map at index `0`!
  - **Return `[0, 2]` in single pass $O(N)$ time!**

---

### 🌟 Example 2: Subarray Sum Equals K (Prefix Sum Hashing)
- **Input**: `nums = [1, 2, 3, -2, 2, 1]`, `k = 3`
- **Formula**: If `prefix_sum[j] - prefix_sum[i] == k`, then subarray `nums[i+1...j]` sums to $k$.
- **Trace**:

| Index | Num | Current Prefix Sum | Needed (`Prefix - k`) | Seen Prefixes Map | Subarrays Found Count |
|---|---|---|---|---|---|
| - | - | 0 | - | `{0: 1}` | 0 |
| 0 | 1 | 1 | $1 - 3 = -2$ | `{0:1, 1:1}` | 0 |
| 1 | 2 | 3 | $3 - 3 = 0$ | `{0:1, 1:1, 3:1}` | +1 (Subarray `[1,2]`) |
| 2 | 3 | 6 | $6 - 3 = 3$ | `{0:1, 1:1, 3:1, 6:1}` | +1 (Subarray `[3]`) |
| 3 | -2 | 4 | $4 - 3 = 1$ | `... 4:1` | +1 (Subarray `[3, -2, 2]` from index 1) |
| 4 | 2 | 6 | $6 - 3 = 3$ | `... 6:2` | +1 (Subarray `[-2, 2, 1]` / `[1, 2]`) |

---

### 🌟 Example 3: LRU Cache State Transitions
- **Capacity = 2**
- `put(1, 1)`: Cache: `[1=1]` (Head $\to$ 1 $\to$ Tail)
- `put(2, 2)`: Cache: `[2=2, 1=1]` (Head $\to$ 2 $\to$ 1 $\to$ Tail)
- `get(1)`: Returns 1. Move 1 to Front: Cache: `[1=1, 2=2]`
- `put(3, 3)`: Capacity full (2)! Evict Least Recently Used (Tail node `2=2`).
  - New Cache: `[3=3, 1=1]`
- `get(2)`: Returns `-1` (Not found!).

---

### 🌟 Example 4: Longest Consecutive Sequence in $O(N)$
- **Input**: `nums = [100, 4, 200, 1, 3, 2]`
- Convert to Set: `{1, 2, 3, 4, 100, 200}`
- **Check starting points** (numbers where `x - 1 not in set`):
  - Is `100` a start? Yes (`99` not in set) $\implies$ streak: `[100]` (length 1).
  - Is `4` a start? No (`3` is in set) $\implies$ skip.
  - Is `200` a start? Yes (`199` not in set) $\implies$ streak: `[200]` (length 1).
  - Is `1` a start? Yes (`0` not in set) $\implies$ streak: `1 -> 2 -> 3 -> 4` (length 4!).
- **Max length = 4!**

---

## ✍️ 5. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch14_hashing_practice.py` to write your code:

- **Problem 14.1**: Group Anagrams (LeetCode 49)
- **Problem 14.2**: Subarray Sum Equals K (LeetCode 560)
- **Problem 14.3**: Design LRU Cache in $O(1)$ (LeetCode 146)
- **Problem 14.4**: Longest Consecutive Sequence in $O(N)$ (LeetCode 128)
