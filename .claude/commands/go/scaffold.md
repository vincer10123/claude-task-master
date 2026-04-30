# Scaffold Command

Generate boilerplate code for new modules, components, or features in the project.

## Usage

```
/go/scaffold <type> <name> [options]
```

## Arguments

- `type` — The type of scaffold to generate (e.g., `module`, `command`, `provider`, `tool`)
- `name` — The name of the new entity to scaffold
- `options` — Optional flags to customize the scaffold

## What This Does

1. Identifies the scaffold type and target directory
2. Reads existing similar files to match conventions
3. Generates boilerplate with proper imports, exports, and structure
4. Creates associated test file if applicable
5. Updates any index or registry files that need to reference the new entity
6. Adds a task to task-master if a relevant task doesn't exist

## Scaffold Types

### `module`
Creates a new core module with:
- Main implementation file
- Corresponding test file
- JSDoc comments matching project style
- Proper exports

### `command`
Creates a new CLI command with:
- Command definition file
- Handler function
- Argument/option parsing
- Help text

### `provider`
Creates a new AI provider integration with:
- Provider class skeleton
- Required interface methods
- Config schema

### `tool`
Creates a new tool definition with:
- Tool schema
- Handler implementation
- Input validation

## Steps

1. Ask for clarification if `type` or `name` is ambiguous
2. Look at 2-3 existing files of the same type to understand conventions
3. Generate the scaffold matching those conventions exactly
4. Show a summary of files created/modified
5. Suggest next steps (e.g., implement TODOs, run tests)

## Notes

- Always match the existing code style — don't introduce new patterns
- Use the same import style (ESM vs CJS) as the rest of the project
- Check if a similar entity already exists before scaffolding
- If unsure about placement, ask before creating files
