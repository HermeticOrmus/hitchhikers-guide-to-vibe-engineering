# Context Windows

**Risk Level:** 🟡 Caution Advised

---

## Guide Entry

**CONTEXT WINDOW** *(n.)*: The amount of text an AI can "remember" at once. Like RAM, but for conversation. When you exceed it, early information falls off the edge into the void, taking your carefully specified requirements with it.

---

## The Problem

AI models have limited context windows:
- GPT-4: ~128k tokens
- Claude: ~200k tokens
- Others: Varies

Sounds like a lot until:
- Your codebase is 50 files
- Your conversation is 100 messages
- Your paste is 1000 lines

Then: **context overflow**.

---

## Symptoms of Context Problems

### The Forgotten Requirement
**Message 1:** "We're using TypeScript strict mode"
**Message 50:** *AI generates untyped JavaScript*

### The Style Drift
**Early:** Clean, consistent code matching your patterns
**Later:** Generic code that doesn't fit your codebase

### The Contradiction
**AI:** "As I mentioned earlier..."
**You:** You mentioned the opposite earlier.

### The Repetition Request
**AI:** "Could you remind me what framework you're using?"
**You:** I told you three times.

---

## Survival Strategies

### Start Fresh Often
Long conversations accumulate errors. New chat = clean slate.

```
Rule of thumb:
- Simple task: 1 conversation
- Medium task: 2-3 conversations
- Complex task: Multiple focused conversations
```

### Restate Key Constraints
Periodically remind the AI of critical requirements:

```
"Quick reminder before we continue:
- TypeScript strict mode
- No new dependencies
- Follow existing patterns"
```

### Use CLAUDE.md / System Context
Put project constants in a file the AI always sees:

```markdown
# Project Context
- Language: TypeScript 5.0
- Framework: Next.js 14
- Style: Functional components with hooks
- Testing: Jest + React Testing Library
```

### Chunk Large Requests
Instead of:
```
"Here's my entire codebase, refactor it"
```

Do:
```
"Here's file 1, refactor this"
"Here's file 2, refactor this using the same patterns"
"Here's file 3..."
```

### Summarize Before Continuing
After complex discussions:
```
"Let's summarize what we've decided:
1. Using approach X
2. With constraint Y
3. Excluding Z

Confirm this is correct before we continue."
```

---

## The Street Rule

> "The AI's memory is shorter than you think. Repeat important things."

---

## Move to Make

Check your last long conversation:
1. Find where the AI "forgot" something
2. Identify what context would have helped
3. Plan where to repeat key constraints next time
