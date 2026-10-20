# 3. MCP tool specification

All tools are read-only. All results carry citations. All calls are entitlement-checked and audited.

## 3.1 Tools

### `search_research`
Search research the caller is entitled to.

| Input | Type | Notes |
|---|---|---|
| `query` | string | Natural-language question |
| `tickers` | string[] | Optional filter |
| `note_types` | enum[] | `initiation`, `update`, `earnings_preview`, `earnings_review`, `sector` |
| `since` | date | Optional |
| `limit` | int | Default 5, max 20 |

Returns a list of passages: `note_id`, `title`, `section`, `ticker`, `published_at`, `analyst`, `text`, `score`.

### `get_note`
Return the entitled sections of one note, with its metadata. Embargoed or non-entitled notes return a clear error, never partial text.

### `get_coverage`
Return the coverage list for a ticker or sector: covering analyst, rating, last note date. Structured data from the warehouse.

### `get_estimates`
Return the house estimates for a ticker (revenue, EPS) with the note that published them.

### `get_filing`
Return public filing passages (SEC EDGAR) for a ticker, so answers can combine house research with primary sources.

## 3.2 Entitlement model

| Rule | Example |
|---|---|
| Coverage scope | Client A is entitled to Europe Banks and US Tech |
| Note type | Some clients receive sector notes only |
| Embargo | No access before publish time + delay for agent channels |
| Channel | A client may allow human reading but not agent access |

Rules are evaluated **before retrieval**, as a filter on the search, not after generation.

## 3.3 Error and refusal behaviour

- No entitled source → the tool returns "no entitled research found", never a model-generated guess.
- Rate limits per client and per tool, with clear error codes.
- Every error is audited like a success.

## 3.4 Example call

```json
{
  "tool": "search_research",
  "arguments": { "query": "What is the house view on net interest margin for European banks?",
                 "note_types": ["sector", "update"], "limit": 3 }
}
```

```json
{
  "results": [
    { "note_id": "SYN-2026-0412", "title": "European Banks: margins past the peak",
      "section": "thesis", "ticker": null, "published_at": "2026-09-14",
      "analyst": "Synthetic Analyst 3", "text": "…", "score": 0.82 }
  ],
  "entitlement_rule": "client:A/sector:eu-banks",
  "audit_id": "evt_01J…"
}
```

*All note ids, titles and analysts above are synthetic.*
