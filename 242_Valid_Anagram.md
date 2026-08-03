https://leetcode.com/problems/valid-anagram/

## Basic solution

##### Time Complexity

- Sorting `s`: **O(n log n)**
- Sorting `t`: **O(n log n)**
- Comparing strings: **O(n)**
- **Total:** **O(n log n)**

```c++
#include <algorithm>

#include <string>

using namespace std;

class Solution {

public:

    bool isAnagram(string s, string t) {

        if(s.length() != t.length()){

            return false ;

        }

        sort(s.begin(),s.end());

        sort(t.begin(),t.end());

        return s==t;

    }

};
```

## using frequency counting

```c++
#include <string>
using namespace std;

class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) return false;

        int count[26] = {0}; // For 26 lowercase letters

        for (char c : s) count[c - 'a']++;
        for (char c : t) count[c - 'a']--;

        for (int i = 0; i < 26; i++) {
            if (count[i] != 0) return false;
        }

        return true;
    }
};
```

**Time Complexity:** O(n)  
**Space Complexity:** O(1) (fixed 26-size array)

## Unicode

```c++
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) return false;

        unordered_map<char, int> freq;

        for (char c : s) freq[c]++;
        for (char c : t) {
            if (--freq[c] < 0) return false;
        }

        return true;
    }
};
```

**Time Complexity:** O(n)  
**Space Complexity:** O(k) where k is number of unique characters
