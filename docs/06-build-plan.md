# 6. Build plan (4 weeks)

Local first and free: Docker Compose, Azurite, open models or free-tier APIs, DuckDB. Azure deployment is the last step.

| Week | Deliverable |
|---|---|
| **1. Data and retrieval** | Synthetic corpus (notes in sections, clients, entitlements); public SEC filings for the same tickers; pgvector + document store + DuckDB; hybrid retrieval with entitlement filter; leak tests |
| **2. MCP gateway and API** | MCP tools from the spec; FastAPI endpoints; audit log with hash chaining; retrieval evaluation script and first numbers |
| **3. Workflow** | C# Azure Function intake (queue-triggered, xUnit tests); triage with structured output and evaluation set; drafting with citation check; analyst inbox UI |
| **4. Production readiness** | GitHub Actions (Python + .NET); OpenTelemetry; cost tracking; Azure AI Foundry provider; deployment notes for Azure; README results |

## Definition of done

- `docker compose up` and one seed command run the full demo on a fresh machine.
- CI is green for Python and .NET.
- Zero entitlement leaks on the leak test set.
- Every number in the README is produced by a script in the repository.
