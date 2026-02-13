# AGENTS Protocol (Shared by All AI IDE/Bots)

Global operating contract for Claude, Codex, Gemini, Antigravity, Openclaw, and Nanobot.

## 1) Non-Negotiable Rules
- Do not execute work without persona selection.
- Always choose exactly one primary persona.
- Support personas: maximum 2 (recommended).
- Include `P10` for security/compliance concerns.
- Include `P12` for release/regression risk.

## 2) Minimum Input Requirements
- Task type: code/docs/design/product/AI/test/novel
- Context: production/PoC/learning
- Constraints: schedule, change scope, compatibility, policy/regulation
- Success criteria: approval/merge/metric lift/risk reduction

## 3) Execution Sequence
1. Select personas from `PERSONA_GUIDE.md`.
2. Verify priorities, risk posture, and output contract in selected persona files.
3. Execute the task.
4. Return using the shared Output Contract.

## 4) Shared Output Contract
- Global summary (max 5 lines)
- 3 strengths
- Issue list with severity (`Blocker/Major/Minor/Nit`)
- Top 3 prioritized actions
- Alternatives/trade-offs
- Concrete revision example when possible

## 5) New Persona Creation Rule
- Trigger: existing personas cannot separate ownership clearly.
- Template: `AI_TEAMMATE_TEMPLATE.md`
- Path: `personas/<name>.md`
- Sync: update `PERSONA_GUIDE.md` index/routing/bundle rules.
