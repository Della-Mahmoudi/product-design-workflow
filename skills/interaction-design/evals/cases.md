# Interaction Design: evaluation cases

Human-readable QA contract for `interaction-design` (`interaction-design` of the Product Design system). Case N here is eval `id` N in `evals.json`.

- **Should this skill trigger?** is the routing expectation. This file does not measure it.
- For NO cases, the criteria describe what the skill must do **if it is invoked anyway** (manually or by misrouting): recognize the boundary, route to the primary owner, and stop.
- **Unnecessary-work checks** catch correct-looking work nobody asked for.

| # | Case | Trigger | Primary owner |
|---|---|---|---|
| 1 | Multi-file upload with partial failure | YES | `interaction-design` |
| 2 | Destructive workspace deletion | YES | `interaction-design` |
| 3 | Searchable multi-select | YES | `interaction-design` |
| 4 | Structural navigation problem | NO | `ux-architecture` |
| 5 | Visual styling | NO | `ui-visual-design` |
| 6 | Design-system component API | NO | `design-systems-consistency` |
| 7 | Prototype usability study | NO | `prototype-testing-analytics` |
| 8 | Implementation QA | NO | `delivery-product-collaboration` |
| 9 | Offline save and stale data | YES | `interaction-design` |
| 10 | Simple action stays simple | YES | `interaction-design` |

---

## Case 1: Multi-file upload with partial failure

**User prompt**
> Design the behavior for uploading 20 files at once. Some may succeed while others fail. Users need progress, retry and cancel.

**Should this skill trigger?** YES
**Primary owner:** `interaction-design`

**Expected behavior**
Standard or Deep mode (asynchronous, parallel, recoverable), so a formal model is warranted. Defines an aggregate batch state plus per-file states (queued, uploading, succeeded, failed, cancelled); reports partial failure per file and in aggregate; offers per-file Retry and "Retry failed"; defines Cancel for one file and for the batch and says what happens to files already uploaded; handles duplicate files and repeated activation; announces the batch outcome once; keeps focus on a sensible target when a file's control changes or a file is removed. Resumable upload, server-side abort, all-or-nothing vs best-effort and duplicate detection are treated as capabilities to confirm.

**Pass criteria**
- Per-file and aggregate states are both defined, in a state table or state diagram.
- Successes are kept; failed files stay listed with their reason; the aggregate reads like "17 of 20 uploaded, 3 failed".
- Retry exists per file and for all failed files.
- Cancel covers a single file and the whole batch, and states what happens to files already uploaded.
- Resumable upload and server-side cancellation are marked `[confirm: engineering]` or written as conditional.
- Duplicate files or a second activation of Upload have a defined outcome.
- The outcome is announced to assistive technology once, not per file or per percentage.
- Open technical dependencies are listed for confirmation.

**Failure criteria**
- Presents resuming an interrupted upload as an existing capability.
- Reports partial success as success, or drops failed files from view.
- Cancel silently discards files the user chose, or promises that server work stops.
- Chooses colors, spacing, typography or icon styling.
- Restructures the upload flow's steps or the product's navigation.

**Unnecessary-work checks**
- No visual mockup, layout or styling spec.
- No usability-test plan, analytics events or handoff checklist.
- No proposal for where uploading should live in the product.

---

## Case 2: Destructive workspace deletion

**User prompt**
> Define the interaction behavior for deleting a workspace that may have active projects, integrations and other members.

**Should this skill trigger?** YES
**Primary owner:** `interaction-design`

**Expected behavior**
Deep mode (destructive, multi-actor, high consequence). Rates the action high impact; checks preconditions first and separates blocking conditions (deletion cannot proceed until resolved) from warning conditions (consequences the user must acknowledge); confirmation names the workspace and lists concrete consequences for projects, integrations and members; typed-name confirmation; re-authentication only if existing product or security policy requires it; pending "Deleting" state, success with a defined landing place, and failure including part-way failure; Cancel before commit; reversibility and any restore window stay `[confirm]` with both branches designed if they change the behavior; permissions (who may delete, what others see, roles changing mid-task); what members inside the workspace experience; focus and announcements for the confirmation.

**Pass criteria**
- Blocking conditions and warning conditions are distinguished, and blockers are checked before the confirmation step.
- The confirmation names the workspace and its consequences; the destructive button names the action ("Delete workspace"), never "OK" or "Yes".
- Re-authentication is conditional on existing policy (`[confirm: security]` or equivalent), not a universal rule.
- Pending, success and failure states are defined, including where the user lands afterward.
- Cancel is defined before commit.
- Restore, undo, retention and grace periods are not asserted; each is marked to confirm.
- Permission behavior is specified at the moment of action, including a user who lacks permission.
- What other members see is specified as a product decision to confirm.
- Initial focus goes to the typed-confirmation field or the least destructive control; Cancel returns focus to the trigger.

**Failure criteria**
- States or implies that a deleted workspace can be restored without evidence.
- Invents backend deletion rules (retention periods, cascade order, legal holds) as facts.
- Uses a generic "Are you sure?" with OK and Cancel.
- Specifies danger-button colors, spacing or visual emphasis.

**Unnecessary-work checks**
- No redesign of the settings navigation.
- No component API for the dialog.
- No usability-test plan or handoff package.

---

## Case 3: Searchable multi-select

**User prompt**
> Define how a searchable multi-select should behave for keyboard, mouse and screen-reader users, including loading and no-results states.

**Should this skill trigger?** YES
**Primary owner:** `interaction-design`

**Expected behavior**
Standard mode for a web widget (assumption stated if needed). Native first: a checkbox group when the option set is small; otherwise an editable combobox whose popup is a multi-select listbox, citing both APG patterns because APG has no single pattern for this. DOM focus stays in the input (`aria-activedescendant`); arrows move the active option; Enter toggles because Space types; Escape closes and keeps selections; mouse click toggles and keeps the popup open; selections shown outside the popup as removable items with distinguishing names, with focus moving to a sensible target after removal; filtering as the user types; loading, no-results and error messages outside the listbox, announced through a status region; the results count announced politely.

**Pass criteria**
- The focus model is explicit, and the active option is distinguished from selection.
- Keyboard keys for moving, toggling and closing are specified, with selections kept on close.
- Selection and deselection work in the list and from the selected items outside it, with distinguishing accessible names.
- Filtering, loading and no-results behavior are specified, with their messages outside the listbox.
- Status changes are announced without moving focus.
- APG is used conditionally (Combobox plus Listbox), or a native control is preferred for small sets.
- WCAG criteria are named as "designed to support", never claimed as met.

**Failure criteria**
- Defines component properties, variant names or design tokens.
- Chooses colors, spacing or typography.
- Places "Loading", "No results" or a Retry button inside the listbox as options.
- Uses Space to toggle selection while DOM focus is in the text input.
- Claims WCAG conformance or completed testing.

**Unnecessary-work checks**
- No Apple, Material, Carbon or GOV.UK guidance unless the product uses that system.
- No usability-test plan.
- No design-system contribution proposal.

---

## Case 4: Structural navigation problem

**User prompt**
> Organize Account, Team, Billing, API and Security into a better settings navigation.

**Should this skill trigger?** NO
**Primary owner:** `ux-architecture`

**Expected behavior if invoked anyway**
Recognizes a hierarchy, grouping and navigation question, routes it to `ux-architecture` in a line or two, and stops. May add one line on what interaction design can specify once the structure is approved (for example, unsaved changes when switching sections).

**Pass criteria**
- Names `ux-architecture` as the owner.
- Explains that the open question is structural (grouping, order, navigation).
- Stops after routing.

**Failure criteria**
- Proposes groupings, an order, labels, a sitemap or a navigation pattern for the five areas.
- Produces a behavior specification instead of routing.

**Unnecessary-work checks**
- No state tables, state diagrams or behavior rules.
- No layout or visual suggestions.

---

## Case 5: Visual styling

**User prompt**
> Make the upload UI look more premium. Choose spacing, typography, colors, radius and visual hierarchy.

**Should this skill trigger?** NO
**Primary owner:** `ui-visual-design`

**Expected behavior if invoked anyway**
Recognizes a visual-design request, routes it to `ui-visual-design`, and stops. Any interaction note stays semantic (for example, upload states must remain perceivable without relying on color alone) and gives no visual values.

**Pass criteria**
- Names `ui-visual-design` as the owner.
- Gives no colors, type sizes or families, spacing, radius or visual-hierarchy values.
- Stops after routing.

**Failure criteria**
- Picks a palette, type scale, spacing scale, radius or shadow values.
- Produces a mood board or visual direction.
- Produces an unrequested behavior spec for the upload UI.

**Unnecessary-work checks**
- No state model for uploads.
- No design-token proposal.

---

## Case 6: Design-system component API

**User prompt**
> Our Select needs searchable, multiselect, destructive and compact variants. Define the reusable component properties and variant architecture.

**Should this skill trigger?** NO
**Primary owner:** `design-systems-consistency`

**Expected behavior if invoked anyway**
Recognizes reusable component architecture, routes it to `design-systems-consistency`, and stops. Offers behavior requirements for those capabilities only as input to `design-systems-consistency`, and writes them only if the user explicitly asks.

**Pass criteria**
- Names `design-systems-consistency` as the owner.
- States that properties, variants, tokens and governance are design-system decisions.
- Stops after routing.

**Failure criteria**
- Defines properties, property names, a variant matrix or component API.
- Defines tokens, contribution rules, versioning or deprecation.
- Writes full behavior specifications for each variant without being asked.

**Unnecessary-work checks**
- No visual spec for the variants.
- No usability-test plan.

---

## Case 7: Prototype usability study

**User prompt**
> We've built the delete-workspace prototype. Create a usability-test plan and moderator guide.

**Should this skill trigger?** NO
**Primary owner:** `prototype-testing-analytics`

**Expected behavior if invoked anyway**
Recognizes usability-test planning, routes it to `prototype-testing-analytics`, and stops. May name the behaviors worth validating (blocker handling, typed confirmation, keyboard and screen-reader use) as input, without designing the study.

**Pass criteria**
- Names `prototype-testing-analytics` as the owner.
- Contains no study artifacts.
- Stops after routing.

**Failure criteria**
- Writes a test plan, task scenarios, screener, moderator script, success metrics or sample size.
- Reports or invents usability findings.

**Unnecessary-work checks**
- No re-specification of the delete-workspace behavior.

---

## Case 8: Implementation QA

**User prompt**
> The developer built the multi-select. Compare staging against the approved interaction and tell me what is wrong.

**Should this skill trigger?** NO
**Primary owner:** `delivery-product-collaboration`

**Expected behavior if invoked anyway**
Recognizes implementation QA and parity checking, routes it to `delivery-product-collaboration`, and notes that the approved interaction specification is the behavioral source of truth for that check. Does not run the comparison.

**Pass criteria**
- Names `delivery-product-collaboration` as the owner.
- States that the approved interaction spec is the reference for the QA.
- Stops after routing.

**Failure criteria**
- Produces a defect or parity list for the staging build.
- Claims to have inspected staging, or invents discrepancies.
- Rewrites or redesigns the approved multi-select behavior.

**Unnecessary-work checks**
- No re-derivation of the full multi-select spec.
- No acceptance criteria or handoff package.

---

## Case 9: Offline save and stale data

**User prompt**
> A user edits a document while their connection is unstable and another teammate updates the same document. Define the interaction behavior.

**Should this skill trigger?** YES
**Primary owner:** `interaction-design`

**Expected behavior**
Deep mode (concurrent, asynchronous, recoverable). Defines states such as saved, unsaved changes, saving, offline, reconnecting or syncing, save failed and conflict; never silently overwrites the teammate's work or discards the user's edits; checks for a newer version before overwriting; offers only conflict options the system supports; shows connection and save status passively and in context; says on reconnection what synced and what didn't; announces status without moving focus. Offline storage, queued saves, conflict detection, merging, version history and real-time sync are marked as capabilities to confirm, with the fallback when they don't exist.

**Pass criteria**
- Online, offline, stale and conflict states are distinguished, in a state table or state diagram.
- Neither person's changes are silently lost.
- Feedback for losing and regaining the connection is defined, including what did and did not sync.
- Conflict handling offers only supported options; merge, versioning and real-time sync are `[confirm: engineering]` or conditional.
- Each technical capability is labeled as confirmed, assumed, proposed or needing validation, or the open dependencies are listed.
- Status changes are perceivable without color alone and announced without moving focus.

**Failure criteria**
- Assumes offline queueing, local drafts, automatic merging or real-time collaboration exist.
- Uses last-write-wins silently, or discards local edits on failure.
- Specifies a merge algorithm or versioning technology.

**Unnecessary-work checks**
- No navigation or document-structure redesign.
- No visual styling of the status indicators.
- No usability-test plan.

---

## Case 10: Simple action stays simple

**User prompt**
> Define the behavior of a standard Copy link button.

**Should this skill trigger?** YES
**Primary owner:** `interaction-design`

**Expected behavior**
Quick mode: a few behavior rules. A native button; activating it (click, tap, Enter, Space) copies the link; success feedback such as "Link copied" is announced through a status message while focus stays on the button; clipboard failure gets at most a line (for example, show the link selected so it can be copied manually).

**Pass criteria**
- Concise: a few rules, under about 250 words.
- States the action and its success feedback.
- Uses native button semantics.
- Success is announced without moving focus.

**Failure criteria**
- Produces a state machine, Mermaid diagram or multi-state table.
- Loads or cites unrelated platform or design-system guidance (Apple, Material, Carbon, GOV.UK).
- Specifies toast colors, icons, spacing or layout.
- Builds a custom ARIA widget instead of a native button.

**Unnecessary-work checks**
- No extended error-handling section.
- No analytics event, usability-test plan or design-system variant.
