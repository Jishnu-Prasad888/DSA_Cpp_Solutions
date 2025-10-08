
[169. Majority Element](https://leetcode.com/problems/majority-element/)
Easy

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**
**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**
**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

## my approach 

```cpp
#include <map>
#include <algorithm>
#include <cmath>
#include <vector>
using namespace std;

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int size = nums.size();
        int threshold = size / 2;
        vector<int> f = {};
        map<int, int> n = {};
        
        // Count frequency of ALL elements
        for(int i = 0; i < size; i++) {
            n[nums[i]] += 1;
        }
        
        // Find elements with frequency > threshold
        for(auto& pair : n) {
            if(pair.second > threshold) {  // Use > instead of >=
                f.push_back(pair.first);
            }
        }
        
        // Since majority element always exists, return the first one found
        return f[0];
    }
};
```


## O(1) approach 

only works when it is assured that max element exits if not given so use boyer-moore

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());    // Step 1: Sort the array
        return nums[nums.size() / 2];      // Step 2: Return middle element
    }
};
```

#### Step-by-Step Example

**Example 1:** `nums = [3, 2, 3]`

- n = 3, threshold = ⌊3/2⌋ = 1 (needs >1 occurrence)
- After sorting: `[2, 3, 3]`
- Middle index = 3/2 = 1 → `nums[1] = 3` ✓

**Example 2:** `nums = [2, 2, 1, 1, 1, 2, 2]`

- n = 7, threshold = ⌊7/2⌋ = 3 (needs >3 occurrences    
- After sorting: `[1, 1, 1, 2, 2, 2, 2]`
- Middle index = 7/2 = 3 → `nums[3] = 2` 

## Why This Works Mathematically

Let's say:

- Array size = n
- Majority element appears k times, where k > n/2
- After sorting, the majority element occupies a contiguous block

The middle position is at index n/2. Since k > n/2, the block of majority elements must:

- Start before or at position n/2
- End after or at position n/2

## Boyer-moore approach ( Boyer-Moore Voting Algorithm)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = nums[0];
        int count = 1;
        
        for (int i = 1; i < nums.size(); i++) {
            if (count == 0) {
                candidate = nums[i];
                count = 1;
            } else if (nums[i] == candidate) {
                count++;
            } else {
                count--;
            }
        }
        
        return candidate;
    }
};
```


