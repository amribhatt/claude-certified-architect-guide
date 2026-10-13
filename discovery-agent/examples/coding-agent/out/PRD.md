# Product Requirements Document — AI Coding Agent
*Structured with the S.P.E.C.T.S. framework · archetype: Agentic (supervised) · status: Approved 2026-10-13*
*Illustrative example: numbers are worked defaults, marked 🟡 where assumed.*

---

## S — Scope

### I) Clarifying questions (resolved)
| Dimension | Question | Answer | Source |
|---|---|---|---|
| Task domain | Narrow or general? Vertical or horizontal? | Narrow vertical: software engineering — write, debug, review code | C-001–C-004 |
| Autonomy | Fully autonomous or human-in-the-loop? Act without approval? | Human-in-the-loop: propose → approve → execute (L2); no prod deploy rights | C-005, C-010 |
| Adaptation | Same domain or new domains? Few-shot or zero-shot? | New frameworks/patterns within software; few-shot (3–5 examples) within 2 days | C-008, C-009 |
| Scale & users | How many? Tenancy? Enterprise or consumer? | 10K devs → 100K; multi-tenant enterprise SaaS | C-006, C-007 🟡 |

### II) Restated problem
> "So we're building an **AI coding agent for software development teams** that can:
> - Execute coding tasks (implement features, debug, code review)
> - Adapt to new frameworks and patterns with 3–5 examples
> - Operate with human oversight (propose → approve → execute workflow)
> - Start with 10K developers, plan for 100K
> - Safety-first: production deployments require explicit human action"

### III) Assumptions ✅ · Non-goals ❌
✅ Access to code repositories (GitHub, GitLab) · ✅ Integration with IDEs and CI/CD ·
✅ Access to foundation LLMs under an enterprise data agreement

❌ Not replacing developers (augmentation only) · ❌ No infrastructure/DevOps initially ·
❌ No autonomous production deployment · ❌ No approving/merging PRs

### IV) Definition of success
> "Success means the agent takes a scoped coding task and produces a PR that **passes tests
> and is accepted with minor edits ≥ 60%** of the time, learns a new framework from **≤ 5
> examples within 2 days**, and cuts **time-to-PR on those tasks by 40%** 🟡 — with **zero
> unapproved production changes**."

> ⚠️ *Discovery note:* the original sentence ("take a chat prompt, retrieve answers,
> generate visualisation on the fly … reduce users' time by 80%") described a different
> product and an unbenchmarked target. Grilled and replaced (Q-01, Q-06).

---

## P — Product requirements

### I) User segments
| Segment | Type | Needs | Trust signal they need |
|---|---|---|---|
| Software developers (ICs) | Primary | offload well-scoped tasks, fast debugging | readable plan, small diffs, green tests |
| Engineering managers | Primary | assign tasks to the agent, see throughput | queue view, acceptance-rate dashboard |
| QA engineers | Secondary | validate agent output | test evidence attached to every PR |
| Tech leads | Secondary | teach team patterns, control quality | pattern review, override history |

### II) Core use cases
**UC-1 Autonomous task execution** — developer describes task ("Add rate limiting to the
API") → agent analyses codebase → creates plan (subtasks, files, risks) → *developer
approves plan* → implements across files on an agent branch → runs tests and lint → *developer
reviews diff and approves* → agent commits and opens PR with description and test evidence.

**UC-2 Learning new patterns** — agent meets an unfamiliar framework → asks for or is given
3–5 example implementations → extracts a *pattern card* (when to use, structure, do/don't,
examples) → *tech lead approves card* → stored in team pattern memory → applied and cited in
current and future tasks.

**UC-3 Self-correction** — implementation done → tests fail → agent analyses failure,
hypothesises fix → iterates up to **3 attempts** (or $2 budget) → if still failing,
escalates with diagnosis, attempts tried and partial diff.

**UC-4 Code review** *(added in discovery — "review" was in scope but had no use case)* —
PR opened → agent reviews against team patterns, tests and security checks → posts
comments with severity → never approves or merges.

**UC-5 Debug from a report** — bug report / stack trace / failing CI run → agent
reproduces in sandbox → proposes root cause + fix → continues as UC-1 from plan approval.

Failure / unknown / escalation paths: low-confidence plan → ask clarifying question; unknown
framework → trigger UC-2; budget or attempts exhausted → escalate (UC-3).

### III) Functional requirements — MVP

**Core capabilities (P0 — must have)**
| ID | Requirement | Use case | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-1 | Accept tasks from chat, issue link or IDE; ask clarifying questions when ambiguous | UC-1, UC-5 | ambiguous tasks get ≤ 2 questions before planning | C-002 |
| FR-2 | Understand the codebase via a code index (symbols, dependencies, conventions) | all | relevant files retrieved for ≥ 90% of golden-set tasks | C-014 |
| FR-3 | Produce an execution plan: subtasks, files touched, risks, test strategy | UC-1 | plan shown before any write; developer can edit/approve/reject | C-005 |
| FR-4 | Implement multi-file changes on an isolated agent branch | UC-1 | no writes outside agent branch | C-002 |
| FR-5 | Run tests, lint and type checks in a sandbox; attach results | UC-1, UC-3 | every PR includes test evidence | C-002 |
| FR-6 | Self-correct up to 3 attempts / $2, then escalate with diagnosis | UC-3 | escalation contains failing output, hypotheses, attempts | C-018, C-015 |
| FR-7 | Approval gates: plan approval and diff approval before commit/PR | UC-1 | 0 commits without approval | C-005 |
| FR-8 | Open PR with description, linked task and test evidence | UC-1 | PR template filled | C-002 |
| FR-9 | Review PRs and post severity-tagged comments | UC-4 | cannot approve/merge | C-004 |
| FR-10 | Debug from stack trace / failing CI and propose root cause | UC-5 | reproduction step shown | C-003 |
| FR-11 | Full audit trail of perceive → plan → act → outcome | all | trace retrievable per task | C-010 |

**Adaptation capabilities (P0 — must have)**
| ID | Requirement | Use case | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-12 | Learn a pattern from 3–5 examples into a reviewable pattern card | UC-2 | card produced in < 10 min | C-009 |
| FR-13 | Tech-lead approval before a pattern becomes active | UC-2 | unapproved cards never used | C-019 |
| FR-14 | Retrieve and apply relevant patterns; cite which ones were used | UC-1, UC-2 | citation in plan and PR | C-009 |
| FR-15 | Capture feedback: plan edits, diff edits, rejections, review outcomes | all | ≥ 95% of tasks have an outcome label | C-019 |
| FR-16 | Scope memory per org/team/repo; no cross-tenant learning | all | isolation test passes | C-006 |

### IV) MVP vs nice-to-have
| Capability | MVP | v2 | v3 | Why |
|---|---|---|---|---|
| Plan → approve → implement → test → PR | ✅ | | | core value loop |
| Self-correction (3 attempts) | ✅ | | | reduces escalations cheaply |
| PR review comments | ✅ | | | high value, read-mostly, low risk |
| Few-shot pattern learning with review | ✅ | | | the adaptation promise |
| Feedback capture | ✅ | | | needed for learning *and* metrics |
| EM task queue & dashboard | | ✅ | | needs usage data first |
| Auto-propose patterns mined from repo history | | ✅ | | after manual patterns prove useful |
| Skip plan approval for low-risk small tasks (L3) | | ✅ | | gated on acceptance data |
| Auto-merge of trivial PRs (docs, lint) | | | ✅ | needs months of trust evidence |
| Infra/DevOps tasks | | | ✅ | non-goal for MVP |
| Org-specific fine-tuning | | | ✅ | only if few-shot + RAG plateau |

**Why this prioritisation:** supervised autonomy — human oversight builds trust, learning
from corrections improves the agent, and starting narrow ensures quality.

---

## E — Engineering constraints

### Model performance requirements
| ID | Metric | MVP target | v2 target | Measured how | Source |
|---|---|---|---|---|---|
| NFR-1 | PR acceptance (merged with ≤ minor edits) | ≥ 60% | ≥ 75% | PR outcome + edit size | playback |
| NFR-1b | Tests green when handed to human | ≥ 85% | ≥ 92% | sandbox results | FR-5 |
| NFR-2 | Plan latency (p95) | < 60 s | < 30 s | trace timings | 🟡 |
| NFR-2b | End-to-end task time (p50, standard task) | < 15 min | < 8 min | trace timings | 🟡 |
| NFR-3 | New framework proficiency | ≥ 70% acceptance after ≤ 5 examples in ≤ 2 days | ≤ 3 examples | per-pattern acceptance | C-008, C-009 |
| NFR-4 | Hallucinated APIs / non-existent symbols in diffs | < 2% of PRs | < 1% | compile/type check + review tags | 🟡 |
| NFR-4b | Review comment precision (accepted as valid) | ≥ 70% | ≥ 80% | developer reactions | 🟡 |

### Safety & reliability
| ID | Requirement | Target | Enforced where | Source |
|---|---|---|---|---|
| NFR-5 | No production deploy, merge or protected-branch push by the agent | 0 events | **infra**: agent token lacks those permissions | C-010, C-004 |
| NFR-5b | No commit without explicit developer approval | 0 events | execution engine state machine + audit | C-005 |
| NFR-6 | Self-correction budget | 3 attempts or $2 per task | execution engine | C-018, C-015 |
| NFR-7 | Availability | 99.5% business hours; degrade to suggest-only if sandboxes unavailable | platform | 🟡 |
| NFR-8 | Sandbox isolation | ephemeral container, no network except allow-listed package mirrors | infra | C-020 |
| NFR-8b | Secrets | secret scan on every diff; secrets never in prompts or logs | safety layer | 🟡 |
| NFR-8c | Tenant isolation | separate indexes and memory per org; no cross-org training | data layer | C-006 |
| NFR-8d | Prompt injection | repo/issue text is task content, never policy; tool allow-list per step | safety layer | C-020 |
| NFR-9 | Audit trail | full trace per task, retained 1 year | observability | 🟡 |

### Computational resources
| Resource | Requirement | Sizing: 10K devs → 100K devs | Source |
|---|---|---|---|
| Model inference | 32K–128K-token context; retrieval keeps prompts ≤ ~64K | ~5 tasks/dev/day → 50K → 500K tasks/day 🟡 | C-014 |
| Cost per task | $0.10–$1.00 target, $2.00 hard stop | ~$15K/day at $0.30 avg → ~$150K/day; requires routing + caching | C-015 |
| Memory | vector DB (code + pattern embeddings) + structured pattern-card store | one index per repo; pattern cards per team | C-016 |
| Sandboxes | ephemeral containers for tests | ~1.4 tasks/s peak-hour avg × ~10 min ≈ 800 concurrent → ~8K at 100K | 🟡 |

### How these constraints shape the architecture
- **Repos exceed 128K tokens** → a code index + retrieval layer, not "whole repo in prompt".
- **$0.10–$1.00 per task at 500K tasks/day** → model routing (small model for retrieval,
  lint fixes and summaries; large model for planning and hard edits), prompt caching of
  repo context and patterns, hard per-task budget.
- **"No prod deploy" is safety-critical** → enforced by missing credentials and branch
  protection, not by instructions in the prompt.
- **Propose → approve → execute** → the execution engine is an explicit state machine with
  approval states, not a free-running loop.
- **Few-shot adaptation in days** → pattern memory (retrieval + reviewed cards) rather than
  fine-tuning; fine-tuning only as a v3 option.
- **Multi-tenant at 100K devs** → per-org isolation of indexes, memory and logs; horizontal
  sandbox pool with per-org quotas.
- **Untrusted repo content** → sandboxed execution and a per-step tool allow-list.

---

## C — Components

### The 9 core components
| Layer | Component | Responsibility | Realised by (proposed) | Serves |
|---|---|---|---|---|
| Agent | 1. Task Planner | decompose task, produce plan with files, risks, tests | large model + planning prompt + retrieved context | FR-1, FR-3 |
| Agent | 2. Execution Engine | approval state machine, subtask orchestration, retries, budgets | workflow service | FR-4–FR-7, NFR-6 |
| Agent | 3. Learning Module | extract pattern cards, route for review, write to memory | small-model pipeline + review UI | FR-12, FR-13 |
| Intelligence | 4. Foundation Model | reasoning and code generation | Claude (routing across sizes) | all |
| Intelligence | 5. Memory System | session context, code index, pattern cards, task history | vector DB + relational store, per org | FR-2, FR-14, FR-16 |
| Intelligence | 6. Reasoning Engine | confidence scoring: act vs ask vs escalate | heuristics + model self-assessment + test signals | FR-1, FR-6 |
| Action | 7. Tool Integration | Git, CI, test runner, IDE, issue tracker | GitHub/GitLab app, sandbox runner, IDE plugin | FR-4, FR-5, FR-8–FR-10 |
| Action | 8. Safety Layer | permissions, secret scan, injection guard, policy checks | policy service + scoped tokens | NFR-5, NFR-8 |
| Action | 9. Feedback Loop | capture approvals, edits, rejections, PR outcomes | event pipeline → metrics + learning | FR-15, §S |

### Action & tool inventory
| Action | Tool | Reversible? | Blast radius | Autonomy | Guardrail |
|---|---|---|---|---|---|
| Read repo / issues | Git app | n/a | none | L4 | org-scoped token |
| Run tests | sandbox | yes | none | L4 | no network, time limit |
| Create agent branch | Git app | yes | small | L3 | `agent/*` prefix only |
| Apply plan / push commits | Git app | yes | small | L2 | approval required |
| Open PR | Git app | yes | small | L2 | approval required |
| Post review comments | Git app | yes | small | L3 | cannot approve |
| Merge / deploy / edit CI / secrets | — | no | large | **never** | no permission granted |

---

## T — Trade-offs

| Decision | Chosen | Rejected alternative | Why | Revisit when |
|---|---|---|---|---|
| Autonomy vs control | L2: two approval gates | L3 auto-commit | trust not yet earned; errors in shared repos are costly | acceptance ≥ 85% over 1,000 tasks for a task class |
| Safety vs speed | approval gates + sandbox | direct execution in dev env | gates add ~minutes, prevent incidents | skip plan approval for small low-risk tasks in v2 |
| Learning mechanism | few-shot pattern cards + RAG | fine-tuning per org | cheap, reversible, reviewable, works in days | few-shot plateaus with ≥ 10K labelled examples |
| Single vs multi-agent | one agent, role-specific prompts (plan, implement, review) | multi-agent swarm | simpler to debug and audit | review quality suffers from shared context |
| Context strategy | retrieval over code index | long-context only | cost and repo size | context costs fall 10× |
| Build vs buy | build orchestration on a foundation model API | adopt off-the-shelf agent | need approval gates, tenant isolation, pattern review | market product meets those |

### Evolution path
| Stage | Scope | Autonomy | Learning | Gate to next stage |
|---|---|---|---|---|
| MVP (pilot 500 devs → 10K) | UC-1–UC-5, top 3 languages | L2 everywhere writes happen | reviewed pattern cards | ≥ 60% acceptance, 0 safety incidents for 8 weeks |
| v2 (→ 50K) | EM queue, mined patterns, more languages | L3 for small low-risk tasks | corrections auto-proposed as cards | ≥ 75% acceptance; override rate falling |
| v3 (→ 100K) | trivial auto-merge, DevOps tasks | L3–L4 for narrow classes | optional fine-tuning | per-class trust evidence; security sign-off |

---

## S — Success metrics

| Type | Metric | Baseline | Target (MVP) | Measured how | Owner |
|---|---|---|---|---|---|
| North star | Time-to-PR on in-scope tasks | pilot measurement (manual) | −40% 🟡 | issue → PR timestamps vs matched human tasks | VP Eng |
| Quality | PR acceptance with ≤ minor edits | n/a | ≥ 60% | PR outcome + diff of human edits | Eng Productivity |
| Quality | Tests green at hand-off | n/a | ≥ 85% | sandbox results | Eng Productivity |
| Safety | Unapproved commits / prod changes | — | **0** | audit log | Security |
| Safety | Escalation rate | — | 10–25% (too low = overconfident) | execution engine events | Eng Productivity |
| Safety | Secrets caught in agent diffs | — | 100% blocked | secret scanner | Security |
| Adoption | Weekly active developers | 0 | ≥ 40% of enabled devs | product analytics | PM |
| Adoption | Tasks delegated per active dev / week | 0 | ≥ 3 | product analytics | PM |
| Learning | Examples → 70% acceptance on new framework | — | ≤ 5 examples, ≤ 2 days | per-pattern acceptance | Tech leads |
| Cost | $ per accepted PR | — | ≤ $1.50 | billing ÷ accepted PRs | Platform |

### Evaluation plan
- **Offline:** golden set of ≥ 200 real historical tasks (20+ per use case and language),
  including failing-test, unknown-framework and prompt-injection cases; launch bar = NFR-1 and
  NFR-4 targets met.
- **Online:** 5% of agent PRs sampled weekly for expert review; drift alert if acceptance drops
  > 5 points week over week.
- **Guardrails:** kill switch per org and global (Security + VP Eng); rollback = close agent PRs
  and revert agent branches; escalation SLA 1 business day.

---

## Risks & open items
| Item | Type | Owner | Due |
|---|---|---|---|
| C-013 time-saving target needs pilot baseline | 🟡 | VP Eng | pilot week 6 |
| C-007 timeline to 100K | 🟡 | Platform lead | Q2 |
| Retrieval quality on large legacy monorepos | risk | Eng Productivity | pilot |
| Learning bad patterns from corrections | risk | Tech leads | mitigated by FR-13 |

## Consistency check
- ✅ Every P0 FR maps to a component and has an acceptance criterion.
- ✅ Every write action has a tool, autonomy level and guardrail.
- ✅ Every use case is covered by the golden set.
- ⚠️ NFR-2/NFR-4 targets are assumed 🟡 — confirm after offline eval.
