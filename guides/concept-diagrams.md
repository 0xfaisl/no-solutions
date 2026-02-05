# Programming Concept Diagrams

A visual guide to abstract programming concepts using ASCII/text-based diagrams.

---

## Table of Contents

1. [JavaScript Event Loop](#1-javascript-event-loop)
2. [JavaScript Scope Chain](#2-javascript-scope-chain)
3. [Closure Visualization](#3-closure-visualization)
4. [Promise States](#4-promise-states)
5. [HTTP Request/Response Cycle](#5-http-requestresponse-cycle)
6. [REST API Structure](#6-rest-api-structure)
7. [React Component Tree](#7-react-component-tree)
8. [React useState Flow](#8-react-usestate-flow)
9. [React useEffect Lifecycle](#9-react-useeffect-lifecycle)
10. [SQL JOIN Visualizations](#10-sql-join-visualizations)
11. [Database Relationships](#11-database-relationships)
12. [Git Branching Model](#12-git-branching-model)
13. [MVC / Three-Layer Architecture](#13-mvc--three-layer-architecture)
14. [Authentication Flow (JWT)](#14-authentication-flow-jwt)

---

## 1. JavaScript Event Loop

The event loop is the mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              JAVASCRIPT RUNTIME                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────┐          ┌─────────────────────────────────────┐  │
│   │     CALL STACK      │          │            WEB APIs                 │  │
│   │                     │          │   (Browser/Node Environment)        │  │
│   │  ┌───────────────┐  │          │                                     │  │
│   │  │  function()   │  │  ───────▶│  • setTimeout()                     │  │
│   │  ├───────────────┤  │          │  • fetch()                          │  │
│   │  │  function()   │  │          │  • DOM Events                       │  │
│   │  ├───────────────┤  │          │  • XMLHttpRequest                   │  │
│   │  │    main()     │  │          │  • setInterval()                    │  │
│   │  └───────────────┘  │          │                                     │  │
│   │                     │          └──────────────┬──────────────────────┘  │
│   │   Executes code     │                         │                         │
│   │   synchronously     │                         │ When async operation    │
│   │   (LIFO - Last In,  │                         │ completes, callback     │
│   │    First Out)       │                         │ is pushed to queue      │
│   └─────────────────────┘                         │                         │
│            ▲                                      ▼                         │
│            │                         ┌────────────────────────────────────┐ │
│            │                         │        CALLBACK QUEUE              │ │
│            │                         │       (Task Queue)                 │ │
│            │                         │                                    │ │
│            │                         │   ┌──────┐ ┌──────┐ ┌──────┐      │ │
│            │                         │   │ cb1  │ │ cb2  │ │ cb3  │ ···  │ │
│            │                         │   └──────┘ └──────┘ └──────┘      │ │
│            │                         │                                    │ │
│            │                         │   FIFO - First In, First Out      │ │
│            │                         └──────────────┬─────────────────────┘ │
│            │                                        │                       │
│            │         ┌──────────────────────────────┘                       │
│            │         │                                                      │
│            │         ▼                                                      │
│   ┌────────┴─────────────────────────────────────────────────────────────┐  │
│   │                          EVENT LOOP                                  │  │
│   │                                                                      │  │
│   │   Continuously checks: "Is the Call Stack empty?"                    │  │
│   │                                                                      │  │
│   │   If YES → Take first callback from queue → Push to Call Stack      │  │
│   │   If NO  → Wait until stack is empty                                │  │
│   │                                                                      │  │
│   └──────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Execution Flow Example

```
console.log('1');              │  CALL STACK        │  CALLBACK QUEUE
setTimeout(() => {             │                    │
  console.log('2');            │  ┌──────────────┐  │
}, 0);                         │  │ console('1') │  │  (empty)
console.log('3');              │  └──────────────┘  │
                               │         ↓          │
Output: 1, 3, 2                │  ┌──────────────┐  │
                               │  │ setTimeout   │──┼──▶ Web API (timer)
                               │  └──────────────┘  │
                               │         ↓          │
                               │  ┌──────────────┐  │  ┌────────────┐
                               │  │ console('3') │  │  │ callback() │
                               │  └──────────────┘  │  └────────────┘
                               │         ↓          │         ↓
                               │     (empty)        │  callback moves
                               │         ↓          │  to call stack
                               │  ┌──────────────┐  │
                               │  │ console('2') │  │  (empty)
                               │  └──────────────┘  │
```

**Key Points:**
- JavaScript is single-threaded (one call stack)
- Web APIs handle async operations in the background
- Callbacks wait in the queue until the stack is empty
- The event loop moves callbacks from queue to stack

---

## 2. JavaScript Scope Chain

Scope determines where variables are accessible. JavaScript uses lexical (static) scoping.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                            GLOBAL SCOPE                                     │
│                                                                             │
│   var globalVar = "I'm global";                                             │
│   let globalLet = "Also global";                                            │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                       FUNCTION SCOPE                                │   │
│   │                                                                     │   │
│   │   function outer() {                                                │   │
│   │     var outerVar = "I'm in outer";                                  │   │
│   │     let outerLet = "Also in outer";                                 │   │
│   │                                                                     │   │
│   │     ┌───────────────────────────────────────────────────────────┐   │   │
│   │     │                    FUNCTION SCOPE                         │   │   │
│   │     │                                                           │   │   │
│   │     │   function inner() {                                      │   │   │
│   │     │     var innerVar = "I'm in inner";                        │   │   │
│   │     │                                                           │   │   │
│   │     │     ┌─────────────────────────────────────────────────┐   │   │   │
│   │     │     │              BLOCK SCOPE                        │   │   │   │
│   │     │     │                                                 │   │   │   │
│   │     │     │   if (true) {                                   │   │   │   │
│   │     │     │     let blockLet = "I'm block-scoped";          │   │   │   │
│   │     │     │     const blockConst = "Also block-scoped";     │   │   │   │
│   │     │     │     var blockVar = "I'm function-scoped!";      │   │   │   │
│   │     │     │   }                                             │   │   │   │
│   │     │     │                                                 │   │   │   │
│   │     │     └─────────────────────────────────────────────────┘   │   │   │
│   │     │   }                                                       │   │   │
│   │     │                                                           │   │   │
│   │     └───────────────────────────────────────────────────────────┘   │   │
│   │   }                                                                 │   │
│   │                                                                     │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Scope Chain Lookup

```
Variable Lookup: When a variable is referenced, JS looks up the scope chain

                    ┌─────────────┐
                    │   GLOBAL    │  ← 4. Finally check global
                    │   SCOPE     │     (ReferenceError if not found)
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   OUTER     │  ← 3. Then check outer function
                    │  FUNCTION   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   INNER     │  ← 2. Then check inner function
                    │  FUNCTION   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   BLOCK     │  ← 1. First check current block
                    │   SCOPE     │
                    └─────────────┘
                           ▲
                           │
                      myVariable   (Where is it defined?)
```

### var vs let vs const

```
┌────────────┬─────────────────┬─────────────────┬─────────────────┐
│  Keyword   │     Scope       │    Hoisting     │   Reassign      │
├────────────┼─────────────────┼─────────────────┼─────────────────┤
│    var     │   Function      │   Yes (undefined)│      Yes       │
├────────────┼─────────────────┼─────────────────┼─────────────────┤
│    let     │   Block         │   Yes (TDZ*)    │      Yes        │
├────────────┼─────────────────┼─────────────────┼─────────────────┤
│   const    │   Block         │   Yes (TDZ*)    │      No         │
└────────────┴─────────────────┴─────────────────┴─────────────────┘

*TDZ = Temporal Dead Zone (cannot access before declaration)
```

---

## 3. Closure Visualization

A closure is a function that "remembers" variables from its outer scope even after the outer function has returned.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           CLOSURE CREATION                                  │
└─────────────────────────────────────────────────────────────────────────────┘

function createCounter() {
  let count = 0;                    // Outer variable

  return function increment() {     // Inner function (closure)
    count++;
    return count;
  };
}

const counter = createCounter();    // createCounter returns and is popped off stack
counter();  // 1                    // But count is still accessible!
counter();  // 2
counter();  // 3


╔══════════════════════════════════════════════════════════════════════════════╗
║  BEFORE createCounter() returns:                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║   CALL STACK                              HEAP MEMORY                        ║
║   ┌─────────────────┐                     ┌────────────────────────────┐     ║
║   │ createCounter() │ ──────────────────▶ │  count: 0                  │     ║
║   │                 │                     │                            │     ║
║   │ returns         │                     │  increment: function() {   │     ║
║   │ increment fn    │                     │    count++;                │     ║
║   └─────────────────┘                     │    return count;           │     ║
║                                           │  }                         │     ║
║                                           └────────────────────────────┘     ║
╚══════════════════════════════════════════════════════════════════════════════╝


╔══════════════════════════════════════════════════════════════════════════════╗
║  AFTER createCounter() returns:                                              ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║   CALL STACK                              HEAP MEMORY                        ║
║   ┌─────────────────┐                                                        ║
║   │    (empty)      │                     ┌────────────────────────────┐     ║
║   └─────────────────┘                     │  count: 0    ◄─────────┐   │     ║
║                                           │                        │   │     ║
║   GLOBAL SCOPE                            │  increment: function() ┼───┘     ║
║   ┌─────────────────┐                     │  [[ Scope ]]          │   │     ║
║   │                 │                     │                        │   │     ║
║   │ counter ────────┼────────────────────▶│  }                     │   │     ║
║   │                 │                     └────────────────────────┘   │     ║
║   └─────────────────┘                              ▲                   │     ║
║                                                    │                   │     ║
║                                            CLOSURE LINK ───────────────┘     ║
║                                        (increment "closes over" count)       ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

### Practical Example: Private Variables

```
┌─────────────────────────────────────────────────────────────────┐
│                    CLOSURE AS PRIVATE STATE                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   function createBankAccount(initial) {                         │
│     let balance = initial;        // Private - cannot access    │
│                                   // from outside               │
│     return {                                                    │
│       deposit(amount) {                                         │
│         balance += amount;        // Can access via closure     │
│       },                                                        │
│       getBalance() {                                            │
│         return balance;           // Can access via closure     │
│       }                                                         │
│     };                                                          │
│   }                                                             │
│                                                                 │
│   const account = createBankAccount(100);                       │
│   account.balance;      // undefined (private!)                 │
│   account.getBalance(); // 100 (accessed via closure)           │
│   account.deposit(50);                                          │
│   account.getBalance(); // 150                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4. Promise States

Promises represent eventual completion (or failure) of an async operation.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PROMISE STATES                                    │
└─────────────────────────────────────────────────────────────────────────────┘

                              ┌─────────────────┐
                              │                 │
                              │    PENDING      │
                              │                 │
                              │  (Initial State)│
                              │                 │
                              └────────┬────────┘
                                       │
                                       │
              ┌────────────────────────┼────────────────────────┐
              │                        │                        │
              │ resolve(value)         │         reject(error)  │
              │                        │                        │
              ▼                        │                        ▼
    ┌─────────────────┐                │              ┌─────────────────┐
    │                 │                │              │                 │
    │   FULFILLED     │                │              │    REJECTED     │
    │                 │                │              │                 │
    │  (Success!)     │                │              │   (Error!)      │
    │                 │                │              │                 │
    └────────┬────────┘                │              └────────┬────────┘
             │                         │                       │
             │                         │                       │
             ▼                         ▼                       ▼
         .then()                   SETTLED                 .catch()
                               (Cannot change
                                state again)
```

### Promise Chaining

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         PROMISE CHAIN FLOW                                  │
└─────────────────────────────────────────────────────────────────────────────┘

fetch('/api/user')
  .then(response => response.json())
  .then(user => fetch(`/api/posts/${user.id}`))
  .then(response => response.json())
  .then(posts => console.log(posts))
  .catch(error => console.error(error))
  .finally(() => console.log('Done'));


    ┌──────────────┐
    │   fetch()    │
    │  (Promise)   │
    └──────┬───────┘
           │
           ▼ returns Promise
    ┌──────────────┐
    │   .then()    │───────▶ response.json()
    │              │
    └──────┬───────┘
           │
           ▼ returns Promise
    ┌──────────────┐
    │   .then()    │───────▶ fetch user posts
    │              │
    └──────┬───────┘
           │
           ▼ returns Promise
    ┌──────────────┐
    │   .then()    │───────▶ response.json()
    │              │
    └──────┬───────┘
           │
           ▼ returns Promise
    ┌──────────────┐
    │   .then()    │───────▶ console.log(posts)
    │              │
    └──────┬───────┘
           │
           │◄───────────────────────────────────────────┐
           │         If ANY promise rejects,            │
           ▼         error flows here                   │
    ┌──────────────┐                                    │
    │   .catch()   │───────▶ Handle all errors ─────────┘
    │              │
    └──────┬───────┘
           │
           ▼ Always runs
    ┌──────────────┐
    │  .finally()  │───────▶ Cleanup (runs success or failure)
    │              │
    └──────────────┘
```

### async/await (Syntactic Sugar)

```
// Promise chain                    // async/await equivalent
fetch('/api/user')                  async function getData() {
  .then(res => res.json())            try {
  .then(user => {                       const res = await fetch('/api/user');
    return fetch(`/api/${user.id}`)     const user = await res.json();
  })                                    const posts = await fetch(`/api/${user.id}`);
  .then(res => res.json())              const data = await posts.json();
  .catch(err => console.error(err))     return data;
                                      } catch (err) {
                                        console.error(err);
                                      }
                                    }
```

---

## 5. HTTP Request/Response Cycle

The HTTP cycle is the foundation of web communication.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      HTTP REQUEST/RESPONSE CYCLE                            │
└─────────────────────────────────────────────────────────────────────────────┘


    ┌──────────────────┐                              ┌──────────────────┐
    │                  │                              │                  │
    │     CLIENT       │                              │     SERVER       │
    │   (Browser)      │                              │   (Backend)      │
    │                  │                              │                  │
    └────────┬─────────┘                              └────────┬─────────┘
             │                                                 │
             │  1. HTTP REQUEST                                │
             │ ──────────────────────────────────────────────▶ │
             │                                                 │
             │  ┌─────────────────────────────────────────┐    │
             │  │ GET /api/users HTTP/1.1                 │    │
             │  │ Host: api.example.com                   │    │
             │  │ Authorization: Bearer token123          │    │
             │  │ Content-Type: application/json          │    │
             │  │ Accept: application/json                │    │
             │  │                                         │    │
             │  │ {                                       │    │
             │  │   "name": "John",                       │    │
             │  │   "email": "john@example.com"           │    │
             │  │ }                                       │    │
             │  └─────────────────────────────────────────┘    │
             │                                                 │
             │                                                 │  2. Server
             │                                                 │     Processes
             │                                                 │     Request
             │                                                 │
             │  3. HTTP RESPONSE                               │
             │ ◀────────────────────────────────────────────── │
             │                                                 │
             │  ┌─────────────────────────────────────────┐    │
             │  │ HTTP/1.1 200 OK                         │    │
             │  │ Content-Type: application/json          │    │
             │  │ Cache-Control: max-age=3600             │    │
             │  │ X-Request-Id: abc123                    │    │
             │  │                                         │    │
             │  │ {                                       │    │
             │  │   "id": 1,                              │    │
             │  │   "name": "John",                       │    │
             │  │   "email": "john@example.com"           │    │
             │  │ }                                       │    │
             │  └─────────────────────────────────────────┘    │
             │                                                 │
             ▼                                                 ▼
```

### Request Structure

```
┌─────────────────────────────────────────────────────────────┐
│                    HTTP REQUEST ANATOMY                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │              REQUEST LINE                           │   │
│   │  METHOD   PATH          VERSION                     │   │
│   │   GET    /api/users    HTTP/1.1                     │   │
│   └─────────────────────────────────────────────────────┘   │
│                         │                                   │
│   ┌─────────────────────▼───────────────────────────────┐   │
│   │              HEADERS                                │   │
│   │  Host: api.example.com                              │   │
│   │  User-Agent: Mozilla/5.0                            │   │
│   │  Authorization: Bearer eyJhbG...                    │   │
│   │  Content-Type: application/json                     │   │
│   │  Accept: application/json                           │   │
│   └─────────────────────────────────────────────────────┘   │
│                         │                                   │
│   ┌─────────────────────▼───────────────────────────────┐   │
│   │              BODY (optional)                        │   │
│   │  {                                                  │   │
│   │    "username": "john_doe",                          │   │
│   │    "password": "secret123"                          │   │
│   │  }                                                  │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Common Status Codes

```
┌────────┬──────────────────────┬──────────────────────────────────────┐
│  Code  │       Category       │            Meaning                   │
├────────┼──────────────────────┼──────────────────────────────────────┤
│  1xx   │   Informational      │  Request received, continuing        │
├────────┼──────────────────────┼──────────────────────────────────────┤
│  200   │   Success            │  OK - Request succeeded              │
│  201   │   Success            │  Created - Resource created          │
│  204   │   Success            │  No Content - Success, no body       │
├────────┼──────────────────────┼──────────────────────────────────────┤
│  301   │   Redirection        │  Moved Permanently                   │
│  302   │   Redirection        │  Found (Temporary Redirect)          │
│  304   │   Redirection        │  Not Modified (use cache)            │
├────────┼──────────────────────┼──────────────────────────────────────┤
│  400   │   Client Error       │  Bad Request - Invalid syntax        │
│  401   │   Client Error       │  Unauthorized - Auth required        │
│  403   │   Client Error       │  Forbidden - No permission           │
│  404   │   Client Error       │  Not Found - Resource missing        │
│  422   │   Client Error       │  Unprocessable Entity - Validation   │
├────────┼──────────────────────┼──────────────────────────────────────┤
│  500   │   Server Error       │  Internal Server Error               │
│  502   │   Server Error       │  Bad Gateway                         │
│  503   │   Server Error       │  Service Unavailable                 │
└────────┴──────────────────────┴──────────────────────────────────────┘
```

---

## 6. REST API Structure

REST (Representational State Transfer) uses HTTP methods to perform CRUD operations on resources.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    REST API - RESOURCE-BASED URLs                           │
└─────────────────────────────────────────────────────────────────────────────┘


    HTTP Method + URL Path = Action on Resource

    ┌──────────┬─────────────────────┬──────────────────────────────────────┐
    │  Method  │      URL            │         Action (CRUD)                │
    ├──────────┼─────────────────────┼──────────────────────────────────────┤
    │  GET     │  /users             │  READ - Get all users                │
    │  GET     │  /users/123         │  READ - Get user with id 123         │
    │  POST    │  /users             │  CREATE - Create new user            │
    │  PUT     │  /users/123         │  UPDATE - Replace user 123           │
    │  PATCH   │  /users/123         │  UPDATE - Partial update user 123    │
    │  DELETE  │  /users/123         │  DELETE - Remove user 123            │
    └──────────┴─────────────────────┴──────────────────────────────────────┘


                        ┌─────────────────────────┐
                        │       RESOURCE          │
                        │       /users            │
                        └────────────┬────────────┘
                                     │
         ┌───────────────────────────┼───────────────────────────┐
         │                           │                           │
         ▼                           ▼                           ▼
    ┌─────────┐               ┌─────────────┐              ┌─────────────┐
    │  GET    │               │    POST     │              │   GET       │
    │ /users  │               │   /users    │              │ /users/123  │
    │         │               │             │              │             │
    │ List    │               │  Create     │              │  Get One    │
    │ All     │               │  New        │              │             │
    └─────────┘               └─────────────┘              └──────┬──────┘
                                                                  │
                                     ┌────────────────────────────┼────────┐
                                     │                            │        │
                                     ▼                            ▼        ▼
                              ┌─────────────┐              ┌────────┐ ┌────────┐
                              │    PUT      │              │ PATCH  │ │ DELETE │
                              │ /users/123  │              │/users/ │ │/users/ │
                              │             │              │  123   │ │  123   │
                              │  Replace    │              │Partial │ │ Remove │
                              │  Entire     │              │ Update │ │        │
                              └─────────────┘              └────────┘ └────────┘
```

### Nested Resources

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       NESTED RESOURCE URLS                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   /users/123/posts              →  All posts by user 123                    │
│   /users/123/posts/456          →  Post 456 by user 123                     │
│   /users/123/posts/456/comments →  All comments on post 456                 │
│                                                                             │
│                                                                             │
│              ┌────────────┐                                                 │
│              │   User     │                                                 │
│              │   /users   │                                                 │
│              └─────┬──────┘                                                 │
│                    │                                                        │
│           ┌────────┴────────┐                                               │
│           │                 │                                               │
│           ▼                 ▼                                               │
│    ┌────────────┐    ┌────────────┐                                         │
│    │   Posts    │    │  Profile   │                                         │
│    │/users/     │    │ /users/    │                                         │
│    │ :id/posts  │    │ :id/profile│                                         │
│    └─────┬──────┘    └────────────┘                                         │
│          │                                                                  │
│          ▼                                                                  │
│   ┌────────────┐                                                            │
│   │  Comments  │                                                            │
│   │ /users/:id/│                                                            │
│   │ posts/:pid/│                                                            │
│   │ comments   │                                                            │
│   └────────────┘                                                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### REST Best Practices

```
┌──────────────────────────────────────────────────────────────────────────┐
│                        REST API BEST PRACTICES                           │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ✓ Use nouns for resources:     /users, /posts, /comments                │
│  ✗ Avoid verbs:                 /getUsers, /createPost                   │
│                                                                          │
│  ✓ Use plural nouns:            /users/123                               │
│  ✗ Avoid singular:              /user/123                                │
│                                                                          │
│  ✓ Use kebab-case:              /user-profiles                           │
│  ✗ Avoid camelCase:             /userProfiles                            │
│                                                                          │
│  ✓ Use query params for         /users?status=active&sort=name           │
│    filtering/sorting:                                                    │
│                                                                          │
│  ✓ Version your API:            /api/v1/users                            │
│                                                                          │
│  ✓ Return appropriate           201 for created, 204 for deleted         │
│    status codes:                                                         │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 7. React Component Tree

React applications are structured as a tree of components with data flowing down via props.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        REACT COMPONENT TREE                                 │
└─────────────────────────────────────────────────────────────────────────────┘


                            ┌─────────────────┐
                            │      App        │
                            │   (Root)        │
                            │                 │
                            │ state: {        │
                            │   user: {...},  │
                            │   theme: 'dark' │
                            │ }               │
                            └────────┬────────┘
                                     │
                  ┌──────────────────┼──────────────────┐
                  │                  │                  │
                  │ props: {user}    │ props: {theme}   │ props: {user}
                  ▼                  ▼                  ▼
         ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
         │   Header    │    │   Sidebar   │    │   Content   │
         │             │    │             │    │             │
         │ Displays    │    │ Navigation  │    │ Main area   │
         │ user info   │    │ links       │    │             │
         └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
                │                  │                  │
                │                  │                  │
                ▼                  ▼                  ▼
         ┌───────────┐      ┌───────────┐      ┌───────────┐
         │  Avatar   │      │  NavLink  │      │  Article  │
         │           │      │  NavLink  │      │  Article  │
         │  Logo     │      │  NavLink  │      │  Article  │
         └───────────┘      └───────────┘      └───────────┘


    DATA FLOWS DOWN (Props)              EVENTS FLOW UP (Callbacks)

    ┌──────────┐                         ┌──────────┐
    │  Parent  │                         │  Parent  │
    │          │                         │          │
    │ state: x │                         │ setState │◀─────┐
    └────┬─────┘                         └──────────┘      │
         │                                                 │
         │ props={{                                        │ onClick()
         │   value: x,                                     │
         │   onChange: fn                                  │
         │ }}                                              │
         ▼                                                 │
    ┌──────────┐                         ┌──────────┐      │
    │  Child   │                         │  Child   │──────┘
    │          │                         │          │
    │ {value}  │                         │  Button  │
    └──────────┘                         └──────────┘
```

### Re-render Cascade

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    STATE CHANGE TRIGGERS RE-RENDER                          │
└─────────────────────────────────────────────────────────────────────────────┘

                    setState() called here
                            │
                            ▼
                    ┌─────────────┐
                    │     App     │  ←── RE-RENDERS
                    │  state: {   │
                    │   count: 1  │  (state changed)
                    │  }          │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
        ┌─────────┐  ┌─────────┐  ┌─────────┐
        │ Header  │  │ Counter │  │ Footer  │
        │         │  │         │  │         │
        └────┬────┘  └────┬────┘  └────┬────┘
             │            │            │
             ▼            ▼            ▼
          RE-RENDERS   RE-RENDERS   RE-RENDERS
         (child of     (receives   (child of
          parent)      new props)   parent)


    OPTIMIZATION: Use React.memo() to skip re-renders when props haven't changed

        ┌─────────┐
        │ Footer  │  ←── React.memo(Footer)
        │         │
        └─────────┘
             │
             ▼
         SKIPPED!
        (props same)
```

---

## 8. React useState Flow

useState provides a state variable and a function to update it.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         useState FLOW                                       │
└─────────────────────────────────────────────────────────────────────────────┘


    const [count, setCount] = useState(0);
           │        │               │
           │        │               └── Initial value (only used on first render)
           │        │
           │        └── Setter function (triggers re-render)
           │
           └── Current state value


╔═══════════════════════════════════════════════════════════════════════════╗
║   INITIAL RENDER                                                          ║
╠═══════════════════════════════════════════════════════════════════════════╣
║                                                                           ║
║      useState(0)                                                          ║
║          │                                                                ║
║          ▼                                                                ║
║   ┌─────────────┐         ┌─────────────────────────────────────────┐     ║
║   │ React       │         │  Component renders with count = 0      │     ║
║   │ creates     │ ──────▶ │                                         │     ║
║   │ state slot  │         │  <p>Count: 0</p>                        │     ║
║   │ value: 0    │         │  <button onClick={() => setCount(1)}>  │     ║
║   └─────────────┘         └─────────────────────────────────────────┘     ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝


╔═══════════════════════════════════════════════════════════════════════════╗
║   STATE UPDATE                                                            ║
╠═══════════════════════════════════════════════════════════════════════════╣
║                                                                           ║
║      User clicks button                                                   ║
║          │                                                                ║
║          ▼                                                                ║
║   ┌─────────────┐         ┌─────────────────────────────────────────┐     ║
║   │ setCount(1) │         │  React schedules re-render              │     ║
║   │ called      │ ──────▶ │                                         │     ║
║   │             │         │  (state update is async/batched)        │     ║
║   └─────────────┘         └──────────────────┬──────────────────────┘     ║
║                                              │                            ║
║                                              ▼                            ║
║                           ┌─────────────────────────────────────────┐     ║
║                           │  Component re-renders with count = 1   │     ║
║                           │                                         │     ║
║                           │  <p>Count: 1</p>                        │     ║
║                           │  <button onClick={() => setCount(2)}>  │     ║
║                           └─────────────────────────────────────────┘     ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

### Functional Updates

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FUNCTIONAL vs DIRECT UPDATES                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   DIRECT UPDATE (uses stale value in rapid updates):                        │
│                                                                             │
│   setCount(count + 1);  // count is captured at render time                 │
│   setCount(count + 1);  // same stale value!                                │
│   setCount(count + 1);  // Result: only +1, not +3                          │
│                                                                             │
│                                                                             │
│   FUNCTIONAL UPDATE (always uses latest value):                             │
│                                                                             │
│   setCount(prev => prev + 1);  // prev is always current                    │
│   setCount(prev => prev + 1);  // gets updated value                        │
│   setCount(prev => prev + 1);  // Result: +3 as expected                    │
│                                                                             │
│                                                                             │
│   Timeline:                                                                 │
│                                                                             │
│   count = 0                                                                 │
│       │                                                                     │
│       │  setCount(prev => prev + 1)                                         │
│       ├─────────────────────────────▶  queued: 0 + 1 = 1                    │
│       │                                                                     │
│       │  setCount(prev => prev + 1)                                         │
│       ├─────────────────────────────▶  queued: 1 + 1 = 2                    │
│       │                                                                     │
│       │  setCount(prev => prev + 1)                                         │
│       ├─────────────────────────────▶  queued: 2 + 1 = 3                    │
│       │                                                                     │
│       ▼  Re-render                                                          │
│   count = 3                                                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 9. React useEffect Lifecycle

useEffect handles side effects in functional components.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       useEffect LIFECYCLE                                   │
└─────────────────────────────────────────────────────────────────────────────┘


   useEffect(() => {
     // Effect code (runs after render)

     return () => {
       // Cleanup code (runs before next effect or unmount)
     };
   }, [dependencies]);


╔═══════════════════════════════════════════════════════════════════════════╗
║                         COMPONENT LIFECYCLE                                ║
╠═══════════════════════════════════════════════════════════════════════════╣
║                                                                           ║
║   MOUNT                    UPDATE                      UNMOUNT            ║
║     │                        │                           │                ║
║     ▼                        ▼                           ▼                ║
║  ┌───────┐               ┌───────┐                   ┌───────┐           ║
║  │Render │               │Render │                   │Cleanup│           ║
║  │  DOM  │               │  DOM  │                   │ runs  │           ║
║  └───┬───┘               └───┬───┘                   └───────┘           ║
║      │                       │                                           ║
║      ▼                       ▼                                           ║
║  ┌───────┐               ┌───────┐                                       ║
║  │Effect │               │Cleanup│ (from previous effect)                ║
║  │ runs  │               │ runs  │                                       ║
║  └───────┘               └───┬───┘                                       ║
║                              │                                           ║
║                              ▼                                           ║
║                          ┌───────┐                                       ║
║                          │Effect │                                       ║
║                          │ runs  │                                       ║
║                          └───────┘                                       ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

### Dependency Array Behavior

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     DEPENDENCY ARRAY PATTERNS                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   useEffect(() => {...});        // Runs after EVERY render                 │
│                                                                             │
│   Mount   Render   Render   Render                                          │
│     │       │        │        │                                             │
│     ▼       ▼        ▼        ▼                                             │
│   [Run]   [Run]    [Run]    [Run]   ← Effect runs each time                 │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   useEffect(() => {...}, []);    // Runs ONLY on mount                      │
│                                                                             │
│   Mount   Render   Render   Render                                          │
│     │       │        │        │                                             │
│     ▼       │        │        │                                             │
│   [Run]     ·        ·        ·     ← Effect runs once                      │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   useEffect(() => {...}, [dep]); // Runs when dep changes                   │
│                                                                             │
│   Mount   dep:1    dep:1    dep:2                                           │
│     │       │        │        │                                             │
│     ▼       │        │        ▼                                             │
│   [Run]     ·        ·      [Run]   ← Effect runs on mount + when dep       │
│                                       changes                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Common useEffect Patterns

```
// Data fetching
useEffect(() => {
  let cancelled = false;              ┌─────────────────────────────────┐
                                      │  Mount                          │
  async function fetchData() {        │    │                            │
    const data = await fetch(url);    │    ▼                            │
    if (!cancelled) {                 │  fetch() starts                 │
      setData(data);                  │    │                            │
    }                                 │    ▼                            │
  }                                   │  if still mounted → setData     │
                                      │                                 │
  fetchData();                        │  Unmount before fetch returns?  │
                                      │    │                            │
  return () => {                      │    ▼                            │
    cancelled = true;  // Cleanup     │  cancelled = true (no setData)  │
  };                                  └─────────────────────────────────┘
}, [url]);


// Event listener
useEffect(() => {                     ┌─────────────────────────────────┐
  function handleResize() {           │  Mount                          │
    setWidth(window.innerWidth);      │    │                            │
  }                                   │    ▼                            │
                                      │  addEventListener               │
  window.addEventListener(            │    │                            │
    'resize',                         │    │   User resizes window      │
    handleResize                      │    │         │                  │
  );                                  │    │         ▼                  │
                                      │    │   handleResize fires       │
  return () => {                      │    │                            │
    window.removeEventListener(       │  Unmount                        │
      'resize',                       │    │                            │
      handleResize                    │    ▼                            │
    );                                │  removeEventListener            │
  };                                  └─────────────────────────────────┘
}, []);
```

---

## 10. SQL JOIN Visualizations

JOINs combine rows from two or more tables based on related columns.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          SQL JOIN TYPES                                     │
└─────────────────────────────────────────────────────────────────────────────┘


    TABLE A (users)                    TABLE B (orders)
    ┌────┬───────┐                     ┌────┬─────────┬─────────┐
    │ id │ name  │                     │ id │ user_id │ product │
    ├────┼───────┤                     ├────┼─────────┼─────────┤
    │ 1  │ Alice │                     │ 1  │    1    │ Laptop  │
    │ 2  │ Bob   │                     │ 2  │    1    │ Mouse   │
    │ 3  │ Carol │                     │ 3  │    3    │ Monitor │
    │ 4  │ Dave  │                     │ 4  │    5    │ Keyboard│
    └────┴───────┘                     └────┴─────────┴─────────┘

    Note: Dave (id=4) has no orders
          Order 4 references user_id=5 (doesn't exist)


    ═══════════════════════════════════════════════════════════════════════

    INNER JOIN - Only matching rows from both tables

    SELECT * FROM users u INNER JOIN orders o ON u.id = o.user_id

         ┌───────────────────────┐
         │   ┌───────────────┐   │
         │   │               │   │
    ┌────┴───┴───┐       ┌───┴───┴────┐
    │   TABLE A  │       │   TABLE B  │
    │            │░░░░░░░│            │
    │   users    │░░░░░░░│   orders   │
    │            │░░░░░░░│            │
    └────────────┘       └────────────┘
                  ▲
                  │
           Only this part
           (matching rows)

    Result:
    ┌────┬───────┬────┬─────────┬─────────┐
    │ id │ name  │ id │ user_id │ product │
    ├────┼───────┼────┼─────────┼─────────┤
    │ 1  │ Alice │ 1  │    1    │ Laptop  │
    │ 1  │ Alice │ 2  │    1    │ Mouse   │
    │ 3  │ Carol │ 3  │    3    │ Monitor │
    └────┴───────┴────┴─────────┴─────────┘


    ═══════════════════════════════════════════════════════════════════════

    LEFT JOIN - All from left table + matching from right

    SELECT * FROM users u LEFT JOIN orders o ON u.id = o.user_id

    ┌────────────────────────────┐
    │                            │
    │   ┌─────────────────────┐  │
    │   │           │         │  │
    ┌───┴───────────┴──┐  ┌───┴──┴────┐
    │░░░TABLE A░░░░░░░░│  │   TABLE B  │
    │░░░░░░░░░░░░░░░░░░│░░│            │
    │░░░users░░░░░░░░░░│░░│   orders   │
    │░░░░░░░░░░░░░░░░░░│  │            │
    └──────────────────┘  └────────────┘
     ▲
     │
    All left rows + matching right rows

    Result:
    ┌────┬───────┬──────┬─────────┬─────────┐
    │ id │ name  │  id  │ user_id │ product │
    ├────┼───────┼──────┼─────────┼─────────┤
    │ 1  │ Alice │  1   │    1    │ Laptop  │
    │ 1  │ Alice │  2   │    1    │ Mouse   │
    │ 2  │ Bob   │ NULL │  NULL   │ NULL    │  ← No matching order
    │ 3  │ Carol │  3   │    3    │ Monitor │
    │ 4  │ Dave  │ NULL │  NULL   │ NULL    │  ← No matching order
    └────┴───────┴──────┴─────────┴─────────┘


    ═══════════════════════════════════════════════════════════════════════

    RIGHT JOIN - All from right table + matching from left

    SELECT * FROM users u RIGHT JOIN orders o ON u.id = o.user_id

              ┌────────────────────────────┐
              │                            │
              │  ┌─────────────────────┐   │
              │  │         │           │   │
    ┌─────────┴──┴──┐  ┌───┴───────────┴───┐
    │   TABLE A     │  │░░░TABLE B░░░░░░░░░│
    │               │░░│░░░░░░░░░░░░░░░░░░░│
    │   users       │░░│░░░orders░░░░░░░░░░│
    │               │  │░░░░░░░░░░░░░░░░░░░│
    └───────────────┘  └───────────────────┘
                                          ▲
                                          │
              Matching left rows + all right rows

    Result:
    ┌──────┬───────┬────┬─────────┬──────────┐
    │  id  │ name  │ id │ user_id │ product  │
    ├──────┼───────┼────┼─────────┼──────────┤
    │  1   │ Alice │ 1  │    1    │ Laptop   │
    │  1   │ Alice │ 2  │    1    │ Mouse    │
    │  3   │ Carol │ 3  │    3    │ Monitor  │
    │ NULL │ NULL  │ 4  │    5    │ Keyboard │  ← No matching user
    └──────┴───────┴────┴─────────┴──────────┘


    ═══════════════════════════════════════════════════════════════════════

    FULL OUTER JOIN - All rows from both tables

    SELECT * FROM users u FULL OUTER JOIN orders o ON u.id = o.user_id

    ┌────────────────────────────────────────┐
    │                                        │
    │   ┌──────────────────────────────┐     │
    │   │              │               │     │
    ┌───┴──────────────┴────┐  ┌───────┴─────┴───┐
    │░░░░░TABLE A░░░░░░░░░░░│  │░░░░TABLE B░░░░░░│
    │░░░░░░░░░░░░░░░░░░░░░░░│░░│░░░░░░░░░░░░░░░░░│
    │░░░░░users░░░░░░░░░░░░░│░░│░░░orders░░░░░░░░│
    │░░░░░░░░░░░░░░░░░░░░░░░│  │░░░░░░░░░░░░░░░░░│
    └───────────────────────┘  └─────────────────┘
     ▲                                          ▲
     │                                          │
     └──────────── All rows from both ──────────┘

    Result:
    ┌──────┬───────┬──────┬─────────┬──────────┐
    │  id  │ name  │  id  │ user_id │ product  │
    ├──────┼───────┼──────┼─────────┼──────────┤
    │  1   │ Alice │  1   │    1    │ Laptop   │
    │  1   │ Alice │  2   │    1    │ Mouse    │
    │  2   │ Bob   │ NULL │  NULL   │ NULL     │  ← No matching order
    │  3   │ Carol │  3   │    3    │ Monitor  │
    │  4   │ Dave  │ NULL │  NULL   │ NULL     │  ← No matching order
    │ NULL │ NULL  │  4   │    5    │ Keyboard │  ← No matching user
    └──────┴───────┴──────┴─────────┴──────────┘
```

---

## 11. Database Relationships

Database relationships define how tables are connected to each other.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       DATABASE RELATIONSHIPS                                │
└─────────────────────────────────────────────────────────────────────────────┘


═══════════════════════════════════════════════════════════════════════════════
                           ONE-TO-ONE (1:1)
═══════════════════════════════════════════════════════════════════════════════

    Each user has exactly one profile.
    Each profile belongs to exactly one user.

    ┌──────────────────┐         ┌──────────────────┐
    │      USERS       │         │     PROFILES     │
    ├──────────────────┤         ├──────────────────┤
    │ id (PK)          │────────▶│ id (PK)          │
    │ email            │    1:1  │ user_id (FK, UQ) │◀── Unique constraint
    │ password         │         │ bio              │    ensures 1:1
    └──────────────────┘         │ avatar_url       │
                                 └──────────────────┘

    Example:
    ┌────┬─────────────────┐     ┌────┬─────────┬───────────────┐
    │ id │ email           │     │ id │ user_id │ bio           │
    ├────┼─────────────────┤     ├────┼─────────┼───────────────┤
    │ 1  │ alice@mail.com  │────▶│ 1  │    1    │ "Hello!"      │
    │ 2  │ bob@mail.com    │────▶│ 2  │    2    │ "Hi there"    │
    └────┴─────────────────┘     └────┴─────────┴───────────────┘


═══════════════════════════════════════════════════════════════════════════════
                          ONE-TO-MANY (1:N)
═══════════════════════════════════════════════════════════════════════════════

    One user can have many posts.
    Each post belongs to exactly one user.

    ┌──────────────────┐         ┌──────────────────┐
    │      USERS       │         │      POSTS       │
    ├──────────────────┤         ├──────────────────┤
    │ id (PK)          │◀───┐    │ id (PK)          │
    │ name             │    │    │ user_id (FK)     │────┘
    │ email            │    └────│ title            │
    └──────────────────┘   1:N   │ content          │
                                 └──────────────────┘

    Example:
    ┌────┬───────┐           ┌────┬─────────┬──────────────────┐
    │ id │ name  │           │ id │ user_id │ title            │
    ├────┼───────┤           ├────┼─────────┼──────────────────┤
    │ 1  │ Alice │◀──────────│ 1  │    1    │ "First Post"     │
    │    │       │◀──────────│ 2  │    1    │ "Second Post"    │
    │    │       │◀──────────│ 3  │    1    │ "Third Post"     │
    │ 2  │ Bob   │◀──────────│ 4  │    2    │ "Bob's Post"     │
    └────┴───────┘           └────┴─────────┴──────────────────┘


═══════════════════════════════════════════════════════════════════════════════
                         MANY-TO-MANY (N:N)
═══════════════════════════════════════════════════════════════════════════════

    A student can enroll in many courses.
    A course can have many students.
    Requires a JOIN TABLE (junction/bridge table).

    ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
    │    STUDENTS      │     │  ENROLLMENTS     │     │     COURSES      │
    ├──────────────────┤     │   (Join Table)   │     ├──────────────────┤
    │ id (PK)          │◀───┐├──────────────────┤┌───▶│ id (PK)          │
    │ name             │    ││ student_id (FK)  ││    │ name             │
    │ email            │    └┤ course_id (FK)   ├┘    │ credits          │
    └──────────────────┘     │ enrolled_at      │     └──────────────────┘
                             │ grade            │
                             └──────────────────┘

    Example:
    STUDENTS              ENROLLMENTS              COURSES
    ┌────┬───────┐        ┌────────────┬───────────┐        ┌────┬─────────┐
    │ id │ name  │        │ student_id │ course_id │        │ id │ name    │
    ├────┼───────┤        ├────────────┼───────────┤        ├────┼─────────┤
    │ 1  │ Alice │◀───────│     1      │     1     │───────▶│ 1  │ Math    │
    │    │       │◀───────│     1      │     2     │───────▶│ 2  │ Physics │
    │ 2  │ Bob   │◀───────│     2      │     1     │───────▶│    │         │
    │    │       │◀───────│     2      │     3     │───────▶│ 3  │ History │
    └────┴───────┘        └────────────┴───────────┘        └────┴─────────┘

    Alice is in: Math, Physics
    Bob is in: Math, History
    Math has: Alice, Bob


═══════════════════════════════════════════════════════════════════════════════
                        SELF-REFERENCING
═══════════════════════════════════════════════════════════════════════════════

    An employee can have a manager who is also an employee.

    ┌──────────────────────────────────┐
    │           EMPLOYEES              │
    ├──────────────────────────────────┤
    │ id (PK)                          │
    │ name                             │
    │ manager_id (FK) ─────────────────┼───┐
    │                                  │   │
    └──────────────────────────────────┘   │
                    ▲                      │
                    └──────────────────────┘
                      References itself

    Example:
    ┌────┬─────────┬────────────┐
    │ id │ name    │ manager_id │
    ├────┼─────────┼────────────┤
    │ 1  │ CEO     │ NULL       │  ← No manager (top level)
    │ 2  │ Manager │ 1          │  ← Reports to CEO
    │ 3  │ Dev 1   │ 2          │  ← Reports to Manager
    │ 4  │ Dev 2   │ 2          │  ← Reports to Manager
    └────┴─────────┴────────────┘

              CEO (1)
               │
           Manager (2)
            /      \
        Dev 1 (3)  Dev 2 (4)
```

---

## 12. Git Branching Model

Git branches allow parallel development and feature isolation.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        GIT BRANCHING MODEL                                  │
└─────────────────────────────────────────────────────────────────────────────┘


═══════════════════════════════════════════════════════════════════════════════
                           BASIC BRANCHING
═══════════════════════════════════════════════════════════════════════════════

    main        ●───●───●───●───●───●───●───●───●
                        │       ▲       ▲
                        │       │       │
    feature-a           └───●───●───●───┘
                                │
                        branch  │  merge
                        created │  completed


═══════════════════════════════════════════════════════════════════════════════
                        FEATURE BRANCH WORKFLOW
═══════════════════════════════════════════════════════════════════════════════

    main          ●───────────●───────────────────●───────────●
                  │           ▲                   ▲           │
                  │           │ merge             │ merge     │
                  │           │                   │           │
    feature/      └───●───●───┘                   │           │
    login                                         │           │
                                                  │           │
    feature/              ┌───●───●───●───●───────┘           │
    signup                │                                   │
                          │                                   │
    main                  ●───────────────────────────────────●
                          │
                          │  (feature/signup branched
                          │   from this point)


═══════════════════════════════════════════════════════════════════════════════
                        GITFLOW BRANCHING MODEL
═══════════════════════════════════════════════════════════════════════════════

    production     ●─────────────────────●─────────────────────●  (tags: v1.0, v1.1)
    (main)         │                     ▲                     ▲
                   │                     │                     │
    release        │           ●───●───●─┘           ●───●───●─┘
                   │           ▲                     ▲
                   │           │                     │
    develop        ●───●───●───●───●───●───●───●───●───●───●───●
                   │       ▲       │       ▲       │
                   │       │       │       │       │
    feature/       └───●───┘       └───●───┘       │
    branches                                       │
                                                   │
    hotfix                                         └───●───●───▶ (emergency fix
                                                               to production)


═══════════════════════════════════════════════════════════════════════════════
                            MERGE STRATEGIES
═══════════════════════════════════════════════════════════════════════════════

    FAST-FORWARD MERGE (linear history, no merge commit)

    Before:
    main      ●───●───●
                      │
    feature           └───●───●───●  (HEAD)

    After (git merge feature):
    main      ●───●───●───●───●───●  (HEAD)
                          │
                   feature commits are
                   now on main


    THREE-WAY MERGE (creates merge commit)

    Before:
    main      ●───●───●───●───●  (has new commits)
                      │
    feature           └───●───●───●  (also has commits)

    After (git merge feature):
    main      ●───●───●───●───●───◆  (HEAD)
                      │           │
    feature           └───●───●───┘
                                  │
                           merge commit
                           (combines both)


    REBASE (replays commits on new base)

    Before:
    main      ●───●───●───●───●
                      │
    feature           └───●───●───●

    After (git rebase main) on feature:
    main      ●───●───●───●───●
                              │
    feature                   └───●'──●'──●'
                                  │
                           commits are replayed
                           (new commit hashes)
```

### Common Git Commands

```
┌────────────────────────────────────────────────────────────────────────────┐
│                       GIT COMMAND REFERENCE                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  git branch feature/new    Create new branch                               │
│  git checkout feature/new  Switch to branch                                │
│  git checkout -b feature   Create AND switch (shortcut)                    │
│                                                                            │
│  git merge feature         Merge feature into current branch               │
│  git rebase main           Replay current branch on top of main            │
│                                                                            │
│  git branch -d feature     Delete branch (safe - only if merged)           │
│  git branch -D feature     Force delete branch                             │
│                                                                            │
│  git push origin feature   Push branch to remote                           │
│  git push -u origin feat   Push and set upstream tracking                  │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 13. MVC / Three-Layer Architecture

The Model-View-Controller pattern separates concerns in application design.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     MVC ARCHITECTURE                                        │
└─────────────────────────────────────────────────────────────────────────────┘


    ┌─────────────────────────────────────────────────────────────────────────┐
    │                              USER                                       │
    └─────────────────────────────────┬───────────────────────────────────────┘
                                      │
                                      │ Interacts with
                                      ▼
    ╔═════════════════════════════════════════════════════════════════════════╗
    ║                              VIEW                                       ║
    ║                                                                         ║
    ║   • User Interface (HTML, CSS, React components)                        ║
    ║   • Displays data to user                                               ║
    ║   • Sends user actions to Controller                                    ║
    ║                                                                         ║
    ╚════════════════════════════════╤════════════════════════════════════════╝
                                     │
                   ┌─────────────────┴─────────────────┐
                   │                                   │
        User input │                                   │ Updated data
                   ▼                                   │
    ╔══════════════════════════════════╗               │
    ║          CONTROLLER              ║               │
    ║                                  ║               │
    ║  • Handles user requests         ║               │
    ║  • Contains business logic       ║               │
    ║  • Coordinates Model and View    ║               │
    ║  • Routes, middleware            ║               │
    ║                                  ║               │
    ╚═══════════════╤══════════════════╝               │
                    │                                  │
      Request data  │                                  │
                    ▼                                  │
    ╔══════════════════════════════════╗               │
    ║            MODEL                 ║               │
    ║                                  ║               │
    ║  • Data and business rules       ║───────────────┘
    ║  • Database interactions         ║  Returns data
    ║  • Data validation               ║
    ║  • ORM entities                  ║
    ║                                  ║
    ╚══════════════════════════════════╝


═══════════════════════════════════════════════════════════════════════════════
                    THREE-LAYER / N-TIER ARCHITECTURE
═══════════════════════════════════════════════════════════════════════════════


    ┌─────────────────────────────────────────────────────────────────────────┐
    │                         USER / CLIENT                                   │
    │                     (Browser, Mobile App)                               │
    └─────────────────────────────────┬───────────────────────────────────────┘
                                      │
                                      │ HTTP Request
                                      ▼
    ╔═════════════════════════════════════════════════════════════════════════╗
    ║                     PRESENTATION LAYER                                  ║
    ║                        (Frontend)                                       ║
    ║  ┌───────────────────────────────────────────────────────────────────┐  ║
    ║  │  • React / Vue / Angular components                               │  ║
    ║  │  • HTML / CSS / JavaScript                                        │  ║
    ║  │  • User interface logic                                           │  ║
    ║  │  • Form validation (client-side)                                  │  ║
    ║  │  • API calls to backend                                           │  ║
    ║  └───────────────────────────────────────────────────────────────────┘  ║
    ╚════════════════════════════════╤════════════════════════════════════════╝
                                     │
                                     │ API Request (REST/GraphQL)
                                     ▼
    ╔═════════════════════════════════════════════════════════════════════════╗
    ║                      BUSINESS LOGIC LAYER                               ║
    ║                         (Backend)                                       ║
    ║  ┌───────────────────────────────────────────────────────────────────┐  ║
    ║  │  • Express / Django / Spring controllers                          │  ║
    ║  │  • Authentication & Authorization                                 │  ║
    ║  │  • Business rules and validation                                  │  ║
    ║  │  • Data transformation                                            │  ║
    ║  │  • External API integrations                                      │  ║
    ║  └───────────────────────────────────────────────────────────────────┘  ║
    ╚════════════════════════════════╤════════════════════════════════════════╝
                                     │
                                     │ Database Query (SQL/NoSQL)
                                     ▼
    ╔═════════════════════════════════════════════════════════════════════════╗
    ║                       DATA ACCESS LAYER                                 ║
    ║                        (Database)                                       ║
    ║  ┌───────────────────────────────────────────────────────────────────┐  ║
    ║  │  • PostgreSQL / MySQL / MongoDB                                   │  ║
    ║  │  • ORM (Sequelize, Prisma, TypeORM)                               │  ║
    ║  │  • Data persistence                                               │  ║
    ║  │  • Queries and transactions                                       │  ║
    ║  │  • Caching (Redis)                                                │  ║
    ║  └───────────────────────────────────────────────────────────────────┘  ║
    ╚═════════════════════════════════════════════════════════════════════════╝


═══════════════════════════════════════════════════════════════════════════════
                          REQUEST FLOW EXAMPLE
═══════════════════════════════════════════════════════════════════════════════

    User clicks "Submit Order" button

    FRONTEND                    BACKEND                     DATABASE
    (React)                     (Express)                   (PostgreSQL)
       │                           │                            │
       │  POST /api/orders         │                            │
       │  {items: [...]}           │                            │
       │ ─────────────────────────▶│                            │
       │                           │                            │
       │                           │  Validate request          │
       │                           │  Check user auth           │
       │                           │  Apply business rules      │
       │                           │                            │
       │                           │  INSERT INTO orders...     │
       │                           │ ───────────────────────────▶
       │                           │                            │
       │                           │  ◀─── { id: 123, ... }     │
       │                           │                            │
       │  ◀─── 201 Created         │                            │
       │       { orderId: 123 }    │                            │
       │                           │                            │
       │  Update UI                │                            │
       │  Show success message     │                            │
       ▼                           ▼                            ▼
```

---

## 14. Authentication Flow (JWT)

JSON Web Tokens (JWT) enable stateless authentication.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        JWT AUTHENTICATION FLOW                              │
└─────────────────────────────────────────────────────────────────────────────┘


═══════════════════════════════════════════════════════════════════════════════
                           INITIAL LOGIN
═══════════════════════════════════════════════════════════════════════════════

    CLIENT                          SERVER                         DATABASE
       │                              │                                │
       │  1. POST /login              │                                │
       │     {email, password}        │                                │
       │ ────────────────────────────▶│                                │
       │                              │                                │
       │                              │  2. Query user by email        │
       │                              │ ───────────────────────────────▶
       │                              │                                │
       │                              │  3. User found                 │
       │                              │ ◀───────────────────────────────
       │                              │                                │
       │                              │  4. Verify password            │
       │                              │     (bcrypt.compare)           │
       │                              │                                │
       │                              │  5. Generate JWT               │
       │                              │     ┌───────────────────────┐  │
       │                              │     │ HEADER.PAYLOAD.SIG    │  │
       │                              │     └───────────────────────┘  │
       │                              │                                │
       │  6. Return token             │                                │
       │ ◀────────────────────────────│                                │
       │     {token: "eyJhbG..."}     │                                │
       │                              │                                │
       │  7. Store token              │                                │
       │     (localStorage or         │                                │
       │      httpOnly cookie)        │                                │
       ▼                              ▼                                ▼


═══════════════════════════════════════════════════════════════════════════════
                      AUTHENTICATED REQUESTS
═══════════════════════════════════════════════════════════════════════════════

    CLIENT                          SERVER
       │                              │
       │  GET /api/profile            │
       │  Authorization: Bearer eyJ...│
       │ ────────────────────────────▶│
       │                              │
       │                              │  1. Extract token from header
       │                              │
       │                              │  2. Verify JWT signature
       │                              │     ┌─────────────────────────┐
       │                              │     │ jwt.verify(token,       │
       │                              │     │   SECRET_KEY)           │
       │                              │     └─────────────────────────┘
       │                              │
       │                              │  3. Check expiration (exp claim)
       │                              │
       │                              │  4. Token valid → extract user data
       │                              │     {userId: 123, role: "user"}
       │                              │
       │  5. Return protected data    │
       │ ◀────────────────────────────│
       │     {name: "Alice", ...}     │
       │                              │
       ▼                              ▼


═══════════════════════════════════════════════════════════════════════════════
                          JWT STRUCTURE
═══════════════════════════════════════════════════════════════════════════════

    eyJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOjEyM30.SflKxwRJSMeKKF2QT4fwpM
    ──────────────────── ─────────────────────── ─────────────────────────
           HEADER              PAYLOAD                 SIGNATURE
           (Base64)            (Base64)                (Base64)


    ┌─────────────────────────────────────────────────────────────────────────┐
    │  HEADER                                                                 │
    │  {                                                                      │
    │    "alg": "HS256",         // Signing algorithm                         │
    │    "typ": "JWT"            // Token type                                │
    │  }                                                                      │
    ├─────────────────────────────────────────────────────────────────────────┤
    │  PAYLOAD (Claims)                                                       │
    │  {                                                                      │
    │    "sub": "1234567890",    // Subject (user ID)                         │
    │    "name": "Alice",        // Custom claim                              │
    │    "role": "admin",        // Custom claim                              │
    │    "iat": 1516239022,      // Issued at (timestamp)                     │
    │    "exp": 1516242622       // Expiration (timestamp)                    │
    │  }                                                                      │
    ├─────────────────────────────────────────────────────────────────────────┤
    │  SIGNATURE                                                              │
    │                                                                         │
    │  HMACSHA256(                                                            │
    │    base64UrlEncode(header) + "." + base64UrlEncode(payload),            │
    │    SECRET_KEY                                                           │
    │  )                                                                      │
    │                                                                         │
    │  → Ensures token hasn't been tampered with                              │
    │  → Only server with SECRET_KEY can create valid tokens                  │
    └─────────────────────────────────────────────────────────────────────────┘


═══════════════════════════════════════════════════════════════════════════════
                      TOKEN REFRESH FLOW
═══════════════════════════════════════════════════════════════════════════════

    Access Token:  Short-lived (15 min - 1 hour)
    Refresh Token: Long-lived (7 days - 30 days)

    CLIENT                          SERVER
       │                              │
       │  Access token expires        │
       │                              │
       │  POST /refresh               │
       │  {refreshToken: "..."}       │
       │ ────────────────────────────▶│
       │                              │
       │                              │  Verify refresh token
       │                              │  Check if not revoked
       │                              │
       │  New access token            │
       │ ◀────────────────────────────│
       │  {accessToken: "eyJ..."}     │
       │                              │
       ▼                              ▼


═══════════════════════════════════════════════════════════════════════════════
                        LOGOUT FLOW
═══════════════════════════════════════════════════════════════════════════════

    CLIENT                          SERVER                       DATABASE
       │                              │                              │
       │  POST /logout                │                              │
       │ ────────────────────────────▶│                              │
       │                              │                              │
       │                              │  Add token to blacklist      │
       │                              │  (or delete refresh token)   │
       │                              │ ─────────────────────────────▶
       │                              │                              │
       │  Clear local token           │                              │
       │  ┌─────────────────────┐     │                              │
       │  │ localStorage.remove │     │                              │
       │  │ ('token')           │     │                              │
       │  └─────────────────────┘     │                              │
       │                              │                              │
       │  Redirect to login           │                              │
       ▼                              ▼                              ▼
```

### Security Best Practices

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     JWT SECURITY BEST PRACTICES                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  DO:                                                                        │
│  ✓ Use HTTPS for all requests                                               │
│  ✓ Set short expiration times for access tokens                             │
│  ✓ Store tokens in httpOnly cookies (prevents XSS access)                   │
│  ✓ Use strong, unique secret keys                                           │
│  ✓ Implement refresh token rotation                                         │
│  ✓ Validate all claims (exp, iss, aud)                                      │
│                                                                             │
│  DON'T:                                                                     │
│  ✗ Store sensitive data in JWT payload (it's base64, not encrypted)         │
│  ✗ Use weak secrets or hardcode them in code                                │
│  ✗ Store tokens in localStorage (vulnerable to XSS)                         │
│  ✗ Create tokens that never expire                                          │
│  ✗ Ignore token validation on the server                                    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Quick Reference: When to Use What

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CONCEPT QUICK REFERENCE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Need to...                              Look at diagram for...             │
│                                                                             │
│  Understand async code timing     →      Event Loop (#1)                    │
│  Debug variable access issues     →      Scope Chain (#2)                   │
│  Create private state/factory     →      Closures (#3)                      │
│  Handle async operations          →      Promises (#4)                      │
│  Debug API calls                  →      HTTP Cycle (#5)                    │
│  Design API endpoints             →      REST Structure (#6)                │
│  Structure React app              →      Component Tree (#7)                │
│  Manage React state               →      useState Flow (#8)                 │
│  Handle side effects              →      useEffect Lifecycle (#9)           │
│  Combine database tables          →      SQL JOINs (#10)                    │
│  Design database schema           →      DB Relationships (#11)             │
│  Manage code versions             →      Git Branching (#12)                │
│  Architect full-stack app         →      MVC Architecture (#13)             │
│  Implement login system           →      JWT Auth Flow (#14)                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

*These diagrams are designed to be viewed in a monospace font for proper alignment.*
