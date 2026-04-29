# Generate or Update Documentation

Generate, update, or sync project documentation based on current code state.

## Steps

1. **Identify documentation scope**
   - Check `$ARGUMENTS` for specific target (e.g., `api`, `readme`, `changelog`, `all`)
   - Default to `all` if no argument provided

2. **Audit existing docs**
   - Scan `docs/`, `README.md`, `CHANGELOG.md`, and any `*.md` files in root
   - Identify stale sections, missing coverage, or broken links
   - Note any JSDoc/TSDoc comments in source files that need to be reflected

3. **Generate documentation based on target**

   ### If target is `readme` or `all`:
   - Review `package.json` for project name, description, scripts, and dependencies
   - Check recent git log for major changes: `git log --oneline -20`
   - Update `README.md` with accurate installation, usage, and configuration sections
   - Ensure CLI commands table is current with actual implemented commands

   ### If target is `api` or `all`:
   - Scan `src/` or main source directories for exported functions/classes
   - Check for existing JSDoc comments and fill gaps
   - Generate or update `docs/api.md` with function signatures and descriptions

   ### If target is `changelog` or `all`:
   - Run `git log --oneline` since last tag or last 30 commits
   - Group changes by type: Features, Bug Fixes, Breaking Changes
   - Append new section to `CHANGELOG.md` with today's date
   - Do NOT overwrite existing changelog entries

4. **Validate documentation**
   - Check all internal links resolve to real files/sections
   - Verify code examples in docs actually match current API
   - Confirm version numbers in docs match `package.json`

5. **Report changes**
   - List every file modified or created
   - Summarize what was added, updated, or removed
   - Flag anything that needs manual review (e.g., ambiguous API behavior)

## Notes

- Never delete documentation without explicit confirmation
- Preserve existing formatting style in each file
- If unsure about a function's behavior, note it as "needs verification" rather than guessing
- Keep examples minimal but realistic — no lorem ipsum or placeholder data
