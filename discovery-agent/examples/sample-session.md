# Sample session (abridged)

Client: a mid-size insurer. Sources: a 6-slide vision deck and a 40-minute kickoff transcript.

---

**User:** `/discovery-agent:discover ./acme-claims "Claims Triage Agent"`

**Agent:**
▸ Phase 1 · Ingest — 2 sources, 47 atomic claims, 3 conflicts.
▸ Phase 2 · Classify — Perceive 2 · Decide 2 · Act 1 · Learn 1 · Adapt 1 → **Agentic
(supervised)**, hybrid with a predictive fraud score. Loading agentic lens + insurance lens.
▸ Phase 3 · Grill — Scope (12 open).

> **Q-01 · Scope · task domain**
> The deck says *"AI handles all claims end-to-end"* (slide 2), but in the kickoff the
> claims director said *"let's start with motor"* (14:32).
> Is the first release motor claims only?
> **My recommendation:** motor, first-notice-of-loss to triage decision only — one line of
> business keeps the rules and eval set tractable; property/health follow once triage
> accuracy is proven.
> *(yes · no, because… · your call · park)*

**User:** yes, but include glass claims, they're the highest volume.

**Agent:** Recorded C-004 ✅ "MVP = motor incl. glass, FNOL → triage". Added C-048
"glass claims are highest volume" ❓ — need a number.

> **Q-02 · Scope · autonomy**
> You said *"it should just settle the small glass ones"* (21:10).
> Settling pays money out — that's hard to reverse. What's the most it may pay without a
> handler approving?
> **My recommendation:** in the MVP it *prepares* the settlement and a handler approves
> with one click (L2). Promote glass ≤ €300 to auto-settle (L3) after 1,000 approved
> cases at ≥ 98% agreement and zero fraud leakage.

**User:** your call.

**Agent:** Recorded C-012 🟡 (assumed per recommendation; owner: claims director).

… *(19 more questions across P, E, C, T, Sm)* …

▸ Phase 4 · Playback

> **So we're building** a claims triage agent for motor (incl. glass) that:
> - reads FNOL forms, photos and call notes and builds a claim summary
> - checks policy cover and flags fraud signals
> - routes to fast-track, standard or specialist queue
> - prepares glass settlements for one-click handler approval
> - learns from handler overrides weekly (reviewed by a senior handler)
>
> ✅ Assumes: access to policy admin system (read), claims system (write: notes, queue).
> ❌ Not: denying claims, contacting customers, non-motor lines.
> **Autonomy:** alone → summarise, route, flag · approval → settlements · never → deny a claim.
> **Success means:** median FNOL-to-triage time from 2 days to 2 hours at ≥ 95% routing
> accuracy with zero unapproved payouts.
> **Is this right? What's wrong or missing?**

**User:** Right. Signed off — Head of Claims, today.

▸ Phase 5 · Generate — wrote `discovery/out/BRD.md`, `PRD.md`,
`domain-knowledge-pack.md`, `data-pack.md`. 61 claims: 44 ✅ · 14 🟡 · 3 ❓.
Riskiest assumptions: C-012 settlement limit, C-031 photo quality, C-040 override
labelling effort. Next step: collect 20 real claims per use case for the eval set.
