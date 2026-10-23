# Acceptance criteria and implementation specs

Read this for: writing or reviewing acceptance criteria, Definition-of-Done items that concern
design, ticket-level implementation specs, and annotations that explain intent to engineering.
Do not generate a full Ready-for-Dev manifest from here unless the feature is complex enough to
need one (see the handoff reference).

## Contents

1. What a criterion is for
2. Anatomy of a testable criterion
3. Plain statements vs Given / When / Then
4. Criteria by dimension (behavior, state, error, permission, destructive, responsive, accessibility, content, analytics)
5. Technical assumptions inside criteria
6. Product behavior vs implementation detail, what not to specify
7. Anti-patterns and rewrites
8. Traceability
9. Ticket-level spec block
10. Review checklist

---

## 1. What a criterion is for

An acceptance criterion lets a developer know when they are done and lets a tester know what to
check, without either of them asking the designer. A criterion that cannot be observed cannot be
tested, and a criterion that cannot be tested will be interpreted, usually differently by each
reader. Criteria describe **outcomes the user or system can observe**, under **stated
conditions**, in **named states**, with **relevant constraints**, including **failure behavior**
where it exists. They do not describe how the code is organised.

Criteria translate **approved** product and design behavior into observable, testable statements.
They are not where undecided behavior gets decided. If nobody approved what happens, where focus
goes after Cancel, whether duplicates are allowed, what undo restores, the criterion cannot be
written yet: mark the gap `Missing design decision`, block or condition readiness, and route it to
its owner (the owner routing table in SKILL.md). A confident Given/When/Then for unapproved
behavior hides the gap instead of closing it.

## 2. Anatomy of a testable criterion

Each criterion should let you answer: *who/which role*, *under what condition or state*, *does
what*, *observes what*, *and what happens when it fails*. Not every criterion needs every part,
but a criterion missing both condition and observable outcome is not a criterion.

Weak → strong, same intent:

| Weak | Why it fails | Testable rewrite |
|---|---|---|
| The modal should work correctly. | No observable outcome | When the user confirms deletion, the modal closes, the item is removed from the list without a page reload, and focus returns to the list item that preceded the deleted one (or to the list heading if none). |
| Responsive design should work. | No breakpoint, no transformation | At the product's compact breakpoint, secondary metadata moves below the title while the primary action remains available without horizontal scrolling. |
| Errors are handled gracefully. | "Gracefully" is unobservable | When saving fails with a network error, the form keeps the user's input, shows the inline error "Couldn't save, check your connection and try again", and the Save action remains available. |
| Users without permission can't delete. | Unclear whether hidden, disabled, or rejected | When a user without delete permission opens workspace settings, the destructive delete action is not rendered; a direct request to the delete endpoint is rejected (server behavior, requires engineering confirmation). |
| The list loads fast. | Vague adjective (the book's "fast" problem) | The list renders a skeleton within the first paint and shows results or an empty state within the product's loading budget (confirm budget with engineering; design assumes ≤ 2 s before a "still loading" message). |

The rewrites assume the behavior they describe was approved; where it was not, the rewrite is not
yours to write, route the decision first.

Avoid the words the Technical Product Management practice flags as meaningless in requirements:
simple, user-friendly, fast, flexible, optimal, maximum/minimum without a number, "as soon as
possible", "scalable". Replace with numbers, named states, or comparisons to an existing product
behavior ("behaves like the existing Rename flow").

## 3. Plain statements vs Given / When / Then

Use plain criteria by default; they read faster and most teams test from them directly. Use
Given / When / Then when the criterion has a precondition that readers would otherwise miss, when
several conditions share one outcome, or when the team's tooling consumes Gherkin. Do not force
Gherkin onto every ticket, a one-line observable statement is often clearer than three lines of
scaffolding.

```
Given a user with the Editor role and at least one saved search
When they rename a saved search to a name that already exists in their workspace
Then the rename is rejected inline with "A saved search with this name already exists",
     the original name is preserved, and focus stays in the name field
```

Keep each scenario to one outcome. If you need "and also…", that is a second criterion.

## 4. Criteria by dimension

Write criteria only for the dimensions the feature actually has. Examples are patterns, not text
to paste.

**Behavior**, trigger, outcome, side effects visible to the user. "After a successful save, the
new saved search appears at the top of the list and the toast 'Search saved' is shown for 5 s or
until dismissed."

**State**, what each required state shows and what remains actionable. "While saving, the Save
button shows the loading indicator, is not re-triggerable, and the form fields remain visible but
non-editable; Cancel remains available and discards the pending save." (Whether cancel can
actually abort the request is technical, label it.)

**Error**, identification, wording ownership, recovery, preservation of input. "Validation
errors appear inline under the field on blur and on submit, are announced to assistive
technology, and submission is blocked until resolved."

**Permission**, per role: visible, disabled, hidden, denied message, and whether the server
enforces it. Never write "the server also checks" unless confirmed.

**Destructive**, confirmation, consequence statement, reversibility, dependants. "Deleting a
shared saved search shows a confirmation naming the number of other users who will lose access
(count supplied by API, requires engineering confirmation) and offers no undo; the design assumes
irreversibility until confirmed otherwise."

**Responsive**, per named breakpoint: what stacks, collapses, hides, and what must stay
reachable without horizontal scrolling. Include text-wrapping behavior for the longest realistic
content.

**Accessibility**, write as observable behavior, not as "is accessible": the control has the
accessible name "Save search"; all actions are reachable by keyboard in reading order; opening
the modal moves focus to its heading and Escape closes it, restoring focus to the triggering
control; success and error messages are announced via a live region; text and non-text contrast
meet the team's target; targets meet the team's minimum size; animation respects the
reduced-motion preference.

**Content**, which strings are final, which are provisional, dynamic ranges (min/max/empty), and
truncation rules. "Saved search names are limited to 60 characters; longer names are truncated
with an ellipsis in the list and shown in full in the tooltip/accessible name."

**Analytics (only when a tracking plan exists)**, event name, trigger moment (attempt vs
success), required properties, privacy constraints. "On successful save (not on click),
`saved_search_created` fires with `{filter_count, source: 'results_page'}`; no free-text search
terms are sent." Do not invent events, properties, or triggers; they come from the approved
tracking plan (`prototype-testing-analytics`).

## 5. Technical assumptions inside criteria

A criterion must not quietly assert technical behavior. When the outcome depends on something
engineering has not confirmed, keep the user-facing expectation and label the dependency:

```
AC-7  When the user undoes a deletion within 10 s, the item is restored to its previous position.
      [Assumed: deletion is soft and reversible for 10 s, requires engineering confirmation.
       If not reversible, AC-7 is replaced by a confirmation dialog, product decision, owner: PM]
```

Classification words to use consistently: Confirmed, Proposed, Assumed, Requires engineering
confirmation, Blocked. A criterion that is `Blocked` cannot be accepted into a sprint as written.

## 6. Product behavior vs implementation detail

Specify what the user experiences and what the system guarantees to the user; leave how to
engineering unless the "how" is itself an approved design decision (e.g. a specific system
component, a token) or an accessibility requirement (e.g. a native button element rather than a
clickable div).

| Specify (product behavior / approved design) | Do not specify (implementation) |
|---|---|
| Which system component and variant | Internal component architecture, state-management approach |
| Semantic token names used | Hex values already carried by the token |
| Focus placement and order | Which focus library implements it |
| "Input is preserved after a failed save" | Whether preservation uses local state or a draft API |
| "Results update without a full page reload" | Fetch strategy, caching |
| Announcement text and timing | ARIA implementation details beyond the required role/name |
| Error message wording and recovery options | HTTP status mapping (unless user-facing text depends on it, then ask) |

Over-specification creates false defects (engineering did it a different, equivalent way) and
hides real ones (nobody checked the outcome because they were checking the method).

## 7. Anti-patterns and rewrites

- **The happy-path-only ticket.** Criteria cover success only. Add the states a user will hit in
  week one: loading, empty, error, permission-denied.
- **The disguised decision.** "Dev to decide whether duplicates are allowed." That is a product
  decision; list it as an open question with a PM owner, not as a criterion.
- **The invented criterion.** A criterion that settles behavior nobody approved, written so the
  ticket looks complete. Mark it `Missing design decision` and route it; the criterion follows the
  decision.
- **The borrowed guarantee.** "Deleted items can be restored for 30 days." Unless confirmed by
  engineering, label it Assumed and name the fallback.
- **The adjective criterion.** "Fast", "intuitive", "clean". Replace with observable behavior.
- **The pixel criterion.** "Gap is 12px." If the system token decides it, reference the token;
  if the token is wrong, that is a `design-systems-consistency` question.
- **The Gherkin wall.** Ten Given/When/Then blocks for a toggle. Collapse to the two that carry
  decisions.
- **The silent analytics drop.** The tracking plan defines an event; the ticket does not mention
  it. Add the trigger criterion.

## 8. Traceability

Each criterion should point back to the approved artifact (frame/section/version or status note)
and, where it exists, to the requirement or decision it comes from. When implementation later
disputes a criterion, that chain is how the dispute is resolved without re-litigating the design:
look at the criterion, then the approved artifact, then the requirement or decision record, the
same step-back logic the product-management practice recommends for unclear stories.

## 9. Ticket-level spec block

A compact shape that fits most tickets; drop sections that do not apply.

```
Feature / ticket: <id>, <name>
Approved artifact: <file / section / version or status>
Scope: in: … / out: …
Components: <system component → variant/props>, custom: <none | name + reason>
Tokens: <notable semantic tokens; raw values: none>
States covered: <list>; not applicable: <list>
Responsive: <breakpoint → transformation>, or "system grid rules apply"
Accessibility contract: <semantics / names / keyboard / focus / announcements / contrast / targets / motion>
Content: <final | provisional items | dynamic ranges>
Permissions: <role → visible/actionable/denied>
Destructive: <confirmation / reversibility (classification) / dependants>
Analytics: <linked events + trigger moment> | none supplied
Technical statements: <each with Confirmed / Proposed / Assumed / Requires confirmation / Blocked>
Acceptance criteria: AC-1 … AC-n
Open questions: Q-1 … (owner, blocking?)
```

## 10. Review checklist

Before calling a set of criteria done, confirm each applicable item:

- Every criterion has an observable outcome a tester could verify without asking the designer.
- Conditions, roles, and states are named where they change the outcome.
- Failure behavior is covered for every action that can fail.
- No criterion asserts a technical guarantee that is not Confirmed.
- No product decision is hidden as an implementation choice.
- Every criterion traces to approved behavior; none was written to fill a design gap.
- Accessibility criteria describe behavior (names, keyboard, focus, announcements), not "is accessible".
- Responsive criteria name the product's breakpoints and the transformation.
- Content status is explicit; no placeholder is behavior-relevant.
- Already-defined analytics triggers are present; none were invented.
- Criteria reference the approved artifact and, where relevant, the originating requirement.
- The set is as short as it can be while still preventing a developer from having to guess.
