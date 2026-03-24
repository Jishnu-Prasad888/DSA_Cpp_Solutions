

## Brute force

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        string maxStr = "";
        int maxCount = 0;

        for(int k = 0; k < s.length(); k++) {
            string temp = "";
            temp.push_back(s[k]);

            for(int i = k + 1; i < s.length(); i++) {
                temp.push_back(s[i]);

                bool pal = true;  // reset here for each substring

                for(int j = 0; j < temp.length(); j++) {
                    int n = temp.length() - 1;

                    if(temp[j] != temp[n - j]) {  // FIX: use j, not i
                        pal = false;
                        break;
                    }
                }

                if(pal && maxCount < temp.length()) {  // only update if palindrome
                    maxCount = temp.length();
                    maxStr = temp;
                }
            }

            // handle single character case
            if(maxCount == 0) {
                maxStr = string(1, s[k]);
                maxCount = 1;
            }
        }

        return maxStr;
    }
};
```



## Optimised


```cpp
class Solution {
public:
    string expand(string &s, int left, int right) {
        while(left >= 0 && right < s.length() && s[left] == s[right]) {
            left--;
            right++;
        }
        return s.substr(left + 1, right - left - 1);
    }

    string longestPalindrome(string s) {
        string result = "";

        for(int i = 0; i < s.length(); i++) {
            // Odd length palindrome
            string odd = expand(s, i, i);

            // Even length palindrome
            string even = expand(s, i, i + 1);

            if(odd.length() > result.length()) {
                result = odd;
            }
            if(even.length() > result.length()) {
                result = even;
            }
        }

        return result;
    }
};
```


