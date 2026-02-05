# How to Use AI as a Learning Tool (Not a Crutch)

AI coding assistants like Claude, ChatGPT, Copilot, and Cursor can either accelerate your learning or completely sabotage it. This guide teaches you how to use them effectively.

---

## The Problem

AI can write code for you. This feels helpful but is actually harmful to learning.

When AI writes your code:
- You don't build the mental pathways
- You can't debug what you don't understand
- You become dependent, not capable
- You'll fail technical interviews

When you struggle and AI guides you:
- You build real understanding
- You develop debugging skills
- You become independent
- You'll pass technical interviews

---

## The Rule

> **Use AI to understand, not to solve.**

Ask AI to explain concepts, not to write your code.

---

## Good vs Bad AI Usage

### ❌ Bad (Sabotages Learning)

```
You: "Write a function that filters an array to only include even numbers"
AI: [writes the complete function]
You: [copy-pastes, moves on]
```

**Result:** You learned nothing. You'll be stuck again on the next filter problem.

### ✅ Good (Accelerates Learning)

```
You: "I'm trying to filter an array but my code returns undefined. Here's what I tried: [code]. What am I misunderstanding about filter?"
AI: "Filter returns a new array, it doesn't modify the original. Also, the callback needs to return true/false. What do you think your callback is currently returning?"
You: [thinks, fixes it yourself]
```

**Result:** You now understand filter deeply. Next time will be easier.

---

## How to Ask AI Questions

### Before Asking

1. **Try for 15-30 minutes first** — Don't ask immediately
2. **Identify specifically what's confusing** — Not "it doesn't work" but "I don't understand why X happens"
3. **Have your attempt ready** — Show what you tried

### When Asking

Use this template:

```
I'm working on [specific problem].

I expect [what you think should happen].

Actually [what's happening instead].

Here's what I tried: [your code/approach].

I think the issue might be [your hypothesis].

Can you help me understand what I'm missing?
```

### After Getting Help

1. **Don't copy-paste** — Understand first, then type it yourself
2. **Explain it back** — Can you teach the concept to someone else?
3. **Try a similar problem** — Apply what you learned immediately

---

## Types of Questions (And How AI Should Help)

### Concept Questions ✅ Ask Freely

"What's the difference between let and const?"
"Why do we need async/await?"
"How does the event loop work?"

AI explaining concepts = great for learning

### Syntax Questions ✅ Ask Freely

"What's the syntax for destructuring an object?"
"How do I write an arrow function?"

AI showing syntax examples = fine

### Implementation Questions ⚠️ Ask Carefully

"How would I implement a filter function?"

**Bad:** AI writes the whole thing
**Good:** AI asks what you've tried, gives hints, lets you discover

### "Do My Work" Questions ❌ Don't Ask

"Write a todo app for me"
"Fix my code" (without showing what you tried)
"Complete this function"

This defeats the purpose of learning

---

## Setting Up AI Tools for Learning Mode

### Claude Code

This repository includes a `CLAUDE.md` file that automatically puts Claude in teaching mode. Claude will:
- Ask what you've tried before helping
- Give hints instead of solutions
- Encourage you to solve it yourself

### Cursor

This repository includes a `.cursorrules` file. Cursor will:
- Avoid autocompleting your exercise solutions
- Explain concepts instead of writing code
- Act as a teaching assistant

### GitHub Copilot

This repository includes `.github/copilot-instructions.md`. Copilot will:
- Reduce autocomplete suggestions for learning exercises
- Encourage you to write code yourself

### ChatGPT / Other AI

Copy and paste this at the start of your conversation:

```
I'm learning to code. Please act as a teaching assistant, not a code writer.

Rules:
1. Don't write complete code solutions for me
2. Ask what I've tried before helping
3. Give hints and explanations, not answers
4. Use Socratic questioning to guide me
5. Let me struggle — that's how I learn

If I ask you to write code, remind me of these rules and help me understand the concept instead.
```

---

## Recognizing When You're Cheating Yourself

Warning signs:

- You copy-pasted AI code without understanding it
- You can't explain what your code does
- You feel relief instead of accomplishment when AI solves it
- You're asking AI before trying yourself
- You couldn't recreate the solution without AI

If you notice these, reset:
1. Delete the AI-provided code
2. Try again yourself
3. Only ask for conceptual help

---

## The Struggle is the Point

When you're frustrated and stuck, remember:

- Professional developers feel this way every day
- The frustration means your brain is growing
- Each struggle you overcome makes you stronger
- AI can't take technical interviews for you

The goal isn't to complete the curriculum. The goal is to **become a developer**.

A developer who can only code with AI assistance isn't really a developer.

---

## When AI IS Helpful

AI is great for:

1. **Explaining concepts** — "Explain closures like I'm 5"
2. **Comparing approaches** — "What's the difference between X and Y?"
3. **Understanding errors** — "What does this error message mean?"
4. **Code review** — "Here's my working solution. How could I improve it?"
5. **Learning alternatives** — "I solved it this way. Are there other approaches?"

Use AI to deepen understanding, not to skip understanding.

---

## Summary

| Situation | Good AI Usage | Bad AI Usage |
|-----------|--------------|--------------|
| Stuck on a problem | "Can you give me a hint about X?" | "Can you solve this for me?" |
| Don't understand concept | "Can you explain X?" | "Just show me the code" |
| Code doesn't work | "What should I investigate?" | "Fix my code" |
| Finished a problem | "How else could I solve this?" | — |
| Starting a problem | Try yourself first | "Write this for me" |

---

## Remember

> AI is a bicycle for the mind, not a wheelchair.

Use it to go further and faster — not to avoid the journey entirely.
