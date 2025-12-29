# The Hitch-Hiker's Guide to Vibe Engineering

> **DON'T PANIC**

*In many of the more relaxed civilizations on the Outer Eastern Rim of the Galaxy, the Hitch-Hiker's Guide to Vibe Engineering has already supplanted the great Encyclopedia Galactica as the standard repository of all knowledge and wisdom, for though it has many omissions and contains much that is apocryphal, or at least wildly inaccurate, it scores over the older, more pedestrian work in two important respects.*

*First, it is slightly cheaper; and secondly it has the words* **DON'T PANIC** *inscribed in large friendly letters on its cover.*

---

## What Is Vibe Engineering?

In February 2025, [Andrej Karpathy coined the term](https://x.com/karpathy/status/1886192184808149383):

> "There's a new kind of coding I call 'vibe coding', where you fully give in to the vibes, embrace exponentials, and forget that the code even exists."

**VIBE ENGINEERING** *(n.)*: The deliberate practice of building software through AI collaboration—describing intent, reviewing output, and iterating toward working systems. Distinguished from "vibe coding" by the emphasis on *engineering*: understanding what you build, owning what you ship, and knowing the difference between a prototype and production.

The Guide's entry on Vibe Engineering begins:

> "Vibe Engineering is the second-best way to write software in the known universe. The best way, of course, is to have someone else do it entirely while you sip Pan Galactic Gargle Blasters. Since most developers cannot afford infinite monkeys or infinitely patient colleagues, Vibe Engineering represents a reasonable compromise."

*Note: We call it "engineering" deliberately. Whether that's accurate is addressed in [Chapter 0](chapters/00-the-great-debate.md).*

---

## The Complete Guide

### Part 0: Philosophy

| Chapter | Title | Summary |
|---------|-------|---------|
| 0 | [The Great Debate](chapters/00-the-great-debate.md) | Is this real engineering? Both sides examined |

### Part I: Fundamentals

| Chapter | Title | Summary |
|---------|-------|---------|
| 1 | [DON'T PANIC](chapters/01-dont-panic.md) | Getting started without losing your mind |
| 2 | [The Towel Principle](chapters/02-towel-principle.md) | Version control as your essential survival tool |
| 3 | [42](chapters/03-forty-two.md) | Dealing with ambiguity and asking the right questions |
| 4 | [The Babel Fish Problem](chapters/04-babel-fish.md) | Communication with AI and its failure modes |

### Part II: Applied Wisdom

| Chapter | Title | Summary |
|---------|-------|---------|
| 5 | [Mostly Harmless](chapters/05-mostly-harmless.md) | Risk assessment and when to vibe freely |
| 6 | [The Total Perspective Vortex](chapters/06-total-perspective-vortex.md) | Understanding AI's true limitations |
| 7 | [The Restaurant at the End of the Sprint](chapters/07-restaurant-end-of-sprint.md) | Planning, iteration, and shipping |
| 8 | [So Long, and Thanks for All the Code](chapters/08-so-long.md) | Knowing when to stop and ship |

### Part III: Surviving Success

| Chapter | Title | Summary |
|---------|-------|---------|
| 9 | [The Disaster Area](chapters/09-disaster-area.md) | When vibed MVPs meet production reality |

---

## Field Guide Entries

*Short, occasionally accurate entries on specific topics.*

| Entry | Risk Level | Description |
|-------|------------|-------------|
| [Prompts](entries/prompts.md) | 🟢 Mostly Harmless | The anatomy of effective prompts |
| [Context Windows](entries/context-windows.md) | 🟡 Caution Advised | Managing AI's limited memory |
| [Hallucinations](entries/hallucinations.md) | 🔴 DANGER | When AI makes things up |
| [Code Review](entries/code-review.md) | 🟢 Essential | Reviewing AI-generated code |
| [Accept All](entries/accept-all.md) | 🟡 Context-Dependent | When to accept without reading |
| [Testing](entries/testing.md) | 🟢 Essential | Verifying AI code works |
| [MVP Sanity Check](entries/mvp-sanity-check.md) | 🟠 Danger | The 4-question diagnostic for shipped MVPs |

---

## The Risk Classification System

This Guide uses a four-tier system inspired by the original Guide's planetary ratings:

- 🟢 **Mostly Harmless** - If it breaks, nothing bad happens
- 🟡 **Caution Advised** - Annoying but recoverable failures
- 🟠 **Danger** - Real problems occur if this fails
- 🔴 **Here Be Dragons** - Catastrophic consequences possible

Match your vibe level to your risk level.

---

## Honest Questions

Before you proceed, ask yourself:

1. **Can you debug it?** If the AI-generated code breaks, can you fix it?
2. **Can you explain it?** Could you walk someone through what the code does?
3. **Can you extend it?** When requirements change, can you modify it?
4. **Can you own it?** Are you willing to be responsible for this in production?

If you answered "no" to most of these, that's okay—for prototypes. For production, keep reading.

---

## Quick Reference

### Before Prompting
```
[ ] I know what I'm building
[ ] I know the constraints
[ ] I know what "done" looks like
```

### The Karpathy Spectrum
```
"Fully give in to the vibes" ←——————→ "Read every line"
        ↑                                      ↑
    Prototypes                            Production
```

### The Street Rules
1. **Context is currency** - Specific beats terrific
2. **Verify before trust** - The AI can't test itself
3. **Ship before perfect** - Done is better than ideal

---

## Inspirations & References

This Guide draws wisdom from:

- [Andrej Karpathy's "Vibe Coding" Tweet](https://x.com/karpathy/status/1886192184808149383) - The origin of the term
- [*Vibe Coding: Mistakes and Tradeoffs*](https://www.manning.com/books/vive-coding-mistakes-and-tradeoffs) (Manning) - Practical guidance on AI-assisted development
- Douglas Adams' *The Hitchhiker's Guide to the Galaxy* - The format and philosophy

---

## How to Use This Guide

1. **DON'T PANIC**
2. Start with [Chapter 0](chapters/00-the-great-debate.md) if you're skeptical, or [Chapter 1](chapters/01-dont-panic.md) if you're ready to build
3. Read the chapters in order (or don't—it's your life)
4. Reference the Field Guide entries as needed
5. Make mistakes
6. Learn from them
7. **DON'T PANIC**

---

## Contributing

This Guide is a living document, much like the original. Contributions are welcome from all sentient beings, and some non-sentient ones (we're looking at you, CI bots).

---

## A Note on Accuracy

*The Guide has, in various editions, suggested that:*
- *AI models understand what they're doing (they don't)*
- *Generated code is always correct (it isn't)*
- *You can skip testing (please don't)*

*The editors apologize for any confusion, destruction of production databases, or existential crises that may have resulted.*

---

**Share and Enjoy!**

*"Share and Enjoy" is the company motto of the Sirius Cybernetics Corporation, whose complaints division now covers most of the known universe. This is also good advice for Vibe Engineering—share your prompts, enjoy the process, and file bugs when things inevitably go wrong.*

---

*This Guide is dedicated to Douglas Adams, who taught us that the universe is not only queerer than we suppose, but queerer than we CAN suppose. The same is true of large language models.*

**— The Editors**
