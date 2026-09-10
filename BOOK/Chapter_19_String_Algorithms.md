# 📖 Chapter 19: String Matching & Pattern Algorithms
> *Data Structures and Algorithms Made Easy — Python Edition*

---

## 🎯 1. The String Matching Problem

Given a text $T$ (length $N$) and pattern $P$ (length $M$), find all starting indices of $P$ inside $T$.

---

## ⚡ 2. Step-by-Step String Algorithm Examples

---

### 🌟 Example 1: KMP LPS Array Construction
- **Pattern**: `P = "AAACAAAA"`
- Construct Longest Prefix-Suffix (LPS) array:

| Index $i$ | Substring $P[0...i]$ | Proper Prefix = Proper Suffix | LPS[$i$] |
|---|---|---|---|
| 0 | `"A"` | None | 0 |
| 1 | `"AA"` | `"A"` | 1 |
| 2 | `"AAA"` | `"AA"` | 2 |
| 3 | `"AAAC"` | None | 0 |
| 4 | `"AAACA"` | `"A"` | 1 |
| 5 | `"AAACAA"` | `"AA"` | 2 |
| 6 | `"AAACAAA"` | `"AAA"` | 3 |
| 7 | `"AAACAAAA"` | `"AAA"` | 3 |

**LPS Array = `[0, 1, 2, 0, 1, 2, 3, 3]` in $O(M)$ time!**

---

### 🌟 Example 2: KMP Search in Action
- **Text**: `T = "ABABDABACDABABCABAB"`, **Pattern**: `P = "ABABCABAB"`
- Match proceeds until index 4 (`'D'` in text vs `'C'` in pattern mismatch).
- Instead of rewinding text pointer, lookup `LPS[3] = 2` $\implies$ align pattern prefix `"AB"` directly with matching suffix! Total comparisons $= O(N + M)$!

---

### 🌟 Example 3: Rabin-Karp Rolling Hash
- **Text**: `"3141592653589793"`, **Pattern**: `"26"` (hash $= 26 \pmod{13} = 0$)
- Window 1 `"31"`: $31 \pmod{13} = 5$
- Window 2 `"14"`: $((5 - 3 \times 10) \times 10 + 4) \pmod{13} = 14 \pmod{13} = 1$
- Slide in $O(1)$ until encountering `"26"` with matching hash 0!

---

### 🌟 Example 4: Longest Palindromic Substring (Expand Around Center)
- **String**: `s = "babad"`
- Centers (both odd and even lengths):
  - Center at `'a'` (index 1): Expand $\implies$ `"bab"` (Length 3).
  - Center at `'b'` (index 2): Expand $\implies$ `"aba"` (Length 3).
- **Longest Palindrome = `"bab"` (or `"aba"`) in $O(N^2)$ time and $O(1)$ space!**

---

## ✍️ 3. Your Coding Challenge Workbook

Create `YOUR_CODE_PRACTICE/ch19_string_algorithms_practice.py` to write your code:

- **Problem 19.1**: Find the Index of the First Occurrence (LeetCode 28)
- **Problem 19.2**: Longest Happy Prefix (LeetCode 1392 - Hard)
- **Problem 19.3**: Longest Palindromic Substring (LeetCode 5)
