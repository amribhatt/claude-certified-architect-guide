# S.P.E.C.T.S. Question Bank

A menu, not a script. Pick the questions the sources leave open, in dependency order,
highest impact first. Rephrase into the client's vocabulary. Each section lists what you
must walk away with.

---

## S — Scope: clarify the problem and context

**Walk away with:** problem statement, who hurts today and how much, task domain,
autonomy level, adaptation scope, scale, in/out of scope, assumptions, non-goals, one
measurable success sentence.

**Problem & value**
- What happens today, step by step? Who does it, how long does it take, what does it cost?
- What's the most painful moment in that process? Give me last week's worst example.
- If we do nothing, what happens in 12 months?
- Why now?

**Task domain**
- What kinds of tasks should it handle? Narrow domain or general purpose?
- One vertical (e.g. claims, support, coding, research) or horizontal across teams?
- Which tasks are explicitly *out*?

**Autonomy level** *(see agentic-lens.md for the L0–L4 ladder)*
- Fully autonomous or human-in-the-loop?
- Can it take actions without approval, or suggest and wait?
- What must it never do, even if asked?

**Adaptation scope**
- New tasks in the same domain, or completely new domains?
- Few-shot (learns from a handful of examples) or zero-shot (instructions only)?
- How fast must it pick up something new — minutes, days, a release cycle?

**Scale & users**
- How many users at launch, in 12 months? Single-tenant or multi-tenant?
- Enterprise, internal, or consumer? Which geographies / languages?

**Close Scope in four steps — always in this order, each confirmed by the user:**
1. *Clarify* — the questions above (only those the sources leave open).
2. *Restate* — "So we're building {one sentence} that can: …" (3–6 bullets).
3. *Assumptions ✅ and non-goals ❌* — explicit lists.
4. *Define success* — one measurable sentence. Check it against the restated scope:
   a success sentence that mentions capabilities not in scope (copy-paste from another
   project is common) or an unbenchmarked number ("reduce time by 80%") is a ⚠️ — grill it.

---

## P — Product requirements: what to build

**Walk away with:** user segments (primary/secondary), 2–5 core use cases walked end to
end, functional requirements prioritised P0/P1/P2, MVP vs nice-to-have line.

**Users**
- Who uses it daily? Who assigns work to it? Who checks its output? Who teaches it?
- What does each of them need to *see* to trust it?

**Use cases** — for each, get a real example and walk:
1. Trigger — what starts it?
2. Understand — what context does it need, from where?
3. Plan — what sub-steps?
4. Act — what does it change, in which system?
5. Validate — how does it (or a person) know it worked?
6. Approve / escalate — who, when, through what screen/channel?
7. Learn — what is captured for next time?

Always also walk: **the failure path** (it's wrong), **the unknown path** (it's never seen
this), and **the escalation path** (it gives up — after how many attempts?).

**Prioritisation**
- If we could ship only three capabilities in 90 days, which three?
- What would make a user stop using it in week one?
- Classic split to propose: P0 = supervised core loop + safety + feedback capture;
  P1 = learning from corrections, more tools; P2 = higher autonomy, new domains.

---

## E — Engineering constraints: non-functional requirements

**Walk away with:** a number or an explicit "not a constraint" for each row.

| Area | Ask |
|---|---|
| Latency | Interactive (seconds) or background (minutes/hours)? p95 target? |
| Quality | What accuracy / task-success rate is acceptable to launch? What's the human baseline? |
| Cost | Acceptable cost per task / per user / per month? What does the manual process cost? |
| Availability | Business hours or 24×7? What happens when it's down — fallback to manual? |
| Volume | Tasks per day at launch / peak? Seasonal spikes? |
| Context size | How big are the documents / histories it must reason over? |
| Security | SSO? Role-based access? Can it see everything the user sees, or less? |
| Privacy | PII / PHI / PCI / trade secrets involved? Data residency? Can data go to a third-party model provider? |
| Compliance | Which regulations / audits apply? Need for explainability, audit trail, record retention? |
| Integration | Which systems must it read? Write to? APIs available or screen-scraping only? |
| Model | Any vendor constraints, on-prem requirement, approved model list? |

Then ask: *"Which of these would you trade for which?"* — that feeds T.

---

## C — Components: high-level architecture (validate, don't lecture)

**Walk away with:** each use-case step mapped to a component; each action mapped to a
tool and a permission level; where memory/knowledge comes from.

Propose the reference shape and ask the client to correct it, in their terms:

- **Agent layer** — Task planner · Execution engine · Learning module
- **Intelligence layer** — Foundation model · Memory (session, long-term, patterns) ·
  Reasoning / confidence scoring
- **Action layer** — Tool integrations · Safety layer (policy checks, approvals, limits) ·
  Feedback loop (outcomes, corrections, ratings)

Business-friendly questions:
- Where does it *look things up*? (knowledge sources → RAG / Domain Knowledge Pack)
- What can it *touch*? (systems → tools, each with read/write/approve permissions)
- What does it need to *remember* between tasks? Between users? What must it forget?
- Where does a person *step in*, and what screen/channel do they use?
- What's logged for audit, and who reviews it?

---

## T — Trade-offs: alternatives and evolution

**Walk away with:** for each big decision, the rejected alternative and the reason; an
MVP → v2 → v3 path with the gate to move between them.

Standard trade-offs to put to the client (pick the relevant ones):
- **Autonomy vs control** — more auto-actions = faster, but higher blast radius.
- **Safety vs speed** — approval gates add latency; which actions are worth it?
- **Learning mechanism** — prompt/instructions → few-shot examples → RAG over knowledge →
  fine-tuning. Cheapest and most reversible first; fine-tune only with stable, labelled
  data and a clear gap.
- **Build vs buy** — platform agent vs custom.
- **General vs narrow** — one agent for everything vs specialised agents per task.
- **Single-agent vs multi-agent** — simplicity vs specialisation and parallelism.
- **Cost vs quality** — bigger model vs smaller model + better context.

Evolution path question: *"What would you need to see to let it do more on its own?"*
(the answer becomes the gate from L2 → L3 autonomy).

---

## S — Success metrics: validation, guardrails, outcomes

**Walk away with:** each metric has baseline, target, measurement method, owner.

| Type | Examples |
|---|---|
| North star / business | time saved per task, cost per case, revenue, cycle time, backlog size |
| Quality | task success rate, first-pass acceptance rate, edit distance of human corrections |
| Safety / guardrails | unapproved-action count (target 0), policy violations, escalation rate, false-confidence rate |
| Adoption / trust | weekly active users, % tasks delegated, override rate, CSAT |
| Learning | time to adopt a new task/pattern, examples needed, quality trend over time |
| Cost | $ per task, $ per user, infra $ |

Also ask:
- How will we evaluate before launch? (golden set of real cases → Data Pack eval seeds)
- Who reviews a sample of its work each week, and for how long?
- What's the kill switch, and who can pull it?
