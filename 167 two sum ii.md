Given a **1-indexed** array of integers `numbers` that is already **_sorted in non-decreasing order_**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return _the indices of the two numbers,_ `index1` _and_ `index2`_, **added by one** as an integer array_ `[index1, index2]` _of length 2._

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int i = 0;
        int n =numbers.size();
        int j = n -1;
        while(i < j){
            if(numbers[i] + numbers[j] == target){
                return {i+1,j+1};
            }
            if(numbers[i] + numbers[j] < target){
                i++;
            }
            else{
                j--;
            }
        } 

        return {i+1,j+1};
    }
};
```

