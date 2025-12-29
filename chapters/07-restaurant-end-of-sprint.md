# Chapter 7: The Restaurant at the End of the Sprint

> *"The Restaurant at the End of the Universe is where you can enjoy a meal while watching the entire universe explode. It's a tourist destination for those who want to experience endings in a comfortable setting with good service."*
>
> *Sprint planning with AI assistance is similar, except the explosions happen to your estimates.*

---

## The Plan-Execute-Debug Loop

The Manning book *Vibe Coding: Mistakes and Tradeoffs* reveals a fundamental truth:

> "Split reasoning over the feature phase and writing code phase—like all good engineers are taught to do. The more time you spend on spec, the more predictable results from AI Agent can be expected."

This is the secret to surviving the sprint. Not vibing harder. Planning smarter.

---

## Why Planning Matters More with AI

Without AI:
```
Think → Write Code → Debug → Think → Write More → Debug More
```

With AI (bad approach):
```
Prompt → Accept All → Confusion → More Prompts → More Confusion → Despair
```

With AI (good approach):
```
Think → Spec → Prompt → Review → Adjust → Test → Ship
```

The AI accelerates execution. It does not accelerate understanding. If you don't understand what you're building, the AI will help you build the wrong thing faster.

---

## The Pre-Flight Checklist

Before you write a single prompt:

### 1. What Are You Building?

Not "a login system."

```
A login system that:
- Accepts email and password
- Validates against PostgreSQL users table
- Returns JWT tokens valid for 24 hours
- Handles rate limiting (5 attempts per IP per minute)
- Logs all attempts for security audit
- Does NOT handle registration (that's a separate ticket)
```

### 2. What Are the Constraints?

```
Constraints:
- Must work with existing User model (no schema changes)
- Must use our existing JWT library (jose)
- Must follow our REST conventions (see API_STANDARDS.md)
- Must be deployable behind our existing load balancer
- Must not introduce new dependencies without approval
```

### 3. What Does Done Look Like?

```
Definition of Done:
- [ ] Login endpoint accepts POST /auth/login
- [ ] Returns { token, expiresAt } on success
- [ ] Returns 401 with { error } on failure
- [ ] Rate limiting works (tested manually)
- [ ] All attempts logged to security_events table
- [ ] Unit tests pass
- [ ] Integration test with real database passes
- [ ] Code review approved
```

### 4. What's Out of Scope?

```
NOT in this ticket:
- Password reset
- Email verification
- OAuth integration
- Admin user management
```

---

## The Prompting Workflow

With your spec in hand, you can now prompt effectively:

### Phase 1: Structure

```
I'm implementing a login system with these requirements:
[paste your spec]

Before writing code, outline your approach:
1. What functions/classes will you create?
2. What's the flow from request to response?
3. What edge cases should we handle?
```

Review the approach before generating code. Course-correct here, not after 500 lines of wrong code.

### Phase 2: Skeleton

```
Good approach. Now create the skeleton:
- Function signatures with docstrings
- Type hints
- No implementation yet, just structure
```

This is your checkpoint. Does the skeleton match your mental model?

### Phase 3: Implementation

```
Implement the authenticate_user function.
Remember:
- Use our existing PasswordHasher.verify() method
- Return None for invalid credentials, User for valid
- Don't handle rate limiting here (that's middleware)
```

One piece at a time. Verify as you go.

### Phase 4: Integration

```
Now let's wire this into the Express router.
Show me the route handler that:
1. Extracts email/password from request body
2. Calls authenticate_user
3. Generates JWT on success
4. Returns appropriate responses
```

### Phase 5: Tests

```
Write tests for authenticate_user:
- Valid credentials return user
- Invalid password returns None
- Invalid email returns None
- Empty inputs return None
- SQL injection attempts are safe
```

---

## The Estimation Problem

"How long will this take?"

With AI, the honest answer is: **"I don't know, but I'll know soon."**

### Why AI Breaks Estimates

Traditional estimates assumed:
- Typing speed is a bottleneck
- You know how to solve the problem
- Time = complexity × experience factor

AI changes this:
- Typing is instant
- You might not know the solution (but AI might)
- Time = prompting iterations × review thoroughness

### The New Estimation Model

Instead of estimating time, estimate **iterations**:

| Task Complexity | Estimated Iterations |
|-----------------|---------------------|
| Trivial | 1-2 prompts |
| Simple | 3-5 prompts |
| Medium | 5-10 prompts |
| Complex | 10-20 prompts |
| Very Complex | 20+ prompts (consider breaking down) |

Each iteration is:
1. Prompt
2. Review
3. Test
4. Adjust

Some iterations take 2 minutes. Some take 30. Variability is high.

### The Spike First Pattern

For uncertain work:

```
Day 1: Spike
- Try the AI approach
- See how many iterations it takes
- Identify blockers
- Don't commit to shipping

Day 2+: Implement
- Now you know the shape of the work
- Estimate based on actual data
- Ship with confidence
```

---

## The Debugging Dinner

At the Restaurant at the End of the Universe, you can watch entropy win. In sprint debugging sessions, you experience something similar.

### AI Debugging Workflow

**Step 1: Reproduce**
```
I have this error:
[paste exact error message and stack trace]

This happens when:
[describe exact steps to reproduce]

Here's the relevant code:
[paste minimal reproduction case]
```

**Step 2: Diagnose**
```
Based on that error, what are the likely causes?
Rank them by probability.
```

**Step 3: Fix**
```
Let's try your first hypothesis.
Show me the minimal change to test if that's the issue.
```

**Step 4: Verify**
```
That fixed the immediate error. Now:
1. Are there other places this bug might exist?
2. Should we add a test to prevent regression?
3. Is there a deeper architectural issue here?
```

### The Context Tax

Remember the Manning insight: **"Context is Currency."**

Every debugging session starts with context establishment:
- What's the error?
- What's the code?
- What did you expect?
- What actually happened?

This context costs tokens and time. Minimize it by:
- Keeping good logs
- Writing clear error messages
- Maintaining documentation
- Using consistent patterns

---

## The Iteration Mindset

The Restaurant exists at the end of time, where all outcomes are visible. In development, you can't see the end—but you can iterate toward it.

### The Vibe Coding Iteration Pattern

```
v0.1: Make it work (vibe freely)
v0.2: Make it right (review carefully)
v0.3: Make it fast (if needed)
v1.0: Make it maintainable (always)
```

Don't try to achieve all of these in one prompt. Iterate.

### When to Stop Iterating

The AI will always have "improvements" to suggest. Stop when:

1. **It works** - Passes all tests
2. **It's readable** - You understand every line
3. **It's appropriate** - Matches the risk level (see Chapter 5)
4. **It's done** - Meets the Definition of Done

Not when it's perfect. Perfect is a trap. "Good enough to ship" is the goal.

---

## The End of Sprint Retrospective

At the end of each sprint using AI, ask:

### What Prompts Worked?
Save effective prompts for reuse. Build a library of patterns that work for your codebase.

### Where Did the AI Struggle?
Identify patterns where AI consistently fails. These are candidates for manual work or better context.

### What Should Have Been Planned Better?
The AI can't fix bad requirements. Where did vague specs cause wasted iterations?

### What Verification Caught Issues?
Celebrate the bugs you found before production. This is the system working.

---

## The Restaurant's Menu

At the end of the sprint, you have choices:

**The Sirloin of Safe Commits**
Ship what works. Leave experiments on branches.

**The Prototype Parfait**
Demo what you learned. Get feedback. Iterate next sprint.

**The Technical Debt Tasting Menu**
Acknowledge what you shipped fast but need to revisit.

**The Full Release Feast**
Everything works, tested, documented, and deployed.

Choose based on your timeline, risk tolerance, and customer needs—not on how much code the AI generated.

---

## The Check, Please

Sprint complete. Before you leave the restaurant:

```
[ ] All code reviewed (by human eyes)
[ ] All tests passing
[ ] All documentation updated
[ ] All debt documented
[ ] All stakeholders notified
[ ] All commits clean
[ ] All vibes good
```

Pay the check. Go home. Rest.

The universe will still be there tomorrow, waiting to explode again.

---

*Next: [So Long, and Thanks for All the Code](08-so-long.md)*
