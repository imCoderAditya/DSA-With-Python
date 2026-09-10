# Topic 01: Arrays, Strings, Two Pointers & Sliding Window - Practice Problems

---

## 📋 Problem List
1. [Maximum Subarray Sum (Kadane's Algorithm)](#problem-1-maximum-subarray-sum-kadanes-algorithm)
2. [Two Sum II - Input Array Is Sorted (Two Pointers)](#problem-2-two-sum-ii---input-array-is-sorted)
3. [Container With Most Water](#problem-3-container-with-most-water)
4. [Longest Substring Without Repeating Characters (Sliding Window)](#problem-4-longest-substring-without-repeating-characters)
5. [Sort Colors (Dutch National Flag Algorithm)](#problem-5-sort-colors-dutch-national-flag)
6. [3Sum (Three Pointer Technique)](#problem-6-3sum)
7. [Trapping Rain Water](#problem-7-trapping-rain-water)

---

### Problem 1: Maximum Subarray Sum (Kadane's Algorithm)
**Difficulty:** Medium | **Tags:** `Array`, `Dynamic Programming`, `Kadane's`

#### Description
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

#### Examples
- **Example 1:**
  - **Input:** `nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`
  - **Output:** `6`
  - **Explanation:** `[4, -1, 2, 1]` has the largest sum `= 6`.
- **Example 2:**
  - **Input:** `nums = [1]`
  - **Output:** `1`
- **Example 3:**
  - **Input:** `nums = [5, 4, -1, 7, 8]`
  - **Output:** `23`

#### Constraints
- $1 \le \text{nums.length} \le 10^5$
- $-10^4 \le \text{nums}[i] \le 10^4$

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 2: Two Sum II - Input Array Is Sorted
**Difficulty:** Medium | **Tags:** `Array`, `Two Pointers`, `Binary Search`

#### Description
Given a **1-indexed** array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where $1 \le index1 < index2 \le \text{numbers.length}$.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

#### Examples
- **Example 1:**
  - **Input:** `numbers = [2, 7, 11, 15], target = 9`
  - **Output:** `[1, 2]`
  - **Explanation:** The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return `[1, 2]`.
- **Example 2:**
  - **Input:** `numbers = [2, 3, 4], target = 6`
  - **Output:** `[1, 3]`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 3: Container With Most Water
**Difficulty:** Medium | **Tags:** `Array`, `Two Pointers`, `Greedy`

#### Description
You are given an integer array `height` of length $n$. There are $n$ vertical lines drawn such that the two endpoints of the $i^{th}$ line are $(i, 0)$ and $(i, \text{height}[i])$.

Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store.

#### Examples
- **Example 1:**
  - **Input:** `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`
  - **Output:** `49`
  - **Explanation:** The vertical lines are at index 1 (`height=8`) and index 8 (`height=7`). Area = $\min(8, 7) \times (8 - 1) = 7 \times 7 = 49$.

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Problem 4: Longest Substring Without Repeating Characters
**Difficulty:** Medium | **Tags:** `Hash Table`, `String`, `Sliding Window`

#### Description
Given a string `s`, find the length of the longest substring without repeating characters.

#### Examples
- **Example 1:**
  - **Input:** `s = "abcabcbb"`
  - **Output:** `3` (Substring: `"abc"`)
- **Example 2:**
  - **Input:** `s = "bbbbb"`
  - **Output:** `1` (Substring: `"b"`)
- **Example 3:**
  - **Input:** `s = "pwwkew"`
  - **Output:** `3` (Substring: `"wke"`)

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(\min(N, \Sigma))$ where $\Sigma$ is alphabet size.

---

### Problem 5: Sort Colors (Dutch National Flag)
**Difficulty:** Medium | **Tags:** `Array`, `Two Pointers`, `Sorting`

#### Description
Given an array `nums` with $n$ objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red (0), white (1), and blue (2).

You must solve this problem without using the library's sort function and in a single pass with $O(1)$ extra space.

#### Examples
- **Example 1:**
  - **Input:** `nums = [2, 0, 2, 1, 1, 0]`
  - **Output:** `[0, 0, 1, 1, 2, 2]`
- **Example 2:**
  - **Input:** `nums = [2, 0, 1]`
  - **Output:** `[0, 1, 2]`

#### Target Complexity
- **Time Complexity:** $O(N)$ (One-pass)
- **Space Complexity:** $O(1)$

---

### Problem 6: 3Sum
**Difficulty:** Medium | **Tags:** `Array`, `Two Pointers`, `Sorting`

#### Description
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that $i \ne j$, $i \ne k$, and $j \ne k$, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

#### Target Complexity
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(1)$ extra (ignoring output array)

---

### Problem 7: Trapping Rain Water
**Difficulty:** Hard | **Tags:** `Array`, `Two Pointers`, `Dynamic Programming`, `Stack`

#### Description
Given $n$ non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

#### Examples
- **Input:** `height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`
- **Output:** `6`

#### Target Complexity
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
