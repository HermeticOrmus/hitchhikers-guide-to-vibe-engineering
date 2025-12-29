# Chapter 2: The Towel Principle

> *"A developer who can navigate the treacherous waters of AI-generated code, survive hallucinated dependencies, endure the heat of production incidents, and still knows where their git history is, is clearly a developer to be reckoned with."*

---

## Your Towel Is Version Control

In the vast, cold emptiness of software development, you need something to cling to. Something reliable. Something that will be there when everything else fails.

That something is **version control**.

More specifically: `git`.

The AI will generate code with supreme confidence. It will refactor your functions without asking. It will "improve" your architecture in ways that break everything. It will do all of this while maintaining the cheerful disposition of someone who has never experienced consequences.

Your towel—your git repository—is what saves you.

---

## The Essential Commands

Every vibe coder must know these commands the way a hitchhiker knows where their towel is:

### The Safety Net

```bash
# Before you do ANYTHING with AI
git status
git stash
# or
git commit -m "WIP: checkpoint before AI experiment"
```

### The Escape Hatch

```bash
# When everything goes wrong
git diff                    # See what changed
git checkout .              # Undo all changes
git stash pop              # Get your stuff back
```

### The Time Machine

```bash
# When you need to go back further
git log --oneline -10       # See recent history
git checkout <commit>       # Visit the past
git revert <commit>         # Undo a specific change
```

### The Parallel Universe

```bash
# For risky experiments
git checkout -b experiment-with-ai
# ... let the AI do its thing ...
git checkout main           # Return to safety
git branch -D experiment-with-ai  # Destroy evidence
```

---

## The Three Laws of Towel-Keeping

### First Law: Commit Before Generating

Before you ask the AI to generate anything significant, commit your current state. This is not optional. This is survival.

```bash
git add -A
git commit -m "checkpoint: before AI refactoring"
```

Think of it as putting on your seatbelt before letting a very enthusiastic but occasionally confused robot drive your car.

### Second Law: Review Before Committing

The AI has generated code. Wonderful. Now read it. All of it.

```bash
git diff
```

Look for:
- Deleted code you actually needed
- New dependencies you didn't ask for
- "Improvements" to files you didn't mention
- Security vulnerabilities cheerfully introduced
- Comments that say things like `// TODO: implement this`

### Third Law: Small Commits, Clear Messages

When you do commit AI-generated code, make small, focused commits with clear messages:

```bash
# Good
git commit -m "Add user validation function (AI-assisted)"

# Bad
git commit -m "AI stuff"

# Worse
git commit -m "."

# You will regret this
git commit -m "it works i think"
```

Future you will need to understand what past you was thinking. Future you will also need to know which code was AI-generated so they know to review it more carefully.

---

## The Wet Towel Problem

Sometimes your towel gets wet. In git terms, this means:

- You forgot to commit before the AI went wild
- You committed broken code
- You pushed broken code
- You pushed broken code to main
- On a Friday
- Before a holiday

For each of these situations, there is a solution. They get progressively more embarrassing to execute:

### Level 1: Uncommitted Changes
```bash
git checkout .
```
Crisis averted. Nobody needs to know.

### Level 2: Committed but Not Pushed
```bash
git reset --soft HEAD~1    # Undo commit, keep changes
# or
git reset --hard HEAD~1    # Undo commit, discard changes
```
Still fixable. Still secret.

### Level 3: Pushed but Nobody Noticed
```bash
git revert HEAD
git push
```
A revert commit appears in history. You can claim you "caught it in code review."

### Level 4: Pushed and Everyone Noticed
```bash
# Step 1: Accept your fate
# Step 2: Fix it properly
# Step 3: Write a postmortem
# Step 4: Never speak of it again
```

### Level 5: It's in Production
```bash
# Consult your incident response procedures
# This guide cannot help you now
# DON'T PANIC
```

---

## Advanced Towel Techniques

### The Stash Stack

When you're exploring multiple AI approaches:

```bash
git stash push -m "AI approach 1: microservices"
# try another approach
git stash push -m "AI approach 2: monolith"
# try yet another
git stash push -m "AI approach 3: serverless"

# Compare them
git stash list
git stash show -p stash@{0}
git stash show -p stash@{1}
git stash show -p stash@{2}

# Pick the winner
git stash pop stash@{1}
git stash drop stash@{0}
git stash drop stash@{0}  # indices shift!
```

### The Bisect Investigation

When AI-generated code introduced a bug but you don't know which commit:

```bash
git bisect start
git bisect bad                 # Current state is broken
git bisect good <known-good>   # This commit worked
# Git will checkout commits for you to test
git bisect good  # or bad
# Repeat until found
git bisect reset
```

This is particularly useful when you've been vibing for a while and lost track of when things went wrong.

### The Blame Game

When you need to know who (or what) wrote a particular line:

```bash
git blame <file>
```

If the commit message says "AI-assisted" or was authored at 3 AM, treat that code with extra suspicion.

---

## A Towel Is Not Enough

Even the most reliable towel cannot protect you from everything. You also need:

1. **Tests** - The AI can generate these too, but verify them
2. **CI/CD** - Automated checks catch what you miss
3. **Code Review** - Human eyes on AI code
4. **Backups** - For when git itself isn't enough
5. **Documentation** - So you remember what the AI was supposed to do

---

## The Hoopy Frood Checklist

Before each vibe coding session, ask yourself:

- [ ] Do I know where my repository is?
- [ ] Is my working directory clean?
- [ ] Do I have a branch for experiments?
- [ ] Have I committed recently?
- [ ] Could I recover if everything went wrong?

If you can answer yes to all of these, you are a hoopy frood who really knows where their towel is.

---

*Next: [42: The Answer to Ambiguity](03-forty-two.md)*
