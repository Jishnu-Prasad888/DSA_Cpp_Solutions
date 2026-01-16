
The naive method tries every number, which is slow when n is large. But our possible answer space (from 1 to n) is sorted, meaning if a certain number squared is less than or equal to n, then all smaller numbers will also work. This allows us to apply Binary Search on the answer space to efficiently find the largest number whose square is less than or equal to n.

- First, note that the answer lies between 1 and the given number n.
- Set the search range with the smallest value as 1 and the largest value as n.
- Use binary search within this range to test possible numbers.
- At each step, take the middle number and check if its square is less than or equal to n.
- If it is, record this number as a candidate and move right to check for a larger number.
- If the square is greater than n, move left to check smaller numbers.
- Continue this process until the range closes, and the largest recorded number will be the square root.

```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // This function returns the floor value of the square root of a number
    int mySqrt(int x) {
        // Handle small numbers directly
        if (x < 2) return x;

        // Initialize binary search range
        int left = 1, right = x / 2, ans = 0;

        // Perform binary search
        while (left <= right) {
            // Find middle point
            long long mid = left + (right - left) / 2;

            // Check if mid*mid is less than or equal to x
            if (mid * mid <= x) {
                // Store mid as potential answer
                ans = mid;
                // Move to right half
                left = mid + 1;
            } else {
                // Move to left half
                right = mid - 1;
            }
        }

        // Return final answer
        return ans;
    }
};

int main() {
    Solution s;
    cout << s.mySqrt(8) << endl;
    return 0;
}
```

