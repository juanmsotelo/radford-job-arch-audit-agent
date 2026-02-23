# radford-job-arch-audit-agent

A **signals-based Job Architecture Audit** workflow inspired by Radford-style leveling and Total Rewards governance.

This repo is designed for the common situation where you **don’t yet have a clean job catalog + JDs**, but you do have:
- Level distribution signals
- Compensation health signals
- Hiring offer signals

It produces a defensible “Audit Output Pack”:
- Executive summary + maturity score
- Red-flag dashboard by level
- Ranked root-cause hypotheses (with confirm/deny data)
- Governance-first recommendations
- 30/60/90 plan
- Next data request list for a full Radford-style audit

> This project **does not** use proprietary Radford survey codes. It is *internal-signals-first* and clearly labels inferences vs facts.

## Repository layout

- `docs/` — Methodology, schemas, metrics, output pack spec, agent design
- `prompts/` — Prompt pack (audit, recommendations, QA validation)
- `schemas/` — JSON schemas for inputs and outputs
- `templates/` — Input templates + output outlines
- `examples/` — Sample inputs/outputs (sanitized)
- `src/` — (optional) code to compute metrics, validate inputs, and generate outputs
- `agent/` — agent spec + system prompt + test cases

## Quick start (manual)
1. Add your three tables (Level Distribution, Comp Health, Hiring Offers)
2. Use `prompts/audit_prompt.md` to generate the audit narrative
3. Use `prompts/qa_validation_prompt.md` to validate the output

## Agent direction
See `docs/07_agent_design.md` for the plan to turn this into a repeatable agent:
1) ingest → 2) validate → 3) compute metrics → 4) classify risk → 5) draft audit → 6) QA → 7) export JSON/MD

## Disclaimer
This is not legal, tax, or compensation advice. Use with your organization’s policies, counsel, and (where applicable) survey subscriptions.
