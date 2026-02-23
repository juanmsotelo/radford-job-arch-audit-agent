# Audit Playbook (Signals-Based Job Architecture Audit)

This playbook operationalizes a Radford-style, governance-first **Job Architecture Audit** when you only have aggregated signals:
- Level Distribution
- Compensation Health
- Hiring Offers

It is designed to produce a defensible output pack and a clear path to a deeper (catalog + JD + matching) audit.

---

## 0) Outcomes

By the end, you should have:
- A **Red Flag Dashboard** by level (derived metrics + risk ratings)
- **Ranked root-cause hypotheses** with confirm/deny data requests
- A **governance-first recommendations** list (what to stabilize now vs fix structurally)
- A **30/60/90 plan**
- A **data request list** for a full Radford-style audit

---

## 1) Inputs and minimum checks

### Required tables
1) **Level Distribution**
2) **Comp Health**
3) **Hiring Offers**

### Pre-flight checks (must pass before analysis)
- Each table has a **Level** column and consistent level values (e.g., L2–L7)
- Percent fields are consistently represented (either all proportions or all percents)
- No duplicate rows per Level (unless explicitly segmented by geo/family; if so, add those dimensions)

### Normalization rules
- Normalize percent-like columns to proportions (e.g., `12% → 0.12`, `105% → 1.05`)

---

## 2) Compute derived metrics (deterministic)

Compute per level:
- HC Growth = Current HC − 12 Months Ago HC
- HC Growth % = HC Growth / (12 Months Ago HC)
- Promo Rate % = Promotions Last 12 Months / Current HC
- Midpoint pressure indicators: Median Compa-Ratio, % Above Midpoint
- Ceiling pressure indicators: % Above Max
- Hiring pressure indicators: Avg % of Midpoint, % Offers Above Band Max
- Risk ratings:
  - Ceiling Pressure Risk
  - Midpoint Pressure Risk
  - Progression Drift Risk
  - Overall Risk
  - Primary Risk Type

Reference `docs/03_metrics_definitions.md` for thresholds.

---

## 3) Read the system (interpretation order)

### Step 1: Identify “where the system breaks”
Start with **Overall Risk = High** levels.
- If **Ceiling pressure is High**, prioritize range architecture and offer governance.
- If **Midpoint pressure is High** but ceiling isn’t, ranges may be “too tight” or hiring practices skew.
- If **Progression drift is High**, suspect leveling rubric gaps or promotion policy drift.

### Step 2: Check for structural pattern
Ask:
- Are the highest risks concentrated in **senior levels (L5–L7)**?
- Are junior levels shrinking while senior levels expand?
- Are offers structurally above midpoint at the same levels where incumbents are above midpoint?

### Step 3: Build 5–7 ranked hypotheses
Each hypothesis must include:
- Evidence (from dashboard metrics)
- What would confirm it (1–3 specific data points)
- What to do if confirmed (actionable intervention)

---

## 4) Write the audit narrative (output pack)

### A) Executive summary (10 bullets max)
- Maturity score (signals-based heuristic)
- Top risks (ranked)
- Top recommendations (ranked)
- Main root-cause hypothesis (single sentence)

### B) Findings by theme
Use this structure per theme:
**What I see → Why it matters → Evidence → Recommendation**

Themes:
- Level distribution & progression
- Promotion engine signals
- Pay band health
- Hiring offers vs structure
- Architecture integrity risk

### C) Red Flag Dashboard
Include:
- Level + all derived metrics
- Risk ratings
- Primary risk type

### D) Governance-first recommendations
Separate:
- Stabilize now (stop exceptions culture)
- Structural fixes (ranges / levels / titles)
- Operating rhythm (quarterly health review)

### E) 30/60/90 plan
- 30 days: controls + minimal data pull
- 60 days: proposals + calibration
- 90 days: pilot + rollout + audit loop

### F) Appendix
- Assumptions
- “Data needed next” list

---

## 5) QA checklist (must run before publishing)

Hard rules:
- No market percentile claims unless supported by external data (not in this signals-only scope)
- No survey codes or proprietary Radford mappings
- Every recommendation cites at least one dashboard signal (metric/risk)
- Percent normalization is consistent
- Risk ratings align with thresholds (no “High” without meeting criteria)

---

## 6) Escalation path (when to move beyond signals)

Move to a full Radford-style audit when:
- High ceiling pressure persists after range refresh
- Promotions remain high + time-in-level remains short
- “Hot” families drive exceptions (needs family/geo segmentation)
- You need credible job matching and market pricing governance

Next inputs:
- Job catalog + family/track/title + location
- JD links or standardized role summaries
- Promotion and offer event logs
- Range assignment by job

See `docs/07_agent_design.md` for the roadmap.