

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array `nums`, find the subarray with the largest sum, and return _its sum_.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1
**Explanation:** The subarray [1] has the largest sum 1.

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`



### Brute 

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0];
        int currentSum = nums[0];
        
        for(int i = 1; i < nums.size(); i++) {
            // Either extend the previous subarray or start fresh
            currentSum = max(nums[i], currentSum + nums[i]);
            // Keep track of maximum sum seen so far
            maxSum = max(maxSum, currentSum);
        }
        
        return maxSum;
    }
};
```

## Better : 

```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to find maximum sum of subarrays
    int maxSubArray(vector<int>& nums) {
        
        /* Initialize maximum sum with
        the smallest possible integer*/
        int maxi = INT_MIN; 

        // Iterate over each starting index of subarrays
        for (int i = 0; i < nums.size(); i++) {
            
            /* Variable to store the sum
            of the current subarray*/
            int sum = 0; 
            
            /* Iterate over each ending index
            of subarrays starting from i*/
            for (int j = i; j < nums.size(); j++) {
                
                /* Add the current element nums[j] to
                the sum i.e. sum of nums[i...j-1]*/
                sum += nums[j];

                /* Update maxi with the maximum of its current
                value and the sum of the current subarray*/
                maxi = max(maxi, sum);
            }
        }

        // Return the maximum subarray sum found
        return maxi;
    }
};

int main() {
    vector<int> arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

    // Create an instance of Solution class
    Solution sol;

    int maxSum = sol.maxSubArray(arr);

    // Print the max subarray sum
    cout << "The maximum subarray sum is: " << maxSum << endl;

    return 0;
}
```

## Optimal

**My Approach**

```c++
#include <vector>
#include <algorithm>
#include <climits>  // For INT_MIN
using namespace std;
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_sum = INT_MIN;
        int sum = 0;
        for(int i = 0 ; i < nums.size() ; i++){
            sum = sum + nums[i];
            if(sum<0) {
                sum = 0;
            }
            if(sum > 0){
                max_sum = max(max_sum,sum);
            }
        }
        sort(nums.begin(),nums.end());
        if(max_sum == INT_MIN){
            return nums[nums.size() - 1];
        }
        else {
        return max_sum ;
        }
    }
};
```



**Best One** : 

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0];
        int currentSum = nums[0];
        
        for(int i = 1; i < nums.size(); i++) {
            // Either extend the previous subarray or start fresh
            currentSum = max(nums[i], currentSum + nums[i]);
            // Keep track of maximum sum seen so far
            maxSum = max(maxSum, currentSum);
        }
        
        return maxSum;
    }
};
```

