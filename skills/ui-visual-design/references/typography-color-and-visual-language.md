# Typography, Color and Visual Language

This reference covers applying type, color, surfaces, shape, iconography, imagery and state styling at screen level, using the product's existing styles and tokens. Defining scales, palettes or token architecture belongs to the Design Systems skill (Skill 05).

## Contents
1. Typography
2. Color application
3. Contrast: thresholds and measurement
4. Light, dark and high-contrast themes
5. Borders, dividers, radius and elevation
6. Icons
7. Imagery and illustration
8. Visual affordance
9. State differentiation
10. Brand expression and the decoration budget

## 1. Typography

**Apply roles, not sizes.** Map each piece of content to a text style from the design system by role: display, heading levels, title, body, label, caption, or whatever names the system uses. If the screen needs a style the system lacks, record a `[DS GAP]`. Don't create a parallel scale.

**Hierarchy**
- Use only as many distinct styles as the content hierarchy needs.
- Each style must differ visibly from its neighbor in size, weight or both.
- De-emphasize secondary text with size, weight or position before color. If you do use color, the text must still meet contrast minimums.
- Hints and captions step down clearly from labels. A difference so small that it looks accidental fails as hierarchy.

**Readability**
- Alignment:
  - Align body text to the start edge with a ragged end.
  - Center only short lines.
  - Avoid justified body text.
- Line length: keep body text to roughly 45–80 characters per line. This is a common typographic range. WCAG 1.4.8 (AAA) caps it at 80 characters, or 40 for CJK.
- Line spacing:
  - Use about 1.4–1.6× for body text; at AAA, 1.4.8 asks for at least 1.5× inside paragraphs.
  - Go looser for long reading and tighter only for short display lines.
  - Layouts must survive users raising line height to 1.5× and paragraph spacing to 2× (1.4.12).
- Weight: avoid light and thin weights for small or body text. Regular through bold reads best.
- Faces: avoid all caps, italics, decorative or display faces in running text. Keep display faces for large headings.
- Numbers: use tabular (fixed-width) figures for numbers that people compare or that update in place. Make sure codes can't confuse 0 with O, or 1 with l and I.

**Scaling and minimums**
- Text must scale with user settings: Dynamic Type on Apple platforms, sp on Android, rem or em on the web.
- Specify how lines wrap and how containers grow. Never fix the height of a text container.
- Take minimum sizes from the design system first, then from the platform block in the responsive reference §10. On the web, WCAG sets no minimum size, but text must resize to 200% without loss (1.4.4).
- Truncate only non-critical text, as a last resort. When you do, specify:
  - where it cuts: at the end, or in the middle for file names and IDs;
  - the maximum number of lines.
  How users reach the full text is an interaction dependency.

**Fonts and scripts**
- Prefer the platform's system fonts unless the brand font is licensed for the platform and covers every target script and weight.
- Check glyph coverage for every target locale and define fallbacks.
- Scripts with tall shapes or stacked marks, such as Thai, Arabic, Devanagari and Vietnamese, need more line height.
- Avoid letter-spacing on connected scripts such as Arabic.
- Custom fonts must support the platform's text-scaling and bold-text settings the way system fonts do.

**If no type scale exists**
- Propose the smallest workable set of roles, often 4–6.
- Start from a body size that suits the platform: around 16 px on the web; native defaults are in the platform blocks of the responsive reference §10.
- Step up with a modest, consistent ratio, and set line heights on the spacing grid.
- Mark every value `[PROVISIONAL]`. If the product has a design system that only lacks a type scale, also record that as a `[DS GAP]` for Skill 05. With no system at all, the values stay local to this interface.

## 2. Color application

Assign each color a role and use the design system's semantic tokens:

| Role | Used for | Guardrail |
|---|---|---|
| Neutrals | backgrounds, surfaces, text levels, borders, dividers | most of the UI; hierarchy comes from here |
| Interactive accent | primary actions, links, selection, focus | one accent family; don't spend it on decoration |
| Status (error, warning, success, info) | feedback and state | reserved for meaning; always paired with an icon or text |
| Brand | identity moments, accent, illustration | not wallpaper across task areas |
| Data visualization | series and categories | separate palette; never reuse status colors as categories |

- Give each color one meaning across the product. If a brand color marks interactive text, don't reuse it for static text.
- Hierarchy must survive grayscale. Color reinforces it; it doesn't create it.
- Color must never be the only thing that conveys meaning, state, action or distinction (WCAG 1.4.1). Pair it with text, an icon, shape, weight, position or a pattern.
- Check color meanings for the target markets. For example, the colors that mean "price up" and "price down" differ between markets.
- If a brand color fails contrast in a role it must fill:
  - use the accessible variant from the design or brand system;
  - if none exists, flag a `[DS GAP]` and a brand dependency. Don't quietly change the brand.

## 3. Contrast: thresholds and measurement

| What | Minimum | Source |
|---|---|---|
| Body and small text, including placeholder and helper text | 4.5:1 | WCAG 2.2 SC 1.4.3 (AA) |
| Large text: at least 18 pt, or 14 pt bold (≈24 CSS px, or ≈18.5 CSS px bold) | 3:1 | SC 1.4.3 (AA) |
| Component boundaries needed to identify a control; state indicators; meaningful graphics and icons | 3:1 against adjacent colors | SC 1.4.11 (AA) |
| Enhanced text contrast | 7:1 (large text 4.5:1) | SC 1.4.6 (AAA) |

**Exemptions**
- Disabled or inactive components, pure decoration and logotypes are exempt.
- Disabled elements should still be recognizable as present.

**Platform guides**
- Some platform guides state looser or stricter contrast numbers than WCAG; the specifics are in the platform blocks of the responsive reference §10.
- When the accessibility target includes WCAG, apply WCAG's thresholds.

**Measuring**
- Measure token or hex values, not screenshots, whenever possible.
- Screenshot sampling is approximate because of compression, anti-aliasing and color profiles. Report screenshot measurements with a confidence level.
- Test the worst case. For text over photos, gradients or translucent materials, check against the lightest and darkest backdrop the text could plausibly sit on. Add a scrim or dimming layer, or move the text.
- Check every state (hover, pressed, selected, focus, error) in every supported theme and contrast setting. A pair that passes in light mode can fail in dark mode.

## 4. Light, dark and high-contrast themes

**Dark mode is its own theme, not an inversion**
- Backgrounds get dimmer and foregrounds brighter. Many colors are adjusted rather than flipped.
- Use theme tokens. A missing theme token is a `[DS GAP]`.

**Elevation in dark themes**
- Show elevation with lighter surfaces; each platform's version is in its block in the responsive reference §10.
- Shadows do little on dark backgrounds, so add tonal steps or borders where separation matters.

**Color variants**
- Brand and status colors usually need theme-specific variants to keep both their contrast and their meaning.

**Images and icons**
- Soften white-background images in dark contexts.
- Give icons and illustrations dark variants where their edges disappear.
- Never flip an image in a way that changes its meaning.

**High contrast**
- Don't rely on background color, shadows or tints alone for any boundary or meaning; contrast modes can remove them.
- Which user settings to test against is in the responsive reference §8.

**Appearance setting**
- The theme follows the system setting. An app-specific appearance toggle is a product decision.

**Per-theme checklist** (for each supported theme: light, dark, high contrast)
- the surface hierarchy still reads, and the borders that matter stay visible;
- text and non-text contrast hold in every state;
- semantic colors keep their meaning, and brand colors stay accessible;
- the focus indicator is visible;
- disabled and read-only stay distinguishable;
- status uses more than color;
- images, illustrations and icons have suitable variants;
- translucent materials stay legible with reduced transparency.

## 5. Borders, dividers, radius and elevation

**Borders**
- Use a border when the boundary carries meaning: inputs, focus, selection, dense data grids. Otherwise prefer spacing.
- A boundary that identifies a control needs 3:1 contrast (1.4.11).

**Dividers**
- Use dividers in dense lists and tables, or between regions of different kinds. Don't put one between every element.

**Radius**
- Take radii from one family in the design system, and scale them with component size.
- Keep nested shapes concentric: the inner radius is roughly the outer radius minus the padding.
- Elements that touch the screen edge are usually square.
- Mixing sharp and rounded corners needs a semantic reason.

**Elevation**
- Use elevation to show layering and temporary surfaces, such as menus, popovers and dialogs above content. It isn't decoration.
- Keep few levels and one light direction, and treat each theme on its own terms.

## 6. Icons

**Consistency**
- Use one icon family per product and platform, with a consistent style (outline or fill), stroke weight, corner treatment, perspective and level of detail.
- Size and weight icons to match the adjacent text.
- A filled variant can mark a selected state, as long as the system does so consistently.

**Meaning and labels**
- Pair icons with text labels unless the icon is conventional and unambiguous in context.
- An icon-only control also needs an accessible name; that is an engineering dependency.
- An icon that carries meaning needs 3:1 contrast against its background; a decorative one doesn't.
- The same function gets the same icon and label everywhere (WCAG 3.2.4). One icon never means two things.

**RTL:** which icons mirror and which don't is covered in the responsive reference §7.

## 7. Imagery and illustration

**Images**
- First decide whether each image is content or decoration. Decorative images are the first thing to cut on small screens or in dense layouts.
- Within a collection, use one aspect ratio and crop to the subject. Keep native proportions only when the shape itself carries meaning.
- Always specify a fallback for missing and broken images at the same size and ratio, so the layout holds.
- Text over an image needs a scrim or a region with guaranteed contrast. Measure the worst case.
- Don't put text inside images unless it's essential (WCAG 1.4.5). Text in an image can't scale, translate or reflow.
- Provide dark-mode variants where needed.
- Don't flip photos for RTL. If direction matters, create a new version.
- Avoid generic stock imagery that adds no information.

**Illustration**
- Use illustration in empty states, onboarding and success moments, not in dense work areas.
- Keep one consistent style.
- Never let an illustration be the only carrier of essential information.

## 8. Visual affordance

- Interactive elements look interactive at rest. Static elements never borrow interactive styling.
- Give primary buttons a filled, contrasting shape with clear padding. A pale outlined button next to rich visuals disappears.
- Keep prominence scarce: one prominent action per region.
- Distinguish the preferred option from the alternatives by style, not by size.
- Underline links in running text. It's the simplest robust way to meet 1.4.1. Use one link color throughout.
- Touch screens have no hover. Any cue that appears only on hover needs an equivalent that's visible at rest.
- Flat styles still need affordance. Use position, shape and a consistent treatment for each type of control.

## 9. State differentiation

Style the states that already exist: those defined by the interaction spec, product behavior, platform convention or the component's existing contract. Drawing a state doesn't decide its logic: when it appears, what triggers it, how long it lasts and what happens next are interaction decisions. If a state you need is missing, flag `[DEPENDENCY: Interaction]` rather than inventing it. Focus splits the same way: the indicator's appearance is visual; focus order and movement are interaction.

| State | Visual cue (combine cues; color alone never suffices) | Watch for |
|---|---|---|
| Default | resting style from the design system | must already look interactive |
| Hover (pointer only) | subtle change in fill or overlay | never the only way to discover anything |
| Focus (keyboard) | clearly visible indicator around the whole control, at least 3:1 against adjacent colors | must differ from hover and selected, and must not be hidden by sticky UI (2.4.11). At AAA (2.4.13), its area must be at least a 2 px perimeter, with 3:1 contrast between focused and unfocused states |
| Pressed | brief shift, stronger than hover | every custom control needs one |
| Selected | persistent cue: indicator, checkmark, weight, or fill plus border | must differ from focus and survive grayscale |
| Disabled | reduced emphasis, still recognizable as present | exempt from contrast, so it can't be relied on to explain anything |
| Read-only | value at full contrast; field affordance removed or subdued | must not look disabled |
| Loading | indicator in place; dimensions preserved | label what is loading where possible |
| Error, warning, success, info | color plus icon plus text, in a consistent severity order | status colors are reserved for status |

- Systematic state overlays are a design-system decision. Platform-specific values are in the platform blocks of the responsive reference §10.
- Check every state in every theme and contrast setting.

## 10. Brand expression and the decoration budget

**Where brand lives**
- Brand comes through in:
  - typeface choice;
  - accent color;
  - illustration and imagery style;
  - iconography;
  - voice;
  - a few signature moments, such as onboarding, empty states and marketing surfaces.
- Task-heavy areas stay quiet. Separate productive moments, where the user is working, from expressive ones.

**The decoration budget**
- For every shadow, gradient, glass or blur effect, border, card and extra accent, name its job: separate, layer, emphasize, identify, or delight in a low-stakes moment. If it has no job, remove it.

**Glass and translucency**
- Use translucent and glass materials only where the platform's design language calls for them, and only where legibility is verified over the worst backdrop.
- Platform rules on where glass may go are in the platform blocks of the responsive reference §10.

**Novelty**
- Novelty isn't usability. Convention wins unless a new pattern is self-explanatory or clearly worth learning.
