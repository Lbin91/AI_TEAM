# CLAUDE Adapter

## Read Order
1. `AGENTS.md`
2. `README.md` (project context)
3. `PERSONA_GUIDE.md`
4. Required files in `personas/*.md`

## Persona Selection Rules
- One primary persona + up to two support personas.
- Add `P10` for security/compliance.
- Add `P12` for release/regression risk.

## Response Format
Emit persona selection metadata first, then body.

```yaml
selection:
  primary: Pxx
  support: [Pxx]
  reason: short
```

Body order: `summary -> issues by severity -> top 3 actions -> revision examples`.

## Commit Rules (Project Override)
Commit messages in this repo MUST be in **English**, overriding the global Korean default.

Format:
```
type: short description

Optional body with details.

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
```

Types: `feat`, `fix`, `refactor`, `docs`, `chore`, `test`
