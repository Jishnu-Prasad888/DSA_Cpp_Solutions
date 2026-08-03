https://leetcode.com/problems/n-queens/description/

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.




```cpp
class Solution {
private:
    bool isQueenSafe(vector<string>& board, int col, int row) {

        int temp_col = col;
        int temp_row = row;

        // upper-left diagonal
        while (col >= 0 && row >= 0) {
            if (board[row][col] == 'Q') return false;
            col--;
            row--;
        }

        col = temp_col;
        row = temp_row;

        // left side
        while (col >= 0) {
            if (board[row][col] == 'Q') return false;
            col--;
        }

        col = temp_col;
        row = temp_row;

        // lower-left diagonal
        while (col >= 0 && row < board.size()) {
            if (board[row][col] == 'Q') return false;
            col--;
            row++;
        }

        return true;
    }

    void helper(vector<vector<string>>& ans,
                vector<string>& board,
                int col,
                int n) {

        if (col == n) {
            ans.push_back(board);
            return;
        }

        for (int row = 0; row < n; row++) {
            if (isQueenSafe(board, col, row)) {
                board[row][col] = 'Q';
                helper(ans, board, col + 1, n);
                board[row][col] = '.';
            }
        }
    }

public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> ans;
        vector<string> board(n, string(n, '.'));

        helper(ans, board, 0, n);
        return ans;
    }
};
```




