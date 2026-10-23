# Source map — what to trust, when to load it, and when to leave it alone

Read this when you are unsure which source should settle a question, or whether going online is
justified. The default at runtime is: use what the user supplied (Tier 0), apply the distilled
guidance in the other reference files, and do **not** browse. Online verification is for when a
tool's current behavior, a current API detail, or a conformance detail genuinely changes the
delivery decision — or when the user explicitly asks for current-source verification.

Verification note: every external source below was checked against its official page on
2026-10-20 while this skill was built; the WCAG, Figma, Storybook, and DTCG entries were re-checked
on 2026-10-21. Tool behavior and plan availability change; if a Figma, Storybook, or DTCG detail
would change a decision, re-check the page rather than trusting the summary here.

Tools are optional and never the methodology. A tool status — Figma's *Ready for dev*, a tracker
column — is workflow metadata, not Tier 0 evidence that a design is ready; readiness is decided by
the gate in `ready-for-dev-and-handoff.md` whether or not the team uses the tool.

---

## Category 1 — Actual production truth (Tier 0)

| Field | Detail |
|---|---|
| Sources | The team's repository and production component library; real API contracts; engineering architecture notes; the current design-system and token implementation (Figma variables and code tokens as they actually exist); platform constraints; product requirements; current tickets; the team's Definition of Done; approved design artifacts and interaction specs; the team's actual accessibility requirements; constraints engineering has confirmed. |
| Authority | Highest contextual authority. Nothing external overrides it for "what does this product do and use". |
| Domain | Everything the skill decides: readiness, mapping, parity, deviations. |
| When to use | Always, first. If the user did not supply it, name it as missing and classify dependent statements as *requires confirmation*. |
| When not to use | Never treat current production behavior as automatically correct. If it conflicts with approved requirements or mandatory accessibility, flag the conflict instead of normalising it. |
| Runtime/load policy | Read what is supplied or reachable (repo, Storybook, Figma file, tickets). Do not fabricate what is not supplied. |
| Limitations | Often incomplete; frequently undocumented; may contain legacy inconsistencies the team has decided to live with. |
| Licensing/access | The team's own material; access depends on what the session is given. |

---

## Category 2 — Accessibility standards (Tier 1)

### WCAG 2.2 — https://www.w3.org/TR/WCAG22/

| Field | Detail |
|---|---|
| Authority | Normative W3C Recommendation (current version dated 12 December 2024; backwards compatible with 2.0/2.1). |
| Domain | Accessibility requirements and the vocabulary for accessibility defects. |
| When to use | Naming a defect precisely; checking that approved accessibility behavior survived implementation; deciding severity of an accessibility issue. |
| When not to use | Do not claim full WCAG conformance from design QA alone; conformance is page/product-level and needs real assistive-technology testing. Do not fetch the spec to re-derive basics already in `implementation-qa-and-parity.md`. |
| Runtime/load policy | Do not fetch by default. Fetch only when an exact criterion wording or a new-in-2.2 detail matters to the decision. |
| Verified facts (re-checked 2026-10-21) | New in 2.2: 2.4.11 Focus Not Obscured (Minimum) AA; 2.4.12 Focus Not Obscured (Enhanced) AAA; 2.4.13 Focus Appearance AAA; 2.5.7 Dragging Movements AA; 2.5.8 Target Size (Minimum) AA; 3.2.6 Consistent Help A; 3.3.7 Redundant Entry A; 3.3.8 Accessible Authentication (Minimum) AA; 3.3.9 Accessible Authentication (Enhanced) AAA. 4.1.1 Parsing was removed. Frequently relevant: 1.3.1 Info and Relationships (A), 1.4.3 Contrast (Minimum) (AA), 1.4.10 Reflow (AA), 1.4.11 Non-text Contrast (AA), 1.4.12 Text Spacing (AA), 2.1.1 Keyboard (A), 2.1.2 No Keyboard Trap (A), 2.4.3 Focus Order (A), 2.4.7 Focus Visible (AA), 3.3.1 Error Identification (A), 3.3.3 Error Suggestion (AA), 4.1.2 Name, Role, Value (A), 4.1.3 Status Messages (AA), 2.3.3 Animation from Interactions (AAA). |
| Limitations | Web-oriented; native platforms need their platform guidance too (below). |
| Licensing/access | W3C document licence; freely readable. |

### Platform accessibility guidance (Apple HIG Accessibility, Android/Material accessibility, Windows)

| Field | Detail |
|---|---|
| Authority | Official platform guidance; normative for platform conventions (focus, traversal, labels, dynamic type, etc.). |
| When to use | Native apps, or web features whose platform behavior matters (e.g., iOS focus/VoiceOver traversal). |
| Runtime/load policy | Fetch only if the platform-specific behavior is the open question. |
| Limitations | Not a substitute for the product's own accessibility requirements. |

---

## Category 3 — Design tools (Tier 1, optional — only when the team uses Figma)

### Figma — Guide to Dev Mode — https://help.figma.com/hc/en-us/articles/15023124644247-Guide-to-Dev-Mode-in-Figma

| Field | Detail |
|---|---|
| Authority | Official vendor documentation for the tool. Authoritative about the tool, not about delivery methodology. |
| Domain | Developer-facing context in Figma: inspect, measurements, annotations, statuses, compare changes, variables, component playground, Code Connect, resource links, plugins. |
| When to use | The team uses Figma and the question is how handoff, annotations, change comparison, or component/variable inspection should be expressed or read in the file — never whether the design is ready (that is the gate in `ready-for-dev-and-handoff.md`). |
| When not to use | Teams not on Figma; teams using Figma only for pictures with handoff happening elsewhere (then the ticket/spec is the artifact of record). Do not require Figma, Dev Mode, or any status as a precondition for readiness. |
| Runtime/load policy | Do not fetch by default. Fetch when a current UI detail or plan/seat gating matters. |
| Verified facts (re-checked 2026-10-21) | Plan- and seat-gated (Figma Design files only; a Full or Dev seat; check the page for the current plan list). Inspect shows layer properties, applied styles and variables, and component metadata. "Compare changes" opens frame history (for instances: "Compare with main component"). The Variables view shows applied and suggested variables. "Explore component behavior" opens the component playground. Annotations and measurements are designer-added developer notes. Resource links (GitHub, Jira, Storybook, VS Code) added to components propagate to instances. Content inside *sections* is prioritised, and designs marked ready appear under "Ready for development" in the Dev Mode layers panel. |
| Limitations | Generated code is a starting point, not the product's code; auto-generated snippets do not know the team's components unless Code Connect is used. |
| Licensing/access | Public help article; Dev Mode is plan- and seat-gated. |

### Figma — Dev Mode statuses (optional workflow metadata) — https://help.figma.com/hc/en-us/articles/26781702258583-Dev-Mode-statuses-and-notifications

| Field | Detail |
|---|---|
| Domain | The *Ready for dev* status Figma offers for signalling handoff, plus plan-dependent extras. |
| Role in this skill | Workflow metadata only. If the team uses Figma, the status may be set after the design passes the team's readiness criteria. It never substitutes for the readiness gate, a marked design can still be `Not Ready`, and the absence of the status never blocks handoff. |
| When to use | Only when the team signals handoff in Figma and the question is how to set or read that signal. |
| Runtime/load policy | Do not fetch by default; fetch only if a current plan or UI detail would change the answer. |
| Verified facts (re-checked 2026-10-21) | *Ready for dev* is set on a section, frame, or component and can carry a note; a *Completed* status and some status-change notifications are plan-dependent. Optional feature: Figma puts a design marked Ready for dev (or Completed) into a *Changed* state when it is later edited, and developers can compare versions — a convenience for spotting post-handoff edits. How that state is cleared and who is notified depend on the plan, and not every edit is flagged (library instance updates and value changes to already-attached styles or variables are not). |
| Limitations | A status records intent, not completeness. A change flag tracks edits to the marked design, not whether the build diverged. Change management never depends on it: surface, record, and synchronize material changes regardless (see `collaboration-and-change-management.md`). |

### Figma — Code Connect — https://help.figma.com/hc/en-us/articles/23920389749655-Code-Connect

| Field | Detail |
|---|---|
| Domain | Mapping Figma components to real code components so Dev Mode (and the Figma MCP server) show the team's actual code instead of generated code. Creating and maintaining mappings is design-system work (`design-systems-consistency`); this skill only reads existing mappings. |
| When to use | The team already uses Code Connect and the question is "which code component should this feature have used". |
| When not to use | Do not require it. A missing mapping is not a readiness blocker and not evidence that no code component exists (connections can be absent, or deactivated for plan reasons); a written component map in the handoff is sufficient. Do not use it to reconcile a Figma component with its code component — that is Skill 05. |
| Runtime/load policy | Fetch only when current setup, behavior, or eligibility would change the answer. |
| Verified facts (re-checked 2026-10-21) | Code Connect is plan- and seat-gated; exact eligibility can change, so verify the current official Figma documentation when it matters. Two ways to connect are available: the **Code Connect CLI** (runs in the repository, supports property mappings, and can surface production-oriented code examples in Dev Mode) and the **Code Connect UI** (runs inside Figma and can map design components to code paths/repositories to improve Dev Mode and MCP context). Both contribute to Figma's Code Connect/MCP workflow. |
| Limitations | A mapping proves which components correspond; it does not prove behavior, states, or accessibility parity. |

---

## Category 4 — Engineering documentation and test tools (Tier 2, conditional on the team using Storybook)

### Storybook — How to test UIs — https://storybook.js.org/docs/writing-tests
### Storybook — Accessibility testing — https://storybook.js.org/docs/writing-tests/accessibility-testing

| Field | Detail |
|---|---|
| Authority | Official docs for the tool (re-checked 2026-10-21; the docs then current were version 10.6 — re-check if the version matters). Authoritative about Storybook, not about product QA. |
| Domain | Component state coverage, interaction tests, visual regression, automated accessibility checks, CI. |
| When to use | The engineering system uses Storybook. Then: use stories as the implemented state inventory to compare against the approved state inventory; use interaction tests as behavioral evidence; use the a11y panel as a first filter. |
| When not to use | Teams without Storybook. Never equate component tests with product usability testing; never treat a green a11y addon run as accessibility sign-off. |
| Runtime/load policy | Do not fetch by default. Fetch only for current configuration behavior. |
| Verified facts (re-checked 2026-10-21) | Test types documented: render (smoke), interaction (`play` function), accessibility, visual (Chromatic), snapshot (lower priority); stories can be reused in Playwright/Cypress/Vitest/Jest. **Storybook Test** runs stories as Vitest tests in browser mode via the Vitest addon (`@storybook/addon-vitest`); the test runner is the fallback. Accessibility addon `@storybook/addon-a11y` is built on axe-core, which the docs say "automatically catches up to 57% of WCAG issues"; results are split into Violations / Passes / **Incomplete** — Incomplete items must be confirmed manually. `parameters.a11y.test` can be `'off'`, `'todo'` (warn), or `'error'` (fail). Async components may be checked before they finish rendering, causing false negatives. By default the addon runs WCAG 2.0 and 2.1 A/AA rules plus best practices; WCAG 2.2 rules run only if the team configures them. |
| Limitations | Automated checks cannot judge accessible-name quality, focus management across views, announcement timing, or screen-reader comprehension. Manual verification remains required. Stories exercise components in isolation: a green run does not prove feature usability, full product accessibility, or production feature parity. |
| Licensing/access | MIT-licensed tool; public docs. |

---

## Category 5 — Token specifications (Tier 1, conditional on token parity mattering)

### DTCG — Design Tokens Format Module 2025.10 — https://www.designtokens.org/TR/2025.10/format/

| Field | Detail |
|---|---|
| Authority | Final Community Group Report of the W3C Design Tokens Community Group, dated 28 October 2025; the document states it "is considered stable". It is not a W3C Standard. |
| Domain | Interchange format and semantics for design tokens: structure, types, aliases, deprecation. |
| When to use | Token interchange between tools, questions about token semantics in a handoff (e.g., "is this alias resolving to the approved semantic token?"), or design/code token parity disputes where the file format is the evidence. |
| When not to use | Do not redesign the token architecture — route it to `design-systems-consistency` (Skill 05). Do not fetch to check an ordinary "raw value replaced a token" defect — that needs the team's token names, not the spec. |
| Runtime/load policy | Do not fetch by default. |
| Verified facts (re-checked 2026-10-21) | JSON files, recommended extensions `.tokens` / `.tokens.json`, MIME `application/design-tokens+json`. A token is an object with `$value` (required); `$type` optional but must be determinable from the token or an ancestor group; `$description`, `$extensions` (tools must preserve unknown extensions), `$deprecated` (boolean or string). Groups are objects without `$value`; group properties `$description`, `$type`, `$extends` (deep-merge inheritance; circular chains invalid), `$deprecated`, `$extensions`; reserved `$root`. Aliases: `{group.token}` curly-brace references resolve to a complete token's `$value`; `$ref` JSON Pointer references (RFC 6901) reach property-level values and are required for tools to support; circular references are errors. Types: color, dimension (px/rem), fontFamily, fontWeight, duration, cubicBezier, number; composite: strokeStyle, border, transition, shadow, gradient, typography. |
| Not verified | Theme/mode semantics were not present in the portion of the Format Module read; treat theme and mode behavior as the team's own convention (Figma variable modes, code theme layers) unless the team cites a specific DTCG resolver document. |
| Licensing/access | W3C Community Group document; freely readable. |

---

## Category 6 — External design-system exemplars (Tier 2)

| Field | Detail |
|---|---|
| Sources | IBM Carbon, Microsoft Fluent, Google Material (and Storybook as a tooling exemplar). |
| Authority | Mature professional models of component APIs, states, accessibility expectations, token naming, and documentation structure. |
| When to use | Only as a comparison point when the team's own system is silent and you need to show what a complete state set or accessible behavior for a component type usually includes — labelled as a model, never as the requirement. |
| When not to use | Never as the product's source of truth. Never to overrule the team's own component library or tokens. Never fetched by default. |
| Runtime/load policy | Do not browse. If a session offers an offline Carbon reference skill, prefer it over the web, and only when the team's system is silent. |
| Limitations | Different products, different constraints; their decisions do not transfer automatically. |
| Licensing/access | Apache 2.0 (Carbon, Material), MIT (Fluent); public documentation. |

---

## Category 7 — Build-time book knowledge (Tier 2; distilled, never a runtime dependency)

### Frank Lemser, *Technical Product Management according to Open Product Management Workflow™*, last updated September 2025 edition (proProduktmanagement GmbH)

| Field | Detail |
|---|---|
| Authority | Professional practice model for technical product teams. Supporting knowledge only. |
| Domain | Technical Product Team roles; precise requirements; work packages and dependencies; estimation confidence; prototypes/mock-ups; review meetings; approval; retrospective. |
| What was distilled (and where) | Role boundaries and "only involve roles needed" → `collaboration-and-change-management.md`. Vague-word avoidance and traceability story→requirement→evidence → `acceptance-criteria-and-specs.md`. "A work package solves its problem 100%; a feature with a missing main capability is not shippable" → readiness and severity logic. Estimation confidence labels (high/medium/low) and "the surprise is the problem, not the change" → technical-unknown labels and change logging. Review-meeting agenda (plan vs actual, requirements compliance, QA coverage of scenarios) and team approval with one accountable decision-maker → QA approval rules. Bidirectional information flow (step back to the story, then the requirement, then the evidence) → routing decisions back to the owning stage. Over-documentation as a symptom of distance from reality → "avoid documentation theater". |
| When to use | Never at runtime. The practices above are already in the reference files. |
| When not to use | Do not copy its organisational model (strategic PM / technical PM / product architect / concept developer / QA / technical writer) into every company; map to the roles the team actually has. Do not use its requirements-rating formula — prioritisation is not this skill's job. |
| Runtime/load policy | Not loaded. The skill must work without the PDF. |
| Limitations | Written for a product-manager audience and partly promotional for the author's tooling; the role split is one model among many. |
| Licensing/access | Published under CC BY-SA 4.0 (attribution required for reuse). This skill distils ideas and does not reproduce substantial passages. |

---

## Decision rule when sources conflict

1. Approved requirements and mandatory accessibility requirements win over current production behavior — flag the conflict, do not normalise it.
2. Production truth wins over exemplar systems and generic advice, always.
3. Official tool documentation wins over memory about the tool — if a tool detail would change the decision, verify it.
4. The owning discipline wins over this skill: if the conflict is a product or design decision, route it rather than settling it here.
