# Source Map

This file says which source governs which decision, how far to trust each one, and what to do when they disagree. Read it when a source conflict, a citation question or a currency question comes up. Routine design work doesn't need it.

## Contents
1. Authority order
2. Source profiles
3. Conflict-resolution algorithm
4. Known conflicts and their resolutions
5. Verification log and limits
6. Runtime citation and copyright rules

## 1. Authority order

From highest to lowest:
1. Mandatory constraints:
   - the product's accessibility target;
   - applicable law;
   - brand restrictions;
   - platform requirements that the OS or app store enforces, such as reserved screen areas and system-controlled UI.
2. Tier 0, product truth.
3. Tier 1, normative and platform: WCAG 2.2, plus the Apple HIG or Material 3 when they apply.
4. Tier 2, canonical and exemplar: *Designing Interfaces*, *The Elements of User Experience*, Carbon, Fluent 2.
5. Tier 3, sanity check: *Don't Make Me Think*.

**Platform recommendations aren't mandatory constraints.** Guidance such as Apple's 44 pt hit region or Material's 48 dp target is Tier 1 guidance. Follow it unless the product has a documented reason not to. It becomes mandatory only when the product's accessibility target or a platform rule requires it.

A higher tier wins within its own domain. Existing product visuals are evidence, but they aren't automatically correct. When they break a mandatory constraint, flag the conflict instead of copying it.

## 2. Source profiles

Each profile below lists the source's type, authority, domain, what it's useful for, when to use it and when not to, its priority, how it resolves conflicts, and its access and copyright limits.

### Product visual truth
- **Type:** The product's own materials:
  - design system: components, variants, tokens and variables, type and color styles, icons, breakpoints;
  - brand system;
  - real content;
  - approved UX structure and interaction spec;
  - platform and viewport data;
  - relevant research;
  - the accessibility target.
- **Authority:** The highest contextual authority for this product.
- **Domain:** This product, on its supported platforms.
- **Useful for:** Every value, component and pattern decision.
- **When to use:** Always, before anything external.
- **When not to use:** Don't treat a screen that breaks a mandatory constraint as precedent, and don't silently fill gaps. Mark them `[DS GAP]`, `[ASSUMPTION]` or `[DEPENDENCY]`.
- **Priority:** Tier 0.
- **Conflict rule:** Beats Tiers 1–3, except where a mandatory constraint applies.
- **Copyright/access:** Limited to whatever the user supplies or connected tools expose.

### Accessibility law and standards by jurisdiction
- **Type:** Law and the standards it cites. In the EU, for example, accessibility requirements build on EN 301 549, which incorporates WCAG success criteria.
- **Authority:** Mandatory wherever it applies to the product.
- **Domain:** Depends on the market, sector and product type.
- **Useful for:** Setting the accessibility target the design must meet.
- **When to use:** When the user or the product names a market, regulation or conformance target.
- **When not to use:** Never interpret the law yourself. The skill gives design guidance, not legal advice.
- **Priority:** A mandatory constraint.
- **Conflict rule:** Overrides every tier where it applies.
- **Copyright/access:** Not verified in this build. Confirm the applicable target with the product's accessibility or compliance owner.

### WCAG 2.2 (W3C)
- **Type:** W3C Recommendation, first published 5 Oct 2023. The latest publication is 12 Dec 2024, and errata exist. https://www.w3.org/TR/WCAG22/
- **Authority:** The normative accessibility standard for web content, and the usual baseline in accessibility law and procurement.
- **Domain:** Web content. W3C applies it to native software through two informative notes: WCAG2ICT (Group Note; latest completed version 11 Dec 2025, with a further draft update in progress in 2026) and WCAG2Mobile (Group Draft Note, 6 May 2025, still the latest publication when checked).
- **Useful for:**
  - use of color;
  - text and non-text contrast;
  - resize, reflow and text spacing;
  - content on hover or focus;
  - focus visibility, appearance and not-obscured;
  - target size;
  - consistent identification;
  - error identification and labels.
- **When to use:** For any web UI, and for native UI whose accessibility target references WCAG.
- **When not to use:**
  - Don't claim conformance from a static design.
  - Don't load the whole standard, only the applicable criteria.
  - Don't treat AAA criteria as required unless the target says so.
- **Priority:** Tier 1. It is mandatory when it is the product's accessibility target.
- **Conflict rule:** Overrides product precedent, the books and the exemplars. Against platform guidance, apply whichever requirement is stricter when both apply.
- **Copyright/access:** An open W3C document. Cite it by SC number and short name.

### Apple Human Interface Guidelines
- **Type:** Apple's platform design guidance. https://developer.apple.com/design/human-interface-guidelines/
- **Authority:** Platform authority for Apple platforms.
- **Domain:** Native apps on iOS, iPadOS, macOS, watchOS, tvOS and visionOS only.
- **Useful for:**
  - layout: safe areas, size classes;
  - typography: text styles, Dynamic Type, minimum sizes;
  - color: system and semantic colors;
  - materials: Liquid Glass and the standard materials;
  - Dark Mode;
  - icons: SF Symbols;
  - right-to-left;
  - accessibility;
  - buttons.
- **When to use:** When the product or feature runs natively on an Apple platform.
- **When not to use:** For web or Android products, and never mixed with Material.
- **Priority:** Tier 1, conditional on an Apple platform.
- **Conflict rule:** Platform truth for Apple builds. Where it is looser than WCAG (its contrast table allows 3:1 for bold text at any size and for 18 pt text), use WCAG when the accessibility target includes it.
- **Currency:** The Liquid Glass design language dates from June 2025, and WWDC26 brought refinements. Pages were updated through 13 Oct 2026, including a new "Designing for iPhone Duo" page (9 Sep 2026).
- **Copyright/access:** Apple content: paraphrase it, don't reproduce it. The pages are rendered with JavaScript, but adding `.md` to a HIG page URL returns Apple's Markdown version.

### Material Design 3
- **Type:** Google's design system and Android's platform design language. https://m3.material.io/ ; implementation guidance lives on developer.android.com.
- **Authority:** Platform authority for Android and for products built on Material.
- **Domain:** Android apps and products that explicitly use Material, including Material-based web products.
- **Useful for:**
  - window size classes and adaptive layouts;
  - color roles and type roles;
  - shape and tonal elevation;
  - state layers;
  - touch targets;
  - RTL support.
- **When to use:** For an Android or Material-based product.
- **When not to use:** For iOS or for non-Material web products. Don't turn every product into a Material product.
- **Priority:** Tier 1, conditional on Android or Material.
- **Conflict rule:** Platform truth for Android and Material builds. The product's own design-system adaptations win wherever they don't break a mandatory constraint.
- **Currency:** Material 3 Expressive was announced in May 2025. Confirm whether the product has adopted it.
- **Copyright/access:** m3.material.io pages couldn't be read by machine during this build. Values were verified through developer.android.com, the Compose Material 3 API reference and official token sources.

### IBM Carbon Design System (v11)
- **Type:** An open-source enterprise design system. https://carbondesignsystem.com/
- **Authority:** A mature exemplar. It is not a universal visual language.
- **Domain:** Enterprise and data-dense web UI.
- **Useful for:** Benchmarks:
  - 2x Grid and gutter modes;
  - productive versus expressive type;
  - the layering model;
  - data-table densities;
  - dashboard and data-visualization guidance.
- **When to use:** For enterprise or data-heavy UI when the product's design system lacks guidance on the question, or when a reasoned comparison helps.
- **When not to use:**
  - Don't adopt IBM Plex, Carbon colors, spacing or component styling for a non-IBM product.
  - Don't consult it alongside Fluent unless you are comparing the two.
- **Priority:** Tier 2. For IBM products it is Tier 0.
- **Conflict rule:** Never overrides Tier 0 or Tier 1.
- **Copyright/access:** An open site. The relevant pages were updated through Sep–Oct 2026.

### Microsoft Fluent 2
- **Type:** Microsoft's design system. https://fluent2.microsoft.design/
- **Authority:** A mature exemplar. It is not a universal visual language.
- **Domain:** Microsoft-ecosystem and enterprise UI.
- **Useful for:** Benchmarks:
  - the layout ramp and size classes;
  - the type ramp;
  - brand and semantic color usage;
  - elevation built from key and ambient shadows;
  - shape;
  - light, dark and high-contrast theming.
- **When to use:** For enterprise UI benchmarks, or as platform guidance for Windows apps and Teams or Office add-ins.
- **When not to use:** Don't copy Segoe or Fluent styling into unrelated products.
- **Priority:** Tier 2. For Microsoft-ecosystem products it acts as Tier 1.
- **Conflict rule:** Never overrides Tier 0 or Tier 1 for unrelated products.
- **Copyright/access:** An open site. Some values on the site differ from the published code tokens (section 4). When exact values matter, prefer the code tokens.

### Designing Interfaces, 3rd ed. (Tidwell, Brewer, Valencia; O'Reilly, 2020)
- **Type:** A book of interaction and interface patterns.
- **Authority:** Canonical practitioner reference; not normative.
- **Domain:** Screen-based web and mobile UI.
- **Useful for:**
  - visual hierarchy, Gestalt grouping and visual flow;
  - layout patterns and visual style;
  - recomposing for mobile;
  - lists and cards;
  - action priority;
  - complex data;
  - forms and how errors are presented.
- **When to use:** Construction-time only. Its principles are already distilled into these references, so don't open it at runtime.
- **When not to use:** Don't let it override WCAG 2.2 or current platform guidance. Several of its remarks on contrast, color and sizing predate them (section 4).
- **Priority:** Tier 2 (primary book).
- **Conflict rule:** Loses to Tiers 0–1.
- **Copyright/access:** Copyrighted, and used for principles only. Chapters drawn on: 2 (the Dashboard and Settings Editor patterns), 4, 5, 6, 7, 8 (selected sections), 9 and 10.

### The Elements of User Experience, 2nd ed. (Garrett; New Riders, 2011)
- **Type:** A conceptual framework: five planes, from strategy to surface.
- **Authority:** Canonical conceptual reference; not a visual system.
- **Domain:** Any digital product.
- **Useful for:**
  - telling the skeleton plane from the surface plane, i.e. spotting when a "visual" problem is really structural;
  - follow-the-eye checks;
  - decisive contrast versus uniformity;
  - internal and external consistency;
  - palettes and type treated as systems of roles;
  - checking that comps map back to wireframes.
- **When to use:** Construction-time only. Its principles are already distilled into these references, so don't open it at runtime.
- **When not to use:** As a visual system, or as a source of accessibility thresholds. It predates them.
- **Priority:** Tier 2.
- **Conflict rule:** Loses to Tiers 0–1.
- **Copyright/access:** Copyrighted, and used for principles only. Chapters drawn on: 2, 6 and 7.

### Don't Make Me Think, Revisited, 3rd ed. (Krug; New Riders, 2014)
- **Type:** A book of web usability heuristics.
- **Authority:** A sanity check. It is not a design methodology.
- **Domain:** Web and mobile usability.
- **Useful for:**
  - scanability;
  - conventions;
  - clear visual hierarchy and clearly defined areas;
  - making clickable things obvious;
  - noise reduction;
  - formatting for scanning;
  - visible affordances on touch screens.
- **When to use:** Construction-time only. Its checks are already distilled into these references as clarity tests, so don't open it at runtime.
- **When not to use:** As a visual-design methodology, or to override product or accessibility evidence.
- **Priority:** Tier 3.
- **Conflict rule:** Loses to every higher tier.
- **Copyright/access:** Copyrighted, and used for principles only. Chapters drawn on: 3, 4, 5, 10 and 12.

### W3C Internationalization, "Text size in translation"
- **Type:** An informative W3C article. https://www.w3.org/International/articles/article-text-size.en.html
- **Authority:** Informative guidance. It cites IBM's figures for how much text expands when translated from English into European languages.
- **Domain:** Localization of any UI.
- **Useful for:** Expansion heuristics for localization stress tests.
- **When to use:** When translation length is in scope.
- **When not to use:** As limits, or for CJK. Its figures are averages for European languages.
- **Priority:** Tier 2 (supporting).
- **Conflict rule:** Real translated strings for the product win over these averages.
- **Copyright/access:** An open W3C article. Cite it by title.

## 3. Conflict-resolution algorithm

1. Name the exact visual decision, e.g. "secondary text color in table rows".
2. Name the platform and product context.
3. Apply the mandatory constraints: the accessibility target, legal and platform requirements, and brand restrictions.
4. Look for an existing answer in the product's design system and brand.
5. Test that answer against real content: lengths, languages, data ranges.
6. If the decision is still open, apply the most relevant Tier 1 source for the platform.
7. Consult a Tier 2 exemplar only for a reasoned benchmark. Use one system, not a blend.
8. Prefer consistency with valid existing product patterns over a new convention.
9. Introduce a new convention only with an explicit reason, and mark it `[LOCAL EXCEPTION]` or `[DS GAP]`.
10. Record anything left unresolved, with the options and what would decide between them.

Never assemble a UI from the visual languages of several design systems.

## 4. Known conflicts and their resolutions

| Conflict | Resolution |
|---|---|
| A book advises de-emphasizing with low contrast, or "toning down" high contrast | WCAG wins. De-emphasize with size, weight and position; text keeps 4.5:1 (3:1 for large text). |
| A book sets the minimum error styling as color and/or a small graphic | WCAG 3.3.1 and 1.4.1 win. Use a text message plus an icon plus color. |
| The book's "loading indicator" is a determinate bar; Material's "loading indicator" is indeterminate, for short waits | Say "determinate" or "indeterminate" explicitly. |
| Apple allows 3:1 for bold text at any size and for 18 pt text; WCAG's large text starts at 14 pt bold (≈18.5 CSS px) or 18 pt (≈24 CSS px) | Use WCAG's thresholds when the accessibility target includes WCAG. |
| Apple's minimum control size is 28 pt, but its button hit region is at least 44 pt | The visual can stay small if needed, but keep the hit region at 44 pt or more. |
| Material requires 48 dp; WCAG AA requires 24 CSS px | On Android, use 48 dp. On the web, use the product's design-system value or at least 24 px (AA), and 44 px for touch-first UI where feasible. |
| Fluent's site and code disagree: radius "Large" is 8 on the site and 6 in code; Subtitle 1's line height is 26 on the site and 28 in code | It's only an exemplar. If exact values matter, the code tokens are the published implementation. |
| Existing product screens violate contrast or target-size requirements | The mandatory constraint wins. Flag the existing screens. |

## 5. Verification log and limits (2026-10-20)

**Books.** All three were checked as the claimed editions and complete: title, copyright and contents pages, the final chapter and the index are present, and the text is extractable. No page numbers are cited anywhere in this skill.

**Read directly in primary sources by the author:**
- **WCAG 2.2:** success-criterion text on w3.org, from:
  - the TR document;
  - the "What's New in WCAG 2.2" page;
  - the Understanding pages for 1.4.3, 2.5.8, 3.3.1 and 3.3.2, and for 3.2.4 the WCAG 2.1 page (the criterion's text is unchanged in 2.2);
  - the WCAG2ICT and WCAG2Mobile status pages.
- **Apple HIG:** the Accessibility, Typography, Color, Dark Mode, Materials, Buttons and Right to Left pages, and the "What's new" log.
- **Material 3:** on developer.android.com, the window-size-class and accessibility pages; state-layer values from the official AndroidX token file.
- **Carbon:** the data-table guidelines.
- **Fluent 2:** the layout page.
- **W3C Internationalization:** "Text size in translation".

**Re-checked in a separate review pass against primary sources:**
- Carbon: grid breakpoints and columns, productive and expressive type sets, condensed gutters, data-table densities.
- Fluent: global versus alias tokens, key and ambient shadows, size classes and targets, and the radius difference between site and code.
- Material: color-role names, type roles and emphasized styles, font scaling on Android 14.
- Apple: SF Symbols weight matching.

The review pass found one error, in the WCAG 1.4.13 row of the responsive reference, and it has been corrected.

**Re-checked in the boundary patch pass (2026-10-20), against primary sources:**
- WCAG: the W3C WCAG 2 overview (2.2 published 5 Oct 2023, updated 12 Dec 2024) and the WCAG2ICT and WCAG2Mobile publication status.
- Apple HIG: the "What's new" log (Liquid Glass guidance from June 2025, WWDC26 refinements on 8 Jun 2026, "Designing for iPhone Duo" on 9 Sep 2026, latest entries 13 Oct 2026) and the Markdown version of the HIG root page.
- Android: the window-size-class page, including the large and extra-large widths, and the accessibility foundations page (48 dp targets, 12 sp minimum body text, 4.5:1 text and 3:1 non-text contrast); Material 3 Expressive's May 2025 announcement.
- Carbon: data-table row sizes, from the website source.
- Fluent 2: the radius and Subtitle 1 values on the site versus the code tokens.

This pass found one more error: the hierarchy reference gave Carbon a documented default row height of 40 px. Carbon's guidance states no default (its React component defaults to the 48 px size), so the claim was removed.

**From the research pass only** (official pages, not re-read line by line):
- Carbon's layering model;
- Fluent's brand-color usage;
- Material's tonal elevation.

**Not verified:**
- Carbon's dark-theme token values.
- Fluent's table component page (it returned 404).
- Material's exact margins above compact width.
- The legal status in any particular jurisdiction.

When a later run needs one of these facts and it matters to the decision, re-verify that single page rather than trusting this snapshot.

## 6. Runtime citation and copyright rules

- Cite sources by identifier, e.g. "WCAG 2.2 SC 1.4.11", "Apple HIG › Materials", "Material 3 › window size classes". Don't cite page numbers, and don't quote more than a few words.
- Book-derived principles are stated in this skill's own words. Never reproduce passages, chapters or figures from the books.
- If a source can't be reached, say so. Don't reconstruct its content from memory.
