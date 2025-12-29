# Code Review

**Risk Level:** 🟢 Essential (but Mostly Harmless to do)

---

## Guide Entry

**CODE REVIEW** *(n.)*: The practice of having human eyes examine code before it ships. With AI-generated code, this is not optional. The AI has no judgment. You provide the judgment. Review is where judgment happens.

---

## Why Review AI Code Differently

Traditional code review asks:
- Is this correct?
- Is this readable?
- Does this follow our patterns?

AI code review adds:
- **Did the AI understand the requirement?**
- **Is this real?** (hallucination check)
- **Is this what I asked for?** (scope creep check)
- **Is this secure?** (AI optimizes for function, not security)

---

## The AI Code Review Checklist

### Understanding Check
```
[ ] Does this solve the actual problem?
[ ] Does it handle the cases I need?
[ ] Does it avoid the cases I said to avoid?
```

### Reality Check
```
[ ] Do all imports exist?
[ ] Do all methods exist?
[ ] Are API calls to real endpoints?
[ ] Are dependencies in package.json/requirements.txt?
```

### Scope Check
```
[ ] Did it only change what I asked?
[ ] Are there surprise "improvements"?
[ ] Did it add features I didn't request?
[ ] Did it delete code I need?
```

### Security Check
```
[ ] No hardcoded secrets?
[ ] No SQL injection vulnerabilities?
[ ] No XSS vulnerabilities?
[ ] Input validation present?
[ ] Authentication checked where needed?
```

### Quality Check
```
[ ] Is this readable?
[ ] Will I understand this in a month?
[ ] Does it match our patterns?
[ ] Is it appropriately commented?
```

---

## Review Depth by Risk Level

### 🟢 Mostly Harmless
Quick scan:
- Does it work?
- Obviously broken?
- Ship it.

### 🟡 Caution Advised
Standard review:
- Run the checklist above
- Test the main path
- Verify key logic

### 🟠 Danger
Deep review:
- Line-by-line reading
- Run all checks
- Write tests first
- Get a second reviewer

### 🔴 Dragons
Formal review:
- Multiple independent reviewers
- Security audit
- Performance audit
- Compliance verification

---

## Common Issues in AI Code

### Over-Engineering
AI loves to add:
- Unnecessary abstractions
- Configurable everything
- Handling for cases that can't happen

**Fix:** Delete what you don't need.

### Under-Engineering
AI misses:
- Edge cases you mentioned
- Security concerns
- Performance implications

**Fix:** Add what's missing.

### Style Drift
AI ignores:
- Your naming conventions
- Your file organization
- Your preferred patterns

**Fix:** Refactor to match your style.

### Confidence Without Verification
AI never says:
- "I'm not sure about this"
- "You should test this carefully"
- "This might have issues"

**Fix:** Assume everything needs verification.

---

## Self-Review Technique

When reviewing your own AI-generated code:

### 1. Step Away
Don't review immediately. Let the vibes settle.

### 2. Explain It
Can you explain every line? If not, you don't understand it.

### 3. Test First
Write a test before reviewing the implementation.

### 4. Delete Test
Can you delete this code and still have a working system? If yes, maybe you should.

### 5. Future You
Will future you thank or curse present you for this code?

---

## The Street Rule

> "The AI writes code. You accept responsibility. Review is where responsibility is exercised."

---

## Move to Make

For your next AI-generated code:
1. Wait 10 minutes before integrating
2. Run through the full checklist
3. Note what you caught
4. Adjust your prompts to prevent those issues next time
