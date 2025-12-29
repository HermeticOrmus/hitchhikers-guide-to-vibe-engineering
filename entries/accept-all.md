# Accept All

**Risk Level:** 🟡 Caution Advised to 🔴 DANGER (context-dependent)

---

## Guide Entry

**ACCEPT ALL** *(v.)*: The practice of accepting AI-generated code without reading the diff. Coined by Andrej Karpathy as part of his "vibe coding" workflow: "I 'Accept All' always, I don't read the diffs anymore."

---

## The Karpathy Context

When Karpathy described Accept All, he was:
- Building personal projects
- Prototyping ideas
- Experimenting with LLM capabilities
- Working at low stakes

This context matters. Accept All at scale or in production is a different game entirely.

---

## When Accept All Works

### 🟢 Safe to Accept All

**Prototypes nobody will use:**
```
"Make the button blue"
[Accept All]
"Add a loading spinner"
[Accept All]
```
Stakes: Zero. Speed: Maximum. Vibes: Excellent.

**Learning exercises:**
```
"Show me how to use this library"
[Accept All]
[Run it, see what happens, learn]
```

**Throwaway experiments:**
```
"Let's try approach X"
[Accept All]
[Evaluate, probably delete]
```

### 🟡 Accept All with Caution

**Internal tools:**
Accept All, but test before deploying.

**Non-critical features:**
Accept All, but review before commit.

**Paired with good tests:**
Accept All, but run the test suite.

### 🔴 Never Accept All

**Production code:**
Always review diffs before shipping.

**Security-related code:**
Always review line by line.

**Financial calculations:**
Always verify logic manually.

**Anything with user data:**
Always check for vulnerabilities.

---

## The Accept All Spectrum

```
Full Accept All ←————————————————→ Full Review
     ↑                                    ↑
 Karpathy                            Production
 Prototyping                         Systems

 Fast, risky                      Slow, safe
```

Your position on this spectrum should match your stakes.

---

## Upgrading from Accept All

When you need to transition from prototype to production:

### Level 1: Glance All
Accept quickly, but glance at what changed.
```
[See diff] [Notice nothing crazy] [Accept]
```

### Level 2: Scan All
Read file names and rough changes.
```
[Which files changed?] [What's the gist?] [Accept]
```

### Level 3: Review Key
Accept most, review critical paths.
```
[Accept UI changes] [Review auth changes] [Accept tests]
```

### Level 4: Review All
Read every diff before accepting.
```
[Read] [Understand] [Verify] [Accept or Modify]
```

---

## The Accept All Safety Net

If you're going to Accept All, protect yourself:

### 1. Version Control
```bash
git commit -m "checkpoint before vibing"
```
So you can always go back.

### 2. Tests
```bash
npm test
```
So failures are caught automatically.

### 3. CI/CD
Automated checks catch what you miss.

### 4. Code Review
Someone else reviews before merge.

### 5. Staging Environment
Deploy to staging before production.

---

## The Anti-Pattern

```
"Accept All" + "Push to Main" + "No Tests" + "Production"
= Incident waiting to happen
```

Each safety net you remove increases risk exponentially.

---

## The Street Rule

> "Accept All is a tool, not a policy. Use it where appropriate, not everywhere."

---

## Move to Make

Define your personal Accept All policy:
1. Where can I Accept All safely?
2. Where must I always review?
3. What safety nets do I have in place?

Write it down. Follow it.
