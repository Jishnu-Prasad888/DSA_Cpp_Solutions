

## Brute

```cpp
class Solution {
public:
    // Function to count subarrays with XOR equal to B
    int countSubarraysXOR(vector<int>& A, int B) {
        // Initialize count of valid subarrays
        int count = 0;
        // Traverse all starting points
        for (int i = 0; i < A.size(); i++) {
            // Maintain xor of current subarray
            int xorVal = 0;
            // Extend subarray till end
            for (int j = i; j < A.size(); j++) {
                // Update xor
                xorVal ^= A[j];
                // If xor equals B, increment count
                if (xorVal == B) {
                    count++;
                }
            }
        }
        return count;
    }
};

```



## Optimal


```cpp
class Solution {
public:
    // Function to count subarrays with given XOR
    int countSubarrays(vector<int>& A, int k) {
        // Store frequency of prefix XORs
        unordered_map<int, int> freq;
        // Initialize with prefix XOR 0
        freq[0] = 1;

        // Current prefix XOR
        int prefixXor = 0;
        // Answer count
        int count = 0;

        // Traverse array
        for (int num : A) {
            // Update prefix XOR
            prefixXor ^= num;

            // Compute required XOR
            int target = prefixXor ^ k;

            // If target exists in map, add its frequency
            if (freq.find(target) != freq.end()) {
                count += freq[target];
            }

            // Store current prefix XOR in map
            freq[prefixXor]++;
        }
        return count;
    }
};
```


