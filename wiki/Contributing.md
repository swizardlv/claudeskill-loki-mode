# Contributing

Guide for contributing to Loki Mode.

---

## Getting Started

### Prerequisites

- Node.js 16+
- Git
- Claude Code CLI (for testing)

### Clone Repository

```bash
git clone https://github.com/asklokesh/loki-mode.git
cd loki-mode
```

### Install Dependencies

```bash
npm install
npm link
```

### Verify Setup

```bash
loki --version
./tests/run-all-tests.sh
```

---

## Project Structure

```
loki-mode/
  SKILL.md               # Core skill definition
  VERSION                 # Version number
  CHANGELOG.md           # Release history

  autonomy/              # Runtime components
    run.sh               # Main orchestrator
    notify.sh            # Notification system
    api-server.js        # HTTP API server

  providers/             # AI provider integrations
    claude.sh
    codex.sh
    gemini.sh
    loader.sh

  skills/                # Modular skill documentation
    00-index.md
    model-selection.md
    quality-gates.md
    ...

  references/            # Detailed documentation
    ...

  wiki/                  # GitHub Wiki content
    ...

  tests/                 # Test scripts
    run-all-tests.sh
    test-*.sh

  vscode-extension/      # VS Code integration
    ...
```

---

## Development Workflow

### Create Feature Branch

```bash
git checkout -b feature/my-feature
```

### Make Changes

1. Edit relevant files
2. Follow existing code patterns
3. Add tests if needed

### Run Tests

```bash
# Run all tests
./tests/run-all-tests.sh

# Run specific test
./tests/test-wrapper.sh
```

### Commit Changes

```bash
git add -A
git commit -m "feat: add my feature"
```

### Create Pull Request

```bash
git push origin feature/my-feature
gh pr create
```

---

## Code Style

### Shell Scripts

- Use POSIX-compatible syntax when possible
- Use `shellcheck` for linting
- Add `set -euo pipefail` for error handling
- Quote variables: `"$var"` not `$var`

### JavaScript

- Node.js built-ins only (no npm dependencies for core)
- ES6+ syntax
- JSDoc comments for public functions

### Markdown

- Use consistent heading levels
- Include code examples
- Add "See Also" sections

### Important Rules

- **No emojis** - Never use emojis in code, documentation, or commits
- **Keep it simple** - Don't over-engineer
- **Test changes** - All changes should be tested
- **Clean up** - Remove test files and kill test processes

---

## Testing

### Running Tests

```bash
# All tests
./tests/run-all-tests.sh

# Individual tests
./tests/test-wrapper.sh
./tests/test-state-recovery.sh
./tests/test-circuit-breaker.sh
./tests/test-rate-limiting.sh
```

### Writing Tests

Create `tests/test-my-feature.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
source "$SCRIPT_DIR/test-utils.sh"

echo "Testing my feature..."

# Test case 1
assert_equals "expected" "$(my_function)"

# Test case 2
assert_file_exists "./expected-file.txt"

echo "All tests passed!"
```

---

## Documentation

### Wiki Pages

Wiki source is in `wiki/` directory. Changes sync automatically on release.

### Adding New Page

1. Create `wiki/My-Page.md`
2. Add to `wiki/_Sidebar.md`
3. Add cross-references with `[[Page Name]]`

### Updating Existing Docs

1. Edit file in `wiki/`
2. Verify links work
3. Update version if needed

---

## Pull Request Guidelines

### Title Format

```
type: short description

Examples:
feat: add voice input support
fix: correct API port in docs
docs: update installation guide
refactor: simplify provider loading
test: add circuit breaker tests
```

### Description Template

```markdown
## Summary
Brief description of changes.

## Changes
- Change 1
- Change 2

## Testing
How this was tested.

## Checklist
- [ ] Tests pass
- [ ] Documentation updated
- [ ] No emojis added
- [ ] Follows code style
```

---

## Release Process

Releases are handled by maintainers:

1. Update VERSION file
2. Update CHANGELOG.md
3. Create commit: `release: vX.Y.Z - description`
4. Push to main (GitHub Actions handles the rest)

---

## Getting Help

- **Questions**: Open a GitHub Discussion
- **Bugs**: Open a GitHub Issue
- **Features**: Open a GitHub Issue with `[Feature]` prefix

---

## Code of Conduct

- Be respectful and inclusive
- Focus on constructive feedback
- Help others learn
- No spam or self-promotion

---

## License

Loki Mode is MIT licensed. By contributing, you agree that your contributions will be licensed under MIT.

---

## See Also

- [[FAQ]] - Frequently asked questions
- [[Troubleshooting]] - Common issues
- [GitHub Issues](https://github.com/asklokesh/loki-mode/issues)
