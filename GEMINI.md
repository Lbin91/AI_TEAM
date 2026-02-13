# GEMINI Adapter

## Read Order
1. `README.md`
2. `AGENTS.md`
3. `PERSONA_GUIDE.md`
4. Required files in `personas/*.md`

## Persona Selection Rules
- Exactly one primary persona.
- Up to two support personas.
- Add `P10` for security/compliance risk.
- Add `P12` for release/testing risk.

## Output Rules
1. `selection` metadata block
2. Output contract body
3. Top 3 immediately executable actions

```yaml
selection:
  primary: Pxx
  support: [Pxx, Pxx]
  risk: low|medium|high
```
