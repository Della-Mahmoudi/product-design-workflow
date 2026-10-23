---
name: refresh-capability-index
description: Maintenance only. Use when someone explicitly asks to benchmark execution profiles or connectors, or to refresh, update or correct the Product Design capability index (capability-index.json). Not for ordinary design work, routing or choosing an executor; product-design-supervisor handles those without benchmarking.
---

# Refresh Capability Index

Maintain the compact [runtime index](../product-design-supervisor/references/capability-index.json) owned by `product-design-supervisor`. This Skill and its evidence are maintenance-only; normal routing does not load them.

## Decide what needs evidence
- Extract the requested routing decision and its task/output family, affected profile or capability, and known gaps. Reuse applicable evidence; do not rerun every model or connector by default.
- Separate a capability's documentation, successful invocation, tested output quality and real-workflow impact. A connection probe or a plausible route plan does not demonstrate output quality. Synthetic fixtures do not prove productivity on real internal work.
- Reuse task/checkpoint authorization for the named checks. Ask only for missing authority, material scope/consequences or spending approval, and obey actual runtime permissions. No unapproved credit-consuming generation, new credentials, unrelated content access or production writes. An unattended permission gap leaves that check unexecuted with a reason; it is not a failed quality result.

## Method and evidence
- Follow [benchmark-method.md](references/benchmark-method.md). Freeze inputs, rubrics, candidate/grader separation, call budget, repetitions, holdouts and stopping rules before runs.
- The raw 0.1 pilot data is not shipped; [the 0.2.0 summary](references/evidence-2026-10-21-v0.2.0.md) holds published findings. Record new observed runs in separate versioned evidence files, first in the task workspace; never invent a run record to fill a gap.
- [evidence-2026-10-21-v0.2.0.md](references/evidence-2026-10-21-v0.2.0.md) summarizes the 0.2.0 release evaluation: findings, limits and external kit hashes. Raw records stay in those kits.
- An authorized test operator may check objective fixtures and evidence. Designer approval remains necessary for subjective creative preferences and the production Human checkpoints; a benchmark does not replace them.

## Update
1. Choose the smallest discriminating evaluation: targeted availability checks, a frozen task bundle, matched old/new policy comparisons, or representative real tool execution. Include bounded repeats only where variability could change the decision.
2. Execute the frozen plan with self-contained inputs and current supported parameters. Keep raw outputs, metadata, initial judgments and adverse results. Record skipped, unavailable and failed calls separately from judged quality.
3. Check exact properties with deterministic code, then use calibrated blinded semantic comparison. Keep corrections/adjudications separate with their reasons. A safety or scope failure must not disappear inside an average score.
4. Regenerate a compact, task-oriented index: per-route scope/date and evidence maturity, supported recommendation and uncertainty, verification/fallback limits. Keep full results and old pilot scores out of runtime context. Model identity/version/cost stay unknown unless evidenced; no personal account details or raw-evidence paths in the index.
5. Validate references, JSON, evidence-summary consistency and preservation of historical records. Present the candidate changes, decision-relevant findings and remaining unknowns. Edit/package in the selected workspace, not installed Skill files; installation or publication needs its own existing task authorization.

## Never
- Run maintenance benchmarks as part of ordinary design routing, or add recurring retests without a cadence request.
- Treat accepted model aliases, self-reports, token totals or isolated durations as verified identity, billing or general speed.
- Infer a universal winner, or label a new capability quality-tested without inspectable output and scoped evidence.
- Leak expected routes, grader rubrics, answer oracles, prior verdicts or parent reasoning into candidate prompts.
