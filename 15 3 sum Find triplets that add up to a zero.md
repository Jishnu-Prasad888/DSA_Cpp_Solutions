
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

### Brute force :

O(n^3)

### better

```cpp
#include <bits/stdc++.h>
using namespace std;

// Class to solve 3-sum problem
class Solution {
public:
    // Function to find triplets with sum zero
    vector<vector<int>> threeSum(vector<int>& arr, int n) {
        // Store unique triplets
        set<vector<int>> ans;

        // First loop for first element
        for (int i = 0; i < n; i++) {
            // Set to store elements seen in this iteration
            set<int> hashset;

            // Second loop for second element
            for (int j = i + 1; j < n; j++) {
                // Calculate third element needed
                int third = -(arr[i] + arr[j]);

                // If third already in set, we found a triplet
                if (hashset.find(third) != hashset.end()) {
                    vector<int> temp = {arr[i], arr[j], third};
                    sort(temp.begin(), temp.end());
                    ans.insert(temp);
                }

                // Add current element to set
                hashset.insert(arr[j]);
            }
        }

        // Convert set to vector
        return vector<vector<int>>(ans.begin(), ans.end());
    }
};

// Driver code
int main() {
    vector<int> arr = {-1, 0, 1, 2, -1, -4};
    int n = arr.size();
    Solution obj;
    vector<vector<int>> res = obj.threeSum(arr, n);

    for (auto &triplet : res) {
        for (auto &num : triplet) cout << num << " ";
        cout << endl;
    }
    return 0;
}

```

### Optimal

```cpp
#include <bits/stdc++.h>
using namespace std;

// Class to solve 3-sum problem
class Solution {
public:
    // Function to find triplets with sum zero
    vector<vector<int>> threeSum(vector<int>& arr, int n) {
        // Sort the array
        sort(arr.begin(), arr.end());
        // Store final result
        vector<vector<int>> ans;

        // First loop for first element
        for (int i = 0; i < n; i++) {
            // Skip duplicates for first element
            if (i > 0 && arr[i] == arr[i - 1]) continue;

            // Two pointers
            int left = i + 1, right = n - 1;

            // Find pairs for current arr[i]
            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];

                if (sum == 0) {
                    ans.push_back({arr[i], arr[left], arr[right]});
                    left++, right--;

                    // Skip duplicates for left
                    while (left < right && arr[left] == arr[left - 1]) left++;
                    // Skip duplicates for right
                    while (left < right && arr[right] == arr[right + 1]) right--;
                }
                else if (sum < 0) left++;
                else right--;
            }
        }
        return ans;
    }
};

// Driver code
int main() {
    vector<int> arr = {-1, 0, 1, 2, -1, -4};
    int n = arr.size();
    Solution obj;
    vector<vector<int>> res = obj.threeSum(arr, n);

    for (auto &triplet : res) {
        for (auto &num : triplet) cout << num << " ";
        cout << endl;
    }
    return 0;
}

```



```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        
        for(int k = 0; k < n - 2; k++) {  // Only go until n-2
            // Skip duplicate values for k
            if(k > 0 && nums[k] == nums[k-1]) continue;
            
            int i = k + 1;  // Start from k+1, not k!
            int j = n - 1;
            int target = -nums[k];  // We need nums[i] + nums[j] = -nums[k]
            
            while(i < j) {
                int sum = nums[i] + nums[j];
                
                if(sum == target) {
                    res.push_back({nums[k], nums[i], nums[j]});
                    
                    // Skip duplicates for i and j
                    while(i < j && nums[i] == nums[i+1]) i++;
                    while(i < j && nums[j] == nums[j-1]) j--;
                    
                    i++;
                    j--;
                }
                else if(sum < target) {
                    i++;
                }
                else {
                    j--;
                }
            }
        }
        
        return res;
    }
};
```

