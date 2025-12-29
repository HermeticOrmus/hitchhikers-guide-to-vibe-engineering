# Hallucinations

**Risk Level:** 🔴 DANGER

---

## Guide Entry

**HALLUCINATION** *(n.)*: When an AI generates something that looks correct, sounds confident, and is completely made up. Named for its similarity to seeing things that aren't there, except in this case, the things are npm packages, API methods, and library functions.

---

## The Danger

Hallucinations are dangerous because they're **indistinguishable from real information** in the AI's output.

The AI doesn't signal uncertainty:
```python
# AI might generate:
from fastsort import QuickSort  # This library doesn't exist
result = QuickSort.parallel_sort(data)  # This API is invented
```

It looks legitimate. It compiles (sometimes). It just doesn't work.

---

## Common Hallucination Types

### Invented Libraries
```python
# Not real
from datahelper import CSVParser
from quickauth import JWTManager
from fastvalidate import EmailValidator
```

### Invented Methods
```python
# Real library, fake method
import pandas as pd
df.smart_merge(other_df)  # .smart_merge() doesn't exist
```

### Invented Parameters
```javascript
// Real function, fake parameter
fetch(url, {
  retryCount: 3,      // Not a real option
  cacheMode: 'smart'  // Also invented
})
```

### Invented APIs
```bash
# Real service, fake endpoint
curl https://api.github.com/repos/owner/repo/smart_analytics
```

### Confident Misinformation
```
"React 18's useAutoMemo hook automatically memoizes..."
```
(useAutoMemo doesn't exist)

---

## Detection Strategies

### The Suspicion Checklist

Be suspicious when:
- [ ] Library name you've never heard of
- [ ] API seems too convenient
- [ ] Feature solves exact problem perfectly
- [ ] No import errors but runtime fails
- [ ] Documentation search returns nothing

### Immediate Verification

```bash
# For npm packages
npm search <package-name>
npm info <package-name>

# For Python packages
pip search <package-name>  # deprecated, use web
pip show <package-name>

# For any library
# Just Google it. If it exists, you'll find it.
```

### Documentation Check

```python
# In Python REPL
import library
help(library.method_name)
dir(library)

# If it exists, help() works
# If not, you get AttributeError
```

### The Controlled Test

```python
# Test in isolation before integrating
from mysterious_library import mystery_function

# If this fails, the library is hallucinated
print(mystery_function("test"))
```

---

## Why Hallucinations Happen

The AI predicts what tokens should come next based on patterns. When you describe a problem:

1. AI recognizes the problem pattern
2. AI predicts solution tokens
3. Those tokens might describe a real library
4. Or they might describe a plausible-sounding library
5. AI can't tell the difference

The AI isn't lying. It's generating statistically plausible sequences. Sometimes plausible ≠ real.

---

## Defense in Depth

### Layer 1: Suspicion
Assume AI-suggested libraries/methods might not exist until verified.

### Layer 2: Verification
Check before using. Search, documentation, `pip show`.

### Layer 3: Isolation
Test new dependencies in isolation before integrating.

### Layer 4: Review
Code review catches hallucinations that got past you.

### Layer 5: CI/CD
Automated builds fail on missing dependencies.

---

## The Street Rule

> "If the AI suggests a library that perfectly solves your problem and you've never heard of it, verify before you `npm install`."

---

## Move to Make

1. Find a piece of AI-generated code from your history
2. List every external dependency/library/API call
3. Verify each one exists and works as described
4. Note any hallucinations you find

This builds the verification habit.
