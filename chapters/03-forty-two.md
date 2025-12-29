# Chapter 3: 42

> *"The answer to the Ultimate Question of Life, the Universe, and Everything was computed by Deep Thought over 7.5 million years. It was 42. The problem, of course, was that nobody knew what the question actually was."*

---

## The Problem with Questions

When you ask an AI to generate code, you are essentially asking the Ultimate Question of your codebase. And much like the ancient philosophers of a certain fictional Earth, you will often receive an answer that is:

1. Technically correct
2. Completely useless
3. Missing the point entirely

This is not the AI's fault. The AI did exactly what you asked. The problem is that you didn't know what to ask.

---

## Why "42" Happens

Consider this prompt:

```
Make this code better.
```

The AI will absolutely make your code "better." It might:
- Add 47 design patterns
- Refactor into microservices
- Introduce a state management library
- Convert everything to functional programming
- Add comprehensive error handling for errors that can't happen
- Optimize for a scale you'll never reach

All of these are "better" by some definition. None of them might be what you needed.

The AI gave you 42. A perfect answer to the wrong question.

---

## Asking the Right Question

The secret to avoiding 42 is **specificity**. Not just what you want, but:

### The Context

```
# Bad
"Add authentication"

# Good
"Add JWT authentication to this Express.js API.
We're using PostgreSQL for the database.
Users are already in a 'users' table with email and password_hash columns.
We need login and logout endpoints.
Tokens should expire after 24 hours."
```

### The Constraints

```
# Bad
"Make it faster"

# Good
"This function processes 10,000 records and takes 30 seconds.
We need it under 5 seconds.
We can't change the database schema.
We have 512MB of memory available.
The solution should be readable by junior developers."
```

### The Non-Goals

```
# Bad
"Refactor this"

# Good
"Refactor this for readability.
Don't change the public API.
Don't add new dependencies.
Don't optimize for performance—it's fast enough.
Don't add features—just clean up."
```

---

## The Specificity Spectrum

```
Vague                                              Specific
|--------------------------------------------------|
"Fix it"   "Fix the bug"   "Fix the null pointer"   "On line 47,
                            in the user service"     handle the case
                                                     where user.email
                                                     is undefined by
                                                     returning early
                                                     with a 400 error"
```

The further right you go, the more useful your answer will be.

But there's a trap: go too far right, and you might as well write the code yourself.

The sweet spot is giving enough context for the AI to understand the problem, while leaving room for it to contribute solutions you hadn't considered.

---

## When 42 Is Actually the Answer

Sometimes, after much deliberation, 42 really is the answer. In vibe coding terms, this means:

### "It depends"

Q: Should I use React or Vue?
A: 42. (It depends on your team, your requirements, your existing code.)

### "Good enough"

Q: Is this the best architecture?
A: 42. (It's good enough. Ship it. You can improve it later.)

### "Nobody knows"

Q: Will this scale to a million users?
A: 42. (Nobody knows until you try. Build it, measure it, fix it.)

The wisdom is knowing when 42 is a cop-out and when it's genuine insight.

---

## The Question Behind the Question

Often, when you ask the AI something and get 42, the real problem is that you haven't figured out what you actually need.

**You ask:** "What's the best database for this project?"

**You get:** A 2000-word comparison of PostgreSQL, MongoDB, MySQL, and seventeen other options.

**What you needed to ask yourself first:**
- What kind of data am I storing?
- What queries will I run most often?
- Do I need transactions?
- What does my team already know?
- What's already deployed in our infrastructure?

The AI can help you explore these questions, but it can't answer them for you. That requires understanding your own context—something the AI fundamentally cannot do.

---

## The Deep Thought Protocol

When you're stuck in a 42 loop, try this:

### Step 1: State the Problem
Write out, in plain English, what you're trying to accomplish. Not the technical solution—the actual problem.

```
"Users are complaining that the checkout process is too slow."
```

### Step 2: Define Success
What does "solved" look like? Be specific.

```
"Checkout completes in under 2 seconds, 95th percentile."
```

### Step 3: List Constraints
What can't you change? What resources do you have?

```
"Can't change the payment provider.
Can't add more servers.
Have 2 days to fix it."
```

### Step 4: Now Ask the AI
With this context, your question becomes:

```
"Our checkout process takes 8 seconds (95th percentile).
We need it under 2 seconds.
Here's the current code: [code]
We can't change the payment provider or add servers.
What are the top 3 optimizations we should try first?"
```

This question will not receive 42 as an answer.

---

## Embracing Uncertainty

Sometimes the best answer really is uncertain. The AI might say:

> "There are several approaches, each with trade-offs..."

This isn't a failure. This is honesty. The AI is telling you that:

1. Multiple solutions exist
2. None is obviously superior
3. You need to make a judgment call

Your job as a vibe coder is to:
1. Understand the trade-offs
2. Make a decision
3. Live with the consequences
4. Adjust if needed

The AI is a tool for exploration, not a oracle of certainty.

---

## The Ultimate Answer

After 7.5 million years of computation, here is the Ultimate Answer to Vibe Coding:

**Understand your problem before you ask for solutions.**

This sounds obvious. It is obvious. It is also routinely ignored.

The AI will happily generate thousands of lines of code to solve a problem you don't have, using technologies you don't need, at a scale you'll never reach.

The only defense against this is clarity of thought. Know what you want. Know why you want it. Know how you'll know when you have it.

Then, and only then, ask the AI.

You might still get 42. But at least you'll know why.

---

*Next: [The Babel Fish Problem](04-babel-fish.md)*
