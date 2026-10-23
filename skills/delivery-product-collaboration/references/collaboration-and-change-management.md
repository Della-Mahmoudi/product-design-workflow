# Collaboration and change management

Read this for: engineering feasibility discussions, proposed deviations from the approved design,
PM/design/engineering decisions during development, scope changes, implementation discoveries
that affect the design, decision and change logging, and keeping design artifacts and
acceptance criteria in parity. Focus on decision ownership and impact. Do not redesign the
feature here.

## Contents

1. The collaboration stance
2. Who decides what
3. Feasibility discussions
4. Evaluating a proposed deviation
5. Approved exceptions
6. Implementation discoveries and routing back
7. Scope changes during development
8. Change log
9. Keeping artifacts and acceptance criteria in parity
10. Open questions and decision log
11. Escalation
12. Practices worth keeping (distilled)
13. Anti-patterns

---

## 1. The collaboration stance

Delivery is not a designer-to-developer transfer; it is a shared commitment to ship the approved
experience in a way the codebase can sustain. Engineering constraints can legitimately change a
design. "Harder to build" is not by itself a reason to change an approved experience, and "it's
in Figma" is not by itself a reason to keep one. Frame every discussion around the user outcome,
the real constraint, and the cost of each option — never around which side wins. Involve only the
roles the decision needs; do not build meeting processes.

Roles that may be needed (use the team's actual titles): designer, engineer(s), PM/product owner,
design-system owner, accessibility specialist, content/design writing, data/analytics, QA. Where a
role does not exist, name who is covering it rather than leaving the responsibility unassigned.

## 2. Who decides what

| Decision | Owner | This skill's part |
|---|---|---|
| What the product does (behavior, rules, scope) | PM / product owner, with design | Make the decision visible, state impact, record the outcome |
| How the experience behaves and looks | Design — `interaction-design` for behavior, `ui-visual-design` for visuals | Evaluate deviations; route redesign back |
| How it is built (architecture, method) | Engineering | Ask only for what affects the user-observable outcome |
| Whether the design system changes | Design-system owner (`design-systems-consistency`, Skill 05) | Raise the request with evidence; do not design the extension |
| Whether an accessibility exception is acceptable | Accessibility owner + PM | Classify the barrier; never approve exceptions alone |
| Content wording | Content owner (or design if none) | Flag mismatches and provisional strings |
| Analytics definitions | Data/analytics (`prototype-testing-analytics`, Skill 06) | Verify the approved contract is in the handoff and that the build implements it; never redefine it |
| Ship / no-ship | The release owner the team's process names (often PM or technical product owner) | Supply the design QA verdict and open risks; never present the verdict as the release decision |

When this skill is asked to "just decide", decide only what is in its column; for the rest,
produce the decision packet (options, impacts, recommendation) and name the owner.

## 3. Feasibility discussions

When engineering says an approved behavior is hard, infeasible, or expensive, run the assessment
before anyone proposes a replacement:

| Dimension | Question |
|---|---|
| Original requirement | What user/product outcome was the behavior serving? (Check the AC and, if needed, the approved rationale — Tier 3, only when it matters.) |
| Existing capability | Does an existing component, pattern, or API already achieve the outcome a different way? |
| Technical constraint | What exactly is the constraint — platform, API, performance, time, skills? Is it Confirmed or Assumed? |
| Implementation cost | Rough cost of the approved behavior vs each alternative, with engineering's own confidence in the estimate (high / medium / low) |
| Accessibility impact | Does any alternative lose approved accessibility behavior? |
| UX impact | What does the user lose or gain under each alternative? |
| Design-system impact | Does an alternative introduce a one-off or bypass system components/tokens? |
| Maintenance cost | Who maintains the alternative, and for how long? |
| Cross-platform impact | Does the alternative diverge across platforms? |
| Simpler compliant alternative | Is there an option that meets the outcome with less cost and no accessibility or system loss? |
| Decision needed | Can engineering choose freely (implementation detail), or does PM/design need to approve? |

Distinguish three situations: **infeasible** (cannot be built as approved — decision required),
**costly** (can be built; cost vs value is a product trade-off — PM decides with design input),
**unfamiliar** (can be built; the team has not done it before — often solvable with a spike or a
system component). Do not let the third masquerade as the first.

## 4. Evaluating a proposed deviation

1. State the approved behavior and the proposed change side by side.
2. Classify (one of): Approved implementation detail · Equivalent implementation · Design-system
   compliant adaptation · Necessary technical deviation · Product/design decision required ·
   Design defect discovered during implementation · Implementation defect · Accessibility defect
   · Content mismatch · Unknown.
3. Assess impact using the §3 dimensions, in proportion to the change.
4. Recommend one of: keep approved behavior; accept as equivalent; accept as approved deviation
   (record it); extend the system (request logged); escalate the decision to the owner.
5. If accepted, update the artifacts and acceptance criteria (§9) and log the change (§8).

The "custom component instead of the system one" case follows the parity questions in the QA
reference (does the system component already cover it, semantic difference, missing behavior,
duplication, accessibility, maintenance, inconsistency, extend-instead, temporary-with-migration).
Prefer existing system capability when it is sufficient; accept custom work when a real gap
exists and the exception is recorded with an owner and a sunset condition. This skill decides
whether the deviation is acceptable for this delivery; if the answer is to extend the reusable
component, its props, variants, states, and API are designed in `design-systems-consistency`.

## 5. Approved exceptions

Record every accepted deviation so it does not quietly become the new standard.

```
Exception: EX-12
Feature: saved-search / delete flow
Approved behavior: undo toast (10 s) after delete
Deviation: confirmation dialog instead of undo
Reason: deletion is hard (not soft) in search-service v2 — Confirmed by backend lead on 2026-10-14
Impact: user: one extra step, no accidental-loss risk; a11y: dialog follows system Modal contract; system: none; analytics: `saved_search_deleted` trigger unchanged
Approved by: PM (name) with design (name)
Scope: this feature only — not a precedent for other delete flows
Sunset / revisit: when soft delete ships (ticket PX-480)
Artifacts updated: Figma section v1.5, AC-7 replaced, ticket PX-401 description
```

## 6. Implementation discoveries and routing back

Implementation regularly reveals things design could not know: an API that cannot page, a
permission that is only checked server-side, an interaction that cannot be made accessible with
the chosen component. When that happens:

- Record the constraint (and its classification), the affected behavior, the decision required,
  and the options engineering supplied.
- Do **not** invent a replacement interaction here. Route the decision to the owning stage — the
  same step-back logic as unclear requirements: look at the acceptance criterion, then the
  approved artifact, then the originating requirement or decision; whoever owns the layer that
  needs to change makes the change (interaction behavior → `interaction-design`; product rules
  and trade-offs → PM, with `product-discovery-framing` if the problem itself is in question).
  Engineering-supplied alternatives can be summarized as options; they are not decisions until
  the owner picks one.
- Once the owning stage decides, update the artifact, the acceptance criteria, and the change log,
  and tell QA what the new baseline is.

## 7. Scope changes during development

Scope can shrink (a work package split across iterations) or grow (a "small" addition). The
practice that holds up: a delivered slice should solve its problem completely — shipping 80% of a
flow with a missing main capability is not a partial success, it is a broken feature. When scope
is cut, cut whole capabilities with their states, not the error paths of a capability that stays.
When scope grows, treat the addition as a new handoff item with its own readiness check rather
than letting it ride on the existing one.

## 8. Change log

The rule, independent of any tool: after handoff, any material design change is explicitly
surfaced, recorded, and synchronized with implementation. A design tool's change detection (Figma,
for example, can flag edits to a design marked Ready for dev) may help you notice an edit; it is
neither the record nor a requirement.

Log every change to an approved design during development, however small it looks.

```
Change: CH-31
Date: 2026-10-16
What changed: duplicate-name handling moved from inline error to pre-validated disabled Save
Why: API returns duplicate conflict only after submit (Confirmed); inline check would require a new endpoint
Triggered by: engineering discovery during PX-401
User impact: user learns about the duplicate on submit rather than while typing; message wording unchanged
Technical impact: no new endpoint; one extra round trip on conflict
Design-system impact: none (system inline error pattern)
Accessibility impact: error announced via live region on submit (unchanged contract)
Analytics impact: none
Design artifacts updated: yes — section v1.5, status note added
Acceptance criteria updated: yes — AC-6 rewritten
Decision owner: PM (name) with design (name)
```

Logging prevents the two failure modes that cost the most later: the design file says one thing
and the product does another, and nobody remembers why.

## 9. Keeping artifacts and acceptance criteria in parity

Every accepted deviation or change has three places to update: the design artifact (and its
readiness status or version note, if the team uses one), the acceptance criteria, and the
ticket/spec. A change that touches one without the others creates a false defect for the next
reviewer. Make "artifacts updated: yes/no" a field in every change record so the gap is visible
rather than assumed.

## 10. Open questions and decision log

Keep both lightweight and in one place the team already uses (ticket, doc, status note).

```
Q-5 | Should saved-search limits be shown before the user hits them? | owner: PM | blocking: no | needed by: before limits UI ticket
D-9 | Duplicates rejected on submit, not inline (see CH-31) | decided by: PM + design | date | supersedes: AC-6 v1
```

Questions get owners and needed-by dates; decisions get a decider, a date, and what they
supersede. Both stay short.

## 11. Escalation

Escalate when a decision is outside this skill's ownership and the owner has not decided, when a
deviation would remove approved accessibility behavior, when a BLOCKER cannot be fixed before
release, or when engineering and design disagree on facts (then the resolution is to establish
the fact — a spike, a test, a look at the API — not to argue preferences). Escalate with a
decision packet: the question, the options, impact per option, your recommendation, and the
deadline. Keep it to the people who own the decision.

## 12. Practices worth keeping (distilled from technical product management practice)

- Communicate deviations early and plainly. The costly thing is not the change; it is the
  surprise. A delay or a cut capability surfaced early is a team decision; surfaced late it is a
  failure.
- Attach confidence to estimates and technical claims (high / medium / low; Confirmed / Assumed).
  Low-confidence claims that shape the UX are the first things to verify.
- Shared status in a short, regular review: plan vs actual, whether the product still meets the
  requirements, which scenarios QA has covered, what has changed. Everyone hears the same
  information.
- Approval is collective, accountability is singular: the whole team signs off for their area;
  one accountable person makes the final call and documents the final status.
- Let engineering choose how to build; ask only for what the user must experience.
- Avoid over-documentation; the specification is as detailed as the team's shared understanding
  requires and no more.
- Close with a short retrospective on the collaboration itself: what went well, what blocked,
  what to change next time.

## 13. Anti-patterns

- Framing the conversation as design vs engineering, or asking "who wins".
- Letting "harder" stand in for "infeasible", or "in Figma" stand in for "required".
- Silently accepting a deviation in a PR comment with no record and no artifact update.
- Inventing a replacement interaction in the moment instead of routing the decision.
- Approving an accessibility exception without the accessibility owner and PM.
- Treating a technical assumption ("it's reversible") as a fact because it was said confidently.
- Escalating preferences; escalate decisions and facts.
- Creating a recurring meeting where a logged decision would do.
