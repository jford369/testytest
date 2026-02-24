# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working in this repository.

## Repository Overview

This is an **OSINT (Open Source Intelligence) investigation workspace** using Bellingcat toolkit methodologies. See `OSINT_WORKSPACE.md` for the full project reference (tools, APIs, workflows).

Focus areas:
- Federal detention facility expansion (property records, procurement, permits)
- Corporate/financial research on government contractors
- Geolocation and visual analysis from photographic evidence
- Cross-referencing public records across multiple databases

Collaborative project with **Project Salt Box** (Maryland-based volunteer OSINT group).

---

## User Skill Level — READ THIS FIRST

The user is **familiar with R but new to Python and command-line tooling**. This means:

- **Explain what scripts do before running them** — use clear comments in all code
- **When installing tools, explain what each dependency does**
- **If something can be done simply, do it simply. Don't over-engineer.**
- **Prefer step-by-step workflows** the user can understand and repeat
- Use `pandas` conventions (similar to R dataframes) when possible

---

## Project Structure

```
/data/{investigation-name}/       # Raw collected data per investigation (GITIGNORED)
/data/{investigation-name}/notes/ # Methodology notes, hypothesis tracking
/outputs/                         # Analysis outputs, visualizations, reports
/scripts/                         # Reusable collection and analysis scripts
/tools/                           # Local tool configs and setup notes
OSINT_WORKSPACE.md                # Full tool/API/workflow reference
CLAUDE.md                         # This file (AI assistant guidance)
.gitignore                        # Keeps data and secrets out of git
```

---

## Python Environment

Use a virtual environment. Set up with:
```bash
python -m venv venv
source venv/bin/activate   # Linux/Mac
pip install -r requirements.txt
```

Key base packages:
- `requests`, `beautifulsoup4` — web scraping basics
- `pandas` — data analysis (similar to R dataframes)
- `playwright` — for JavaScript-heavy government sites that need a real browser
- `folium` — interactive mapping
- `python-dotenv` — managing API keys safely via `.env`

---

## Data Handling Rules — CRITICAL

- **NEVER** commit API keys or credentials. Use `.env` (gitignored).
- **NEVER** commit personal data about private individuals. Keep in `/data/` (gitignored).
- Raw data files (CSVs, JSONs, images) go in `/data/`, not tracked by git.
- Only commit scripts, documentation, and sanitized/aggregated outputs.

---

## Git Workflow

### Branch Naming
- Feature branches: `feature/<short-description>`
- Bug fix branches: `fix/<short-description>`
- AI-generated branches: `claude/<task-id>`

### Commit Messages
Use the imperative mood and keep the first line under 72 characters:
```
Add EDGAR scraping script for contractor filings
Fix CSV parsing for SDAT property records
Add folium map for facility locations
```

### Push Convention
Always push with tracking:
```bash
git push -u origin <branch-name>
```

---

## Code Conventions

### General
- Prefer clarity over cleverness — the user needs to understand and maintain this code
- Keep functions small and focused on a single responsibility
- Avoid unnecessary abstractions; don't build for hypothetical future requirements
- Delete unused code rather than commenting it out
- Add clear comments explaining *why*, not just *what*

### Python Style
- Use descriptive variable names (not single letters)
- Add docstrings to functions explaining inputs, outputs, and purpose
- Print progress messages in scripts so the user knows what's happening
- Handle errors with clear messages, not silent failures

### Files
- Never create files unless they are required by the task
- Prefer editing existing files over creating new ones
- Do not add auto-generated boilerplate or placeholder comments

### Dependencies
- Do not add new dependencies without explaining what they do
- Prefer standard library / built-in solutions where reasonable
- Install tools one at a time as needed, not all at once

---

## Investigation Methodology

- Document every step: what was searched, when, what was found or not found
- Cross-reference findings across at least 2 independent sources before treating as confirmed
- Archive/screenshot evidence at time of discovery (pages change or disappear)
- Track hypotheses explicitly — note when evidence supports or contradicts them
- Acknowledge tool limitations honestly rather than presenting overconfident conclusions

---

## Security

- Never commit secrets, credentials, API keys, or tokens
- Use environment variables or `.env` for sensitive configuration
- Validate all external input at system boundaries
- Be cautious with scraping — respect rate limits and `robots.txt`

---

## Working with AI Assistants

When using Claude Code or similar tools in this repository:

1. **Read before editing** — always read a file fully before modifying it
2. **Minimal changes** — only change what is necessary for the task
3. **No speculative features** — do not add features that aren't explicitly requested
4. **Explain everything** — the user is learning Python; explain what code does and why
5. **Preserve conventions** — match the style and patterns already present in the codebase
6. **Update this file** — if you establish a new convention or add significant tooling, update CLAUDE.md
7. **Respect data rules** — never stage or commit anything from `/data/` or `.env`
