
```cpp
class Solution {
public:
    const long long MOD = 1e9 + 7;

    long long power(long long n, long long times) {
        if (times == 0) {
            return 1;
        }

        long long half = power(n, times / 2);

        long long ans = (half * half) % MOD;

        if (times % 2) {
            ans = (ans * n) % MOD;
        }

        return ans;
    }

    int countGoodNumbers(long long n) {
        long long evenCount = (n + 1) / 2;
        long long oddCount = n / 2;

        long long evenWays = power(5, evenCount);
        long long oddWays = power(4, oddCount);

        return (evenWays * oddWays) % MOD;
    }
};
```


