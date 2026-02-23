# Methodology (Signals-Based Job Architecture Audit)

## Principle
Use internal signals to infer structural issues — then define what evidence is needed to confirm root causes.

## What we measure (by level)
Derived metrics:
1. HC growth = Current HC - HC 12 months ago
2. HC growth % = HC growth / HC 12 months ago
3. Promotion rate = Promotions / Current HC (and optionally / prior HC)
4. Time-in-level sanity check vs promotion rate
5. Midpoint pressure: % above midpoint, median compa ratio
6. Ceiling pressure: % above max
7. Hiring pressure: avg offer % of midpoint, % offers above max
8. Compression signals:
   - high offer % of midpoint + high % above midpoint
   - offers above max + incumbents above max

## What we do NOT claim
- We do not assert a market percentile or benchmark mapping without external survey references.
- We do not assign Radford codes.

## Typical root causes (ranked)
- stale ranges vs market movement (range refresh cadence issue)
- leveling drift / weak level definitions
- inconsistent job matching
- promotion guardrails tied to cycles rather than role evidence
- hiring strategy skewed to senior levels vs pipeline

## Output structure
See `docs/06_output_pack_spec.md`.