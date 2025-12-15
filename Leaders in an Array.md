**Problem:** Leaders in an Array

You are given an array `arr` of size `n`. An element is considered a **leader** if it is greater than or equal to all the elements to its right. The rightmost element is always a leader.

Return a list of all leaders in the array in the **order they appear** from left to right.

**Examples:**

```
Input: arr = [16, 17, 4, 3, 5, 2]
Output: [17, 5, 2]
Explanation:
- 17 is greater than all elements to its right (4, 3, 5, 2).
- 5 is greater than all elements to its right (2).
- 2 is the rightmost element, so it is always a leader.
```

```
Input: arr = [1, 2, 3, 4, 0]
Output: [4, 0]
Explanation:
- 4 is greater than all elements to its right (0).
- 0 is the rightmost element, so it is always a leader.
```

```
Input: arr = [5, 4, 3, 2, 1]
Output: [5, 4, 3, 2, 1]
Explanation: Each element is greater than or equal to all elements to its right, so all are leaders.
```

**Constraints:**

- `1 <= n <= 10^5`
- `0 <= arr[i] <= 10^9`


### Brute-force approach

loop from back with two for loops and check right of every element

### Optimal

- Set a variable `max` to the last element of the array (`nums[sizeOfArray - 1]`), as the last element is always a leader.
- Create an empty list `ans` to store the leader elements, and initially add the last element of the array to this list, as it is always a leader.
- Start from the second last element (index = `sizeOfArray - 2`) and move towards the first element (index = 0).
- For each element, compare it with the `max` variable. If the current element is greater than `max`, add this element to the `ans` list and update `max` to the current element.
- After processing all elements, the `ans` list will contain all the leader elements in reverse order. Reverse the `ans` list and return it.
```c++
#include<bits/stdc++.h>
using namespace std;

class Solution {
public:
    //Function to find the leaders in an array.
    vector<int> leaders(vector<int>& nums) {
        vector<int> ans;
        
        if(nums.empty()) {
            return ans;
        }
        
        // Last element of the vector is always a leader
        int max = nums[nums.size() - 1];
        ans.push_back(nums[nums.size() - 1]);
        
        // Check elements from right to left
        for (int i = nums.size() - 2; i >= 0; i--) {
            if (nums[i] > max) {
                ans.push_back(nums[i]);
                max = nums[i];
            }
        }
        
        /* Reverse the vector to match
        the required output order*/
        reverse(ans.begin(), ans.end());
        
        //Return the leaders
        return ans;
    }
};

int main() {
    vector<int> nums = {10, 22, 12, 3, 0, 6};
    
    // Create an instance of the Solution class
    Solution finder;
    
    // Get leaders using class method
    vector<int> ans = finder.leaders(nums);
    
    cout << "Leaders in the array are: ";
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
    cout << endl;
    
    return 0;
}
```


