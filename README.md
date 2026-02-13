# AI_TEAM

Shared persona SSOT for coding and writing agents.

## For AI Agents
Start with `AGENTS.md`.

Then read, in order:
1. Adapter file (`CLAUDE.md`, `CODEX.md`, `GEMINI.md`) when applicable
2. `PERSONA_GUIDE.md`
3. `personas/*.md`
4. `AI_TEAMMATE_TEMPLATE.md` (for new persona creation)

## What This Repository Provides
- Stable persona definitions for common task domains
- Selection/routing rules and bundles
- A template for creating new personas without drift
- SSOT setup guide for multi-device use (`SSOT_SETUP.md`)

## Repository Layout
```text
AGENTS.md                # Global contract for AI agents
PERSONA_GUIDE.md         # Persona index, routing, bundles, QC
AI_TEAMMATE_TEMPLATE.md  # Canonical persona authoring template
SSOT_SETUP.md            # Multi-device SSOT setup (symlink/submodule)
CLAUDE.md                # Claude adapter
CODEX.md                 # Codex adapter
GEMINI.md                # Gemini adapter
personas/*.md            # Persona specifications
```

## Quick Start (Human Maintainers)
1. Clone this repository once per device to `~/.AI_TEAM`.
2. In each project, link `.AI_TEAM` to `~/.AI_TEAM` (or use submodule fallback).
3. Keep persona edits centralized in this repo.

See `SSOT_SETUP.md` for exact commands.

## Public Repository Policy
- Keep content non-sensitive and portable.
- Do not commit API keys, secrets, private credentials, or personal data.
- Keep persona files in English for token efficiency and cross-agent consistency.
