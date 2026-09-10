# 📖 Chapter 18: Bit Manipulation
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. Fundamental Bitwise Operators

At the CPU hardware level, bitwise operations execute in **1 CPU clock cycle ($O(1)$)**.

---

## 🧙‍♂️ 2. Step-by-Step Bitwise Examples

---

### 🌟 Example 1: Checking if Number is a Power of 2
- **Rule**: A power of 2 in binary has exactly one `'1'` bit (e.g., $8 = 1000_2, 16 = 10000_2$).
- Notice what happens when subtracting 1:
  $$8 = 1000_2, \quad 7 = 0111_2$$
  $$8 \ \& \ 7 = 1000_2 \ \& \ 0111_2 = \mathbf{0000_2 = 0}$$
- **Formula**: `(n > 0) and (n & (n - 1) == 0)` gives an instant $O(1)$ check!

---

### 🌟 Example 2: Single Number (XOR Cancellation)
- **Input**: `nums = [4, 1, 2, 1, 2]`
- XOR all elements:
  $$4 \oplus 1 \oplus 2 \oplus 1 \oplus 2 = 4 \oplus (1 \oplus 1) \oplus (2 \oplus 2) = 4 \oplus 0 \oplus 0 = \mathbf{4}$$
- All duplicate numbers eliminate each other to `0`, leaving only the unique number in **$O(N)$ time and $O(1)$ space**!

---

### 🌟 Example 3: Single Number III (Finding 2 Unique Numbers)
- **Input**: `nums = [1, 2, 1, 3, 2, 5]` (Unique numbers are 3 and 5).
- XOR of all elements $= 3 \oplus 5 = 0011_2 \oplus 0101_2 = 0110_2 = 6$.
- Find lowest set bit: `diff_bit = 6 & (-6) = 0010_2 = 2`.
- Partition array into 2 groups based on whether the 2nd bit is set:
  - Group 1 (bit is 1): `[2, 3, 2]` $\implies$ XOR $= \mathbf{3}$
  - Group 2 (bit is 0): `[1, 1, 5]` $\implies$ XOR $= \mathbf{5}$
- **Two unique numbers [3, 5] found in $O(N)$ time and $O(1)$ space!**

---

### 🌟 Example 4: Generating All Subsets using Bitmasking
- **Input**: `['A', 'B', 'C']` ($N = 3 \implies 2^3 = 8$ subsets).
- Iterate integer `mask` from $0$ to $7$ ($000_2$ to $111_2$):
  - `mask = 0 (000)`: `[]`
  - `mask = 1 (001)`: `['A']`
  - `mask = 3 (011)`: `['A', 'B']`
  - `mask = 7 (111)`: `['A', 'B', 'C']`

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch18_bit_manipulation_practice.py` to write your code:

- **Problem 18.1**: Single Number (LeetCode 136)
- **Problem 18.2**: Number of 1 Bits (Hamming Weight) (LeetCode 191)
- **Problem 18.3**: Counting Bits (LeetCode 338)
- **Problem 18.4**: Single Number III (Two Unique Numbers) (LeetCode 260)
