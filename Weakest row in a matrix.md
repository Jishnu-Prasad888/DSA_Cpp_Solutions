[1337. The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/)


You are given an `m x n` binary matrix `mat` of `1`'s (representing soldiers) and `0`'s (representing civilians). The soldiers are positioned **in front** of the civilians. That is, all the `1`'s will appear to the **left** of all the `0`'s in each row.

A row `i` is **weaker** than a row `j` if one of the following is true:

- The number of soldiers in row `i` is less than the number of soldiers in row `j`.
- Both rows have the same number of soldiers and `i < j`.

Return _the indices of the_ `k` _**weakest** rows in the matrix ordered from weakest to strongest_.

**Example 1:**

**Input:** mat = 
[[1,1,0,0,0],
 [1,1,1,1,0],
 [1,0,0,0,0],
 [1,1,0,0,0],
 [1,1,1,1,1]], 
k = 3
**Output:** [2,0,3]
**Explanation:** 
The number of soldiers in each row is: 
- Row 0: 2 
- Row 1: 4 
- Row 2: 1 
- Row 3: 2 
- Row 4: 5 
The rows ordered from weakest to strongest are [2,0,3,1,4].

**Example 2:**

**Input:** mat = 
[[1,0,0,0],
 [1,1,1,1],
 [1,0,0,0],
 [1,0,0,0]], 
k = 2
**Output:** [0,2]
**Explanation:** 
The number of soldiers in each row is: 
- Row 0: 1 
- Row 1: 4 
- Row 2: 1 
- Row 3: 1 
The rows ordered from weakest to strongest are [0,2,3,1].

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `2 <= n, m <= 100`
- `1 <= k <= m`
- `matrix[i][j]` is either 0 or 1.


## brute


```cpp
class Solution {
public:
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        vector<pair<int, int>> rows;

        // Count soldiers in each row
        for (int i = 0; i < mat.size(); i++) {
            int soldiers = 0;
            for (int j = 0; j < mat[i].size(); j++) {
                if (mat[i][j] == 1)
                    soldiers++;
            }
            rows.push_back({soldiers, i});
        }

        // Sort by soldiers first, then index
        sort(rows.begin(), rows.end());

        // Collect k weakest rows
        vector<int> ans;
        for (int i = 0; i < k; i++) {
            ans.push_back(rows[i].second);
        }

        return ans;
    }
};

```


## Optimised


```cpp
class Solution {
public:
    int countSoldiers(const vector<int>& row) {
        int left = 0, right = row.size();
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (row[mid] == 1)
                left = mid + 1;
            else
                right = mid;
        }
        return left; // number of 1s
    }

    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        vector<pair<int, int>> strength;

        for (int i = 0; i < mat.size(); i++) {
            int soldiers = countSoldiers(mat[i]);
            strength.push_back({soldiers, i});
        }

        sort(strength.begin(), strength.end());

        vector<int> result;
        for (int i = 0; i < k; i++) {
            result.push_back(strength[i].second);
        }

        return result;
    }
};

```