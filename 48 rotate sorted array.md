
You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

![[Pasted image 20251216225800.png]]


## Optimal 

To rotate a matrix 90 degrees clockwise in-place (without using extra space), we use two key matrix operations:

- **Step 1: Transpose the matrix**: swap elements across the diagonal. This converts rows into columns.
- **Step 2: Reverse each row**: this turns the new columns into the final rotated rows.

  
This works because:

- Transposing moves elements from (i, j) to (j, i), effectively rotating across the diagonal.
- Reversing the rows repositions the elements in each row, finalizing the clockwise rotation.

- Get the size of the square matrix (number of rows or columns).
- Start the first phase: **Transpose the matrix**
    - For each row starting from the top to bottom:
    - For each column starting from the diagonal element (excluding already visited elements):
    - Swap the current element with the element that is diagonally opposite across the main diagonal.
    - This effectively flips the matrix over its top-left to bottom-right diagonal, converting rows into columns.
- Move to the second phase: **Reverse each row**
    - For every row in the matrix:
    - Reverse the order of the elements in that row (first element becomes last, second becomes second last, and so on).
    - This realigns the columns to their correct position for the clockwise rotation.
- Once both phases are done, the matrix will have been rotated 90 degrees clockwise in-place.


```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to rotate matrix 90 degrees clockwise in-place
    void rotateClockwise(vector<vector<int>>& matrix) {
        int n = matrix.size();

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                // Swap element at (i, j) with (j, i) to transpose
                swap(matrix[i][j], matrix[j][i]);
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; ++i) {
            // Reverse the current row to complete clockwise rotation
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};

// Driver code
int main() {
    vector<vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    Solution obj;
    obj.rotateClockwise(matrix);

    // Print rotated matrix
    for (auto row : matrix) {
        for (int val : row) {
            cout << val << " ";
        }
        cout << endl;
    }

    return 0;
}

```