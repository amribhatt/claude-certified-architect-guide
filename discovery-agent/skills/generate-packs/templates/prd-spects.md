# Product Requirements Document — {{Project name}}
*Structured with the S.P.E.C.T.S. framework · archetype: {{Traditional / Predictive / Generative / Agentic / Hybrid}}*

---

## S — Scope

### Problem & context
### Restated problem
> "So we're building **{{one sentence}}** that can:
> - …
> - …"

### Task domain · autonomy level · adaptation scope · scale
| Dimension | Decision | Source |
|---|---|---|
| Task domain | narrow / horizontal — … | (C-…) |
| Autonomy | L0–L4 overall; per-action table in §C | (C-…) |
| Adaptation | same-domain / cross-domain; few-shot (n=…) / zero-shot | (C-…) |
| Scale | users at launch → 12 months; tenancy | (C-…) |

### Assumptions ✅ · Non-goals ❌
### Definition of success
> "Success means **{{measurable sentence}}**."

---

## P — Product requirements

### User segments
| Segment | Primary / secondary | Needs | Trust signal they need |
|---|---|---|---|

### Core use cases
For each: trigger → understand → plan → act → validate → approve/escalate → learn.
Include failure path, unknown path and escalation path.

#### UC-1 {{name}}
1. …

### Functional requirements
| ID | Requirement | Use case | Priority | Acceptance criteria | Source |
|---|---|---|---|---|---|
| FR-1 | | UC-1 | P0 | | (C-…) |

Group as: Core capabilities (P0) · Adaptation / learning capabilities · Safety & oversight · Nice-to-have.

### MVP vs nice-to-have
| Capability | MVP | v2 | v3 | Why |
|---|---|---|---|---|

---

## E — Engineering constraints (non-functional)

| ID | Area | Requirement | Target | Rationale | Source |
|---|---|---|---|---|---|
| NFR-1 | Latency | | p95 … | | |
| NFR-2 | Quality | | task success ≥ … | | |
| NFR-3 | Cost | | $… per task | | |
| NFR-4 | Availability | | | | |
| NFR-5 | Security & privacy | | | | |
| NFR-6 | Compliance & audit | | | | |
| NFR-7 | Context / data volume | | | | |

### How these constraints shape the architecture
One bullet per constraint → design consequence.

---

## C — Components

### Architecture overview
| Layer | Component | Responsibility | Realised by (proposed) |
|---|---|---|---|
| Agent | Task planner | decompose tasks, plan | |
| Agent | Execution engine | orchestrate subtasks, retries | |
| Agent | Learning module | adapt from feedback/examples | |
| Intelligence | Foundation model | reasoning & generation | |
| Intelligence | Memory | session, long-term, patterns | |
| Intelligence | Reasoning / confidence | decide act vs ask | |
| Action | Tool integrations | systems it reads/writes | |
| Action | Safety layer | policies, limits, approvals | |
| Action | Feedback loop | capture outcomes & corrections | |

Drop or rename components to fit the archetype.

### Action & tool inventory *(agentic only)*
| Action | Tool / system | Reversible? | Blast radius | Autonomy level | Guardrail | Source |
|---|---|---|---|---|---|---|

### Use case → component map
### Knowledge & memory sources → see Domain Knowledge Pack
### Data flows → see Data Pack

---

## T — Trade-offs

| Decision | Chosen | Rejected alternative | Why | Revisit when | Source |
|---|---|---|---|---|---|
| Autonomy vs control | | | | | |
| Safety vs speed | | | | | |
| Learning mechanism | | | | | |
| Build vs buy | | | | | |

### Evolution path
| Stage | Scope | Autonomy | Learning | Gate to next stage |
|---|---|---|---|---|
| MVP | | L1–L2 | instructions + few-shot | |
| v2 | | | | |
| v3 | | | | |

---

## S — Success metrics

| Type | Metric | Baseline | Target | Measured how | Owner | Linked to |
|---|---|---|---|---|---|---|
| North star | | | | | | BO-…, FR-… |
| Quality | | | | | | |
| Safety / guardrail | | | 0 | | | |
| Adoption / trust | | | | | | |
| Learning | | | | | | |
| Cost | | | | | | |

### Evaluation plan
- Offline: golden set (see Data Pack §Evaluation), pass bar before launch.
- Online: sampling rate, human review cadence, drift alerts.
- Guardrails: kill switch, rollback, escalation SLAs.

---

## Risks & open items
## Consistency check
## Traceability matrix (FR/NFR → ledger IDs → BR IDs)
