# 4. Security and compliance

## 4.1 Principles

1. **Least privilege by design.** The model only sees what the caller is entitled to; the filter runs before retrieval.
2. **Read by agents, sent by humans.** No outbound message leaves without analyst approval.
3. **Everything is traceable.** Who asked, what was returned, which rule allowed it, what was sent.
4. **Data stays inside the boundary.** Models are called through the bank's Azure tenant in the target design.

## 4.2 Threats and controls

| Threat | Control |
|---|---|
| Client sees research they are not entitled to | Entitlement filter on the search query; integration tests per rule; deny by default |
| Prompt injection inside a note, filing or email | Retrieved text is wrapped and labelled as data; screening for instruction-like text; tools are read-only |
| Hallucinated claims in drafts | Sentence-level citation check; unsupported sentences removed; analyst approval |
| Personal data in prompts and logs | Masking of names, emails and phone numbers before model calls; logs store hashes, not raw queries |
| Tampering with the audit trail | Append-only log with hash chaining; periodic integrity check |
| Secret leakage | Key Vault + managed identity; secret scanning in CI |
| Cost abuse | Per-client rate limits and token budgets; alerts on anomalies |

## 4.3 Regulatory context (design-level, not legal advice)

- **Research rules (EU MiFID II as amended by the Listing Act):** clients must assess research quality and value every year;
  usage records help both the desk and its clients.
- **Data protection:** Moroccan Law 09-08 (CNDP) for the team's processing; GDPR for EU personal data.
- **Record-keeping:** audit events retained per the bank's retention policy (configurable).

## 4.4 Tests

- Entitlement matrix tests: every client × note type × channel combination.
- Red-team set: notes and emails containing injection attempts; expected outcome: no tool misuse, no instruction followed.
- Leak test: queries designed to retrieve non-entitled content must return nothing.
