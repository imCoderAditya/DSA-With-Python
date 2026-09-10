# Topic 01: Arrays, Strings, Two Pointers & Sliding Window - Optimal Solutions

---

## 📌 Index of Solutions
1. [Maximum Subarray Sum (Kadane's Algorithm)](#1-maximum-subarray-sum-kadanes-algorithm)
2. [Two Sum II - Input Array Is Sorted](#2-two-sum-ii---input-array-is-sorted)
3. [Container With Most Water](#3-container-with-most-water)
4. [Longest Substring Without Repeating Characters](#4-longest-substring-without-repeating-characters)
5. [Sort Colors (Dutch National Flag Algorithm)](#5-sort-colors-dutch-national-flag-algorithm)
6. [3Sum (Three Pointer Technique)](#6-3sum)
7. [Trapping Rain Water (Two Pointers)](#7-trapping-rain-water)

---

### 1. Maximum Subarray Sum (Kadane's Algorithm)

#### 💡 Intuition & Approach
Kadane's Algorithm tracks the maximum subarray ending at the current index.
- If the running sum becomes negative, starting fresh from the current number is better.
- Recurrence: `current_max = max(num, current_max + num)`.

#### 💻 Python Solution
```python
from typing import List

def max_sub_array(nums: List[int]) -> int:
    max_so_far = nums[0]
    current_max = nums[0]
    
    for num in nums[1:]:
        current_max = max(num, current_max + num)
        max_so_far = max(max_so_far, current_max)
        
    return max_so_far
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Single pass through the array.
- **Space Complexity:** $O(1)$ — Only two scalar variables used.

---

### 2. Two Sum II - Input Array Is Sorted

#### 💡 Intuition & Approach
Since the array is sorted in ascending order, we place two pointers: `left` at the start and `right` at the end.
- If `sum == target`: return indices.
- If `sum < target`: we need a larger sum, so move `left += 1`.
- If `sum > target`: we need a smaller sum, so move `right -= 1`.

#### 💻 Python Solution
```python
from typing import List

def two_sum_sorted(numbers: List[int], target: int) -> List[int]:
    left, right = 0, len(numbers) - 1
    
    while left < right:
        curr_sum = numbers[left] + numbers[right]
        if curr_sum == target:
            return [left + 1, right + 1]  # 1-indexed
        elif curr_sum < target:
            left += 1
        else:
            right -= 1
            
    return []
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Each step eliminates at least one element.
- **Space Complexity:** $O(1)$ — In-place two pointers.

---

### 3. Container With Most Water

#### 💡 Intuition & Approach
The volume of water between two lines is limited by the **shorter line**:
$$\text{Area} = \min(\text{height}[L], \text{height}[R]) \times (R - L)$$
Moving the taller line inward can never increase the area because width decreases and height is bounded by the shorter line. Therefore, always move the shorter line inward.

#### 💻 Python Solution
```python
from typing import List

def max_area(height: List[int]) -> int:
    left, right = 0, len(height) - 1
    max_water = 0
    
    while left < right:
        width = right - left
        h = min(height[left], height[right])
        max_water = max(max_water, width * h)
        
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
            
    return max_water
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### 4. Longest Substring Without Repeating Characters

#### 💡 Intuition & Approach
We maintain a dynamic sliding window `[left ... right]` and store the last seen index of each character in a dictionary `char_map`.
When a character `s[right]` repeats within the current window (`char_map[ch] >= left`), we jump `left = char_map[ch] + 1`.

#### 💻 Python Solution
```python
from typing import Dict

def length_of_longest_substring(s: str) -> int:
    char_map: Dict[str, int] = {}
    left = 0
    max_len = 0
    
    for right, ch in enumerate(s):
        if ch in char_map and char_map[ch] >= left:
            left = char_map[ch] + 1
        char_map[ch] = right
        max_len = max(max_len, right - left + 1)
        
    return max_len
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Each character is visited at most twice.
- **Space Complexity:** $O(\min(N, \Sigma))$ — Where $\Sigma$ is the alphabet size (e.g. 128 for ASCII).

---

### 5. Sort Colors (Dutch National Flag Algorithm)

#### 💡 Intuition & Approach
We partition the array into 4 zones using 3 pointers:
- `nums[0 ... low-1]` $\to 0$ (Red)
- `nums[low ... mid-1]` $\to 1$ (White)
- `nums[mid ... high]` $\to$ Unsorted
- `nums[high+1 ... end]` $\to 2$ (Blue)

#### 💻 Python Solution
```python
from typing import List

def sort_colors(nums: List[int]) -> None:
    low, mid, high = 0, 0, len(nums) - 1
    
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:  # nums[mid] == 2
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$ — Single pass.
- **Space Complexity:** $O(1)$ — In-place.

---

### 6. 3Sum

#### 💡 Intuition & Approach
1. Sort the array.
2. Iterate `i` from $0$ to $N-3$. If `nums[i] > 0`, break (no 3 positive numbers sum to 0).
3. Skip duplicate elements for `i`.
4. Use Two Pointers `left = i + 1`, `right = N - 1` to find pairs that sum to `-nums[i]`.
5. Skip duplicates for `left` and `right`.

#### 💻 Python Solution
```python
from typing import List

def three_sum(nums: List[int]) -> List[List[int]]:
    nums.sort()
    res = []
    n = len(nums)
    
    for i in range(n - 2):
        if nums[i] > 0:
            break
        if i > 0 and nums[i] == nums[i - 1]:
            continue
            
        left, right = i + 1, n - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                res.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1
                
    return res
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(1)$ extra memory.

---

### 7. Trapping Rain Water

#### 💡 Intuition & Approach
Using two pointers (`left` and `right`) and tracking `left_max` and `right_max`:
- Water trapped on current position depends on $\min(\text{left\_max}, \text{right\_max}) - \text{height}[i]$.
- If `left_max < right_max`, water is bounded by `left_max`, so calculate for `left` and increment `left`.
- Else, calculate for `right` and decrement `right`.

#### 💻 Python Solution
```python
from typing import List

def trap(height: List[int]) -> int:
    if not height:
        return 0
        
    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    water = 0
    
    while left < right:
        if left_max < right_max:
            left += 1
            left_max = max(left_max, height[left])
            water += left_max - height[left]
        else:
            right -= 1
            right_max = max(right_max, height[right])
            water += right_max - height[right]
            
    return water
```

#### ⏱️ Complexity Analysis
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
