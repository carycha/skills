# Quality Evaluation Guide & Checklist

## Evaluation Criteria

Each skill is evaluated against this checklist:

- [ ] **Content Overlap**: Does this duplicate `MEMORY.md`, `GEMINI.md`, or another skill?
- [ ] **Technical Freshness**: Are CLI flags, APIs, or tool names current? (Use `google_web_search` if uncertain)
- [ ] **Actionability**: Does it provide concrete code examples or deterministic steps?
- [ ] **Scope Fit**: Is the trigger name and description specific enough to prevent false positives?

## Verdict Definitions

| Verdict | Meaning |
|---------|---------|
| **Keep** | High quality, unique value, and current. |
| **Improve** | Useful, but needs trimming or better examples. |
| **Update** | Technical references are outdated. |
| **Retire** | Redundant, low quality, or superseded. |
| **Merge** | Overlaps significantly with another skill. |

## Reason Quality Requirements

The `reason` field must be self-contained:
- **Bad**: "Superseded"
- **Good**: "Overlap with `auto-skill`; `auto-skill` already handles the logic for X, making this 40-line skill redundant."
