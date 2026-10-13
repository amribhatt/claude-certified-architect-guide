# Agentic Lens

Load when the system perceives, decides, acts, learns or adapts. Agentic systems are not
static software, not just prediction, not just content generation: they pursue goals,
take actions and improve from experience. You are scoping an **autonomous collaborator
that operates alongside users**, not a tool users operate — so discovery must cover
autonomy, safety, control and learning explicitly.

## The five characteristics — probe each

| Characteristic | What to pin down | Question to ask |
|---|---|---|
| **Goal-oriented** | the objective and its stopping condition | "When is a task *done*? How would it know?" |
| **Autonomous** | decisions it makes without a human | "Which decisions are you comfortable it makes alone today?" |
| **Adaptive** | new situations/tasks it must handle | "What's the last new kind of request your team had to learn? How long did it take?" |
| **Action-taking** | systems it changes | "List every system it would need to *change*, not just read." |
| **Self-improving** | the feedback signal and loop | "When it gets something wrong, who notices, and how does it find out?" |

## Perceive → Decide → Act → Learn → Adapt — map the loop

For each core use case, fill this mini-table in the ledger:

| Stage | Question |
|---|---|
| Perceive | What inputs (text, docs, events, screens)? How messy? What does it need to know about the environment (user, account, history)? |
| Decide | What choices does it make? What's the confidence threshold to act vs ask? |
| Act | Which tools/APIs? Reversible? Blast radius? |
| Learn | Which outcome signals (approval, edit, rating, downstream result)? Stored where? |
| Adapt | How does it handle a never-seen case: ask, escalate, try with examples? |

## Autonomy ladder — set it *per action*, not per system

| Level | Name | Behaviour |
|---|---|---|
| L0 | Inform | Answers / summarises only |
| L1 | Suggest | Proposes an action; a human performs it |
| L2 | Act with approval | Prepares the action; executes after explicit approval |
| L3 | Act and notify | Executes within limits; human can review/undo |
| L4 | Autonomous within bounds | Executes and self-corrects; humans audit samples |

Place each action using **reversibility × blast radius**:

|  | Small impact | Large impact |
|---|---|---|
| **Easily reversible** | L3–L4 | L2–L3 |
| **Hard / irreversible** | L2 | L1–L2 (MVP: never above L2) |

Recommend starting the MVP at **L1–L2** (supervised autonomy) and agree the evidence
that would promote an action one level (e.g. "≥ 98% approval rate over 500 tasks with zero
severity-1 errors").

## Learning mechanisms — recommend the cheapest that works

| Mechanism | Use when | Data needed | Risk |
|---|---|---|---|
| Instructions / system prompt | rules are known and stable | written policies | low |
| Few-shot examples | patterns are easier to show than tell (3–5 examples) | curated examples | low |
| RAG over knowledge | facts change, large corpus, need citations | docs + metadata, access controls | medium (stale/wrong docs) |
| Memory of corrections | team-specific conventions emerge over time | approved corrections | medium (learning bad habits) |
| Fine-tuning | stable task, thousands of labelled examples, persistent gap | labelled dataset | high (cost, drift, re-validation) |

Ask: *"Who is allowed to teach it, and who reviews what it learned?"*

## Safety & control — must be in every agentic MVP

- **Guardrails:** allow-list of tools and actions; hard limits (amounts, records, rate).
- **Approval gates:** which actions, which approver, timeout behaviour.
- **Self-correction budget:** max retries (e.g. 3) before escalating to a human.
- **Confidence & uncertainty:** when it must say "I'm not sure" and ask.
- **Observability:** full trace of perceive → decide → act; audit log retention.
- **Kill switch & rollback:** who can stop it, how fast, how actions are undone.
- **Data boundaries:** what it may read/write per user/tenant; prompt-injection exposure
  from untrusted inputs (emails, web pages, uploaded docs).
- **Evaluation:** offline golden set before launch; online sampling and drift checks after.

## Anti-patterns — call them out when you hear them

| You hear | Anti-pattern | Ask |
|---|---|---|
| "We train it once and launch" | treating it like traditional ML (train → deploy → done) | "How does it get better after week one, and how do we know it isn't getting worse?" |
| "It'll just handle it" | ignoring safety mechanisms | "What's the worst thing it could do here? What stops it?" |
| "It'll do everything the team does" | over-promising capabilities | "Which single task, done reliably, would be worth it on its own?" |
| No mention of corrections/ratings | missing the feedback/learning loop | "When a user fixes its output, where does that fix go?" |
| "Fully autonomous from day one" | no human oversight in the MVP | "What would you need to see before you'd let it act alone?" |

## Real-world analogues — use to make questions concrete

Use the closest analogue to ground a question ("Like a support agent that can process a
refund but escalates disputes — where's your equivalent line?"):

- **Coding agents** (Copilot Workspace, Devin, Cursor): issue → plan across files → code
  → run tests → PR → adapts to codebase style.
- **Customer service agents** (Intercom, Zendesk): intent → knowledge search → action
  (refund, order update, callback) → escalate → learn from resolutions.
- **Research agents** (Perplexity, Claude with tools): question → search/read → synthesise
  → cite + state uncertainty → adapt search strategy.
