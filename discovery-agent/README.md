# Discovery Agent — a Claude Code plugin

A lightweight, industry-agnostic **requirements & discovery agent**. Give it whatever the
client has — docs, call transcripts, decks, emails, notes — and it will:

1. **Ingest** everything into atomic, quoted, traceable claims (in parallel, via a subagent).
2. **Classify** the system: traditional, predictive, generative, **agentic** or hybrid —
   scoring Perceive / Decide / Act / Learn / Adapt — and load only the question modules
   that matter (agentic lens, industry lens).
3. **Grill** the business user sentence by sentence, *one question at a time, always with a
   recommended answer* (in the spirit of Matt Pocock's `grill-me`), walking the
   **S.P.E.C.T.S.** framework in dependency order.
4. **Play back** the scope ("So we're building…", assumptions, non-goals, autonomy
   contract, success sentence) and get explicit sign-off.
5. **Generate** four deliverables, every line traced back to a ledger claim:

| Output | For | Contains |
|---|---|---|
| `BRD.md` | sponsor & business owners | objectives, scope, process, business rules, risks, sign-off |
| `PRD.md` | product & engineering | S.P.E.C.T.S.: scope, requirements, NFRs, components, trade-offs, metrics |
| `domain-knowledge-pack.md` | the agent being built (RAG / prompt / few-shot) + new joiners | glossary, rules, heuristics, edge cases, worked examples, autonomy contract |
| `data-pack.md` | data, platform & security | sources, entities, tools & actions with autonomy levels, feedback signals, eval seeds |

## Install

```text
/plugin marketplace add amribhatt/claude-certified-architect-guide
/plugin install discovery-agent@architect-guide-plugins
```

Or load locally while iterating:

```bash
claude --plugin-dir ./discovery-agent
```

## Use

```text
/discovery-agent:discover ./client-docs "Claims Triage Agent"
```

Other entry points:

| Skill | When |
|---|---|
| `/discovery-agent:discover` | full engagement: ingest → classify → grill → playback → generate (resumable) |
| `/discovery-agent:grill` | grill any single statement, requirement or doc — no workspace needed |
| `/discovery-agent:generate-packs [all\|brd\|prd\|dkp\|data]` | (re)generate outputs from the ledger |

Claude also picks these skills automatically when you say things like *"grill me on this
vision"* or *"help me scope this project and write a BRD"*.

While being grilled you can always answer: **yes** (accept recommendation) · **no,
because…** · **your call** (record as assumption) · **park** (open item) ·
**fast-forward** (accept all recommendations for this section).

## Workspace

```
discovery/
├── sources/      # what the client gave you
├── context.md    # archetype scores, industry lens, stakeholders, source inventory
├── ledger.md     # every atomic claim: ✅ confirmed · 🟡 assumed · ❓ open · ⚠️ conflict · ❌ non-goal
├── playback.md   # the signed-off restatement
└── out/          # BRD.md · PRD.md · domain-knowledge-pack.md · data-pack.md
```

The ledger is the single source of truth: stop any time, come back next week, and
`/discovery-agent:discover` resumes from the first open item.

## Design choices

- **Simple:** markdown skills + one read-only subagent. No servers, no databases, no code.
- **Progressive disclosure:** the agentic and industry lenses load only when the
  classification says they're needed, keeping context small.
- **Context isolation:** long or numerous sources are read by `source-extractor`
  subagents in parallel; only structured claims return to the main conversation.
- **Adaptive questioning:** the question bank is a menu; what gets asked depends on the
  archetype, the industry, what the sources already answer and impact × uncertainty.
- **Safety by default for agentic systems:** per-action autonomy levels (L0–L4) set by
  reversibility × blast radius, mandatory guardrails, kill switch and feedback loop —
  and it calls out the classic mistakes (train→deploy→done, no oversight, over-promising,
  no learning loop).

## Layout

```
discovery-agent/
├── .claude-plugin/plugin.json
├── agents/source-extractor.md
├── skills/
│   ├── discover/SKILL.md
│   │   └── references/{spects-question-bank,agentic-lens,industry-lenses}.md
│   ├── grill/SKILL.md
│   └── generate-packs/SKILL.md
│       └── templates/{brd,prd-spects,domain-knowledge-pack,data-pack}.md
└── examples/
    ├── sample-session.md          # abridged grilling transcript (insurance)
    └── coding-agent/              # full worked S.P.E.C.T.S. run: brief → ledger → playback → PRD
```
