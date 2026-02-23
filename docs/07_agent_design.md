# Agent Design (Roadmap)

## Goal
Turn a repeatable audit workflow into an agent that:
- validates inputs
- computes derived metrics
- generates audit narrative + recommendations
- produces standardized outputs (MD/JSON) to render into memo/deck

## Proposed agent pipeline
1) Ingest: read Excel/CSV/JSON
2) Validate: schema checks + % formatting normalization
3) Compute: derived metrics per level
4) Classify: risk rating (Low/Med/High) per level based on thresholds
5) Draft: executive summary + findings + hypotheses + 30/60/90
6) QA: consistency checks (no invented data, citations to input rows)
7) Export:
   - audit_output.json (structured)
   - audit_summary.md (narrative)
   - red_flag_dashboard.csv

## Interfaces
- Inputs: files or JSON payloads
- Outputs: JSON + markdown
- Optional: renderers to PPTX/DOCX

## Guardrails
- Never claim market facts not present in inputs
- Always label inferences
- Always list missing data to confirm hypotheses