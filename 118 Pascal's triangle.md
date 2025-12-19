
Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:


```c++
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        if(numRows == 1){
            return {{1}};
        }

        vector<vector<int>> res;
        vector<int> temp = {1};
        vector<int> temp2;
        res.push_back(temp);
        for(int i = 0 ; i < numRows -1 ; i++){
            temp2.push_back(1);
            for(int j = 0 ; j < (int)temp.size() - 1 ; j++){
                temp2.push_back(temp[j] + temp[j+1]);
            }
            temp2.push_back(1);
            
            res.push_back(temp2);
            temp = temp2;
            temp2.clear();
        }

        return res;
    }
};
```