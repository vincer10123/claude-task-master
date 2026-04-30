# Audit

Run a comprehensive security and dependency audit of the project.

## Usage

```
/go/audit [--fix] [--level <low|moderate|high|critical>]
```

## What this does

1. **Dependency audit** — Run `npm audit` to check for known vulnerabilities
2. **License check** — Scan dependencies for license compatibility issues
3. **Outdated packages** — List packages with available updates
4. **Dead code detection** — Check for unused exports/imports if tools are available
5. **Secret scanning** — Look for accidentally committed secrets or API keys
6. **Summary report** — Provide a prioritized list of findings with remediation steps

## Steps

### 1. Run npm audit

```bash
npm audit --json 2>/dev/null || npm audit
```

If `--fix` flag is passed, also run:
```bash
npm audit fix
```

### 2. Check for outdated dependencies

```bash
npm outdated
```

Group results by:
- **Patch updates** (safe to apply)
- **Minor updates** (review changelog)
- **Major updates** (breaking changes likely)

### 3. Scan for secrets

Search for common secret patterns in tracked files:
- API keys (e.g., `sk-`, `AKIA`, `ghp_`)
- Hardcoded passwords or tokens
- `.env` files accidentally committed

```bash
git ls-files | xargs grep -l -E '(password|secret|api_key|token)\s*=\s*["\x27][^"\x27]{8,}' 2>/dev/null
```

### 4. Check license compatibility

If `license-checker` is available:
```bash
npx license-checker --summary 2>/dev/null
```

Flag any GPL/AGPL licenses if the project is proprietary.

### 5. Report findings

Output a structured summary:

```
## Audit Report — <date>

### 🔴 Critical / High
- ...

### 🟡 Moderate
- ...

### 🟢 Low / Info
- ...

### 📦 Dependency Updates Available
- Patch: X packages
- Minor: Y packages  
- Major: Z packages

### ✅ No issues found in:
- Secret scanning
- License compatibility
```

## Notes

- Do not auto-apply major version bumps without explicit confirmation
- If vulnerabilities are in devDependencies only, note that they don't affect production
- Always check if a vulnerability has a fix available before reporting it as blocking
