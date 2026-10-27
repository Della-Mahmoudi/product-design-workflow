# Token architecture, executable guidance

Load for: creating or reshaping a token architecture, auditing raw values, renaming tokens, mapping
light/dark/high-contrast modes, deduplication, token migration, or producing a DTCG-oriented token file.
Do not load for a simple component-reuse question.

Contents: 1 Layers · 2 Naming · 3 Aliasing · 4 Themes and modes · 5 Type selection · 6 Audit procedure ·
7 Deduplication and semantic distinction · 8 Hard-coded values · 9 Migration · 10 DTCG-oriented serialization ·
11 Warnings · 12 Output shapes

## 1. Layers (conceptual, independent of any tool's vocabulary)

| Layer | Purpose | Names describe | Mode-dependent? | Examples (illustrative only) |
|---|---|---|---|---|
| Primitive / global / reference | The palette of raw values the system is allowed to use | the value (`blue.600`, `space.400`, `radius.200`, `font.size.300`) | normally no | `blue.600 = #2457F5` |
| Semantic / alias / system | The *role* a value plays in the UI; the theme switch lives here | the role (`color.text.primary`, `color.surface.default`, `color.action.primary.background`, `color.border.subtle`, `space.inset.md`) | yes, one value per mode | `color.action.primary.background → {color.blue.600}` |
| Component (only when justified) | A component-level theming or API seam | component + part + property (+ state) (`button.primary.background.hover`) | inherits from semantic | `button.primary.background → {color.action.primary.background}` |

Exemplar vocabularies map onto the same three ideas: Fluent 2 *global → alias*; Material 3 *reference → system →
component*; Carbon *palette → core tokens (+ a few component tokens)*. Keep the product's own names.

Rules:
- Components and screens consume **semantic** tokens. They never consume primitives directly except for
  documented exceptions (section 8).
- Create a **component token** only when (a) the component must be themed independently of the semantic layer,
  (b) a code API exposes it as a customization seam, or (c) several parts of one component need a stable shared
  value that no semantic role expresses. Not for every CSS property, not for one-off overrides.
- A semantic token must have a role statement that a designer and an engineer would both apply the same way:
  "default text on surfaces", "background of the single most important action", "1px separators inside
  content". If the role cannot be stated without naming a component or a screen, it is probably a component
  token or not a token at all.

## 2. Naming principles

- Structure names by **category → role → variant → state**, consistently: `color.text.primary`,
  `color.action.primary.background.hover`, `color.feedback.danger.text`. Pick one delimiter and casing per
  platform and keep the *segments* identical across Figma, tokens file and code (`color/text/primary` in Figma,
  `color.text.primary` in the file, `--color-text-primary` in CSS is one token).
- Semantic names say what a thing is *for*, never what it looks like or where it is implemented. Reject
  `color.red`, `blue-button-bg`, `gray-light-2`, `headerBlue`, `textColorForBannerV2` at the semantic layer.
- Primitive names may describe the value (`gray.100`, `space.400`), but keep scales ordinal and stable; do not
  encode the current hex in the name.
- State is a trailing segment with a fixed vocabulary (`default` implied, `hover`, `pressed`/`active`,
  `focus`, `selected`, `disabled`). Use the product's existing vocabulary if it has one; never two spellings.
- Intent vocabulary is shared with components: the same word (`primary`, `secondary`, `danger`/`destructive`,
  `success`, `warning`, `info`) must mean the same thing in tokens and in component properties.
- Avoid numbers that imply order where there is none (`text.1`, `text.2`); prefer `primary / secondary /
  tertiary / disabled / inverse / on-brand`.
- Do not bake platform units or implementation details into semantic names (`space.16px`, `shadowDp4`).
- DTCG 2025.10 governs the token *file* format (types, aliases, `$deprecated`, serialization); it prescribes no
  semantic naming scheme or role vocabulary. Names, roles, theme strategy and governance come from Tier 0.

## 3. Aliasing

- Direction is always downward: component → semantic → primitive. Never alias a primitive to a semantic token,
  never alias sideways between semantic roles unless one is explicitly defined as "same as X by policy".
- Keep alias depth short (typically ≤ 3 hops). Every hop must add meaning (role, theme, component seam). An alias
  that only renames another token with the same meaning is noise, remove it or make it a documented
  deprecation alias (section 9).
- Each semantic token resolves to a value in *every* mode; a missing mode value is a defect.
- When two roles intentionally share a primitive, keep two semantic tokens (section 7). When one role has two
  names, you have a duplicate.
- In Figma, model aliases as variable aliases across collections (primitives collection → semantic collection
  with modes → optional component collection). In code, alias at build time or via CSS custom properties; verify
  the pipeline actually preserves the chain instead of flattening it into disconnected literals.

## 4. Themes and modes

- Modes (light, dark, high-contrast, brand A/B, density compact/comfortable) change **values of semantic
  tokens**, not token names. Components never branch on the mode; they consume the role.
- Primitives are usually mode-independent. If dark mode needs different primitives (lifted surfaces, desaturated
  brand colour), add primitives, do not fork the semantic layer.
- High contrast is not "dark mode with more contrast": borders that were optional become mandatory, elevation
  via shadow disappears, focus rings and selection need their own roles. On the web also account for OS forced
  colours (`forced-colors` / system colour keywords) where the platform applies them regardless of tokens.
- Per mode, verify the pairs that must meet WCAG 2.2: text on its surface (1.4.3, 4.5:1; 3:1 for large text),
  component boundaries and state indicators against adjacent colours (1.4.11, 3:1), focus indicator visibility
  (2.4.7; 2.4.13 at AAA). Record contrast as a property of the *pair*, not of a single token.
- Do not create a mode for a single screen or campaign; that is an override, documented as an exception.
- Density/size modes belong to spacing and typography semantics (`space.inset.md`, `font.size.body`), not to
  colour, and not to component booleans like `compact=true` when a mode or size property exists.

## 5. Token type selection (DTCG 2025.10 vocabulary; use even when not emitting files)

The vocabulary is synthesized below; consult the DTCG spec itself only when emitting or inspecting token files.

| Need | Type | Notes |
|---|---|---|
| Colours | `color` | Value is a colour object (`colorSpace`, `components`, optional `alpha`, optional `hex`). |
| Sizes, spacing, radii, stroke widths, breakpoints | `dimension` | `{value, unit}` with `px` or `rem`. Unit required even for 0. |
| Font families, weights | `fontFamily`, `fontWeight` | Weight accepts numbers or standard keyword names. |
| Durations, easings | `duration`, `cubicBezier` | Motion tokens: use only if the product animates systematically. |
| Unitless numbers (line-height ratio, opacity, z-index, scale factors) | `number` | Do not store opacity as a colour. |
| Text styles | `typography` (composite) | Only when the system treats a text style as one decision; otherwise separate tokens. |
| Shadows / elevation | `shadow` (composite, single or layered) | Elevation levels are semantic (`elevation.raised`), the shadow values are primitives. |
| Borders, stroke styles, transitions, gradients | `border`, `strokeStyle`, `transition`, `gradient` (composite) | Use composites when the parts always travel together. |

Composite vs. separate: if designers change the parts independently (e.g., font size without weight), keep them
separate; if a style is always applied as one unit, a composite reduces drift.

## 6. Token audit procedure (raw values, drift, "convert everything to tokens" requests)

Never convert N observed values into N tokens. Run this instead:

1. **Inventory**: collect each distinct value with where it is used (component, layer, property: fill, text,
   border, icon, shadow), count of uses, and whether a token/variable was available but bypassed.
2. **Normalize**: canonical form (hex case, alpha, rem/px) so trivial spelling differences collapse.
3. **Cluster primitives**: group near-identical values (same hue family, within a perceptual step, ±1 px).
   Each cluster is a *candidate* primitive; the intended scale step is the one in the existing palette or the
   most used value, not the average.
4. **Assign roles**: for every usage, name the role it plays (body text, secondary text, divider, input border,
   primary action background, hover of that, error text…). The role list, not the value list, becomes the
   semantic layer.
5. **Classify each value** as one of: *legitimate role already tokenized* (bypass → migrate to existing token);
   *legitimate role missing a token* (add semantic token aliasing an existing or new primitive); *accidental
   drift* (off-by-one tints, legacy hexes → map to nearest intended primitive); *intentional exception*
   (illustration, chart series, third-party brand marks, marketing surfaces → document, do not tokenize into the
   core system); *unknown* (cannot determine role → list for verification, do not guess).
6. **Decide architecture**: typically far fewer primitives than observed values and a semantic set sized by
   roles, with every mode value filled in. Preserve semantically distinct roles even if values coincide today.
7. **Produce the migration map** (old value/usage → token), the exception register, and the unknowns list.
8. Emit a DTCG-oriented file only if the user asked for machine-readable output (section 10).

Report in this order: counts (observed → primitives → semantic roles → exceptions → unknowns), the mapping, the
rules that prevent recurrence (lint: no raw colour outside the primitives file; Figma: styles/variables only).
Report counts only after classification; do not forecast how many primitives or roles "will" result before the
inventory exists, a guessed number anchors the audit and is indistinguishable from evidence to the reader.

### When the inventory comes from a rendered page or an extraction report

Apply this only when extracted evidence informs the current token decision; it is not an extra audit or a
requirement to install an extractor, crawl more pages, or produce a manifest for a Quick naming question.

- Keep enough capture context to re-check the affected observation: source URL/route or artifact and version,
 capture time when available, selector/node and property, viewport/zoom, theme, component state and relevant
 locale. Record the method/tool version and supplied limits when known; do not invent missing metadata or
 collect credentials. Reuse the audit coverage record in `governance-and-consistency.md` §2 when applicable.
- Preserve the authored value or declaration when available, the computed value at the captured condition,
 and any normalized value separately. Keep colour space/alpha and the root-size context for rem/px conversion;
 do not collapse materially different values through rounding, dropped alpha or an assumed conversion.
- Separate **observed value/use**, **inferred semantic role** (with its reason and uncertainty), and
 **proposed mapping to the product's token**. Frequency, visual similarity and classifier confidence do not
 establish intent. Generated ramps, default values and suggested modes are proposals, not observations.
- A computed value proves that rendering, not the authored token, alias chain or winning CSS declaration.
 A matching stylesheet rule is only a candidate source until the cascade/binding is inspected. If code or
 bindings are unavailable, leave token use/bypass unverified even when the displayed value matches a token.
- One page, viewport or theme is a sample, not the complete design system. Route-local values may be valid
 exceptions; observed foreground/background pairs must retain their state, theme and text size/weight.
 An unassessed transparent, image or gradient background, failed capture, or zero inspected pairs is not a
 contrast pass. Use the applicable pair requirement in §4; an extractor's score is not conformance evidence.
- Reconcile candidates with the accepted product system before proposing changes. Preserve approved names,
 aliases, modes and manual overrides unless changing them is in scope; extraction never authorizes importing
 another site's identity or overwriting the current system. Keep unresolved mappings explicit.

## 7. Deduplication and semantic distinction

- Identical value ≠ identical meaning. `color.border.focus` and `color.action.primary.background` may both be
  `{blue.600}` today and still be two tokens, because a theme or an accessibility fix may move one without the
  other. Merge only when the *role statements* are the same.
- Two tokens with the same role and different values are the real duplicates (drift). Pick the intended value
  from Tier 0 evidence (newest library version, documented spec, code), alias the other, deprecate.
- A primitive used by exactly one semantic token is fine; a semantic token used by nothing is a candidate for
  removal only after checking code consumers and modes.
- Never merge across categories because values match (`space.200` and `radius.200` both 8 px).

## 8. Hard-coded values

Policy to apply unless the product documents otherwise:
- Raw values live only in the primitive definitions. Everything else references a token.
- Allowed exceptions, each documented with reason and owner: brand illustration/imagery colours, data-
  visualization series palettes (they need their own system), third-party embeds, legally mandated colours,
  pixel-exact platform affordances, truly one-off marketing surfaces. "No matching token existed" is a reason
  to add a role, not an exception.
- Audit output for a hard-coded value: location, value, nearest token, decision (migrate / add role / document
  exception / unknown).

## 9. Token migration (rename, restructure, remove)

1. Count consumers first: Figma (library usage, variable references, styles), code (grep/usage analytics,
   generated outputs, downstream packages), docs.
2. Keep the old name resolvable during a compatibility window: a deprecated alias pointing at the new token
   (DTCG `$deprecated` with a message naming the replacement; in code a deprecated export or CSS variable alias;
   in Figma rename in place when the reference graph is preserved, otherwise swap via variable mapping).
3. Change values and names in separate steps when both change; a simultaneous change hides regressions.
4. Verify per mode after migration (contrast pairs, visual regression on key stories/screens).
5. Remove only when consumer count is zero or the owner accepts the break; announce in the changelog.
6. A renamed token with an unchanged value and a kept alias is non-breaking; a removed name, changed semantics,
   or value change that alters layout/contrast is breaking.

## 10. DTCG-oriented serialization (only when a token file is requested)

Prefer the stable DTCG 2025.10 structure to any proprietary schema. Illustrative shape, names and values are
placeholders, never evidence for a real system:

```json
{
  "color": {
    "$type": "color",
    "blue": {
      "600": {
        "$value": { "colorSpace": "srgb", "components": [0.141, 0.341, 0.961], "hex": "#2457F5" },
        "$description": "Primitive. Do not use directly in components."
      }
    },
    "action": {
      "primary": {
        "background": {
          "$value": "{color.blue.600}",
          "$description": "Background of the single most important action on a surface."
        }
      }
    },
    "brand": {
      "primary": {
        "$value": "{color.action.primary.background}",
        "$deprecated": "Renamed; use color.action.primary.background."
      }
    }
  },
  "space": {
    "$type": "dimension",
    "400": { "$value": { "value": 16, "unit": "px" } },
    "inset": { "md": { "$value": "{space.400}" } }
  }
}
```

Rules: `$value` required; `$type` on the token or inherited from the nearest group (tools must not guess);
aliases in curly braces resolve to the referenced token's whole value and may chain but not cycle; colour values
are objects (hex is an optional fallback); dimensions are `{value, unit}`; use `$deprecated` (boolean or message)
for retired names; `$extensions` for tool-specific data under a vendor key; file as `*.tokens.json` /
`*.tokens`. Modes: the 2025.10 format has no mode construct, represent modes as separate files or sets per mode
with identical semantic names, or via the consuming tool's theme mechanism, and say which you chose. Check the
consuming tool's support: several pipelines still expect legacy string values (`"#2457F5"`, `"16px"`).

**When importing or exporting extracted token data:**
- Confirm the destination's actual format/version and validate the requested output against it; a filename,
 `$value`/`$type` pair or successful JSON round-trip alone does not establish schema compatibility.
- Check that aliases resolve without cycles or missing targets, and preserve required types, colour alpha,
 mode identity and source metadata through conversion. Report any flattening, substitution or information
 loss instead of silently converting it into an approved value; never fill missing evidence with defaults.
- Compare the proposed mapping/output with the accepted system before an authorized import or replacement.
 Export generation does not itself authorize writing into production code or a design library. Do not claim
 a destination import or round-trip was verified unless it was actually checked; otherwise name that limit.

## 11. Warnings

- One-token-per-value conversion creates a palette, not a system; it moves the drift into token names.
- Excessive abstraction (five-hop aliases, a token for every CSS property) makes the system unreadable and
  unmaintainable; nobody will know which layer to change.
- Meaningless aliases (`color.primary → color.brand → color.blue600` with no role difference) are noise.
- Merging semantically distinct roles because their values match destroys theming and accessibility headroom.
- Raw hex/pixel usage when a valid token exists is a defect (token bypass), not a preference.
- Do not invent tokens for a hypothetical dark mode the product has not committed to; architect so it can be
  added (semantic layer with one mode) without pretending the values exist.
- With no Tier 0 inventory, recommend layers, naming rule and role list as a template with placeholders; never
  present invented values, counts or modes as the product's.
- Do not rename the whole system to match an exemplar's naming.

## 12. Output shapes

Quick token question → Decision, existing token evidence, recommendation, consequence.
Architecture change → layers proposed, naming rule, mode table (semantic token × mode), migration map, breaking
changes, open unknowns. Audit → counts, classification table (confirmed / probable / intentional exception /
unknown), migration approach, prevention rules. Token file → DTCG-oriented JSON plus a one-paragraph note on
tool compatibility and how modes were represented.

Sources synthesized here: DTCG Format and Color Modules 2025.10 (format, types, alias and deprecation rules);
WCAG 2.2 (contrast and focus thresholds); Fluent 2, Material 3 and Carbon as layered-token exemplars;
*Designing Interfaces* 3e (style inheritance from a single base, consistency to avoid UX debt). See
`source-map.md`.
