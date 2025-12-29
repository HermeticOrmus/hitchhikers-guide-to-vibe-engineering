# Chapter 5: Mostly Harmless

> *"The Guide's entry on Earth was originally one word: 'Harmless.' After extensive research, Ford Prefect updated it to 'Mostly Harmless.' This was considered a major upgrade."*
>
> *The same rating system applies to AI-generated code.*

---

## The Karpathy Scale

In February 2025, Andrej Karpathy [coined the term "vibe coding"](https://x.com/karpathy/status/1886192184808149383):

> "There's a new kind of coding I call 'vibe coding', where you fully give in to the vibes, embrace exponentials, and forget that the code even exists."

He described a workflow where you:
- Talk to the AI with voice input
- "Accept All" without reading diffs
- Copy-paste error messages with no comment
- Build projects without really "coding"

This is liberating. This is powerful. This is also **context-dependent**.

Karpathy was building personal projects and prototypes. The stakes were low. The code was, in Guide terminology, *Mostly Harmless*.

But not all code is Mostly Harmless.

---

## The Risk Classification System

This Guide proposes a four-tier classification system for vibe coding risk:

### 🟢 MOSTLY HARMLESS

**Definition:** If it breaks, nothing bad happens.

**Examples:**
- Personal side projects
- Prototypes and proofs of concept
- Learning exercises
- Internal tools with no data access
- Scripts you'll run once

**Vibe Level:** Full Karpathy. Accept All. Embrace the vibes.

**Verification:** Run it, see if it works, move on.

### 🟡 CAUTION ADVISED

**Definition:** If it breaks, it's annoying but recoverable.

**Examples:**
- Team internal tools
- Development environments
- Non-critical automation
- Content that will be reviewed before publishing
- Code that affects only you

**Vibe Level:** Moderate vibing. Skim the diffs. Test the happy path.

**Verification:** Quick review, basic testing, have a rollback plan.

### 🟠 DANGER

**Definition:** If it breaks, real problems occur.

**Examples:**
- Production code
- Code handling user data
- Financial calculations
- Authentication/authorization
- Anything with compliance requirements
- Public APIs

**Vibe Level:** Low vibing. Read every line. Question everything.

**Verification:** Code review, comprehensive testing, security audit, staged rollout.

### 🔴 HERE BE DRAGONS

**Definition:** If it breaks, catastrophic consequences.

**Examples:**
- Medical systems
- Financial trading
- Security infrastructure
- Safety-critical systems
- Anything where failure means lawsuits, injuries, or deaths

**Vibe Level:** No vibing. AI assists research only. Humans write and verify all code.

**Verification:** Multiple independent reviews, formal verification where possible, extensive testing, regulatory compliance.

---

## The Tradeoff Matrix

As the Manning book *Vibe Coding: Mistakes and Tradeoffs* emphasizes, every vibe coding decision involves tradeoffs. Here's how to think about them:

| Factor | Full Vibe | Careful Vibe | No Vibe |
|--------|-----------|--------------|---------|
| Speed | 🚀🚀🚀 | 🚀🚀 | 🚀 |
| Risk | ⚠️⚠️⚠️ | ⚠️⚠️ | ⚠️ |
| Learning | 📉 | 📊 | 📈 |
| Quality | 🎲 | 🎯 | ✅ |
| Fun | 😎 | 🙂 | 😐 |

There's no universally correct position on this spectrum. The right choice depends on:

1. **What are you building?** (Stakes)
2. **Who will use it?** (Audience)
3. **How long will it live?** (Lifespan)
4. **Who will maintain it?** (Future developers)

---

## Context Is Currency

The Manning book's core insight applies here: **"Specific beats terrific. High-resolution context = high-precision code."**

When assessing risk, context is everything:

### The Same Code, Different Risk

```python
def calculate_total(items):
    return sum(item.price for item in items)
```

This function is:
- 🟢 **Mostly Harmless** in a shopping list app for personal use
- 🟡 **Caution Advised** in an e-commerce prototype
- 🟠 **Danger** in a production checkout system
- 🔴 **Dragons** in a financial trading platform

The code is identical. The context determines the risk.

### Check the Vibe

Before you vibe code anything, ask:

> "If this code is completely wrong, what's the worst that happens?"

- "I have to restart the script" → 🟢 Vibe away
- "I lose an hour of work" → 🟡 Maybe skim the diff
- "Users see an error" → 🟠 Read carefully
- "Users lose money" → 🔴 Manual mode

---

## The Mostly Harmless Checklist

Before going full vibe on any code:

### Environment Check
- [ ] Is this a personal/learning project?
- [ ] Is the data fake or backed up?
- [ ] Can I easily revert if something breaks?
- [ ] Am I the only person affected by bugs?

### Consequence Check
- [ ] If this breaks, will anyone lose data?
- [ ] If this breaks, will anyone lose money?
- [ ] If this breaks, will anyone be harmed?
- [ ] Could this create security vulnerabilities?

### Scale Check
- [ ] How many people will use this?
- [ ] How long will this code exist?
- [ ] Will someone else need to maintain this?

If you answered "yes" to any consequence question, or your scale is significant, **reduce your vibe level accordingly**.

---

## The Street Rules

Practical wisdom for risk-aware vibe coding:

### Street Rule #1: Prototype Wild, Production Careful

When exploring:
```
"Build me a quick prototype of a user dashboard with
charts showing activity over time. Don't worry about
error handling—just get something visual working."
```

When shipping:
```
"Review this dashboard code for production. Check for:
- Proper error handling for API failures
- Input validation on all user inputs
- Performance with 10,000 data points
- Accessibility compliance"
```

### Street Rule #2: Separate Generation from Integration

Generate code freely, but integrate carefully:

1. **Generate:** Let the AI create in a sandbox
2. **Review:** Read and understand what it created
3. **Test:** Verify it works in isolation
4. **Integrate:** Carefully merge into your codebase
5. **Verify:** Test the integration

### Street Rule #3: Trust But Verify, Proportionally

```
Risk Level    | Verification Effort
--------------+--------------------
🟢 Mostly Harmless | Run it
🟡 Caution    | Test happy path
🟠 Danger     | Test edge cases
🔴 Dragons    | Prove correctness
```

### Street Rule #4: When in Doubt, Slow Down

The vibes will still be there tomorrow. If you're unsure about the risk level, treat it as one level higher than you think.

---

## Move to Make

After reading this chapter, do the following:

1. **Audit your current projects** - Classify each as Mostly Harmless, Caution, Danger, or Dragons

2. **Adjust your workflow** - Match your vibe level to the risk level of what you're building

3. **Create templates** - Write prompts for each risk level:
   - "Quick prototype, don't worry about edge cases"
   - "Production code, include error handling and validation"
   - "Security-critical, I'll review each line"

4. **Practice awareness** - Before each AI interaction, consciously identify the risk level

---

## The Philosophical Bit

The original *Hitchhiker's Guide* rated Earth as "Mostly Harmless" as a kind of cosmic dismissal—a planet of little significance in the grand scheme.

But "Mostly Harmless" is actually a profound compliment for code. It means:
- It probably won't hurt anyone
- Failures are recoverable
- Experimentation is safe
- You can move fast without fear

The goal of good engineering isn't to eliminate all risk. It's to **know what risks you're taking** and **match your process to those risks**.

Full vibe coding on a prototype? Excellent.
Full vibe coding on a medical device? Reckless.

The wisdom is knowing the difference.

---

## The Guide's Verdict

Earth: Mostly Harmless.

Your side project: Probably also Mostly Harmless.

Your production database migration: **Definitely not Mostly Harmless. Read the diffs.**

---

*Next: [The Total Perspective Vortex](06-total-perspective-vortex.md)*
