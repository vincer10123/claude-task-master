# Deploy Command

Deploy the current branch or a specific environment.

## Usage

```
/go/deploy [environment]
```

## Arguments

- `environment` (optional): Target environment (`staging`, `production`). Defaults to `staging`.

## What This Does

1. **Pre-flight checks** — Verifies the working tree is clean and all tests pass before deploying
2. **Build validation** — Runs the build to ensure it compiles without errors
3. **Environment confirmation** — For production deploys, prompts for explicit confirmation
4. **Deploy** — Executes the appropriate deploy command for the target environment
5. **Post-deploy verification** — Checks that the deploy succeeded and the service is healthy

## Steps

### 1. Check working tree

Run `git status --porcelain` and abort if there are uncommitted changes.

### 2. Run tests

Execute `npm test` or the project's test command. If tests fail, abort and report which tests failed.

### 3. Build

Run `npm run build` (or equivalent). Abort on build errors.

### 4. Confirm production deploys

If deploying to `production`, display a warning and ask the user to type `yes` to confirm before proceeding.

### 5. Deploy

For `staging`: run `npm run deploy:staging`
For `production`: run `npm run deploy:production`

Capture stdout/stderr and display in real time.

### 6. Health check

After deploy completes, run `npm run healthcheck:[environment]` if it exists. Report pass/fail.

## Error Handling

- If any step fails, stop immediately and report the failure with full output
- Never deploy to production without explicit confirmation
- Always show the git commit SHA being deployed

## Example Output

```
✓ Working tree clean (commit: a1b2c3d)
✓ Tests passed (42 passed, 0 failed)
✓ Build succeeded
⚠ Deploying to PRODUCTION — type "yes" to confirm: yes
→ Deploying...
✓ Deploy succeeded
✓ Health check passed
```
