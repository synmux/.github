# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a GitHub account-level configuration repository (`.github`). It provides organization-wide defaults for:

- GitHub Actions workflows
- Code quality automation (linting, security scanning)
- Community health files (CODE_OF_CONDUCT, CONTRIBUTING, SECURITY)
- AI-assisted code review configuration

## Commands

### Linting and Formatting

```bash
# Run all linters
trunk check

# Run linters with auto-fix
trunk fmt

# Check specific file
trunk check path/to/file

# Format specific file
trunk fmt path/to/file
```

### Git Hooks (Trunk-managed)

- **Pre-commit**: Runs `trunk fmt` on staged files
- **Pre-push**: Runs `trunk check` on all changes

## Code Quality Standards

### Enabled Linters

| Linter         | Purpose                                   |
| -------------- | ----------------------------------------- |
| `actionlint`   | GitHub Actions workflow validation        |
| `checkov`      | Infrastructure-as-code security           |
| `markdownlint` | Markdown formatting (Prettier-compatible) |
| `prettier`     | General formatting                        |
| `trufflehog`   | Secret detection                          |
| `yamllint`     | YAML validation                           |

### YAML Conventions

- Quote strings only when needed
- No implicit octal values
- No duplicate keys

### Markdown Conventions

- Prettier-compatible formatting (formatting rules delegated to Prettier)
- Focus on content structure, not whitespace

## Architecture

```text
.github/
├── workflows/           # GitHub Actions
│   ├── claude.yaml      # @claude mention responder (issues/PRs/comments)
│   ├── claude-code-review.yaml  # Automatic PR review
│   └── devskim.yaml     # Microsoft security scanning
├── dependabot.yml       # Daily dependency updates
└── CODEOWNERS           # @synmux owns all files

.trunk/
├── trunk.yaml          # Linter orchestration config
└── configs/            # Linter-specific settings
```

## AI Integration

### Claude Code Action

Two workflows use Claude Code:

1. **`claude.yaml`** - Responds to `@claude` mentions in issues, PRs, and comments
2. **`claude-code-review.yaml`** - Automatic PR review on open/sync

Both use Claude Opus with restricted tools (`gh` CLI only for GitHub operations).

### Review Guidelines

When reviewing PRs in this repository:

- Validate GitHub Actions workflow syntax and best practices
- Check for security issues (secrets exposure, overly permissive permissions)
- Ensure YAML follows the yamllint rules (quote only when needed, no implicit octals)
- Verify Markdown is well-structured
- Confirm Dependabot and workflow configurations are valid

## Required Status Checks

PRs must pass:

- **CodeQL** - Static analysis
- **devskim** - Security scanning
- **codacy** - Code quality

## Contributing

PRs must be from a feature branch (not `main`/`master` in the fork).
