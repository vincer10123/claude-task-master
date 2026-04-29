# Migrate

Run database migrations or data transformation tasks for the project.

## Usage

```
/go/migrate [direction] [options]
```

## Arguments

- `direction` - Migration direction: `up` (default), `down`, or `status`
- `options` - Additional flags like `--dry-run`, `--steps N`, `--target VERSION`

## What This Does

1. **Check current migration state** - Determine which migrations have been applied
2. **Validate migration files** - Ensure migration scripts are syntactically valid
3. **Run migrations** - Apply pending migrations in order (or rollback if `down`)
4. **Verify integrity** - Confirm the schema/data is in a consistent state after migration
5. **Report results** - Show which migrations ran, skipped, or failed

## Steps

### 1. Detect migration setup

Look for migration configuration in:
- `package.json` scripts (e.g., `migrate`, `db:migrate`)
- Common migration tools: `knex`, `prisma`, `sequelize`, `typeorm`, `drizzle`
- Migration directories: `migrations/`, `db/migrations/`, `prisma/migrations/`
- Config files: `knexfile.js`, `prisma/schema.prisma`, `.sequelizerc`

### 2. Check migration status

Before running, always check what's pending:
```bash
# Examples depending on tool detected
npx knex migrate:status
npx prisma migrate status
npx sequelize-cli db:migrate:status
```

### 3. Run the migration

For `up` (default):
```bash
npx knex migrate:latest
npx prisma migrate deploy
npx sequelize-cli db:migrate
```

For `down` (rollback):
```bash
npx knex migrate:rollback
npx prisma migrate reset  # careful!
npx sequelize-cli db:migrate:undo
```

For `status` only — just report, don't run.

### 4. Handle dry-run mode

If `--dry-run` is passed, show what *would* run without executing. Some tools support this natively; otherwise simulate by listing pending migration files.

### 5. Post-migration checks

- Run any seed scripts if `--seed` flag is passed
- Verify the app can still connect and query the database
- If tests exist for DB layer, offer to run them

## Error Handling

- If a migration fails mid-way, report which step failed and the error
- Suggest rollback command if appropriate
- Never auto-rollback production — warn and let the user decide
- If no migration tool is detected, say so clearly and ask the user to specify

## Environment Awareness

- Check `NODE_ENV` or `.env` to understand which database is targeted
- Warn loudly if `NODE_ENV=production` before destructive operations
- Prefer `.env.local` or `.env.development` for local runs

## Example Output

```
📦 Detected migration tool: knex
🔍 Current status: 3 migrations applied, 2 pending

Pending migrations:
  - 20240301_add_user_roles.js
  - 20240315_add_task_metadata.js

▶ Running migrations...
  ✓ 20240301_add_user_roles.js
  ✓ 20240315_add_task_metadata.js

✅ All migrations applied successfully.
```
