# Industry Lenses

Short prompts to make generic questions industry-sharp. They are reminders of *what to
ask about*, never facts to write into the ledger without confirmation. Regulations
listed are common examples — always ask the client which apply to them.

## Universal lens (derive one for any unlisted industry)

1. **Who regulates this?** (regulator, auditor, standards body, works council)
2. **What is irreversible?** (money moved, record filed, message sent, physical action)
3. **Who gets hurt if it's wrong?** (customer, patient, employee, public, the company)
4. **What data is sensitive?** (personal, financial, health, IP, safety-critical)
5. **What's the human expert's tacit knowledge?** (heuristics never written down)
6. **What's the system of record?** (where truth lives; who owns it)

## Financial services & insurance
- Irreversible: payments, trades, claim payouts, credit decisions, customer notices.
- Probe: explainability of decisions (adverse-action reasons), model risk management,
  four-eyes approval thresholds, fraud and AML hand-offs, record retention.
- Regs to ask about: SOX, PCI DSS, GDPR/CCPA, fair-lending rules, EU AI Act (credit
  scoring is high-risk), local insurance/banking supervisors.
- Data: transactions, KYC documents, policy/claims history, call recordings.

## Healthcare & life sciences
- Irreversible: clinical advice reaching patients, orders, prescriptions, submissions.
- Probe: clinician-in-the-loop, intended use (is it a medical device?), evidence
  standards, clinical terminology (ICD, SNOMED, LOINC), adverse-event reporting.
- Regs to ask about: HIPAA, GDPR (special category data), FDA SaMD / EU MDR, GxP.
- Data: EHR, claims, imaging, trial data, PHI de-identification needs.

## Retail, e-commerce & consumer
- Irreversible: refunds, price changes, customer communications at scale, inventory moves.
- Probe: peak seasons, brand voice, promotion rules, returns policy edge cases, catalog quality.
- Regs to ask about: consumer protection, GDPR/CCPA, accessibility, marketing consent.
- Data: orders, catalog, CRM, reviews, support tickets.

## Manufacturing, energy & industrial
- Irreversible: physical actions, setpoint changes, maintenance shutdowns, safety systems.
- Probe: OT/IT boundary, latency at the edge, safety integrity levels, operator override,
  shift handovers, sensor reliability.
- Regs to ask about: ISO 9001/45001, IEC 61508/62443, environmental permits.
- Data: sensor/time-series, MES/ERP, maintenance logs, SOPs, CAD.

## Public sector & government
- Irreversible: eligibility decisions, benefits, enforcement, citizen notices.
- Probe: fairness/bias, appeal process, transparency obligations, procurement rules,
  accessibility, multilingual needs, records/FOI.
- Regs to ask about: data protection law, AI/algorithmic transparency rules, EU AI Act
  (many public uses are high-risk), accessibility standards.

## Legal & professional services
- Irreversible: filings, advice to clients, contract execution, deadlines missed.
- Probe: privilege and confidentiality, citation accuracy, conflict checks, matter
  boundaries (no cross-client leakage), partner sign-off.
- Data: contracts, matters, precedents, time entries, research databases.

## Telecom, media & tech
- Irreversible: network changes, customer plan changes, content publication.
- Probe: change windows, rollback, scale (millions of events), content moderation,
  copyright, recommendation fairness.
- Data: CDRs/logs, tickets, content libraries, usage telemetry.

## HR & people operations
- Irreversible: hiring/firing decisions, pay changes, employee communications.
- Probe: bias in screening, works-council consultation, employee consent, manager override.
- Regs to ask about: employment law, GDPR, EU AI Act (employment is high-risk), NYC AEDT-style audit rules.

## Logistics & supply chain
- Irreversible: orders placed, shipments dispatched, supplier commitments.
- Probe: exceptions (delays, damages, customs), carrier integrations, forecast vs actual,
  cut-off times.
- Data: WMS/TMS, EDI messages, tracking events, contracts/rate cards.

## Software & engineering teams
- Irreversible: production deploys, data migrations, secrets exposure, public releases.
- Probe: repo access, CI/CD gates, coding conventions, review policy, test coverage,
  environment separation.
- Data: code, issues, PRs, CI logs, runbooks, incident history.
