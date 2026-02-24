# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working in this repository.

## Repository Status

This is a **new, empty repository**. No source files, dependencies, or infrastructure exist yet. This CLAUDE.md serves as a starting point for conventions to follow as the project is built out.

When the project is initialized with actual code, update this file to reflect:
- The chosen technology stack
- Build and test commands
- Project-specific conventions

---

## Git Workflow

### Branch Naming
- Feature branches: `feature/<short-description>`
- Bug fix branches: `fix/<short-description>`
- AI-generated branches: `claude/<task-id>`

### Commit Messages
Use the imperative mood and keep the first line under 72 characters:
```
Add user authentication module
Fix null pointer in payment processor
Refactor database connection pooling
```

### Push Convention
Always push with tracking:
```bash
git push -u origin <branch-name>
```

---

## Development Setup

> **TODO**: Fill this in once the project stack is chosen.

Typical sections to add here:
- Prerequisites (runtime versions, system dependencies)
- Installation steps
- Environment variable configuration
- Local development server commands

---

## Build & Test Commands

> **TODO**: Fill this in once build tooling is configured.

Document the exact commands to:
```bash
# Install dependencies
<command>

# Run the development server
<command>

# Run tests
<command>

# Run linter / formatter
<command>

# Build for production
<command>
```

Always run tests and the linter before committing. If tests fail, fix them before pushing.

---

## Project Structure

> **TODO**: Update this once the project is scaffolded.

```
/
├── src/           # Application source code
├── tests/         # Test files (mirror the src/ structure)
├── docs/          # Documentation
└── CLAUDE.md      # This file
```

---

## Code Conventions

### General
- Prefer clarity over cleverness
- Keep functions small and focused on a single responsibility
- Avoid unnecessary abstractions; don't build for hypothetical future requirements
- Delete unused code rather than commenting it out

### Files
- Never create files unless they are required by the task
- Prefer editing existing files over creating new ones
- Do not add auto-generated boilerplate or placeholder comments

### Dependencies
- Do not add new dependencies without a clear need
- Prefer standard library / built-in solutions where reasonable
- Document why a non-obvious dependency was chosen

---

## Security

- Never commit secrets, credentials, API keys, or tokens
- Use environment variables for sensitive configuration
- Validate all external input at system boundaries
- Follow OWASP Top 10 guidance for web applications

---

## Working with AI Assistants

When using Claude Code or similar tools in this repository:

1. **Read before editing** — always read a file fully before modifying it
2. **Minimal changes** — only change what is necessary for the task; avoid refactoring unrelated code
3. **No speculative features** — do not add error handling, fallbacks, or features that aren't explicitly requested
4. **Preserve conventions** — match the style and patterns already present in the codebase
5. **Update this file** — if you establish a new convention or add significant tooling, update CLAUDE.md to reflect it
