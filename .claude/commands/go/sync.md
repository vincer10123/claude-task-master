# Sync Task Master State

Synchronize the local task state with the latest changes from the repository and ensure everything is up to date.

## What this does

1. Pulls latest changes from the remote repository
2. Re-reads the tasks.json file to refresh in-memory state
3. Checks for any drift between task statuses and actual code state
4. Reports any inconsistencies found

## Steps

1. Run `git fetch origin` and `git status` to understand current state
2. Check if there are uncommitted changes that might conflict
3. Read the current `tasks/tasks.json` to understand task state
4. Cross-reference task statuses with recent git commits
5. Identify tasks marked as `done` that may not have corresponding commits
6. Identify tasks marked as `in-progress` that may have been completed
7. Report findings and suggest corrections

## Usage

Run this command when:
- You've been away from the project and need to catch up
- After merging a PR to update task statuses
- When task state seems out of sync with actual progress
- Before starting a new work session

## Output

The command will provide:
- Summary of current git state
- List of tasks that may need status updates
- Suggested `task-master set-status` commands to run
- Any tasks referencing files that no longer exist

## Notes

- This command is read-only by default — it won't modify tasks automatically
- Use `--auto-fix` flag intent if you want Claude to apply suggested fixes
- Always review suggestions before applying them
