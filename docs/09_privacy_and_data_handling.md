# Privacy & Data Handling

This project can be used with compensation and workforce data. Treat it as sensitive by default.

---

## 1) Data classification

### Allowed in a public repo
- Aggregated, non-identifiable example data
- Sanitized synthetic datasets
- Schemas, templates, methodology docs
- Sample outputs produced from synthetic data

### Not allowed in a public repo
- Employee-level compensation data
- Names, emails, IDs, job codes linked to individuals
- Small-group aggregates that can re-identify individuals (e.g., “L7 in a 3-person org”)
- Offer details tied to identifiable people
- Any contractual or survey proprietary content (e.g., Radford benchmark IDs)

---

## 2) Minimum anonymization standards

If you must share examples:
- Use only aggregated tables by level (as this repo does)
- If segmenting by family/geo, ensure each segment has adequate size (e.g., k-anonymity threshold)
- Remove:
  - direct identifiers (name/email/employee ID)
  - quasi-identifiers (unique titles + location + niche team)

Recommended:
- Replace numbers with scaled/synthetic values while preserving ratios and patterns.

---

## 3) Local data handling (recommended workflow)

- Store real datasets **outside** git (e.g., `./local_data/` ignored by `.gitignore`)
- Use environment variables for paths
- Encrypt at rest where possible
- Restrict access to only the audit team (least privilege)

---

## 4) Logging policy

Never log:
- Raw row-level datasets
- Compensation values at employee level
- Any tokens/secrets

Safe logs:
- Row counts
- Column presence validation results
- Summary of normalization actions (e.g., “converted % columns to proportions”)

---

## 5) Secure defaults in this repo

Recommended default ignores:
- `outputs/`
- `deliverables/`
- `*.env`

If you choose to commit outputs:
- Only commit outputs derived from synthetic datasets
- Add a checklist in PR template: “No sensitive data included”

---

## 6) LLM / agent considerations

If using an external LLM provider:
- Do not send employee-level data
- Prefer aggregated metrics and precomputed dashboards
- Add a data minimization layer:
  - send only what is needed for the narrative
  - strip columns not needed for analysis

If running locally / private:
- Use a private repo
- Use enterprise controls and data retention policies

---

## 7) Compliance notes (non-exhaustive)

Depending on jurisdiction and company policies, compensation data may fall under:
- GDPR (EU), UK GDPR
- State pay transparency laws (US)
- Internal policy constraints (confidential compensation data)

This repo is a methodology and tooling scaffold. Always consult internal policy and counsel.

---

## 8) Incident response (if something leaks)

If sensitive data is accidentally committed:
1) Rotate/secure any impacted credentials immediately (if applicable)
2) Remove the data from git history (not just a revert)
3) Invalidate forks if possible / contact GitHub support if needed
4) Document the incident and update prevention controls