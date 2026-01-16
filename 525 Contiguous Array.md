[Contiguous Array - LeetCode](https://leetcode.com/problems/contiguous-array/description/)

Given a binary array `nums`, return _the maximum length of a contiguous subarray with an equal number of_ `0` _and_ `1`.

**Example 1:**

**Input:** nums = [0,1]
**Output:** 2
**Explanation:** [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.

**Example 2:**

**Input:** nums = [0,1,0]
**Output:** 2
**Explanation:** [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.

**Example 3:**

**Input:** nums = [0,1,1,1,1,1,0,0,0]
**Output:** 6
**Explanation:** [1,1,1,0,0,0] is the longest contiguous subarray with equal number of 0 and 1.

## Brute

```c++
// O(n²) time, O(1) space - Not optimal for large n
int findMaxLength(vector<int>& nums) {
    int maxLen = 0;
    for (int i = 0; i < nums.size(); i++) {
        int count0 = 0, count1 = 0;
        for (int j = i; j < nums.size(); j++) {
            if (nums[j] == 0) count0++;
            else count1++;
            
            if (count0 == count1) {
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }
    return maxLen;
}
```


## Optimal 


```c++
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return 0;
        
        unordered_map<int, int> m; // Stores first occurrence index of each prefix sum
        int prefixSum = 0;
        int maxLength = 0;
        
        // Initialize with prefix sum 0 at index -1
        m[0] = -1;
        
        for (int i = 0; i < n; i++) {
            // Treat 0 as -1 and 1 as +1
            prefixSum += (nums[i] == 0) ? -1 : 1;
            
            // If we've seen this prefix sum before
            if (m.find(prefixSum) != m.end()) {
                // The subarray from m[prefixSum] + 1 to i has equal 0s and 1s
                maxLength = max(maxLength, i - m[prefixSum]);
            } else {
                // Store the first occurrence of this prefix sum
                m[prefixSum] = i;
            }
        }
        
        return maxLength;
    }
};
```


Let me explain the corrected code step by step:

## Core Concept
We want to find the **longest contiguous subarray with equal number of 0s and 1s**.

The trick is: 
- Treat `0` as `-1`
- Treat `1` as `+1`
- Equal number of 0s and 1s means the sum of this transformation = 0

## Key Insight
If the cumulative sum (prefix sum) at index `i` equals the cumulative sum at index `j` (where `j < i`), then the subarray from `j+1` to `i` has equal 0s and 1s.

**Why?**
- Prefix sum at `j`: `sum(0...j)`
- Prefix sum at `i`: `sum(0...i)`
- If they're equal: `sum(0...i) = sum(0...j)`
- Then: `sum(j+1...i) = 0`
- Which means equal number of -1s and +1s → equal number of 0s and 1s

## Code Breakdown

### 1. Initialization
```cpp
if (n == 1) return 0;
unordered_map<int, int> m;
int prefixSum = 0;
int maxLength = 0;
m[0] = -1;
```
- `m[0] = -1`: This is **crucial**. It represents that before we start (at "index -1"), the prefix sum is 0.
- `m` will store: `{prefix_sum_value : first_index_where_it_occurred}`

### 2. Main Loop
```cpp
for (int i = 0; i < n; i++) {
    prefixSum += (nums[i] == 0) ? -1 : 1;
```
For each element:
- If it's 0: add -1 to prefix sum
- If it's 1: add +1 to prefix sum

### 3. Checking for Subarrays
```cpp
if (m.find(prefixSum) != m.end()) {
    maxLength = max(maxLength, i - m[prefixSum]);
} else {
    m[prefixSum] = i;
}
```
Two cases:

**Case 1: We've seen this prefix sum before**
- Example: Prefix sum was 3 at index 2, and now it's 3 again at index 7
- The subarray from index 3 to 7 has sum = 0
- Length = `7 - 2 = 5`
- Update `maxLength` if this is longer

**Case 2: First time seeing this prefix sum**
- Store it in the map: `m[prefixSum] = i`
- We store only the **first occurrence** because we want the longest subarray

## Example Walkthrough

Let's trace `nums = [0,1,0,1]`:

**Initial**: `m[0] = -1`, `prefixSum = 0`, `maxLength = 0`

| i | nums[i] | prefixSum | Action | maxLength |
|---|---------|-----------|--------|-----------|
| 0 | 0 | -1 | First time seeing -1, store m[-1] = 0 | 0 |
| 1 | 1 | 0 | Seen 0 before at index -1, length = 1 - (-1) = 2 | 2 |
| 2 | 0 | -1 | Seen -1 before at index 0, length = 2 - 0 = 2 | 2 |
| 3 | 1 | 0 | Seen 0 before at index -1, length = 3 - (-1) = 4 | 4 |

**Result**: 4

## Visualization

For `nums = [0,1,0,1]`:

```
Index:   -1    0     1     2     3
Array:         [0    1     0     1]
Treat as:      [-1   +1    -1    +1]

Prefix Sums:
At i=-1: sum = 0
At i=0:  sum = 0 + (-1) = -1
At i=1:  sum = -1 + 1 = 0
At i=2:  sum = 0 + (-1) = -1  
At i=3:  sum = -1 + 1 = 0

When prefix sum repeats:
- Sum = 0 at i=-1 and i=1 → subarray [0,1] length = 2
- Sum = 0 at i=-1 and i=3 → subarray [0,1,0,1] length = 4
- Sum = -1 at i=0 and i=2 → subarray [1,0] length = 2
```

## Why This Works

The algorithm finds **all possible subarrays** with equal 0s and 1s efficiently:
1. Subarray starting from beginning: when prefix sum = 0
2. Subarray in the middle: when prefix sum repeats
3. Always finds the longest because we store only first occurrence

## Edge Cases Handled

1. **Empty or single element**: `if (n == 1) return 0`
2. **Starting from index 0**: Handled by `m[0] = -1`
3. **All 0s or all 1s**: No equal subarray except possibly empty
4. **Large arrays**: O(n) time, O(n) space

This is a classic example of using prefix sums with a hashmap to solve subarray problems efficiently!