# CLAUDE Adapter

## Read Order
1. `README.md`
2. `AGENTS.md`
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
