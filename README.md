# AI_TEAM Router README (Agent-Only)

This repository is an agent routing hub, not a human-facing handbook.
Goal: map each request to the right persona set and return executable output.

## Scope
- Claude Code
- Codex
- Gemini
- Antigravity
- Openclaw
- Nanobot

## Read Order
1. `AGENTS.md` (global contract)
2. Adapter file (`CLAUDE.md`, `GEMINI.md`, `CODEX.md`)
3. `PERSONA_GUIDE.md` (index, routing, bundles)
4. `personas/*.md` (persona specs)
5. `AI_TEAMMATE_TEMPLATE.md` (new persona template)

## Minimal Execution Flow
1. Classify request: `code | product | design | docs | ai | security | test | novel`.
2. Set risk: `low | medium | high`.
3. Select one primary persona and up to two support personas.
4. If security/compliance is involved, include `P10`.
5. If release regression risk exists, include `P12`.
6. Return output using the shared Output Contract.

## Default Routing Map
- Production code: `P03 + P05 + P10 + P12`
- Product/PRD: `P01 + P11 (+P02)`
- Design/UX: `P08 + P04 (+P01)`
- AI/LLM systems: `P06 + P07 (+P10)`
- Security/compliance: `P10 + domain primary`
- QA/testing: `P12 + domain primary (+P10)`
- Novel/manuscript: `P13 (+P09)`

## Missing Persona Rule
Create a new persona only when existing personas cannot separate responsibility cleanly.

Required actions:
- Use `AI_TEAMMATE_TEMPLATE.md`
- Save as `personas/<new_persona>.md`
- Update `PERSONA_GUIDE.md` (index, routing rule, and bundle if needed)

## Required Response Metadata
```yaml
selection:
  primary: Pxx
  support: [Pxx, Pxx]
  reason: short
  risk: low|medium|high
```
