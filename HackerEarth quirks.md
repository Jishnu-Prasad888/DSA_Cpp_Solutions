
You do **not** need to change your coding style much at all.  
If you are comfortable with LeetCode C++, HackerEarth will feel very similar.  
The **main difference** is _how input and output are handled_.

---

## Key Difference: LeetCode vs HackerEarth

### LeetCode

- You usually **do not write `main()`**
    
- Input is passed as function arguments
    
- Output is returned from a function
    

Example:

```cpp
class Solution {
public:
    int solve(int n) {
        return n * 2;
    }
};
```

---

### HackerEarth

- You **must write `main()`**
    
- Input comes from **standard input (stdin)**
    
- Output goes to **standard output (stdout)**
    

You read input using `cin` and print using `cout`.

---

## Basic HackerEarth C++ Template

This works for almost all problems:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // read input
    int n;
    cin >> n;

    // process
    cout << n << "\n";

    return 0;
}
```

---

## How to Read Input (Most Common Patterns)

### 1. Two integers

```cpp
int N, M;
cin >> N >> M;
```

---

### 2. Reading edges (like this problem)

```cpp
int N, M;
cin >> N >> M;

for (int i = 0; i < M; i++) {
    int A, B;
    cin >> A >> B;
}
```

---

### 3. Reading an array

```cpp
int n;
cin >> n;
vector<int> arr(n);

for (int i = 0; i < n; i++) {
    cin >> arr[i];
}
```

---

### 4. Reading strings

```cpp
string s;
cin >> s;        // no spaces
getline(cin, s); // full line
```

---

## How to Print Output

Single value:

```cpp
cout << answer << "\n";
```

Multiple values:

```cpp
cout << a << " " << b << "\n";
```

---

## Important Performance Tips (Very Important on HackerEarth)

Always add these lines at the start of `main()`:

```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
```

This makes `cin/cout` fast like `scanf/printf`.

Below are the **most common mistakes LeetCode users make on HackerEarth**, and **practical ways to debug wrong answers**. This is based on how HackerEarth judges input/output and constraints.

---

## Common Input Traps on HackerEarth

### 1. Forgetting to read _everything_

On LeetCode, input is guaranteed and clean.  
On HackerEarth, **missing even one `cin` breaks everything**.

Example trap:

```cpp
int N, M;
cin >> N;
// forgot to read M
```

Correct:

```cpp
int N, M;
cin >> N >> M;
```

If input format says “next M lines…”, you **must** loop exactly M times.

---

### 2. 1-based vs 0-based indexing

Most HackerEarth problems use **1-based labels**.

Example:

```
Countries are numbered from 1 to N
```

Trap:

```cpp
vector<vector<int>> adj(N);
adj[A].push_back(B);   // WRONG
```

Correct:

```cpp
vector<vector<int>> adj(N + 1);
adj[A].push_back(B);
adj[B].push_back(A);
```

---

### 3. Multiple test cases hidden

Some problems **do not clearly mention test cases**, but still include them.

Always check:

- Does the input start with `T`?
    
- Do sample inputs have multiple blocks?
    

Safe pattern:

```cpp
int T;
cin >> T;
while (T--) {
    solve();
}
```

If not mentioned, assume **single test case only**.

---

### 4. Integer overflow

HackerEarth often uses **large constraints**.

Trap:

```cpp
int ways = factorial(N);   // overflow
```

Correct:

```cpp
long long ways;
const long long MOD = 1e9 + 7;
ways = (ways * x) % MOD;
```

Rule:

- Use `long long` for counts
    
- Apply `% MOD` **at every multiplication**
    

---

### 5. Modulo mistakes

Very common error.

Trap:

```cpp
ans = ans * i;
ans %= MOD;
```

If `ans * i` overflows **before modulo**, result is wrong.

Correct:

```cpp
ans = (ans * i) % MOD;
```

---

### 6. Assuming graph is connected

HackerEarth frequently tests **edge cases**.

Always consider:

- Isolated nodes
    
- Disconnected components
    
- Nodes with degree 0
    

Never assume full connectivity unless explicitly stated.

---

### 7. Reading input too slowly

Large input → **TLE due to slow I/O**

Always include:

```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
```

Avoid `endl` (it flushes output).

---

## How to Debug Wrong Answers on HackerEarth

### 1. Print intermediate values (most effective)

You are allowed to print debugging output **locally**, just remove it before final submission.

Example:

```cpp
cerr << "N = " << N << " M = " << M << "\n";
```

Why `cerr`?

- Does **not affect output**
    
- Faster for debugging
    

---

### 2. Test against sample input manually

Use **Custom Input** and paste sample test.

Then:

- Print key variables
    
- Compare step-by-step with explanation
    

---

### 3. Reduce the input size

If logic is complex:

- Test with `N = 2, 3, 4`
    
- Print all states
    

Example:

```cpp
for (auto x : dp) cerr << x << " ";
cerr << "\n";
```

---

### 4. Check edge cases explicitly

Always test:

- `N = 1`
    
- `M = 0`
    
- Fully connected graph
    
- Completely disconnected graph
    

Many HackerEarth WA come from **unhandled corner cases**.

---

### 5. Verify constraints vs approach

Ask:

- Is `O(N!)`, `O(2^N)` allowed?
    
- Is `N <= 16` → bitmask OK
    
- Is `N <= 10^5` → DFS per node NOT OK
    

Wrong Answer sometimes is actually **hidden TLE or overflow**.

---

### 6. Compare with brute force (small input)

For small N:

- Write a brute solution
    
- Compare outputs with optimized solution
    

Example:

```cpp
if (N <= 8) {
    brute();
    optimized();
}
```

If outputs differ → logic bug.

---

### 7. Understand judge behavior

HackerEarth:

- Exact output match required
    
- No extra spaces
    
- No extra lines
    

Trap:

```cpp
cout << ans << " ";
```

Correct:

```cpp
cout << ans << "\n";
```

---

Below is a **fully HackerEarth-compatible C++ solution** for the **Travelling Spy Problem**, written in the style you should submit there (with `main()`, `cin/cout`, fast I/O).

I’ll first explain the idea briefly, then give the **final clean code**.

---

## Key Idea (Why this works)

- There are **N countries (N ≤ 16)**
    
- The spy must visit **every country exactly once**
    
- A valid passport stamp pattern = a **permutation of countries**
    
- The permutation is valid **only if every consecutive pair has a direct route**
    

So this is exactly:

> **Count the number of Hamiltonian paths in an undirected graph**

---

## Technique Used

Since **N ≤ 16**, we use:

### Bitmask Dynamic Programming

### State

```
dp[mask][last]
```

- `mask`: which countries have been visited
    
- `last`: the last visited country
    
- Value = number of ways to reach this state
    

---

### Transition

From `dp[mask][u]`, try to go to `v` if:

- `v` is not yet visited
    
- there is a route between `u` and `v`
    

```
dp[mask | (1<<v)][v] += dp[mask][u]
```

---

### Initialization

Any country can be the starting point:

```
dp[1<<i][i] = 1
```

---

### Final Answer

Sum of all:

```
dp[(1<<N) - 1][i]   for all i
```

---

## Time Complexity

```
O(N * 2^N * N)  ≈ 16 * 65536 * 16 → OK
```

---

## HackerEarth Compatible C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

static const long long MOD = 1000000007;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int N, M;
    cin >> N >> M;

    // adjacency matrix
    vector<vector<int>> adj(N, vector<int>(N, 0));
    for (int i = 0; i < M; i++) {
        int A, B;
        cin >> A >> B;
        --A; --B;                 // convert to 0-based
        adj[A][B] = adj[B][A] = 1;
    }

    int FULL = (1 << N);
    vector<vector<long long>> dp(FULL, vector<long long>(N, 0));

    // starting from any single country
    for (int i = 0; i < N; i++) {
        dp[1 << i][i] = 1;
    }

    // DP over subsets
    for (int mask = 1; mask < FULL; mask++) {
        for (int u = 0; u < N; u++) {
            if (!(mask & (1 << u))) continue;
            long long ways = dp[mask][u];
            if (ways == 0) continue;

            for (int v = 0; v < N; v++) {
                if ((mask & (1 << v)) == 0 && adj[u][v]) {
                    int newMask = mask | (1 << v);
                    dp[newMask][v] = (dp[newMask][v] + ways) % MOD;
                }
            }
        }
    }

    long long answer = 0;
    for (int i = 0; i < N; i++) {
        answer = (answer + dp[FULL - 1][i]) % MOD;
    }

    cout << answer << "\n";
    return 0;
}
```

---

## Why This Passes on HackerEarth

- Uses `main()` and standard input/output
    
- Fast I/O enabled
    
- Correct modulo handling
    
- No extra output
    
- Handles disconnected graphs correctly
    

---

If you want next:

- Step-by-step dry run on **Sample Case 2**
    
- How to optimize memory further
    
- How to detect impossibility early
    
- How this differs from TSP on LeetCode
    

Just tell me.