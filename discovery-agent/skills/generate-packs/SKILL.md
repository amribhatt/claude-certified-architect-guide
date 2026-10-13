---
name: generate-packs
description: Generate the discovery deliverables — BRD, S.P.E.C.T.S. PRD, Domain Knowledge Pack and Data Pack — from a discovery/ledger.md and playback.md. Use after discovery is played back and signed off, or when the user asks to (re)generate any of these documents.
argument-hint: "[all | brd | prd | dkp | data] (default: all)"
---

# Generate Packs

Inputs: `discovery/context.md`, `discovery/ledger.md`, `discovery/playback.md`.
If the ledger is missing, stop and suggest running `discover` first.
If `playback.md` isn't signed off, warn and continue only if the user agrees; mark every
output **DRAFT — not played back**.

Write to `discovery/out/` using the templates:

| Output | Template | Audience | Purpose |
|---|---|---|---|
| `BRD.md` | [templates/brd.md](templates/brd.md) | sponsor, business owners | *why* and *what* in business terms; sign-off document |
| `PRD.md` | [templates/prd-spects.md](templates/prd-spects.md) | product, architects, engineering | *what* and *how well*, structured by S.P.E.C.T.S. |
| `domain-knowledge-pack.md` | [templates/domain-knowledge-pack.md](templates/domain-knowledge-pack.md) | the agent itself (RAG / system prompt / few-shot) + new team members | the domain, in a form an AI can use |
| `data-pack.md` | [templates/data-pack.md](templates/data-pack.md) | data/platform engineers, security | sources, tools/actions, permissions, evals, feedback signals |

## Rules

1. **Traceability is mandatory.** Every requirement, rule, metric, data source and tool
   cites ledger IDs, e.g. `(C-012, C-031)`. Nothing appears that isn't in the ledger. If
   a template section has no ledger support, write `Not discussed — see open items` rather
   than inventing content.
2. **Status shows through.** 🟡 assumed items are visibly marked in every output; ❓ open
   items are collected in each document's *Open items* table with owner and due date.
3. **Drop irrelevant sections.** If the archetype is not agentic, remove the autonomy,
   learning-loop and tool-permission sections rather than filling them with filler — but
   keep a one-line note saying why they were dropped.
4. **Same facts, different altitude.** The BRD speaks business outcomes; the PRD speaks
   capabilities and NFRs; the packs are reference data. Don't copy-paste prose between them.
5. **Domain Knowledge Pack is machine-first.** Short, declarative, one fact per bullet,
   consistent headings — it will be chunked for retrieval or pasted into a system prompt.
   Use the client's own words for terms and examples.
6. **Data Pack never contains real sensitive values** — describe fields and
   classifications, not records. Use synthetic or redacted example rows.
7. After writing, run a **consistency pass**: every P0 requirement has a success metric;
   every action has a tool + autonomy level + guardrail; every use case has ≥ 1 eval seed;
   every glossary term used in the BRD is defined. List any gaps found at the end of the
   PRD under *Consistency check*.

Finish with a 5-line summary in chat: files written, counts, top gaps, next step.
