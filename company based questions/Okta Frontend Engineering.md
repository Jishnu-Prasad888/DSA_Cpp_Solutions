### Interview Overview

**Company:** Okta **Role:** Software Development Engineer 2 (Frontend) **Experience Level:** SDE-2 **Interview Mode:** Online **Verdict:** Rejected

### Round 1: ReactJS & JavaScript Deep Dive

The first round consisted of a React machine coding exercise followed by an extensive JavaScript discussion.

#### React Machine Coding Problem

#### Dynamic Grid with Incremental Values

The interviewer provided a pre-configured React environment and asked me to build a dynamic grid application.

#### Problem Statement

The application should accept a number **n** from an input box and render an **n × n grid**.

#### Grid Behavior

Initially:

- All cells are empty

When clicking an empty cell:

- Fill it with `max(existingValues) + 1`

When clicking an already filled cell:

- Update it with `max(existingValues)`

### Example

Initial State:

```
_ _ __ _ __ _ _
```

Click the first cell:

```
1 _ __ _ __ _ _
```

Click another empty cell:

```
1 2 __ _ __ _ _
```

Click the first cell again:

```
2 2 __ _ __ _ _
```

#### What The Interviewer Was Evaluating

This question looked simple initially, but the real evaluation criteria were much deeper.

#### React Fundamentals

- Component architecture
- State management
- Event handling
- Rendering logic

#### Performance Optimization

The interviewer specifically discussed:

- Avoiding unnecessary re-renders
- Efficient computation of maximum values
- Derived state vs stored state
- React rendering behavior

#### Code Structure

The interviewer expected:

- Modular components
- Clean separation of concerns
- Readable code
- Scalable implementation

One important lesson from this round was that interviewers often care more about design decisions and trade-offs than simply producing a working solution.

#### JavaScript Deep Dive

After the React exercise, the discussion shifted entirely toward JavaScript fundamentals.

This section was significantly more challenging than the coding problem itself.

### Topics Covered

#### Event Loop

Questions included:

- How JavaScript executes code
- Call stack behavior
- Callback queue
- Event loop execution order

#### Microtasks vs Macrotasks

Discussion around:

```
Promise.resolve().then(...)setTimeout(...)
```

Questions focused on:

- Execution order
- Why Promises execute before timers
- How microtask queues are processed

#### Async vs Defer

The interviewer asked:

- What happens when a browser encounters script tag
- Difference between async and defer
- Impact on page rendering

#### Async/Await vs Then/Catch

Topics discussed:

- Internal working of async functions
- Promise wrapping
- Error propagation
- Readability vs implementation

#### Memory Management

This was one of the areas where the discussion became deeper.

Questions included:

- Garbage Collection
- Memory leaks
- Closures causing retained memory
- Detached DOM nodes
- Common memory issues in frontend applications

#### Debouncing & Throttling

The interviewer wasn't interested in textbook definitions.

Instead, they asked:

- Real-world use cases
- Search bars
- Infinite scrolling
- Resize handlers
- API optimization

#### Synchronous vs Asynchronous APIs

Discussion included:

- Browser APIs
- Network requests
- Rendering behavior
- Thread blocking

#### Browser Internals

The interviewer explored:

- What happens after an API call
- How browsers process asynchronous tasks
- Interaction between JavaScript runtime and browser APIs

### Hey New Readers 👋

If you're new here, make sure to check out my [Frontend Army](https://medium.com/frontend-army) publication, which is a collection of 55+ detailed Frontend interview experiences covering JavaScript, ReactJS, Machine Coding, System Design, DSA, and real interview insights from top tech companies.

Great resource for anyone preparing for Frontend Engineer interviews 🚀

### Round 2: Frontend System Design

The second round focused on frontend architecture and scalability.

#### Problem Statement

Design a content publishing platform where:

#### Admins

Can:

- Create articles
- Publish articles
- Store content as Markdown files

#### Users

Can:

- Browse articles
- Search content
- Read articles efficiently

The platform should be scalable and performant.

#### Discussion Areas

The interviewer intentionally kept the requirements broad and expected me to drive the discussion.

#### Role-Based Access Control

Different permissions for:

#### Admins

- Create content
- Edit content
- Publish content

#### Readers

- Read-only access

Discussion involved:

- Authentication
- Authorization
- Access boundaries

#### Markdown Storage & Rendering

The interviewer explored:

- Why Markdown was chosen
- Rendering approaches
- Security concerns
- Content processing strategies

#### Client-Side vs Server-Side Rendering

We discussed trade-offs between:

#### CSR

Advantages:

- Faster interactions
- Simpler deployments

Challenges:

- SEO

#### SSR

Advantages:

- Better SEO
- Faster initial content visibility

Challenges:

- Higher server cost

#### CDN Discussion

An interesting discussion involved whether CDN usage is even necessary for Markdown-based content.

Topics covered:

- Static asset delivery
- Edge caching
- Performance gains
- Cost considerations

#### SEO & Discoverability

Questions included:

- How search engines discover articles
- Sitemap generation
- Indexing strategies
- Metadata handling

#### Feed Delivery & Pagination

Discussion around:

- Infinite scroll
- Pagination
- Content fetching strategies
- Caching mechanisms

#### Capacity Estimation

The interviewer also asked for rough estimates around:

- Daily article creation
- Average Markdown size
- Concurrent readers
- Traffic expectations

The goal wasn't perfect numbers.

The goal was to understand how engineers reason about scale.

### Final Verdict

Unfortunately, I was not selected for the next stage.

Although the React implementation and system design discussion went reasonably well, the primary feedback was around JavaScript fundamentals.

The interviewers were looking for deeper expertise in:

- Async execution
- Event Loop
- Promise internals
- Memory management
- Browser behavior

### Final Thoughts

The Okta SDE-2 Frontend interview process was a strong reminder that senior frontend engineering is much more than building React components.

Modern frontend interviews increasingly focus on:

- JavaScript internals
- Browser behavior
- Performance engineering
- System Design
- Architectural thinking

If you're preparing for SDE-2 Frontend roles, invest significant time in mastering JavaScript fundamentals. In many cases, that knowledge becomes the deciding factor between clearing and missing the next round.