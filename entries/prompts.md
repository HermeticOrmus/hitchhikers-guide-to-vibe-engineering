# Prompts

**Risk Level:** 🟢 Mostly Harmless

---

## Guide Entry

**PROMPT** *(n.)*: The text you give to an AI to tell it what you want. The quality of your prompt directly determines the quality of your output. Garbage in, garbage out—but fancy garbage.

---

## The Anatomy of a Prompt

```
[Context] + [Task] + [Constraints] + [Format] = Prompt
```

### Context
What the AI needs to know:
```
"I'm building a REST API in Python using FastAPI.
The codebase uses async/await patterns throughout."
```

### Task
What you want done:
```
"Create an endpoint that returns user profile data."
```

### Constraints
What limits apply:
```
"Don't add new dependencies.
Use our existing User model.
Follow RESTful conventions."
```

### Format
How you want the output:
```
"Show me just the route handler function.
Include type hints and a docstring."
```

---

## Prompt Patterns

### The Direct Ask
```
"Write a function that validates email addresses."
```
🟢 Simple, clear, effective for straightforward tasks.

### The Contextual Ask
```
"In this Django project using DRF, write a serializer
for the User model that includes email validation."
```
🟢 Better results when context matters.

### The Constrained Ask
```
"Write a sorting function that:
- Works in O(n log n) time
- Uses constant extra space
- Is stable
- Handles empty arrays"
```
🟢 Precise when you have specific requirements.

### The Example-Driven Ask
```
"Write a function in this style:

def existing_function(x: int) -> str:
    '''Brief description.'''
    return str(x)

New function should validate passwords."
```
🟢 Excellent for matching existing code patterns.

---

## Common Prompt Mistakes

### Too Vague
❌ "Fix this"
✅ "Fix the null pointer exception on line 47 when user.email is undefined"

### Too Broad
❌ "Build me an e-commerce site"
✅ "Create the product listing component that displays name, price, and image"

### Missing Context
❌ "Add authentication"
✅ "Add JWT authentication to this Express API using our existing User model"

### Assumed Knowledge
❌ "Use our standard pattern"
✅ "Use this pattern: [paste example]"

---

## The Street Rule

> "Specific beats terrific. High-resolution context = high-precision code."

The more specific your prompt, the less the AI has to guess. The less it guesses, the less it hallucinates.

---

## Move to Make

Write three versions of your next prompt:
1. How you'd naturally ask
2. With added context
3. With constraints and format

Compare the outputs. Learn what details matter for your use case.
