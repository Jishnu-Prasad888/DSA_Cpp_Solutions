Given two sorted arrays **nums1** and **nums2**, return an array that contains the **union** of these two arrays. The elements in the union must be in ascending order.

The union of two arrays is an array where all values are distinct and are present in either the first array, the second array, or both.

Examples:

**Input**: nums1 = [1, 2, 3, 4, 5], nums2 = [1, 2, 7]
**Output**: [1, 2, 3, 4, 5, 7]
**Explanation**:
The elements 1, 2 are common to both, 3, 4, 5 are from nums1 and 7 is from nums2

**Input**: nums1 = [3, 4, 6, 7, 9, 9], nums2 = [1, 5, 7, 8, 8]
**Output**: [1, 3, 4, 5, 6, 7, 8, 9]
**Explanation**:
The element 7 is common to both, 3, 4, 6, 9 are from nums1 and 1, 5, 8 is from nums2

## Using sets

```cpp
#include <vector>
#include <set>
using namespace std;

vector<int> findUnion(vector<int>& nums1, vector<int>& nums2) {
    set<int> unionSet;
    
    // Add all elements from both arrays to set
    for(int num : nums1) {
        unionSet.insert(num);
    }
    for(int num : nums2) {
        unionSet.insert(num);
    }
    
    // Convert set to vector
    return vector<int>(unionSet.begin(), unionSet.end());
}
```


## Two pointers

```cpp
#include <vector>
using namespace std;

vector<int> findUnion(vector<int>& nums1, vector<int>& nums2) {
    vector<int> result;
    int i = 0, j = 0;
    int m = nums1.size(), n = nums2.size();
    
    while(i < m && j < n) {
        if(nums1[i] < nums2[j]) {
            // Add if it's not duplicate
            if(result.empty() || result.back() != nums1[i]) {
                result.push_back(nums1[i]);
            }
            i++;
        } else if(nums1[i] > nums2[j]) {
            // Add if it's not duplicate
            if(result.empty() || result.back() != nums2[j]) {
                result.push_back(nums2[j]);
            }
            j++;
        } else { // Equal elements
            // Add if it's not duplicate
            if(result.empty() || result.back() != nums1[i]) {
                result.push_back(nums1[i]);
            }
            i++;
            j++;
        }
    }
    
    // Add remaining elements from nums1
    while(i < m) {
        if(result.empty() || result.back() != nums1[i]) {
            result.push_back(nums1[i]);
        }
        i++;
    }
    
    // Add remaining elements from nums2
    while(j < n) {
        if(result.empty() || result.back() != nums2[j]) {
            result.push_back(nums2[j]);
        }
        j++;
    }
    
    return result;
}
```

## Using Hashmap

```cpp
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;

vector<int> findUnion(vector<int>& nums1, vector<int>& nums2) {
    unordered_map<int, bool> seen;
    vector<int> result;
    
    // Add all elements from both arrays to hashmap
    for(int num : nums1) {
        seen[num] = true;
    }
    for(int num : nums2) {
        seen[num] = true;
    }
    
    // Extract keys from hashmap
    for(auto& pair : seen) {
        result.push_back(pair.first);
    }
    
    // Sort the result (since hashmap doesn't maintain order)
    sort(result.begin(), result.end());
    
    return result;
}
```


```cpp
#include <vector>
#include <unordered_set>
#include <algorithm>
using namespace std;

vector<int> findUnion(vector<int>& nums1, vector<int>& nums2) {
    unordered_set<int> unionSet;
    
    // Pre-allocate space for better performance
    unionSet.reserve(nums1.size() + nums2.size());
    
    // Insert all elements
    for(int num : nums1) unionSet.insert(num);
    for(int num : nums2) unionSet.insert(num);
    
    // Convert to vector and sort
    vector<int> result;
    result.reserve(unionSet.size());
    result.assign(unionSet.begin(), unionSet.end());
    sort(result.begin(), result.end());
    
    return result;
}
```


