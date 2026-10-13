# Data Pack — {{Project name}}
*What data the system perceives, what it can act on, what it learns from, and how it is
evaluated. Describes fields and classifications — never real sensitive values.*

## 1. Source inventory
| ID | Source / system | Owner | Type (DB, API, docs, files, events) | Access (read/write) | Volume & freshness | Classification | Source |
|---|---|---|---|---|---|---|---|
| DS-1 | | | | | | Public / Internal / Confidential / Restricted | (C-…) |

## 2. Entities & key fields
| Entity | Field | Type | Meaning | Required? | Sensitive? (PII/PHI/PCI/IP) | System of record |
|---|---|---|---|---|---|---|

## 3. Knowledge corpus (for RAG)
| Collection | Contents | Format | Size | Update cadence | Access control | Chunking / metadata notes |
|---|---|---|---|---|---|---|

## 4. Tools & actions *(agentic only)*
| Tool | System | Operation | Input schema (summary) | Side effects | Reversible? | Autonomy level | Rate / value limits | Auth model |
|---|---|---|---|---|---|---|---|---|

## 5. Data quality & readiness
| Source | Known issues | Impact on use cases | Remediation | Owner |
|---|---|---|---|---|

## 6. Privacy, security & governance
- Lawful basis / consent:
- Residency & third-party model processing:
- Masking / de-identification:
- Retention & deletion:
- Access model (per user / tenant / role):
- Untrusted inputs (prompt-injection exposure):
- Audit log contents and retention:

## 7. Feedback & learning signals
| Signal | Captured where | Label meaning | Who provides it | Used for (memory / few-shot / eval / fine-tune) | Guard against bad learning |
|---|---|---|---|---|---|
| Approval / rejection | | | | | |
| Human edit / correction | | | | | |
| Outcome (downstream success) | | | | | |
| Explicit rating | | | | | |

## 8. Evaluation dataset (seeds)
| ID | Use case | Input (synthetic/redacted) | Expected output / action | Must-not-do | Difficulty | Source |
|---|---|---|---|---|---|---|
| EV-1 | UC-1 | | | | easy / hard / adversarial | (C-…) |

Target: ≥ 20 seeds per P0 use case before build, including failure, unknown and
adversarial cases.

## 9. Telemetry & metrics data
How each success metric in the PRD will be computed: event, fields, aggregation, dashboard owner.

## 10. Open items
