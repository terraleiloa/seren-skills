# Contributing to Seren Skills

Thanks for contributing! This guide covers how to add new skills or improve existing ones.

## Before You Start

- Check the [repo structure](README.md#structure) to avoid duplicates
- Skills that run code autonomously (trading bots, scrapers) get more scrutiny — open an issue first to discuss

## Creating a New Skill

### 1. Create the directory

Skills live at `{org}/{skill-name}/` at the repo root. Use an existing org or create a new one.

```bash
# First-party Seren skill
mkdir -p seren/browser-automation/

# Third-party skill under your org
mkdir -p coinbase/grid-trader/
```

The slug is derived from the path: `coinbase/grid-trader/` → `coinbase-grid-trader`.

### 2. Write SKILL.md

Every skill needs a `SKILL.md` with YAML frontmatter:

```yaml
---
name: My Skill Name
description: "Clear description of what this skill does and when to use it"
kind: agent              # agent | integration | guide
runtime: python          # python | node | bash | docs-only
author: Your Name
version: 1.0.0
tags: [relevant, searchable, tags]
publishers: [seren-publishers-used]    # optional
cost_estimate: "$X per operation"       # optional
---

# My Skill Name

Detailed documentation goes here...
```

**Required fields:** `name`, `description`, `kind`, `runtime`

The `kind` field describes the nature of the skill:

- **agent** — Runs code autonomously (trading bot, scraper, automation)
- **integration** — Documents an API for agents to use (SKILL.md only)
- **guide** — Teaches users or agents how to do something (SKILL.md only)

### 3. Include runtime files if applicable

Skills with `runtime: python` or `runtime: node` should include:

- Runtime code (e.g., `agent.py`, `index.js`)
- Dependency file (`requirements.txt` or `package.json`)
- `.env.example` if environment variables are needed
- `.gitignore` for local config and secrets

Skills with `runtime: docs-only` only need `SKILL.md`.

## Pull Request Process

1. Fork the repo and create a branch
2. Add your skill under `{org}/{skill-name}/`
3. Open a PR with a description of what the skill does

### What we look for

- **All skills**: Clear description, correct frontmatter, no secrets committed
- **Agent skills**: Code review, security review, and smoke test — expect thorough review
- **Integration skills**: API contract accuracy, auth handling, example correctness
- **Guide skills**: Clarity, accuracy, completeness

## Style Guide

- Skill names: title case (`Coinbase Grid Trader`, not `coinbase-grid-trader`)
- Directory names: kebab-case (`grid-trader`, not `GridTrader`)
- Org names: lowercase kebab-case (`coinbase`, `apollo`, `seren`)
- Description: write for the agent — explain **when** to use the skill, not just what it is
- Tags: lowercase, use existing tags when possible
- Keep SKILL.md focused. Put extended docs in a `README.md` alongside it.
