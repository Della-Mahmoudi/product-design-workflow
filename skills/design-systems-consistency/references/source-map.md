# Source map, provenance, authority and routing

Read this when you need to know *which* source governs a decision, how to resolve a conflict between sources, or
whether a source may be consulted at runtime. Every other reference file in this skill is an original synthesis
built from the sources below; none reproduces substantial text from any of them.

## Authority tiers (summary)

| Tier | What | Role in a decision |
|---|---|---|
| 0 | The product's own system: Figma library, production component library, tokens/variables, component APIs, documented patterns, contribution and governance rules, accessibility contract, platform constraints | The actual design system. Highest contextual authority. Not automatically correct: flag conflicts with accessibility, legal or platform requirements. |
| 1 | Normative/implementation specifications: DTCG Format 2025.10, WCAG 2.2, WAI-ARIA APG | Stronger requirements inside their own domain only. Use selectively. |
| 2 | Mature exemplars: Carbon, Fluent 2, Material 3, Storybook, *Designing Interfaces* (3rd ed.) | Comparative reasoning about architecture, patterns, documentation, quality. Never the user's system. |
| 3 | Tool bridge: Figma Variables / Dev Mode, Figma Code Connect | Only when design-system design-to-code synchronization is in scope and the team uses the tool. Feature build QA belongs to `delivery-product-collaboration`. |

Conflict order: exact decision → product constraints → accessibility/platform requirements → current system
conventions → production code/API behaviour → relevant Tier 1 spec → exemplars as comparison → prefer
backward-compatible evolution → name breaking changes explicitly → record unresolved design/code conflicts.
Never blend Carbon, Fluent, Material and product conventions into a hybrid.

## Source records

### The product's own system (Tier 0)
- **Identity:** whatever the user supplies or the session can inspect: Figma files/libraries, variables, styles,
  component properties, code components, Storybook, docs, Code Connect mappings, audit data, platform rules.
- **Use for:** every decision. Search it before proposing anything new.
- **When not to use:** never ignore it; but do not treat existing behaviour as proof of correctness.
- **Conflict rule:** wins on conventions, naming, ownership and scope; loses to WCAG/platform/legal requirements,
  which must be flagged (not silently overridden either way).
- **Access:** supplied by the user or inspected via session tools. Mark anything not supplied as *unknown*.
- **Runtime:** always relevant.

### DTCG, Design Tokens Format Module 2025.10 (Tier 1)
- **Identity:** https://www.designtokens.org/TR/2025.10/format/, Design Tokens Community Group, Final Community
  Group Report dated 28 October 2025; the document states it is "considered stable". Companion: Color Module
  2025.10 (same date) defines the colour value object.
- **Verified at construction time (2026-10-20):** token properties `$value` (required), `$type`, `$description`,
  `$extensions`, `$deprecated`; group properties `$description`, `$type`, `$extends`, `$deprecated`,
  `$extensions`; `$root` reserved; curly-brace aliases `{group.token}` that may chain (no cycles) plus JSON
  Pointer `$ref`; type inheritance from alias target, else nearest group `$type`, else invalid (tools must not
  guess); primitive types color, dimension, fontFamily, fontWeight, duration, cubicBezier, number; composite
  types strokeStyle, border, transition, shadow, gradient, typography; colour `$value` is an object
  (`colorSpace`, `components`, optional `alpha` default 1, optional 6-digit `hex` fallback) with 14 colour
  spaces (srgb, srgb-linear, hsl, hwb, lab, lch, oklab, oklch, display-p3, a98-rgb, prophoto-rgb, rec2020,
  xyz-d65, xyz-d50); dimension `$value` is `{value, unit}` with unit `px` or `rem`; file extensions `.tokens` /
  `.tokens.json`; media type `application/design-tokens+json`.
- **Use for:** machine-readable token artifacts, token types, alias/reference structure, cross-tool exchange,
  deprecation metadata.
- **When not to use:** conceptual token audits or naming discussions; do not force DTCG syntax there. Do not treat
  later drafts or resolver previews as more authoritative than 2025.10 unless the user asks to evaluate a draft.
- **Conflict rule:** governs *format*; the product's semantics and naming still come from Tier 0. Many tools
  still emit the pre-2025 string forms (`"#2457F5"`, `"16px"`): check the consuming tool's support before
  insisting on object values.
- **Licensing/access:** public W3C Community Group report; free to read; cite rather than copy.
- **Runtime:** conditional, consult only when actual token format matters.

### WCAG 2.2 (Tier 1)
- **Identity:** https://www.w3.org/TR/WCAG22/, W3C Recommendation, 12 December 2024 edition.
- **Verified at construction time:** 1.4.3 Contrast (Minimum) AA 4.5:1 text / 3:1 large text; 1.4.11 Non-text
  Contrast AA 3:1 for UI components and graphical objects; 1.4.10 Reflow AA (320 CSS px); 1.4.12 Text Spacing AA;
  1.4.13 Content on Hover or Focus AA; 2.1.1 Keyboard A; 2.1.2 No Keyboard Trap A; 2.4.3 Focus Order A; 2.4.7
  Focus Visible AA; 2.4.11 Focus Not Obscured (Minimum) AA; 2.4.12 (Enhanced) AAA; 2.4.13 Focus Appearance AAA
  (2 CSS px perimeter, 3:1 change); 2.5.7 Dragging Movements AA; 2.5.8 Target Size (Minimum) AA 24×24 CSS px with
  exceptions spacing / equivalent / inline / user-agent control / essential; 2.5.5 Target Size (Enhanced) AAA
  44×44; 3.2.6 Consistent Help A; 3.3.7 Redundant Entry A; 3.3.8 Accessible Authentication (Minimum) AA; 3.3.9
  (Enhanced) AAA; 2.3.3 Animation from Interactions AAA; 1.3.1 Info and Relationships A; 4.1.1 Parsing is
  obsolete and removed in 2.2. (3.2.3 Consistent Navigation AA, 3.2.4 Consistent Identification AA, 4.1.2 Name
  Role Value A and 4.1.3 Status Messages AA are carried over unchanged from 2.1, not re-fetched at construction
  time; high confidence from the standard's stable history.)
- **Use for:** the accessibility requirements a reusable component must satisfy (contrast, focus, keyboard,
  target size, states exposed programmatically, motion, consistency of identification).
- **When not to use:** as a design-system architecture guide; it says nothing about tokens or variants.
- **Conflict rule:** overrides Tier 0 conventions where applicable; always flag, never silently rewrite.
- **Licensing/access:** public W3C document; cite success-criterion numbers rather than copying text.
- **Runtime:** conditional, consult for the specific criterion when it is decision-relevant.

### WAI-ARIA Authoring Practices Guide, APG (Tier 1, applicability-limited)
- **Identity:** https://www.w3.org/WAI/ARIA/apg/, W3C WAI guide with Patterns (e.g., Button, Switch, Tabs,
  Dialog, Combobox, Listbox, Menu/Menubar, Menu Button, Radio Group, Slider, Tooltip, Tree View, Toolbar,
  Disclosure, Accordion, Grid, Treegrid, Feed, Alert; check the live index for the current set) and Practices
  (e.g., Read Me First, Landmarks, Names and Descriptions, Keyboard Interface).
- **Verified at construction time:** "No ARIA is better than Bad ARIA"; "A role is a promise" (roles do not add
  keyboard behaviour or styling); interoperability testing with assistive technology is essential before using
  the guide's code in production; the guide does not indicate mobile/touch compatibility of examples.
- **Use for:** roles, states/properties, keyboard behaviour and focus behaviour of reusable *web* widgets when
  native HTML cannot express the semantics.
- **When not to use:** when a native element already solves it; for non-web platforms (use the platform's
  accessibility guidelines); as proof of WCAG conformance.
- **Conflict rule:** implementation guidance, not a conformance standard; WCAG requirements and real AT testing
  outrank an APG example.
- **Licensing/access:** public; cite the pattern name rather than copying code.
- **Runtime:** conditional, the specific pattern page only when a widget's interaction contract is being defined.

### Carbon Design System (Tier 2 exemplar)
- **Identity:** https://carbondesignsystem.com/, IBM's open-source system. At construction time (re-checked
  2026-10-20) the site organizes Foundations (Color, Themes, Typography, Spacing, Motion, Icons, Accessibility),
  Components, Patterns, Contributing (including a product development lifecycle and component checklist) and
  Migrating; component pages carry Guidelines / Specifications / Code / Accessibility tabs and a status label
  (e.g., "Stable"). Behaviour
  planned for the next major release is previewed behind opt-in feature flags (code flags plus a boolean
  property in the design kit) that become defaults at that major, a useful exemplar for staged breaking
  changes. Version numbers and release timing change: check the current release before citing either.
- **Verified exemplar facts (Button kinds and sizes re-checked 2026-10-20):** colour tokens are role-named per UI
  element (background, layer, field, border, text, link, icon, support, focus, interactive…) with state suffixes
  (`-hover`, `-active`, `-selected`, `-disabled`); a layering model (`layer-01/02/03` with matching
  fields/borders); four themes (White, Gray 10, Gray 90, Gray 100); a small set of component tokens that "should
  never be used for anything other than their own component"; Button kinds primary / secondary / tertiary /
  ghost / danger (danger has primary, tertiary and ghost sub-styles) with seven sizes, a useful comparison for
  "destructive is an intent of Button, not a new component".
- **Use for:** component architecture and anatomy, reuse, accessibility documentation, state naming, enterprise
  patterns, documentation structure, design/code alignment, lifecycle and contribution ideas.
- **When not to use:** as the user's conventions; do not import Carbon names, scales or themes into another
  product because Carbon has them.
- **Licensing/access:** Apache-2.0 code, public docs; paraphrase, do not bulk-copy.
- **Runtime:** conditional, only when a mature comparative pattern genuinely helps a component decision.

### Fluent 2 design tokens (Tier 2 exemplar)
- **Identity:** https://fluent2.microsoft.design/design-tokens, Microsoft Fluent 2.
- **Verified exemplar facts:** two-layer model, *global tokens* (context-agnostic raw values: colour, type, radius,
  stroke, motion) and *alias tokens* (semantic meaning; one alias can bundle several values for complex styles
  such as shadows and type); tokens support OS-level light, dark and high-contrast modes plus brand; stated goal
  of a common language across platforms and disciplines.
- **Use for:** layered token reasoning, theme-aware aliases, light/dark/high-contrast, cross-platform
  consistency.
- **When not to use:** copying Fluent naming (e.g., its camel-cased alias names) into a system that uses another
  convention.
- **Licensing/access:** public docs; code under MIT; paraphrase only.
- **Runtime:** conditional, layered-token comparison only.

### Material Design 3 (Tier 2 exemplar, conditional)
- **Identity:** https://m3.material.io/, Google. The site renders only with JavaScript, so at construction time
  its token page could not be read directly; the token model was verified on the official Material Web theming
  docs (material-web.dev): *reference tokens* hold concrete values (`md-ref`), *system tokens* define roles and
  decisions (`md-sys`, e.g., `--md-sys-color-primary`), *component tokens* are attributes assigned to component
  elements that can point to system tokens or concrete values.
- **Use for:** three-layer token examples, component/state models (state layers), theming concepts, when the
  product is already Material-based or the comparison is genuinely useful.
- **When not to use:** do not turn unrelated products into Material products; do not import Material colour
  roles or shape scales by default.
- **Licensing/access:** public docs (CC BY 4.0 text / Apache-2.0 code); paraphrase only.
- **Runtime:** conditional and rare.

### Storybook, accessibility testing (Tier 2 tooling)
- **Identity:** https://storybook.js.org/docs/writing-tests/accessibility-testing
- **Verified facts (re-checked 2026-10-20 against the docs source in the official storybookjs repository):** the
  a11y addon is built on axe-core; Storybook itself states it catches "up to 57% of WCAG issues"; results are
  reported as Violations / Passes / Incomplete (Incomplete = confirm manually); checks run in the addon panel, via
  the Vitest addon or the test-runner, and in CI; `parameters.a11y.test` is `'off' | 'todo' | 'error'` (only
  `'error'` fails CI); default ruleset WCAG 2.0/2.1 A+AA plus best practices, with WCAG 2.2 and AAA rules opt-in
  via axe `runOnly`; rules can be configured per project, file or story. No Storybook version is relied on.
- **Use for:** engineering-side component documentation (stories per variant/state), interaction tests,
  automated accessibility checks, visual-regression concepts, documentation parity.
- **When not to use:** as evidence of complete accessibility; automated checks are one layer.
- **Licensing/access:** public docs, MIT.
- **Runtime:** conditional, when component engineering, testing or stories are in scope and the team uses it.

### Figma, Variables in Dev Mode (Tier 3 tool bridge)
- **Identity:** https://help.figma.com/hc/en-us/articles/27882809912471-Variables-in-Dev-Mode
- **Verified facts:** variables appear in the Inspect panel and in code snippets; a variable-details view shows
  name, source file, collection, mode, value, scope and a code snippet; modes can be switched to see each value;
  alias chains can be followed back to the raw value (semantic alias → primitive → hex); an "Open variables
  table" read-only view exists when nothing is selected; suggested variables for a raw value require an exact
  value match and an appropriate scope; some values are converted for CSS output (e.g., font-weight strings) and
  variable names are normalized to valid CSS names in code (re-checked 2026-10-20).
- **Use for:** variable inspection, modes, alias-chain inspection, token visibility for developers.
- **When not to use:** teams not on Figma or not using variables; never require variables where styles are the
  team's convention.
- **Licensing/access:** public help article; feature availability depends on plan/seat (not stated in the
  article, treat as unknown per team).
- **Runtime:** conditional, design-system parity or variable-inspection tasks only.

### Figma, Code Connect (Tier 3 tool bridge)
- **Identity:** https://help.figma.com/hc/en-us/articles/23920389749655-Code-Connect
- **Verified facts (re-checked 2026-10-20 against the official article):** connects code components to Figma
  components so Dev Mode (and Figma's MCP server) shows real design-system code instead of autogenerated
  snippets; two setup paths that can be combined, Code Connect UI in Figma (GitHub repository link or manual
  component paths; Inspect shows file/component name and AI-generated previews, not snippets; one design
  component can map to several frameworks; per-mapping custom instructions) and the CLI (template files map Figma
  properties to the production component API and publish connections, so Dev Mode shows snippets; CLI-created
  connections appear in the UI but are edited only through the CLI); framework-specific parsers are no longer
  actively maintained in favour of template files; the UI's GitHub connection does not support GitHub Enterprise
  Server. Access is plan- and seat-gated; exact eligibility and limits can change and should not be stored as
  durable skill knowledge.
- **Durability rule:** when exact Code Connect availability matters, verify the current official Figma article;
  in runtime advice say "plan/seat-gated, verify the team's current eligibility".
- **Use for:** mapping Figma components/properties to code components/props, surfacing accurate examples,
  detecting naming and property mismatches.
- **When not to use:** do not assume a team uses it; never require it; a maintained mapping table in docs is a
  valid substitute.
- **Licensing/access:** public help article; plan-gated feature.
- **Runtime:** conditional, design-system parity tasks only (feature handoff belongs to
  `delivery-product-collaboration`).

### *Designing Interfaces*, 3rd edition, Tidwell, Brewer, Valencia (O'Reilly, 2020) (Tier 2, construction-time)
- **Identity:** ISBN 978-1-492-05196-1. Relevant material: Chapter 11 "User Interface Systems and Atomic Design"
  (UI systems as styles-and-standards systems that keep look-and-feel consistent while remaining
  implementation-agnostic; atomic design summarized as break-it-down, style guide, consistency to avoid "UX debt",
  modularity, nesting/inheritance of styles, build-it-up, not tied to technology; atoms → molecules → organisms →
  templates → pages; UI frameworks as "a floor, not a ceiling"; "design the system, not one-off screens");
  Chapter 4 pattern *Visual Framework* (shared layout/colour/type/spacing conventions across all screens, defined
  in one place and separated from content, so what is constant recedes and what changes is noticed); Chapter 1
  behaviours such as *Habituation* (consistent placement and behaviour lets users act without re-learning).
- **Use for:** conceptual grounding of reuse, consistency, modularity, inheritance and system thinking.
- **When not to use:** its framework survey (Bootstrap, Foundation, Semantic UI, Materialize, Blueprint, UIkit,
  Fluent circa 2019) is historical; current official documentation outranks it for any tool or system detail.
- **Conflict rule:** conceptual only; never cited against Tier 0 or Tier 1.
- **Licensing/access:** copyrighted. Do not reproduce passages. Works without the original books; links are for optional verification.
- **Runtime:** not needed; ideas are already synthesized into the reference files.
