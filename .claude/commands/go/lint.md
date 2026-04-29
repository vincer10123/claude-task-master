# Lint & Fix Command

Run linting and automatically fix issues in the codebase.

## Usage

```
/go/lint [path]
```

## What This Does

1. **Run ESLint** on the target path (defaults to `src/`)
2. **Auto-fix** any fixable issues
3. **Report** remaining issues that need manual attention
4. **Format** code with Prettier if configured
5. **Summarize** what was fixed vs what needs manual review

## Steps

### 1. Check for lint config

Look for `.eslintrc*`, `eslint.config.*`, or `eslint` config in `package.json`.

If no config found, note it and skip ESLint.

### 2. Run ESLint with auto-fix

```bash
npx eslint $ARGUMENTS --fix --format=stylish
```

If no path argument provided, default to `src/`.

### 3. Check for Prettier

Look for `.prettierrc*` or `prettier` config in `package.json`.

If found, run:
```bash
npx prettier --write $ARGUMENTS
```

### 4. Run ESLint again (no fix) to capture remaining issues

```bash
npx eslint $ARGUMENTS --format=stylish
```

Capture the output to report remaining issues.

### 5. Summarize results

Report:
- How many issues were auto-fixed
- How many issues remain and need manual attention
- List any files with remaining errors (not warnings)
- Suggest next steps if there are blocking errors

## Notes

- Warnings are informational — only errors should block progress
- If there are too many errors to fix manually, consider running `/go/fix` on specific files
- Type errors from TypeScript are separate — use `tsc --noEmit` for those
- Always commit before running lint fixes so changes are easy to review/revert
