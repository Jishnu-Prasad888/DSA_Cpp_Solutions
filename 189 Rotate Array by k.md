Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

**Example 1:**

**Input:** nums = [1,2,3,4,5,6,7], k = 3
**Output:** [5,6,7,1,2,3,4]
**Explanation:**
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

**Example 2:**

**Input:** nums = [-1,-100,3,99], k = 2
**Output:** [3,99,-1,-100]
**Explanation:** 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]

## Using STL

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n;
        std::rotate(nums.begin(), nums.begin() + (n - k), nums.end());
    }
};
```


## manual approach my method

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n; // Handle cases where k > n
        
        vector<int> temp(n);
        
        // Copy last k elements to beginning of temp
        for (int i = 0; i < k; i++) {
            temp[i] = nums[n - k + i];
        }
        
        // Copy first n-k elements to remaining positions
        for (int i = 0; i < n - k; i++) {
            temp[k + i] = nums[i];
        }
        
        // Copy back to original array
        nums = temp;
    }
};
```


## Manual Optimal 

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n;
        
        // Reverse entire array
        reverse(nums.begin(), nums.end());
        // Reverse first k elements
        reverse(nums.begin(), nums.begin() + k);
        // Reverse remaining elements
        reverse(nums.begin() + k, nums.end());
    }
};
``


`