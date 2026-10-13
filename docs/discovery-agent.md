# Discovery Agent — Worked Example

A small, real Claude Code plugin in this repo that applies the exam concepts end to end:
a **requirements & discovery agent** that turns client documents and conversations into a
BRD, a S.P.E.C.T.S. PRD, a Domain Knowledge Pack and a Data Pack.

Source: [`discovery-agent/`](https://github.com/amribhatt/claude-certified-architect-guide/tree/main/discovery-agent)

!!! info "Install"
    ```text
    /plugin marketplace add amribhatt/claude-certified-architect-guide
    /plugin install discovery-agent@architect-guide-plugins
    /discovery-agent:discover ./client-docs "Project name"
    ```

## What it does

| Phase | Mode | What happens |
|---|---|---|
| 1. Ingest | autonomous | Reads docs, transcripts, decks; splits into atomic, quoted claims in `discovery/ledger.md` |
| 2. Classify | autonomous | Scores Perceive / Decide / Act / Learn / Adapt → traditional, predictive, generative, agentic or hybrid; loads matching question modules |
| 3. Grill | interactive | One question at a time, each with a recommended answer, sentence by sentence, in S.P.E.C.T.S. order |
| 4. Playback | interactive | "So we're building…", assumptions, non-goals, autonomy contract, success sentence → explicit sign-off |
| 5. Generate | autonomous | BRD, PRD, Domain Knowledge Pack, Data Pack — every line traced to a ledger ID |

## S.P.E.C.T.S. in one table

| Step | Question it answers | Exit criterion |
|---|---|---|
| **S**cope | What problem, for whom, how autonomous, how adaptive, what scale? | Measurable success sentence + non-goals confirmed |
| **P**roduct requirements | Which users, which use cases, what's P0? | 2–5 use cases walked incl. failure & escalation paths |
| **E**ngineering constraints | How fast, how accurate, how cheap, how safe? | Every NFR has a number or "not a constraint" |
| **C**omponents | What parts, what tools, what memory? | Every action → tool + autonomy level + guardrail |
| **T**rade-offs | What did we reject and why? How does it evolve? | MVP → v2 → v3 with promotion gates |
| **S**uccess metrics | How do we know it works and stays safe? | Baseline, target, method, owner per metric |

## Autonomy per action, not per system

| | Small impact | Large impact |
|---|---|---|
| **Easily reversible** | L3–L4 act (and notify) | L2–L3 |
| **Hard / irreversible** | L2 act with approval | L1–L2 (MVP: never above L2) |

## How it maps to the exam domains

??? note "Agent Skills (Domain 5)"
    Three skills with `name`/`description` frontmatter so Claude auto-invokes them;
    `argument-hint` and `$ARGUMENTS` for slash-command use; **progressive disclosure** —
    the agentic and industry lenses are separate reference files loaded only when needed.

??? note "Subagents & context management (Domains 6, 10)"
    `source-extractor` is a read-only subagent dispatched once per source **in parallel**.
    Raw documents stay in the subagent's context; only structured claims return. The ledger
    is durable external state, so a long engagement survives `/compact` and new sessions.

??? note "Agentic patterns & workflow design (Domains 7, 8)"
    A fixed workflow (ingest → classify → grill → playback → generate) with an adaptive
    step inside it: question selection depends on archetype, industry, what the sources
    already answer, and impact × uncertainty. Human-in-the-loop gates at playback sign-off.

??? note "Prompt engineering & structured output (Domain 9)"
    Fixed output schemas (ledger table, extractor markdown, four templates), explicit
    status vocabulary, few-shot style "recommended answer" questions, and a rule that
    outputs may only contain ledger-backed facts — reducing hallucinated requirements.

!!! warning "Anti-patterns it calls out during discovery"
    Train → deploy → done · no safety mechanisms · over-promised capability ·
    no feedback/learning loop · no human oversight in the MVP.
