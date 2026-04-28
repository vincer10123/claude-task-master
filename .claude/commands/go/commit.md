# Commit Changes

Create a well-structured git commit for the current staged or unstaged changes.

## Steps

1. **Check current status**
   ```
   git status
   git diff --staged
   git diff
   ```

2. **Review what's changed**
   - Look at modified, added, and deleted files
   - Understand the scope of changes
   - Group related changes if needed

3. **Stage appropriate files**
   - If nothing is staged, stage relevant files based on the task context
   - Use `git add <file>` for specific files or `git add -p` for partial staging
   - Avoid staging unrelated changes

4. **Craft the commit message**
   - Use conventional commit format: `type(scope): description`
   - Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `style`, `perf`
   - Keep subject line under 72 characters
   - Add body if the change needs explanation
   - Reference task IDs if applicable (e.g., `Closes #123`)

5. **Create the commit**
   ```
   git commit -m "<message>"
   ```

6. **Verify the commit**
   ```
   git log --oneline -5
   ```

## Commit Message Examples

- `feat(tasks): add dependency resolution for subtasks`
- `fix(cli): handle missing config file gracefully`
- `docs(readme): update installation instructions`
- `chore(deps): bump anthropic sdk to latest`
- `refactor(core): extract task parsing into separate module`

## Notes

- Never commit secrets, API keys, or sensitive data
- If changes span multiple concerns, suggest splitting into separate commits
- Check `.gitignore` before staging — don't commit build artifacts or `node_modules`
- If there are no changes to commit, report that clearly
