# Module 4: React with TypeScript

**Duration:** 10 weeks (1-2 hours/day)
**Philosophy:** Build-Your-Own-X approach with heavy labs. No solutions provided.

---

## Why React?

### Why React Over Other Frameworks?

**React vs Vue:**
- React has a larger ecosystem and job market
- React's "learn once, write anywhere" applies to React Native, Electron, etc.
- Vue is excellent but has a smaller community and fewer third-party libraries
- React's explicit data flow makes debugging easier in large applications

**React vs Svelte:**
- Svelte compiles away the framework, resulting in smaller bundles
- However, React's virtual DOM approach offers better debugging tools
- React's ecosystem is vastly larger (component libraries, tutorials, jobs)
- Svelte is newer—fewer battle-tested patterns for complex apps

**React vs Angular:**
- Angular is opinionated and includes everything (routing, forms, HTTP)
- React is "just the view layer"—you choose your own tools
- Angular has a steeper learning curve due to TypeScript decorators, RxJS, etc.
- React's flexibility makes it easier to adopt incrementally

### What Problems Does React Solve?

1. **UI as a function of state:** You describe what the UI should look like for any given state, and React handles updates efficiently.

2. **Component reusability:** Build once, use everywhere. Components encapsulate markup, styles, and behavior.

3. **Predictable data flow:** One-way data flow makes it easier to understand how data changes propagate.

4. **Declarative programming:** You say "what" you want, not "how" to do it. React handles DOM manipulation.

5. **Performance at scale:** Virtual DOM and reconciliation algorithm efficiently update only what changed.

### Why React Is Still Dominant in 2026

- **Massive ecosystem:** More npm packages, component libraries, and tools than any competitor
- **Meta's continued investment:** React Server Components, Concurrent Features, and ongoing development
- **Job market:** Most frontend job listings still require React
- **Community knowledge:** More tutorials, Stack Overflow answers, and battle-tested patterns
- **Framework flexibility:** Works with any backend, any state management, any styling approach

### Why TypeScript with React?

- **Catch errors at compile time:** Typos in prop names, wrong prop types, missing required props
- **Better IDE support:** Autocomplete, refactoring, and go-to-definition work perfectly
- **Self-documenting code:** Interfaces describe exactly what a component expects
- **Refactoring confidence:** Rename a prop and TypeScript shows you every place to update
- **Industry standard:** Most React codebases in 2026 use TypeScript

---

## Learning Objectives

By the end of this module, you will:
- Build complete React applications with TypeScript
- Manage component state and side effects
- Create reusable, accessible component libraries
- Implement data fetching patterns
- Write tests for React components
- Deploy React applications to production

---

## Week 1-2: Fundamentals

### Topics

**Components and JSX**
- Function components in TypeScript
- JSX syntax and expressions
- Conditional rendering
- Rendering lists with keys
- Fragment syntax

**Props and Prop Types**
- Defining prop interfaces
- Required vs optional props
- Default prop values
- Union types for props
- The `children` prop type (`React.ReactNode`)

**Component Composition**
- Breaking UI into components
- Single responsibility principle
- Container vs presentational components
- Compound components pattern

**Children Pattern**
- Passing children to components
- Render props pattern
- Slot pattern for flexible layouts

**Project Setup with Vite**
- Creating a React + TypeScript project
- Project structure conventions
- ESLint and Prettier configuration
- Path aliases with `tsconfig.json`

### Reading

- React documentation: "Describing the UI" section
- TypeScript handbook: "Everyday Types"
- Vite documentation: "Getting Started"

### Lab 1.1: Counter Variations
🔴 **Core** — must complete before moving on

Build three counter implementations:

1. **Basic Counter**
   - Increment, decrement, reset buttons
   - Display current count
   - Prevent negative numbers

2. **Step Counter**
   - Configurable step amount via props
   - Min and max boundaries
   - Display as progress bar

3. **Multiple Counters**
   - Add/remove counter instances
   - Each counter independent
   - Total sum displayed

**Requirements:**
- All counters must be TypeScript components
- Props must have proper interfaces
- No inline styles (use CSS modules or classes)

### Lab 1.2: Accordion Component
🟡 **Recommended** — reinforces understanding

Build an accordion that:
- Accepts an array of items (title + content)
- Only one item open at a time (or optionally multiple)
- Smooth open/close animations
- Keyboard accessible (Enter/Space to toggle)
- Proper ARIA attributes

**Props interface to implement:**
```typescript
interface AccordionItem {
  id: string;
  title: string;
  content: React.ReactNode;
}

interface AccordionProps {
  items: AccordionItem[];
  allowMultiple?: boolean;
  defaultOpenId?: string;
}
```

### Weekly Review Prompts

Before moving to Week 3-4, reflect on these questions:

1. **What did you learn?**
   - What React concepts clicked for you this week?
   - What TypeScript patterns are you starting to internalize?

2. **What's still unclear?**
   - Which concepts do you need to revisit?
   - What error messages are you still confused by?

3. **What would you teach someone else?**
   - If you had to explain components and props to a beginner, what would you say?
   - What analogy would you use for JSX?

---

## Week 3-4: State & Events

### Topics

**useState Hook**
- State initialization
- Updating state immutably
- State with objects and arrays
- Lazy initial state
- TypeScript generics with useState

**Event Handling**
- Event handler types (`React.MouseEvent`, `React.ChangeEvent`, etc.)
- Synthetic events
- Event delegation
- Preventing default behavior

**Controlled vs Uncontrolled Inputs**
- Controlled input pattern
- When to use uncontrolled inputs
- `useRef` for uncontrolled access
- File inputs

**Forms and Validation**
- Form state management
- Real-time validation
- Submit validation
- Error message display
- TypeScript for form data

**Lifting State Up**
- Identifying shared state
- Single source of truth
- Passing callbacks to children
- State colocation principles

### Reading

- React documentation: "Adding Interactivity" and "Managing State"
- React TypeScript Cheatsheet: Forms and Events

### Lab 3.1: Search Filter
🔴 **Core** — must complete before moving on

Build a searchable, filterable list:

**Requirements:**
- Text search input (debounced)
- Category filter dropdown
- Sort by multiple fields
- Clear all filters button
- Display result count
- Empty state when no results

**Data structure:**
```typescript
interface Product {
  id: string;
  name: string;
  category: string;
  price: number;
  inStock: boolean;
  rating: number;
}
```

### Lab 3.2: Multi-Step Form Wizard
🔴 **Core** — must complete before moving on

Build a multi-step form with:

**Step 1: Personal Information**
- Name, email, phone
- All fields required
- Email format validation

**Step 2: Address**
- Street, city, state, zip
- State dropdown
- Zip code format validation

**Step 3: Preferences**
- Newsletter opt-in
- Contact preference (email/phone/none)
- Interests (multiple selection)

**Step 4: Review & Submit**
- Display all entered data
- Edit buttons to jump to specific steps
- Submit button

**Requirements:**
- Progress indicator showing current step
- Back/Next navigation
- Persist data between steps
- Validate before allowing next step
- TypeScript interfaces for all form data
- Accessible form labels and error messages

### Weekly Review Prompts

Before moving to Week 5-6, reflect on these questions:

1. **What did you learn?**
   - How does state differ from props?
   - When do you choose controlled vs uncontrolled inputs?

2. **What's still unclear?**
   - Are you comfortable with immutable state updates?
   - Do you understand why we lift state up?

3. **What would you teach someone else?**
   - How would you explain the useState hook to someone who only knows vanilla JS?
   - What mental model do you use for form validation?

---

## Week 5-6: Effects & Data

### Topics

**useEffect Hook**
- Effect dependencies
- When effects run
- Strict Mode and double invocation
- Effects vs event handlers

**Cleanup Functions**
- Subscription cleanup
- Timer cleanup
- Why cleanup matters
- Cleanup timing

**Data Fetching Patterns**
- Fetch in useEffect
- Race conditions
- Caching considerations
- Error boundaries for fetch errors

**Loading and Error States**
- Loading spinners and skeletons
- Error message display
- Retry mechanisms
- Optimistic updates

**Abort Controllers**
- AbortController API
- Canceling fetch requests
- Cleanup with abort
- Timeout patterns

### Reading

- React documentation: "Escape Hatches" section
- MDN: AbortController
- Article: "How to fetch data with React Hooks"

### Lab 5.1: Data Table
🔴 **Core** — must complete before moving on

Build a data table component with:

**Features:**
- Fetch data from a public API (JSONPlaceholder, etc.)
- Column sorting (ascending/descending)
- Text search across all fields
- Pagination (configurable page size)
- Loading skeleton while fetching
- Error state with retry button

**Requirements:**
- Abort fetch on component unmount
- Abort previous fetch when filters change
- Debounce search input
- URL state sync (filters in query params)
- TypeScript generics for table data type

**Bonus challenges:**
- Column visibility toggle
- Row selection with checkboxes
- Export to CSV

### Lab 5.2: Kanban Board
🟡 **Recommended** — reinforces understanding

Build a Kanban-style task board:

**Columns:**
- To Do
- In Progress
- Done

**Features:**
- Add new tasks
- Move tasks between columns (buttons, not drag-drop)
- Edit task title and description
- Delete tasks
- Persist to localStorage
- Filter by search term
- Task count per column

**Data structure:**
```typescript
interface Task {
  id: string;
  title: string;
  description: string;
  status: 'todo' | 'in-progress' | 'done';
  createdAt: Date;
}
```

**Requirements:**
- Optimistic UI updates
- Confirmation before delete
- Empty state for columns
- Mobile responsive layout

### Weekly Review Prompts

Before moving to Week 7-8, reflect on these questions:

1. **What did you learn?**
   - What are the common pitfalls with useEffect?
   - How do you handle race conditions in data fetching?

2. **What's still unclear?**
   - Do you understand when effects run vs when they clean up?
   - Are you comfortable with the dependency array?

3. **What would you teach someone else?**
   - How would you explain AbortController to a colleague?
   - What's your strategy for loading and error states?

---

## Week 7-8: Patterns & Performance

### Topics

**useContext for State Sharing**
- Creating context
- Provider pattern
- Consuming context
- Context with TypeScript
- When to use context vs props

**useReducer for Complex State**
- Reducer pattern
- Actions and dispatch
- useReducer vs useState
- TypeScript discriminated unions for actions
- Combining with context

**Custom Hooks**
- Extracting logic into hooks
- Hook composition
- Return values and conventions
- Testing custom hooks

**useRef**
- DOM references
- Mutable values without re-render
- Previous value pattern
- Forward refs

**Performance Basics**
- React's rendering behavior
- When to optimize (measure first)
- React.memo
- useMemo and useCallback
- Avoiding premature optimization

### Reading

- React documentation: "Reusing Logic with Custom Hooks"
- React documentation: "Scaling Up with Reducer and Context"
- Article: "Before You memo()"

### Build-Your-Own: Custom Hooks

Implement these hooks from scratch:

#### Project Variations

**Option A: Guided (Step-by-step)**
Follow this structure for each hook:
1. Start with a basic version that handles the happy path
2. Add TypeScript types one at a time
3. Handle edge cases (null, undefined, SSR)
4. Add error handling
5. Write tests for each step

**Option B: Standard (Current approach)**
Use the signatures below and implement each hook to spec. Reference the React docs if stuck, but write the code yourself.

**Option C: Open-ended (Just requirements)**
Build a collection of 4+ reusable hooks that solve real problems you've encountered. They must be typed, tested, and handle edge cases. You choose which hooks to build.

---

**useLocalStorage**
```typescript
function useLocalStorage<T>(key: string, initialValue: T): [T, (value: T) => void]
```
- Sync state with localStorage
- Handle JSON serialization
- Handle SSR (no window)
- Update when other tabs change (storage event)

**useFetch**
```typescript
function useFetch<T>(url: string): {
  data: T | null;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}
```
- Loading and error states
- Abort on unmount or URL change
- Refetch function
- Optional caching

**useDebounce**
```typescript
function useDebounce<T>(value: T, delay: number): T
```
- Return debounced value
- Reset timer on value change
- Cleanup on unmount

**useClickOutside**
```typescript
function useClickOutside(ref: RefObject<HTMLElement>, handler: () => void): void
```
- Detect clicks outside element
- Handle touch events
- Cleanup listeners

### Lab 7.1: Theme Context
🟡 **Recommended** — reinforces understanding

Implement a theme system:

**Requirements:**
- ThemeProvider component
- useTheme hook
- Light/dark/system modes
- Persist preference to localStorage
- System preference detection
- CSS variables for theme values
- Toggle component

### Weekly Review Prompts

Before moving to Week 9-10, reflect on these questions:

1. **What did you learn?**
   - When do you reach for context vs prop drilling?
   - What makes a good custom hook?

2. **What's still unclear?**
   - Are you comfortable with the reducer pattern?
   - Do you understand when to optimize and when not to?

3. **What would you teach someone else?**
   - How would you explain the difference between useMemo and useCallback?
   - What rules would you give someone for creating custom hooks?

---

## Week 9-10: Modern React

### Topics

**React Server Components (Concepts)**
- Server vs client components
- "use client" directive
- Benefits and trade-offs
- Mental model for RSC
- When to use each

**Suspense and Streaming**
- Suspense for data fetching
- Loading fallbacks
- Streaming HTML
- Nested Suspense boundaries

**Testing with Vitest + React Testing Library**
- Setting up Vitest
- Component testing philosophy
- Querying elements
- User event simulation
- Async testing
- Mock patterns

**Accessibility Basics**
- Semantic HTML in React
- ARIA attributes
- Focus management
- Keyboard navigation
- Screen reader testing

### Reading

- React documentation: "Server Components"
- Testing Library documentation
- WebAIM: Introduction to Web Accessibility

### Build-Your-Own: Component Library

Build an accessible component library:

#### Project Variations

**Option A: Guided (Step-by-step)**
Build each component in order, with each building on the previous:
1. Start with Button (learn variants, sizes, states)
2. Build Modal (learn portals, focus trap, keyboard handling)
3. Build Dropdown (combines Button + Modal concepts)
4. Build Toast (state management for multiple instances)
5. Build Tabs (ARIA roles, keyboard nav)

For each component:
- First, make it render correctly
- Then, add TypeScript props
- Then, add accessibility
- Then, add tests
- Then, add documentation

**Option B: Standard (Current approach)**
Build all five components to the specifications below. Each must be fully typed, accessible, and tested.

**Option C: Open-ended (Just requirements)**
Build a component library of 5+ components that you would actually use in a project. Requirements:
- Must include at least one modal/overlay component
- Must include at least one form-related component
- Must include at least one navigation component
- All components must be keyboard accessible
- All components must have TypeScript props
- Must include a demo page showing all components

---

**Button**
- Variants: primary, secondary, outline, ghost
- Sizes: sm, md, lg
- Loading state with spinner
- Disabled state
- Icon support (left/right)
- Full TypeScript props

**Modal**
- Portal rendering
- Focus trap inside modal
- Close on Escape key
- Close on backdrop click (optional)
- Animate in/out
- Prevent body scroll

**Dropdown**
- Trigger button
- Menu positioning
- Keyboard navigation (arrows, Enter, Escape)
- Close on outside click
- Support for icons and disabled items

**Toast**
- Toast container with positioning
- Multiple toasts stacked
- Auto-dismiss with timer
- Pause on hover
- Types: success, error, warning, info
- Manual dismiss

**Tabs**
- Horizontal and vertical orientation
- Keyboard navigation
- Proper ARIA roles
- Controlled and uncontrolled modes
- Lazy vs eager panel rendering

**Requirements for all components:**
- Full TypeScript interfaces
- ARIA compliant
- Keyboard accessible
- Documented props
- Unit tests with React Testing Library

### Lab 9.1: Testing Practice
🔴 **Core** — must complete before moving on

Write tests for your Kanban board:

**Test cases to cover:**
- Renders all columns
- Adds a new task
- Moves task between columns
- Edits task title
- Deletes task with confirmation
- Filters tasks by search
- Persists to localStorage

**Requirements:**
- Use React Testing Library queries
- Test user interactions, not implementation
- Mock localStorage
- Test async operations
- Achieve 80% coverage

### Weekly Review Prompts

Before completing this module, reflect on these questions:

1. **What did you learn?**
   - How do Server Components change your mental model?
   - What's your testing philosophy now?

2. **What's still unclear?**
   - Are there accessibility patterns you need more practice with?
   - Do you understand when to use Suspense?

3. **What would you teach someone else?**
   - How would you explain the testing pyramid for React apps?
   - What's the most important accessibility lesson from this module?

---

## Third Deploy Checkpoint: React App to Vercel
🔴 **Core** — must complete before moving on

Deploy your best React project to Vercel.

### Requirements

**Project selection:**
- Choose Kanban board, data table, or component library demo
- Must be a complete, polished application
- Include proper error handling
- Mobile responsive

**Deployment steps:**
1. Push project to GitHub repository
2. Connect repository to Vercel
3. Configure build settings (Vite defaults usually work)
4. Set up environment variables if needed
5. Deploy and verify

**Verification checklist:**
- [ ] App loads without console errors
- [ ] All features work in production
- [ ] Responsive on mobile devices
- [ ] Lighthouse performance score > 80
- [ ] Accessible (run Lighthouse accessibility audit)

**Bonus:**
- Set up preview deployments for PRs
- Add custom domain
- Configure analytics

---

## Recommended Resources

### Official Documentation
- [React Documentation](https://react.dev) — The official React docs, completely rewritten in 2023. Start here.
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/) — Official TypeScript documentation
- [Vite Documentation](https://vitejs.dev) — Build tool documentation
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) — Testing library docs

### Video Tutorials
- **React.dev Learn Section** — Interactive tutorials built into the official docs
- **Codevolution React Playlist** — Comprehensive YouTube series covering fundamentals to advanced
- **Jack Herrington** — YouTube channel with advanced React patterns and TypeScript
- **Theo Browne (t3.gg)** — Modern React ecosystem and best practices

### Practice Platforms
- **React Challenges on Frontend Mentor** — Build real projects with designs provided
- **Exercism React Track** — Mentored exercises for React
- **CodeSandbox** — Quick prototyping and sharing React code
- **StackBlitz** — Browser-based IDE for React projects

### Component Library Examples (Study Their Code)
- [Radix UI](https://www.radix-ui.com/) — Unstyled, accessible components
- [shadcn/ui](https://ui.shadcn.com/) — Copy-paste components built on Radix
- [Headless UI](https://headlessui.com/) — Unstyled components from Tailwind team
- [Chakra UI](https://chakra-ui.com/) — Accessible component library with great DX
- [Mantine](https://mantine.dev/) — Full-featured React component library

### Tools
- React DevTools browser extension
- VS Code extensions: ES7+ React snippets, Prettier
- Vitest UI for test visualization

### Practice APIs
- JSONPlaceholder (fake REST API)
- PokeAPI (Pokemon data)
- OpenWeatherMap (weather data)

---

## Self-Assessment Checklist

Before moving to Module 5, verify you can:

- [ ] Create React components with TypeScript props
- [ ] Manage component state with useState and useReducer
- [ ] Handle forms with validation
- [ ] Fetch data with proper loading/error states
- [ ] Create and use custom hooks
- [ ] Use context for global state
- [ ] Write component tests
- [ ] Build accessible components
- [ ] Deploy React apps to Vercel

---

## Can You Do This? (Final Self-Assessment)

If you can complete these challenges without hints or tutorials, you're ready for Module 5. If you struggle, revisit the relevant sections before moving on.

### Challenge 1: Dynamic Form Generator
Build a component that accepts a JSON schema and renders a form dynamically. The schema defines field types (text, number, select, checkbox), validation rules, and labels. The form should validate on submit and return typed form data.

### Challenge 2: Infinite Scroll Hook
Create a `useInfiniteScroll` hook that:
- Detects when the user scrolls near the bottom
- Calls a provided fetch function with the next page number
- Handles loading and error states
- Supports both window scroll and container scroll

### Challenge 3: Compound Select Component
Build a Select component using the compound component pattern:
```jsx
<Select value={value} onChange={setValue}>
  <Select.Trigger placeholder="Choose..." />
  <Select.Options>
    <Select.Option value="a">Option A</Select.Option>
    <Select.Option value="b">Option B</Select.Option>
  </Select.Options>
</Select>
```
Must be keyboard accessible and handle focus correctly.

### Challenge 4: Optimistic Todo List
Build a todo list that:
- Shows changes immediately (optimistic updates)
- Reverts on API failure with an error message
- Handles concurrent updates correctly
- Uses proper TypeScript for all state

### Challenge 5: Accessible Data Grid
Build a data grid component that:
- Supports keyboard navigation (arrow keys between cells)
- Has proper ARIA roles for grid, row, and cell
- Supports cell editing on Enter/click
- Announces changes to screen readers

### Challenge 6: State Machine Component
Build a multi-step process (like a checkout flow) using a state machine pattern with useReducer. States should be explicit (e.g., 'idle', 'loading', 'error', 'success'), and impossible state transitions should be prevented by TypeScript.

---

## What's Next

Module 5 will cover backend development with Node.js, where you'll build APIs that your React applications can consume. You'll connect frontend and backend skills to build full-stack applications.
