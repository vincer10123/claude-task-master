# Release Command

Automate the release process using changesets.

## Usage

```
/go/release [patch|minor|major]
```

## What This Does

1. Verifies the working tree is clean
2. Runs the full test suite
3. Runs linting checks
4. Creates or validates changeset entries
5. Bumps version via changesets
6. Updates CHANGELOG.md
7. Commits the version bump
8. Creates a git tag
9. Pushes to remote with tags
10. Optionally publishes to npm

## Steps

### Pre-flight Checks

```bash
# Ensure clean working tree
git status --porcelain

# Run tests
npm test

# Run lint
npm run lint
```

If any pre-flight check fails, **stop and report the error**. Do not proceed with the release.

### Changeset Validation

Check if there are pending changesets:

```bash
ls .changeset/*.md | grep -v README.md
```

If no changesets exist and a bump type was provided as argument, create one:

```bash
npx changeset add
```

Otherwise, remind the user to create a changeset first with `/dedupe` or manually.

### Version Bump

```bash
npx changeset version
```

This will:
- Consume all pending `.changeset/*.md` files
- Update `package.json` version
- Update `CHANGELOG.md`

### Commit & Tag

```bash
# Stage all version-related changes
git add package.json CHANGELOG.md .changeset/

# Get new version for commit message
NEW_VERSION=$(node -p "require('./package.json').version")

# Commit
git commit -m "chore: release v$NEW_VERSION"

# Tag
git tag -a "v$NEW_VERSION" -m "Release v$NEW_VERSION"
```

### Push

```bash
git push origin main --follow-tags
```

### Publish to npm (optional)

Only run if the user confirms or passes `--publish` flag:

```bash
npm publish
```

## Notes

- Always verify the CHANGELOG entry looks correct before pushing
- For pre-releases, use `npx changeset pre enter <tag>` beforehand
- If pushing fails due to branch protection, open a PR instead
- Check `.changeset/config.json` for configured publish settings
