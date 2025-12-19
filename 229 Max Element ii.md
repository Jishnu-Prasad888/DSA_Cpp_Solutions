Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** [3]

**Example 2:**

**Input:** nums = [1]
**Output:** [1]

**Example 3:**

**Input:** nums = [1,2]
**Output:** [1,2]

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-109 <= nums[i] <= 109`


# Boyer-Moore Majority Vote Algorithm (for n/3)

For this problem, we need an **O(n) time, O(1) space** solution. The standard Boyer-Moore algorithm can be extended for elements appearing more than `n/k` times.

## Key Insight
- There can be **at most 2 elements** that appear more than `⌊ n/3 ⌋` times
- Why? If an element appears more than n/3 times, it occupies more than 1/3 of the array. You can't have 3 such elements because 3 × (n/3 + 1) > n

## Algorithm Steps (Boyer-Moore for n/3)

### Phase 1: Find Candidates (Count votes)
We maintain **two potential candidates** and their counts:
1. Initialize two variables `num1`, `num2` and their counts `count1`, `count2` to 0
2. For each number in the array:
   - If it equals `num1`, increment `count1`
   - Else if it equals `num2`, increment `count2`
   - Else if `count1 == 0`, set `num1` to current number, `count1 = 1`
   - Else if `count2 == 0`, set `num2` to current number, `count2 = 1`
   - Else, decrement both `count1` and `count2`

### Phase 2: Verify Candidates
3. Reset counts to 0
4. Count actual occurrences of `num1` and `num2`
5. Keep only those with count > n/3

## Implementation

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int num1 = INT_MIN, num2 = INT_MIN;
        int count1 = 0, count2 = 0;
        int n = nums.size();
        
        // Phase 1: Find potential candidates
        for(int num : nums) {
            if(num == num1) {
                count1++;
            }
            else if(num == num2) {
                count2++;
            }
            else if(count1 == 0) {
                num1 = num;
                count1 = 1;
            }
            else if(count2 == 0) {
                num2 = num;
                count2 = 1;
            }
            else {
                count1--;
                count2--;
            }
        }
        
        // Phase 2: Verify the candidates
        count1 = 0;
        count2 = 0;
        
        for(int num : nums) {
            if(num == num1) count1++;
            else if(num == num2) count2++;
        }
        
        vector<int> result;
        if(count1 > n/3) result.push_back(num1);
        if(count2 > n/3) result.push_back(num2);
        
        return result;
    }
};
```

## Example Walkthrough

For `nums = [3,2,3]` (n=3, n/3=1):
```
Phase 1:
- num1=3, count1=1
- num1=3, count1=2
- num1=3, count1=1 (decrement)
Result: num1=3

Phase 2:
- Count 3's: 2 occurrences
- 2 > 1 → [3]
```

For `nums = [1,2]` (n=2, n/3=0):
```
Phase 1:
- num1=1, count1=1
- num2=2, count2=1
Phase 2:
- Count 1's: 1 > 0 → keep
- Count 2's: 1 > 0 → keep
Result: [1,2]
```

## Alternative Solutions (for comparison):

### 1. Hash Map (O(n) time, O(n) space)
```cpp
vector<int> majorityElement(vector<int>& nums) {
    unordered_map<int, int> freq;
    vector<int> result;
    int n = nums.size();
    
    for(int num : nums) freq[num]++;
    
    for(auto& [num, count] : freq) {
        if(count > n/3) result.push_back(num);
    }
    
    return result;
}
```

### 2. Sorting (O(n log n) time, O(1) space if sorting in-place)
```cpp
vector<int> majorityElement(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<int> result;
    int n = nums.size();
    int count = 1;
    
    for(int i = 1; i <= n; i++) {
        if(i < n && nums[i] == nums[i-1]) {
            count++;
        } else {
            if(count > n/3) result.push_back(nums[i-1]);
            count = 1;
        }
    }
    
    return result;
}
```

## Why Boyer-Moore is Optimal
- **Time**: O(n) - two passes through the array
- **Space**: O(1) - only using a few variables
- **Single pass** version exists but two-pass is clearer and same complexity

## Common Mistakes to Avoid
1. Not handling the case where only one candidate exists
2. Not verifying candidates after Phase 1
3. Using `else if` instead of `if` when checking for candidate equality
4. Forgetting to initialize candidates with a value that won't appear in the array


## Generalized Solution for n/k

```c++
#include <vector>
#include <unordered_map>
#include <climits>
using namespace std;

class Solution {
public:
    vector<int> majorityElement(vector<int>& nums, int k) {
        // For elements appearing more than n/k times
        int n = nums.size();
        if (n == 0) return {};
        
        // We need at most (k-1) candidates
        vector<int> candidates(k-1, INT_MIN);
        vector<int> counts(k-1, 0);
        
        // Phase 1: Find candidates
        for (int num : nums) {
            bool found = false;
            
            // Check if num matches any candidate
            for (int i = 0; i < k-1; i++) {
                if (candidates[i] == num) {
                    counts[i]++;
                    found = true;
                    break;
                }
            }
            
            if (found) continue;
            
            // Check for empty candidate slot
            for (int i = 0; i < k-1; i++) {
                if (counts[i] == 0) {
                    candidates[i] = num;
                    counts[i] = 1;
                    found = true;
                    break;
                }
            }
            
            if (found) continue;
            
            // Decrease all counts
            for (int i = 0; i < k-1; i++) {
                counts[i]--;
            }
        }
        
        // Phase 2: Verify candidates
        vector<int> finalCounts(k-1, 0);
        for (int num : nums) {
            for (int i = 0; i < k-1; i++) {
                if (candidates[i] == num) {
                    finalCounts[i]++;
                    break;
                }
            }
        }
        
        vector<int> result;
        for (int i = 0; i < k-1; i++) {
            if (finalCounts[i] > n / k) {
                result.push_back(candidates[i]);
            }
        }
        
        return result;
    }
    
    // Wrapper for n/4 case
    vector<int> majorityElement(vector<int>& nums) {
        return majorityElement(nums, 4);
    }
};
```

