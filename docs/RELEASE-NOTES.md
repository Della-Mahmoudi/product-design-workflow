# Changelog

## 0.2.5
- Broadened the Supervisor's trigger description so direct product-design requests (including Persian and Finglish ones) start the workflow without naming it.
- Public release: generic Final QA tool access (read-only, works with any connected browser or Figma MCP), trimmed maintenance evidence, MIT license.

## 0.2.4
- Added conditional expert-workflow guidance from the Della Product Design baseline 0.1: logic-dependent UX (PD-C01), exploration and convergence (PD-C02), semantic design-system migration (PD-C03).

## 0.2.3
- Updated the `product-discovery-framing` skill description.

## 0.2.2
- Clarified readiness: ask only when a material human-owned decision blocks the step; routine UI and flow judgment stays with the Supervisor.
- Completeness fixes to 0.2.1 policy text.

## 0.2.1
- Policy wording for human result gates, worker reuse and the Final QA fallback reviewer.

## 0.2.0
- Added on-demand execution routing (`routing-policy.md`), a per-route capability index, step-package notes and the `refresh-capability-index` maintenance skill.
- Synthetic policy tests (2026-10-21) showed no measurable difference from 0.1.3. The changes ship as clarifications, not proven improvements.

## 0.1.x
- First versions: Supervisor, seven domain skills and the independent Final QA agent (PASS / FAIL / BLOCKED).

## Known limits
- Skill activation depends on description matching. It isn't a guaranteed hook.
- Figma reads/writes, document creation, media generation and interactive browser QA have not been quality-tested.
