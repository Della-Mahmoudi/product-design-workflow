# Evaluation cases, delivery-product-collaboration

Cases A–C test real delivery failures: approving on visual completeness, QA reduced to
screenshot matching, and deviation decisions made by preference instead of evidence. Cases D–L
test the boundaries: tool status vs real readiness, system parity vs feature parity, and
decisions that belong to Skills 03, 04, and 06. Each case is run with the prompt exactly as
written and with no further context, because the skill's value shows in how it handles missing
information: it must not invent it.

Grading convention: a case **passes** only if every pass criterion holds and no failure criterion
occurs. The unnecessary-work checks are graded separately; they catch the skill doing too much.
For cases marked *Should this skill trigger? NO*, a trigger test passes when the skill does not
load; if the skill is invoked manually anyway, the case passes only when it routes to the primary
owner without doing that owner's work. `evals/evals.json` carries the same twelve cases in the
skill-creator eval format (ids 1–12 = A–L).

| Case | Prompt (short) | Should trigger | Primary owner |
|---|---|---|---|
| A | Mark it Ready; only the default desktop screen exists | YES | `delivery-product-collaboration` |
| B | Build looks almost identical to Figma; can we approve? | YES | `delivery-product-collaboration` |
| C | Developer wants a custom dropdown instead of Select | YES | `delivery-product-collaboration` |
| D | Figma section already marked Ready for Dev | YES | `delivery-product-collaboration` |
| E | Button properties differ between Figma and code | NO | `design-systems-consistency` |
| F | New checkout on staging vs the approved design | YES | `delivery-product-collaboration` |
| G | Nobody decided focus after Cancel; fill it in | YES (readiness) | `delivery-product-collaboration`; behavior → `interaction-design` |
| H | Define the Saved Search event, properties, metric | NO | `prototype-testing-analytics` |
| I | Verify `saved_search_created` fires after server confirmation | YES | `delivery-product-collaboration` |
| J | Is this label final or placeholder copy? | YES | `delivery-product-collaboration` |
| K | API cannot support the approved undo | YES | `delivery-product-collaboration`; redesign → `interaction-design` |
| L | Redesign spacing, typography, hierarchy of a dense page | NO | `ui-visual-design` |

---

## Evaluation A, Not actually Ready for Dev

### User prompt

> Mark this feature Ready for Dev. We only have the default desktop screen right now; developers can figure out the rest.

### Expected behavior

- Refuses to mark the feature Ready for Dev and says why in terms of implementation clarity,
  not visual polish.
- Identifies which missing information is implementation-critical, proportionately: required
  states (loading, empty, error, success at minimum; permission and destructive where the
  feature has them), alternate flows, responsive behavior beyond desktop, component mapping to the
  team's system, token usage, the accessibility contract (semantics, names, keyboard, focus,
  announcements), content status, and technical unknowns.
- Asks for or checks the inputs it would need (approved flows, system components, breakpoints,
  accessibility requirements, tickets/AC) rather than assuming them.
- Separates hard blockers from non-blocking documentation gaps.
- Returns the minimum list needed to unblock engineering, with owners where they can be named,
  and offers a conditional path (e.g. "Ready with conditions" once X, Y, Z are supplied).
- States its verdict as `Not Ready` (or at most `Ready with conditions` only if it explains that
  conditions must be met before the affected parts are built, given the prompt, `Not Ready` is
  the expected verdict).

### Pass criteria

- Does not approve purely because the default screen looks complete.
- Does not create the missing behavior itself (no invented states, flows, error copy, breakpoints,
  or keyboard models presented as the design).
- Separates blocker from nice-to-have documentation explicitly.
- Gives a concise unblock plan (what, who, before which step).
- Labels any technical statements it makes as Confirmed / Assumed / Requires engineering
  confirmation rather than asserting them.

### Failure criteria

- Marks the feature Ready (or effectively ready, "go ahead, fill in later").
- Assumes developers can invent states, responsive behavior, or accessibility behavior.
- Generates arbitrary interaction behavior and presents it as the feature's design.
- Produces unnecessary full project documentation (a complete manifest, state inventory, and
  acceptance-criteria set for a feature whose scope it does not know).
- Lectures about readiness in general without naming the specific gaps.

### Unnecessary-work checks

- Did not load or reproduce the implementation-QA guidance (no built product exists).
- Did not browse Figma, Storybook, WCAG, or DTCG documentation.
- Did not write a manifest or Gherkin set before scope and states are known.
- Response length proportional to a quick-mode verdict with an unblock list.

---

## Evaluation B, Implementation looks close

### User prompt

> The developer implementation looks almost identical to Figma. QA it and tell me if we can approve it.

### Expected behavior

- Does not limit QA to screenshot similarity; explains that "looks almost identical" covers one
  state, one viewport, one theme.
- Establishes the baseline (which approved artifact/version, whether the design changed since
  Ready for Dev) and the build under review (environment, viewport, theme, role), or states that
  these were not supplied.
- Compares, or sets out to compare, the relevant dimensions: behavior against acceptance
  criteria, state transitions, semantics, components (system vs lookalike), tokens (raw values vs
  semantic tokens, theme behavior), responsive behavior, content, accessibility (keyboard, focus,
  names, announcements, contrast, target size, reduced motion), and analytics if a tracking plan
  exists.
- Uses the Expected / Actual / Impact / Evidence / Category / Severity / Next action issue shape
  for any issue it can actually support.
- Classifies severity with BLOCKER / MAJOR / MINOR / POLISH and distinguishes visual polish from
  meaningful defects.
- Clearly marks every dimension it could not inspect as "not inspected" and does not claim a
  verdict it cannot support; the honest answer with no build access is "cannot approve yet -
  here is what I need to inspect and how".

### Pass criteria

- Behavioral and accessibility parity are explicitly considered, not just visual parity.
- Any issue stated has evidence and impact; dimensions without evidence are marked not inspected.
- Severity is proportional to user impact.
- The approval decision follows the rules (no approval with BLOCKER/MAJOR or with critical
  dimensions uninspected) and names who makes the final call.

### Failure criteria

- Says "looks close, approve" (or approves on visual similarity alone).
- Only compares pixels, spacing, and colours.
- Invents implementation behavior it has not inspected (e.g. "focus restoration works", "tokens
  are used") and reports it as verified.
- Reports a long list of fabricated defects to look thorough.

### Unnecessary-work checks

- Did not load the handoff/readiness guidance (the feature is already built).
- Did not fetch Storybook or Figma documentation unless the user indicated those tools are in use
  and a tool detail mattered.
- Did not produce a deep-mode report when a quick/standard verdict with an inspection plan was the
  proportionate answer.

---

## Evaluation C, Custom dropdown divergence

### User prompt

> The developer says building a custom dropdown is easier than using our existing Select component. Should we let them?

### Expected behavior

- Does not answer yes or no on principle. Inspects (or asks for) the actual requirement the
  dropdown must meet and the existing Select component's actual capability (variants, props,
  composition, accessibility behavior).
- Identifies the gap, if any, between the requirement and Select, and says plainly when no gap
  has been demonstrated ("easier" is not a gap).
- Considers accessibility (the system Select's keyboard model, naming, focus management, and
  announcements that a custom build would have to re-implement), component/API parity,
  maintenance and design-system debt, implementation cost (including the hidden cost of the
  custom path), and consistency.
- Determines, or sets out the decision path for, which outcome applies: reuse Select; extend
  Select (request to the design-system owner); compose from system parts; custom is justified.
- If custom is accepted, records it as an approved deviation with reason, owner, scope, and a
  sunset/migration condition.
- Names who decides (design-system owner with design and engineering; PM if the behavior
  changes) rather than deciding unilaterally.

### Pass criteria

- Does not automatically side with design or with engineering.
- Evaluates product, technical, accessibility, and system impact.
- Prefers existing system capability when it is sufficient, and states the conditions under
  which a custom component would be justified.
- Treats "easier" as a claim to examine (easier to start vs cheaper over the component's life).

### Failure criteria

- Accepts the custom implementation only because it is easier.
- Rejects it only because Figma used Select.
- Ignores accessibility or long-term system cost.
- Invents the Select component's capabilities or the requirement instead of asking.

### Unnecessary-work checks

- Did not redesign the dropdown or produce a new component spec (that belongs to `design-systems-consistency`).
- Did not fetch Carbon/Material/Fluent select documentation as if it were the team's standard.
- Did not generate a Ready-for-Dev manifest or a QA report for a question that is a
  collaboration/deviation decision.
- Kept the answer to a decision packet: requirement, capability, gap, impacts, recommendation,
  decision owner, exception record if applicable.

---

## Evaluation D, Figma status is not readiness

### User prompt

> The Figma section is already marked Ready for Dev. Can we send it to engineering?

### Should this skill trigger?

YES.

### Primary owner

`delivery-product-collaboration`.

### Expected behavior

- Treats the Figma *Ready for dev* status as workflow metadata, a record that someone intended
  handoff, not as evidence that the design is complete.
- Performs, or requests the inputs for, the minimum readiness checks rather than a full audit:
  required states (loading, empty, error, success), alternate and error-recovery flows,
  destructive and permission behavior where the feature has them, responsive behavior for
  supported viewports, component and token mapping, accessibility behavior for any custom
  interaction, content status, technical unknowns, and open product decisions.
- Separates hard blockers from non-blocking gaps, proportionately; a missing annotation is not a
  blocker unless it hides one of those decisions.
- Returns `Ready`, `Not Ready`, or `Ready with conditions`. With no artifact supplied it does not
  return `Ready`: it says what must be checked (or checks what was supplied) and what would make
  the verdict `Ready` or `Ready with conditions`.

### Pass criteria

- States explicitly that the status does not prove readiness, and why.
- Bases the verdict on the skill's readiness gates, not on the status.
- Checks implementation-critical unknowns proportionately and names concrete gaps or checks.
- Does not make Figma or the status a precondition for handoff.

### Failure criteria

- Approves (or effectively approves) because Figma says Ready for dev.
- Treats the status as Tier 0 evidence or lets it override missing states or behavior.
- Requires the team to use Figma statuses, or blocks a non-Figma handoff for lacking the status.
- Runs a deep-mode audit, or invents states and behavior to fill gaps.

### Unnecessary-work checks

- Did not browse Figma documentation (no tool-specific detail matters to the answer).
- Did not load the implementation-QA reference (nothing is built yet).
- Did not produce a manifest or acceptance criteria.
- Response length proportional to a quick-mode verdict with a check list.

---

## Evaluation E, Design-system parity (should not trigger)

### User prompt

> Our Button component has different properties in Figma and code. Which one should be the source of truth and how should we reconcile them?

### Should this skill trigger?

NO. This is system object ↔ system object parity.

### Primary owner

`design-systems-consistency`.

### Expected behavior (if this skill is invoked manually)

- Recognises the question as reusable design-system parity, the Figma Button component vs the
  code Button API, not feature implementation parity.
- Routes it to `design-systems-consistency`, optionally noting the evidence that skill will want
  (the Figma component properties and variants, the code props, real usage, any Code Connect
  mapping).
- Notes, at most in one line, what stays with this skill: checking that a specific feature build
  used the approved Button once `design-systems-consistency` has settled the component.

### Pass criteria

- Routes to `design-systems-consistency` by name.
- Does not choose a source of truth or propose a reconciled property/API mapping.
- Keeps the response to a short routing note.

### Failure criteria

- Decides which side is the source of truth.
- Designs the reconciled Button props, variants, or states.
- Runs a feature QA pass or produces handoff artifacts for a question about a reusable component.

### Unnecessary-work checks

- Did not load any reference file.
- Did not fetch Code Connect or Storybook documentation.
- Did not produce a component spec, migration plan, or parity table.

---

## Evaluation F, Feature implementation parity

### User prompt

> The new checkout is on staging. Compare it with the approved design and tell me whether design QA passes.

### Should this skill trigger?

YES.

### Primary owner

`delivery-product-collaboration`.

### Expected behavior

- Establishes the baseline: which approved design and version, the acceptance criteria, and
  whether the design changed after handoff, or states that these were not supplied.
- Establishes the build: staging build or commit, viewports, browsers/devices, themes, locale,
  roles/accounts, test data (for example test cards and a declined payment), feature flags, or
  states what is missing.
- Selects the checkout-relevant QA dimensions instead of comparing pixels: behavior against the
  acceptance criteria (including validation and payment-failure paths), loading/error/empty
  states, form semantics, keyboard and focus, error announcements, components and tokens,
  responsive behavior, content (prices, totals, legal copy), and analytics only if a tracking
  plan is supplied.
- Reports only defects it can support, each with Expected / Actual / Impact / Evidence /
  Category / Severity / Next action; marks every uninspected dimension "not inspected" with the
  reason.
- Gives a design QA verdict (or says what must be inspected before one is possible) and does not
  present it as the organisation's release decision.

### Pass criteria

- Baseline and build are fixed, or their absence is stated.
- Behavioral and accessibility dimensions are considered, not only visual ones.
- No finding without evidence; uninspected dimensions are labelled as such.
- Severity follows user and product impact.

### Failure criteria

- Redesigns any part of checkout.
- Reports behavior it could not inspect as verified, or fabricates defects.
- Passes design QA on visual similarity alone.
- Claims accessibility conformance from design QA.

### Unnecessary-work checks

- Did not load the readiness/handoff reference (the feature is built).
- Did not fetch Figma, Storybook, or WCAG documentation.
- Did not produce a deep-mode report unless the supplied scope justified it.

---

## Evaluation G, Missing interaction decision

### User prompt

> We are handing off this delete dialog, but nobody decided what happens to focus after cancel. Can you fill that in so we can mark it Ready?

### Should this skill trigger?

YES, for the readiness evaluation.

### Primary owner

`delivery-product-collaboration` for the readiness verdict; the missing behavior is owned by
`interaction-design`.

### Expected behavior

- Identifies focus placement after Cancel as an implementation-critical interaction and
  accessibility decision for a destructive dialog, not a dev detail and not a cosmetic gap.
- Checks whether the team's approved system dialog/modal contract already defines focus
  restoration: if it does, cites it as resolving the gap instead of inventing anything; if it
  does not (or none is supplied), treats the gap as open.
- Classifies the open gap as `Missing design decision` (`Product/design decision required`) and
  routes the behavior definition to `interaction-design`, naming what the decision must cover
  without answering it.
- Blocks readiness (`Not Ready`) while the decision is open, or, if the team scopes the dialog
  out of the current build, conditions the rest of the handoff on it with an owner and a
  resolve-before point. It never marks the dialog Ready.

### Pass criteria

- Declines to fill in the focus behavior and says why.
- Routes the decision to `interaction-design` by name.
- The dialog is not marked `Ready` while the decision is open.

### Failure criteria

- Specifies where focus goes after Cancel (for example "return focus to the Delete button") as
  the design.
- Writes an acceptance criterion or Given/When/Then that decides the behavior.
- Marks the dialog Ready.
- Produces a full accessibility contract for the dialog.

### Unnecessary-work checks

- Did not browse WCAG or platform documentation.
- Did not produce a manifest or a full acceptance-criteria set.
- Quick-mode length: verdict, the gap, its owner, next action.

---

## Evaluation H, Tracking-plan definition (should not trigger)

### User prompt

> Define the analytics event, properties and metric for successful Saved Search creation.

### Should this skill trigger?

NO. Defining the measurement contract is `prototype-testing-analytics` work.

### Primary owner

`prototype-testing-analytics`.

### Expected behavior (if this skill is invoked manually)

- Routes the definition of the event, its properties, its trigger semantics, and the metric to
  `prototype-testing-analytics`.
- States, at most briefly, this skill's later role: carrying the approved contract into the
  handoff and verifying that the build implements it.

### Pass criteria

- Routes by name and does not define the contract.

### Failure criteria

- Names the event, lists properties, or defines the metric or funnel.
- Writes analytics acceptance criteria for a contract that does not exist yet.

### Unnecessary-work checks

- Did not load any reference file.
- Did not produce a tracking plan, event schema, or dashboard suggestion.

---

## Evaluation I, Tracking implementation QA

### User prompt

> Our approved tracking plan says `saved_search_created` fires only after the server confirms creation. Engineering says it's done. Verify the implementation.

### Should this skill trigger?

YES.

### Primary owner

`delivery-product-collaboration`.

### Expected behavior

- Treats the approved tracking plan as the contract and verifies the build against it; does not
  redefine the event, trigger, or metric.
- Does not accept "engineering says it's done" as evidence.
- Checks, or sets out how to check, the trigger semantics: fires only after server-confirmed
  creation; not on click or attempt; not on a failed or rejected save; not twice on retry or
  double-submit.
- Checks required properties and privacy constraints against the plan when supplied; asks for the
  property list rather than inventing one when it is not.
- Names the evidence needed (network or analytics debugger on staging with success and forced
  failure paths) and marks the checks "not inspected" if there is no access.
- Classifies a mismatch as an implementation defect, or `Product/design decision required` if
  engineering proposes different semantics, with impact-based severity.

### Pass criteria

- Verification is framed against the approved contract.
- Failure and retry paths are included, not only the happy path.
- No property, event, or metric is invented or redefined.

### Failure criteria

- Redefines the event or proposes a different trigger as the new standard.
- Reports the event as verified without evidence.
- Expands into a full design QA of the Saved Search UI.

### Unnecessary-work checks

- Did not load the handoff reference.
- Did not fetch documentation.
- Kept the output to the analytics verification (quick or standard mode).

---

## Evaluation J, Simple developer question

### User prompt

> Dev asks whether this label is final or still placeholder copy.

### Should this skill trigger?

YES.

### Primary owner

`delivery-product-collaboration`.

### Expected behavior

- Uses Quick mode and answers only the question.
- Checks the supplied artifact for the label's content status (Final, Approved placeholder,
  Dynamic, Unknown…); with no artifact or content source supplied, says the status is unknown,
  asks for the source (design file, ticket, content doc) or names the content owner, and says not
  to treat the label as final until confirmed.

### Pass criteria

- A few lines; content-status vocabulary or equivalent; no guess presented as fact.

### Failure criteria

- Declares the label final (or placeholder) without evidence.
- Turns the question into a readiness review.

### Unnecessary-work checks

- Did not produce a manifest, a full readiness audit, or acceptance criteria.
- Did not audit responsive, accessibility, or state coverage.
- Did not load any reference file.

---

## Evaluation K, Technical constraint requires redesign

### User prompt

> Engineering confirmed that the API cannot support undo, but the approved interaction depends on undo. What do we do?

### Should this skill trigger?

YES.

### Primary owner

`delivery-product-collaboration` for recording and routing; the replacement interaction is owned
by `interaction-design`, with PM for the product trade-off.

### Expected behavior

- Records the limitation as a Confirmed technical constraint (asking who confirmed it and where,
  if that is not stated).
- Identifies the affected approved behavior: the undo affordance and what depends on it, the
  safety of the destructive action, related acceptance criteria, announcements, and any analytics
  trigger tied to undo.
- States that a product/design decision is required and routes the replacement interaction to
  `interaction-design`, with PM where the trade-off is about product risk.
- Summarises engineering-supplied alternatives only if any were given, as options for the owner,
  and asks engineering what they can support if none were.
- Notes the delivery consequence: the affected part is not Ready (or is conditioned) until the
  decision is made; afterwards the artifact, acceptance criteria, and change log are updated.

### Pass criteria

- The constraint, the affected behavior, the decision required, and its owner are all explicit.
- No replacement interaction is chosen or specified.

### Failure criteria

- Silently substitutes a confirmation dialog, or any other behavior, as the answer.
- Treats the constraint as an engineering detail that engineering can resolve alone.
- Ignores the effect on destructive-action safety or on the acceptance criteria.

### Unnecessary-work checks

- Did not redesign the flow or produce a new interaction spec.
- Did not produce a manifest or a QA report.
- Output sized as a decision packet: constraint, impact, decision required, owner, next step.

---

## Evaluation L, Visual redesign request (should not trigger)

### User prompt

> The implemented page feels too dense. Can you redesign the spacing, typography and hierarchy?

### Should this skill trigger?

NO. Visual redesign belongs to `ui-visual-design`.

### Primary owner

`ui-visual-design`.

### Expected behavior (if this skill is invoked manually)

- Routes the redesign of spacing, typography, and hierarchy to `ui-visual-design`.
- Distinguishes the two situations: if the build departs from the approved visual design (raw
  spacing instead of tokens, wrong type roles), that is an implementation mismatch this skill can
  document; if the build matches the approved design and still feels dense, the design itself
  needs revising, `ui-visual-design`.

### Pass criteria

- Routes by name; proposes no new values.

### Failure criteria

- Proposes new spacing values, a type scale, or a new hierarchy.
- Produces a redesigned layout or mockup.

### Unnecessary-work checks

- Did not run a full QA pass or produce handoff artifacts.
- Did not load any reference file unless an implementation mismatch was actually being documented.
