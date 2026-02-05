# Module 2: JavaScript & Web Basics

**Duration:** 6 weeks (1-2 hours/day)

**Philosophy:** Build-Your-Own-X approach. Heavy labs. No solutions provided. Struggle, experiment, and learn through doing.

**Prerequisites:** Module 1 completed (Dev Environment & Git Fundamentals)

---

## Why ES6+ and Web Basics?

Before diving into React, you need a solid foundation. This section explains why we cover what we cover.

### Why Modern JavaScript (ES6+) Over Older Syntax?

- **Readability:** Arrow functions, template literals, and destructuring make code cleaner and more expressive. Compare `function(x) { return x * 2; }` to `x => x * 2`.
- **Fewer Bugs:** `let` and `const` have block scope, eliminating entire categories of bugs caused by `var`'s function scope and hoisting quirks.
- **Industry Standard:** Every modern codebase, tutorial, and job posting assumes ES6+ knowledge. Legacy syntax is maintenance code, not new development.
- **React Requires It:** React components use arrow functions, destructuring props, spread operators, and modules constantly. You cannot write modern React without ES6+.
- **Better Async Handling:** Promises and async/await replace callback hell with readable, maintainable asynchronous code.

### Why Learn HTML/CSS Before React?

- **React Outputs HTML:** JSX is syntactic sugar for creating HTML elements. If you don't understand semantic HTML, your React apps will have accessibility and SEO problems.
- **CSS Still Applies:** React doesn't replace CSS. Whether you use CSS modules, styled-components, or Tailwind, you need to understand selectors, specificity, flexbox, and responsive design.
- **Debugging Skills:** When your React component doesn't look right, you need to inspect the DOM and understand what CSS rules are being applied.
- **Appreciation for React:** Building interactive UIs with vanilla JavaScript is tedious. Experiencing this pain helps you understand what React solves.

### Why Async Is Critical to Understand?

- **Real Apps Fetch Data:** Every non-trivial application loads data from APIs. You cannot build useful apps without understanding async operations.
- **React Hooks Require It:** `useEffect` for data fetching, handling loading/error states, and cleanup all require solid async fundamentals.
- **Common Source of Bugs:** Race conditions, stale closures, and improper error handling cause subtle bugs. Understanding async deeply prevents these.
- **Interview Staple:** Async JavaScript questions appear in nearly every frontend interview. Promises, async/await, and the event loop are expected knowledge.

---

## Learning Objectives

By the end of this module, you will be able to:
- Structure semantic HTML documents and style them with modern CSS
- Write modern ES6+ JavaScript with confidence
- Handle asynchronous operations using callbacks, Promises, and async/await
- Manipulate the DOM and respond to user interactions
- Build and deploy a static website

---

## Week 1: HTML & CSS Fundamentals

### Topics

#### Semantic HTML Elements
- Document structure: `<!DOCTYPE>`, `<html>`, `<head>`, `<body>`
- Structural elements: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`
- Text content: `<h1>`-`<h6>`, `<p>`, `<blockquote>`, `<ul>`, `<ol>`, `<li>`
- Inline elements: `<a>`, `<strong>`, `<em>`, `<span>`, `<code>`
- Forms: `<form>`, `<input>`, `<label>`, `<button>`, `<select>`, `<textarea>`
- Media: `<img>`, `<video>`, `<audio>`, `<figure>`, `<figcaption>`
- Why semantics matter: accessibility, SEO, maintainability

#### CSS Selectors and Specificity
- Basic selectors: element, class (`.`), ID (`#`), universal (`*`)
- Combinators: descendant (` `), child (`>`), adjacent sibling (`+`), general sibling (`~`)
- Attribute selectors: `[attr]`, `[attr=value]`, `[attr^=value]`, `[attr$=value]`
- Pseudo-classes: `:hover`, `:focus`, `:first-child`, `:nth-child()`, `:not()`
- Pseudo-elements: `::before`, `::after`, `::first-letter`
- Specificity calculation: inline > ID > class > element
- The cascade and inheritance

#### Flexbox Basics
- `display: flex` and flex containers
- Main axis vs cross axis
- `flex-direction`: row, column, row-reverse, column-reverse
- `justify-content`: flex-start, center, space-between, space-around, space-evenly
- `align-items`: stretch, flex-start, center, flex-end, baseline
- `flex-wrap` and `flex-flow`
- Flex items: `flex-grow`, `flex-shrink`, `flex-basis`, shorthand `flex`
- `align-self` for individual items

#### Basic Responsive Design
- The viewport meta tag
- Mobile-first vs desktop-first approach
- Media queries: `@media screen and (min-width: ...)`, `(max-width: ...)`
- Common breakpoints and when to use them
- Fluid typography and spacing with `rem`, `em`, `vw`, `vh`
- Responsive images: `max-width: 100%`, `srcset`, `picture` element

### Labs: Week 1

1. **Semantic Structure Challenge** | 🔴 **Core**
   Given a design mockup (text description), identify and implement the correct semantic HTML elements. No `<div>` soup allowed.

2. **Specificity Battle** | 🔴 **Core**
   Write CSS rules to style elements where multiple conflicting rules exist. Predict which styles will win, then verify.

3. **Selector Olympics** | 🟡 **Recommended**
   Target specific elements using only CSS selectors (no adding classes or IDs to HTML). Increasingly complex targeting challenges.

4. **Flexbox Froggy Recreate** | 🔴 **Core**
   Build a series of layouts using only flexbox. Start with simple centering, progress to complex navigation bars.

5. **Card Component** | 🔴 **Core**
   Build a reusable card component with image, title, description, and button. Must use semantic HTML and flexbox.

6. **Navigation Challenge** | 🟡 **Recommended**
   Create a horizontal navigation bar that collapses to a vertical layout on mobile. No JavaScript.

7. **Form Styling** | 🟡 **Recommended**
   Style a contact form with proper label associations, focus states, and validation indicators (using `:valid`, `:invalid`).

8. **Responsive Grid** | 🔴 **Core**
   Create a 3-column layout that becomes 2-column on tablets and 1-column on mobile using only flexbox.

9. **Specificity Debugging** | 🟢 **Stretch**
   Given broken CSS with specificity issues, fix the styles without using `!important`.

10. **Holy Grail Layout** | 🟢 **Stretch**
    Implement the classic header-sidebar-content-sidebar-footer layout using flexbox. Must be responsive.

### Week 1 Review Prompts

Take 10-15 minutes to reflect on your learning:

- **What did you learn?** List the three most important concepts you grasped this week about HTML and CSS.
- **What's still unclear?** Be honest. Which topics felt confusing? What would you like to revisit?
- **What would you teach someone else?** If a friend asked you to explain flexbox or semantic HTML, what would you say? Teaching reveals gaps in understanding.

---

## Week 2-3: ES6+ Features

### Topics

#### let/const vs var
- Block scope vs function scope
- The temporal dead zone
- Hoisting behavior differences
- When to use `const` vs `let` (hint: prefer `const`)
- Why `var` should be avoided in modern code

#### Arrow Functions
- Syntax variations: `() => {}`, `x => x * 2`, `(a, b) => a + b`
- Implicit vs explicit return
- Lexical `this` binding (no own `this`, `arguments`, `super`)
- When NOT to use arrow functions: methods, constructors, event handlers needing `this`
- Arrow functions and the arguments object

#### Template Literals
- Basic string interpolation: `` `Hello, ${name}` ``
- Multi-line strings without concatenation
- Expression evaluation inside `${}`
- Tagged template literals (advanced): how libraries like styled-components work

#### Destructuring
- Array destructuring: `const [first, second, ...rest] = array`
- Skipping elements: `const [, , third] = array`
- Default values: `const [a = 1] = []`
- Object destructuring: `const { name, age } = person`
- Renaming: `const { name: personName } = person`
- Nested destructuring: `const { address: { city } } = person`
- Function parameter destructuring
- Mixed array and object destructuring

#### Spread/Rest Operators
- Spread in arrays: `[...arr1, ...arr2]`, copying arrays
- Spread in objects: `{ ...obj1, ...obj2 }`, shallow copying
- Spread in function calls: `Math.max(...numbers)`
- Rest in function parameters: `function sum(...numbers)`
- Rest in destructuring: `const [first, ...others] = arr`
- Spread vs `Object.assign()`

#### ES Modules
- Named exports: `export const foo = ...`, `export function bar() {}`
- Default exports: `export default ...`
- Named imports: `import { foo, bar } from './module'`
- Default imports: `import MyModule from './module'`
- Renaming imports: `import { foo as myFoo } from './module'`
- Importing all: `import * as utils from './utils'`
- Re-exporting: `export { foo } from './other'`
- Dynamic imports: `import('./module').then(...)`

### Labs: Week 2-3

1. **Scope Detective** | 🔴 **Core**
   Given code snippets with `var`, `let`, and `const`, predict the output. Then convert all `var` to appropriate `let`/`const`.

2. **Arrow Function Conversion** | 🔴 **Core**
   Convert traditional functions to arrow functions. Identify cases where conversion changes behavior.

3. **The `this` Challenge** | 🔴 **Core**
   Create scenarios demonstrating `this` differences between regular and arrow functions in objects, event handlers, and callbacks.

4. **Template Literal Builder** | 🟡 **Recommended**
   Build a function that generates HTML strings using template literals. Handle nested data structures.

5. **Destructuring Drill** | 🔴 **Core**
   Extract nested data from complex API response objects using destructuring. One-liner challenges.

6. **Config Merger** | 🟡 **Recommended**
   Use spread operator to merge configuration objects with defaults, with later properties overriding earlier ones.

7. **Function Refactor** | 🟡 **Recommended**
   Given functions with many parameters, refactor to use object destructuring with defaults.

8. **Module Organizer** | 🔴 **Core**
   Take a single large file and split it into multiple modules with proper imports/exports.

9. **Rest Parameter Calculator** | 🟡 **Recommended**
   Build calculator functions that accept any number of arguments using rest parameters.

10. **Deep Clone Challenge** | 🟢 **Stretch**
    Understand why spread creates shallow copies. Demonstrate the problem and discuss solutions.

11. **Dynamic Import Loader** | 🟢 **Stretch**
    Create a module that conditionally loads other modules based on user input.

12. **Babel Output Analysis** | 🟢 **Stretch**
    Write ES6+ code and examine the Babel transpilation output. Understand what modern syntax compiles to.

13. **Default Parameter Gotchas** | 🟢 **Stretch**
    Explore edge cases with default parameters: `undefined` vs `null`, expression evaluation, parameter shadowing.

14. **Shorthand Property Challenge** | 🟡 **Recommended**
    Convert verbose object literals to use property shorthand and method shorthand.

15. **ES6 Quiz Builder** | 🟢 **Stretch**
    Build a self-testing quiz that drills ES6 syntax recognition.

### Week 2-3 Review Prompts

Take 10-15 minutes to reflect on your learning:

- **What did you learn?** Which ES6+ features feel natural now? Which will change how you write JavaScript?
- **What's still unclear?** Are there features you memorized but don't truly understand? Identify them.
- **What would you teach someone else?** Explain destructuring or the spread operator to an imaginary beginner. Where do you struggle to find the right words?

---

## Week 4-5: Asynchronous JavaScript

### Topics

#### Callbacks and Callback Hell
- What is asynchronous code and why it exists
- The JavaScript event loop (conceptual understanding)
- Callback functions: passing functions as arguments
- Error-first callback pattern (Node.js convention)
- The pyramid of doom: nested callbacks
- Problems: inversion of control, error handling complexity, readability

#### Promises
- What is a Promise: pending, fulfilled, rejected states
- Creating Promises: `new Promise((resolve, reject) => {})`
- Consuming Promises: `.then(onFulfilled, onRejected)`
- Chaining: return values become next Promise's value
- Error handling: `.catch()`, error propagation through chains
- `.finally()` for cleanup
- `Promise.all()`: parallel execution, fail-fast
- `Promise.allSettled()`: wait for all, regardless of outcome
- `Promise.race()`: first to settle wins
- `Promise.any()`: first to fulfill wins

#### async/await
- `async` functions always return Promises
- `await` pauses execution until Promise settles
- Error handling with try/catch
- Parallel execution with `await Promise.all()`
- Common mistake: sequential await when parallel is possible
- Top-level await (in modules)
- Async iteration: `for await...of`

#### fetch API
- Basic GET request: `fetch(url)`
- Handling the Response object
- Parsing JSON: `response.json()`
- Checking response status: `response.ok`, `response.status`
- POST requests with options: method, headers, body
- Sending JSON data
- Sending form data
- Handling network errors vs HTTP errors
- AbortController for cancellation
- Request and Response objects in detail

#### Error Handling Patterns
- Synchronous vs asynchronous error handling
- Try/catch limitations with callbacks
- Promise rejection handling
- Unhandled rejection events
- Error boundaries (conceptual, full implementation in React module)
- Creating custom error classes
- When to throw vs when to return error values
- Graceful degradation strategies

### Labs: Week 4-5

1. **Callback Converter** | 🔴 **Core**
   Take synchronous code and convert it to callback-based async code. Experience the pain firsthand.

2. **Callback Hell Escape** | 🔴 **Core**
   Given deeply nested callback code, refactor to Promises, then to async/await. Compare readability.

3. **Promise from Scratch** | 🔴 **Core**
   Implement a basic Promise constructor that supports `.then()` and `.catch()`. (See Build-Your-Own section)

4. **Sequential vs Parallel** | 🔴 **Core**
   Given multiple async operations, implement both sequential and parallel execution. Measure performance difference.

5. **Fetch Wrapper** | 🟡 **Recommended**
   Build a wrapper around fetch that handles common cases: timeout, retry, JSON parsing, error normalization.

6. **API Explorer** | 🔴 **Core**
   Use fetch to interact with a public API (JSONPlaceholder, Pokemon API, etc.). Implement CRUD operations.

7. **Promise.all Dashboard** | 🟡 **Recommended**
   Fetch data from multiple endpoints simultaneously. Display loading states and handle partial failures.

8. **Retry Logic** | 🟡 **Recommended**
   Implement exponential backoff retry logic for failed requests.

9. **Request Queue** | 🟢 **Stretch**
   Build a queue that limits concurrent requests to prevent overwhelming an API.

10. **Cancellation Pattern** | 🟡 **Recommended**
    Implement request cancellation using AbortController. Handle user navigation away from loading content.

11. **Error Handler Factory** | 🟢 **Stretch**
    Create a higher-order function that wraps async functions with consistent error handling and logging.

12. **Loading State Machine** | 🟢 **Stretch**
    Model loading states (idle, loading, success, error) and transitions between them.

13. **Polling Implementation** | 🟢 **Stretch**
    Build a polling mechanism that fetches data at intervals with proper cleanup.

14. **Timeout Wrapper** | 🟡 **Recommended**
    Create a utility that adds timeout capability to any Promise.

15. **Race Condition Demo** | 🟢 **Stretch**
    Create a scenario demonstrating race conditions in async code and implement a solution.

### Week 4-5 Review Prompts

Take 10-15 minutes to reflect on your learning:

- **What did you learn?** Can you explain the event loop to someone? What clicked about Promises vs callbacks?
- **What's still unclear?** Which async patterns still trip you up? Error handling? Race conditions?
- **What would you teach someone else?** Walk through converting callback hell to async/await. What are the key insights?

---

## Week 6: DOM & Events

### Topics

#### Selecting Elements
- `document.getElementById()`: fastest, returns single element or null
- `document.querySelector()`: CSS selector, returns first match or null
- `document.querySelectorAll()`: CSS selector, returns static NodeList
- `document.getElementsByClassName()`: returns live HTMLCollection
- `document.getElementsByTagName()`: returns live HTMLCollection
- Live vs static collections: implications for loops
- Traversal: `parentElement`, `children`, `nextElementSibling`, `previousElementSibling`
- `closest()`: finds nearest ancestor matching selector

#### Modifying Content and Styles
- `textContent` vs `innerHTML` vs `innerText`
- Security: XSS risks with innerHTML
- Creating elements: `document.createElement()`
- Appending: `appendChild()`, `append()`, `prepend()`, `before()`, `after()`
- Removing: `remove()`, `removeChild()`
- Cloning: `cloneNode(shallow)`, `cloneNode(true)`
- Attributes: `getAttribute()`, `setAttribute()`, `removeAttribute()`, `hasAttribute()`
- Data attributes: `dataset` property
- Class manipulation: `classList.add()`, `.remove()`, `.toggle()`, `.contains()`, `.replace()`
- Inline styles: `element.style.property`
- Getting computed styles: `getComputedStyle()`

#### Event Listeners
- `addEventListener(type, handler, options)`
- Event types: click, submit, input, change, keydown, keyup, focus, blur, load, DOMContentLoaded
- The Event object: `type`, `target`, `currentTarget`, `preventDefault()`, `stopPropagation()`
- Removing listeners: `removeEventListener()` (requires reference to same function)
- Event listener options: `capture`, `once`, `passive`
- `this` in event handlers (regular functions vs arrow functions)

#### Event Delegation
- Event bubbling: events propagate up the DOM tree
- Event capturing: events propagate down first (rarely used)
- Delegation pattern: listen on parent, check `event.target`
- Benefits: performance, handling dynamic elements
- `matches()` for checking if target matches selector
- `closest()` for finding the actual element to handle

#### Building Dynamic UIs
- Rendering lists from data
- Updating the DOM efficiently
- Managing application state (simple patterns before frameworks)
- Separation of concerns: data, rendering, event handling
- Templating patterns without a framework
- Virtual DOM concept (understanding what React does)

### Labs: Week 6

1. **DOM Treasure Hunt** | 🔴 **Core**
   Navigate through a complex DOM structure using only traversal methods. No querySelector allowed.

2. **Dynamic List Builder** | 🔴 **Core**
   Create an application that renders a list from an array. Implement add, edit, delete operations.

3. **Form Validator** | 🔴 **Core**
   Build client-side form validation without libraries. Display errors dynamically, validate on blur and submit.

4. **Event Logger** | 🟡 **Recommended**
   Build a tool that logs all events on a page. Visualize event propagation (capture and bubble phases).

5. **Delegation Challenge** | 🔴 **Core**
   Given a dynamic list that adds/removes items, implement click handling using event delegation only.

6. **Tab Component** | 🟡 **Recommended**
   Build a tabbed interface from scratch. Active state management, content switching, keyboard navigation.

7. **Modal Dialog** | 🟡 **Recommended**
   Create an accessible modal dialog. Handle open/close, focus trapping, escape key, background click.

8. **Infinite Scroll** | 🟢 **Stretch**
   Implement infinite scrolling that loads more content as the user scrolls. Use Intersection Observer.

9. **Drag and Drop** | 🟢 **Stretch**
   Build a simple drag-and-drop interface for reordering list items. Native drag events only.

10. **Live Search** | 🟡 **Recommended**
    Create a search input that filters a list in real-time. Debounce the input for performance.

11. **Theme Switcher** | 🟡 **Recommended**
    Build a light/dark theme toggle that persists preference to localStorage.

12. **Accordion Component** | 🟢 **Stretch**
    Create an accessible accordion with proper ARIA attributes and keyboard support.

13. **Toast Notifications** | 🟢 **Stretch**
    Build a notification system that can show, stack, and auto-dismiss toast messages.

14. **State-Driven Counter** | 🔴 **Core**
    Build a counter where the UI is always derived from state. Never manipulate DOM directly outside of render.

15. **Mini Framework** | 🟢 **Stretch**
    Create a tiny function that takes data and a template function, returning rendered HTML. First step toward understanding React.

### Week 6 Review Prompts

Take 10-15 minutes to reflect on your learning:

- **What did you learn?** How comfortable are you manipulating the DOM? What's your go-to approach for handling events?
- **What's still unclear?** Event delegation? The difference between live and static collections? State management?
- **What would you teach someone else?** Explain why React exists after this week. What problems does it solve?

---

## Build-Your-Own Projects

These projects require you to implement fundamental concepts from scratch. No solutions are provided. Research, experiment, fail, and learn.

### Project 1: Implement Array Methods

**Objective:** Recreate core array methods to understand how they work internally.

#### Project Variations

**Option A: Guided (More Structure)**
- Start with pseudocode provided for each method
- Implement one method at a time with explicit test cases given
- Use console.log statements to trace execution
- Compare your output against native methods after each step
- Suggested order: myForEach -> myMap -> myFilter -> myReduce

**Option B: Standard (Current)**
Follow the requirements below without additional guidance.

**Option C: Open-ended (Minimal Hints)**
- Implement all Array.prototype methods you can think of
- Add support for thisArg, sparse arrays, and negative indices
- Write your own test suite
- Optimize for performance and compare against native methods

#### Requirements (Option B):

Implement the following methods that work identically to their native counterparts:

**myMap(array, callback)**
- Accepts an array and a callback function
- Callback receives: (currentValue, index, array)
- Returns a new array with callback results
- Does not mutate original array
- Must handle sparse arrays correctly

**myFilter(array, callback)**
- Accepts an array and a callback function
- Callback receives: (currentValue, index, array)
- Returns new array with elements where callback returned truthy
- Does not mutate original array
- Must handle sparse arrays correctly

**myReduce(array, callback, initialValue)**
- Accepts array, callback, and optional initial value
- Callback receives: (accumulator, currentValue, index, array)
- If no initial value, first element is used (must throw on empty array)
- Returns single reduced value
- Must handle sparse arrays correctly

**Testing your implementations:**
- Test against native methods with various inputs
- Edge cases: empty arrays, single element, sparse arrays, different data types
- Verify callback receives correct arguments
- Verify return values match native behavior

**Stretch goals:**
- Implement `myForEach`, `myFind`, `myFindIndex`, `myEvery`, `mySome`
- Add support for `thisArg` parameter

---

### Project 2: Simple Promise Implementation

**Objective:** Build a basic Promise implementation to understand asynchronous patterns.

#### Project Variations

**Option A: Guided (More Structure)**
- Start with a provided class skeleton with method signatures
- Implement state management first (pending, fulfilled, rejected)
- Add .then() support for already-resolved promises
- Then add support for async resolution
- Finally add chaining
- Test each feature before moving to the next

**Option B: Standard (Current)**
Follow the requirements below without additional guidance.

**Option C: Open-ended (Minimal Hints)**
- Build a Promises/A+ compliant implementation
- Run it against the official test suite
- Implement all static methods: all, allSettled, race, any, resolve, reject
- Add debugging/tracing capabilities

#### Requirements (Option B):

Create a `MyPromise` class/constructor with the following behavior:

**Constructor:**
- Accepts an executor function: `(resolve, reject) => {}`
- Executor runs immediately upon construction
- `resolve(value)` transitions to fulfilled state
- `reject(reason)` transitions to rejected state
- Can only transition once (first call wins)
- Must catch synchronous errors in executor

**then(onFulfilled, onRejected):**
- Registers callbacks for fulfilled/rejected states
- Returns a new Promise for chaining
- If already settled, callbacks execute asynchronously
- Callbacks receive the resolved value or rejection reason
- If callback returns a value, next Promise resolves with it
- If callback throws, next Promise rejects with error
- If callback returns a Promise, next Promise adopts its state
- If callback is not a function, value passes through

**catch(onRejected):**
- Shorthand for `.then(undefined, onRejected)`
- Returns a Promise for chaining

**Testing your implementation:**
- Basic resolve/reject
- Chaining multiple `.then()` calls
- Error propagation through chain
- `.catch()` recovery
- Returning Promises from callbacks
- Asynchronous resolution

**Note:** A full Promises/A+ compliant implementation is complex. Focus on the core behavior first.

**Stretch goals:**
- Implement `MyPromise.resolve()` and `MyPromise.reject()` static methods
- Implement `MyPromise.all()`
- Pass relevant Promises/A+ compliance tests

---

### Project 3: Event Emitter

**Objective:** Build a pub/sub system to understand event-driven programming.

#### Project Variations

**Option A: Guided (More Structure)**
- Start by implementing a simple on/emit pair
- Use an object to store listeners (event name -> array of functions)
- Add off() after on/emit work
- Add once() last
- Test each method before adding the next
- Draw diagrams of your data structure as you build

**Option B: Standard (Current)**
Follow the requirements below without additional guidance.

**Option C: Open-ended (Minimal Hints)**
- Build a full-featured event system like Node.js EventEmitter
- Add namespaced events (e.g., 'user:login', 'user:logout')
- Implement wildcard listeners
- Add async event emission
- Build a debugging mode that logs all events

#### Requirements (Option B):

Create an `EventEmitter` class with the following methods:

**on(eventName, listener)**
- Registers a listener function for an event
- Same listener can be registered multiple times
- Returns `this` for chaining

**emit(eventName, ...args)**
- Calls all listeners registered for the event
- Passes additional arguments to listeners
- Listeners called in registration order
- Returns `true` if event had listeners, `false` otherwise

**off(eventName, listener)**
- Removes a specific listener from an event
- If registered multiple times, removes only first occurrence
- Returns `this` for chaining

**once(eventName, listener)**
- Registers a listener that fires only once
- Listener is automatically removed after first call
- Returns `this` for chaining

**Additional requirements:**
- Handle events that don't exist gracefully
- Removing a listener during emit should not affect current emit cycle

**Testing your implementation:**
- Basic on/emit/off flow
- Multiple listeners on same event
- Different events don't interfere
- Once fires only once
- Arguments passed correctly
- Return values correct
- Edge cases: remove non-existent listener, emit non-existent event

**Stretch goals:**
- Implement `removeAllListeners(eventName?)` method
- Implement `listenerCount(eventName)` method
- Add `maxListeners` warning like Node.js
- Implement `prependListener()` to add to front

---

## Second Deploy Checkpoint

### Objective
Deploy a static website to demonstrate your HTML, CSS, and JavaScript skills.

### Requirements

Create and deploy a personal project or portfolio page that includes:

**Technical requirements:**
- Semantic HTML structure
- Responsive design (mobile, tablet, desktop)
- At least one interactive JavaScript feature
- Clean, organized CSS (consider using CSS custom properties)
- No frameworks or libraries (vanilla HTML/CSS/JS only)

**Suggested features to include:**
- Navigation with smooth scrolling
- Interactive component (tabs, accordion, modal, etc.)
- Form with client-side validation
- Dynamic content rendering from data
- Theme toggle or other preference persistence

### Deployment Options

**GitHub Pages:**
1. Create a repository for your project
2. Push your code to the main branch
3. Enable GitHub Pages in repository settings
4. Your site will be live at `https://username.github.io/repo-name`

**Netlify:**
1. Create a Netlify account
2. Drag and drop your project folder, OR
3. Connect to your GitHub repository for automatic deploys
4. Your site will be live at `https://random-name.netlify.app`
5. Optional: Configure a custom subdomain

### Verification

Your deployed site should:
- Load without errors in browser console
- Be fully responsive on mobile devices
- Have all interactive features working
- Pass basic accessibility checks (use browser dev tools)

---

## Recommended Resources

### MDN Documentation (Primary Reference)

**HTML:**
- [HTML Elements Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
- [HTML Forms Guide](https://developer.mozilla.org/en-US/docs/Learn/Forms)

**CSS:**
- [CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [Flexbox Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)
- [CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

**JavaScript:**
- [JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [DOM Manipulation](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

### Video Tutorials

- **JavaScript.info** - [The Modern JavaScript Tutorial](https://javascript.info/) (comprehensive, free)
- **Traversy Media** - JavaScript Crash Course (YouTube, beginner-friendly)
- **Fireship** - JavaScript in 100 seconds series (YouTube, quick overviews)
- **The Net Ninja** - Modern JavaScript tutorials (YouTube, project-based)
- **Philip Roberts** - "What the heck is the event loop anyway?" (YouTube, essential for async understanding)

### Practice Platforms

- **[Exercism](https://exercism.org/tracks/javascript)** - JavaScript track with mentorship
- **[JavaScript30](https://javascript30.com/)** - 30 vanilla JS projects by Wes Bos (free)
- **[Frontend Mentor](https://www.frontendmentor.io/)** - HTML/CSS challenges with designs
- **[Codewars](https://www.codewars.com/)** - JavaScript algorithm challenges
- **[LeetCode](https://leetcode.com/)** - Algorithm practice (useful for array methods)
- **[CSS Battle](https://cssbattle.dev/)** - CSS challenges (fun for selector mastery)

### Concepts Deep Dives

- **[Loupe](http://latentflip.com/loupe/)** - Event loop visualizer by Philip Roberts
- **[Promises/A+ Specification](https://promisesaplus.com/)** - The official spec
- **[CSS-Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)** - Visual flexbox reference
- **[JavaScript Visualizer](https://www.jsv9000.app/)** - See how JavaScript executes

---

## Resources for Self-Study

### Documentation
- MDN Web Docs (HTML, CSS, JavaScript references)
- JavaScript.info (modern JavaScript tutorial)
- CSS-Tricks (especially for Flexbox and Grid)

### Practice
- Exercism JavaScript track
- JavaScript30 by Wes Bos (30 vanilla JS projects)
- Frontend Mentor (HTML/CSS challenges)

### Concepts
- Event loop visualizer (Loupe by Philip Roberts)
- Promises/A+ specification
- ECMAScript specification (for the brave)

---

## Self-Assessment Checkpoint: Can You Do This?

Before moving to Module 3, complete these challenges without looking at notes or documentation. If you can do them all, you're ready.

### Challenge 1: HTML/CSS Layout
Build a responsive card grid (3 columns desktop, 2 tablet, 1 mobile) with:
- Semantic HTML structure
- Flexbox layout
- Hover effects on cards
- No class names on HTML - use only CSS selectors

### Challenge 2: ES6+ Transformation
Given this code, refactor it using ES6+ features (arrow functions, destructuring, template literals, spread):
```javascript
function createUser(name, age, city, country) {
  var user = {
    name: name,
    age: age,
    location: {
      city: city,
      country: country
    }
  };
  return 'User ' + user.name + ' is ' + user.age + ' years old from ' + user.location.city;
}
```

### Challenge 3: Async Data Fetching
Write a function that:
- Fetches data from two different API endpoints in parallel
- Returns combined results only if both succeed
- Handles errors gracefully with a fallback value
- Uses async/await (not .then())

### Challenge 4: DOM Manipulation
Without using any framework:
- Create a todo list from an array of items
- Add new items via a form
- Delete items with a button click
- Use event delegation for the delete buttons
- Keep data and UI in sync

### Challenge 5: Implement debounce()
Write a `debounce(fn, delay)` function that:
- Returns a new function that delays invoking `fn`
- Resets the timer if called again before delay expires
- Passes arguments to the original function correctly

### Challenge 6: Promise Chain
Write code that:
- Fetches a user by ID
- Then fetches that user's posts
- Then fetches comments for the first post
- Logs the result
- Handles errors at any step
- Uses a single .catch() at the end

---

## Module Checklist

Before proceeding to Module 3, ensure you can:

- [ ] Structure HTML documents semantically without relying on div soup
- [ ] Write CSS selectors with understanding of specificity
- [ ] Create responsive layouts with Flexbox
- [ ] Use all ES6+ features covered (let/const, arrows, destructuring, spread/rest, modules)
- [ ] Explain the difference between callbacks, Promises, and async/await
- [ ] Fetch data from APIs and handle errors appropriately
- [ ] Select and manipulate DOM elements programmatically
- [ ] Handle events and implement event delegation
- [ ] Build interactive UI components without frameworks
- [ ] Deploy a static website to the public internet
- [ ] Complete all three Build-Your-Own projects

---

**Next Module:** React Fundamentals

Building vanilla JavaScript components is painful. That's intentional. You now understand the problems that React solves. You're ready to learn why frameworks exist.
