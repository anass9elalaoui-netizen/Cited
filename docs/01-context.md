# 1. Context and research findings

*Research date: October 2026. All findings are paraphrased from the sources listed at the end.*

## 1.1 The bank: an AI programme measured in euros

- At its Capital Markets Day on 21 September 2026, Société Générale set a 2029 plan with about **€1.9bn of gross savings**,
  of which **€500–600m is expected from AI**, around €350m already identified [1][2].
- AI is named as a lever across the group, including **process redesign and automation in Global Banking and Investor Solutions**
  (the division that includes markets) [2].
- Reported targets include cutting coding costs by more than 30% with AI and simplifying half of end-to-end processes [1].
- The same day, the bank announced a **strategic agreement with Anthropic** to roll out Claude models across the group [2][3].
- Earlier, in early 2026, the bank **retired its in-house chatbot SoGPT and moved employees to Microsoft Copilot**, because
  in-house tools could not keep pace with market products [4].

**What this means for an AI Developer:** the bank buys general assistants and pays for savings. The work that remains in-house is
connecting those assistants to the bank's own data and workflows, securely and measurably: MCP servers, APIs, event-driven
automation, enterprise data integration, and Azure deployment. That is the profile in the job description.

## 1.2 The bank already proved request triage

Before generative AI, Société Générale deployed NLP tools on client workflows, for example:

- **SG Markets "My Cases"** categorises client requests, detects intent and extracts data; the bank reported a 30% shorter response time [5].
- **Trading Assistant** recognises request-for-quote types in client messages [5].

Cited's triage module is the generative-AI successor of a pattern the bank already trusts, extended to research requests and
connected to retrieval and drafting.

## 1.3 The business: Bernstein

- Bernstein is the cash equities and research joint venture between Société Générale and AllianceBernstein, launched in 2024 [6][7].
- Its research covers **over 1,000 stocks**, with hubs in New York, London, Paris, Hong Kong and Mumbai [7].
- The two parent firms brought different client bases (long-only funds vs. quant and hedge funds) and **separate systems that were
  kept side by side** at launch, with a review planned over time [7]. Two technology estates mean integration work: one common,
  governed access layer is more realistic than rebuilding either side.
- Société Générale plans to own 100% of the business after five years [7].

## 1.4 The market: research is moving into AI agents

- **FactSet** launched a production MCP server in December 2025, giving AI systems governed access to nine datasets
  (fundamentals, estimates, ownership, events and more) without warehouses or exports [8].
- In June 2026 **Aiera** launched a platform, backed by BofA, Citi, Deutsche Bank, Evercore and HSBC, that lets clients query and
  summarise the sell-side research they are entitled to through secure **API and MCP connectors**. Entitlements are checked on each
  pull, requests are logged and usage metrics go back to the research provider [9].
- The same report notes banks' concerns: clients uploading research into general chatbots, access by non-clients, and trust in
  AI summaries. It cites a former Citi research COO saying a large share of research pages were routine earnings previews and
  reviews [9].

**What this means:** a research desk needs its **own** governed channel into client AI agents, with entitlements, citations and
usage tracking, or its research leaks into channels it cannot control or measure.

## 1.5 The rules: research value must be assessed

- In the EU, the **Listing Act** changed MiFID II so firms can pay for research and execution jointly or separately; the measures
  apply from **6 June 2026** [10].
- Whatever the payment method, firms must **assess the quality, usability and value of research every year**, using robust criteria
  and taking remedial action when needed [10].
- The UK reintroduced bundled payments in August 2024 [10].

**What this means:** per-client, per-note usage data (who read what, through which channel) supports both the desk's commercial
conversations and its clients' annual assessments. Cited logs it as a by-product of access control.

## 1.6 Local constraint: data protection in Morocco

The team sits in SG GSC Morocco, so personal data handling follows Moroccan **Law 09-08** (CNDP), alongside group and client-side
rules (e.g., GDPR for EU clients). Cited minimises personal data in prompts and logs (see [Security](04-security.md)).

## 1.7 Requirement mapping

| Job requirement | Where Cited covers it |
|---|---|
| AI apps and workflow automation | Triage → retrieval → draft → approval workflow |
| REST APIs, MCP, event-driven, orchestration | FastAPI, MCP gateway, queue-triggered intake, orchestrated steps |
| Structured, semi-structured, unstructured data | Warehouse, document DB, vector store behind one retrieval layer |
| Data warehouses, lakes, Databricks/Snowflake | Usage and coverage tables in Databricks (DuckDB locally) |
| Azure and Azure AI Foundry | Target deployment and model provider |
| .NET/C# | Azure Function for event intake |
| CI/CD and DevOps | GitHub Actions for Python and .NET |
| Security, observability, scalability, cost | Entitlements, audit, OpenTelemetry, per-request cost, model routing |
| Stakeholders and adoption | Analyst approval UI, usage dashboard for desk heads |

## Sources

1. FStech, *Société Générale targets nearly €600m in AI savings by 2029* (Sept 2026): https://www.fstech.co.uk/fst/Societe_Generale_targets_nearly_600m_in_AI_savings_by_2029.php
2. Société Générale, Capital Markets Day press release (21 Sept 2026): https://www.societegenerale.com/sites/default/files/documents/2026-09/capital-markets-day-press-release.pdf
3. AML Intelligence, *Société Générale signs deal with Anthropic* (Sept 2026): https://www.amlintelligence.com/2026/09/news-societe-generale-signs-deal-with-anthropic-to-cut-costs-and-accelerate-ai-rollout/
4. Le Monde Informatique, *La Société Générale bascule vers Copilot pour son assistant IA* (2026): https://www.lemondeinformatique.fr/actualites/lire-la-societe-generale-bascule-vers-copilot-pour-son-assistant-ia-99084.html
5. Société Générale, *Applying Data and AI: flagship use cases*: https://www.societegenerale.com/sites/default/files/documents/2024-09/applying-data-ia-flagship-use-cases.pdf
6. Société Générale and AllianceBernstein, launch press release: https://www.societegenerale.com/sites/default/files/pr-press-release-societe-generale-official-launch-of-bernstein.pdf
7. The TRADE, *The new kid on the block: a closer look at Bernstein*: https://www.thetradenews.com/the-new-kid-on-the-block-a-closer-look-at-bernstein/
8. FactSet, MCP server announcement (16 Dec 2025): https://www.globenewswire.com/fr/news-release/2025/12/16/3206057/7768/en/FactSet-Meets-Demand-for-AI-Ready-Data-First-to-Announce-MCP-Sans-Intermediary.html
9. AI Street, *AI agents gain access to sell-side research* (June 2026): https://www.ai-street.co/p/ai-agents-gain-access-to-sell-side
10. McCann FitzGerald, *The long and winding road (back) to bundling: MiFID II research payments*: https://www.mccannfitzgerald.com/knowledge/financial-services-regulation/the-long-and-winding-road-back-to-bundling-mifid-ii-research-payments
