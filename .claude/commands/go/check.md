# Check

Run all quality checks on the codebase — tests, linting, type checking, and build validation.

## Usage

```
/go/check [scope]
```

## Arguments

- `scope` (optional): Limit checks to a specific area (`tests`, `lint`, `types`, `build`)

## Steps

1. **Determine scope**
   - If `$ARGUMENTS` is provided, run only that check
   - Otherwise run all checks in sequence

2. **Run tests**
   - Execute `npm test` or `npm run test`
   - Capture output and note any failures
   - Report pass/fail counts

3. **Run linter**
   - Execute `npm run lint` if available
   - Report any lint errors or warnings
   - Note files with issues

4. **Type checking** (if applicable)
   - Execute `npm run typecheck` or `tsc --noEmit` if tsconfig.json exists
   - Report any type errors

5. **Build validation**
   - Execute `npm run build` if a build script exists
   - Confirm build completes without errors

6. **Summarize results**
   - Provide a clear pass/fail summary for each check
   - If any checks failed, list the specific issues
   - Suggest fixes for common problems

## Notes

- Stop after first failing check unless `--all` is passed
- Use existing npm scripts from package.json rather than running tools directly
- If a check script doesn't exist, skip it and note it's not configured
