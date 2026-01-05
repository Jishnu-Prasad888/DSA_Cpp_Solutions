Length of the longest subarray with zero Sum

**Problem Statement:** Given an array containing both positive and negative integers, we have to find the length of the longest subarray with the sum of all elements equal to zero.

**Examples**

**Example 1:****Input:** N = 6, array[] = {9, -3, 3, -1, 6, -5}  
**Result:** 5  
**Explanation:** The following subarrays sum to zero:
- {-3, 3}
- {-1, 6, -5}
- {-3, 3, -1, 6, -5}
The length of the longest subarray with sum zero is 5.

**Example 2:****Input:** N = 8, array[] = {6, -2, 2, -8, 1, 7, 4, -10}  
**Result:** 8  
**Explanation:** Subarrays with sum zero:
- {-2, 2}
- {-8, 1, 7}
- {-2, 2, -8, 1, 7}
- {6, -2, 2, -8, 1, 7, 4, -10}
The length of the longest subarray with sum zero is 8.

## Brute Force

```c++
int maxLen(vector<int>& arr) {
    int n = arr.size();
    int maxLength = 0;
    
    // Check all possible subarrays
    for(int i = 0; i < n; i++) {
        int sum = 0;
        for(int j = i; j < n; j++) {
            sum += arr[j];
            
            // If sum becomes 0, update maxLength
            if(sum == 0) {
                maxLength = max(maxLength, j - i + 1);
            }
        }
    }
    
    return maxLength;
}
```
  

## Optimal Approach


```c++
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;

int maxLen(vector<int>& arr) {
    int n = arr.size();
    int maxLength = 0;
    int sum = 0;
    
    // Map to store first occurrence of each prefix sum
    unordered_map<int, int> prefixSumMap;
    
    for(int i = 0; i < n; i++) {
        sum += arr[i];
        
        // Case 1: Current prefix sum is 0
        if(sum == 0) {
            maxLength = i + 1;  // Subarray from index 0 to i
        }
        else {
            // Case 2: Check if this prefix sum has been seen before
            if(prefixSumMap.find(sum) != prefixSumMap.end()) {
                // If seen, subarray from (previous index + 1) to i has sum 0
                int prevIndex = prefixSumMap[sum];
                maxLength = max(maxLength, i - prevIndex);
            }
            else {
                // Store first occurrence of this prefix sum
                prefixSumMap[sum] = i;
            }
        }
    }
    
    return maxLength;
}
```

