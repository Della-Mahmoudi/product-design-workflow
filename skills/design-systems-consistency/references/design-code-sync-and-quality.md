# Design-to-code synchronization and quality, executable guidance

Load for: design-system Figma/code parity audits (library component ↔ production component, Figma variable ↔
code token), Figma variables and Dev Mode inspection, alias-chain checks, component/property mapping, Code
Connect, Storybook stories and tests, accessibility automation, visual regression, documentation parity,
breaking API changes and quality gates. Load the Figma or Storybook sources themselves only when the team's
workflow uses those tools.

Scope: SYSTEM OBJECT ↔ SYSTEM OBJECT only, component names, anatomy, reusable props, variants, states, sizes,
tokens, modes, defaults, deprecations, reusable accessibility behaviour, Storybook stories and DS documentation.
A staging page, a built feature, or a screenshot of one product feature compared with approved screens is
FEATURE BUILD ↔ APPROVED FEATURE DESIGN work for `delivery-product-collaboration` (design QA, Ready for Dev,
release-blocking defects). Audit here only the specific reusable component or token behind such a finding, and
only when the user asks about that system-level mismatch.

Contents: 1 Source of truth · 2 Parity audit procedure · 3 Mismatch classification · 4 Figma variables and Dev
Mode · 5 Alias-chain inspection · 6 Component and property mapping · 7 Code Connect · 8 Storybook · 9 Testing
expectations · 10 Accessibility automation limits · 11 Visual regression and documentation parity · 12 Breaking
API changes · 13 Quality gates · 14 Output shapes

## 1. Source of truth (decide per decision, never globally)

Neither Figma nor code is right by default. For each mismatch ask which side encodes the *decision* the system
owners made: documented spec and governance decisions outrank both; an accessibility or platform requirement
outranks both; production behaviour that users rely on is strong evidence for code; an approved, published
library change that engineering has not shipped is "Figma ahead", not "code wrong". Record the chosen source of
truth per item.

## 2. Parity audit procedure

1. Scope the surface: which components/tokens, which Figma library version, which code package version.
2. Build the comparison table per component: name · purpose · anatomy regions · properties and values ·
   defaults · variants · states · sizes · tokens/variables per part · modes/themes · deprecated options ·
   accessibility behaviour · responsive behaviour · documentation.
3. Fill it from evidence: Figma (component properties panel, variables table, Dev Mode inspect, library
   changelog), code (prop types/API docs, Storybook stories, token source, tests), docs.
4. Mark each cell match / mismatch / unknown. Classify mismatches (section 3) and name the source of truth.
5. Recommend the smallest reconciliation per mismatch and whether it is breaking.
6. Record unresolved conflicts explicitly (owner, decision needed).

## 3. Mismatch classification

| Class | Meaning | Typical resolution |
|---|---|---|
| Figma ahead | Design added/changed something code lacks | Code change ticket; keep design marked "not yet in code" |
| Code ahead | Code has props/states/tokens design lacks | Add to library or declare code-only (documented) |
| Naming mismatch | Same concept, different names | Rename the side without consumers, or alias/map and document |
| Missing mapping | No link between a design object and its code counterpart | Add Code Connect mapping or docs mapping row |
| Unsupported Figma property | Design property with no code equivalent | Remove, mark documentation-only, or add code prop |
| Unsupported code prop | Code prop with no design representation | Add design property/variant or mark as engineering-only |
| Token mismatch | Different token/variable or value per part or mode | Fix the side that diverged from the role definition |
| State mismatch | States drawn vs. implemented differ | Complete the missing side; check precedence rules |
| Documentation mismatch | Docs describe neither side accurately | Update docs after resolving the above |
| Intentional divergence | Known, owned, documented difference | Keep; review date |
| Unknown | Insufficient evidence | List; do not guess |

## 4. Figma variables and Dev Mode (when the team uses variables)

- Model primitives, semantics and (optionally) component tokens as separate collections; modes live on the
  semantic collection. Scope variables so suggestions in Dev Mode are meaningful (colour variables scoped to
  fill/stroke/text as appropriate; dimensions to gap/padding/radius).
- Names mirror code token names segment for segment; agree one normalization rule for the differences the
  tools impose (slashes vs. dots vs. dashes, casing).
- Dev Mode shows variables in the Inspect panel and code snippets; the variable details view exposes name,
  source file, collection, current mode (switchable), value, scope and a snippet; with nothing selected an
  "Open variables table" read-only view is available. Suggested variables appear for raw values only when a
  variable with the exact same value and a fitting scope exists, a raw value with no suggestion is either a
  missing token or a scope problem.
- Mark primitives as not for direct use (naming prefix or description) so Dev Mode consumers reach for semantic
  variables; hide primitive collections from publishing where the team's convention allows.
- Styles vs. variables: if the product still uses styles for typography or effects, document which objects are
  styles and which are variables; do not report "no variables" as a defect when styles are the convention.

## 5. Alias-chain inspection

For a sampled set of components (high-traffic first), inspect each bound value: semantic alias → primitive →
raw value. Findings: (a) part bound to a primitive directly (bypass of the semantic layer); (b) part bound to a
semantic token of the wrong role (border using a text token); (c) raw value, no variable (hard-coded); (d) chain
broken across modes (value present in light, missing in dark); (e) code uses a different token for the same part.
Compare the chain in Figma with the alias chain in the token source/CSS output; they should resolve to the same
primitive per mode.

## 6. Component and property mapping

- One mapping row per component: Figma component (set) → code component; per property: Figma property (variant
  / boolean / instance swap / text) → code prop and value vocabulary → default. Mark Figma-only properties
  (e.g., a `State` variant used to draw states) and code-only props (e.g., `onClick`, `ref`).
- Rules: property names and values identical where tools allow; booleans in Figma map to booleans in code;
  instance-swap maps to a slot/children; text properties map to label/children; unsupported combinations are
  listed once and enforced on both sides.
- Keep the mapping where engineers look (Storybook docs page, Code Connect, or the component's doc page).

## 7. Code Connect (only if the team uses it)

Code Connect links code components to Figma components so that Dev Mode (and Figma's MCP server) shows the real
design-system code instead of autogenerated snippets. Two setup paths, usable together: the Code Connect UI inside
Figma (repository link or manual paths; Inspect shows file/component names and AI-generated previews rather than
snippets) and the CLI with template files, which maps Figma properties to the production component API and
publishes connections so snippets appear in Dev Mode. Access is plan- and seat-gated and those terms change:
confirm the team's current eligibility in Figma's Code Connect help article before recommending it (last-checked
terms and provenance in `source-map.md`). Plan limits can deactivate existing connections, so check a mapping's
status before reporting it missing. Use it to expose the property mapping from section 6 and to detect drift (a
Figma property that has no mapping is a finding).
When the team does not use it, a maintained mapping table is the deliverable; do not require Code Connect and do
not create implementation configuration unless asked.

## 8. Storybook (only if the team uses it)

- One story per meaningful variant and state that the design documents, including the "unhappy" ones (loading,
  disabled, invalid, long content, RTL, dark/high-contrast mode). Story names mirror design property vocabulary.
- Autodocs or MDX pages carry the same anatomy names, property table and do/don't guidance as the design docs;
  divergence here is a documentation mismatch.
- Interaction tests (play functions) encode the interaction contract: keyboard activation, focus return,
  announcements. They are the executable form of the accessibility contract's keyboard and focus rows.
- Accessibility addon: built on axe-core; results split into Violations / Passes / Incomplete (Incomplete must be
  checked manually); `parameters.a11y.test` is `'off' | 'todo' | 'error'`, use `'error'` for stable components
  so violations fail CI, `'todo'` while fixing legacy; default rules cover WCAG 2.0/2.1 A+AA plus best practices,
  while WCAG 2.2 and AAA rules are opt-in (axe `runOnly`), a WCAG 2.2 contract needs them enabled or checked
  manually; rules and context can be configured per project, file or story.

## 9. Testing expectations per reusable component

| Layer | Expectation |
|---|---|
| Unit/props | Every public prop value renders; invalid combinations rejected or documented |
| States | Each documented state reachable and visually/semantically distinct; precedence verified |
| Interaction | Keyboard activation, arrow/Escape/Home/End where applicable, focus order and return |
| Accessibility (automated) | axe/Storybook a11y clean at `'error'` for stable components |
| Accessibility (manual) | Proportional to interaction complexity and supported platforms (a static Badge needs far less than a Combobox): keyboard-only pass; screen reader pass on at least one desktop and one mobile AT; 200 % zoom and 320 px reflow; high-contrast / forced-colours; reduced motion; RTL |
| Visual regression | Snapshots per story per theme/mode; review diffs on token changes |
| Token/theme | Snapshot of resolved token values per mode; contrast pairs computed per mode |
| Parity | Mapping table or Code Connect has no unmapped properties |

## 10. Accessibility automation limits (state this in every parity or quality report that cites automation)

Automated accessibility testing does not replace manual accessibility validation. Storybook's own documentation
puts automated coverage at "up to 57 %" of WCAG issues; what it cannot judge includes accessible-name quality,
focus order sense, keyboard operability of custom widgets, announcement timing, content on hover/focus
behaviour, motion, cognitive load, and most of the APG pattern expectations. A green axe run is a necessary
gate, never a conformance claim: report it as "no automated violations under <ruleset>" plus the manual checks
still open, and never label a component "accessible" or "conformant" on that basis.

## 11. Visual regression and documentation parity

- Visual regression catches unintended drift when tokens or shared styles change; run it per theme/mode and
  per story; triage diffs as intended (token change) vs. regression.
- Documentation parity check: for each component, the design doc, the Storybook page and the Figma component
  description agree on purpose, anatomy names, property vocabulary, states, accessibility notes and status.
  Three sources that disagree are worse than one that is incomplete; consolidate or link to a single source.

## 12. Breaking API changes (design or code)

Detect: removed/renamed prop, value, slot, variant or variable without alias; changed default; changed anatomy
or sizing that shifts layouts; changed keyboard/focus semantics; token semantic or value change affecting
contrast or layout. Handle: deprecation alias and warning period; codemod or Figma swap guidance; changelog
entry mirrored in design and code; migration note with before/after; version bump by the package's convention.

## 13. Quality gates for design-to-code work

Fail or flag when: Figma and code APIs disagree with no named source of truth; a Figma property has no code
counterpart and is not marked documentation-only; code exposes behaviour design never specified; tokens resolve
to different primitives per side or per mode; states exist on one side only; stories/tests do not cover
documented states; automation is presented as full accessibility validation; a breaking change ships without
deprecation and migration notes; documentation describes neither side.

## 14. Output shapes

Parity report → scope and versions, comparison table, mismatch list with class and source of truth, smallest
reconciliation per item, breaking-change list, unresolved conflicts. Variables/Dev Mode review → collection
and mode structure, scope issues, alias-chain findings, naming alignment actions. Storybook/testing review →
story coverage vs. state matrix, a11y configuration, test gaps, manual validation checklist.

Sources synthesized here: Figma Help (Variables in Dev Mode; Code Connect) and Storybook accessibility-testing
docs (verified at construction time and re-checked in the v2 patch, see `source-map.md`); WCAG 2.2 and APG for
what automation cannot cover; the product's own tooling conventions (Tier 0) decide whether any of this applies.
