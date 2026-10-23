# Changelog

## 0.3.0 (first public release)
- Product Design Supervisor skill, seven domain skills and an independent Final QA agent (PASS / FAIL / BLOCKED).
- The Supervisor frames the brief, loads only the domain skills a step needs, reviews each result and waits for your decision.
- The Final QA agent blocks editing and shell tools with `disallowedTools` and otherwise inherits your session's tools.

## Known limits
- Skill activation depends on description matching. It is not a guaranteed hook.
- Works on briefs, text, screenshots and specs. Figma integration is experimental and untested.
- Document creation, media generation and interactive browser QA have not been quality-tested.
