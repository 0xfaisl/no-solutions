# Module 3: TypeScript Fundamentals

**Duration:** 4 weeks (1-2 hours/day)

**Prerequisites:** Module 1 (JavaScript Foundations), Module 2

**Philosophy:** Learn types by building type-safe systems from scratch. No solutions provided—struggle is the teacher.

---

## Why TypeScript?

### The Problem with JavaScript

JavaScript is dynamically typed—variables can hold any value, and types are only checked at runtime. This flexibility comes at a cost:

```javascript
// JavaScript lets you do this without warning
function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}

calculateTotal("not an array"); // Runtime error!
calculateTotal([{ cost: 10 }]); // Returns NaN (price vs cost typo)
```

These bugs only appear when the code runs—often in production, often discovered by users.

### What TypeScript Solves

TypeScript adds **static type checking** to JavaScript. Types are verified at compile time, before your code ever runs:

1. **Catches bugs early** - Type errors appear in your editor as you type
2. **Better tooling** - Autocomplete, refactoring, and navigation that actually work
3. **Self-documenting code** - Types serve as always-up-to-date documentation
4. **Safer refactoring** - Change a type and see everywhere that breaks instantly
5. **Team scalability** - Types enforce contracts between different parts of the codebase

```typescript
// TypeScript catches these immediately
function calculateTotal(items: { price: number }[]): number {
  return items.reduce((sum, item) => sum + item.price, 0);
}

calculateTotal("not an array"); // Error: Argument of type 'string' is not assignable
calculateTotal([{ cost: 10 }]); // Error: Property 'price' is missing
```

### Alternatives to TypeScript

**Flow** (Facebook)
- Similar concept: static type checker for JavaScript
- Less popular, smaller ecosystem
- Facebook has been migrating to TypeScript

**JSDoc Type Annotations**
- Type hints in comments, no compilation step
- Limited compared to full TypeScript
- Good for gradual adoption or library authors

```javascript
/**
 * @param {string} name
 * @returns {string}
 */
function greet(name) {
  return `Hello, ${name}`;
}
```

### Why TypeScript Won

TypeScript has become the **industry standard** because:

- **Backed by Microsoft** - Long-term support and development
- **Massive ecosystem** - DefinitelyTyped has types for 10,000+ packages
- **Framework adoption** - Angular, Vue 3, and most React projects use it
- **Gradual adoption** - Valid JavaScript is valid TypeScript
- **VS Code integration** - First-class support in the most popular editor
- **Hiring signal** - TypeScript skills are expected in most frontend roles

**Bottom line:** Learning TypeScript isn't optional for modern web development. It's the expected baseline.

---

## Learning Objectives

By the end of this module, you will:
- Write type-safe JavaScript with full TypeScript annotation
- Design flexible APIs using generics
- Leverage utility types to avoid repetition
- Convert existing JavaScript projects to TypeScript
- Configure TypeScript for real-world projects

---

## Week 1: Core Types

### Day 1-2: Type Annotations & Basic Types

**Concepts:**
- What TypeScript adds to JavaScript (compile-time checking)
- Type annotations syntax: `let name: string = "value"`
- Basic types: `string`, `number`, `boolean`, `null`, `undefined`
- Arrays: `string[]` vs `Array<string>`
- Tuples: `[string, number]`

**Practice:**
```typescript
// Annotate these variables
let username = "alice";
let age = 25;
let isActive = true;
let scores = [95, 87, 92];
let coordinates = [10, 20]; // Should be a tuple
```

**Key Questions:**
- When does TypeScript infer types automatically?
- What's the difference between `null` and `undefined` in TypeScript?

### Day 3-4: Objects, Interfaces & Type Aliases

**Concepts:**
- Object type annotations: `{ name: string; age: number }`
- Interfaces: named object shapes
- Type aliases: `type Name = ...`
- Optional properties: `property?: type`
- Readonly properties: `readonly property: type`

**Interface vs Type Alias:**
```typescript
// Interface - extendable, for object shapes
interface User {
  id: number;
  name: string;
  email?: string;
}

// Type alias - more flexible, can represent any type
type ID = string | number;
type Point = { x: number; y: number };
```

**When to use which:**
- Use `interface` for object shapes that might be extended
- Use `type` for unions, primitives, tuples, or complex type expressions

**Practice:**
- Define interfaces for a blog post, comment, and author
- Create types for API response shapes

### Day 5-7: Union, Intersection & Literal Types

**Union Types:**
```typescript
type Status = "pending" | "approved" | "rejected";
type Result = string | number;

function process(value: string | number) {
  // Must handle both cases
}
```

**Intersection Types:**
```typescript
type Employee = Person & { employeeId: number };
```

**Literal Types:**
```typescript
type Direction = "north" | "south" | "east" | "west";
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;
```

**Lab: Type System Exploration**

1. Create a type for HTTP methods: GET, POST, PUT, DELETE, PATCH - **Core**
2. Create a type for a response that can be success (with data) or error (with message) - **Core**
3. Model a shopping cart item with required and optional fields - **Recommended**

### Week 1 Review Prompts

Before moving to Week 2, take 10-15 minutes to reflect:

- **What did you learn?** Write down 3 key insights about TypeScript's type system.
- **What's still unclear?** List any concepts you're uncertain about—research them before proceeding.
- **What would you teach someone else?** Explain union types vs intersection types as if teaching a friend.

---

## Week 2: Functions & Generics

### Day 1-2: Typed Functions

**Concepts:**
- Parameter type annotations
- Return type annotations
- Void vs undefined returns
- Function type expressions
- Call signatures

**Syntax:**
```typescript
// Parameter and return types
function greet(name: string): string {
  return `Hello, ${name}`;
}

// Arrow function
const add = (a: number, b: number): number => a + b;

// Function type
type MathOperation = (a: number, b: number) => number;
```

**Optional & Default Parameters:**
```typescript
function createUser(name: string, age?: number, role = "user"): User {
  // age is number | undefined
  // role is string (default value provides type)
}
```

**Rest Parameters:**
```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}
```

### Day 3-4: Generic Functions

**Why Generics:**
- Write reusable code that works with multiple types
- Maintain type safety without repetition
- Let the caller decide the specific type

**Basic Generic Syntax:**
```typescript
function identity<T>(value: T): T {
  return value;
}

// TypeScript infers T from usage
const str = identity("hello");  // T is string
const num = identity(42);       // T is number

// Or specify explicitly
const explicit = identity<boolean>(true);
```

**Multiple Type Parameters:**
```typescript
function pair<T, U>(first: T, second: U): [T, U] {
  return [first, second];
}
```

**Practice:**
- Write a generic `first` function that returns the first element of an array - **Core**
- Write a generic `map` function that transforms array elements - **Recommended**

### Day 5-7: Generic Constraints

**Constraining Type Parameters:**
```typescript
// T must have a length property
function logLength<T extends { length: number }>(item: T): void {
  console.log(item.length);
}

logLength("hello");     // OK - strings have length
logLength([1, 2, 3]);   // OK - arrays have length
logLength(42);          // Error - numbers don't have length
```

**The `keyof` Operator:**
```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Alice", age: 25 };
const name = getProperty(user, "name");  // string
const age = getProperty(user, "age");    // number
const invalid = getProperty(user, "foo"); // Error!
```

**Lab: Generic Utilities**
1. Implement a generic `Stack<T>` class with push, pop, peek - **Core**
2. Write a generic `groupBy<T>` function - **Recommended**
3. Create a generic `Result<T, E>` type for success/error handling - **Stretch**

### Week 2 Review Prompts

Before moving to Week 3, take 10-15 minutes to reflect:

- **What did you learn?** Write down the key difference between a regular function and a generic function.
- **What's still unclear?** Can you explain `keyof` and indexed access types confidently?
- **What would you teach someone else?** Explain why generics matter using a real example from your practice.

---

## Week 3: Advanced Types

### Day 1-2: Utility Types

TypeScript provides built-in type transformations:

**Partial<T>** - Makes all properties optional
```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

type UserUpdate = Partial<User>;
// { id?: number; name?: string; email?: string }
```

**Required<T>** - Makes all properties required
```typescript
type CompleteUser = Required<Partial<User>>;
```

**Pick<T, K>** - Select specific properties
```typescript
type UserPreview = Pick<User, "id" | "name">;
// { id: number; name: string }
```

**Omit<T, K>** - Exclude specific properties
```typescript
type UserWithoutEmail = Omit<User, "email">;
// { id: number; name: string }
```

**Record<K, V>** - Create object type with specific keys and value type
```typescript
type Scores = Record<string, number>;
// { [key: string]: number }

type StatusMap = Record<"pending" | "active" | "done", boolean>;
```

**Other Useful Utilities:**
- `Readonly<T>` - Make all properties readonly
- `ReturnType<T>` - Extract return type of function
- `Parameters<T>` - Extract parameter types as tuple
- `NonNullable<T>` - Remove null and undefined

### Day 3-4: Type Guards & Narrowing

**Type Narrowing:**
```typescript
function process(value: string | number) {
  if (typeof value === "string") {
    // TypeScript knows value is string here
    return value.toUpperCase();
  }
  // TypeScript knows value is number here
  return value.toFixed(2);
}
```

**typeof Guard:**
```typescript
typeof x === "string"
typeof x === "number"
typeof x === "boolean"
typeof x === "object"
typeof x === "function"
typeof x === "undefined"
```

**instanceof Guard:**
```typescript
if (error instanceof TypeError) {
  // error is TypeError
}
```

**Custom Type Guards:**
```typescript
interface Fish { swim(): void }
interface Bird { fly(): void }

function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

if (isFish(pet)) {
  pet.swim();  // TypeScript knows it's Fish
}
```

### Day 5-7: Discriminated Unions & unknown vs any

**Discriminated Unions:**
```typescript
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "rectangle"; width: number; height: number }
  | { kind: "triangle"; base: number; height: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
    case "triangle":
      return (shape.base * shape.height) / 2;
  }
}
```

**unknown vs any:**
```typescript
// any - disables type checking (avoid!)
let dangerous: any = fetchData();
dangerous.anything.goes();  // No error, but might crash

// unknown - type-safe alternative
let safe: unknown = fetchData();
safe.anything;  // Error! Must narrow first

if (typeof safe === "string") {
  safe.toUpperCase();  // OK after narrowing
}
```

**Rule:** Use `unknown` when you don't know the type. Use `any` only as last resort.

**Lab: Type-Safe Validation**
1. Create discriminated unions for form field types (text, number, select, checkbox) - **Core**
2. Write type guards for validating API responses - **Core**
3. Implement a type-safe event handler using discriminated unions - **Recommended**

### Week 3 Review Prompts

Before moving to Week 4, take 10-15 minutes to reflect:

- **What did you learn?** Which utility types do you see yourself using most often?
- **What's still unclear?** Can you implement `Pick` from scratch without looking it up?
- **What would you teach someone else?** Explain the difference between `unknown` and `any` with examples.

---

## Week 4: Real-World Patterns

### Day 1-2: Typing API Responses

**Defining API Types:**
```typescript
// Response wrapper
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

// Error response
interface ApiError {
  code: string;
  message: string;
  details?: Record<string, string[]>;
}

// Specific resource types
interface User {
  id: number;
  username: string;
  email: string;
  createdAt: string;
}

interface PaginatedResponse<T> {
  items: T[];
  total: number;
  page: number;
  pageSize: number;
  hasMore: boolean;
}
```

**Typing fetch:**
```typescript
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }
  return response.json() as Promise<User>;
}
```

### Day 3-4: Error Handling with Types

**Result Pattern:**
```typescript
type Result<T, E = Error> =
  | { success: true; data: T }
  | { success: false; error: E };

async function safeFetch<T>(url: string): Promise<Result<T>> {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      return {
        success: false,
        error: new Error(`HTTP ${response.status}`)
      };
    }
    const data = await response.json();
    return { success: true, data };
  } catch (error) {
    return {
      success: false,
      error: error instanceof Error ? error : new Error(String(error))
    };
  }
}

// Usage forces error handling
const result = await safeFetch<User>("/api/user/1");
if (result.success) {
  console.log(result.data.name);
} else {
  console.error(result.error.message);
}
```

### Day 5: tsconfig.json Essentials

**Key Configuration Options:**
```json
{
  "compilerOptions": {
    // Strict mode (recommended)
    "strict": true,

    // Module system
    "module": "ESNext",
    "moduleResolution": "bundler",

    // Output
    "target": "ES2020",
    "outDir": "./dist",

    // Type checking
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,

    // Interop
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,

    // Source maps for debugging
    "sourceMap": true,

    // Path aliases
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

**Strict Mode Flags (all enabled by `"strict": true`):**
- `strictNullChecks` - null/undefined handled explicitly
- `noImplicitAny` - must annotate when type can't be inferred
- `strictFunctionTypes` - stricter function type checking
- `strictPropertyInitialization` - class properties must be initialized

### Day 6-7: Converting JavaScript to TypeScript

**Migration Strategy:**
1. Rename `.js` to `.ts` (or `.jsx` to `.tsx`)
2. Fix immediate compilation errors
3. Add type annotations incrementally
4. Replace `any` with proper types
5. Enable stricter compiler options over time

**Common Patterns:**
```typescript
// Typing third-party libraries
// Install @types/libraryname or declare module

// Typing JSON imports
import data from "./data.json";
// Configure: "resolveJsonModule": true

// Handling dynamic object keys
const cache: Record<string, unknown> = {};

// Typing event handlers
function handleClick(event: MouseEvent) { }
function handleSubmit(event: React.FormEvent<HTMLFormElement>) { }
```

**Lab: Migration Practice**
- Convert your Module 1 JavaScript projects to TypeScript - **Core**
- Add proper types to all functions and data structures - **Core**
- Enable strict mode and fix all errors - **Recommended**

### Week 4 Review Prompts

Before moving to Module 4, take 10-15 minutes to reflect:

- **What did you learn?** What's the most important tsconfig option and why?
- **What's still unclear?** Are you comfortable converting any JS file to TS with strict mode?
- **What would you teach someone else?** Walk through the Result pattern and why it improves error handling.

---

## Build-Your-Own Projects

### Project 1: Type-Safe Event Emitter

Build an event emitter where event names and their payload types are enforced at compile time.

#### Project Variations

**Option A: Guided (More Structure)**

Follow these implementation steps:
1. Start by defining the `EventMap` type constraint
2. Create the class with a private `listeners` Map
3. Implement `on` first—use `keyof` to constrain event names
4. Implement `emit` with payload type checking
5. Add `off` and `once` last

Starter template:
```typescript
type EventMap = Record<string, unknown>;

class TypedEventEmitter<Events extends EventMap> {
  private listeners = new Map<keyof Events, Set<Function>>();

  // Implement these methods:
  // on<K extends keyof Events>(event: K, callback: (payload: Events[K]) => void): void
  // off<K extends keyof Events>(event: K, callback: (payload: Events[K]) => void): void
  // emit<K extends keyof Events>(event: K, payload: Events[K]): void
  // once<K extends keyof Events>(event: K, callback: (payload: Events[K]) => void): void
}
```

**Option B: Standard (Current)**

**Requirements:**
- Define events and their payload types using generics
- `on(event, callback)` - register typed event listener
- `off(event, callback)` - remove listener
- `emit(event, payload)` - emit with type-checked payload
- `once(event, callback)` - listener that auto-removes after first call

**Type Safety Goals:**
```typescript
// Define your event map
interface MyEvents {
  userLogin: { userId: string; timestamp: Date };
  userLogout: { userId: string };
  message: { from: string; text: string };
}

const emitter = new TypedEventEmitter<MyEvents>();

// These should work with full autocomplete
emitter.on("userLogin", (payload) => {
  // payload should be typed as { userId: string; timestamp: Date }
});

emitter.emit("userLogin", { userId: "123", timestamp: new Date() });

// These should cause TypeScript errors
emitter.emit("userLogin", { wrong: "payload" });  // Error!
emitter.on("nonexistent", () => {});              // Error!
```

**Hints:**
- Use `keyof` to constrain event names
- Use indexed access types for payload types
- Consider how to type the internal listeners storage

**Option C: Open-Ended (Minimal Hints)**

Build a type-safe event emitter. The only requirements:
- Event names and payloads must be type-checked at compile time
- Incorrect event names or payload shapes must produce TypeScript errors

No starter code. No hints. Design the API yourself.

---

### Project 2: Typed Fetch Wrapper

Build a type-safe API client that provides autocomplete and type checking for API endpoints.

#### Project Variations

**Option A: Guided (More Structure)**

Follow these implementation steps:
1. Define the `ApiSchema` type structure for routes
2. Create helper types to extract response/body types from schema
3. Build the base `request` method with proper typing
4. Implement `get`, `post`, `put`, `delete` as typed wrappers
5. Add URL parameter extraction using template literal types

Starter template:
```typescript
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";

interface RouteConfig {
  response: unknown;
  body?: unknown;
  params?: Record<string, string>;
}

type ApiSchema = Record<string, Partial<Record<HttpMethod, RouteConfig>>>;

// Build from here...
function createApiClient<Schema extends ApiSchema>(baseUrl: string) {
  // Return an object with typed get, post, put, delete methods
}
```

**Option B: Standard (Current)**

**Requirements:**
- Define API routes with their request/response types
- Type-safe GET, POST, PUT, DELETE methods
- Proper error typing
- Request/response interceptors (typed)
- Support for query parameters and request bodies

**Type Safety Goals:**
```typescript
// Define your API schema
interface ApiSchema {
  "/users": {
    GET: { response: User[] };
    POST: { body: CreateUserDto; response: User };
  };
  "/users/:id": {
    GET: { response: User };
    PUT: { body: UpdateUserDto; response: User };
    DELETE: { response: void };
  };
}

const api = createApiClient<ApiSchema>(baseUrl);

// Full type safety and autocomplete
const users = await api.get("/users");           // User[]
const user = await api.get("/users/:id", { params: { id: "1" } }); // User
const newUser = await api.post("/users", { body: { name: "Alice" } }); // User

// Errors at compile time
await api.get("/nonexistent");                   // Error!
await api.post("/users", { body: { wrong: 1 }}); // Error!
```

**Hints:**
- Use template literal types for URL patterns
- Use conditional types to extract response types
- Consider how to handle URL parameters (`:id`)
- Implement proper error discrimination

**Option C: Open-Ended (Minimal Hints)**

Build a type-safe API client. The only requirements:
- API routes, methods, and payloads must be type-checked
- Wrong routes, wrong methods, or wrong body shapes must produce TypeScript errors

No starter code. No hints. Design the schema format and API yourself.

---

## Labs

### Lab 1: Convert Previous Projects to TypeScript

Take your JavaScript projects from Modules 1-2 and convert them to TypeScript.

**Tasks:**
1. Set up a TypeScript project with proper tsconfig.json - **Core**
2. Rename files from .js to .ts - **Core**
3. Add type annotations to all functions - **Core**
4. Create interfaces for all data structures - **Recommended**
5. Enable strict mode and resolve all errors - **Recommended**
6. Replace any `any` types with proper types - **Stretch**

**Projects to Convert:**
- DOM manipulation projects
- Async/Promise-based code
- Data processing utilities

### Lab 2: Type Challenges

Complete these exercises from [Type Challenges](https://github.com/type-challenges/type-challenges):

**Easy Level (Required):**
- Pick - Implement `Pick<T, K>` from scratch - **Core**
- Readonly - Implement `Readonly<T>` from scratch - **Core**
- Tuple to Object - Convert tuple to object type - **Core**
- First of Array - Get first element type - **Core**
- Length of Tuple - Get tuple length as type - **Recommended**
- Exclude - Implement `Exclude<T, U>` - **Recommended**
- Awaited - Get the type inside a Promise - **Recommended**
- If - Implement conditional type `If<C, T, F>` - **Stretch**
- Concat - Concatenate two tuple types - **Stretch**
- Includes - Check if type exists in tuple - **Stretch**

**Approach:**
1. Understand what the utility type should do
2. Write test cases first
3. Implement using conditional types and mapped types
4. Verify against the expected results

### Lab 3: API Typing Exercises

**Exercise 1: Type a REST API** - **Core**
Given this API documentation, create complete TypeScript types:
- GET /posts - Returns array of posts
- GET /posts/:id - Returns single post
- POST /posts - Creates post, returns created post
- PUT /posts/:id - Updates post, returns updated post
- DELETE /posts/:id - Returns nothing
- GET /posts/:id/comments - Returns array of comments

**Exercise 2: Type a WebSocket API** - **Recommended**
Create types for a real-time chat application:
- Message events (sent, received, edited, deleted)
- Presence events (user joined, left, typing)
- Room events (created, updated, user added/removed)

**Exercise 3: Third-Party API** - **Stretch**
Choose a public API and create complete TypeScript types for it:
- GitHub API
- OpenWeather API
- Spotify API
- Any API you're interested in

---

## Recommended Resources

### Official Documentation
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/) - The definitive guide, read the whole thing
- [TypeScript Playground](https://www.typescriptlang.org/play) - Experiment with types in the browser
- [TypeScript Cheat Sheets](https://www.typescriptlang.org/cheatsheets) - Quick reference for syntax

### Interactive Practice
- [Type Challenges](https://github.com/type-challenges/type-challenges) - Gym for your type muscles
- [TypeScript Exercises](https://typescript-exercises.github.io/) - Progressive difficulty exercises
- [Exercism TypeScript Track](https://exercism.org/tracks/typescript) - Mentored coding exercises

### Video Tutorials
- [No BS TS by Jack Herrington](https://www.youtube.com/playlist?list=PLNqp92_EXZBJYFrpEzdO2EapvU0GOJ09n) - Practical TypeScript series
- [Total TypeScript by Matt Pocock](https://www.totaltypescript.com/) - Deep dives into advanced patterns
- [TypeScript Course by The Net Ninja](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI) - Beginner-friendly walkthrough

### Deep Dives
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/) - Free online book with advanced topics
- [Effective TypeScript](https://effectivetypescript.com/) - 62 specific ways to improve your TypeScript
- [Programming TypeScript](https://www.oreilly.com/library/view/programming-typescript/9781492037644/) - Comprehensive O'Reilly book

### Tools
- [ts-reset](https://github.com/total-typescript/ts-reset) - Improved types for built-in methods
- [zod](https://zod.dev/) - Runtime validation with TypeScript inference
- [ts-pattern](https://github.com/gvergnaud/ts-pattern) - Exhaustive pattern matching

---

## Self-Assessment Checkpoint

Before moving to Module 4, test yourself with these challenges. No hints provided—if you can complete them all, you're ready.

### Challenge 1: Strict Object Type
Create a type `Exact<T>` that only allows objects with exactly the properties of T—no extra properties allowed. Test it with:
```typescript
interface User { name: string; age: number }
const valid: Exact<User> = { name: "Alice", age: 25 }; // OK
const invalid: Exact<User> = { name: "Bob", age: 30, extra: true }; // Should error
```

### Challenge 2: Deep Readonly
Implement `DeepReadonly<T>` that makes all properties readonly, including nested objects:
```typescript
interface Config {
  server: { host: string; port: number };
  features: string[];
}
type ReadonlyConfig = DeepReadonly<Config>;
// All nested properties should be readonly
```

### Challenge 3: Function Overloads
Write a function `process` with proper overloads:
- When passed a string, returns a string
- When passed a number, returns a number
- When passed an array, returns the first element's type

### Challenge 4: Extract Route Params
Create a type that extracts URL parameters from a route string:
```typescript
type Params = ExtractParams<"/users/:userId/posts/:postId">;
// Should be { userId: string; postId: string }
```

### Challenge 5: Type-Safe Builder Pattern
Implement a type-safe query builder where:
- Methods can only be called in valid order
- `select()` must be called before `where()`
- `where()` must be called before `orderBy()`
- TypeScript should error if methods are called out of order

### Challenge 6: Discriminated Union Exhaustiveness
Given this type, write a function that handles all cases with exhaustive checking:
```typescript
type Event =
  | { type: "click"; x: number; y: number }
  | { type: "keypress"; key: string }
  | { type: "scroll"; direction: "up" | "down" };

function handleEvent(event: Event): string {
  // Implement with exhaustive checking
  // TypeScript should error if a case is missing
}
```

---

## Checklist: Module 3 Complete

Before moving to Module 4, verify you can:

- [ ] Annotate variables, functions, and objects with proper types
- [ ] Choose appropriately between interface and type alias
- [ ] Use union and intersection types effectively
- [ ] Write generic functions with constraints
- [ ] Apply utility types (Partial, Pick, Omit, Record, etc.)
- [ ] Implement type guards for runtime type checking
- [ ] Design discriminated unions for complex state
- [ ] Type API responses and error handling
- [ ] Configure tsconfig.json for a project
- [ ] Convert JavaScript code to TypeScript
- [ ] Complete Project 1: Type-Safe Event Emitter
- [ ] Complete Project 2: Typed Fetch Wrapper

---

**Next Module:** Module 4 - React Fundamentals
