Recently, I went through multiple frontend interview experiences for a **Senior Software Engineer — Frontend** role at Paytm Money and found the process extremely interesting because it focused heavily on **practical frontend engineering skills rather than only DSA**.

The interviews evaluated:

- JavaScript fundamentals
- ReactJS concepts
- Machine coding
- API handling
- Custom hooks
- Frontend system design
- Performance optimization
- Browser concepts
- Problem-solving ability

This article combines experiences from multiple candidates and gives a complete overview of what you can expect during frontend interviews at Paytm Money.

### Interview Overview

**Role:** Senior Software Engineer — Frontend **Location:** Bangalore **Experience Range:** 2.5+ Years

### Interview Process

- Online Assessment
- JavaScript & React Rounds
- Machine Coding
- Frontend Design Discussion

### Online Assessment Round

The first round was an online assessment containing:

- JavaScript MCQs
- DOM-related questions
- ReactJS fundamentals
- Basic CSS concepts
- One DSA problem

Another candidate also mentioned:

- Basic jQuery questions
- JavaScript output-based questions
- CSS positioning concepts

### Topics Asked in OA

#### JavaScript

Focus on:

- Closures
- Hoisting
- Event loop
- Promise outputs
- Array methods
- Prototype concepts

#### ReactJS

Questions included:

- React lifecycle
- Hooks
- Re-rendering
- State vs props
- Virtual DOM

#### CSS

Typical topics:

- Flexbox
- Positioning
- z-index
- Centering elements

### Round 1: JavaScript + React + Machine Coding

This round focused on JavaScript fundamentals along with practical React implementation.

#### 1. What is Currying?

One of the first questions asked was:

#### Explain Currying in JavaScript

Currying is a technique where:

- A function takes one argument at a time
- Returns another function

Example:

```
function sum(a) {  return function(b) {    return function(c) {      return a + b + c;    };  };}console.log(sum(1)(2)(3));
```

#### 2. Implement func(1)(2)(3)…()

This was an extension of currying.

The interviewer expected:

- Closures
- Function chaining
- Dynamic arguments

This problem is very common in frontend interviews nowadays.

#### 3. Machine Coding: Stopwatch in React

One of the major tasks was:

#### Create a Stopwatch in React with:

- Start button
- Pause button
- Restart button

This round tested:

- React hooks
- State management
- setInterval handling
- Cleanup logic

Important concepts expected:

- `useState`
- `useEffect`
- Interval cleanup
- Preventing memory leaks

#### Common Follow-Up Questions

- How would you optimize re-renders?
- What happens if cleanup is not handled?
- Why useEffect dependency array matter?

#### 4. Questions on HTTP Methods

Basic frontend networking questions were asked:

#### Common HTTP Methods

![None](https://freedium-mirror.cfd/img/700/1*tTZ2_Lv7IZ7H7tmiOK3pdA.png)

Interviewers may also ask:

- Idempotency
- Safe methods
- REST principles

#### 5. Questions on Webpack

Webpack-related concepts were discussed:

Topics included:

- Bundling
- Tree shaking
- Code splitting
- Loaders
- Plugins

Very important frontend optimization topic.

#### 6. React Internal Working

The interviewer asked:

- How React re-rendering works
- Virtual DOM
- Diffing algorithm
- Reconciliation

This is a very common senior frontend topic.

#### 7. Multiple Ways to Center a Div

Classic frontend interview question.

Expected approaches:

- Flexbox
- Grid
- Position absolute + transform
- Margin auto

Example using Flexbox:

```
.container {  display: flex;  justify-content: center;  align-items: center;}
```

### Hey New Readers 👋

If you're new here, make sure to check out my [Frontend Army](https://medium.com/frontend-army) publication — a collection of 50+ detailed Frontend interview experiences covering JavaScript, ReactJS, Machine Coding, System Design, DSA, and real interview insights from top tech companies.

Great resource for anyone preparing for Frontend Engineer interviews 🚀

### Round 2: JavaScript Coding + React Machine Coding

This round was more implementation-heavy.

#### 1. Merge Two Sorted Lists

Classic DSA problem.

Expected concepts:

- Two pointers
- Array traversal
- Time complexity optimization

#### 2. Create Autocomplete with Debounce in React

This was one of the most important machine coding questions.

Requirements:

- Search input
- API calling
- Debouncing
- Suggestion dropdown

The interviewer evaluated:

- API handling
- Performance optimization
- State management
- User experience

#### Debouncing Concept

Debouncing helps:

- Reduce API calls
- Improve performance
- Prevent unnecessary renders

Example idea:

```
function debounce(fn, delay) {  let timer;  return function(...args) {    clearTimeout(timer);    timer = setTimeout(() => {      fn(...args);    }, delay);  };}
```

### Another Candidate's JavaScript Round Experience

One candidate was given:

#### Fake JSON API Task

Requirements:

- Consume API
- Render table UI
- Implement sorting
- Implement searching

This round focused heavily on:

- Async JavaScript
- Fetch API
- DOM rendering
- State updates
- UI handling

#### Promise Output Questions

The interviewer asked several:

- Promise chaining outputs
- Async execution order
- Microtask queue behavior

You must prepare:

- Event loop
- Promise resolution
- Async/await internals

#### Polyfill Question: Implement Polyfill for Array Sort

This round tested:

- JavaScript internals
- Prototype understanding
- Algorithm implementation

Polyfills are extremely common in frontend interviews now.

### Round 3: Frontend Design & Advanced React

This round focused more on frontend architecture and React expertise.

### 1. Create a Custom React Hook

**Question:** Create a hook that executes on every render except the first render

This tested:

- Hook internals
- useRef
- useEffect understanding

Typical approach:

```
function useDidUpdate(callback, deps) {  const isFirstRender = useRef(true);  useEffect(() => {    if (isFirstRender.current) {      isFirstRender.current = false;      return;    }    callback();  }, deps);}
```

#### 2. Questions on useCallback & useMemo

Very important React optimization concepts.

Interviewers asked:

- The difference between them
- When to use each
- Memoization tradeoffs
- Preventing unnecessary renders

#### 3. Questions on Redux Saga

Topics discussed:

- Side-effect management
- Generators
- takeLatest
- takeEvery
- Async flow handling

This is frequently asked in large-scale frontend companies.

#### 4. Design a LinkedIn Feed

This was the frontend system design question.

Requirements:

- Show posts/feed
- Hover over username
- Show tooltip with user info

This round tested:

- Component architecture
- State management
- Tooltip positioning
- Performance handling
- Scalability thinking

### Final Thoughts

The interview process at Paytm Money was heavily focused on practical frontend engineering instead of only theoretical DSA.

What stood out most:

- Real-world React coding
- JavaScript depth
- API handling
- UI performance
- Frontend architecture

If you're preparing for senior frontend roles, focus not only on React components but also:

- JavaScript internals
- Browser behavior
- Rendering optimization
- Scalable UI architecture

Those areas make a massive difference during interviews at top product companies.