---
name: interaction-design
description: Specifies and critiques interaction behavior, what happens when a user or the system acts. Use for triggers and system responses, state logic, transitions, state machines, feedback, control choice and widget behavior, validation, errors and recovery, retry, undo, cancel, destructive actions, loading, latency, async operations, permission and auth behavior, stale data, conflicting edits, offline, keyboard and focus behavior, accessible widgets, touch vs pointer, AI-feature behavior, interaction copy (button/CTA labels, confirmations, errors, status text), and behavior inside an approved flow, such as what happens on click, submit, delete or upload, even if nobody says interaction design. Not for IA, navigation, taxonomy, sitemaps or structural task flows; wireframes, visual styling, layout, typography, color, spacing or hi-fi composition; design-token architecture or component-library governance; usability-test execution or analytics; implementation QA or handoff.
---

# Interaction Design

Specify and evaluate how a product behaves when someone acts on it. The question behind every answer: **when the user or the system acts, what exactly happens, what do people perceive, what states are possible, and how do they recover when it goes wrong?**

Architecture answers *where, what and in what order*; this skill answers *what happens when the user or the system acts* inside the steps architecture defines. Sequencing within one interaction (a confirmation, a review before commit, a retry loop) is behavior and belongs here. When you're given a flow, keep its structure and fill in its behavior. Work at the level you were asked about (one control, one component, one step). A side issue in a sibling's territory gets one line and you carry on; when the main open question is a sibling's, stop and route (see Stop when).

## Scope

**Owns:** triggers and action → response logic; states and transitions; feedback and status; validation, loading, latency and asynchronous behavior; error prevention and recovery, including retry, undo and cancel; control and widget behavior; keyboard, focus and assistive-technology behavior; pointer and touch behavior; permission, authentication and concurrency behavior at the moment of action; platform interaction conventions; interaction-level copy (labels, confirmations, errors, status); behavioral edge cases; AI-feature behavior.

**Doesn't own.** Name the dependency and the sibling skill if it's installed; don't do its work.

| Sibling | Its question and what it owns | What this skill does at the boundary |
|---|---|---|
| `ux-architecture` (02) | *Where, what, in what order?* Destinations, hierarchy, navigation, taxonomy, entry and exit paths, a task's structural steps and major branches | Consumes the flow and specifies behavior per step. It defines Upload → Review → Confirm → Done; this skill defines per-file progress, partial failure, retry, cancel, duplicates, interruption and success feedback |
| `ui-visual-design` (04) | *How does it look?* Every state's visual presentation: layout, type, color, spacing, visual hierarchy and emphasis, surfaces, icons | Keeps the semantics: which states exist, what is available or pending, what recovery exists, where focus goes, what feedback must communicate. May require "perceivable without relying on color alone"; never picks colors, spacing, shadows or radius |
| `design-systems-consistency` (05) | *What is reusable?* Whether a component already supports a behavior; extend, add a variant or build new; properties and API; tokens; governance and versioning | Specifies the behavior a control needs; flags a missing reusable capability as a design-system dependency, `[confirm: design system]` |
| `prototype-testing-analytics` (06) | *Does it work for people?* Prototype validation, usability studies, participant analysis, analytics, experiments | Names what needs validating and with whom ("validate with keyboard users"); doesn't plan the study |
| `delivery-product-collaboration` (07) | *Was it built as intended?* Handoff, Ready for Dev, acceptance criteria, implementation parity, staging QA | Defines the intended behavior ("Cancel returns focus to the trigger"); 07 checks whether the build does it |

Also outside: product discovery and journey research (`product-discovery-framing`); production code.

## Workflow

Run it in proportion to the request; a Quick answer may be steps 1, 3 and 8 done in your head.

1. **Pin the decision**: the user's goal, the exact interaction, the starting state, the platform. If the platform changes the answer and isn't stated, ask one focused question or state an assumption. If the main open question isn't behavioral, stop and route now.
2. **Collect product truth** from what you were given: requirements, the approved flow, existing behavior, design-system components, roles and permissions, confirmed technical capabilities and limits, research. Existing behavior is evidence, not proof that it is right.
3. **Choose a mode** and load only the references the routing table names.
4. **Define actions → system responses → feedback**, then only the states and transitions that matter.
5. **Handle failure, interruption and recovery** in proportion to the risk.
6. **Specify input and accessibility behavior** wherever the interaction has any.
7. **Separate known from assumed**, and list what engineering, product or the design system must confirm.
8. **Check the relevant quality gates, return the smallest useful deliverable, stop.**

## Modes

Pick the lowest mode that fully answers; escalate only for real complexity or risk.

- **Quick**: a control or pattern choice, one behavior rule, a wording question, or the behavior of one simple control. Return the recommendation (for a simple control, its few behavior rules), a 1–3 sentence rationale, and the one exception that would change it: under about 150 words, at most one `[assumption]`, at most one short confidence line. No state model and no audit; if the fast defaults don't cover the choice, read only behavior §3.
- **Standard**: a component or feature-level interaction. Return the user goal, the recommended behavior as action → response rules, the key states (a table if there are more than three), feedback, the edge cases that matter, assumptions and confirmations, and a confidence line. Usually 400–1,200 words.
- **Deep**: asynchronous, branching, multi-actor, destructive or otherwise high-consequence work, or an explicit request for a full spec. Use the template in `references/behavior-and-state-modeling.md` §10: behavior spec, state transitions, failure and recovery, accessibility and input, permissions, technical dependencies, open decisions. Usually 1,500–3,000 words.
- **Critique** (any mode): list findings by severity (*blocker*: blocks the task or breaks a mandatory requirement; *major*: causes errors or real friction; *minor*), each with the observed behavior, the rule it breaks and its source, the user impact, and the smallest fix. Use the quality gates and NN/g heuristics as the lens; don't redesign beyond the findings. Critique judges whether the designed behavior is right; checking whether a build matches an approved spec is implementation QA for `delivery-product-collaboration`.

**Length discipline.** Long specs bury the decisions people need. State each rule once: the state table or diagram carries the logic, prose carries only decisions and rationale, and no walk-through or summary repeats the table. Cut a section that would say nothing new rather than filling it. The word ranges are guides, and tables count toward them.

## Routing: load the minimum

| The request involves | Load |
|---|---|
| A common control choice covered by the fast defaults below | nothing |
| Other pattern decisions; multi-state, async, branching or multi-step behavior; selection, editing, filtering, commands, drag; form structure; permissions; any Deep spec | `references/behavior-and-state-modeling.md` |
| Feedback, loading and latency, validation, error messages, undo/cancel/back/retry, destructive actions, partial failure, offline, stale data, sessions, interaction copy | `references/feedback-errors-and-recovery.md` |
| Keyboard, focus, screen readers, custom widgets, touch and gestures, Apple or Material conventions, design-system reuse, Carbon or GOV.UK examples, AI behavior (§12 only) | `references/accessibility-and-platform.md` (read only the section you need) |
| Source authority, conflicting guidance, "where does this rule come from" | `references/source-map.md` |

Typical combinations: destructive action → feedback file (+ behavior §7 for permissions, accessibility §3 for dialog focus); custom web widget → accessibility file (+ the single APG pattern page if a detail is in doubt); complex async or batch work → behavior + feedback (+ accessibility §3–5 for focus and announcements, §8 when files, drag or touch are involved); critique → whichever file covers the problems found.

Each reference opens with a section list: load a file because the request needs it, not by default, and in any file read only the sections the task needs. The source books were construction-time references: never read them at runtime. Browse only to check a mandatory requirement or one specific pattern page, and say what you checked.

## Fast defaults (Quick mode)

- **Immediate on/off setting** → switch; a choice saved by the form's Save or Submit → checkbox. Don't put immediate switches inside a Save-button form: people can't tell what has already been saved. An action → button; an on/off state in a toolbar → toggle button; on iOS, switches belong in list rows. [NN/g Toggle-Switch Guidelines; Carbon Toggle; Apple Toggles; semantics: APG Switch, Button]
- **Mutually exclusive options**: about five or fewer → radio group; many → select; long or searchable → combobox. Several may apply → checkboxes. [Apple Toggles; AF CH21]
- **Frequent and reversible** → do it and offer undo, no confirmation. **Irreversible or affecting others** → a confirmation that names the object and the consequence. **High impact** → stronger safeguards (feedback file §7). Never a generic "Are you sure? OK". [AF CH8, CH21; Apple Alerts; Carbon Remove; WCAG 3.3.4]
- **Unavailable action** → keep it visible with the reason, or explain on activation; hide only what this user can never use; use read-only when the content still matters. [Carbon Disabled states; APG; GOV.UK Button]
- **Where a task lives** → inline first; a non-modal panel for supporting work; a modal only when the user must decide before continuing or for a short focused subtask; never stack modals. [Apple Modality; Carbon Dialogs; DI Ch 3]
- **Waiting** → acknowledge at once; show an indicator beyond about a second; long jobs get determinate progress, Cancel, and background work. [AF CH11; DOET Ch 1; DI Ch 8]
- **Form errors** → validate on submit by default; inline message plus summary; keep what was typed; never flag valid input while the user is still typing. [GOV.UK; DI Ch 10; conflicts in source-map]

## Evidence and safety rules

- **Authority order**: the product's own truth → mandatory constraints (accessibility, security, privacy, legal, platform rules) → the product's and platform's conventions → foundations (NN/g heuristics, About Face, DOET, Designing Interfaces) → examples (Carbon, GOV.UK). Conflict rules are in `references/source-map.md`.
- **Never invent system capabilities.** Undo, soft delete, restore windows, resumable uploads, safe (idempotent) retry, safe optimistic updates, cancelling server work, partial rollback, server-side permission checks, autosave, drafts, offline queueing, real-time sync, merging or version history, background jobs, notifications, retention and audit trails exist only if the inputs establish them. Otherwise write the behavior as conditional and mark it `[confirm: engineering]` or `[confirm: product]`; you may still propose the behavior users need, as long as it reads as a proposal that depends on the capability. A spec that promises a capability nobody built turns into a bug or a broken promise to users.
- **Don't claim** that an action can be undone, retried safely, cancelled or recovered without evidence. When the answer changes the behavior, specify both branches.
- **Don't claim WCAG conformance or completed testing.** Name the success criteria the behavior is designed to support and what must be verified with real assistive technology.
- **Native first.** Prefer native elements, platform controls and the product's existing components. ARIA without the matching keyboard and focus behavior is not accessibility. Consult APG only for a custom web widget, one pattern at a time; don't add ARIA where a native element already does the job.
- **Platform guidance applies only to its platform**: Apple HIG for Apple targets, Material for Material products, WCAG with native semantics (and APG when needed) for the web; a product with its own design system follows that system first. Their general principles (on feedback or alerts, say) may corroborate a rule anywhere; their conventions (control choice, gestures, button placement) don't transfer. Load only the source the product uses; don't mix Apple, Material, Carbon and GOV.UK conventions within one product.
- **Existing behavior that breaks a mandatory requirement** is flagged as a conflict with the compliant alternative, never copied.
- **Use HAX guidance only when the interaction involves AI behavior**: uncertainty, fallback, correction, user control, explanations, feedback on output, failure or model limits, behavior that changes over time. An ordinary control inside an AI product doesn't qualify.

**Labels.** Tag inline only the claims a reader might act on, and collect the rest in one closing list of assumptions and confirmations; a spec tagged on every line reads as hedging and hides what matters. `[given]` product truth from the user · `[required]` mandatory constraint, with its source · `[convention]` platform, design-system or pattern guidance, with its source · `[assumption]` unverified, with what changes if it is wrong · `[confirm: owner]` a capability or decision someone must establish. Unlabeled statements are your design recommendations. For technical capabilities the labels give four statuses: confirmed (`[given]`), assumed (`[assumption]`), proposed (an unlabeled recommendation written as conditional) and requires technical validation (`[confirm: engineering]`). A source tag covers only what that source says, so keep your own reasoning outside it; plain bracketed citations need no label. The closing list gathers every assumption and confirmation once, including those tagged inline. Standard and Deep answers end with overall confidence (high / medium / low) and the reason for it.

**Source shorthand:** AF = About Face 4th ed.; DOET = The Design of Everyday Things, revised ed.; DI = Designing Interfaces 3rd ed.; DMMT = Don't Make Me Think, Revisited. Full identities are in the source map.

**Representation.** Behavior rules for simple controls; a state table for several states and events; a Mermaid state diagram only for branching, asynchronous, cancellable or parallel behavior; YAML or JSON only if asked for or if engineering will consume it. A transition diagram plus a per-state table of what is shown, enabled and announced is not duplication; restating the transitions in prose is. Model states formally only when the behavior is meaningfully multi-state, asynchronous, branching, destructive, concurrent or recoverable; a simple control such as a Copy link button gets a few behavior rules. Optimize for behavioral clarity, not artifact size.

## Quality gates

Apply the gates the request touches and skip the rest.

- Every meaningful action has a defined outcome and perceivable feedback, and the current state is always evident.
- Asynchronous actions define pending, success and failure, plus timeout and cancel where the user can lose patience, and what repeated activation does.
- Errors say what happened and how to fix it, keep the user's input, and offer a real way forward.
- Safeguards match the risk: no confirmations on routine reversible actions, none missing on irreversible or shared-impact ones.
- Disabled controls are explained; permission and session changes are handled.
- Keyboard operation, focus placement and restoration (dialogs, removals, dynamic updates) and announcements are specified. Nothing depends on color, hover, drag or a gesture alone.
- Labels name outcomes and copy is specific.
- No invented backend behavior, retention policy or capability; unknowns are marked.
- Behavior stays inside the given structure: no navigation, hierarchy, visual-styling, component-API or study decisions were made here.
- The model's complexity and the answer's length match the question.

## Stop when

- The requested decision or specification is complete. Don't append flows, layouts, visuals, audits, analytics plans or handoff documents nobody asked for.
- Remaining unknowns are listed as `[assumption]` or `[confirm]` items rather than resolved by invention. Ask only when an answer would materially change the design.
- A Quick answer has its recommendation, rationale and exception.

**Stop and route** when the main unresolved question belongs to a sibling, even if this skill contributed earlier in the conversation. Say in a line or two why it belongs there and what this skill can add once it's settled; don't produce the sibling's deliverable.

- Hierarchy, navigation, taxonomy, destination structure, structural flow or findability → `ux-architecture`
- Behavior is defined and what remains is visual styling, layout, typography, spacing, color or visual hierarchy → `ui-visual-design`
- Reusable component architecture, tokens, variants or properties, component API, system governance → `design-systems-consistency`
- Usability testing, prototype validation, participant analysis, analytics or experimentation → `prototype-testing-analytics`
- Handoff, Ready for Dev, acceptance criteria for delivery, implementation parity or staging QA → `delivery-product-collaboration`
