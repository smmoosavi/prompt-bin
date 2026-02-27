# Setup Husky, Prettier, and Lint-Staged Configuration

Configure code formatting and Git hooks with the following setup:

## 1. Install Dependencies

Add these dev dependencies:

```bash
pnpm add -D husky prettier lint-staged
```

If the project does not already use TypeScript, also install it and initialize config:

```bash
pnpm add -D typescript && pnpm exec tsc --init
```

Set `noEmit` to true in `tsconfig.json`. If your project has no TypeScript files, add a placeholder `src/index.ts`.

## 2. Prettier Configuration

Create `.prettierrc.yml`:

```yaml
trailingComma: 'all'
singleQuote: true
```

Create `.prettierignore`:

```
dist/
.cache/
coverage/
/tsdoc-metadata.json
```

## 3. Lint-Staged Configuration

Create `.lintstagedrc.yml`:

```yaml
'**/*.{js,jsx,ts,tsx,json,yml,css,scss,md}':
  - 'prettier --write'
```

## 4. Package.json Scripts

Add these scripts as the first items in the `scripts` section of `package.json`:

```json
{
  "scripts": {
    "prepare": "husky",
    "pre-commit": "tsc && lint-staged",
    "format": "prettier --write '**/*.{js,jsx,ts,tsx,json,yml,css,scss,md}'",
    "format:check": "prettier --check '**/*.{js,jsx,ts,tsx,json,yml,css,scss,md}'"
  }
}
```

## 5. Husky Pre-commit Hook

Create `.husky/pre-commit` file with this content:

```bash
pnpm run pre-commit
```

Make it executable: `chmod +x .husky/pre-commit`

## 6. Initialize Husky

Run: `pnpm prepare`

## 7. gitignore

make sure to add `node_modules/` to your `.gitignore` file to avoid committing these directories.

## 8. Commit message

Commit should be done by user, not by AI. but this is the suggested commit message:

```
set up husky, prettier, and lint-staged for code formatting
```

## Summary

This setup will:

- Run TypeScript type checking (`tsc`) before each commit
- Auto-format staged files with Prettier before committing
- Use single quotes and trailing commas as code style
- Format JS, TS, JSON, YAML, CSS, and Markdown files
