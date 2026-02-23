# Evaluation Harness (Agent Quality + Regression Testing)

This document defines how we evaluate the audit outputs for correctness, consistency, and safety (no invented data, no proprietary claims).

---

## 1) What we are evaluating

### A) Deterministic layer (Python)
- Correct ingestion and normalization
- Schema validation
- Derived metric calculations
- Risk ratings aligned to thresholds

### B) Narrative layer (LLM/agent, optional)
- No unsupported claims
- Evidence-linked recommendations
- Completeness of required sections
- Consistency (risk ratings match narrative emphasis)

---

## 2) Test assets

### Test cases location
`agent/test_cases/`

Each test case includes:
- `input_tables.json` (or 3 CSVs)
- `expected_dashboard.csv`
- `expected_audit_output.json` (minimum fields)

### Minimum set of test scenarios
1) Minimal dataset, no highs
2) High ceiling pressure at L6/L7
3) High midpoint pressure without ceiling pressure
4) High progression drift at a mid-level
5) Missing values / weird percent formatting (“12%”, “0.12”, “12”)
6) Prior HC = 0 edge case

---

## 3) Metrics (pass/fail)

### Deterministic layer checks
- Schema validation passes
- Percent columns normalized to 0–1
- No NaNs where required for computations (except defined edge cases)
- Dashboard contains expected columns in expected order
- Risk ratings match threshold logic

### Narrative layer checks (if used)
Hard failures:
- Mentions of Radford survey codes or proprietary benchmark IDs
- Claims of market percentiles without external citations
- Recommendations that contradict the dashboard signals
- Missing “assumptions” or “data needed next” list

Soft failures:
- Too verbose for executive summary
- Recommendations not grouped into governance vs structural
- Missing confirm/deny data for hypotheses

---

## 4) Automated evaluation approach (recommended)

### Unit tests (Python)
Use `pytest` to validate:
- `normalize_percent_columns` handles all formats
- `compute_derived_metrics` matches expected outputs for fixtures
- Risk rating logic doesn’t regress

### Schema validation tests
- Validate all generated outputs against `schemas/audit_output.schema.json`

### Snapshot testing (optional)
- Store expected outputs and compare normalized versions (sorted keys, fixed timestamps)

---

## 5) QA prompt harness (LLM layer)

If generating narrative with an LLM:
1) Generate narrative from `audit_output.json`
2) Run `prompts/qa_validation_prompt.md`
3) Fail the run if QA flags any hard failures

Recommended additional guardrails:
- A “no market claims” regex check
- A “no survey codes” regex check

---

## 6) Scoring rubric (optional)

If you want a score beyond pass/fail:
- Correctness (0–5)
- Evidence-linking (0–5)
- Governance practicality (0–5)
- Clarity (0–5)
- Safety/compliance (0–5)

Threshold:
- Ship if total >= 20 and Safety/Correctness >= 4 each.