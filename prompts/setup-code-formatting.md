# Setup Husky, Prettier, and Lint-Staged Configuration

Configure code formatting and Git hooks with the following setup:

## 1. Install Dependencies

Add these dev dependencies:

```bash
pnpm add -D husky prettier lint-staged
```

## 2. Prettier Configuration

Create `.prettierrc.yml`:

```yaml
trailingComma: "all"
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
"**/*.{js,jsx,ts,tsx,json,yml,css,scss,md}":
  - "prettier --write"
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

## Summary

This setup will:

- Run TypeScript type checking (`tsc`) before each commit
- Auto-format staged files with Prettier before committing
- Use single quotes and trailing commas as code style
- Format JS, TS, JSON, YAML, CSS, and Markdown files
