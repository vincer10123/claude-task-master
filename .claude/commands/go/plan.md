# Plan

Analyze the current state of the project and create a detailed implementation plan for the next set of tasks.

## Steps

1. **Review current tasks** — Run `task-master list` to see what's pending, in-progress, and done.

2. **Check project context** — Read relevant source files to understand the current architecture and any recent changes.

3. **Identify blockers** — Look for any tasks marked as blocked and understand why.

4. **Prioritize work** — Based on dependencies and complexity, determine the optimal order to tackle pending tasks.

5. **Break down complex tasks** — For any task that seems large or ambiguous, use `task-master expand --id=<id>` to create subtasks.

6. **Update task details** — If any tasks have outdated descriptions or missing context, update them with `task-master update-task --id=<id> --prompt="<context>"`.

7. **Summarize the plan** — Present a clear, ordered list of what should be worked on next and why, including:
   - Which tasks to tackle first
   - Estimated complexity for each
   - Any dependencies between tasks
   - Potential risks or unknowns to watch out for

## Notes

- Focus on unblocking the critical path
- Prefer smaller, shippable increments over large monolithic changes
- If there are no tasks yet, analyze the codebase and suggest what should be added to `tasks/tasks.json`
- Use `task-master complexity-report` if available to get an overview of task complexity
