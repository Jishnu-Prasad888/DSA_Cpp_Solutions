
```js
function patternMatching(pattern, str) {
  const hashMap = new Map();
  for (let i = 0; i < pattern.length; i++) {
    hashMap.set(pattern[i], i);
  }
  let lastIndex = -1;
  for (let ch of str) {
    if (!hashMap.has(ch)) continue;
    const idx = hashMap.get(ch);
    if (idx < lastIndex) return false;
    lastIndex = idx;
  }
  return true;
}jav
```


This function checks whether the characters from `str` appear in the same relative order as they do in `pattern`.

### Code Breakdown

```js
function patternMatching(pattern, str) {
```

- `pattern`: defines the desired order of characters.
    
- `str`: the string to check.
    

---

### Step 1: Build a lookup table

```js
const hashMap = new Map();
for (let i = 0; i < pattern.length; i++) {
  hashMap.set(pattern[i], i);
}
```

Creates a map from each character in `pattern` to its position.

Example:

```js
pattern = "abcd"
```

Produces:

```js
{
  'a' => 0,
  'b' => 1,
  'c' => 2,
  'd' => 3
}
```

---

### Step 2: Track the last seen pattern position

```js
let lastIndex = -1;
```

This keeps track of the highest pattern index encountered so far.

---

### Step 3: Scan the input string

```js
for (let ch of str) {
```

Iterates through every character in `str`.

---

### Step 4: Ignore characters not in the pattern

```js
if (!hashMap.has(ch)) continue;
```

Characters that don't exist in `pattern` are skipped.

Example:

```js
pattern = "abcd"
str = "axbycz"
```

The characters `x`, `y`, and `z` are ignored.

---

### Step 5: Check ordering

```js
const idx = hashMap.get(ch);

if (idx < lastIndex) return false;

lastIndex = idx;
```

If the current character's position in the pattern is **less than** a previously seen position, the order has been violated.

Example:

```js
pattern = "abcd"
str = "acbd"
```

Traversal:

|Character|Pattern Index|lastIndex|
|---|---|---|
|a|0|0|
|c|2|2|
|b|1|❌ 1 < 2|

Returns:

```js
false
```

because `b` appears after `c`, which violates the pattern order.

---

### Step 6: Success

```js
return true;
```

If no ordering violation is found, the string follows the pattern.

---

## Examples

### Example 1

```js
patternMatching("abcd", "axbyczd");
```

Relevant characters:

```
a → b → c → d
```

Order is preserved.

Result:

```js
true
```

---

### Example 2

```js
patternMatching("abcd", "acbd");
```

Relevant characters:

```
a → c → b → d
```

`b` comes after `c`, violating the pattern.

Result:

```js
false
```

---

### Example 3

```js
patternMatching("abc", "xxaayybbzzcc");
```

Relevant characters:

```
a → a → y → y → b → b → c → c
```

Pattern order is maintained.

Result:

```js
true
```

---

### Example 4

```js
patternMatching("abc", "cab");
```

Relevant characters:

```
c → a
```

`a` has a smaller pattern index than `c`.

Result:

```js
false
```

---

### Important Limitation

The function assumes that characters in `pattern` are unique.

For example:

```js
pattern = "abca"
```

The map becomes:

```js
{
  'a' => 3,
  'b' => 1,
  'c' => 2
}
```

The first `a` at index `0` is overwritten by the last `a` at index `3`, which may not be what you want.

### Time and Space Complexity

- Building the map: **O(p)** where `p = pattern.length`
    
- Scanning the string: **O(s)** where `s = str.length`
    
- Total: **O(p + s)**
    
- Space: **O(p)**
    

In summary, the function verifies that all characters from `str` that also exist in `pattern` appear in a non-decreasing order according to their positions in `pattern`.



A common approach is:

1. Convert the number to a string.
    
2. Mirror the left half onto the right half to form a palindrome.
    
3. If that palindrome is already greater than the original number, return it.
    
4. Otherwise, increment the middle digit(s) and mirror again.
    

### Examples

- `123` → `131`
    
- `808` → `818`
    
- `999` → `1001`
    
- `12932` → `13031`
    

### JavaScript Solution

```js
function nextPalindrome(num) {
  const s = String(num);
  const n = s.length;

  function mirror(arr) {
    const res = [...arr];
    for (let i = 0; i < Math.floor(n / 2); i++) {
      res[n - 1 - i] = res[i];
    }
    return res.join('');
  }

  // First palindrome by mirroring left -> right
  let pal = mirror([...s]);

  if (BigInt(pal) > BigInt(s)) {
    return pal;
  }

  // Increment middle and propagate carry
  let arr = [...s];
  let carry = 1;
  let mid = Math.floor((n - 1) / 2);

  while (mid >= 0 && carry) {
    let digit = Number(arr[mid]) + carry;
    arr[mid] = String(digit % 10);
    carry = Math.floor(digit / 10);
    mid--;
  }

  // Handle cases like 9, 99, 999
  if (carry) {
    return '1' + '0'.repeat(n - 1) + '1';
  }

  return mirror(arr);
}
```

### Walkthrough: `12932`

Original:

```
12932
```

Mirror left to right:

```
12921
```

Not greater than `12932`, so increment the middle:

```
13032
```

Mirror again:

```
13031
```

Result:

```
13031
```

### Complexity

- Time: **O(d)** where `d` is the number of digits.
    
- Space: **O(d)**.
    

This is much more efficient than checking each subsequent number until a palindrome is found.



**Q3: Chainable calc function**

Implement a `calc` function such that:

calc(8).sum(3).mul(3).val(); // 33

A classic test of closures and method chaining. The kind of question that looks easy until you start typing.

```javascript
function calc(num) {
  let value = num;
  return {
    sum(n) { value += n; return this; },
    mul(n) { value *= n; return this; },
    val() { return value; }
  };
}
```

> _Given an array, split it into two parts such that the absolute difference between their sums is minimum. Return both parts._

For example, `[2, 3, 4, 1]` → split at index 1 → `[2, 3]` and `[4, 1]` → both sums are 5 → diff is 0.

The classic prefix-sum + comparison approach. But the discussion went into:

- How would you handle very large arrays?
- What if elements could be negative?
- What’s the time vs space tradeoff?

It wasn’t just “solve it.” It was “solve it, and then _defend_ it.”


```javascript
function minPartition(arr) {
  const total = arr.reduce((a, b) => a + b, 0);
  const target = Math.floor(total / 2);
  const n = arr.length;

  const dp = Array.from(
    { length: n + 1 },
    () => Array(target + 1).fill(false)
  );

  for (let i = 0; i <= n; i++) {
    dp[i][0] = true;
  }

  for (let i = 1; i <= n; i++) {
    for (let s = 1; s <= target; s++) {
      dp[i][s] = dp[i - 1][s];

      if (s >= arr[i - 1]) {
        dp[i][s] ||= dp[i - 1][s - arr[i - 1]];
      }
    }
  }

  let best = target;

  while (best >= 0 && !dp[n][best]) {
    best--;
  }

  const part1 = [];
  const used = Array(n).fill(false);

  let s = best;

  for (let i = n; i > 0 && s > 0; i--) {
    if (
      s >= arr[i - 1] &&
      dp[i - 1][s - arr[i - 1]]
    ) {
      part1.push(arr[i - 1]);
      used[i - 1] = true;
      s -= arr[i - 1];
    }
  }

  const part2 = [];

  for (let i = 0; i < n; i++) {
    if (!used[i]) {
      part2.push(arr[i]);
    }
  }

  return {
    part1,
    part2,
    difference: Math.abs(
      part1.reduce((a, b) => a + b, 0) -
      part2.reduce((a, b) => a + b, 0)
    )
  };
}
```


### Implement an async recursive function to find all files in a file system that match a regex pattern.

```javascript
async function findFilesWithPattern(fs, pattern, currentPath = "") {
  const fullPath = `${currentPath}/${fs.name}`;
  if (fs.type === "file") {
      return pattern.test(fs.name) ? [fullPath] : [];
    }
    const results = await Promise.all(
      fs.children.map(child => findFilesWithPattern(child, pattern, fullPath))
    );
    return results.flat();
 }
```