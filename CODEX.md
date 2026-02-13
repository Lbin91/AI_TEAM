# CODEX Adapter

## Read Order
1. `README.md`
2. `AGENTS.md`
3. `PERSONA_GUIDE.md`
4. Required files in `personas/*.md`

## Persona Selection Rules
- Default: one primary + up to two support personas.
- Add `P10` when security/compliance is in scope.
- Add `P12` when regression/test risk is in scope.

## Work Rules
- Check selected personas' priorities and risk posture before execution.
- Keep output contract intact, with action-first recommendations.
- If a new persona is required, add it and update `PERSONA_GUIDE.md` in the same change.

## Required Metadata
```yaml
selection:
  primary: Pxx
  support: [Pxx]
  reason: short
  constraints: short
```
