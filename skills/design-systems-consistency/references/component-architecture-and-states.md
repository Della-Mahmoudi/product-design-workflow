# Component architecture and states — executable guidance

Load for: component anatomy, properties, variants, sizes, states, accessibility contracts, responsive and
content behaviour, component families, and reuse / compose / extend / create decisions that go beyond a
one-line answer. Do not load for a token-only task. This file defines what every instance of a reusable component
guarantees; what one feature flow does (retry scope, recovery, async outcome) belongs to `interaction-design`.

Contents: 1 Purpose test · 2 Anatomy · 3 Composition · 4 Property model · 5 Semantic naming · 6 Combinatorics ·
7 States · 8 Responsive behaviour · 9 Content constraints · 10 Accessibility contract · 11 RTL and localization ·
12 Reuse vs compose vs extend vs create · 13 Component families · 14 API consistency · 15 Worked mappings ·
16 Output shapes

## 1. Purpose test

Write one sentence: "*Component* lets a person *do/see X* in *context Y*." If two candidate components have the
same sentence, they are one component. If a proposed component's sentence only differs by appearance ("…but
red", "…but on the marketing site"), it is a variant, a token change, or an exception — not a component.

## 2. Anatomy

- Name every region once and reuse the names across design, code and docs (container, leading icon, label,
  trailing icon, helper text, counter…). Mark each region **required** or **optional**; optional regions are
  the usual source of booleans and slots.
- Fix the structural rules that do not vary: order of regions, alignment, minimum/maximum sizes, which regions
  stretch, which truncate or wrap.
- Anatomy belongs to the component family: Button, IconButton and ToggleButton share container/label/icon rules
  so that extending one does not fork the others.

## 3. Composition

- Prefer composition when the need is "this plus that": a card with an action row, a field with a prefix, a
  list item with a badge. Provide **slots/children** (content regions typed loosely) rather than props for every
  conceivable inner element.
- Compound components (Menu + MenuItem, Tabs + Tab + TabPanel) express structure and keep accessibility
  relationships in one place; prefer them over config-object props.
- A composition is a *pattern* worth documenting (not a component) when it repeats with the same parts and the
  same rules but needs no new API surface.
- Do not compose around a missing semantic: if every "dangerous confirm" composes Button + red icon + manual
  colour override, the missing thing is `intent=destructive` on Button (EXTEND), not a pattern.

## 4. Property model

Properties represent meaningful, orthogonal dimensions. Use this taxonomy before adding anything:

| Dimension | Typical name | Type | Belongs to |
|---|---|---|---|
| Semantic purpose of the action/content | `intent` / `kind` / `variant`: primary, secondary, tertiary, destructive/danger… | enum | variant |
| Visual emphasis within the same intent | `emphasis` / `hierarchy` / `appearance`: filled, outlined, ghost | enum | variant (only if orthogonal to intent in the product) |
| Size | `size`: sm / md / lg (product scale) | enum | variant |
| Density | mode or `density` | mode or enum | tokens/mode, rarely a prop |
| Visual feedback state | hover, active/pressed (momentary), focus-visible | drawn (Figma `State` property marked documentation-only); CSS/platform states in code, never a prop | state, not variant |
| Interaction/lifecycle state | `disabled`, `loading`, `selected`/`pressed` (toggle), `checked`, `expanded`, `invalid`, `readOnly` | state (boolean or enum) | state, not variant |
| Content presence | label, icon slots, `iconOnly`/label visibility | content props / slots | content |
| Layout participation | `fullWidth`/`block`, alignment | layout prop or parent layout | layout |
| Platform convention | — | not a boolean: platform theme/mode or a platform implementation of the same API | platform |
| Responsive/viewport behaviour | — | not a property: component responsive rules, or the parent layout sets `size` | responsive rules / tokens |
| Feature-only condition (true for one screen or flow) | — | not a system property: local composition, documented exception, or feature behaviour (`interaction-design`) | feature |

Rules:
- Classify every requested condition into exactly one row before adding anything; one that fits no row is
  usually feature logic, not a system property.
- One concept, one property. `kind=danger` and `destructive=true` cannot coexist.
- Enums for anything with three or more mutually exclusive values, or two values likely to grow. Booleans only
  for true binary, orthogonal switches (`disabled`, `fullWidth`).
- States are not variants: do not model `loading` or `selected` as values of `kind`.
- Defaults must be the most common safe choice and identical in Figma and code.
- A property that only one screen needs is not a property; it is an override or an exception.
- Responsive behaviour is not a property value (`mobile=true`): define how the component behaves across
  containers/breakpoints, or let a size prop be set by the consuming layout.

## 5. Semantic naming

- Prefer names stable under restyling: `intent=destructive` over `red=true`; `hierarchy=primary|secondary|
  tertiary` over `style1|style2|style3`; `size=sm|md|lg` over `compact=true` when a size scale exists.
- Keep the vocabulary shared across components and tokens (same words for intent, size, state).
- Preserve the product's established terminology when it is already consistent (Carbon says `kind`, others say
  `variant`; the point is one word per concept, not the exemplar's word). Rename only with a migration plan.
- Name Figma properties and code props identically where the tool allows; where it cannot (spaces, casing),
  document the mapping once.

## 6. Combinatorics and variant explosion

- Variant count = product of the enum cardinalities × state values that must be drawn. Compute it before adding
  a dimension: 4 intents × 3 sizes × 6 states = 72; add a boolean and it is 144.
- Prevention tactics, in order: (1) move states out of the variant grid where the tool supports interactive
  states or where documentation can show a state matrix instead; (2) make content presence a boolean/instance
  property or slot, not a variant; (3) make size a property only at the scale the product really uses (two sizes
  that differ by 2 px are one size); (4) reject dimensions that are not orthogonal (an "outlined destructive
  ghost" that never exists should not be producible); (5) split a genuinely different anatomy into a family
  member (IconButton) instead of a boolean that mutates half the anatomy.
- Invalid combinations must be either impossible by construction (enum design, family split) or explicitly
  documented and enforced (lint, prop types, Figma property visibility). "We trust people not to use it" fails
  the quality gate.
- Document the allowed matrix (intent × emphasis, size × content) in one table; it doubles as the Figma variant
  plan and the Storybook story list.

## 7. States

Candidate states: default, hover, focus-visible, pressed/active, selected, disabled, loading, error/invalid,
success, warning, read-only, expanded/collapsed, checked/unchecked/indeterminate, dragging, visited (links).
Derive the set from behaviour, not from the list:

| Component behaviour | States it must define |
|---|---|
| Any pointer-operable control | default, hover, pressed, focus-visible, disabled |
| Toggles / selectable items | + selected (or checked; indeterminate only for group parents) |
| Async actions | + loading (and what is disabled/announced while loading) |
| Form inputs | + invalid/error, read-only, and filled vs empty where styling differs; success/warning only if the product uses them |
| Disclosure, accordion, tree | + expanded/collapsed |
| Links | + visited where the product shows it |

Rules:
- Define **precedence** when states coexist: typically disabled ⟶ loading ⟶ pressed ⟶ hover ⟶ default, with
  focus-visible drawn independently of all of them; selected combines with hover/pressed.
- `focus-visible` is mandatory for anything keyboard-operable; hover alone is never sufficient. Focus styling
  comes from a shared focus token/style, not per-component colours.
- Disabled: decide and document whether the control is removed from the tab order (native `disabled`) or kept
  focusable with `aria-disabled` and a reason (the latter helps discoverability of why an action is unavailable).
  Disabled visuals are exempt from contrast minimums but must still read as disabled.
- Loading: keep dimensions stable, prevent duplicate submission, expose the busy state to assistive technology,
  and decide whether the label stays visible.
- Selected on a Button means it is a toggle; that changes semantics (`aria-pressed` or a Switch/Checkbox) and
  usually the family member (ToggleButton), not just the look.
- A state matrix (state × intent/size, listing token per part) is the deliverable for a state audit.

## 8. Responsive behaviour

- In the component: intrinsic sizing, min-height for touch targets, wrapping vs. truncation rules, icon-only
  collapse rules if the component owns them, scroll/overflow behaviour of its own content.
- In the parent layout or via tokens/modes: width, placement, stacking order, density, breakpoint-specific size.
- Targets: at least 24×24 CSS px or the spacing exception (WCAG 2.2 2.5.8, AA); prefer ≥ 44×44 for primary touch
  controls where the platform guidance says so (2.5.5 AAA / platform HIGs). Reflow to 320 CSS px without
  two-dimensional scrolling (1.4.10).
- Never add a `mobile` variant; if touch needs a larger control, that is a size or a density mode.

## 9. Content constraints

- Specify per text region: minimum/maximum recommended length, wrapping or truncation (and where the ellipsis
  goes), whether truncated text gets a tooltip or an accessible full name.
- Plan for text expansion in translation (commonly 30–35 % longer than English, more for short strings — a
  heuristic, not a standard); icon-only controls avoid expansion but require accessible names.
- Icon + label rules: position, spacing token, whether icon is decorative (hidden from AT) or meaningful.
- Formatting (dates, numbers, currencies, plurals) is the content layer's job, not the component's.
- Content guidelines (voice, casing, verbs for buttons) are documentation attached to the component, not props.

## 10. Accessibility contract (fill only the relevant rows)

| Item | Define |
|---|---|
| Native element / platform control | e.g., `<button>`, `<a href>`, `<input type=checkbox>`; ARIA only when native cannot express it |
| Role | native or explicit (APG pattern name if a composite widget) |
| Accessible name | source (visible label, `aria-label`, `aria-labelledby`); required for icon-only |
| States/properties exposed | `aria-pressed`, `aria-expanded`, `aria-disabled`, `aria-busy`, `aria-invalid`, `aria-selected`, `aria-checked`… |
| Keyboard | activation keys, arrow-key model (roving tabindex vs. active-descendant), Escape, Home/End, type-ahead |
| Focus | order, initial focus, focus return on close, focus trap only for modal dialogs, focus not obscured by sticky UI (2.4.11) |
| Focus visibility | shared indicator; 3:1 against adjacent colours (1.4.11); 2 px perimeter / 3:1 change if targeting AAA (2.4.13) |
| Announcements | live region or status role for async results (4.1.3); error messages associated to the field |
| Contrast | text 4.5:1 (3:1 large) (1.4.3); boundaries and state indicators 3:1 (1.4.11); per mode |
| Target size | 24×24 CSS px minimum or spacing exception (2.5.8) |
| Motion | respect reduced-motion; no essential information in animation alone |
| High contrast / forced colours | boundaries survive without shadows; focus and selection remain visible |
| Error behaviour | how invalid is shown, announced and associated; no colour-only signalling |
| Disabled behaviour | focusable or not; reason exposure |
| RTL / text expansion | see section 11 |

Automated checks (axe, Storybook a11y) cover a subset of these; the contract is verified by keyboard, screen
reader, zoom and contrast checks, scaled to the component's interaction complexity. Do not claim conformance from
automation alone. The contract states what every instance guarantees; how one feature uses the component (retry
scope, error copy, batch behaviour) is `interaction-design` work.

## 11. RTL and localization resilience

- Use logical properties and start/end naming (`paddingInlineStart`, `leading`/`trailing` icons) instead of
  left/right; Figma: build with auto layout that mirrors cleanly and test with RTL preview.
- Maintain the list of icons that must mirror (directional: back, forward, next, undo) vs. must not (clock,
  checkmark, media play by convention — check the product's icon guidelines).
- Keep text regions flexible in width; avoid fixed-width labels; allow two-line wrap where the product permits.
- Numbers, bidi punctuation and mixed-direction strings need the content layer to isolate direction; the
  component should not break when it happens.

## 12. Reuse vs compose vs extend vs create

| Decision | Choose when | Required evidence |
|---|---|---|
| REUSE | An existing component (possibly with a property value nobody noticed) already has the same purpose sentence | Locate it; name the property/value |
| COMPOSE | Existing components combined in a documented arrangement solve it with no new API | Show the composition; add it to patterns docs if repeated |
| EXTEND | Same purpose and anatomy; a missing value, state, size, slot or token role | ≥ 2 real occurrences or a product-wide rule; orthogonal to existing properties; code can support the same API; invalid combos handled; parity plan |
| CREATE | Distinct purpose sentence, distinct anatomy or interaction responsibility, repeated need, composition would be brittle | All of: repeated need, distinct semantic purpose, evidence existing/compose fails, anatomy, interaction contract, properties, states, a11y contract, responsive rules, content constraints, token mapping, design owner, code owner or implementation path, documentation, test expectations |

Not evidence for CREATE: one screen, visual similarity, a stakeholder's preferred name, convenience, a colour
difference, a one-off layout, a behaviour that exists only because of one feature flow (decide it in
`interaction-design`; promote it into the system only when reuse across features is evidenced). If the evidence
bar is unmet, return EXTEND/COMPOSE with the gap list, or an *exception* (time-boxed local override with owner)
when the need is real but not yet repeated.

## 13. Component families

- A family shares anatomy rules, token roles, states and vocabulary; members differ in interaction
  responsibility or anatomy, not colour: Button / IconButton / ToggleButton / LinkButton (if links styled as
  buttons are allowed) / SplitButton / MenuButton.
- Add a member when a boolean would mutate anatomy or semantics (icon-only removes the label and changes naming
  requirements; toggle changes the ARIA contract; menu button adds a popup). Add a property when only values
  change (intent, size, emphasis).
- Never name a member after a colour or a screen (`DangerButton`, `CheckoutButton`). Destructive is an intent
  value on the family, with its own token roles and documented pairing rules (confirmation, placement).

## 14. API consistency

- Same prop names, value vocabularies, defaults, event names and slot names across the whole library. A
  checklist per new or changed component: `size` scale identical, `disabled` semantics identical, `intent`
  vocabulary identical, icon slot names identical, controlled/uncontrolled pattern identical.
- Figma property names and values mirror code (`Size: sm` ↔ `size="sm"`); Figma-only properties (e.g., a
  `State` variant property used for documentation) are marked as not part of the code API.
- Deprecate, do not break: keep old prop names working with warnings for a release window; map old Figma
  variants to new properties via the library's swap/rename tooling.

## 15. Worked mappings (illustrative patterns; always confirm against the real system)

Pattern: *a colour- or screen-named component is requested for an existing component's job* (a red button for
delete flows, a green banner for success pages).
→ Search the existing component for its intent/kind/variant property and values; if the intent exists: REUSE and
point to it. If not: EXTEND with a semantic intent value in the product's existing vocabulary (token roles for the
intent's background/text/border and their hover/pressed/disabled/focus), states inherited, usage guidance in docs
(e.g., confirm-before-destroy), Figma value + code enum value added in the same change, non-breaking. Never
CREATE a colour-named component.

Pattern: *a batch of booleans is requested that mixes size, state, content, intent, layout and viewport* (compact,
loading, icon-only, destructive, full-width, selected, mobile — or dense, error, with-avatar, clickable,
highlighted, tablet on a list item).
→ Sort each into its dimension first: size words = `size` enum value or density mode; loading/error/selected =
states (loading with busy exposure/announcement and stable width; selected implies toggle semantics →
ToggleButton / `aria-pressed`, not a visual variant); icon-only / with-avatar = content model (slot or boolean
with an accessible-name rule, or the family member whose anatomy already differs); destructive = `intent` enum
value; full-width = layout prop or parent layout (a boolean is acceptable only if orthogonal and already
conventional); mobile/tablet = not a property (responsive rules + size/density); anything true for only one
feature = not a system property. Then document invalid combos
(state precedence such as loading + disabled, icon-only without accessible name, selected on a non-toggle), check
that code props exist or can be added with the same names, and name breaking changes (folding existing booleans
into enums needs deprecation aliases and Figma value remapping).

## 16. Output shapes

Quick → Decision, evidence from the existing object, recommendation, consequence.
Standard → Decision, current anatomy/properties/states, gap, proposed property/state/token changes, a11y
implications, Figma/code implications, breaking-change risk, migration need, rationale.
Deep → add property matrix (allowed combinations), state matrix (state × variant × token per part), accessibility
contract table, family map, parity notes, migration plan.

Sources synthesized here: the product's own system (Tier 0, always); WCAG 2.2 and WAI-ARIA APG (web behaviour);
Carbon and Material 3 as component/state exemplars; *Designing Interfaces* 3e (component reuse, nesting and
inheritance, consistency as the antidote to UX debt). See `source-map.md`.
