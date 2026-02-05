# Module 1: Programming Fundamentals

**Duration:** 8 weeks (1-2 hours/day)
**Philosophy:** Build-Your-Own-X | Heavy Labs | No Solutions Provided

---

## Why JavaScript?

### Why Learn Programming with JavaScript?

JavaScript is one of the most versatile and widely-used programming languages in the world. Here's why it's an excellent choice for learning programming fundamentals:

**Immediate Feedback:** JavaScript runs in any web browser. Open the developer console (F12), type code, and see results instantly. No complex setup, no waiting for compilation.

**Visual Results:** Unlike languages that only output text, JavaScript can manipulate web pages, create animations, and build interactive applications. Seeing your code change things on screen is motivating.

**Massive Ecosystem:** JavaScript has the largest package ecosystem (npm) of any language. Once you learn the fundamentals, you have access to millions of tools and libraries.

**Full-Stack Capability:** JavaScript works on both the frontend (browsers) and backend (Node.js). Learn one language, build complete applications.

**Job Market:** JavaScript consistently ranks as the most in-demand programming language. The skills you build here directly translate to career opportunities.

### What Are the Alternatives?

| Language | Strengths | Why Not Start Here? |
|----------|-----------|---------------------|
| **Python** | Clean syntax, great for data science | Less immediate visual feedback, different paradigm than web development |
| **Java** | Enterprise standard, strongly typed | Verbose syntax, complex setup, slower iteration cycle |
| **C/C++** | Performance, system programming | Manual memory management, steep learning curve |
| **Ruby** | Elegant syntax, Rails framework | Smaller job market, less versatile than JS |
| **Go** | Simplicity, concurrency | Newer ecosystem, primarily backend-focused |

### Why We Chose JavaScript for This Curriculum

1. **React Requires It:** This curriculum leads to React development. JavaScript is non-negotiable for that path.

2. **Lowest Barrier to Entry:** No installation required to start. Every computer with a browser is a JavaScript development environment.

3. **Transferable Concepts:** The programming fundamentals you learn (variables, functions, loops, data structures) apply to every language. JavaScript teaches these concepts while also being the language you'll use professionally.

4. **Community Support:** When you get stuck, there are more JavaScript answers on Stack Overflow, more tutorials, and more documentation than any other language.

5. **Modern Language Features:** JavaScript has evolved significantly. You'll learn modern patterns (arrow functions, destructuring, modules) that represent current best practices across the industry.

**Bottom Line:** JavaScript lets you learn programming fundamentals with minimal friction while building skills directly applicable to modern web development.

---

## Learning Objectives

By the end of this module, you will be able to:
- Write and debug JavaScript programs using core language features
- Work confidently with variables, functions, and control flow
- Manipulate arrays and objects to solve real problems
- Break down complex problems into smaller, manageable steps
- Build functional CLI applications from scratch

---

## Week 1-2: Logic & Flow

### Variables and Data Types

**Primitive Data Types:**
- `number` - integers and decimals (42, 3.14, -17)
- `string` - text enclosed in quotes ("hello", 'world', \`template\`)
- `boolean` - true or false
- `null` - intentional absence of value
- `undefined` - uninitialized or missing value

**Variable Declaration:**
- `let` - block-scoped, can be reassigned
- `const` - block-scoped, cannot be reassigned
- `var` - function-scoped (legacy, avoid in new code)

**Key Concepts:**
- Type coercion and why it matters
- `typeof` operator for checking types
- Naming conventions (camelCase)

### Operators

**Arithmetic:** `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponent)

**Comparison:** `===`, `!==`, `>`, `<`, `>=`, `<=`
- Strict equality (`===`) vs loose equality (`==`) - always use strict

**Logical:** `&&` (AND), `||` (OR), `!` (NOT)
- Short-circuit evaluation
- Truthy and falsy values

**Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, `++`, `--`

### Conditionals

**if/else:**
```javascript
if (condition) {
  // code block
} else if (anotherCondition) {
  // code block
} else {
  // code block
}
```

**switch:**
```javascript
switch (expression) {
  case value1:
    // code
    break;
  case value2:
    // code
    break;
  default:
    // code
}
```

**Ternary:** `condition ? valueIfTrue : valueIfFalse`

### Loops

**for loop:**
```javascript
for (let i = 0; i < 10; i++) {
  // code runs 10 times
}
```

**while loop:**
```javascript
while (condition) {
  // runs while condition is true
}
```

**do-while loop:**
```javascript
do {
  // runs at least once
} while (condition);
```

**Key Concepts:**
- Loop counters and iteration
- `break` and `continue` statements
- Avoiding infinite loops

### Week 1-2 Review Prompts

Before moving on, take 15 minutes to reflect:

1. **What did you learn?**
   - List three concepts that clicked for you this week
   - What surprised you about how JavaScript handles data?

2. **What's still unclear?**
   - Which topic feels shaky? Be specific.
   - What error messages do you keep seeing?

3. **What would you teach someone else?**
   - Pick one concept and explain it in plain English
   - Could you help a friend understand the difference between `let` and `const`?

---

## Week 3-4: Functions & Scope

### Function Declarations vs Expressions

**Declaration (hoisted):**
```javascript
function greet(name) {
  return "Hello, " + name;
}
```

**Expression (not hoisted):**
```javascript
const greet = function(name) {
  return "Hello, " + name;
};
```

**Arrow Function:**
```javascript
const greet = (name) => "Hello, " + name;
```

### Parameters and Return Values

- Parameters vs arguments
- Default parameters: `function greet(name = "World")`
- Rest parameters: `function sum(...numbers)`
- The `return` statement
- Functions without return (return `undefined`)
- Multiple return paths

### Scope

**Global Scope:** Variables declared outside any function/block

**Local (Function) Scope:** Variables declared inside a function

**Block Scope:** Variables declared with `let`/`const` inside `{}`

**Key Concepts:**
- Variable shadowing
- Scope chain lookup
- Why global variables are dangerous

### Closures (Introduction)

A closure is a function that remembers variables from its outer scope even after that scope has finished executing.

```javascript
function createCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}
```

**Key Concepts:**
- Functions can return other functions
- Inner functions maintain access to outer variables
- Practical uses: data privacy, state persistence

### Week 3-4 Review Prompts

Before moving on, take 15 minutes to reflect:

1. **What did you learn?**
   - Can you explain the difference between function declarations and arrow functions?
   - What's the most useful thing about closures?

2. **What's still unclear?**
   - Does scope still feel confusing? Which part?
   - Are you comfortable with when to use `return`?

3. **What would you teach someone else?**
   - How would you explain why we need different types of functions?
   - Could you draw a diagram showing how scope works?

---

## Week 5-6: Data Structures

### Arrays

**Creation:**
```javascript
const fruits = ["apple", "banana", "orange"];
const numbers = new Array(5); // [empty x 5]
```

**Access and Modification:**
- Index-based access: `fruits[0]` returns "apple"
- `.length` property
- Modifying elements: `fruits[1] = "grape"`

**Common Methods:**
- `push()`, `pop()` - add/remove from end
- `unshift()`, `shift()` - add/remove from start
- `slice()` - extract portion (non-destructive)
- `splice()` - add/remove at index (destructive)
- `indexOf()`, `includes()` - searching
- `join()`, `reverse()`, `sort()`

### Objects

**Creation:**
```javascript
const person = {
  name: "Alex",
  age: 30,
  isStudent: false
};
```

**Accessing Properties:**
- Dot notation: `person.name`
- Bracket notation: `person["name"]`

**Methods (functions as properties):**
```javascript
const calculator = {
  add: function(a, b) {
    return a + b;
  }
};
```

**Nesting:** Objects and arrays inside objects

**Key Concepts:**
- Adding/deleting properties
- Checking if property exists (`in` operator, `hasOwnProperty`)
- Object references vs primitives

### Iteration Patterns

**for...of (arrays, strings):**
```javascript
for (const fruit of fruits) {
  console.log(fruit);
}
```

**for...in (object keys):**
```javascript
for (const key in person) {
  console.log(key, person[key]);
}
```

**forEach (array method):**
```javascript
fruits.forEach(function(fruit, index) {
  console.log(index, fruit);
});
```

### Combining Arrays and Objects

- Arrays of objects (common data pattern)
- Objects with array properties
- Nested data structures
- Accessing deeply nested values

### Week 5-6 Review Prompts

Before moving on, take 15 minutes to reflect:

1. **What did you learn?**
   - When would you use an array vs an object?
   - Which array methods do you use most often?

2. **What's still unclear?**
   - Do you understand the difference between `slice` and `splice`?
   - Can you confidently access deeply nested data?

3. **What would you teach someone else?**
   - How would you explain objects to someone who only knows arrays?
   - Could you list five common things you do with arrays?

---

## Week 7-8: Problem Solving

### Breaking Down Problems

1. **Understand the problem** - What are the inputs? What is the expected output?
2. **Identify the steps** - What operations need to happen?
3. **Start simple** - Solve the smallest version first
4. **Build up** - Add complexity incrementally
5. **Test edge cases** - Empty inputs, large inputs, unexpected values

### Pseudocode Writing

Write logic in plain English before coding:

```
FUNCTION findLargest(numbers)
  SET largest TO first number
  FOR EACH number IN numbers
    IF number > largest
      SET largest TO number
  RETURN largest
```

### Debugging Strategies

- `console.log()` strategically placed
- Read error messages carefully (line numbers, error types)
- Rubber duck debugging (explain your code out loud)
- Binary search debugging (comment out half the code)
- Check your assumptions with typeof and console.log
- Common errors: off-by-one, undefined variables, type mismatches

### Basic Algorithms

**Linear Search:** Check each element until found

**Binary Search:** Divide and conquer on sorted data (concept only)

**Bubble Sort:** Compare adjacent elements and swap

**Selection Sort:** Find minimum, place at start, repeat

Focus on understanding the logic, not memorizing implementations.

### Week 7-8 Review Prompts

Before moving on, take 15 minutes to reflect:

1. **What did you learn?**
   - How has your approach to problem-solving changed?
   - What debugging technique works best for you?

2. **What's still unclear?**
   - Are there algorithm concepts that still feel abstract?
   - Do you struggle with any particular type of problem?

3. **What would you teach someone else?**
   - How would you explain your debugging process step-by-step?
   - Could you walk someone through writing pseudocode?

---

## Build-Your-Own Projects

### Project 1: CLI Calculator

Build a command-line calculator that performs basic arithmetic operations.

**Requirements:**
- Accept two numbers and an operator from the user
- Support addition, subtraction, multiplication, and division
- Handle division by zero gracefully
- Display the result with a clear format
- Allow the user to perform multiple calculations without restarting
- Include an option to exit the program

**Starter Considerations:**
- How will you get user input? (research `readline` or `prompt-sync`)
- How will you determine which operation to perform?
- What happens if the user enters invalid input?

**Stretch Goals:**
- Add support for exponents and modulo
- Implement a history feature showing recent calculations
- Allow chaining operations (e.g., 5 + 3 * 2)

#### Project Variations

**Option A: Guided (More Structure)**
Build the calculator in these specific steps:
1. First, create a function that adds two hardcoded numbers and prints the result
2. Modify it to accept two numbers as function parameters
3. Add a function for each operation (add, subtract, multiply, divide)
4. Add user input for the two numbers only (hardcode the operator first)
5. Add user input for the operator
6. Add a loop to allow multiple calculations
7. Add error handling for invalid inputs
8. Add the exit option

**Option B: Standard (Current Approach)**
Follow the requirements above. Research what you need. Build it your way.

**Option C: Open-Ended (Minimal Requirements)**
Build something that does math based on user input. That's it. Make it yours. Add whatever features interest you. The only rule: it must work and handle errors gracefully.

---

### Project 2: Number Guessing Game

Build a game where the computer picks a random number and the user tries to guess it.

**Requirements:**
- Generate a random number between 1 and 100
- Prompt the user to guess the number
- Provide hints: "Too high" or "Too low"
- Track the number of guesses
- Display a congratulatory message with guess count when correct
- Ask if the user wants to play again

**Starter Considerations:**
- How do you generate a random integer in JavaScript? (research `Math.random()`)
- How will you keep the game running until the correct guess?
- How will you track and display the number of attempts?

**Stretch Goals:**
- Add difficulty levels (easy: 1-50, medium: 1-100, hard: 1-500)
- Implement a maximum number of guesses
- Track and display high scores across games

#### Project Variations

**Option A: Guided (More Structure)**
Build the game in these specific steps:
1. First, generate a random number and print it (to verify it works)
2. Hardcode a guess and check if it matches (print "correct" or "wrong")
3. Add the "too high" / "too low" logic
4. Add user input for the guess (single guess only)
5. Add a loop to allow multiple guesses
6. Add the guess counter
7. Add the congratulations message
8. Add the "play again" feature
9. Remove the line that prints the answer

**Option B: Standard (Current Approach)**
Follow the requirements above. Research what you need. Build it your way.

**Option C: Open-Ended (Minimal Requirements)**
The computer picks a number. The human tries to guess it. The computer gives feedback. That's all you're given. Design the experience. What makes a guessing game fun? Build that.

---

### Project 3: Todo List (CLI)

Build a command-line todo list manager with persistent task tracking.

**Requirements:**
- Add new tasks with a description
- List all tasks with their status (pending/complete)
- Mark tasks as complete by ID or index
- Remove tasks from the list
- Display a menu of available actions
- Handle invalid inputs gracefully

**Starter Considerations:**
- What data structure will you use to store tasks?
- How will you identify each task uniquely?
- How will you keep the program running until the user exits?

**Stretch Goals:**
- Add due dates to tasks
- Filter tasks by status (show only pending or only complete)
- Save tasks to a file so they persist between sessions (research `fs` module)
- Add priority levels (high, medium, low)

#### Project Variations

**Option A: Guided (More Structure)**
Build the todo list in these specific steps:
1. Create an array to store tasks, add two hardcoded tasks, print them
2. Write a function to display all tasks with their index
3. Write a function to add a task (hardcode the task text first)
4. Add user input for the task text
5. Write a function to mark a task complete (hardcode the index first)
6. Add user input for which task to complete
7. Write a function to remove a task
8. Create a menu that shows all options
9. Add a loop that shows the menu and waits for user choice
10. Add input validation and error messages

**Option B: Standard (Current Approach)**
Follow the requirements above. Research what you need. Build it your way.

**Option C: Open-Ended (Minimal Requirements)**
Build something that manages a list of things to do. The user should be able to add things, see things, and mark things done. Everything else is up to you. What would make this actually useful for you personally?

---

## Labs

### Lab Difficulty Key

- **Core** - Must complete before moving on. These build essential skills.
- **Recommended** - Reinforces understanding. Do these if you have time.
- **Stretch** - For deeper mastery. Challenge yourself when ready.

---

### Week 1-2 Labs: Logic & Flow

**Lab 1.1: Variable Swap** - Core
Write a program that swaps the values of two variables without using a third variable. Start with `let a = 5; let b = 10;` and end with `a = 10; b = 5`.

**Lab 1.2: Temperature Converter** - Core
Create a program that converts temperatures between Celsius and Fahrenheit. The user should specify the input scale and value, and receive the converted result.

**Lab 1.3: Grade Calculator** - Core
Write a program that takes a numerical score (0-100) and outputs the letter grade. Handle edge cases like scores below 0 or above 100.

**Lab 1.4: FizzBuzz** - Core
Print numbers from 1 to 100. For multiples of 3, print "Fizz" instead. For multiples of 5, print "Buzz". For multiples of both, print "FizzBuzz".

**Lab 1.5: Leap Year Checker** - Recommended
Write a program that determines if a given year is a leap year. Remember: leap years are divisible by 4, except century years must also be divisible by 400.

**Lab 1.6: Number Pyramid** - Recommended
Using nested loops, print a number pyramid of n rows:
```
1
12
123
1234
```

**Lab 1.7: Prime Number Checker** - Stretch
Write a program that checks if a given number is prime. A prime number is only divisible by 1 and itself.

---

### Week 3-4 Labs: Functions & Scope

**Lab 2.1: Function Factory** - Core
Write three versions of the same function (declaration, expression, arrow) that calculates the area of a rectangle. Verify all three work identically.

**Lab 2.2: Default Greeting** - Core
Create a `greet` function that takes a name and a greeting. If no greeting is provided, default to "Hello". If no name is provided, default to "World".

**Lab 2.3: Sum All** - Core
Write a function using rest parameters that accepts any number of arguments and returns their sum. `sumAll(1, 2, 3, 4)` should return 10.

**Lab 2.4: Scope Detective** - Recommended
Given a code snippet with multiple nested scopes, predict the output without running it. Then run it to verify. Create three examples that demonstrate scope chain behavior.

**Lab 2.5: Counter Factory** - Core
Using closures, create a function that returns a new counter. Each counter should independently track its own count with `increment()`, `decrement()`, and `getCount()` methods.

**Lab 2.6: Once Function** - Stretch
Create a higher-order function called `once` that takes a function as an argument and returns a new function that can only be called once. Subsequent calls should return the result of the first call.

---

### Week 5-6 Labs: Data Structures

**Lab 3.1: Array Statistics** - Core
Write functions that calculate the min, max, sum, and average of an array of numbers without using built-in Math methods.

**Lab 3.2: Remove Duplicates** - Core
Write a function that takes an array and returns a new array with all duplicate values removed. Do not use Set.

**Lab 3.3: Array Rotation** - Recommended
Write a function that rotates an array by k positions. `rotate([1,2,3,4,5], 2)` should return `[4,5,1,2,3]`.

**Lab 3.4: Object Merge** - Core
Write a function that merges two objects. If both objects have the same key, the second object's value should be used.

**Lab 3.5: Nested Value Access** - Recommended
Write a function that safely accesses nested object properties. Given an object and a path like "user.address.city", return the value or undefined if any part of the path doesn't exist.

**Lab 3.6: Array of Objects** - Core
Given an array of student objects with `name` and `grade` properties, write functions to: find the highest grade, calculate the class average, and return all students above a certain grade.

**Lab 3.7: Frequency Counter** - Stretch
Write a function that takes a string and returns an object with each character as a key and its count as the value. "hello" returns `{h: 1, e: 1, l: 2, o: 1}`.

---

### Week 7-8 Labs: Problem Solving

**Lab 4.1: Palindrome Checker** - Core
Write a function that checks if a string is a palindrome (reads the same forwards and backwards). Ignore case and non-alphanumeric characters.

**Lab 4.2: Anagram Detector** - Recommended
Write a function that determines if two strings are anagrams of each other (contain the same characters in different order).

**Lab 4.3: Find the Missing Number** - Core
Given an array containing n distinct numbers from 0 to n, find the one number that is missing. Array `[3, 0, 1]` is missing `2`.

**Lab 4.4: Two Sum** - Core
Given an array of numbers and a target sum, find two numbers that add up to the target. Return their indices.

**Lab 4.5: Implement Linear Search** - Core
Write a function that implements linear search. Return the index of the target element, or -1 if not found.

**Lab 4.6: Implement Bubble Sort** - Recommended
Write a function that sorts an array using the bubble sort algorithm. Do not use the built-in sort method.

**Lab 4.7: Flatten Array** - Stretch
Write a function that flattens a nested array to a single level. `[1, [2, [3, 4]], 5]` becomes `[1, 2, 3, 4, 5]`. Do not use the built-in flat method.

**Lab 4.8: Valid Parentheses** - Stretch
Write a function that determines if a string of parentheses is valid. Every opening parenthesis must have a corresponding closing parenthesis in the correct order.

---

## Weekly Milestones

| Week | Focus | Deliverable |
|------|-------|-------------|
| 1 | Variables, Operators | Labs 1.1-1.3 complete |
| 2 | Conditionals, Loops | Labs 1.4-1.7 complete, Project 1 started |
| 3 | Functions | Labs 2.1-2.3 complete, Project 1 complete |
| 4 | Scope, Closures | Labs 2.4-2.6 complete, Project 2 started |
| 5 | Arrays | Labs 3.1-3.4 complete, Project 2 complete |
| 6 | Objects, Iteration | Labs 3.5-3.7 complete, Project 3 started |
| 7 | Problem Solving | Labs 4.1-4.4 complete |
| 8 | Algorithms, Review | Labs 4.5-4.8 complete, Project 3 complete |

---

## Recommended Resources

### Video Tutorials

**For Visual Learners:**
- **Traversy Media (YouTube)** - "JavaScript Crash Course for Beginners" - Fast-paced, practical introduction
- **The Coding Train (YouTube)** - Creative coding approach, great for understanding loops and logic visually
- **Fireship (YouTube)** - "JavaScript in 100 Seconds" and deeper dives - concise, modern explanations
- **freeCodeCamp (YouTube)** - Full-length courses if you want comprehensive video instruction

**When to Use:** Watch videos when reading isn't clicking. Sometimes seeing someone code helps concepts land.

### Practice Platforms

**For Repetition and Skill Building:**
- **freeCodeCamp** (freecodecamp.org) - Free, structured curriculum with instant feedback
- **Exercism** (exercism.org) - Mentored exercises, excellent for functions and problem-solving
- **Codewars** (codewars.com) - Gamified challenges ranked by difficulty (start with 8kyu and 7kyu)
- **LeetCode** (leetcode.com) - More advanced, good for Week 7-8 algorithm practice
- **JavaScript30** (javascript30.com) - 30 vanilla JS projects (more relevant after this module)

**When to Use:** When you finish labs early or want extra practice. Aim for quantity - doing 50 easy problems teaches more than struggling on 5 hard ones.

### Documentation

**Your Primary References:**
- **MDN Web Docs** (developer.mozilla.org) - The definitive JavaScript reference. Bookmark it. Use it constantly.
- **JavaScript.info** (javascript.info) - Tutorial-style documentation, excellent explanations with examples
- **DevDocs** (devdocs.io) - Combines multiple documentation sources, works offline

**When to Use:** Every time you forget syntax or want to understand a method better. Learning to read documentation is a skill - practice it.

### Books (Optional)

- **Eloquent JavaScript** (eloquentjavascript.net) - Free online, excellent for deeper understanding
- **You Don't Know JS** (github.com/getify/You-Dont-Know-JS) - Free online, goes deep into how JS works

**When to Use:** If you want to understand the "why" behind JavaScript behaviors, not just the "how."

### Community

- **Stack Overflow** - Search before asking. Your question has probably been answered.
- **Reddit r/learnjavascript** - Beginner-friendly community for questions
- **Discord servers** - Many coding communities have help channels (freeCodeCamp, Traversy Media, etc.)

**When to Use:** When you're truly stuck after trying for 20+ minutes. Describe what you tried, not just what's wrong.

---

## Resources for Self-Study

**Documentation:**
- MDN Web Docs (JavaScript reference)
- JavaScript.info (tutorials)

**Practice:**
- Run code in browser console (F12 > Console)
- Use Node.js for CLI programs
- Experiment freely - breaking things teaches you

**Debugging:**
- Read error messages completely
- Google exact error messages
- Explain your code to someone (or something) else

---

## Assessment Criteria

You have mastered this module when you can:

- [ ] Declare variables and explain when to use `let` vs `const`
- [ ] Use all comparison and logical operators correctly
- [ ] Write conditionals that handle multiple cases
- [ ] Choose the right loop for different situations
- [ ] Write functions with parameters and return values
- [ ] Explain scope and identify variable accessibility
- [ ] Create and manipulate arrays using common methods
- [ ] Work with objects and access nested properties
- [ ] Iterate over arrays and objects with appropriate methods
- [ ] Break down problems into pseudocode before coding
- [ ] Debug code systematically using console.log
- [ ] Complete all three projects independently

---

## Self-Assessment Checkpoint: Can You Do This?

Before moving to Module 2, test yourself with these challenges. **No hints provided.** If you can complete all of them without looking anything up, you're ready to move on.

### Challenge 1: Reverse a String
Write a function `reverseString(str)` that takes a string and returns it reversed. Do not use the built-in `reverse()` method.

### Challenge 2: Count Vowels
Write a function `countVowels(str)` that returns the number of vowels (a, e, i, o, u) in a string. Handle both uppercase and lowercase.

### Challenge 3: Find Second Largest
Write a function `secondLargest(arr)` that takes an array of numbers and returns the second largest number. Handle edge cases (duplicates, arrays with fewer than 2 elements).

### Challenge 4: Title Case
Write a function `titleCase(str)` that converts a string to title case (first letter of each word capitalized, rest lowercase). "hello WORLD" becomes "Hello World".

### Challenge 5: Group by Property
Write a function `groupBy(arr, property)` that takes an array of objects and a property name, and returns an object where keys are the unique values of that property and values are arrays of objects with that property value.

Example:
```javascript
const people = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 25 }
];
groupBy(people, "age");
// Returns: { 25: [{name: "Alice", age: 25}, {name: "Charlie", age: 25}], 30: [{name: "Bob", age: 30}] }
```

### Challenge 6: Build a Simple Program
Without any guidance, build a program that:
- Stores a list of items (you decide what kind)
- Lets the user add items
- Lets the user search for items
- Displays results clearly

---

### How Did You Do?

**Completed all 6 with confidence?**
You're ready for Module 2. Your fundamentals are solid.

**Struggled with Challenges 1-4?**
Review Weeks 1-4. Focus on string manipulation, loops, and basic functions. Redo Labs 1.4, 2.3, and 3.1.

**Struggled with Challenge 5?**
Review Week 5-6. Practice with arrays of objects. Redo Labs 3.4 and 3.6.

**Struggled with Challenge 6?**
You may understand individual concepts but need practice combining them. Redo Project 3 from scratch using a different variation than before.

**Couldn't start most challenges?**
That's okay - it means you need more practice, not that you can't do this. Go back to Week 1, but this time focus on typing out every code example yourself. Don't copy-paste. The repetition builds intuition.

---

**Remember:** Struggling is part of learning. If you're not stuck sometimes, you're not challenging yourself enough. Use documentation, experiment, and figure it out.
