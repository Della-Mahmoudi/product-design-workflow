# Implementation QA and parity

Read this for: reviewing a built implementation (staging, PR, Storybook, screenshots, recordings,
a running build) against the approved design, judging whether the feature used the approved
components and tokens, verifying an implemented tracking plan, and giving a design QA verdict.
Use Storybook, Figma, or code references only when they are supplied or clearly relevant.

Scope: feature build ↔ approved feature design. Parity between system objects, a Figma component
vs its code component, props, token definitions, Storybook vs library, belongs to
`design-systems-consistency`.

## Contents

1. What design QA is (and is not)
2. Step 1, fix the baseline and the build under review
3. Step 2, evidence rules: report only what you inspected
4. QA dimensions and how to check each
5. Component parity (custom vs system)
6. Token parity
7. Storybook comparison, when the team uses it
8. Figma / code comparison, when the team uses Figma
9. The issue record: expected vs actual
10. Categories for implementation differences
11. Severity: BLOCKER / MAJOR / MINOR / POLISH
12. Regression risk
13. Design QA verdict (not the release decision)
14. Report shapes
15. Things that are not defects

---

## 1. What design QA is

Design QA checks whether the **approved intent survived implementation**: behavior, states,
semantics, components, tokens, layout, responsive behavior, content, accessibility, and (where
defined) analytics. A screenshot comparison catches a fraction of this. Two builds can be
pixel-identical in the default state while one has no keyboard access, loses the user's input on
error, bypasses every semantic token, and fires analytics on the wrong trigger. Treat "looks
almost identical to Figma" as a statement about one state at one viewport in one theme, useful,
and insufficient.

Design QA also is not a claim of full accessibility conformance. Report what you verified, with
what, and leave the conformance statement to a proper audit. Nor is it redesign: when QA shows the
approved design itself is the problem (too dense, weak hierarchy, undefined behavior), record it
as `Design defect discovered during implementation` and route it, visual redesign to
`ui-visual-design`, behavior to `interaction-design`.

## 2. Step 1, fix the baseline and the build under review

Before comparing anything, write down both sides:

- **Baseline:** which approved artifact and version (file/section/version, spec or ticket
  version, the acceptance criteria set), and whether the design changed after handoff. A design
  tool's change flag or version history can help you spot edits; the change log is the record.
  If the artifact moved after handoff and the change was not logged, say so, QA against a
  moving target produces false defects in both directions.
- **Build:** environment (local, PR preview, staging), commit or build id, browser/OS/device,
  viewport(s), theme(s), locale, role used, feature flags, and data set.

If the person asking cannot supply these, QA is still possible on what they did supply, but the
report must state the limits.

## 3. Step 2, evidence rules

Report findings only on what you actually inspected: a screenshot shows appearance in one state;
a recording shows one path; code shows intent but not rendered behavior; a Storybook story shows
one state in isolation; a live build lets you test behavior, keyboard, and assistive technology.
For every dimension, the report says one of **verified**, **issue found**, **not inspected**
(and why: no build access, no screen reader available, no second viewport supplied). "Not
inspected" is a legitimate and necessary answer; "no issues" without inspection is not.

## 4. QA dimensions and how to check each

Check only dimensions the feature has. Each row: what to compare, how, and the typical defect.

| Dimension | Compare against | How | Typical defect |
|---|---|---|---|
| Behavior | Approved flow + AC | Walk every AC on the build; try cancel/back/retry/double-submit | Save fires twice; cancel loses input; success not shown |
| State transitions | State inventory | Force each state (slow network, empty data, denied role, server error) | Loading never resolves; empty state is a blank area; error replaces the form |
| Semantics | Accessibility contract | Inspect DOM/accessibility tree; check roles and names; heading structure | Clickable div instead of button; icon button with no name; two h1s |
| Components | Component map / Code Connect | Verify the system component (not a lookalike) is used with the mapped variant | Custom dropdown duplicating Select; wrong variant; detached instance equivalent in code |
| Tokens | Token map | Inspect computed styles vs semantic tokens; check theme switch | Raw `#1F6FEB` instead of `surface.action.primary`; hard-coded 12px gap |
| Typography / layout / spacing | Approved artifact at the same breakpoint | Inspect measured values against tokens, not against eyeballing | Wrong type role; spacing scale violated; alignment drifts |
| Responsive | Responsive rules | Test each supported breakpoint and 200% zoom / reflow | Horizontal scroll at compact; primary action pushed off-screen; truncation hides meaning |
| Content | Content classification | Compare strings; test longest realistic content; check provisional items | Lorem ipsum shipped; truncation without full-text access; wrong error wording |
| Empty / loading / error | State inventory | Force each | Spinner with no text; error with no recovery action |
| Permissions | Permission spec | Test each role; attempt denied actions directly if possible | Hidden in UI but reachable by URL; disabled without explanation |
| Keyboard | Accessibility contract | Tab/Shift+Tab/Enter/Space/Escape/arrows through the whole feature | Unreachable control; trap; wrong activation key |
| Focus | Accessibility contract | Open/close/delete flows; check placement, order, restoration, visibility, not obscured by sticky UI | Focus lost to body on close; focus hidden under sticky footer; no visible indicator |
| Screen-reader semantics | Accessibility contract | VoiceOver/NVDA/TalkBack pass if available; otherwise accessibility tree + "not inspected" | Group without label; state (expanded/selected) not conveyed |
| Announcements | Accessibility contract | Trigger success/error; verify live-region output | Toast visible but silent; error announced twice |
| Contrast | Tokens + target | Measure text and non-text (icons, borders, focus ring) in each theme | Placeholder text below target; focus ring fails non-text contrast in dark theme |
| Target size | Target rule | Measure interactive targets at the smallest viewport | Icon buttons below minimum; dense table actions overlapping |
| Motion / reduced motion | Motion spec | Toggle OS reduced-motion | Animation ignores preference; parallax remains |
| RTL / localisation | Locale rules | Switch locale/direction if supported | Mirrored icons wrong; text expansion breaks layout |
| Theme modes | Token set | Switch light/dark/brand/density | Hard-coded colours survive theme switch |
| Analytics (when defined) | Tracking plan + AC | Observe network/console events on trigger | Fires on click not on success; missing property; PII in payload |

Analytics QA verifies the approved measurement contract and nothing more: the event fires at the
approved trigger (for example only after the server confirms, not on click, not on failure, not
twice on retry), carries the required properties, sends nothing the contract excludes, and has
not had its semantics changed silently. "Engineering says it's done" is not evidence; observe it.
A mismatch is an implementation defect, or `Product/design decision required` if engineering
proposes different semantics. Defining or changing the metric, event, or properties belongs to
`prototype-testing-analytics`.

## 5. Component parity, custom vs system

When the build uses a custom component where the component map specified a system component,
do not reject it automatically and do not accept it because it was easier. Assess:

1. Does the approved system component already support the need (variants, props, composition)?
2. Is the custom component semantically different (different role, different interaction model)?
3. What required behavior, if any, is missing from the system component?
4. Does the custom implementation duplicate functionality the system already provides?
5. Does it preserve the accessibility behavior the system component carries (names, keyboard
   model, focus management, announcements)?
6. Does it increase maintenance cost (two implementations to update, theme/token drift)?
7. Does it create visual or behavioral inconsistency with the rest of the product?
8. Should the system be extended instead (route to the design-system owner / `design-systems-consistency`)?
9. Is the deviation temporary, and is there a migration plan with an owner?

Outcome is one of: reuse the system component; extend the system component (request logged);
compose from system parts; custom is justified (record as an approved deviation with reason,
owner, and sunset condition). Record the decision, whichever it is.

This skill makes the delivery decision: is the deviation justified for this feature, does the
existing component meet the requirement, what are the UX, accessibility, maintenance, and cost
impacts, should an exception be approved. If the outcome is "extend the system component", how to
extend it, props, variants, states, API, is designed in `design-systems-consistency`, not here.

## 6. Token parity

Check that the approved semantic tokens survived in three places: the design file uses the
semantic token (not a primitive or detached value); the code uses the corresponding
implementation token; no raw value replaced either silently; the theme/mode behavior still
holds. A raw value is a finding even when it currently equals the token's value, it will not
follow the next token change. If a needed token does not exist, the finding is "token missing",
routed to the system owner (`design-systems-consistency`); do not invent a token name or redesign
the scale. Whether the token definitions themselves match between design and code (values,
aliases, naming) is system parity, not feature QA.

## 7. Storybook comparison, when the team uses it

Use stories as the implemented **state inventory**: compare the set of stories for the component
against the approved state inventory and name states with no story. Use interaction tests
(`play` functions) as evidence of behavior for the paths they cover, and only those. Treat the
accessibility addon (axe-core) as a first filter: its own documentation says it catches "up to
57% of WCAG issues", and its **Incomplete** results explicitly need manual confirmation; a green
run says nothing about accessible-name quality, focus management across views, or announcement
timing; by default it runs WCAG 2.0/2.1 A/AA rules plus best practices, so WCAG 2.2 criteria are
checked only if the team opted in. Visual tests catch rendering regressions, not intent. Stories
show components in isolation: they do not prove feature usability, full product accessibility, or
production feature parity. None of this replaces checking the assembled feature in the product
with keyboard and assistive technology.

## 8. Figma / code comparison, when the team uses Figma

Use the Inspect panel and Variables view to read the **approved** values (component, variant,
applied variables) rather than eyeballing the canvas. If the design was edited after handoff (an
unlogged change, a newer version, or a change flag in the tool), resolve what changed before
filing parity defects. Use *Compare changes* when the developer built from an earlier version. If
Code Connect mappings exist, they tell you which code component should have been used; they do
not prove the behavior or states match. Generated code in Dev Mode is not the reference, the
team's components are.

## 9. The issue record

Every issue, in this shape. Vague comments ("spacing feels off") are not findings.

```
ID: QA-07
Expected: card list uses the system's space-400 vertical gap (token map, SavedSearchCard)
Actual: implementation uses 12px raw spacing (computed style, staging build 4f2c1e, 1280px)
Impact: diverges from approved token mapping; will not follow future spacing changes; visibly tighter than the rest of the list views
Evidence: screenshot qa-07.png; DevTools computed style; Figma Inspect shows space-400
Category: Implementation defect
Severity: MINOR
Next action: replace raw value with the spacing token; owner: FE; no design change needed
```

Keep Expected and Actual symmetrical and specific. Impact is user/product impact, not "it
bothers me". Evidence names the artifact so someone else can re-check.

## 10. Categories for implementation differences

Classify each difference as exactly one of:

| Category | Meaning | Usual next action |
|---|---|---|
| Approved implementation detail | Engineering chose a method the design left open | None; note it |
| Equivalent implementation | Different method, same user-observable outcome | None; confirm with a quick check |
| Design-system compliant adaptation | The system's own rule produced a different but compliant result | Update the design file to match the system |
| Necessary technical deviation | A real constraint forced a change | Record as approved deviation if accepted; else escalate |
| Product/design decision required | The difference exposes an unmade decision | Route to PM/design; do not decide in QA |
| Design defect discovered during implementation | The approved design was wrong or incomplete | Route to the owning design stage (`interaction-design`, `ui-visual-design`, …); log the change |
| Implementation defect | Build does not match the approved, feasible design | Fix in code |
| Accessibility defect | Approved accessibility behavior lost or never built | Fix; severity by barrier |
| Content mismatch | Strings differ from approved/final content | Fix or confirm with content owner |
| Unknown | Cannot classify without more information | Name the missing information |

Not every pixel difference is a bug; not every engineering deviation is acceptable. The category
decides who acts, the severity decides how urgently.

## 11. Severity

Severity reflects **user and product impact**, never designer preference.

- **BLOCKER**, cannot reasonably ship: a critical task cannot be completed; a serious
  accessibility barrier (keyboard trap, unreachable primary action, unnamed critical control);
  destructive behavior is unsafe (no confirmation on irreversible delete, wrong item deleted);
  severe permissions/security-facing UX mismatch (denied action reachable); a critical required
  state is missing; the implementation fundamentally contradicts approved product behavior.
- **MAJOR**, a meaningful usability, behavior, accessibility, responsive, or system-consistency
  failure: input lost on error; focus not restored after a modal; horizontal scroll at a
  supported breakpoint; a system component replaced by a custom one without justification;
  analytics firing on the wrong trigger; a required non-critical state missing.
- **MINOR**, noticeable, limited impact: raw value where a token exists (same visual today);
  wrong variant of the right component; truncation without tooltip on rare long content;
  secondary icon mismatch.
- **POLISH**, small visual refinement with no behavioral impact: 1–2px optical alignment;
  hover-state easing; an icon weight variant.

Calibration rules: weigh user impact, task impact, accessibility barrier, product and safety
risk, and reach (how many users, roles, or flows it touches), never designer preference or the
number of pixel differences. An accessibility issue that blocks a task is BLOCKER regardless of
how small it looks, but accessibility issues are graded by the barrier they create, not
automatically BLOCKER (a weak focus indicator on one secondary control is not a keyboard trap). A
visual issue that affects no task is POLISH regardless of how annoying it looks. Never downgrade a
serious functional or accessibility defect because the screen looks close to the design. When
unsure between two levels, choose by asking "what happens to a real user who hits this in the
first week?".

## 12. Regression risk

For each MAJOR or BLOCKER fix, note what else the fix could break (shared component, shared token,
other breakpoints, other themes, other roles) so the retest scope is explicit. For shared
components, a fix in one place is a change everywhere, flag it to the system owner.

## 13. Design QA verdict (not the release decision)

The verdict is a recommendation from the design-delivery perspective. Who decides whether the
release ships depends on the team's process; when that authority was not supplied, present the
verdict as the design/accessibility input to that decision, not as the decision.

- **Approve** (from a design-QA perspective), no BLOCKER or MAJOR; MINOR/POLISH items logged with
  owners; every relevant dimension is either verified or explicitly "not inspected" with an agreed
  follow-up.
- **Approve with follow-ups**, no BLOCKER; MAJOR items have owners and a committed fix before
  release or an explicitly accepted exception recorded by PM/design.
- **Do not approve**, a release blocker from the design/accessibility perspective: any BLOCKER,
  or a MAJOR accessibility defect without an accepted exception, or critical dimensions could not
  be inspected and the team has not agreed to ship without them.

Never approve because the default state "looks close". Never claim a dimension was verified when
it was not. Team sign-off is collaborative, but one accountable person (usually PM or the
technical product owner) makes the final call, say who, or that the team's process must name
them.

## 14. Report shapes

**Quick**, Design QA verdict (Approve / Approve with follow-ups / Do not approve) · BLOCKER and
MAJOR issues in the issue-record shape · what was not inspected · next action.

**Standard**, add: baseline and build identification; the dimension table with
verified / issue / not inspected per row; MINOR and POLISH list; regression notes; owners.

**Deep**, add: full issue log; component and token parity tables; per-breakpoint and per-theme
results; accessibility pass details (tool, AT, OS); analytics event log; change-log entries for
any design updates agreed during QA.

## 15. Things that are not defects

Equivalent implementations with the same observable outcome; sub-pixel rendering differences
between Figma and browsers; font rasterisation differences; a system-compliant adaptation where
the design file was the one out of date (fix the file, not the code); platform-native behaviors
the design mocked approximately (native select on mobile, scrollbars); content differences where
the build has the final copy and the design has the draft. File these as notes, not issues, so the
real defects stay visible.
