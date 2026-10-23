# Ready for Dev and handoff

Read this for: "is this ready for dev?", handoff completeness, Ready-for-Dev manifests, and the
state, component, token, responsive, accessibility, content, permission, dependency, and
open-question inventories that make a feature implementable. Do not read the QA reference unless a
built product is also under review.

## Contents

1. What you are deciding
2. Step 0, inventory the inputs before judging anything
3. The Ready-for-Dev gate (18 checks, with blocker rules)
4. Scope completeness
5. Flow and state completeness (state inventory, edge-case inventory)
6. Component mapping
7. Token mapping
8. Responsive and adaptive requirements
9. Accessibility requirements (the accessibility contract)
10. Content readiness
11. Permissions and destructive behavior
12. Technical unknowns and dependencies
13. Analytics handoff
14. Open questions
15. The Ready-for-Dev manifest
16. Figma Dev Mode, when the team uses it
17. Avoiding over-documentation
18. Verdict rules and output shapes

---

## 1. What you are deciding

Whether engineering can build the approved design without inventing product behavior. The verdict
is one of `Ready`, `Ready with conditions`, or `Not Ready`. "Ready with conditions" means the
remaining gaps are either non-blocking documentation or questions that can be answered before the
affected part is built, and each condition names an owner. Visual polish is not evidence of
readiness; a complete default screen tells you nothing about error recovery, permissions, or
keyboard behavior.

Nor is a tool status. A Figma section marked *Ready for dev*, a ticket in a "ready" column, or any
other workflow flag records someone's intent; it does not show that the gate below passed. A
flagged design can be `Not Ready`, and a design can be `Ready` on a team that never uses such
flags. If the team uses Figma, set its status only after the design passes this gate (§16).

## 2. Step 0, inventory the inputs

Before any check, write down what was actually supplied and what was not. Readiness judgments made
on imagined inputs are the most common failure of this task.

| Input | Supplied? | Where / version |
|---|---|---|
| Approved design artifact (file, page, section, version; any tool status is metadata, not evidence) | | |
| Approved flow(s), including alternate and failure paths | | |
| Interaction spec / annotations | | |
| Design-system component library (design side) and production component library (code side) | | |
| Token/variable set (Figma variables, code tokens) | | |
| Repository / Storybook / API contract / backend constraints | | |
| Product requirements, ticket(s), Definition of Done | | |
| Accessibility requirements the team has adopted (e.g. WCAG 2.2 AA, platform guidance) | | |
| Analytics tracking plan (already defined by `prototype-testing-analytics`) | | |
| Known technical constraints confirmed by engineering | | |
| Open developer / PM questions | | |

Everything not supplied is unknown. Say so. Do not reconstruct missing flows or states yourself -
that is design work for the owning stage; your job is to name what is missing and why it blocks.

## 3. The Ready-for-Dev gate

Run only the checks that apply to this feature (a read-only list has no destructive flow; a
single-platform internal tool may have no responsive story). For each applicable check decide:
**pass**, **blocker**, or **non-blocking gap**.

| # | Check | Passes when | Blocker when | Not a blocker when |
|---|---|---|---|---|
| 1 | Scope is explicit | A developer can say what is in and out of this delivery | The boundary is unknown and would change what gets built | Scope is clear but the ticket wording is clumsy |
| 2 | Included/excluded behavior is understandable | Exclusions are written, not implied | "Later" behavior is indistinguishable from "now" behavior | Exclusions are listed in a comment rather than a field |
| 3 | Main flow is defined | Entry, steps, exit, and success are shown or described | The success outcome itself is undefined | Minor step ordering can follow an existing pattern |
| 4 | Important alternate flows are defined | Cancel, back, retry, partial completion, interruption are covered where they exist | A common alternate path (e.g. cancel mid-save) has no defined outcome | A rare path can follow an established product convention |
| 5 | Required states are defined | See §5, every state that changes what the user sees or can do | A state the user will certainly hit (loading, empty, error) is missing | A transient visual state already defined by the component |
| 6 | Components map to real system components | Each element names the system component and variant/props it uses, or is explicitly custom | A critical element has no mapping and its behavior is undefined | A minor element is "Button, primary" and the system already defines it |
| 7 | Token usage is clear | Semantic tokens are applied in the design and no raw values hide where tokens exist | A new visual needs tokens that do not exist and nobody owns the decision | Spacing is visible via inspection and uses existing tokens |
| 8 | Responsive/adaptive behavior is defined | The product's breakpoints are named and transformations described | Layout at a supported breakpoint is unknown and the component system does not resolve it | The system's grid and component rules already determine it |
| 9 | Accessibility behavior is defined | §9 contract items relevant to the feature are written | Keyboard, focus, or semantics for a custom interaction are undefined | Standard system components carry the behavior already |
| 10 | Content is final or labelled provisional | Every string is classified (§10) | Behavior depends on unknown content (e.g. error message wording that implies recovery) | Marketing copy pending but layout-safe |
| 11 | Empty/loading/error/success states exist where required | Present for data-dependent views | Missing on a data-dependent view | Not applicable to static content |
| 12 | Permission/role behavior exists where required | Each role's visible and allowed actions are defined | A role can reach the feature and its experience is undefined | Single-role product |
| 13 | Destructive behavior is defined | Confirmation, reversibility, consequences, and recovery are explicit | Any destructive action lacks defined confirmation or outcome | No destructive actions |
| 14 | Technical unknowns are recorded | §12 list exists with classification | A UX-shaping unknown (reversibility, real-time, retry) is unlabeled | Unknowns exist but do not change the UX |
| 15 | External dependencies are visible | APIs, services, other teams, feature flags, content, legal/compliance | A dependency blocks the user-facing behavior and has no owner | Dependency is tracked elsewhere and linked |
| 16 | Analytics requirements linked (if already specified) | Tracking-plan events relevant to this feature are referenced | Defined events are missing from the handoff so they would be silently dropped | No tracking plan exists (note it; do not invent one) |
| 17 | Acceptance criteria are testable | Each criterion is observable (see the AC reference) | Criteria are of the form "should work correctly" | Criteria need tightening but intent is clear |
| 18 | No open product/design decisions disguised as dev details | Open decisions are listed as open | A product decision is hidden in a comment like "dev can choose" | Decision is genuinely an implementation detail |

Hard blockers (any of these alone makes the verdict `Not Ready`): required behavior unknown; an
important state missing; destructive flow undefined; permissions behavior undefined; responsive
behavior unknown for a supported viewport; a critical component unmapped; required accessibility
semantics undefined; keyboard/focus behavior undefined for a custom interaction; error-recovery
behavior undefined; an unresolved product decision; an unresolved technical dependency that
changes the user experience.

Not blockers: 8px vs 12px uncertainty where the system token rule decides; icon choice within an
approved set; copy polish on labels whose meaning is settled; anything an established
design-system rule resolves deterministically. A missing annotation is a blocker only when it
hides one of the hard-blocker decisions above; otherwise it is at most a non-blocking gap.

When a blocker is an unmade decision, classify it `Product/design decision required` (`Missing
design decision` when the behavior was never defined), name its owner (the owner routing table in
SKILL.md), and leave it open. Do not fill it in to reach `Ready`, a guessed behavior written into
the handoff becomes the product by default.

## 4. Scope completeness

Write scope as two lists that a developer and a tester would both read the same way.

- **Included:** the user-facing capabilities, the platforms, the roles, the entry points, the
  states, and the data conditions this delivery covers.
- **Excluded (and where it lives):** anything a reasonable developer might assume is included -
  bulk actions, export, mobile, admin variants, localisation, offline, with a pointer to the
  ticket or decision that defers it.

Scope ambiguity shows up later as "I thought that was part of it". If the brief is "saved
searches", ask whether editing, renaming, sharing, deleting, and limits are in, and record the
answer, not an assumption.

## 5. Flow and state completeness

### State inventory

For each screen, view, or interactive component, walk this list and mark each state as
*defined*, *not applicable*, or *missing*. A missing state that a user will certainly reach is a
blocker.

| State family | Typical members |
|---|---|
| Baseline | default, populated, focused/active, selected, disabled |
| Data lifecycle | loading (initial, incremental, refresh), empty (first-use, filtered-to-nothing, no-permission), partial/degraded |
| Outcome | success (inline, toast, navigation), duplicate/conflict, validation error (field, form), network/server error, timeout |
| Progress | saving/optimistic, in-progress with cancel, interrupted, retry |
| Access | permission-denied, read-only role, feature-flag off, plan/tier gating |
| Destructive | confirm, in-progress, undone/restored, irrecoverable |
| Context | offline, slow network, stale data, concurrent edit |

Ask of each missing state: "Will a real user hit this in the first week?" If yes, it is required.

### Edge-case inventory

Content extremes (zero, one, many, very long strings, missing optional fields), concurrency (two
tabs, two users), timing (slow response, double-submit), interruption (navigate away mid-save,
session expiry), input (paste, IME, autofill), locale (date, number, RTL, pluralisation), and
device (small viewport, zoom at 200%, touch vs pointer). Record only the ones that change
behavior or layout; the rest follow product conventions.

## 6. Component mapping

Map every meaningful element to the real reusable component, not to a generic name.

```
element: "Save search" action
system component: Button
variant/props: kind=primary, size=md, icon=none, loading=true while saving
notes: disabled until the name field is valid; see AC-4
```

Rules that keep this honest:

- Map to the **production** component library where it differs from the design library; note
  the gap when the design library has a variant the code does not.
- Mark anything custom as `custom` with the reason (no existing component covers the behavior;
  system owner informed). Do not disguise a custom build as a system component.
- When a needed variant or behavior is missing from the system, record it as a design-system
  request for `design-systems-consistency` / the system owner, do not design the
  extension here.
- If Code Connect mappings exist, cite them; if not, the written map is enough.
- You check which component this feature uses. Whether the reusable component's Figma and code
  versions match each other (props, variants, states) is system parity, route it to `design-systems-consistency`.

## 7. Token mapping

Token checks here are about whether the **approved semantics survive** in this feature, not about
token architecture or whether token definitions match across design and code
(`design-systems-consistency`).

- Every colour, type, spacing, radius, elevation, and motion decision in the handoff references
  the semantic token the system defines for that purpose (e.g. `surface.action.primary`), not a
  raw value and not a primitive the semantic layer is supposed to hide.
- Raw values are a finding: either the token is missing (route to `design-systems-consistency`) or the design drifted.
- Theme/mode behavior (light/dark, brand, density) is defined by the token set; confirm the
  feature introduces nothing that bypasses it.
- Use the DTCG format only when token files are exchanged between tools or a parity dispute hinges
  on the file semantics (`$value`, `$type`, aliases `{group.token}`, `$deprecated`).

## 8. Responsive and adaptive requirements

Name the product's own breakpoints (never invent names like "tablet" if the system says
`compact`/`medium`/`wide`). For each supported breakpoint state what transforms: what stacks, what
collapses into a menu, what hides and where it goes, what keeps priority (the primary action must
remain reachable without horizontal scroll), minimum target sizes, and text wrapping rules for
long content. If the system's grid and component rules already determine the layout, say so in
one line instead of redrawing every breakpoint.

## 9. Accessibility requirements, the accessibility contract

Write the contract at the level a developer and a tester can act on. Standard system components
carry most of it; write explicitly only what the feature adds or customises.

| Area | What to define |
|---|---|
| Semantics | element roles (button vs link vs menuitem), landmarks, headings, list/table structure |
| Names | accessible names for icon-only controls, images, custom widgets; label associations for fields |
| Keyboard | every action reachable; expected key behavior for custom widgets (arrow keys in a listbox, Escape to dismiss) |
| Focus | initial focus on open, focus order, focus trap for modals, focus restoration on close/delete, visible focus (and not obscured by sticky UI) |
| Announcements | live-region messages for save success, errors, async results; error identification wording |
| Contrast | text and non-text contrast checked at design level against the team's target (e.g. WCAG 2.2 AA) |
| Targets and motion | minimum target size; reduced-motion behavior for any animation |
| Platform | VoiceOver/TalkBack specifics for native; dynamic type |

If any of these is undefined for a custom interaction, it is a blocker, this is exactly the
behavior that disappears in implementation when nobody wrote it down. Mark it `Missing design
decision` and route the behavior to `interaction-design`; do not write the missing keyboard or
focus model yourself (for example, where focus goes after Cancel). If an approved system
component contract already defines the behavior, cite it, that is not a gap.

## 10. Content readiness

Classify every string that affects layout or behavior: **Final**, **Approved placeholder**,
**Dynamic** (from data; define min/max and empty case), **User-generated** (define length limits,
sanitisation display, truncation), **Backend-provided** (e.g. error codes, define mapping to
user-facing messages or mark unknown), **Localization-dependent** (expansion, RTL), or
**Unknown**. Lorem ipsum anywhere behavior-relevant is `Unknown` and must not ship as content.
Where content materially affects layout, test realistic cases (longest real product name, a
20-item list, a 2-character label).

## 11. Permissions and destructive behavior

- For each role or permission level: what is visible, what is actionable, what is disabled vs
  hidden, and what message appears on a denied action. Note whether the check happens
  client-side, server-side, or both, if unknown, label it `requires engineering confirmation`.
- For each destructive action: trigger, confirmation pattern, consequence statement, reversibility
  (undo window? restore? none?), what happens to dependants (shared items, other users), and
  recovery path. "Delete is reversible" is a technical claim, do not assert it without
  confirmation.

## 12. Technical unknowns and dependencies

Keep one list. Each entry: statement, classification (`Confirmed` / `Proposed` / `Assumed` /
`Requires engineering confirmation` / `Blocked`), UX impact if the answer is unfavourable, owner,
needed-by. Examples that are unknown until confirmed: API supports retry; operation is
reversible; data updates in real time; deleted items are recoverable; permission check location;
optimistic updates are safe; duplicate detection exists; limits (max saved items, name length).

Dependencies: external APIs, other teams' work, feature flags, content delivery, legal review,
design-system additions. Each with owner and status. A dependency that changes the user-facing
behavior and has no owner is a blocker.

## 13. Analytics handoff

`prototype-testing-analytics` defines the measurement contract: metrics, event names
and semantics, triggers, properties, funnels, experiment measurement. Here, only check that
already-defined requirements are carried into the handoff: event names, trigger points (attempt
vs success, "save clicked" is not "search saved"), required properties, privacy constraints, and
that each is referenced in an acceptance criterion. If no tracking plan exists, record "no
analytics requirements supplied", do not invent events or metrics. Verifying that the build
implements the contract is implementation QA.

## 14. Open questions

One list, no hidden questions inside annotations.

```
Q-3 | Can a user save a search whose name duplicates an existing one? | owner: PM | blocking: yes (affects duplicate state + AC-6) | needed by: before sprint start
```

Distinguish *blocking* (changes what is built) from *non-blocking* (can be answered while adjacent
work proceeds). Product decisions belong to PM/design, technical ones to engineering; do not
answer either on their behalf.

## 15. The Ready-for-Dev manifest

Use for features with multiple states, platforms, roles, or dependencies. Skip it for a single
component tweak or a one-question handoff, a manifest nobody needs is documentation theater.

```yaml
feature: saved-search
version: 1.4
status: ready-for-dev          # this skill's verdict, not a tool status; or: not-ready | ready-with-conditions
platforms:
  - responsive-web
design:
  artifact: <file / page / section / version>   # a tool status, if used, is metadata only
scope:
  included: [create, rename, delete, apply saved search]
  excluded: [share with others (ticket PX-412), limits UI (pending Q-5)]
components:
  - SearchFilters
  - Button
  - Toast
  - SavedSearchCard
states:
  - default
  - saving
  - success
  - duplicate
  - network-error
  - permission-error
  - empty
responsive:
  compact: defined
  medium: defined
  wide: defined
accessibility:
  keyboard: defined
  focus: defined
  announcements: defined
  contrast: checked-at-design-level
content:
  status: final            # or: provisional (list items)
analytics:
  tracking_plan: linked    # or: none-supplied
technical_unknowns:
  - "duplicate names rejected server-side, requires engineering confirmation"
dependencies:
  - "search-service v2 endpoint, owner: platform team, status: in progress"
open_questions:
  - Q-3 (blocking)
```

Every `defined` must be true in the artifact; the manifest is a summary of evidence, not a
promise.

## 16. Figma Dev Mode, when the team uses it

Apply only if the team hands off in Figma. Figma is optional: nothing in the gate depends on it,
and handoff can live entirely in tickets and specs. Features and plan availability change; if a
detail matters, check the current page (see the source map).

- **Status is workflow metadata, not readiness.** If the team uses Figma, its *Ready for dev*
  status may be used as workflow metadata after the design passes the team's readiness criteria
  (the gate above); attach a status note with scope and links to the ticket/AC if the team uses
  notes. A section that is already marked can still be `Not Ready`, run the gate rather than
  trusting the mark.
- **Changes after handoff.** The rule is tool-independent: any material change after handoff is
  surfaced, recorded in the change log (collaboration reference), and synchronized with
  implementation. Figma can flag later edits to a marked design and lets developers compare
  versions; where the team's plan offers this, treat it as an aid for spotting edits, never as the
  record.
- **Sections.** If the team hands off in sections, keep exploration out of the handed-off section
  so developers see only the approved design.
- **Annotations and measurements.** Use annotations for intent that inspection cannot show
  (behavior, content rules, accessibility, responsive transforms, constraints). Measurements and
  token values are already available in the Inspect panel and the Variables view, do not
  duplicate them.
- **Variables.** Developers see applied and suggested variables; confirm the applied ones are the
  approved semantic tokens, not primitives or detached values.
- **Code Connect.** If the team uses it, CLI connections show the team's real code snippets in
  Inspect; UI connections show file/component references and AI-generated previews. Absence of a
  mapping is not a readiness blocker; a written component map is enough. Creating or fixing
  mappings is design-system work (`design-systems-consistency`).
- **Resource links** (Jira, Storybook, GitHub) on components propagate to instances, link the
  story or ticket rather than describing it in prose.

## 17. Avoiding over-documentation

Document only what engineering cannot safely infer from existing components, tokens, platform
behavior, and responsive rules. Good annotations carry intent: non-obvious behavior, content
rules, accessibility requirements, responsive transformations, unusual constraints, edge cases,
technical dependencies. Do not annotate every gap, every colour, or standard component behavior.
Do not write a flow document for a one-line behavior. The test: would a competent developer on
this team build it wrong without this note? If not, cut it.

## 18. Verdict rules and output shapes

- `Ready`, all applicable checks pass; open questions are non-blocking with owners.
- `Ready with conditions`, no hard blocker; remaining gaps are listed with owner and the point
  before which each must be resolved.
- `Not Ready`, at least one hard blocker. List blockers first, then important non-blocking
  gaps, then the minimum unblock plan (who must supply what). Do not fill the gaps yourself.

**Quick mode output**

```
Verdict: Not Ready
Blocking (must resolve before build):
  1. ...
Important, non-blocking:
  1. ...
Next action: ...
```

**Standard mode output**, only the relevant of: Scope · Readiness verdict · Missing states ·
Component/token mapping · Responsive expectations · Accessibility expectations · Content status ·
Technical unknowns · Dependencies · Open questions · Acceptance-criteria pointers.

**Deep mode** adds the manifest and the full inventories, only when the delivery size justifies it.
