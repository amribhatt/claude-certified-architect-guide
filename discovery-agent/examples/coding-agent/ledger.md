# Ledger — AI Coding Agent (abridged)

Archetype: **Agentic (supervised)** — Perceive 2 · Decide 2 · Act 2 · Learn 1 · Adapt 2.
Lenses loaded: agentic, software & engineering teams.

| ID | Claim (atomic) | Source | SPECTS | Status | Resolution / decision |
|----|----------------|--------|--------|--------|-----------------------|
| C-001 | Users are software development teams | brief ¶1 | Sc | ✅ | Vertical: software engineering; not horizontal |
| C-002 | Agent writes code | brief ¶1 | Sc | ✅ | Feature implementation in an existing repo (UC-1) |
| C-003 | Agent debugs | brief ¶1 | Sc | ✅ | From a failing test, stack trace or bug report (UC-3, UC-5) |
| C-004 | Agent reviews code | brief ¶1 | Sc | ✅ | Comments on PRs; cannot approve or merge (UC-4, Q-04) |
| C-005 | Agent suggests and executes after approval | brief ¶1 | Sc | ✅ | Two gates: plan approval, diff approval → L2 (Q-02) |
| C-006 | Launch at 10K developers | brief ¶1 | Sc | ✅ | Multi-tenant enterprise SaaS; ~200 orgs at launch (Q-05) |
| C-007 | Scale to 100K developers | brief ¶1 | E | 🟡 | Within 18 months; owner: platform lead |
| C-008 | Adapts to new frameworks within days | brief ¶1 | Sc | ✅ | ≤ 2 working days from first example to ≥ 70% acceptance |
| C-009 | Adapts using a few examples | brief ¶1 | Sc | ✅ | 3–5 reference implementations, provided by a tech lead (few-shot, not fine-tuning) |
| C-010 | No production deploy without explicit approval | brief ¶1 | E | ✅ | Hard non-goal for MVP: agent credentials have no prod-deploy permission (Q-03) |
| C-011 | Success: "take a chat prompt, retrieve answers, generate visualisation" | brief ¶2 | Sm | ⚠️→✅ | Conflicts with C-001–C-004 (looks copied from an analytics brief). Replaced by success sentence in playback (Q-01) |
| C-012 | Success: "learn new products from < 5 examples" | brief ¶2 | Sm | ✅ | "products" → "frameworks/patterns" (Q-01) |
| C-013 | Success: "reduce users' time by 80%" | brief ¶2 | Sm | 🟡 | No baseline; unrealistic across all work. Reframed: −40% time-to-PR on in-scope tasks (Q-06) |
| C-014 | Context window 32K–128K tokens | brief ¶3 | E | ✅ | Repos exceed this → retrieval over a code index required |
| C-015 | Cost $0.10–$1.00 per task | brief ¶3 | E | ✅ | Hard ceiling $2.00/task, then stop & escalate (Q-07) |
| C-016 | Vector DB for pattern storage | brief ¶3 | C | 🟡 | Solution-as-requirement; accepted, plus structured "pattern cards" for review |
| C-017 | Nine components in three layers | brief ¶4 | C | ✅ | Adopted as reference architecture |
| C-018 | Self-correct up to 3 attempts then escalate | use cases | P | ✅ | Escalation includes diagnosis + attempts tried |
| C-019 | Learned patterns are reviewed before use | Q-08 | P | ✅ | Tech lead approves each pattern card |
| C-020 | Repo content and issues are untrusted input | Q-09 | E | ✅ | Prompt-injection guard; tool allow-list |
| C-021 | No infra/DevOps tasks initially | non-goals | Sc | ❌ | Non-goal (MVP) |
| C-022 | Not replacing developers | non-goals | Sc | ❌ | Augmentation only |

## Decisions

- **Q-01** Success sentence mentions chat answers and visualisations — not coding. Which product is this? → *Copied from another brief; use coding.* → C-011, C-012
- **Q-02** "Suggests and executes after approval" — approve the plan, the diff, or both? → *Both; plan approval can be skipped for tasks < 50 lines.* → C-005
- **Q-03** Is "no prod deploy without approval" a gate or a ban for MVP? → *Ban: agent has no deploy rights at all.* → C-010
- **Q-04** Can the agent approve or merge PRs it reviews? → *Never.* → C-004
- **Q-05** Tenancy? → *Multi-tenant SaaS, enterprise orgs, SSO, data never shared across orgs.* → C-006
- **Q-06** "80% time reduction" — of what, measured how? → *Your call.* → 🟡 −40% time-to-PR on in-scope tasks, revisit after pilot. → C-013
- **Q-07** What happens when a task exceeds budget? → *Stop at $2, escalate with partial work.* → C-015
- **Q-08** Who can teach the agent a pattern? → *Tech leads only; reviewed before active.* → C-019
- **Q-09** Should the agent follow instructions found in issues or code comments? → *Only as task content, never as policy.* → C-020
