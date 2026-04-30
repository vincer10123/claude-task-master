# Optimize

Analyze and optimize code performance, bundle size, and resource usage.

## Usage
```
/go/optimize [target]
```

## Arguments
- `target` (optional): Specific file, directory, or area to optimize (e.g., `src/`, `bundle`, `db`, `api`)

## What This Does

1. **Identifies optimization targets** based on the provided scope or runs a full project scan
2. **Analyzes performance bottlenecks** — slow functions, redundant computations, unnecessary re-renders
3. **Reviews bundle size** — unused imports, large dependencies, tree-shaking opportunities
4. **Checks database queries** — N+1 problems, missing indexes, inefficient joins
5. **Reviews async patterns** — unparallelized awaits, missing caching, redundant fetches
6. **Applies safe optimizations** with explanations for each change
7. **Reports improvements** with before/after metrics where measurable

## Process

```
Think through the optimization systematically:

1. Run `npm run build 2>&1 | tail -50` to check current bundle output
2. Check for obvious performance issues in the target scope
3. Look for:
   - Sequential awaits that could be Promise.all()
   - Repeated computations that could be memoized or cached
   - Large imports where only small parts are used
   - Missing early returns / unnecessary work
   - Synchronous operations that block the event loop
4. Apply changes incrementally, verifying tests still pass
5. Document what was changed and why
```

## Examples

```bash
# Optimize everything
/go/optimize

# Focus on API layer
/go/optimize api

# Focus on bundle size
/go/optimize bundle

# Focus on a specific file
/go/optimize src/core/task-manager.js
```

## Notes
- Always run tests after optimization to ensure correctness
- Prefer readability over micro-optimizations unless there's a measurable bottleneck
- Document non-obvious optimizations with comments explaining the trade-off
- If optimizations are risky or speculative, list them as recommendations rather than applying automatically
