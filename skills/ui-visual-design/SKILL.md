---
name: ui-visual-design
description: Designs, critiques and specifies the visual layer of UI: hierarchy, composition, layout and grid, spacing and density, typography, color and contrast, surfaces, icons and imagery, visual states, responsive presentation, dark and high-contrast themes, RTL and localization, and visual accessibility, applying the existing design system and approved UX. Use when a screen, dashboard, table or form should look cleaner, clearer or more on-brand, when a UI feels busy or hard to scan, for high-fidelity visual specs or critique, or when a layout must hold up across breakpoints, dark mode, RTL or 200% zoom. Not for research, IA or flows, interaction logic, design-system architecture, handoff or build QA, code or usability testing.
---

# UI & Visual Design

Turn approved structure, behavior and real content into a visual layer that is perceptually clear, accessible, responsive and coherent with the product, brand and platform. Clarity comes first and polish second. Decoration never substitutes for hierarchy, and visuals never hide a structural problem.

The skill works standalone. If upstream artifacts such as research, IA, flows or an interaction spec are missing, work from what is supplied, label assumptions, and don't redo upstream work.

## Triggers

- **Use for:** visual critique ("does this hierarchy work?", "why does this feel busy?"), making a screen cleaner or more modern within its system, high-fidelity visual specs, choosing type, color, spacing or density for a screen, adapting a layout across breakpoints, themes, RTL, translation or zoom, and visual accessibility checks.
- **Hand off:** discovery, research, strategy, IA, sitemap, navigation, flows, interaction logic and state machines, backend behavior, token or component architecture, governance, copywriting, code, usability testing, engineering handoff packages and acceptance criteria, and QA of a build against its design.
- **Mixed requests:** do the visual part and flag the rest as dependencies.
- **Requests wholly owned by another discipline** (when validation fires, a component's variant API, whether staging matches Figma): name the owner from *Stop when*, route it, and add visual input only if it genuinely helps. Don't recast a behavior, system or QA question as styling.

## Scope

**Owns:**
- visual hierarchy, composition and grouping
- layout, grid, spacing and density
- type and color application, contrast
- surfaces, borders, radius and elevation
- icon, imagery and illustration treatment; brand expression in UI
- visual affordance and the visual differentiation of states
- responsive presentation; theme, RTL, localization and zoom resilience
- visual accessibility; screen-level component composition
- high-fidelity visual specs and critique

**Depends on, flag with `[DEPENDENCY: <area>]`, never silently solve:**
- **IA:** navigation, sitemap, content priority and flow changes. Responsive recomposition stays visual: stacking, wrapping, resizing, redistributing approved content, changing spacing or density, or using an approved adaptive pattern. A new navigation model, dropped functionality, changed destinations, a changed task flow or priorities re-ranked without evidence is IA, even when a breakpoint prompts it.
- **Interaction:** decides what happens: state machines and state logic, transitions, system response, loading, retry, validation timing, cancellation, undo, focus movement and keyboard behavior, permissions, error recovery and motion. This skill decides how approved states look and stay distinguishable. Style the states that already exist in the interaction spec, product behavior, platform convention or an existing component contract. If a needed state is missing, flag it; being able to draw a state never licenses inventing its logic. Example: `interaction-design` says the submit goes pending, blocks duplicate submits, keeps entered data on failure and offers retry; this skill makes default, pending, disabled, error and success distinct while hierarchy and accessibility hold.
- **Design Systems & Consistency:** defines and maintains the system: token architecture, naming and tiers, component APIs and reusable properties, variant strategy, library governance, contribution, deprecation, versioning, migration, Figma/code parity and DS documentation. This skill consumes the system (next section).
- **Delivery & Product Collaboration:** Ready-for-Dev, handoff completeness, acceptance criteria, engineering questions, and checking a build, including its accessibility, against the design and judging defect severity. This skill states design intent ("at compact widths, metadata stacks below the title"); `delivery-product-collaboration` checks whether the build did it. Visual specs aren't handoff packages.
- **Other owners:** discovery, strategy, research, content and copy, backend behavior, analytics, testing and code.

**Escalation test:** if a fix adds or removes content or functionality, changes the approved priority, swaps a control type, or changes where something leads or how the task flows, it isn't a visual fix, at any breakpoint. Flag it rather than decorating over it.

## Design system: consume, don't systemize

1. When prescribing values (Standard and Deep modes), first inspect the parts of the system the decision touches: components, variants, tokens and variables, type and color styles, the icon set and breakpoints. Look in supplied files or in connected design tools. A visual question isn't a library audit. In Quick mode, skip the inventory: name roles such as "secondary text style" and label any token mapping as an assumption.
2. Reuse valid primitives. Prefer an existing component or variant to a visually redundant new one.
3. Write every value as `token (resolved value)`, e.g. `space-5 (16px)`. Raw values fork the system and break theming, so never bypass a valid token without saying why.
4. Choosing and composing existing components, variants and tokens on a screen is this skill's job. When they can't express an approved need, record a `[DS GAP]` that states:
   - the need;
   - its context: where it occurs;
   - whether it recurs, if known;
   - a temporary visual workaround, only if the screen needs one now.

   Then stop. Whether the system should reuse, compose, extend or create, and the naming, API and documentation that follow, are `design-systems-consistency`'s decisions. For example, "use the secondary Button variant here" and "set this caption in `text.secondary`" belong here; "add a `quiet` hierarchy property to Button" and "create a new semantic token tier" belong to `design-systems-consistency`.
5. Keep `[LOCAL EXCEPTION]` (justified for this screen only) separate from candidate system additions.
6. If there is no design system at all, propose only the values this interface needs, each marked `[PROVISIONAL]`. Never present them as established product tokens, and don't build a system.

## Source hierarchy

- **Mandatory constraints:** the accessibility target, legal obligations, brand restrictions, and platform requirements the OS or app store enforces (such as reserved screen areas). An existing screen that violates them is a conflict to flag, not a precedent.
- **Tier 0, product truth:** the design system, brand, real content, approved UX and interaction, supported platforms and viewports, research, and the accessibility target. Consistency with valid product patterns beats generic patterns.
- **Tier 1, normative and platform:** WCAG 2.2; Apple HIG only for Apple platforms; Material 3 only for Android or Material-based products. Platform recommendations such as hit-region sizes are followed unless the product has a documented reason. Never load both platform guides by default, because mixing platform languages produces incoherent UI.
- **Tier 2, canonical reference:** principles from *Designing Interfaces* and *The Elements of User Experience*, already distilled into the references. IBM Carbon and Microsoft Fluent 2 serve as enterprise exemplars, never as the product's visual language.
- **Tier 3, sanity check:** *Don't Make Me Think*, for scanability and obviousness.

**On conflict:**
1. Name the exact decision and its context.
2. Apply mandatory constraints.
3. Check product truth.
4. Apply the most applicable authority.
5. Prefer valid existing patterns.
6. Record what stays unresolved.

Never blend Material, Apple, Carbon and Fluent into one UI. The full algorithm and per-source limits are in `references/source-map.md`.

## Load only what the task needs

| Task signal | Read | External source only if |
|---|---|---|
| Hierarchy, layout, grid, spacing, density, grouping; tables, lists, forms, dashboards, cards; empty, loading and error presentation | `references/hierarchy-layout-and-density.md` | never needed |
| Typography, color, contrast, brand, surfaces, borders, radius, elevation, icons, imagery, affordance, visual states, theme treatment and theme checks | `references/typography-color-and-visual-language.md` | an exact WCAG criterion is disputed |
| Breakpoints, adaptive layout, zoom and reflow, targets, content stress, localization, RTL, platform contrast settings, WCAG visual criteria, platform fit | `references/responsive-accessibility-and-platform.md` §1–9, plus only the matching platform block in §10 | the decision needs a platform value that isn't in the block |
| Which source wins, source limits, citations | `references/source-map.md` | never needed |

- A quick critique usually needs one reference or none.
- Section 10 of the responsive reference holds one block each for web, Apple, Android/Material and enterprise exemplars. Find the block you need by its heading and read only that one. If the whole file gets read, apply only the matching block.
- For enterprise or data-dense UI where the design system has no answer, benchmark against Carbon or Fluent, one of them, never both unless a comparison is the point. Never copy their styling.
- Works without the original books; links are for optional verification.
- Browse only to fetch one specific missing or disputed fact. If a source can't be reached, say so; don't reconstruct its content from memory.

## Workflow (internal; show only what the answer needs)

1. Frame the visual decision and choose an output mode.
2. Establish the platform, viewports, accessibility target, and which inputs exist: structure, interaction spec, real content, design system, brand. Ask once for essentials that would change the answer. Otherwise proceed and label assumptions.
3. Inventory the design system when prescribing values (see above).
4. Settle hierarchy first. Rank what matters, compare it with what actually reads first, and fix with the cheapest lever, in this order: remove or demote competitors, then position, spacing, size and weight, color, and finally surface.
5. Then layout, spacing, alignment and density; then type and color; then affordance and states.
6. Cover responsive behavior, content stress and themes, but only those in scope.
7. Check the applicable accessibility criteria now. Don't defer visual accessibility to a later audit stage.
8. Keep assumptions, `[DS GAP]` and `[DEPENDENCY]` items apart from recommendations.
9. Return the smallest output that resolves the decision, then stop.

## Output modes

- **Quick** (one question or a small critique): a verdict, up to 3 key issues each with its minimal fix, and a critical accessibility issue only if one exists. No inventory, specs, token tables or multi-platform rules.
- **Standard** (one screen or feature): only the sections that matter, chosen from hierarchy, layout and spacing, typography, color and states, component mapping, responsive behavior, accessibility, and assumptions and gaps.
- **Deep** (major high-fidelity or multi-screen work; a full specification; several resilience conditions at once, such as breakpoints, translation, RTL, themes and zoom; or on request): may add a visual-direction rationale, layout-system usage, content-stress results, theme rules, platform specifics, product-specific exceptions and missing primitives.

**Conventions in every mode:**
- Label claims Observed (seen in supplied material), Inferred or Recommended when the difference matters.
- Give a confidence level when evidence is partial, e.g. contrast estimated from a compressed screenshot.
- Write values as `token (value)`. Mark invented values `[PROVISIONAL]`.
- For accessibility, write "designed to address WCAG 2.2 SC …". Never call a static design "WCAG compliant".
- Offer one visual direction unless more are requested or a real fork needs a decision.

**Quick-mode shape** (token names illustrative):

```
Verdict: Mostly works. The KPI row competes with the page title.
1. KPI values share the title's weight → values one step down the heading styles, labels in the small label style; the title keeps the top heading style.
2. Status chips are color-only → add the DS status icon and text.
3. Every tile has a border, a fill and a shadow → keep the raised-surface fill, drop the borders, and separate tiles with spacing.
Accessibility: muted labels look ≈4.2:1 from the screenshot (Medium confidence). Verify against the tokens; 4.5:1 is required.
Assumption: style names are generic; map them to your DS when applying.
```

## Quality gates (check those relevant to the request)

**Fail: fix before calling the design done.**
- Text or required non-text contrast misses the applicable threshold.
- Color is the only carrier of meaning or state, or states are indistinguishable.
- Focus can't be seen.
- Text breaks with realistic, translated or enlarged content, or RTL, dark mode or zoom breaks the composition, when those are in scope.
- Visual changes are being used to hide a structural UX problem.

**Flag: raise with the reason and a fix.**
- Hierarchy depends mainly on color, or everything has equal emphasis.
- The primary action lacks priority, or several actions compete for it.
- Spacing doesn't express grouping, or the layout is flat or fragmented into boxes.
- Arbitrary values bypass valid tokens, or a new component duplicates an adequate existing one.
- Type has no coherent hierarchy.
- When responsive behavior is in scope: no responsive decisions, or mobile is a scaled-down desktop.
- Empty, loading or error states collapse the layout or lose meaning.
- Decoration harms clarity, or another design system's aesthetics are copied without reason.

## Stop when

- The requested decision is resolved at the requested fidelity.
- What remains belongs to another discipline: list it as `[DEPENDENCY: <area>]`, name its owner below and stop. Touching another discipline is no reason to continue into it.
- Essential input is missing, e.g. there's no screen to critique. Ask for it instead of inventing a design to judge.

| What remains | Route to |
|---|---|
| Structural hierarchy (content priority), navigation, sitemap or flow | `ux-architecture` |
| Behavior and state logic: validation timing, retry, recovery, focus movement | `interaction-design` |
| Reusable component, variant or token architecture; DS governance | `design-systems-consistency` |
| Prototyping, usability testing, measurement | `prototype-testing-analytics` |
| Ready-for-Dev, handoff, implementation QA | `delivery-product-collaboration` |

Don't add directions, platforms, themes, breakpoints or audits nobody asked for.
