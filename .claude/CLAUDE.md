# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

<!-- Describe what this project does and its main purpose -->

## Setup

```bash
# Install dependencies
# e.g., npm install / pip install -r requirements.txt
```

## Development Commands

```bash
# Run the project
# e.g., npm start / python main.py

# Run tests
# e.g., npm test / pytest

# Run a single test
# e.g., npm test -- --testPathPattern=<name> / pytest tests/test_foo.py

# Lint / format
# e.g., npm run lint / ruff check .
```

## Architecture

<!-- Describe the high-level architecture: main entry points, key modules, data flow -->

## Key Conventions

<!-- Any project-specific patterns, naming conventions, or important constraints -->

## Mandatory Workflow — Obsidian Vault

**EVERY task in this project requires the `obsidian-vault-workflow` skill.**

- **Before starting any task:** Run Phase 1 of the skill — identify topic, read the vault topic file, read recent Meeting Notes.
- **After completing any task:** Run Phase 2 of the skill — write/update the topic file in `vault/`, append a dated Session Log entry, verify the write.

Skip only for pure read-only questions that touch zero files and produce zero decisions.

The vault is at `vault/` — it is Claude Code's long-term memory for this project.
