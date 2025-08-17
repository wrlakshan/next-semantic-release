# Next.js Semantic Release Project

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app) and configured with automated semantic versioning, code quality tools, and deployment workflows.

## 🚀 Getting Started

### Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

### Building the Project

```bash
npm run build    # Build for production
npm run start    # Start production server
```

## 🛠️ Development Workflow

### Code Quality & Linting

This project includes comprehensive code quality tools:

#### Manual Linting & Formatting

```bash
# Run ESLint to check for code issues
npm run lint

# Format all files with Prettier
npm run format

# Check specific files
npx eslint src/app/page.tsx
npx prettier --check src/app/page.tsx
```

#### Pre-commit Hooks (Automatic)

The project uses **Husky** and **lint-staged** to automatically format and lint your code before commits:

- ✅ **Prettier** formats code style (JS, TS, JSON, CSS, MD files)
- ✅ **ESLint** fixes code quality issues (JS, TS files)
- ✅ **Build verification** ensures the project compiles
- ✅ **Only staged files** are processed (efficient)

**What happens on `git commit`:**

1. Prettier formats your staged files
2. ESLint fixes auto-fixable issues in staged JS/TS files
3. Fixed files are re-added to staging
4. Project builds to ensure compilation success
5. Commit proceeds if all checks pass

### Manual Pre-commit Check

To manually run the same checks that happen on commit:

```bash
# Run lint-staged manually
npx lint-staged

# Or run individual tools
npm run lint
npm run format
npm run build
```

## 📝 Commit Process

This project uses **Conventional Commits** with **Commitizen** for consistent commit messages:

### Using Commitizen (Recommended)

```bash
# Stage your changes
git add .

# Use interactive commit tool
npm run commit
```

This will prompt you to:

1. Select commit type (feat, fix, docs, etc.)
2. Enter scope (optional)
3. Write short description
4. Write longer description (optional)
5. Note breaking changes (if any)

### Manual Conventional Commits

If you prefer manual commits, follow this format:

```bash
git commit -m "feat: add user authentication"
git commit -m "fix: resolve navigation bug"
git commit -m "docs: update API documentation"
```

#### Commit Types:

- **feat**: New features
- **fix**: Bug fixes
- **docs**: Documentation changes
- **style**: Code style changes (formatting, etc.)
- **refactor**: Code refactoring
- **perf**: Performance improvements
- **test**: Adding/updating tests
- **build**: Build system changes
- **ci**: CI/CD changes
- **deps**: Dependency updates
- **chore**: Other maintenance tasks

### Commit Message Validation

The project uses **commitlint** to ensure commit messages follow conventional format. Invalid commits will be rejected.

## 🔄 Semantic Release

This project uses **semantic-release** for automated versioning and changelog generation.

### How It Works

Semantic Release automatically:

- 🏷️ Determines version bumps based on commit types
- 📋 Generates CHANGELOG.md
- 🏷️ Creates Git tags
- 📦 Publishes releases (if configured)

#### Version Bump Rules:

- **MAJOR** (1.0.0 → 2.0.0): Breaking changes (`BREAKING CHANGE:` in commit body)
- **MINOR** (1.0.0 → 1.1.0): New features (`feat:` commits)
- **PATCH** (1.0.0 → 1.0.1): Bug fixes (`fix:` commits)
- **PATCH** (1.0.0 → 1.0.1): Dependencies (`deps:` commits)

### Dry Run Semantic Release

Test what semantic-release would do without actually releasing:

```bash
# Dry run (see what would happen)
npx semantic-release --dry-run

# Dry run with verbose output
npx semantic-release --dry-run --debug

# Check if release is needed
npx semantic-release --dry-run --no-ci
```

### Manual Release

```bash
# Run semantic release (usually done by CI)
npm run semantic-release
```

### Supported Branches

Releases happen on these branches:

- **master**: Main releases (1.0.0, 1.1.0, etc.)
- **next**: Next major releases
- **beta**: Beta releases (1.1.0-beta.1)
- **alpha**: Alpha releases (1.1.0-alpha.1)

## 🔧 Pre-commit Hook Details

The `.husky/pre-commit` hook runs:

```bash
# 1. Run lint-staged (format & lint staged files)
npx lint-staged

# 2. Build project (ensure compilation)
npm run build
```

### Lint-staged Configuration

In `package.json`:

```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx,json,css,md}": ["prettier --write", "git add"],
    "*.{js,jsx,ts,tsx}": ["eslint --fix", "git add"]
  }
}
```

### Skip Pre-commit Hooks (Not Recommended)

```bash
# Skip pre-commit hooks (emergency only)
git commit -m "fix: emergency fix" --no-verify
```

## 📁 Project Structure

```
├── .husky/              # Git hooks
│   └── pre-commit       # Pre-commit formatting & linting
├── .github/             # GitHub workflows
├── src/
│   └── app/             # Next.js app directory
├── public/              # Static assets
├── .releaserc.json      # Semantic release config
├── .prettierrc          # Prettier config
├── .prettierignore      # Prettier ignore patterns
├── eslint.config.mjs    # ESLint configuration
├── package.json         # Dependencies & scripts
└── CHANGELOG.md         # Auto-generated changelog
```

## 🚀 Deployment

### Vercel (Recommended)

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

### CI/CD Pipeline

The project includes GitHub Actions for:

- ✅ Code quality checks
- ✅ Automated releases
- ✅ Deployment

## 🛡️ Troubleshooting

### Common Issues

1. **Pre-commit fails**: Run `npm run lint` and `npm run format` manually first
2. **Commit rejected**: Ensure commit message follows conventional format
3. **Build fails**: Check TypeScript errors with `npm run build`
4. **Release not created**: Ensure commits follow semantic conventions

### Reset Git Hooks

```bash
# Reinstall git hooks
npx husky install
```

### Debug Semantic Release

```bash
# Check semantic release logs
npx semantic-release --dry-run --debug
```

## 📚 Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Release](https://semantic-release.gitbook.io/)
- [Husky Git Hooks](https://typicode.github.io/husky/)
- [Prettier Code Formatter](https://prettier.io/)
- [ESLint](https://eslint.org/)
