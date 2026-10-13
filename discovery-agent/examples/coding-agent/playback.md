# Playback — AI Coding Agent

## So we're building…
An **AI coding agent for software development teams** that can:
- Execute coding tasks — implement features, debug failures, review pull requests (C-002–C-004)
- Adapt to new frameworks and team patterns from 3–5 examples, within 2 working days (C-008, C-009)
- Operate with human oversight: **propose → approve → execute** (C-005)
- Serve 10K developers at launch, designed for 100K (C-006, C-007 🟡)
- Safety-first: it **cannot** deploy to production; that stays a human action (C-010)

## Assumptions ✅
- Access to code repositories (GitHub, GitLab) via org-installed app
- Integration with developer tools (IDE, CI/CD) — read CI results, run tests in a sandbox
- Access to foundation LLMs (e.g. Claude) under an enterprise data agreement

## Non-goals ❌
- NOT replacing human developers — augmentation only (C-022)
- NOT handling infrastructure/DevOps initially (C-021)
- NOT autonomous production deployment — no deploy permission at all (C-010)
- NOT approving or merging PRs (C-004)

## Autonomy contract
| Alone (L3) | With approval (L2) | Suggest only (L1) | Never |
|---|---|---|---|
| read repo, run tests in sandbox, create branch, post review comments | apply plan, push commits to agent branch, open PR | dependency upgrades, schema migrations | merge, deploy, change CI config, touch secrets |

## Success means…
> The agent takes a scoped coding task from a developer and produces a pull request that
> **passes tests and is accepted with minor edits ≥ 60% of the time**, learns a new
> framework from **≤ 5 examples within 2 days**, and cuts **time-to-PR on those tasks by
> 40%** — with **zero unapproved production changes**.

*(Replaces the original sentence, which described chat answers and visualisations — C-011 ⚠️ resolved in Q-01. The 80% target is parked as 🟡 C-013 until the pilot gives a baseline.)*

## Top risks
1. Acceptance rate on large legacy repos lower than pilot repos (context retrieval quality).
2. Learning bad patterns from unreviewed corrections → mitigated by pattern review (C-019).
3. Prompt injection via issues/code comments (C-020).

## Open items
- C-007 🟡 timeline to 100K — platform lead
- C-013 🟡 time-saving target — VP Engineering, after 6-week pilot

**Signed off:** VP Engineering (sponsor) · 2026-10-13
