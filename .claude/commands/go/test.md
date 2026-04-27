# Run Tests

Run the test suite for the current changes or specified scope.

## Usage

```
/go/test [scope] [options]
```

## Arguments

- `scope` (optional): Specific test file, directory, or pattern to run. Defaults to all tests.
- `options` (optional): Additional flags like `--watch`, `--coverage`, `--verbose`

## What This Does

1. **Identifies test scope** — Determines which tests to run based on:
   - Recently modified files (if no scope provided)
   - Explicitly provided scope argument
   - Full suite if `all` is passed

2. **Runs the tests** — Executes via the project's test runner (Jest, Vitest, etc.)

3. **Reports results** — Summarizes:
   - Pass/fail counts
   - Coverage if `--coverage` flag used
   - Any failing test details with file + line references

4. **Suggests fixes** — For failing tests, analyzes the failure and suggests likely causes or fixes

## Examples

```
/go/test
/go/test src/core/task-manager.js
/go/test --coverage
/go/test src/commands/ --verbose
```

## Notes

- If tests fail, do NOT auto-fix unless explicitly asked
- Always show the full error output for failing tests
- If coverage drops below threshold, flag it as a warning
- For watch mode, explain how to exit (Ctrl+C)
