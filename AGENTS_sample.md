# AGENTS (Project Configuration)

This project uses a centralized AI persona system via the `.AI_TEAM` symlink.

---

## AI Agent Operating Rules

When performing **document writing/review** or **code writing/review**:

1. Read `.AI_TEAM/AGENTS.md` to understand the global operating protocol.
2. Select appropriate personas from `.AI_TEAM/PERSONA_GUIDE.md` for your task.
3. Follow detailed instructions from `.AI_TEAM/personas/*.md` for selected personas.

**IMPORTANT:** Do not proceed without persona selection.

---

## Project Context (Optional)

**[Fill in project-specific constraints as needed]**

```yaml
# Example:
project: "Project Name"
type: "backend/frontend/fullstack"
constraints:
  - "API compatibility must be maintained"
  - "Performance SLA under 100ms"
default_personas: [P03, P10, P12]  # Recommended default personas
```

---

## References

- `.AI_TEAM/AGENTS.md` - Global protocol
- `.AI_TEAM/PERSONA_GUIDE.md` - Persona selection guide
- `.AI_TEAM/personas/` - Detailed persona definitions (P01~P13)
- `.AI_TEAM/SSOT_SETUP.md` - Setup guide (for humans)
