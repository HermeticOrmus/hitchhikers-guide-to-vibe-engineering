# Testing

**Risk Level:** 🟢 Essential

---

## Guide Entry

**TESTING** *(n.)*: The practice of verifying that code works. With AI-generated code, testing is your primary defense against confident wrongness. The AI will never tell you something is broken. Tests will.

---

## The Testing Paradox

AI can generate tests. But:
- AI-generated tests test AI-generated assumptions
- If both are wrong in the same way, you won't know

**Solution:** Generate tests, but verify they test what matters.

---

## Testing AI Code Workflow

### Step 1: Specify First

Before generating code:
```
"I need a function that:
- Takes a list of numbers
- Returns the average
- Returns 0 for empty lists
- Ignores non-numeric values"
```

### Step 2: Generate Tests First

```
"Write tests for that function before implementing it.
Use pytest.
Include edge cases."
```

### Step 3: Review Tests

**Do the tests match your specification?**
- Test for empty list?
- Test for non-numeric values?
- Test for normal case?

**Do the tests make sense?**
```python
# Good test
def test_average_ignores_strings():
    assert average([1, "two", 3]) == 2.0

# Suspicious test - why would this be expected?
def test_average_returns_none_for_empty():
    assert average([]) is None
# Wait, spec said return 0, not None...
```

### Step 4: Generate Implementation

```
"Now implement the function to pass these tests."
```

### Step 5: Run Tests

```bash
pytest
```

If tests fail, you learned something. Fix and repeat.

---

## What to Test

### The Happy Path
```python
def test_average_normal_case():
    assert average([1, 2, 3, 4, 5]) == 3.0
```

### Edge Cases
```python
def test_average_empty_list():
    assert average([]) == 0

def test_average_single_element():
    assert average([42]) == 42
```

### Error Cases
```python
def test_average_with_invalid_input():
    assert average([1, "two", 3]) == 2.0
```

### Boundaries
```python
def test_average_very_large_numbers():
    assert average([10**100, 10**100]) == 10**100
```

---

## Testing AI-Specific Concerns

### Hallucination Testing
```python
def test_uses_real_library():
    # If this import fails, AI hallucinated the library
    from actual_library import actual_function
```

### Scope Testing
```python
def test_function_only_does_what_asked():
    result = process_data(input_data)
    # Verify it didn't add extra fields
    assert set(result.keys()) == {"expected", "fields", "only"}
```

### Integration Testing
```python
def test_works_with_existing_code():
    # Test that AI code integrates with your codebase
    existing_result = existing_function()
    ai_result = ai_generated_function(existing_result)
    assert ai_result is not None
```

---

## AI Test Generation Prompts

### Good Prompt
```
"Generate pytest tests for this function.
Include:
- 3 happy path tests
- 3 edge case tests
- 2 error case tests

Follow this format:
def test_descriptive_name():
    '''What this tests.'''
    # Arrange
    input = ...
    # Act
    result = function(input)
    # Assert
    assert result == expected"
```

### Review the Output
AI might generate:
- Tests that always pass (useless)
- Tests that test implementation, not behavior
- Tests missing critical edge cases

You catch these by reading the tests.

---

## The Testing Safety Net

```
Level 0: No tests
         AI says it works, you hope it works
         🔴 Dangerous

Level 1: AI-generated tests, unreviewed
         Better than nothing
         🟡 Risky

Level 2: AI-generated tests, reviewed
         You verified they test the right things
         🟢 Good

Level 3: Spec-first tests, then implementation
         Tests define correctness, code follows
         🟢 Better

Level 4: Test + review + CI/CD
         Automated verification on every commit
         🟢 Best
```

---

## The Street Rule

> "The AI cannot test its own correctness. Tests are how you test the AI."

---

## Move to Make

For your next AI-generated function:
1. Write the spec
2. Generate tests from spec
3. Review tests manually
4. Generate implementation
5. Run tests
6. Note what the tests caught

Build the muscle memory of test-first AI development.
