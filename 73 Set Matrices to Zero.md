[73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)


Hint

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Input:** matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
**Output:** [[0,0,0,0],[0,4,5,0],[0,3,1,0]]

### Key notes

`matrix,size() ` : gives the number of **rows**
 

### better approach


```c++
#include <vector>
#include <algorithm>

class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        // Use sets or boolean arrays to avoid duplicates
        vector<bool> rowZero(m, false);
        vector<bool> colZero(n, false);
        
        // First pass: mark which rows and columns have zeros
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(matrix[i][j] == 0) {
                    rowZero[i] = true;
                    colZero[j] = true;
                }
            }
        }
        
        // Second pass: set rows to zero
        for(int i = 0; i < m; i++) {
            if(rowZero[i]) {
                for(int j = 0; j < n; j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        // Third pass: set columns to zero
        for(int j = 0; j < n; j++) {
            if(colZero[j]) {
                for(int i = 0; i < m; i++) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
};
```


## **Optimal In-Place O(1) Space Solution:**

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        // Use first row and first column as markers
        bool firstRowZero = false;
        bool firstColZero = false;
        
        // Check if first row needs to be zeroed
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }
        
        // Check if first column needs to be zeroed
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }
        
        // Use first row and first column as markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;  // Mark row
                    matrix[0][j] = 0;  // Mark column
                }
            }
        }
        
        // Set matrix cells to zero based on markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        // Zero out first row if needed
        if (firstRowZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }
        
        // Zero out first column if needed
        if (firstColZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
};
```

## **Even Cleaner Version:**

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        bool col0 = false;  // Track if first column needs zeroing
        
        // First pass: mark rows and columns
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) col0 = true;
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;  // Mark row in first column
                    matrix[0][j] = 0;  // Mark column in first row
                }
            }
        }
        
        // Second pass: set zeros based on markers (bottom-up)
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 1; j--) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
            if (col0) matrix[i][0] = 0;  // Set first column if needed
        }
    }
};
```

## **Key Ideas for In-Place O(1) Space:**

1. **Use first row and first column as storage** for markers
2. **Track separately** if first row/column themselves need zeroing
3. **Two passes**:
   - First pass: Mark which rows/columns need zeroing
   - Second pass: Apply the zeros
4. **Bottom-up traversal** in second pass to avoid overwriting markers

## **Time & Space Complexity:**
- **Time:** O(m × n) - We traverse the matrix twice
- **Space:** O(1) - We only use a few boolean variables

## **Example Walkthrough:**
For matrix:
```
[1, 1, 1]
[1, 0, 1]
[1, 1, 1]
```

1. Markers after first pass:
   ```
   [1, 0, 1]  // Row markers in first column, column markers in first row
   [0, 0, 1]
   [1, 1, 1]
   ```

2. After second pass:
   ```
   [1, 0, 1]
   [0, 0, 0]
   [1, 0, 1]
   ```

This solution is optimal because it uses constant extra space while maintaining O(m×n) time complexity!