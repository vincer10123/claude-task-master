# Debug Command

Investigate and fix a failing test, error, or unexpected behavior in the codebase.

## Usage

```
/go/debug [error message or description]
```

## What this does

1. **Understand the problem** — Read the error message, stack trace, or description carefully
2. **Reproduce the issue** — Run the failing test or command to confirm the error
3. **Investigate** — Trace through the code to find the root cause
4. **Fix** — Apply the minimal change needed to resolve the issue
5. **Verify** — Run tests to confirm the fix works and nothing is broken

## Steps

### 1. Gather context

- If a specific error was provided, search the codebase for relevant files
- Check recent git changes that might have introduced the bug: `git log --oneline -10`
- Look at the stack trace to identify which files/functions are involved

### 2. Reproduce

```bash
# Run the specific failing test
npm test -- --testPathPattern="<relevant test file>"

# Or run all tests to see what's failing
npm test
```

### 3. Investigate

- Read the relevant source files carefully
- Add temporary debug logging if needed to trace execution
- Check for common issues:
  - Async/await mistakes
  - Missing null/undefined checks
  - Off-by-one errors
  - Incorrect imports/exports
  - Race conditions
  - Wrong variable scope

### 4. Fix

- Make the minimal change to fix the root cause
- Avoid fixing symptoms — find the actual bug
- If the fix is complex, break it into logical steps

### 5. Verify

```bash
# Run the previously failing test
npm test -- --testPathPattern="<relevant test file>"

# Run full test suite to check for regressions
npm test
```

## Notes

- Prefer targeted fixes over broad refactors
- If the bug reveals a design problem, note it as a follow-up task rather than fixing everything at once
- Add a regression test if one doesn't exist for this case
- Use `task-master add-task` to track any follow-up work discovered during debugging
