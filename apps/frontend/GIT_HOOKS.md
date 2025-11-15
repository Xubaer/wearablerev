# Git Hooks Setup

This project uses [Husky](https://typicode.github.io/husky/) for Git hooks, [lint-staged](https://github.com/okonet/lint-staged) for pre-commit linting/formatting, and [commitlint](https://commitlint.js.org/) for enforcing conventional commit messages.

## What Happens Automatically

### Before Each Commit (pre-commit hook)

The `pre-commit` hook runs automatically and will:
- Run ESLint with auto-fix on staged `.js`, `.jsx`, `.ts`, `.tsx`, and `.mjs` files
- Format staged JavaScript/TypeScript files with Prettier
- Format staged `.json`, `.css`, and `.md` files with Prettier

This ensures all committed code is properly formatted and follows the project's linting rules.

### On Commit Message (commit-msg hook)

The `commit-msg` hook validates your commit message against the [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Commit Message Format

Your commit messages must follow this format:

```
<type>(<scope>): <subject>
```

### Valid Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that don't affect the meaning of the code (white-space, formatting, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit

### Examples

✅ Valid commit messages:
```
feat: add user authentication
fix: resolve navigation bug on mobile
docs: update README with setup instructions
style: format code with prettier
refactor: simplify user service logic
perf: optimize image loading
test: add unit tests for user service
chore: update dependencies
```

❌ Invalid commit messages:
```
Added new feature          # Missing type
FIX: bug fix              # Type must be lowercase
update docs               # Missing type prefix
feat add feature          # Missing colon
```

## Configuration Files

- **`.husky/`** - Contains Git hook scripts (in repository root)
- **`apps/frontend/commitlint.config.js`** - Commitlint configuration
- **`apps/frontend/package.json`** - Contains `lint-staged` configuration

## Manual Commands

If you need to run these checks manually:

```bash
# Format all files
pnpm format

# Check formatting without changing files
pnpm format:check

# Run linter
pnpm lint

# Run lint-staged on staged files
pnpm lint-staged

# Test a commit message
echo "feat: test message" | pnpm commitlint
```

## Bypassing Hooks (Not Recommended)

In rare cases, you can bypass hooks with:

```bash
git commit --no-verify -m "your message"
```

**Note**: This is not recommended as it bypasses code quality checks.

## Troubleshooting

### Commit is rejected due to formatting

If your commit is rejected:
1. The hook will auto-fix most issues
2. Review the changes: `git diff`
3. Stage the fixes: `git add .`
4. Try committing again

### Commit message is rejected

If your commit message is rejected:
1. Read the error message to understand what's wrong
2. Use the correct format with a valid type
3. Try again with: `git commit --amend`

### Hooks not running

If hooks aren't running:
1. Ensure you're in a Git repository
2. Run `pnpm install` to reinstall hooks
3. Check that `.husky/` directory exists in the repository root
4. Verify hooks are executable: `ls -la .husky/`
