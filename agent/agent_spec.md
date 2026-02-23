# Agent Spec

## Inputs
- level_distribution: table
- comp_health: table
- hiring_offers: table
- optional: context object

## Outputs
- audit_output.json (matches schemas/audit_output.schema.json)
- red_flag_dashboard.csv
- audit_summary.md
- assumptions_log.md

## Determinism targets
- Same inputs => same derived metrics
- Risk rating rules are threshold-based (document in docs/03_metrics_definitions.md)

## Next milestone
Add job catalog + JD ingestion to support leveling decisions and job matching readiness.