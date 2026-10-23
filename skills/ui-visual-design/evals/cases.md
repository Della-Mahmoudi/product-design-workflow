# Evaluation Cases: ui-visual-design

There are eight cases. A–C test core visual work; D–H test the boundaries with sibling skills and proportionality. Each one gives the user prompt, whether this skill should trigger, the primary owner, any context the run needs, the expected behavior and routing, the pass and failure criteria, and checks for unnecessary work. `evals/evals.json` holds the same eight cases in the skill-creator eval format.

Grade both the answer and the transcript: which reference files were read, and which external sources were fetched. A run passes only if it meets every pass criterion and hits none of the failure criteria. For cases marked **NO**, the router should choose the primary owner; when this skill is invoked anyway, grade the routing behavior the case describes.

## Case A: Existing enterprise design system

**User prompt**
> Redesign this dense B2B analytics dashboard to feel cleaner and more modern. We already have an established component library, typography scale, color tokens, and spacing tokens.

**Should this skill trigger?** YES

**Primary owner:** `ui-visual-design`

**Context for the run.** Attach a dashboard screenshot or Figma frame, plus the design system or a list of its tokens and components. If none is attached, the run should first ask for it, or inspect it if it's reachable through connected tools, before prescribing any values.

**Expected behavior**
- Reads "cleaner and more modern" as clarity: stronger hierarchy, fewer containers, less chrome, calmer color and a better scan path. It doesn't read it as a new aesthetic.
- Inventories the design system first, and maps every recommendation to existing components, type styles, and color and spacing tokens.
- Diagnoses hierarchy by comparing perceived and intended order, then grouping, scan path and density. Leads with the metrics that drive decisions.
- Uses the design system's density options for tables and tiles, and keeps target sizes, minimum text sizes and contrast intact.
- Flags only genuine `[DS GAP]` items. Leaves navigation and IA unchanged, and raises any structural issue as a `[DEPENDENCY]`.
- Works in Standard mode, or Deep mode only if a full spec is requested.

**Expected routing**
- SKILL.md → `references/hierarchy-layout-and-density.md` (required).
- `references/typography-color-and-visual-language.md` only if type or color changes are proposed.
- No platform browsing.
- Carbon or Fluent are optional, and only as density benchmarks.

**Pass criteria**
1. Asks for or inspects the existing design system before giving values, and labels any assumption.
2. Every spacing, type and color recommendation names an existing token, style or component, or a clearly marked placeholder for the right token role.
3. Hierarchy and density changes are concrete and tied to the dashboard's tasks: which tiles lead, how rows are grouped, which containers go.
4. De-emphasized text keeps its contrast, and status is never conveyed by color alone.
5. Design-system gaps are listed separately and described as needs, not designed.
6. Navigation and IA are untouched, or any issues with them are flagged as dependencies.

**Failure criteria**
- Invents raw spacing values, font sizes or colors where tokens exist.
- Proposes a new type scale, palette or visual language, or replaces the design system.
- Copies Carbon, Material or Fluent styling.
- Redesigns navigation or IA without evidence.
- Writes token governance, naming conventions or component APIs.

**Unnecessary-work checks**
- Doesn't read `responsive-accessibility-and-platform.md` unless responsiveness or a specific WCAG question is in scope.
- Doesn't browse the web.
- Doesn't produce multiple visual directions, a dark-mode spec or a multi-platform spec unless asked.

## Case B: Responsive content stress

**User prompt**
> Create the visual specification for a responsive account/settings screen that must work from compact mobile widths to large desktop, support long translated strings, RTL, dark mode, validation messages, and 200% text zoom.

**Should this skill trigger?** YES

**Primary owner:** `ui-visual-design`

**Expected behavior**
- Works in Deep mode, covering hierarchy, layout per width range, typography, color and states, component mapping, content stress, themes, accessibility, and assumptions.
- Uses the product's breakpoints and tokens if they're supplied. Otherwise it proposes only the values needed, each marked `[PROVISIONAL]` with a content-driven reason.
- Recomposes for compact widths: a single column in priority order, with labels above fields.
- On wide screens, uses extra width only for panes the approved structure already provides, such as an existing list of settings sections. Otherwise flags `[DEPENDENCY: IA]` rather than inventing navigation. Doesn't stretch forms.
- Specifies how translated text behaves: flexible widths, wrapping, no fixed English-sized buttons or tabs, and stacked buttons where needed.
- Specifies RTL using start and end, mirroring the layout and directional icons but not digits, logos or checkmarks.
- Handles dark mode with theme tokens rather than inversion, checking surface hierarchy and contrast in every state.
- Presents validation as text, an icon and color at the field, with a summary when there are several errors, and reserves space so messages don't overlap. When validation fires is flagged as an interaction decision.
- Covers 200% text, reflow at 320 CSS px, target sizes and focus visibility.
- Phrases accessibility as "designed to address SC …".

**Expected routing**
- SKILL.md → `references/responsive-accessibility-and-platform.md` (required).
- `references/hierarchy-layout-and-density.md` for forms, settings and states.
- `references/typography-color-and-visual-language.md` for themes and states.
- In §10 of the responsive reference, only the web block, unless the prompt names other platforms.

**Pass criteria**
1. Defines a layout transformation for each width range, with content priority, rather than scaling one layout.
2. Specifies behavior concretely for long strings, RTL, dark mode and 200% text.
3. Validation presentation meets SC 3.3.1 and 1.4.1 and keeps the layout stable.
4. Marks invented values `[PROVISIONAL]` and uses supplied tokens wherever they exist.
5. Makes no conformance claim.

**Failure criteria**
- Designs desktop only, or makes mobile a shrunk desktop.
- Sizes fixed-width containers to English text.
- Describes dark mode as inverted colors.
- Claims "WCAG compliant".
- Invents validation timing or a new settings IA instead of flagging them.

**Unnecessary-work checks**
- Doesn't apply or browse Apple or Material guidance, or read their §10 blocks, unless the prompt names those platforms.
- Doesn't produce design-system documentation, a token architecture or multiple directions.

## Case C: Native Apple visual context

**User prompt**
> Refine the high-fidelity UI of this native iOS feature. Interaction behavior is already approved. Focus only on visual presentation and platform fit.

**Should this skill trigger?** YES

**Primary owner:** `ui-visual-design`

**Context for the run.** Attach the screens as screenshots or Figma frames. If they're missing, the run should ask for them, not invent a feature.

**Expected behavior**
- Puts the product's brand and design system first, and applies the Apple HIG selectively from the platform block. Fetches a single HIG page only if a needed detail is missing.
- Covers:
  - hierarchy;
  - typography: text styles, Dynamic Type, weights;
  - spacing: margins and safe areas;
  - color: semantic colors, a restrained accent, and Liquid Glass only in the functional layer;
  - Dark Mode and Increase Contrast;
  - 44 pt hit regions;
  - SF Symbols weight-matched to text.
- Preserves the approved flows and behavior. Any behavioral issue it notices is flagged, not changed.
- Works in Standard mode.

**Expected routing**
- SKILL.md → `references/responsive-accessibility-and-platform.md`: the Apple block, targets and Dynamic Type.
- `references/typography-color-and-visual-language.md` as needed.
- `references/hierarchy-layout-and-density.md` only for layout critique.
- Reads only the Apple block in §10. Never applies or browses Material, Carbon or Fluent guidance.

**Pass criteria**
1. Recommendations follow iOS conventions and the product's design system, with no Material patterns.
2. No interaction-flow changes.
3. Text uses text styles that scale, avoids light weights at small sizes, and the layouts hold up at large Dynamic Type sizes.
4. Liquid Glass isn't added to content-layer elements such as cards, backgrounds or lists.
5. Contrast is checked in both light and dark appearances, and hit regions are checked against 44 pt.

**Failure criteria**
- Brings Material patterns into the iOS feature, such as a floating action button, Material elevation or state layers, or Roboto.
- Alters the behavioral flow.
- Creates a new token architecture or rebuilds the design system.
- Does IA, research or unrelated UX work.

**Unnecessary-work checks**
- Doesn't browse Material or the exemplar systems.
- Doesn't dump the full WCAG table.
- Doesn't produce rules for other platforms.

## Case D: Visual states for approved validation behavior

**User prompt**
> Our checkout form already has approved validation behavior. Design the visual presentation for default, focus, error, disabled, loading and success states.

**Should this skill trigger?** YES

**Primary owner:** `ui-visual-design`

**Context for the run.** Attach the checkout form, the approved interaction spec, and the design system's form and button components and tokens if they exist. If they're missing, the run asks for them once or proceeds with token roles and `[PROVISIONAL]` values labeled as assumptions. Either way it treats the validation behavior as fixed.

**Expected behavior**
- Works in Standard mode, starting from the state-differentiation guidance in the typography-color reference.
- Treats the approved validation behavior as given and styles exactly the states it names.
- Maps each state to existing components, variants and tokens written as `token (value)`, or to token roles and `[PROVISIONAL]` values when no system is supplied.
- Makes every state distinguishable without color alone: error and success pair text and an icon with color; focus has a visible indicator distinct from hover, selected and error; disabled is dimmed but still recognizable; loading shows an in-place indicator and keeps the control's dimensions.
- Checks text contrast (4.5:1) and non-text contrast (3:1) for field boundaries, focus indicators and status icons in every state, and reserves space so messages don't shift the layout.
- Flags anything the visuals need but the spec doesn't define, such as an error summary or a loading state on submit, as `[DEPENDENCY: Interaction]`.
- Phrases accessibility as "designed to address SC …".

**Expected routing**
- SKILL.md → `references/typography-color-and-visual-language.md` (§9 state differentiation, §3 contrast).
- `references/hierarchy-layout-and-density.md` (Forms in §10, and §11) only if form layout or message placement is in play.
- `references/responsive-accessibility-and-platform.md` only for a specific WCAG detail. No platform blocks and no browsing.

**Pass criteria**
1. All six requested states have distinct visual treatments.
2. No state is conveyed by color alone; error and success include text and an icon.
3. The focus indicator is specified as visible, at least 3:1 against adjacent colors, and distinct from error and hover.
4. Values come from supplied tokens and components, or are token roles and `[PROVISIONAL]` values when none are supplied.
5. Validation timing, retry and recovery behavior stay exactly as supplied; gaps are flagged as `[DEPENDENCY: Interaction]`.
6. No conformance claim.

**Failure criteria**
- Decides or changes when validation fires (as the user types, on blur, on submit).
- Changes retry behavior or invents error-recovery logic, such as auto-retry or clearing fields.
- Defines where focus moves after an error.
- Creates component APIs, properties, variants or token architecture.
- Signals error or success with color alone.
- Calls the design "WCAG compliant".

**Unnecessary-work checks**
- No responsive, dark-mode or RTL spec unless asked.
- No platform blocks from §10 and no browsing.
- No design-system audit beyond the form and button pieces the states use.

## Case E: Interaction behavior request

**User prompt**
> Define when validation should fire, what happens after a failed submission, how retry works, and where focus goes after the error.

**Should this skill trigger?** NO

**Primary owner:** `interaction-design`

**Expected behavior**
- The router picks `interaction-design`, not this skill.
- If this skill is invoked anyway, it says in a line or two that all four asks are behavior and state logic, routes them to `interaction-design`, and stops.
- It may offer, as a clearly conditional follow-up, to style the resulting states once the behavior is decided. It doesn't style them now.

**Pass criteria**
1. Names all four asks (validation timing, failed-submission handling, retry, focus movement) as behavior.
2. Routes to `interaction-design`.
3. Any visual content is brief, optional and conditional on behavior decided elsewhere.

**Failure criteria**
- Specifies validation timing, failure handling, retry rules or a focus destination.
- Recasts the behavioral decisions as styling, e.g. "make the error red and users will retry".
- Produces a visual state spec nobody asked for.

**Unnecessary-work checks**
- Reads no reference file.
- Doesn't fetch WCAG or platform guidance.

## Case F: Design-system architecture request

**User prompt**
> We need compact, destructive, icon-only and loading versions of Button. Define the reusable component properties, variants and token architecture.

**Should this skill trigger?** NO

**Primary owner:** `design-systems-consistency`

**Expected behavior**
- The router picks `design-systems-consistency`.
- If this skill is invoked anyway, it identifies the request as reusable component API, variant and token architecture and routes it.
- If useful, it lists the visual requirements those versions must meet, framed as inputs for `design-systems-consistency`: a destructive action is never styled as the primary one; icon-only and compact sizes keep the platform or WCAG target size; loading keeps the button's dimensions; every version keeps text and non-text contrast. An icon-only button also needs an accessible name, which is an engineering dependency.

**Pass criteria**
1. Routes to `design-systems-consistency`.
2. Defines no property names or types, variant matrix, boolean props, token names or token tiers.
3. Any visual requirements are framed as constraints, not API decisions.

**Failure criteria**
- Proposes properties such as `size="compact"`, `iconOnly: boolean` or `loading: boolean`, a variant matrix, or tokens such as `button.danger.bg`.
- Decides between reuse, compose, extend and create.
- Writes governance, naming or versioning rules.

**Unnecessary-work checks**
- No design-system audit.
- No browsing, and no reference reads beyond what a short list of visual requirements needs, ideally none.

## Case G: Implementation QA request

**User prompt**
> The developer implementation looks slightly different from Figma. Compare staging against the approved UI and tell me what should block release.

**Should this skill trigger?** NO

**Primary owner:** `delivery-product-collaboration`

**Expected behavior**
- The router picks `delivery-product-collaboration`.
- If this skill is invoked anyway, it identifies the build-versus-design comparison and the release-blocking judgment as `delivery-product-collaboration` work and routes them.
- It may offer the approved visual intent (hierarchy, token use, states, responsive rules) as an input to that QA. It doesn't run the comparison.

**Pass criteria**
1. Routes to `delivery-product-collaboration`.
2. Produces no defect list, severity ratings or release decision.
3. Any contribution is limited to stating the approved visual intent.

**Failure criteria**
- Compares staging with Figma and lists defects.
- Labels anything BLOCKER, MAJOR, MINOR or POLISH, or decides what blocks release.
- Declares the build accessible, inaccessible or "WCAG compliant".

**Unnecessary-work checks**
- Doesn't ask for staging access or screenshots in order to do the QA itself.
- Reads no reference file and doesn't browse.

## Case H: Simple visual critique

**User prompt**
> This pricing card feels too heavy and hard to scan. What's wrong with the visual hierarchy?

**Should this skill trigger?** YES

**Primary owner:** `ui-visual-design`

**Context for the run.** Attach a screenshot or frame of the card. If none is attached, the run asks for it in one short message. It may name up to three common causes as hypotheses, but it doesn't invent a card to critique.

**Expected behavior**
- Works in Quick mode: a verdict, at most three issues, each with its minimal fix, and an accessibility note only if a critical issue is visible.
- Diagnoses hierarchy and grouping: what competes for the first read (plan name, price, badge, call to action), uniform weights, stacked containers, feature-list density.
- Fixes with the cheapest levers first (remove or demote, spacing and grouping, size and weight), naming token or style roles rather than inventing raw values when the design system is unknown.

**Expected routing**
- SKILL.md, plus `references/hierarchy-layout-and-density.md` at most.

**Pass criteria**
1. Follows the Quick shape: a verdict and no more than three issues, each with a fix.
2. Issues concern hierarchy, grouping or emphasis that can be seen on the card.
3. Fixes use token or style roles, or label any value as an assumption.
4. Mentions accessibility only for a critical visible issue, with a confidence level.

**Failure criteria**
- Runs a design-system inventory or audit, or outputs token tables or a full specification.
- Adds dark mode, breakpoints, RTL or platform rules.
- Browses or cites Apple, Material, Carbon or Fluent.
- Changes the plans, their order or the pricing flow instead of flagging such an issue as a dependency.
- Lists more than three issues or writes a multi-section report.

**Unnecessary-work checks**
- Reads no more than the hierarchy reference; never the responsive reference or the source map.
- No browsing.
