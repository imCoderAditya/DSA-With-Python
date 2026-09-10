# Topic 06: Dynamic Programming - Practice Problems

---

## 📋 Problem List
1. [Climbing Stairs (LeetCode 70)](#problem-1-climbing-stairs)
2. [Coin Change (LeetCode 322)](#problem-2-coin-change)
3. [Longest Increasing Subsequence (LeetCode 300)](#problem-3-longest-increasing-subsequence)
4. [0/1 Knapsack Problem](#problem-4-01-knapsack-problem)
5. [Longest Common Subsequence (LeetCode 1143)](#problem-5-longest-common-subsequence)
6. [Word Break (LeetCode 139)](#problem-6-word-break)
7. [House Robber (LeetCode 198)](#problem-7-house-robber)

---

### Problem 1: Climbing Stairs
**Difficulty:** Easy | **Tags:** `Math`, `Dynamic Programming`, `Memoization`

#### Description
You are climbing a staircase. It takes `n` steps to reach the top.
Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 2: Coin Change
**Difficulty:** Medium | **Tags:** `Array`, `Dynamic Programming`, `BFS`

#### Description
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.
Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

#### Target Complexity
- **Time Complexity:** $O(N \times \text{amount})$
- **Space Complexity:** $O(\text{amount})$

---

### Problem 3: Longest Increasing Subsequence (LIS)
**Difficulty:** Medium | **Tags:** `Array`, `Binary Search`, `Dynamic Programming`

#### Description
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

#### Target Complexity
- **Time Complexity:** $O(N \log N)$ with Binary Search (Patience Sorting) or $O(N^2)$ DP.
- **Space Complexity:** $O(N)$

---

### Problem 4: 0/1 Knapsack Problem
**Difficulty:** Medium | **Tags:** `Dynamic Programming`

#### Description
Given `weights` and `values` of `n` items, put these items in a knapsack of capacity `W` to get the maximum total value in the knapsack. You cannot break an item (either take it completely or leave it).

---

### Problem 5: Longest Common Subsequence (LCS)
**Difficulty:** Medium | **Tags:** `String`, `Dynamic Programming`

#### Description
Given two strings `text1` and `text2`, return the length of their longest common subsequence. If there is no common subsequence, return `0`.

---

### Problem 6: Word Break
**Difficulty:** Medium | **Tags:** `Hash Table`, `String`, `Dynamic Programming`, `Trie`

#### Description
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.
