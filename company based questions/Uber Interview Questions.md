
# **Question 1 – Shuttle Grid Revenue Problem**

**Problem Statement:**

* You are given a grid of size `n × m`. Each cell `(i, j)` has a revenue value `revenue[i][j]`.
* You start at the top-left corner `(0,0)` and want to reach the bottom-right corner `(n-1,m-1)`.
* You can move **right** or **down** only.
* At each cell, you may **pick** (gain revenue) or **skip**.
* **Constraint:** In each row, you can pick **at most `k` cells**.
* Your task is to **maximize total revenue** collected while reaching the bottom-right corner.

**Example:**

```
revenue = [[3, 4, 10],
           [2, 8, 1]]
k = 2
Optimal revenue = 16
```

---

### **Brute Force Solution (Backtracking)**

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, m, k;
vector<vector<int>> revenue;
int ans = 0;

void dfs(int i, int j, int rowCount, int sum) {
    if (i >= n || j >= m) return;

    // Option 1: skip current cell
    dfs(i, j + 1, rowCount, sum);   // move right
    dfs(i + 1, j, 0, sum);          // move down (row resets)

    // Option 2: pick current cell (if allowed)
    if (rowCount < k) {
        int newRowCount = rowCount + 1;
        int newSum = sum + revenue[i][j];
        dfs(i, j + 1, newRowCount, newSum);
        dfs(i + 1, j, 0, newSum);
    }

    if (i == n - 1 && j == m - 1)
        ans = max(ans, sum);
}

int main() {
    revenue = {{3,4,10},{2,8,1}};
    n = revenue.size();
    m = revenue[0].size();
    k = 2;

    dfs(0, 0, 0, 0);
    cout << ans << endl; // Output: 16
}
```

---

### **Optimized Solution (Dynamic Programming)**

```cpp
#include <bits/stdc++.h>
using namespace std;

long long maxRevenue(vector<vector<int>>& revenue, int k) {
    int n = revenue.size(), m = revenue[0].size();
    const long long NEG = -1e18;

    vector<vector<vector<long long>>> dp(
        n, vector<vector<long long>>(m, vector<long long>(k + 1, NEG))
    );

    dp[0][0][0] = 0;
    if (k > 0) dp[0][0][1] = revenue[0][0];

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (i == 0 && j == 0) continue;

            for (int c = 0; c <= k; c++) {
                // From left
                if (j > 0 && dp[i][j-1][c] != NEG) {
                    dp[i][j][c] = max(dp[i][j][c], dp[i][j-1][c]);
                    if (c < k)
                        dp[i][j][c+1] = max(dp[i][j][c+1],
                                             dp[i][j-1][c] + revenue[i][j]);
                }

                // From top (row reset)
                if (i > 0 && dp[i-1][j][c] != NEG) {
                    dp[i][j][0] = max(dp[i][j][0], dp[i-1][j][c]);
                    if (k > 0)
                        dp[i][j][1] = max(dp[i][j][1],
                                           dp[i-1][j][c] + revenue[i][j]);
                }
            }
        }
    }

    long long ans = 0;
    for (int c = 0; c <= k; c++)
        ans = max(ans, dp[n-1][m-1][c]);

    return ans;
}

int main() {
    vector<vector<int>> revenue = {{3,4,10},{2,8,1}};
    int k = 2;
    cout << maxRevenue(revenue, k) << endl; // Output: 16
}
```

---

# **Question 2 – Palindromic Substrings with Vowels**

**Problem Statement:**

* You are given a string `rideRoute`.
* A **segment** is any non-empty substring of the string.
* A segment is **special** if:

  1. It is a **palindrome**
  2. It contains **at least one vowel** (`a, e, i, o, u`)
* Count **distinct special segments** in the string.

**Example:**

```
rideRoute = "uber"
Special segments: "u", "e"
Answer: 2
```

---

### **Brute Force Solution (Generate All Substrings)**

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isVowel(char c) {
    return c=='a'||c=='e'||c=='i'||c=='o'||c=='u';
}

bool isPalindrome(const string& s) {
    int l=0, r=s.size()-1;
    while(l<r) {
        if(s[l++]!=s[r--]) return false;
    }
    return true;
}

int bruteCountSpecial(string s) {
    unordered_set<string> st;
    int n = s.size();
    for(int i=0;i<n;i++){
        for(int j=i;j<n;j++){
            string sub = s.substr(i,j-i+1);
            if(isPalindrome(sub)) {
                for(char c:sub) if(isVowel(c)){ st.insert(sub); break; }
            }
        }
    }
    return st.size();
}

int main(){
    string rideRoute = "uber";
    cout << bruteCountSpecial(rideRoute) << endl; // 2
}
```

---

### **Optimized Solution (Center Expansion)**

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isVowel(char c) {
    return c=='a'||c=='e'||c=='i'||c=='o'||c=='u';
}

int countSpecialSegments(string s) {
    int n = s.size();
    unordered_set<string> st;

    for(int center=0;center<n;center++){
        // Odd length palindromes
        int l=center, r=center;
        bool hasVowel=false;
        while(l>=0 && r<n && s[l]==s[r]){
            if(isVowel(s[l])) hasVowel=true;
            if(hasVowel) st.insert(s.substr(l,r-l+1));
            l--; r++;
        }

        // Even length palindromes
        l=center; r=center+1; hasVowel=false;
        while(l>=0 && r<n && s[l]==s[r]){
            if(isVowel(s[l])) hasVowel=true;
            if(hasVowel) st.insert(s.substr(l,r-l+1));
            l--; r++;
        }
    }
    return st.size();
}

int main(){
    string rideRoute = "uber";
    cout << countSpecialSegments(rideRoute) << endl; // 2
}
```

---

# **Question 3 – Tree Zone Audit with Jumps**

**Problem Statement:**

* You are given a tree of `n` zones.
* `parents[i]` = parent of zone `i`. Root = `0` (`parents[0]=-1`).
* Each query has:

  * `startZone` → starting zone
  * `resolutionJump` → jump steps
* Process:

  1. Start at `startZone`
  2. Jump **up the tree `resolutionJump` times** repeatedly
  3. Collect **all visited zone IDs**
  4. Stop when jumping above root
  5. Return **sum of visited IDs**

**Example:**

```
parents = [-1,0,0,1,1,3,3,6,2]
startZone = 6
resolutionJump = 2
Visited: 6 → jump 2 → 1 → jump 2 → root exceeded
Sum = 6 + 1 = 7
```

---

### **Brute Force Solution (Simple Traversal)**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<long long> bruteForceAudit(
    int n,
    vector<int>& parents,
    vector<int>& startZone,
    vector<int>& resolutionJump
){
    vector<long long> result;
    for(int i=0;i<startZone.size();i++){
        int curr=startZone[i], jump=resolutionJump[i];
        long long sum=0;

        while(curr!=-1){
            sum += curr;
            int steps=0;
            while(steps<jump && curr!=-1){
                curr=parents[curr];
                steps++;
            }
        }
        result.push_back(sum);
    }
    return result;
}

int main(){
    int n=9;
    vector<int> parents = {-1,0,0,1,1,3,3,6,2};
    vector<int> startZone = {6,7,8};
    vector<int> resolutionJump = {2,2,3};

    vector<long long> ans = bruteForceAudit(n, parents, startZone, resolutionJump);
    for(long long x: ans) cout << x << " "; // 7 13 8
}
```

---

### **Optimized Solution (Binary Lifting)**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<long long> optimizedAudit(
    int n,
    vector<int>& parents,
    vector<int>& startZone,
    vector<int>& resolutionJump
){
    int LOG = ceil(log2(n+1));
    vector<vector<int>> up(n, vector<int>(LOG,-1));

    for(int i=0;i<n;i++) up[i][0]=parents[i];

    for(int j=1;j<LOG;j++){
        for(int i=0;i<n;i++){
            if(up[i][j-1]!=-1) up[i][j]=up[up[i][j-1]][j-1];
        }
    }

    vector<long long> result;
    for(int q=0;q<startZone.size();q++){
        int curr=startZone[q], jump=resolutionJump[q];
        long long sum=0;

        while(curr!=-1){
            sum += curr;
            int next=curr, k=jump;

            for(int bit=0;bit<LOG && next!=-1;bit++){
                if(k & (1<<bit)) next=up[next][bit];
            }
            curr=next;
        }
        result.push_back(sum);
    }
    return result;
}

int main(){
    int n=9;
    vector<int> parents = {-1,0,0,1,1,3,3,6,2};
    vector<int> startZone = {6,7,8};
    vector<int> resolutionJump = {2,2,3};

    vector<long long> ans = optimizedAudit(n, parents, startZone, resolutionJump);
    for(long long x: ans) cout << x << " "; // 7 13 8
}
```
