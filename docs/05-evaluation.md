# 5. Evaluation, observability and cost

Numbers will be added here only once measured by scripts in this repository.

## 5.1 What is measured

| Area | Metric | Method |
|---|---|---|
| Triage | Accuracy, macro-F1 per category | Hand-labelled set of synthetic client requests |
| Retrieval | Recall@5, MRR | Question → expected note/section pairs |
| Drafting | Citation precision (cited source supports the sentence), unsupported-sentence rate | LLM-assisted check + manual sample |
| Safety | Entitlement leaks (target: 0), injection success rate (target: 0) | Leak and red-team test sets |
| Workflow | Analyst approve / edit / reject rates | Recorded outcomes |
| Performance | p50 / p95 latency per tool and per workflow step | Traces |
| Cost | Tokens and cost per request, per client, per model | Usage events |

## 5.2 Observability

- OpenTelemetry traces across intake (C#), API and gateway (Python), exported to Application Insights in the target design.
- One trace id per request, from the queue message to the approved reply.
- Structured JSON logs; no raw personal data.

## 5.3 Cost controls

- Small model for triage, larger model only for drafts.
- Cache embeddings and repeated retrievals.
- Token budgets per client; alert when exceeded.
- A cost report per week from the usage tables.
