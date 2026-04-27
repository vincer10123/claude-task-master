# Review Current Changes

Review the current branch's changes before submitting a PR. Performs a thorough code review including task alignment, code quality, and potential issues.

## Steps

1. **Get branch context**
   - Run `git log main..HEAD --oneline` to see commits on this branch
   - Run `git diff main...HEAD --stat` to see what files changed
   - Run `git diff main...HEAD` to see full diff

2. **Check task alignment**
   - Run `task-master list --status=in-progress` to see active tasks
   - Run `task-master list --status=done` to see recently completed tasks
   - Verify the changes align with the task descriptions

3. **Review code quality**
   For each changed file, evaluate:
   - Does the code follow existing patterns in the codebase?
   - Are there any obvious bugs or edge cases not handled?
   - Is error handling consistent with the rest of the project?
   - Are there any hardcoded values that should be configurable?
   - Are imports/dependencies appropriate and minimal?

4. **Check for common issues**
   - Look for `console.log` or debug statements left in
   - Check for TODO/FIXME comments that should be addressed
   - Verify no secrets or sensitive data are included
   - Check that new functions have appropriate JSDoc comments
   - Ensure test files are updated if applicable

5. **Summarize findings**
   Provide a structured review with:
   - **Summary**: What this PR does in 1-2 sentences
   - **Task Alignment**: Does it match the task requirements?
   - **Issues Found**: List any bugs, concerns, or improvements needed (severity: critical/major/minor)
   - **Suggestions**: Optional improvements that aren't blockers
   - **Verdict**: Ready to merge / Needs changes / Needs discussion

## Notes
- Be constructive and specific in feedback
- Distinguish between blocking issues and nice-to-haves
- If the diff is large, focus on the most critical paths first
