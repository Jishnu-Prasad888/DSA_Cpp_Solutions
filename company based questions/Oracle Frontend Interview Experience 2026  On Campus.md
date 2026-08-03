Landing an offer from Oracle through **On-Campus Placement** was an exciting experience. The interview process was well-balanced and tested a mix of **Computer Science fundamentals, Data Structures & Algorithms, System Design thinking, problem-solving ability, and behavioral fit**.

The overall process included:

- **Online Assessment**
- **Technical Round 1**
- **Technical Round 2**
- **Managerial Round**
- **HR Round**

#### Final Verdict: Selected

Here's a detailed breakdown of the entire experience.

Interview Process Overview **Company:** Oracle **Interview Type:** On-Campus Placement **Total Rounds:** 4 Interviews (+ OA) **Difficulty Level:** Medium to Hard

#### Focus Areas:

- Core CS Fundamentals
- Data Structures & Algorithms
- Object-Oriented Programming
- SQL
- Problem Solving & Puzzles
- System Design Basics
- Behavioral & Situational Thinking

### Online Assessment (Initial Screening)

Before the interviews, there was an **Online Assessment (OA)** designed to shortlist candidates.

Typical focus areas included:

- Aptitude & logical reasoning
- Coding problems
- Basic CS concepts
- Time management

Clearing the OA moved candidates to the interview rounds.

### Round 1: Technical Interview (45 Minutes)

This round focused heavily on **core computer science fundamentals**, conceptual clarity, and basic coding ability.

The interviewer moved quickly across multiple domains, so breadth of knowledge mattered a lot.

#### 1. What is TCP and UDP?

A classic networking question.

Topics to prepare:

#### TCP (Transmission Control Protocol)

- Connection-oriented
- Reliable communication
- Error checking
- Packet acknowledgment
- Ordered delivery

Use cases:

- Web browsing
- File transfer
- Emails

#### UDP (User Datagram Protocol)

- Connectionless
- Faster
- No delivery guarantee
- No ordering guarantee
- Lightweight

Use cases:

- Video streaming
- Online gaming
- Live calls

#### 2. When Do We Use TCP vs UDP?

Interviewers often want practical reasoning.

Example answers:

Use **TCP** when:

- Data integrity matters
- Every packet must arrive
- Order matters

Use **UDP** when:

- Speed matters more than reliability
- Some packet loss is acceptable
- Real-time communication is needed

#### 3. HTTP Status Codes

A very common backend/web fundamentals question.

Important categories:

#### 2xx — Success

- 200 OK
- 201 Created

#### 3xx — Redirection

- 301 Moved Permanently
- 302 Found

#### 4xx — Client Errors

- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found

#### 5xx — Server Errors

- 500 Internal Server Error
- 503 Service Unavailable

#### 4. Puzzle: Gold Rod Payment

**Problem:**

An employee works for **7 days**.

Employer has a **gold rod of 7 equal units**.

Payment must be made **1 unit per day**.

Maximum **2 cuts allowed**.

#### Solution

Cut the rod into:

- **1 unit**
- **2 units**
- **4 units**

Daily payment strategy:

![None](https://freedium-mirror.cfd/img/700/1*AxraLcPifTX0l3wj6a3H3A.png)

This tests logical thinking more than coding.

#### 5. Different Types of Constructors

Object-Oriented Programming basics.

Important types:

- Default constructor
- Parameterized constructor
- Copy constructor
- Move constructor (in languages like C++)

Interviewers usually ask for examples.

#### 6. What is a Virtual Function?

Common in **C++** interviews.

Key idea:

A **virtual function** enables **runtime polymorphism**.

It allows derived classes to override base class behavior.

Important concepts:

- Dynamic dispatch
- VTable
- Function overriding

#### 7. Which Data Structure Do You Like Most and Why?

This was more of an opinion-based technical question.

Good answers can include:

#### HashMap

Useful because:

- Average **O(1)** lookup
- Efficient caching
- Fast insert/delete

Or:

#### Trees

Useful because:

- Hierarchical data
- Ordered traversal
- Range queries

The interviewer mainly checks reasoning.

#### 8. Explain Different Types of SQL Joins

A very common database question.

Important joins:

#### INNER JOIN

Returns matching rows from both tables.

#### LEFT JOIN

Returns all rows from the left table + matched rows from the right.

#### RIGHT JOIN

Returns all rows from the right table + matched rows from the left.

#### FULL OUTER JOIN

Returns all rows from both tables.

#### SELF JOIN

Joining a table with itself.

#### 9. Write Code for BFS Algorithm

Classic DSA question.

Expected concepts:

- Queue
- Graph traversal
- Visited array/set

Example approach:

```
function bfs(graph, start) {  const visited = new Set();  const queue = [start];  visited.add(start);  while (queue.length) {    const node = queue.shift();    console.log(node);    for (const neighbor of graph[node]) {      if (!visited.has(neighbor)) {        visited.add(neighbor);        queue.push(neighbor);      }    }  }}
```

### Hey New Readers 👋

If you're new here, make sure to check out my [Frontend Army](https://medium.com/frontend-army) publication — a collection of 50+ detailed Frontend interview experiences covering JavaScript, ReactJS, Machine Coding, System Design, DSA, and real interview insights from top tech companies.

Great resource for anyone preparing for Frontend Engineer interviews 🚀

### Round 2: Technical Interview (45 Minutes)

This round mixed DSA, system design thinking, project discussions, and tricky conceptual questions.

#### 1. String Reversal Problem

**Problem:** Reverse each word individually.

Example:

```
"Hello World" → "olleH dlroW"
```

#### Simple JavaScript Solution

```
function reverseWords(str) {  return str    .split(" ")    .map(word => word.split("").reverse().join(""))    .join(" ");}
```

#### 2. Design Tic-Tac-Toe Game

This tested:

- OOP design
- State handling
- Edge cases
- Winning condition logic

Typical classes:

```
class Board {}class Player {}class Game {}
```

Things to discuss:

- Board representation
- Turn management
- Win checking
- Draw handling
- Scalability for NxN boards

#### 3. SQL Query for Kth Minimum Salary

Very common SQL interview question.

Example:

```
SELECT DISTINCT salaryFROM employeesORDER BY salaryLIMIT 1 OFFSET k-1;
```

Alternatively, using subqueries is also worth knowing.

#### 4. Project-Related Questions

The interviewer asked:

**How would you scale your project further?**

Good discussion points:

- Caching
- Load balancing
- Database sharding
- Rate limiting
- Horizontal scaling
- CDN usage
- Monitoring

This round checks engineering maturity.

#### 5. Duplicate Class Names in JAR

Question: What happens if two classes with the same name exist inside a JAR and you call that class?

Expected discussion:

- Classpath resolution order
- ClassLoader behavior
- Namespace/package importance
- Potential ambiguity or shadowing

Very interesting Java internals question.

#### 6. Puzzle: Fair Cake Sharing

**Problem:** You took an uneven piece of cake. Now your friend arrives. How can both of you share the remaining cake equally?

#### Solution

Use the **"I cut, you choose"** principle.

One person cuts the remaining cake into what they believe are equal halves.

The other person chooses first.

This guarantees fairness.

### Round 3: Managerial Round (30 Minutes)

This round tested personality, ownership, and problem-solving under pressure.

#### 1. Tell Me Something Not in Your Resume

This is meant to understand your personality beyond technical achievements.

Good topics:

- Personal values
- Curiosity
- Discipline
- Hobbies
- Resilience

#### 2. Critical Situation Handling

**Scenario:** Your team has written **100K lines of code**.

Client reports a major issue.

The entire team is on leave.

You are the only person available.

#### Good Answer Framework

1. Stay calm
2. Reproduce issue
3. Check logs
4. Identify impact
5. Communicate transparently
6. Rollback if needed
7. Fix the root cause
8. Document learning

Interviewers evaluate:

- Ownership
- Leadership
- Communication
- Incident handling

#### 3. Explain How HashMap Works

A very common favorite.

Topics to discuss:

- Key hashing
- Buckets
- Collision handling
- Chaining/Open addressing
- Rehashing
- Load factor
- Average **O(1)** complexity

### Round 4: HR Round (5 Minutes)

Short and straightforward.

Questions included:

#### Location Preference

Be flexible if possible.

#### Are You Willing to Relocate?

Usually expected to say yes in campus placements.

#### Do You Have Other Offers?

Answer honestly.

#### Any Questions for Us?

Always ask something thoughtful, such as:

- What does success look like in this role?
- What projects would I likely work on?
- How does onboarding work?

### Final Verdict

I successfully cleared all rounds and received an offer from Oracle.

The interview process was very balanced — it wasn't only about coding, but also about:

- Core CS knowledge
- Problem-solving mindset
- Communication
- System thinking
- Behavioral maturity

### Final Thoughts

Oracle interviews can be unpredictable, but they strongly reward **conceptual clarity and calm problem-solving**.

If your fundamentals are strong and you communicate clearly, you can do very well.

Best of luck to everyone preparing! 🚀