# Fix Command

Automatically diagnose and fix issues in the codebase based on failing tests, error logs, or explicit problem descriptions.

## Usage

```
/go/fix [issue description or error message]
```

## What This Does

1. **Diagnose** — Identify the root cause of the issue
2. **Plan** — Outline the minimal changes needed to fix it
3. **Implement** — Apply the fix with clean, consistent code
4. **Verify** — Run relevant tests to confirm the fix works
5. **Summarize** — Explain what was wrong and what changed

## Instructions

You are fixing a bug or resolving an issue in the claude-task-master project.

### Step 1: Understand the Problem

If an error message or description was provided, analyze it carefully:
- Identify the file(s) and line(s) involved
- Determine if it's a logic error, type error, missing dependency, or configuration issue
- Check if related tests exist that can help confirm the fix

If no description was provided:
- Check for any recent test failures with `npm test 2>&1 | tail -50`
- Look for TODO/FIXME comments that indicate known issues
- Review recent git changes that might have introduced regressions

### Step 2: Investigate Before Changing

Before writing any code:
- Read the relevant source files completely
- Understand the intended behavior vs actual behavior
- Check if there are existing tests covering this area
- Look for similar patterns elsewhere in the codebase to maintain consistency

### Step 3: Apply the Fix

- Make the **minimal change** necessary — avoid refactoring unrelated code
- Follow existing code style and conventions in the file
- Add a comment if the fix is non-obvious
- If the bug could affect other areas, check and fix those too

### Step 4: Verify

After applying the fix:
```bash
npm test
```

If tests don't exist for the fixed area, note that in your summary.

### Step 5: Summarize

Provide a brief summary:
- **Root cause**: What was wrong
- **Fix**: What changed and why
- **Files modified**: List of changed files
- **Tests**: Pass/fail status after fix

## Notes

- Prefer fixing the actual bug over suppressing errors or adding workarounds
- If the fix requires a breaking change, flag it clearly before proceeding
- If you're unsure about the intended behavior, ask before making changes
