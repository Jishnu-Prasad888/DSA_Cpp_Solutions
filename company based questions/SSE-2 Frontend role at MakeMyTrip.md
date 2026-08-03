Recently, I came across an interesting interview experience for an **SSE-2 Frontend role** at MakeMyTrip, and honestly, this was one of the most practical frontend interview processes I have seen.

Unlike interviews that focus heavily only on DSA, this process evaluated:

- JavaScript fundamentals
- Async programming
- ReactJS architecture
- Machine coding
- Low-Level Design (LLD)
- UI state management
- Debugging skills
- Performance optimization

The overall process had **4 rounds**, and every round focused on real frontend engineering problems.

Unfortunately, the final verdict was **rejected**, but the interview questions themselves were extremely valuable for frontend preparation.

### Interview Overview

**Company:** MakeMyTrip **Role:** SSE-2

Interview Focus Areas

- JavaScript
- ReactJS
- Async Programming
- Machine Coding
- UI Architecture
- LLD
- Debugging & Optimization

### Round 1: JavaScript & Async Programming

This round was heavily focused on:

- JavaScript internals
- Recursive thinking
- Async behavior
- Promise handling
- React fundamentals

#### Question 1: Flatten Nested Array

Problem Statement

```
Input: [1, [2, 3], [4, [5, 6]]]Output: [1, 2, 3, 4, 5, 6]
```

The interviewer asked to implement:

- With recursion
- Without recursion

#### Recursive Approach

These tests:

- DFS thinking
- Recursive traversal
- Array handling

```
function flatten(arr) {  let result = [];  for (const item of arr) {      if (Array.isArray(item)) {        result = result.concat(flatten(item));      } else {        result.push(item);      }  }  return result;}
```

#### Iterative Approach (Without Recursion)

This evaluates:

- Stack usage
- Iterative DFS/BFS understanding

```
function flattenIterative(arr) {  const stack = [...arr];  const result = [];  while (stack.length) {    const item = stack.pop();    if (Array.isArray(item)) {      stack.push(...item);    } else {      result.unshift(item);    }  }  return result;}
```

#### Question 2: Implement promiseAllSync without async/await

This was one of the most interesting questions.

The interviewer provided:

```
const getPromiseByIndex = (index) => {  switch (index) {    case 0:      return Promise.resolve(6);    case 1:      return new Promise((resolve) => {        setTimeout(() => {          resolve("done");        }, 2000);      });    case 2:      return new Promise((resolve) => {        setTimeout(() => {          resolve("success");        }, 4000);      });    case 3:      return Promise.resolve(Date.now());  }  return null;};
```

Task:

- Complete `promiseAllSync`
- No `async/await`

#### Concepts Being Tested

This problem evaluates:

- Promise chaining
- Sequential execution
- Closure handling
- Async flow control
- Understanding of Promise APIs

#### Typical Solution Idea:

```
function promiseAllSync(total) {  const results = [];  return new Promise((resolve, reject) => {    let chain = Promise.resolve();    for (let i = 0; i < total; i++) {      chain = chain        .then(() => getPromiseByIndex(i))        .then((data) => {          results.push(data);        });    }    chain      .then(() => resolve(results))      .catch(reject);  });}
```

#### Question 3: Search Bar in React

Requirements:

- User types in search input
- API calls happen dynamically
- Show the list of products
- Minimum 3 characters required

API:

```
fetch('https://dummyjson.com/products/search?q=phone')
```

#### What Interviewers Evaluate Here

This is a very common frontend machine coding question.

Expected concepts:

- Debouncing
- API handling
- Controlled components
- Loading states
- Error handling
- Race condition handling

#### Important Optimization

Avoid API calls on every keystroke.

Typically solved using:

- Debounce
- Throttle
- AbortController

### Hey New Readers 👋

If you're new here, make sure to check out my [Frontend Army](https://medium.com/frontend-army) publication — a collection of 50+ detailed Frontend interview experiences covering JavaScript, ReactJS, Machine Coding, System Design, DSA, and real interview insights from top tech companies.

Great resource for anyone preparing for Frontend Engineer interviews 🚀

### Round 2: Machine Coding / LLD

This round was entirely focused on practical React architecture and UI state management.

#### Question 1: Sequential Progress Bars

Problem Statement: Build a React feature where:

- Clicking Add creates a new progress bar
- Bars fill sequentially
- Only one bar runs at a time
- Each bar takes ~2000ms
- Multiple clicks should queue bars

#### Concepts Being Evaluated

This question was actually much deeper than it initially looked.

Interviewers checked:

- Queue handling
- React state management
- Timers
- Sequential execution
- Side effect management

#### Important Architecture Thinking

A good approach includes:

- Queue data structure
- Active index tracking
- useEffect for progress updates
- Cleanup handling

#### Edge Cases

Interviewers also expect:

- Prevent memory leaks
- Handle rapid Add clicks
- Avoid stale state updates

#### Question 2: File Explorer in React

This was one of the best frontend LLD questions.

Requirements:

- Create `src` root folder
- Add nested folders/files
- Expand/collapse folders
- Recursive rendering
- Arbitrary nesting
- File selection highlighting

#### What This Round Evaluates

This problem checks:

- Recursive components
- Tree structures
- Component architecture
- State normalization
- UI scalability

#### Important Frontend Concepts

#### Recursive Components

Very important React interview topic.

Example structure:

```
function Folder({ node }) {  return (    <div>      <h4>{node.name}</h4>      {node.children?.map(child => (        <Folder key={child.id} node={child} />      ))}    </div>  );}
```

#### Data Structure Expected

Most candidates use:

```
{  id,  type: "folder",  name: "src",  children: []}
```

### Round 3: Advanced JavaScript + UI Components

This round focused on:

- Closures
- Currying
- Bind/Call/Apply
- React component architecture

#### Question 1: Dynamic Sum Generator

Problem:

```
const sum = generateSum(4);console.log(sum(1)(2)(3)(4)); // 10
```

Also:

- Rewrite using bind/call/apply
- Use `this`

#### Concepts Being Tested

This evaluates:

- Closures
- Currying
- Function chaining
- `this` binding
- Higher-order functions

#### Important JavaScript Areas

Must know deeply:

- `bind`
- `call`
- `apply`
- Arrow functions
- Context binding

#### Question 2: Pagination Component

Requirements:

```
<Pagination  currPage={1}  totalPage={10}  onPageClick={() => {}}/>
```

Rules:

- Show:
- First page
- Last page
- Current page
- Current ±1 page
- Show ... for gaps

#### Example Cases

Current Page = 1

```
1 2 ... 10
```

Current Page = 5

```
1 ... 4 5 6 ... 10
```

Current Page = 9

```
1 ... 8 9 10
```

#### What Interviewers Evaluate

This problem tests:

- Conditional rendering
- Edge case handling
- UI logic
- Component abstraction

### Round 4: Hiring Manager / Debugging Round

This was the most interesting and toughest round.

The interviewer shared:

- Existing codebase/repo
- Bugs/issues
- Performance problems

Task:

- Find issues
- Optimize code
- Fix bottlenecks

#### Reality of Senior Frontend Interviews

At senior frontend levels:

- Debugging speed matters A LOT
- Performance understanding matters
- Code reading skills matter more than writing fresh code sometimes

#### Follow-Up Question

The interviewer asked:

- Write a debug logger middleware
- Integrate with existing code

This was completed quickly.

However, the interviewer had already decided based on the debugging speed in the first problem.

#### Important Learning From This Interview

One major takeaway:

#### Senior Frontend Interviews Are Time Sensitive

Sometimes:

- The correct solution is not enough
- Speed matters heavily
- Debugging ability becomes the deciding factor

Especially in:

- Product companies
- Large frontend teams
- High-scale applications

### Final Thoughts

The interview process at MakeMyTrip was genuinely frontend-focused and practical.

What stood out most:

- Real-world UI problems
- JavaScript depth
- React architecture
- Debugging under pressure

Even though the final verdict was rejection, the interview itself provided excellent learning opportunities:

- Time management
- Debugging speed
- Frontend scalability
- Practical React engineering

If you're targeting SSE-2 frontend roles, definitely prepare beyond just DSA.

Focus heavily on:

- Machine coding
- Debugging
- React architecture
- Async JavaScript
- Performance optimization

Those areas are becoming the real differentiators in modern frontend interviews.