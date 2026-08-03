### Round 1: Online Screening (Platform Assessment)

**Role:** Frontend Engineer **Location:** Hyderabad (Remote) **Duration:** 60 minutes **Format:** 10 questions, including both coding and theoretical ones, with varying weightage.

#### 1. Problem Solving: Fetch Keys from Nested Object / Array

I was given a function that takes in a deeply nested object or array and returns all the keys (or paths) that point to primitive values. The expected output should list all the flattened key paths.

**Example Inputs/Outputs:**

**Input:**

```
{ a: { b: {c:1}, d:2 }, e: 3 }
```

**Output:**

```
["a.b.c", "a.d", "e"]
```

Another instance with array input:

**Input:**

```
[1, {a:2, b: [3,4]}, 5]
```

**Output:**

```
["0", "1.a", "1.b.0", "1.b.1", "2"]
```

The implementation needed recursive traversal through both objects and arrays.

**Given Sudo Code:**

```
function fetchKeys(input) {   // TO DEFINE}
```

**My Solution:**

```
/** * Recursively fetches all the paths (keys) to primitive    values from a nested object or array. * * @param {Object|Array} input - The input object or array to traverse. * @returns {Array} - An array of strings,    each representing the path to a primitive value. */function fetchKeys(input) {  const result = [];  /**   * Recursive helper function to traverse the input object/array.   *   * @param {*} value - The current value being traversed.   * @param {string} path - The current path constructed so far.   */  function traverse(value, path) {    // Check if the current value is a primitive    // (string, number, boolean, null, etc.)    const isPrimitive = (val) =>      val === null || typeof val !== 'object';    // If it's a primitive, add the path to result and stop recursion    if (isPrimitive(value)) {      result.push(path);      return;    }    // If the value is an array, iterate over each element    if (Array.isArray(value)) {      value.forEach((item, index) => {        // Construct the new path with the index        const newPath = path ? `${path}.${index}` : `${index}`;        traverse(item, newPath); // Recursively traverse each item      });    } else {      // If it's an object, iterate over its keys      for (const key in value) {        if (value.hasOwnProperty(key)) {          // Construct the new path with the key          const newPath = path ? `${path}.${key}` : key;          traverse(value[key], newPath); // Recursively traverse the value        }      }    }  }  // Start traversing from the root of the input  traverse(input, '');  // Return the list of all paths to primitive values  return result;}
```

#### 2. Problem Solving: Domain Operation Simulator

You are tasked to write a function _processDomain_ Operations(operations) that processes a series of domain-related operations represented in a matrix. The function will take an input argument, which is a matrix of strings. Each row in the matrix denotes an operation. All rows are to be executed sequentially. Each operation row has max 3 string elements: OP, Domain, and IP, respectively.

**Sample Input:**

```
["PUT", "www.apple.com", "10.20.30.40"]["PUT", "jobs.apple.com", "10.20.30.50"]["PUT", "sites.google.com", "142.258.145.693"]["GET", "sample.com"]["GET", "www.apple.com"]["COUNT", "apple.com"]["COUNT", "com"]
```

**Expected Output:**

```
["404", "10.20.30.40", "2", "3"]
```

The PUT commands added entries to a domain-IP map. GET returned the IP or 404, and COUNT checked how many domains matched or ended with the queried domain.

**Given Sudo Code:**

```
function processDomainOperation(operations) {    // TO DEFINE}
```

**My Solution:**

```
/** * Processes a list of operations related to domain-IP mappings. * * Supported operations: * - PUT domain ip     → Stores the domain with the associated IP. * - GET domain        → Retrieves the IP for a given domain or    returns "404" if not found. * - COUNT domain      → Counts how many domains exist for the    exact match or subdomain. * * @param {Array} operations - An array of operations,    each as [operationType, domain, ip?]. * @returns {Array} - Result of GET and COUNT operations. */function processDomainOperation(operations) {  const map = {};  // Stores domain → IP mappings  const res = [];  // Stores the output results for GET and COUNT  for (const [op, domain, ip] of operations) {    if (op === "PUT" && domain && ip) {      // Store or update the IP for the given domain      map[domain] = ip;    } else if (op === "GET" && domain) {      // Retrieve IP if domain exists, else return "404"      res.push(map[domain] || "404");    } else if (op === "COUNT" && domain) {      // Count exact domain and its subdomains      const count = Object.keys(map).filter(d =>        d === domain || d.endsWith("." + domain)      ).length;      res.push(count.toString());  // Store count as a string    }  }  return res;}
```

#### 3. What will be the output of this code snippet?

There was a code snippet involving promises and setTimeout. The idea was to determine the order of console logs.

```
const p = new Promise((resolve) => {  console.log(1);  setTimeout(() => {    resolve();  });});Promise.resolve().then(() => console.log(2));setTimeout(() => console.log(3));p.then(() => console.log(4));setTimeout(() => console.log(5));
```

This question tested your knowledge of JavaScript's event loop, microtasks vs macrotasks, and when promises are resolved.

#### 4. What will be the output of this code snippet?

Another scenario-based question dealt with shallow copying using the spread operator and how nested objects behave when mutated.

```
let person1 = {  name: "Anil Kumar",  address: {    line1: "Patna",    line2: "Bihar"  }};let person2 = { ...person1 };person1.name = "Ravi Kumar";person1.address.line1 = "Hyderabad";console.log(person1);console.log(person2);
```

The point was to observe that while top-level properties are copied, nested objects are still referenced — hence both `person1` and `person2` reflect changes in the `address`.

#### 5. Promise Chain with then and finally

This was a more complex promise chaining example, with a mix of `.then()` and `.finally()` calls. The promise had both a reject and resolve, but only one of them would be used depending on the order of execution.

This tested how promises settle and the behavior of `.finally()` when the promise is rejected or resolved.

#### 6. What will get logged to the console?

Another code-based output question:

```
const shape = {  radius: 10,  diameter() {    return this.radius * 2;  },  perimeter: () => 2 * Math.PI * this.radius,};console.log(shape.diameter());console.log(shape.perimeter());
```

This focused on how `this` behaves differently in regular functions vs arrow functions. Arrow functions don't bind their own `this`, so `shape.perimeter()` returns `NaN`.

#### 7. What will get logged to the console?

A tricky scope-based question with a `const` inside a block:

```
function foo() {  const bar = 'bar';  if (true) {    console.log(bar);    const bar = 'bar1';  }}
```

This throws a `ReferenceError` because the variable `bar` inside the `if` block is in the temporal dead zone when the `console.log` tries to access it.

#### 8. Consider the following reducer:

They shared a reducer function and a series of dispatched actions, asking what the final state would be.

**Initial State:**

```
const initialState = {  foo: [1],  switch: false};
```

**Reducer Snippet:**

```
/** * Reducer to handle 'foo' state operations. * Supports setting a value and pushing into an array. * * @param {Object} state - The current state object. * @param {Object} action - The action dispatched. * @returns {Object} - The updated state. */function FooReducer(state = initialState, action) {  switch (action.type) {    case 'SET FOO':      // Set 'foo' to a new value, and 'switch' to true      return Object.assign({}, state, {        foo: action.foo,        switch: true      });    case 'PUSH FOO':      // Append new item to 'foo' array and toggle 'switch'      return Object.assign({}, state, {        foo: [          ...state.foo,          action.foo        ],        switch: !state.switch      });    default:      // Return current state if action type is unrecognized      return state;  }}
```

What will the state of this reducer be after the following actions are dispatched:

```
dispatch({ type: 'SET_FOO', foo: [1, 2] });dispatch({ type: 'PUSH_FOO', foo: 3 });dispatch({ type: 'PUSH_FOO', foo: 6 });
```

The final state would be something like:

```
{  foo: [1, 2, 3, 6],  switch: false}
```

#### 9. Fetching Data in a Functional Component using Hooks

You are creating a functional component where you need to retrieve data from a network resource and display it when the component loads using hooks.

How would you do this? To simplify the context, consider that you do not have to handle the case where the component would be unmounted before the data is retrieved.

Four Options were given for this problem, all were code snippets of useEffect with some tweaks.

#### 10. Which of the following statements is correct regarding React context in modern React (16.3+)

1. Context can only be accessed in class components using _this.context_
2. A React context is created using React.createContext();
3. The only way to access a context in function components is by using the Consumer component
4. Context values must always be primitive data types

Correct answer: **Option 2**

`React.createContext()` is the standard way to create context. The other options were either outdated or incorrect.

### Final Verdict

I haven't got any update on my application after this round. It's been a long time. That means it's a rejection.

Competition is so tough that even scoring 9/10 doesn't guarantee a selection; you need to be 10/10 in this current job market, which is really down.

### Looking for more frontend interviews?

If you are looking for more frontend interviews, you can check out my profile, and there are 28+ interview experiences already shared till now. You can check them as well.