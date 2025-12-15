

[31. Next Permutation](https://leetcode.com/problems/next-permutation/)

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

- For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the **next permutation** of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

- For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
- Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
- While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.

Given an array of integers `nums`, _find the next permutation of_ `nums`.

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [1,3,2]

**Example 2:**

**Input:** nums = [3,2,1]
**Output:** [1,2,3]

**Example 3:**

**Input:** nums = [1,1,5]
**Output:** [1,5,1]

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 100`

## **1. Brute Force Approach**

### **Idea:**
Generate all permutations, sort them, find the current one, then return the next one.

### **Algorithm:**
1. Generate all permutations of the array
2. Sort them lexicographically
3. Find the current permutation in the sorted list
4. Return the next permutation (wrap around if it's the last)

### **Complexity:**
- **Time:** O(n! * n) - Generating n! permutations, each of size n
- **Space:** O(n!) - Storing all permutations

### **Implementation:**
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        vector<vector<int>> permutations;
        vector<int> temp = nums;
        
        // Generate all permutations
        sort(temp.begin(), temp.end());
        do {
            permutations.push_back(temp);
        } while(next_permutation(temp.begin(), temp.end()));
        
        // Find current permutation
        int idx = -1;
        for(int i = 0; i < permutations.size(); i++) {
            if(permutations[i] == nums) {
                idx = i;
                break;
            }
        }
        
        // Get next permutation (wrap around if needed)
        if(idx == permutations.size() - 1) {
            nums = permutations[0];
        } else {
            nums = permutations[idx + 1];
        }
    }
};
```

---

## **2. Better Approach (Using STL)**

### **Idea:**
Use C++ STL's `next_permutation` function directly.

### **Complexity:**
- **Time:** O(n) - Internally uses the optimal algorithm
- **Space:** O(1)

### **Implementation:**
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        // Using STL's built-in function
        next_permutation(nums.begin(), nums.end());
    }
};
```

**Note:** This is essentially the optimal solution wrapped in one function call.

---

## **3. Optimal Approach (Manual Implementation)**

### **Idea:**
The mathematical algorithm to find next permutation efficiently.

### **Algorithm Steps:**
1. **Find pivot:** From right, find first index `i` where `nums[i] < nums[i+1]`
2. **If no pivot:** Array is in descending order, reverse it
3. **Find swap candidate:** From right, find first element > nums[i] at index `j`
4. **Swap** elements at `i` and `j`
5. **Reverse** the suffix starting from `i+1`

### **Visual Example:**
```
nums = [1, 3, 5, 4, 2]
Step 1: Find pivot i = 1 (3 < 5)
        [1, 3, 5, 4, 2]
               ^ pivot at 3
Step 2: Find j from right where nums[j] > 3
        j = 3 (value 4)
Step 3: Swap nums[i] and nums[j]
        [1, 4, 5, 3, 2]
Step 4: Reverse suffix from i+1
        Suffix: [5, 3, 2] → [2, 3, 5]
        Result: [1, 4, 2, 3, 5]
```

### **Complexity:**
- **Time:** O(n) - Single pass from right, then reverse suffix
- **Space:** O(1) - In-place modifications only

### **Implementation:**
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n - 2;
        
        // Step 1: Find first decreasing element from right
        while(i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
        
        // Step 2: If found, find element to swap with
        if(i >= 0) {
            int j = n - 1;
            while(j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            // Step 3: Swap
            swap(nums[i], nums[j]);
        }
        
        // Step 4: Reverse the suffix
        reverse(nums.begin() + i + 1, nums.end());
    }
};
```

---

## **Comparison Table**

| Approach | Time Complexity | Space Complexity | Key Idea |
|----------|----------------|------------------|----------|
| **Brute Force** | O(n! * n) | O(n!) | Generate all permutations |
| **Better (STL)** | O(n) | O(1) | Use built-in `next_permutation` |
| **Optimal** | O(n) | O(1) | Mathematical algorithm |

---

## **Edge Cases to Test**

1. **Last permutation:** `[3, 2, 1]` → `[1, 2, 3]`
2. **Single element:** `[1]` → `[1]`
3. **All equal:** `[1, 1, 1]` → `[1, 1, 1]`
4. **Already next permutation:** `[1, 2, 3]` → `[1, 3, 2]`
5. **Large gap:** `[1, 5, 1]` → `[5, 1, 1]`

---

## **Why Optimal Solution Works Mathematically**

### **Intuition:**
Think of permutations as numbers:
- `[1, 2, 3]` = 123
- `[1, 3, 2]` = 132
- `[3, 2, 1]` = 321

To get the **next** number:
1. Find where we can increase the least significant digit possible
2. Increase it by the smallest possible amount
3. Make the suffix as small as possible

### **Proof of Correctness:**
- After finding pivot `i`, suffix `[i+1..n-1]` is **decreasing**
- Swapping with the next larger element gives minimal increase
- Reversing the suffix makes it **increasing** (smallest possible)

---

## **Practice Variations**

1. **Previous Permutation:** Reverse the logic (find first increasing from right)
2. **K-th Permutation:** Use factorial number system
3. **All Permutations:** Backtracking with recursion

---

**Key Takeaway:** Always use the optimal O(n) in-place algorithm for interviews. Understand why it works mathematically, not just memorizing the steps.


