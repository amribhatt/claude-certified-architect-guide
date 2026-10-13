---
name: grill
description: Grill the user relentlessly — one question at a time, with a recommended answer each time — on every sentence of a vision, requirement, transcript or plan until it is unambiguous, quantified and testable. Use standalone on any text ("grill me on this", "poke holes in this requirement") or as Phase 3 of the discover skill.
argument-hint: "[text, file path, or ledger section to grill]"
---

# Grill

Interview the user relentlessly about every sentence until you share one understanding of
it. Walk down each branch of the decision tree, resolving dependencies between decisions
one at a time. If a question can be answered from the sources (or the codebase, or the
ledger), **look it up instead of asking.**

## Per sentence

1. **Restate** it as one or more atomic claims (one actor, one action, one outcome).
2. **Scan** it with the detectors below. Each hit is a candidate question.
3. **Pick the single highest-value question** (biggest design impact × most uncertain).
   Park the rest as 🟡 with your recommended default, or queue them.
4. **Ask** in this shape:

   > **Q-07 · Scope · autonomy**
   > You wrote: *"the agent handles refunds."*
   > Can it issue a refund on its own, or does a person approve first?
   > **My recommendation:** auto-approve ≤ $200 and reversible; human approval above —
   > a wrong large refund is costly and hard to claw back.
   > *(yes · no, because… · your call · park)*

   If the `AskUserQuestion` tool is available, use it: recommended option first and
   labelled "(Recommended)", 2–4 concrete options, free text always allowed.
5. **Record** the answer in the ledger right away. If the answer contains new
   sentences, they get grilled too — but only after the current branch is resolved.

## Detectors

| Detector | Trigger words / smell | Ask |
|---|---|---|
| **Vague quantity** | fast, real-time, scalable, many, most, large, high accuracy | "What number would make you say it's working? What number is a failure?" |
| **Universal** | all, every, always, never, any, fully, end-to-end | "Really all? Which are the exceptions on day one?" |
| **Magic verb** | automatically, intelligently, seamlessly, AI will, learns, understands | "Walk me through what happens step by step the first time it sees a new X." |
| **Missing actor** | passive voice ("is approved", "gets escalated") | "Who exactly — role, not name — and what do they see?" |
| **Missing trigger** | no "when" | "What kicks this off? How often?" |
| **Missing failure path** | happy path only | "What happens when it's wrong / the data is missing / the system is down?" |
| **Solution as requirement** | names a tech ("use a chatbot", "LLM", "dashboard") | "What problem does that solve? Would you accept a different way that solved it better?" |
| **Hidden assumption** | "obviously", "of course", "as usual" | "Is that written down anywhere? Who owns that rule?" |
| **Unbounded autonomy** | "decides", "acts", "handles" with no limits | "What may it do alone, what needs approval, what must it never do?" |
| **No learning loop** | "learns", "improves", "gets smarter" | "From what signal? Who labels it? How do we stop it learning the wrong thing?" |
| **Undefined success** | "better", "improved", "efficient" | "Better than what baseline, measured how, by when?" |
| **Conflict** | contradicts another claim | Quote both. "Which wins, or under what condition?" |
| **Jargon** | client-specific terms, acronyms | "What does X mean here, exactly?" → glossary |

## Discipline

- **One question per turn.** No question lists. No preambles longer than one line.
- **Always give a recommendation.** It turns an essay question into a yes/no and shows the
  user what a good answer looks like.
- **Plain language.** Ask business users about outcomes, situations and examples, not
  architectures. "Give me a real example from last week" is your best tool.
- **Ask for examples aggressively** — 3–5 real cases per core use case. They become the
  few-shot examples and eval seeds in the Domain Knowledge Pack.
- **Escape hatches:** "your call" → record your recommendation as 🟡 Assumed;
  "park" → ❓ Open with an owner; "fast-forward" → accept all remaining recommendations
  in this section as 🟡 and list them so the user can veto.
- **Stop** when every claim in scope is ✅, 🟡 with an owner, or ❌ — and there are no ⚠️.
