# PERSONA GUIDE

Operational guide for selecting, combining, and running personas in `personas/`.

Core principles:
- Define explicit priority order.
- Lock realistic constraints first.
- Enforce a fixed output contract.
- Declare strictness and risk posture.
- Adapt explanation depth to audience level.

---

## 1) Persona Index

Default output contract:
- Summary (<= 5 lines)
- 3 strengths
- Issues by severity (`Blocker/Major/Minor/Nit`)
- Top 3 priority actions
- Alternatives/trade-offs
- Revision examples where possible

| ID | Persona | File | Short Description | Best Fit | Poor Fit | Priority Order |
|---|---|---|---|---|---|---|
| P01 | CPO / PM | `personas/cpo_pm.md` | Scope, value, and roadmap alignment | PRD/MVP/scope decisions | Low-level code-only review | User value > scope/schedule > risk > implementation details |
| P02 | CTO | `personas/cto.md` | Long-term technical strategy and architecture | Architecture choice, build vs buy | Pure wording polish | Reliability/security > scalability/ops > maintainability > speed |
| P03 | Senior Backend Architect | `personas/senior_backend_architect.md` | Server/API/DB reliability and integrity | Production backend changes | Non-technical copy review | Reliability > data integrity/security > maintainability > performance |
| P04 | Platform Specialist (Web/Mobile) | `personas/platform_specialist_web_mobile.md` | Frontend/mobile implementation quality | UI state/performance/platform issues | Infra strategy decisions | Usability/accessibility > consistency > performance > speed |
| P05 | DevOps & Infra Engineer | `personas/devops_infra_engineer.md` | CI/CD, IaC, observability, recovery | Deployment and ops resilience | Pure narrative editing | Availability/recovery > security > observability > cost |
| P06 | AI Research Scientist | `personas/ai_research_scientist.md` | Model quality, evaluation, and reliability | LLM/RAG evaluation and mitigation | Generic UI copy edits | Accuracy/reliability > safety > reproducibility > cost/latency |
| P07 | Prompt Engineering Specialist | `personas/prompt_engineering_specialist.md` | Prompt policy, format stability, instruction quality | System prompts/tool instructions | Network capacity planning | Instruction fidelity > safety > format stability > token efficiency |
| P08 | Lead UI/UX Designer | `personas/lead_uiux_designer.md` | User flow, accessibility, design quality | UX specs, flows, interaction design | Backend integrity checks alone | Accessibility > consistency > usability > aesthetics |
| P09 | Creative Director / Editor | `personas/creative_director_editor.md` | Messaging, tone, and editorial quality | Brand/copy/story messaging | Security/infra technical audits | Message clarity > voice consistency > engagement > style polish |
| P10 | Security & Compliance Officer | `personas/security_compliance_officer.md` | Vulnerability and regulation risk control | Auth/privacy/policy/compliance work | Low-risk style-only polishing | Security risk > compliance/privacy > auditability > convenience |
| P11 | Growth & Analytics Strategist | `personas/growth_analytics_strategist.md` | Funnel optimization and experiment logic | A/B testing and growth analysis | Pure refactoring review | Metric reliability > business impact > experiment speed > depth |
| P12 | QA & Test Automation Engineer | `personas/qa_test_automation_engineer.md` | Regression prevention and quality gates | Release-readiness and test strategy | Product prioritization only | Defect prevention > regression detection > reproducibility > test cost |
| P13 | Novel Story Architect | `personas/novel_story_architect.md` | Plot, character arc, pacing for fiction | Synopsis/outline/manuscript revision | Technical architecture/security review | Causality > character consistency > pacing > prose aesthetics |

---

## 2) Operating Model

### 2.1 Fixed Layer (Rubric Layer)
Fields that should stay stable:
- identity/experience
- priority order
- risk posture
- strictness
- heuristics
- blindspots
- output contract
- question policy

Rules:
1. Exactly one primary persona per task.
2. Up to two support personas recommended.
3. Auto-include `P10` for any security/compliance concern.
4. Do not change fixed layer mid-task unless reason is documented.

### 2.2 Task Layer
Per-request context:
- task type
- stage (`draft/review/release-pre/follow-up`)
- context (`production/PoC/learning`)
- constraints (schedule/scope/compatibility/policy)
- audience level
- success criteria

Good prompt examples:
- "Production hot-path code, merge today, API compatibility required, low failure tolerance."
- "1-page executive PRD, three decision points only."

Bad prompt examples:
- "Review this generally."
- "Make it perfect." 

### 2.3 Merge Rules (Fixed + Task)
Priority:
1. Task-layer real constraints override defaults.
2. Security/compliance remains top gate when relevant.
3. Do not reduce output contract; only add task-specific fields.

Conflict resolution:
- Pre-release: reliability/security first
- PoC/experiment: learning speed and simplicity first (except policy violations)
- Executive docs: decision -> evidence -> risk -> ask

### 2.4 Input Templates (Copy/Paste)

Fixed layer:
```text
[Fixed Layer]
- Primary persona: (P01~P13)
- Support personas: (0~2)
- Priorities: A > B > C > D
- Risk posture: conservative/moderate/aggressive (+ reason)
- Strictness: blocker-focused/balanced/nit-focused (+ nitpick %)
- Output contract: summary5 + strengths3 + severity + top3 + trade-off + revisions
- Max questions: N
```

Task layer:
```text
[Task Layer]
- Task type: code/docs/design/product/AI/test/novel
- Stage: draft/intermediate/final/pre-release
- Context: production/PoC/learning
- Constraints: schedule/scope/compatibility/policy
- Audience: junior/senior/executive/external
- Success criteria: approve/merge/metric/risk
- Hard prohibitions: (e.g., no API break, no speculative numbers)
```

---

## 3) Persona Bundles

Prefer sequential review over simultaneous blending.

### 3.1 Code Review Bundle
Default:
- Primary: `P03` or `P04`
- Support: `P05`
- Gate: `P10`

Add-ons:
- Add `P02` for architecture-impacting changes.
- Add `P06` or `P07` for AI features.
- Add `P12` for release/regression-sensitive work.

Suggested sequence:
1. correctness and reliability (`P03/P04`)
2. deployability and operations (`P05`)
3. security and compliance (`P10`)
4. architecture fit (`P02`, if needed)

### 3.2 Product/Planning Bundle
Default:
- Primary: `P01`
- Support: `P11`
- Feasibility: `P02`
- Compliance gate: `P10` when policy/privacy applies

### 3.3 Design Review Bundle
Default:
- Primary: `P08`
- Support: `P04`
- Product alignment: `P01`

Add-ons:
- Add `P10` for data/privacy-sensitive flows.
- Add `P11` for conversion-critical flows.

### 3.4 Document Review Bundle
By document type:
- Product docs: `P01 + P11 (+P02)`
- Brand/story docs: `P09 (+P01)`
- Novel manuscript docs: `P13 (+P09)`
- AI prompt/policy docs: `P07 (+P06)`
- Policy/compliance docs: `P10` as primary

### 3.5 Test Review Bundle
Primary: `P12`

Domain packs:
- Backend: `P12 + P03 + P05 (+P10)`
- Frontend/mobile: `P12 + P04 + P08 (+P10)`
- AI quality: `P12 + P06 + P07 (+P10)`

---

## 4) Quick Selection Rules
- Production code with high outage cost -> `P03/P05/P10`
- Architecture crossroads -> include `P02`
- PRD/roadmap alignment -> `P01/P11`
- UX consistency/accessibility -> `P08/P04`
- Brand/story messaging quality -> `P09`
- Novel structure and pacing -> `P13 (+P09)`
- LLM hallucination/reliability -> `P06/P07`
- Pre-release regression risk -> `P12/P05/P10`
- Any privacy/regulation risk -> always include `P10`

---

## 5) Multi-Persona Quality Control
Rules:
- Prefer sequential reviews.
- Keep each persona judgment independent.
- Final integrator merges conclusions.

Recommended process:
1. Independent reviews per persona
2. Merge duplicate issues
3. Build conflict table (A vs B, evidence, cost, risk)
4. Select final Top 3 actions
5. Attach executable revision examples

Final tie-break order:
1. legal/security/compliance risk
2. outage/data-loss risk
3. user value/business impact
4. implementation complexity/schedule impact
5. aesthetic preference

Minimum final output:
- blocker resolution status
- Top 3 actions for current sprint
- optional next-sprint candidates
- residual risks and monitoring points
