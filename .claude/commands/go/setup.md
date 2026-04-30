# Setup Command

Initialize or configure the project environment for development.

## Usage

```
/go/setup [target]
```

## What This Does

This command helps you get the project up and running by:

1. Checking prerequisites (Node.js version, package manager, etc.)
2. Installing dependencies if needed
3. Setting up environment variables from `.env.example`
4. Initializing any required config files
5. Validating the setup is complete

## Steps

### 1. Check Prerequisites

Verify the environment meets requirements:
- Node.js >= 18.0.0
- npm or pnpm installed
- Git configured

Run: `node --version && npm --version`

### 2. Install Dependencies

If `node_modules` is missing or outdated:

```bash
npm install
# or
pnpm install
```

### 3. Environment Setup

If `.env` doesn't exist but `.env.example` does:

```bash
cp .env.example .env
```

Then prompt the user to fill in required values:
- `ANTHROPIC_API_KEY` — required for AI features
- Any other keys listed in `.env.example`

### 4. Initialize Task Master

If `tasks/` directory doesn't exist:

```bash
npx task-master init
```

### 5. Validate

Run a quick smoke test to confirm everything works:

```bash
npm run lint --if-present
npx task-master list 2>/dev/null || echo "No tasks yet — run task-master init"
```

## Troubleshooting

- **Missing API key**: Add `ANTHROPIC_API_KEY` to your `.env` file
- **Node version mismatch**: Use `nvm use` or install the correct version
- **Permission errors**: Try `npm install --legacy-peer-deps`
- **tasks/ missing**: Run `npx task-master init` to bootstrap the project

## Notes

This command is safe to re-run. It checks before overwriting any existing files.
