

### Brute

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();

        for (int c : nums2) {
            nums1.push_back(c);
        }

        sort(nums1.begin(), nums1.end());

        int total = m + n;

        if (total % 2 != 0) {
            return nums1[total / 2];
        } else {
            return (nums1[total / 2 - 1] + nums1[total / 2]) / 2.0;
        }
    }
};

```


### Optimised

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        // Always binary search the smaller array
        if (nums1.size() > nums2.size())
            return findMedianSortedArrays(nums2, nums1);

        int m = nums1.size();
        int n = nums2.size();

        int low = 0, high = m;

        while (low <= high) {
            int i = (low + high) / 2;
            int j = (m + n + 1) / 2 - i;

            int leftA  = (i == 0) ? INT_MIN : nums1[i - 1];
            int rightA = (i == m) ? INT_MAX : nums1[i];

            int leftB  = (j == 0) ? INT_MIN : nums2[j - 1];
            int rightB = (j == n) ? INT_MAX : nums2[j];

            if (leftA <= rightB && leftB <= rightA) {
                // Correct partition found
                if ((m + n) % 2 == 0) {
                    return (max(leftA, leftB) + min(rightA, rightB)) / 2.0;
                } else {
                    return max(leftA, leftB);
                }
            }
            else if (leftA > rightB) {
                high = i - 1;  // move left
            }
            else {
                low = i + 1;   // move right
            }
        }

        return 0.0; // unreachable
    }
};

```


