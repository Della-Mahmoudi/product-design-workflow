# Evaluation cases — design-systems-consistency (Skill 05)

Human-readable QA contract for this skill. `evals/evals.json` holds the same cases (same numbering) in the
skill-creator eval schema.

**How to grade**
- Grade the answer and the transcript: which reference files were read, which external sources were fetched,
  which tools were called. A run passes only if it meets every pass criterion and hits no failure criterion.
  Unnecessary-work checks are reported separately as efficiency findings.
- Negative-trigger cases (4, 5, 7) are graded as if the skill were invoked manually: the expected behaviour is a
  one-line routing to the owner and no work in that skill's territory. Trigger-rate benchmarking is a later phase.
- No fixtures are attached. Where a case depends on the product's own system (Tier 0), a good run asks for or
  inspects it, marks unknowns, and never invents inventory, values or modes.
- Cases 1–10 are the required set. Cases 11–12 add the positive twin of case 5 (reusable behaviour contract) and
  the automated-accessibility limit.
- Schema source: `skills/skill-creator/references/schemas.md` in `anthropics/skills`, checked 2026-10-20 —
  top-level `skill_name` and `evals`; per eval `id`, `prompt`, `expected_output`, `files`, `expectations`.

---

## Case 1 — DangerButton

**User prompt**
> We need a new DangerButton because delete actions need a red button.

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Names the decision: does a destructive action need a new component, or a semantic value on Button?
- Looks for Tier 0 evidence of an intent/kind/variant property on Button and destructive token roles; without it,
  marks the fact unknown and answers conditionally.
- Applies REUSE > COMPOSE > EXTEND > CREATE: REUSE if the intent value exists, otherwise EXTEND Button with
  `intent=destructive` (or the product's existing term) — token roles per state, inherited states, contrast per
  mode, Figma value and code enum added in the same non-breaking change.
- Quick mode: decision, evidence, recommendation, consequence.

**Pass criteria**
1. Challenges the new-component assumption and does not create DangerButton.
2. Recommends REUSE or EXTEND of Button with a semantic destructive intent, conditional on whether Button already
   has an intent property.
3. Names by meaning, not appearance: no `red=true`, no colour-named component.
4. Marks unknown Tier 0 facts as unknown.
5. Stays at the component decision.

**Failure criteria**
- Creates DangerButton or any colour-named component or property.
- Redesigns the delete screen, its layout or its confirmation flow.
- Asserts that Button has or lacks an intent property without evidence.
- Produces a component spec, RFC, migration plan, changelog or governance process.

**Unnecessary-work checks**
- Answers from SKILL.md; reads at most `references/component-architecture-and-states.md` (§12, §13).
- No web browsing or exemplar lookup; no token file, state matrix, Storybook or Code Connect work.

---

## Case 2 — 87 hex values

**User prompt**
> We found 87 hex values in the product. Convert all of them into design tokens.

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Refuses one-token-per-value conversion and runs the audit procedure instead: inventory usage and context,
  normalize, cluster primitives, assign roles, classify, decide layers, then map.
- Classification: existing-token bypass, legitimate role missing a token, accidental drift, intentional exception,
  unknown. Equal values with different roles stay separate.
- Migration mapping and prevention rules come after classification; component tokens and dark-mode values are not
  created by default.

**Pass criteria**
1. Does not produce 87 tokens or any one-to-one hex-to-token mapping.
2. Starts from an inventory of usage and context, or asks for it.
3. Separates primitive and semantic layers; semantic names come from roles, not values.
4. Uses the classification set including bypass, drift and intentional exception.
5. Keeps semantically distinct roles separate even when their values match.
6. Maps only after classification and states no token counts before the inventory exists.

**Failure criteria**
- Emits 87 tokens or a hex → token table.
- Invents token or role names without usage evidence.
- Forecasts primitive or role counts before the inventory.
- Merges roles because their hex values match; adds component tokens or dark-mode values by default.

**Unnecessary-work checks**
- Reads `references/token-architecture.md` (§6, §7, §8) only.
- No DTCG file unless asked; the DTCG spec is not fetched.

---

## Case 3 — Boolean explosion

**User prompt**
> Add compact, loading, icon-only, destructive, full-width, selected and mobile as boolean properties on Button.

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Classifies every condition before adding anything: compact → size (or density mode); loading → lifecycle state
  with busy exposure and stable width; icon-only → content model or IconButton, with a required accessible name;
  destructive → intent; full-width → layout prop or parent layout; selected → toggle semantics (`aria-pressed`,
  ToggleButton); mobile → responsive behaviour, not a property.
- Checks combinatorics, names invalid combinations, proposes a smaller enum-based model, checks code prop parity,
  and names breaking changes if existing booleans are folded into enums.

**Pass criteria**
1. Classifies all seven conditions into dimensions.
2. Rejects `mobile` as a property.
3. Identifies `selected` as a semantic change, not a visual variant.
4. Names at least two invalid or conflicting combinations and how each is prevented or enforced.
5. Proposes a smaller model (enums for intent and size; states separate from variants).
6. Addresses Figma/code API parity and breaking-change handling.

**Failure criteria**
- Adds all or most of the seven booleans as requested.
- Models loading or selected as values of intent/kind.
- Adds `mobile` or `isMobile`.
- Ignores the accessible-name requirement for icon-only.

**Unnecessary-work checks**
- Reads `references/component-architecture-and-states.md` (§4, §6, §15) only.
- No full variant grid or state matrix unless asked; no Storybook or Code Connect setup.

---

## Case 4 — Screen-level visual composition

**User prompt**
> Use our existing Card, Button and Badge components to make this pricing screen cleaner and improve the hierarchy.

**Should this skill trigger?** NO
**Primary owner:** `ui-visual-design`

**Expected behavior (if invoked manually)**
- One-line routing: composing a screen from existing components is screen-level work for `ui-visual-design`.
- Re-engages only if a reusable gap is found (`[DS GAP]`: a repeated need the existing components cannot meet).

**Pass criteria**
1. Names `ui-visual-design` as the owner.
2. Proposes no new component, variant, property or token.
3. Gives no layout, hierarchy, spacing or typography recommendations.
4. States the condition for returning: a reusable `[DS GAP]`.

**Failure criteria**
- Redesigns the pricing screen.
- Proposes a PricingCard component or new Card/Badge variants without a stated reusable gap.
- Runs a design-system audit of the screen.

**Unnecessary-work checks**
- No reference files loaded; no browsing.

---

## Case 5 — Feature-specific interaction

**User prompt**
> When file upload partially fails, should retry happen per file or for the whole batch?

**Should this skill trigger?** NO
**Primary owner:** `interaction-design`

**Expected behavior (if invoked manually)**
- One-line routing: retry scope after a partial failure is one feature's behaviour.
- Does not turn the decision into a system property. At most names the evidence (the same behaviour needed across
  features) that would make a reusable contract worth evaluating (see case 11).

**Pass criteria**
1. Routes to `interaction-design`.
2. Does not answer per-file vs batch itself.
3. Adds no retry props or states to a reusable FileUpload.

**Failure criteria**
- Designs the retry behaviour, its states or its copy.
- Adds `retryMode`, `batchRetry` or similar to a system component.

**Unnecessary-work checks**
- No reference files loaded; no APG or WCAG lookups.

---

## Case 6 — Design-system Figma/code parity

**User prompt**
> Our Button has `intent=destructive` and `size=compact` in Figma, but the production Button component does not
> support those props. Audit the mismatch.

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency` (SYSTEM OBJECT ↔ SYSTEM OBJECT)

**Expected behavior**
- Scopes the audit to Button: library version, code package version, the two properties.
- Gathers both sides (Figma properties; code props/types, Storybook) and marks gaps unknown.
- Checks for existing code equivalents (`kind="danger"`, `size="sm"`) before proposing new props.
- Classifies each mismatch (Figma ahead, unsupported Figma property, naming mismatch), names a source of truth per
  item without defaulting to Figma, recommends the smallest reconciliation, and states breaking-change status.
- Covers reusable accessibility: compact size vs the 24×24 CSS px minimum (WCAG 2.2 2.5.8), destructive contrast
  and visible states per mode.

**Pass criteria**
1. Treats this as system parity, not feature QA.
2. Asks for or inspects evidence from both sides.
3. Checks for existing code equivalents first.
4. Classifies mismatches with a named source of truth per item.
5. Gives the smallest reconciliation and its breaking status.
6. Covers the target-size and contrast implications.

**Failure criteria**
- Declares Figma (or code) correct by default.
- Produces release-blocking severities or feature acceptance criteria.
- Adds new props without checking existing equivalents.
- Requires Code Connect.

**Unnecessary-work checks**
- Reads `references/design-code-sync-and-quality.md` (§1, §3, §6, §12), plus at most
  `references/component-architecture-and-states.md`.
- No Code Connect configuration; no Figma docs fetched unless the team uses those tools.

---

## Case 7 — Feature implementation QA

**User prompt**
> The checkout page is built on staging. Compare it against the approved Figma screens and tell me what should
> block release.

**Should this skill trigger?** NO
**Primary owner:** `delivery-product-collaboration` (FEATURE BUILD ↔ APPROVED FEATURE DESIGN)

**Expected behavior (if invoked manually)**
- One-line routing: staging build vs approved screens and release blockers are feature build QA.
- Notes that a specific reusable component or token mismatch found there can come back as a system-parity question.

**Pass criteria**
1. Routes to `delivery-product-collaboration`.
2. Does not compare the screens or list defects.
3. Does not decide release blockers or severities.
4. States the condition for returning (a reusable component/token mismatch).

**Failure criteria**
- Runs design QA of the checkout.
- Loads `references/design-code-sync-and-quality.md` to audit the page.

**Unnecessary-work checks**
- No reference files loaded; no browsing.

---

## Case 8 — Token rename and migration

**User prompt**
> We want to rename `color.brand.primary` to `color.action.primary.background`. Can we just rename it in Figma?

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- No Figma-only rename: count consumers in Figma, code (CSS variables, generated outputs, downstream packages)
  and docs first.
- Distinguishes rename from semantic change: `brand` and `action` are different roles. If `color.brand.primary`
  has non-action uses (brand marks, links, highlights), this is a split — add the action role aliasing the same
  primitive, migrate action uses, keep or re-scope the brand role.
- Deprecated alias and compatibility window; name and value changes in separate steps; removal only at zero
  consumers or with an accepted break.

**Pass criteria**
1. Does not approve a Figma-only rename and names code and docs as consumers.
2. Separates rename from semantic change and flags the possible split.
3. Recommends a deprecated alias pointing to the new token.
4. States the breaking conditions (removal without alias breaks; aliased rename with unchanged value does not).

**Failure criteria**
- "Yes, just rename it in Figma."
- Treats Figma as the only consumer.
- Renames or deletes without an alias.
- Invents consumer counts.

**Unnecessary-work checks**
- Reads `references/token-architecture.md` (§7, §9); `references/governance-and-consistency.md` only if the
  deprecation lifecycle is asked about.
- No DTCG fetch; no full token file.

---

## Case 9 — One-off local exception

**User prompt**
> This campaign card needs a unique gradient that will never be reused. Should we add it to the core token system?

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Keeps it out of the core token system: a genuinely one-off marketing surface is an allowed, documented exception.
- Documents the exception: reason, scope, owner, review or expiry date, retirement path.
- Names the evidence that would justify tokenizing later (reuse across campaigns or surfaces).

**Pass criteria**
1. Advises against core tokenization.
2. Recommends a documented intentional exception with owner and review date.
3. States the reuse evidence that would change the answer.
4. Creates no campaign mode, theme or component token.

**Failure criteria**
- Adds a campaign gradient token to the core set by default.
- Insists every raw value must be tokenized.
- Leaves the exception undocumented.

**Unnecessary-work checks**
- Quick mode; reads at most `references/token-architecture.md` (§4, §8).
- No governance RFC; no DTCG gradient file.

---

## Case 10 — Missing inventory

**User prompt**
> Do we already have a component for this pattern? If not, create one.

No Figma, library or code context is provided.

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- States that existence cannot be confirmed without Tier 0 evidence; asks what the pattern is.
- Lists what to inspect: library components with properties and variants, local components, tokens/variables,
  code components and props, Storybook, docs — or inspects them if the session has access.
- Explains the REUSE > COMPOSE > EXTEND > CREATE sequence and the CREATE evidence bar; any recommendation is
  conditional.

**Pass criteria**
1. Makes no claim that a component exists or does not exist.
2. Asks what the pattern is.
3. Lists the Tier 0 sources to inspect.
4. Explains the decision sequence and the CREATE evidence bar.
5. Keeps any recommendation conditional.

**Failure criteria**
- Claims a matching component exists, or that none exists.
- Produces a new component spec, API or anatomy.
- Labels REUSE or CREATE as confirmed.

**Unnecessary-work checks**
- Reads at most `references/component-architecture-and-states.md` (§12); no browsing.

---

## Case 11 — Reusable behaviour contract (positive twin of case 5)

**User prompt**
> What states and keyboard/focus behavior must our reusable FileUpload component support across products?

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Treats this as what every FileUpload instance guarantees, not one feature's behaviour.
- States derived from behaviour: default, hover, focus-visible, disabled, drag-over, uploading/progress,
  error/invalid, success where the products use it.
- Keyboard/focus contract: drag and drop is never the only path (keyboard-operable browse control or native file
  input); focus is managed after files are added or removed; per-file actions have accessible names; progress,
  completion and errors are announced and associated.
- Leaves retry scope, file limits and error copy to `interaction-design` or product configuration.

**Pass criteria**
1. Owns the reusable contract.
2. Derives states from behaviour.
3. Defines a keyboard/focus contract that does not depend on drag and drop.
4. Requires accessible names and announcements.
5. Keeps feature policy out of the contract.

**Failure criteria**
- Prescribes per-file vs batch retry as system behaviour.
- Defines a pointer-only or drop-zone-only contract.
- Claims accessibility from automated checks.

**Unnecessary-work checks**
- Reads `references/component-architecture-and-states.md` (§7, §10); APG only for a specific widget question.
- No visual design.

---

## Case 12 — Automated accessibility is not validation

**User prompt**
> Storybook's accessibility addon shows zero violations for our Combobox. Can we mark it as 'accessible' in the
> design-system docs?

**Should this skill trigger?** YES
**Primary owner:** `design-systems-consistency`

**Expected behavior**
- Declines the "accessible" label on automated evidence alone: axe covers part of WCAG, Incomplete results need
  manual review, and the default ruleset covers WCAG 2.0/2.1 A/AA, so WCAG 2.2 rules must be enabled or checked
  manually.
- Manual checks proportional to a Combobox: keyboard model, focus management, screen-reader announcements on at
  least one desktop and one mobile assistive technology, zoom/reflow, forced colours.
- Accurate docs wording: "no automated violations under <ruleset>; manual validation pending".

**Pass criteria**
1. Does not approve "accessible" or "conformant" from automation.
2. Explains automated coverage limits and Incomplete results.
3. Notes that WCAG 2.2 rules are opt-in.
4. Lists Combobox-proportional manual checks.
5. Proposes accurate documentation wording.

**Failure criteria**
- Approves the label.
- Treats Incomplete results as passes.

**Unnecessary-work checks**
- Reads `references/design-code-sync-and-quality.md` (§8, §10), plus at most
  `references/component-architecture-and-states.md` (§10).
- No Storybook docs fetch; the needed facts are already in the references.
