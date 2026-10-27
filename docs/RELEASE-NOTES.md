# Changelog

## 0.3.2
- Supervisor: read domain skill bodies before judging work; self-review and fix clear in-scope defects; continue authorized work within a stage and pause on coherent stage results (and real decisions/authority), not every internal step; stop repair loops with no progress; pause after every Final QA report for human direction.
- Multi-step contract: stage-level progress, worker self-check within authority, and fresh reassessment after authorized QA follow-up.
- Domain skills: ported 0.2.8 tuning additions (motion, gestures, asset handoff, token/extraction audits, feedback corpora, visual exploration, implementation evidence, and related checks).

## 0.3.1
- Supervisor: readiness triage before a full spec; inline contradiction, scope-drift and state-exit checks; severity by consequence.
- Final QA agent: consequence-based materiality; spec defect vs unchecked; unmet stays unmet even if risk is accepted.
- Multi-step contract: unresolved required execution obligation keeps delivery pending.

## 0.3.0 (first public release)
- Product Design Supervisor skill, seven domain skills and an independent Final QA agent (PASS / FAIL / BLOCKED).
- The Supervisor frames the brief, loads only the domain skills a step needs, reviews each result and waits for your decision.
- The Final QA agent blocks editing and shell tools with `disallowedTools` and otherwise inherits your session's tools.

## Known limits
- Skill activation depends on description matching. It is not a guaranteed hook.
- Works on briefs, text, screenshots and specs. Figma integration is experimental and untested.
- Document creation, media generation and interactive browser QA have not been quality-tested.
