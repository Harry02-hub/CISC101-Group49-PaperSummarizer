Purpose
Prepare inputs, validate completeness, set summarization parameters, and enforce global constraints.
Responsibilities
Section list: Detect and register sections: Introduction, Methods, Results, Discussion.
Constraint application: Set per-section limit (≤100 words) and total limit (≤400 words).
Audience setting: Store audience (“general public” or “expert”) and tone parameters.
Normalization: Trim whitespace, remove headings duplication, and standardize section keys.
Pre-checks: Flag missing/empty sections; pass to Guardrails.
Inputs
Paper sections: Raw text for each section.
Audience: “general public” or “expert.”
Outputs
Config object: Section registry, limits, audience tone settings.
Validation report: Missing/empty sections, anomalies.
Key rules
No new sections: Only the four canonical sections.
Order enforced: Introduction → Methods → Results → Discussion.

