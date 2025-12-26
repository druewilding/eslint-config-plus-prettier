# eslint-config-plus-prettier

> Standard config for ESLint, Prettier and Package Lint. Also includes an optional TSConfig.

## Quick Setup

Install the package:

```bash
npm install --save-dev --save-exact eslint-config-plus-prettier
```

Add the following scripts to your `package.json`:

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "lint": "eslint --fix",
    "lint:check": "eslint",
    "package:lint": "npx npm-package-json-lint ."
  }
}
```

## Configuration

Add a `eslint.config.js` file with the following:

```javascript
import config from "eslint-config-plus-prettier";

export default [config];
```

To exclude specific folders or files from linting, add an `ignores` configuration:

```javascript
import config from "eslint-config-plus-prettier";

export default [
  config,
  {
    ignores: ["_site/**", "build/**", "*.min.js"],
  },
];
```

> **Note:** `dist/**` and `node_modules/**` are ignored by default.

### Prettier

Add prettier configuration to your `package.json`:

```json
{
  "prettier": "eslint-config-plus-prettier/prettier"
}
```

**Optional**: Create a `.prettierignore` file to exclude generated files:

```text
package-lock.json
CHANGELOG.md
dist
```

### Package Lint

Create a `.npmpackagejsonlintrc.json` file in your project root:

**For npm modules/libraries:**

```json
{
  "extends": "eslint-config-plus-prettier/packagelint"
}
```

**For applications/servers (with fixed dependencies):**

```json
{
  "extends": "eslint-config-plus-prettier/packagelint/server"
}
```

### TypeScript (Optional)

Create a `tsconfig.json` file for TypeScript projects:

```json
{
  "extends": "eslint-config-plus-prettier/tsconfig",
  "include": ["src/**/*"],
  "compilerOptions": {
    "outDir": "dist"
  }
}
```

## Usage

Run the following commands to lint and format your code:

```bash
# Lint and auto-fix JavaScript/TypeScript files
npm run lint

# Format all files with Prettier
npm run format

# Validate package.json structure
npm run package:lint

# Check formatting without making changes
npm run format:check

# Check linting without auto-fixing
npm run lint:check
```

## What's Included

### ESLint Rules

- **TypeScript support** with `@typescript-eslint` parser and plugin
- **Import sorting** with `simple-import-sort` plugin
- **Unused import removal** with `unused-imports` plugin
- **Consistent quotes** (double quotes)
- **Prefer const** for immutable variables
- **Unused variable warnings** (with underscore prefix exception)

### Prettier Configuration

- **Double quotes** for strings
- **Semicolons** enabled
- **Trailing commas** in ES5-compatible locations
- **120 character** line width
- **2 spaces** for indentation

### Package Lint Rules

- Validates `package.json` structure and dependencies
- Different rulesets for modules vs. applications
- Ensures consistent package metadata

## Troubleshooting

### ESLint Issues

- Make sure you're using ESLint v9+ for flat config support
- Check that your `eslint.config.js` is in the project root
- Verify all files you want to lint match the file patterns

### Prettier Conflicts

- This config uses `eslint-config-prettier` to disable conflicting ESLint rules
- If you see formatting conflicts, check your `.prettierignore` file

### Import Errors

- Ensure you're using ES modules (`"type": "module"` in package.json)
- For CommonJS projects, use `.cjs` extension for config files

## Contributing

Found an issue or have a suggestion? Please [open an issue](https://github.com/druewilding/eslint-config-plus-prettier/issues) or submit a pull request.
