# Responsive, Accessibility and Platform

A decision guide for adaptive layout, resilience (zoom, text spacing, translation, RTL, contrast settings) and platform fit. The values here were checked against primary sources on 2026-10-20; see `source-map.md` for what was checked and how. The product's own decisions override these values, except where a mandatory accessibility or platform constraint applies.

**How to read this file.** Sections 1–9 are platform-neutral. Section 10 has one block per platform: web, Apple, Android/Material, and enterprise exemplars. Read the sections the task needs, plus only the block for the target platform, which you can find by its heading. If the whole file is read, apply only the matching block.

## Contents
1. Responsive decision procedure
2. Transformation patterns
3. Small and large screens
4. Zoom, reflow and text spacing
5. Targets and spacing for input
6. Content stress and localization
7. Right-to-left
8. Contrast settings and theme resilience
9. WCAG 2.2 visual criteria
10. Platform blocks: web · Apple · Android/Material · enterprise exemplars
11. Cross-platform consistency

## 1. Responsive decision procedure

1. **Use what exists.** Start from the product's breakpoints, grid and layout tokens. If the product has none and a platform applies, use that platform's size classes, listed in its block in §10. Don't invent anything that already exists.
2. **Rank the content on this screen** into four groups, taking the priority from the approved structure (if none is given, infer it and mark `[ASSUMPTION]`):
   - always visible;
   - can collapse;
   - can move to a secondary surface;
   - can be dropped at small widths.

   Dropping content is a content or IA decision, and moving it to another surface needs an interaction decision on how it's reached. Propose both; don't decide them (§2).
3. **Find content breakpoints**, but only if none exist. Widen and narrow the layout until something breaks, and change the layout at that width. Typical breaks:
   - body lines run past about 80 characters;
   - columns get narrower than their content;
   - labels wrap awkwardly;
   - a table can't fit its key columns.

   Mark each new breakpoint `[PROVISIONAL]` and note why it exists.
4. **Pick a transformation for each region** (section 2).
5. **Specify each width range:**
   - columns;
   - margins and gutters, as tokens;
   - maximum content width;
   - any type-role changes;
   - density;
   - image ratios;
   - what collapses or moves, and how users reach it (an interaction dependency).
6. **Stress-test the cases in scope:**
   - 320 CSS px wide;
   - 200% text;
   - text-spacing overrides;
   - landscape phone;
   - very wide windows;
   - long translations;
   - RTL.

## 2. Transformation patterns

These transformations stay visual while they rearrange approved content. If a breakpoint seems to need a new navigation model, removed functionality, different destinations, a new content hierarchy, priorities re-ranked without evidence or a different task flow, that's a structural problem: flag `[DEPENDENCY: IA]` instead of styling around it.

| Pattern | Use when | Visual-layer notes |
|---|---|---|
| Reflow (columns stack) | multi-column content on narrow widths | stack in priority order, not in whatever order the source happens to have |
| Reveal (more panes when wider) | list–detail views, supporting panels the approved structure already has | wide layouts gain panes instead of stretching lines; adding new navigation is an IA decision |
| Reposition | side-panel content on narrow widths | where it goes and how it opens is an interaction dependency |
| Resize (fluid) | within one width range | set minimum and maximum widths; cap the reading measure |
| Re-present | e.g. a table becomes a list for lookup; a side sheet becomes a bottom sheet | this is a different component, and any change in behavior is an interaction dependency |
| Reduce | decorative or secondary content on small screens | removing content is a content or IA decision: propose it, don't decide it |

- How navigation is presented (bar, rail, drawer, tabs) is an IA and interaction decision. This skill styles whichever one is chosen.
- Density can differ by input mode (pointer or touch), following the design system's rules. If the system has no such rules, record a `[DS GAP]`.

## 3. Small and large screens

**Mobile is a recomposition, not a shrunken desktop**
- Use fewer elements, in one column, in priority order.
- Get useful content into the first view: cut decorative chrome and collapse stacked header bands.
- Put labels above fields.
- Stack buttons unless they fit side by side with translated labels at enlarged text sizes.
- Plan for glare and movement: no low-contrast text and no tiny type.
- Give every hover-only cue an equivalent that's visible at rest.

**Large screens**
- Cap the reading width.
- Spend extra width on the panes the structure already defines, on supporting content, or on more columns of data.
- Don't stretch forms to full width; field width signals how long the answer should be.
- A landscape phone is wide but short. Check the height before adding panes or tall stacked chrome.

## 4. Zoom, reflow and text spacing

**WCAG 2.2 criteria (web; adapt them for native apps)**
- **1.4.10 Reflow (AA):** content must work without two-dimensional scrolling at 320 CSS px wide (for vertically scrolling content) or 256 CSS px tall (for horizontally scrolling content). Content that needs a 2D layout is exempt, e.g. data tables, maps, diagrams and complex toolbars.
- **1.4.4 Resize Text (AA):** text can be resized to 200% without loss of content or function.
- **1.4.12 Text Spacing (AA):** nothing is lost when users set line height to 1.5×, paragraph spacing to 2×, letter spacing to 0.12× and word spacing to 0.16× the font size.

**What this means for the design**
- Don't fix the height of text containers.
- Wrap essential labels instead of truncating them.
- Keep sticky headers and footers short. At high zoom they eat the viewport and can cover the focused element (2.4.11).
- Don't place text over images unless there's a plan for how it reflows.

**Native apps:** platform text scaling reaches roughly 200% (exact figures are in each platform block). Rows must be able to grow and side-by-side items must be able to stack.

## 5. Targets and spacing for input

| Source | Minimum target | Notes |
|---|---|---|
| WCAG 2.2 SC 2.5.8 (AA) | 24×24 CSS px | Smaller targets pass if a 24 px circle centered on each target's bounding box doesn't intersect another target or another small target's circle. Other exceptions: an equivalent control on the page, a target inline in text, the user agent's default size, a presentation that is essential or legally required |
| WCAG 2.2 SC 2.5.5 (AAA) | 44×44 CSS px | Exceptions: equivalent control, inline text, user agent, essential presentation |

- Platform minimums (Apple, Android/Material, Fluent) are in their blocks in §10. Apply the strictest minimum that's relevant to the product's platforms and accessibility target.
- A small visual can keep a larger invisible hit area, as long as hit areas don't overlap.
- Spacing between targets matters as much as their size, especially in dense toolbars and table actions.

## 6. Content stress and localization

Stress-test with real content, not ideal placeholders. Check only what the request touches:

- **Labels:** very short, very long, long names, titles that wrap to 2–3 lines.
- **Values:** empty, zero and negative values; very large and very small numbers; long currency and date/time formats; units.
- **Media:** missing images, broken images, unusual aspect ratios.
- **User-generated content:** long unbroken strings (URLs, emails, IDs), emoji, mixed scripts.
- **Feedback:** validation messages of one word and of two lines; several errors at once.
- **Volume:** no results, one item, dense lists of hundreds of rows.

**How much translations expand.** These are IBM's averages for translation from English into European languages, as cited in the W3C Internationalization article "Text size in translation". They are averages, not limits, and they don't describe CJK text.

| Length of the English text | Typical length of the translation |
|---|---|
| up to 10 characters | 200–300% |
| 11–20 | 180–200% |
| 21–30 | 160–180% |
| 31–50 | 140–160% |
| 51–70 | 151–170% (as published; it breaks the downward trend) |
| over 70 | about 130% |

- Short strings carry the highest risk: buttons, tabs, table headers, navigation, badges. Size them to their content with minimum and maximum widths, never at fixed English widths.
- Languages that build compound words (German, Finnish, Dutch) produce long words that can't break. Allow wrapping or hyphenation.
- CJK text can use fewer characters yet take more width per glyph. Thai, Arabic, Devanagari and some other scripts often need more vertical space.
- Don't abbreviate to make text fit, because other languages may not abbreviate the same way.
- Check that aligned items stay aligned when they grow at different rates, and that key content still shows in the first view.

## 7. Right-to-left

Specify layouts with start and end, not left and right.

**Mirror:**
- the overall layout and alignment;
- navigation order (in RTL, back points right);
- controls that show progress or value, such as sliders and progress bars, along with their end glyphs;
- icons that show text or reading direction;
- icons that show forward or backward motion;
- sequences whose order matters, such as ordered images, rating stars and numbered steps.

**Don't mirror:**
- the digits within a number (phone, card and order numbers);
- logos;
- universal marks such as the checkmark;
- photos and illustrations (if direction matters, make a new version);
- real-world objects such as clocks and right-handed tools;
- controls that point to an actual physical direction.

**Also:**
- A paragraph of three or more lines aligns to its own language, even inside an RTL interface.
- Keep alignment consistent across all items in a list.
- Arabic and Hebrew have no capital letters, so next to all-caps Latin text they may need a slightly larger size. Apple suggests about 2 pt.
- Strings that mix directions (brand names, URLs, numbers) need bidi isolation. That is an engineering dependency.

**Platform-specific:** platforms differ on media playback controls, timelines and chart time axes. Check the platform's guidance before mirroring them.

## 8. Contrast settings and theme resilience

How to design each theme, and the per-theme checklist, live in the typography-color reference §4. This section covers the user settings to test the design against:

- **Apple:** Increase Contrast and Reduce Transparency, on their own and together; Bold Text.
- **Android:** contrast levels (Android 14 and later) and font scale.
- **Web:** Windows contrast themes, which trigger CSS `forced-colors`. In forced-colors mode, backgrounds, shadows and background images can disappear:
  - boundaries that matter need real borders or outlines;
  - no information may live only in a background color;
  - icons should follow the text color.

## 9. WCAG 2.2 visual criteria

WCAG 2.2 is a W3C Recommendation, most recently published on 12 December 2024. Use only the rows that apply. A static design can show intent, but conformance needs the built product, so say "designed to address SC …" and never "compliant". Verifying the build belongs to delivery QA. Details: zoom and reflow in §4, targets in §5, contrast in the typography-color reference §3.

| SC | Level | What to check visually | A static design can't confirm |
|---|---|---|---|
| 1.3.1 Info and Relationships | A | structure shown visually (headings, groups, tables) is real structure, not just styling | programmatic markup |
| 1.3.2 Meaningful Sequence | A | visual order matches the meaningful reading order | source/DOM order |
| 1.3.3 Sensory Characteristics | A | instructions don't rely only on shape, color, size, location or sound |, |
| 1.3.4 Orientation | AA | layout works in portrait and landscape unless one orientation is essential | runtime lock |
| 1.4.1 Use of Color | A | color is never the only means of conveying information |, |
| 1.4.3 Contrast (Minimum) | AA | text at 4.5:1; large text at 3:1 | rendered colors |
| 1.4.4 Resize Text | AA | text at 200% without loss | real behavior |
| 1.4.5 Images of Text | AA | real text, not text baked into images |, |
| 1.4.10 Reflow | AA | works at 320 CSS px wide or 256 CSS px tall without 2D scrolling (2D content excepted) | real behavior |
| 1.4.11 Non-text Contrast | AA | 3:1 for the component boundaries that identify controls, state indicators and meaningful graphics | rendered colors |
| 1.4.12 Text Spacing | AA | no clipping or overlap when spacing is increased | real behavior |
| 1.4.13 Content on Hover or Focus | AA | content that appears on hover or focus can be dismissed without moving the pointer or focus (unless it reports an input error or covers nothing), can itself be hovered, and stays visible until dismissed, until the trigger is removed or until it's no longer valid | behavior (interaction) |
| 2.4.7 Focus Visible | AA | every focusable element has a visible focus style | keyboard behavior |
| 2.4.11 Focus Not Obscured (Minimum) | AA | sticky headers, banners and panels can't fully hide a focused element | scroll behavior |
| 2.4.13 Focus Appearance | AAA | indicator area at least a 2 CSS px perimeter; at least 3:1 change between focused and unfocused states | rendering |
| 2.5.8 Target Size (Minimum) | AA | at least 24×24 CSS px, or the spacing exception | real hit areas |
| 2.5.5 Target Size (Enhanced) | AAA | at least 44×44 CSS px | real hit areas |
| 3.2.4 Consistent Identification | AA | the same function has the same label and icon on every screen |, |
| 3.3.1 Error Identification | A | errors are identified and described in text, not by color or an icon alone | detection logic |
| 3.3.2 Labels or Instructions | A | visible labels or instructions wherever input is required |, |
| 1.4.6 Contrast (Enhanced), 1.4.8 Visual Presentation | AAA | 7:1 contrast; text blocks of at most 80 characters, not justified, with at least 1.5 line spacing. Use as quality targets when the target is AAA |, |

**Native apps.** W3C explains how WCAG applies outside the web in two informative documents:
- WCAG2ICT, a Group Note published 11 December 2025;
- WCAG2Mobile, a Group Draft Note published 6 May 2025.

Legal obligations depend on the jurisdiction (for example, EU accessibility requirements built on EN 301 549). Confirm the target with the product's accessibility or compliance owner. This skill gives design guidance, not legal advice.

## 10. Platform blocks

Use exactly one platform design language per platform build, and read only the block that matches.

### Web (default)
- Use the product's design system plus WCAG 2.2.
- No platform visual language is imposed. Don't bring Material or Apple styling into a web product unless the product chose it.

### Apple platforms
Applies to iOS, iPadOS, macOS, watchOS, tvOS and visionOS. Checked against the HIG on 2026-10-20.

**Liquid Glass and materials**
- The current design language is Liquid Glass, introduced in June 2025 and refined since.
- Liquid Glass is the functional layer: controls and navigation floating above content.
  - Don't use it in the content layer, e.g. on cards, backgrounds or lists. Sliders and toggles take it on only while they're active.
  - Use it sparingly on custom controls.
- Glass variants:
  - Regular: when legibility matters and for components with a lot of text.
  - Clear: only over rich media. Over bright content, add a dark dimming layer of about 35%.
- In the content layer, use the standard materials (ultra-thin, thin, regular, thick) with vibrant label colors. Avoid the quaternary label on thin and ultra-thin materials.

**Color**
- Prefer system and semantic colors, and give each color one meaning.
- Provide light, dark and increased-contrast variants.
- Never hard-code system color values or repurpose semantic colors.
- On Liquid Glass, use color sparingly:
  - tint the background of the primary action, not several controls;
  - keep bars monochrome over colorful content.

**Contrast**
- Apple's Accessibility Inspector uses three rows: 4.5:1 for text up to 17 pt, 3:1 for text from 18 pt, and 3:1 for bold text at any size.
- Two of those rows are looser than WCAG:
  - Bold text at any size: WCAG's large text starts at 14 pt bold, about 18.5 CSS px.
  - 18 pt and above: Apple points render at roughly CSS-pixel size, while WCAG's 18 pt is about 24 CSS px. This comparison is inferred, with medium-high confidence.
- When the accessibility target includes WCAG, use WCAG's thresholds.
- In Dark Mode, contrast must be at least 4.5:1. Aim for 7:1 with custom colors, especially for small text.

**Type**
- Use the system text styles with Dynamic Type. Default ("Large") sizes, in pt, as size/leading:

| Style | Size/leading |
|---|---|
| Large Title | 34/41 |
| Title 1 | 28/34 |
| Title 2 | 22/28 |
| Title 3 | 20/25 |
| Headline (semibold) | 17/22 |
| Body | 17/22 |
| Callout | 16/21 |
| Subhead | 15/20 |
| Footnote | 13/18 |
| Caption 1 | 12/16 |
| Caption 2 | 11/13 |

- Body text defaults to 17 pt; the minimum is 11 pt.
- Avoid the Ultralight, Thin and Light weights.
- Support text enlargement of at least 200% (140% on watchOS).
- Custom fonts must honor Dynamic Type and Bold Text.

**Layout**
- Respect safe areas, margins and layout guides.
- Adapt by size class (compact or regular), not by device model.
- At large Dynamic Type sizes, stack side-by-side content and let rows grow.
- Test the smallest and largest layouts.
- The HIG now covers the folding iPhone ("Designing for iPhone Duo", September 2026). Check it when that device is in scope.

**Targets**
- Buttons need a hit region of at least 44×44 pt (60×60 pt on visionOS).
- Default control sizes: 44 pt on iOS and iPadOS, 28 pt on macOS, 66 pt on tvOS, 44 pt on watchOS.
- Leave about 12 pt of padding around controls with a bezel, and about 24 pt around those without.

**Buttons**
- Use the prominent style for the most likely action, at most one or two per view.
- Distinguish options by style, not size.
- Never give a destructive action the primary role.
- Every custom button needs a pressed state.

**Dark Mode**
- Base backgrounds are dimmer; elevated backgrounds are brighter.
- Apple advises against an app-specific appearance setting.

**Icons**
- Use SF Symbols, matched to the weight of adjacent text.
- Keep custom icons consistent in size, detail and stroke.

**When a detail is missing here**, fetch the single relevant HIG page. HIG pages are rendered with JavaScript, but adding `.md` to a HIG page URL returns Apple's Markdown version.

### Android and Material-based products
Material 3, checked on 2026-10-20 through developer.android.com and official token sources (m3.material.io pages couldn't be read by machine).

**Layout: window size classes**
- Classes follow the window, not the device, and can change while the app runs.
- Width: compact under 600 dp; medium 600–839 dp; expanded 840–1199 dp; large 1200–1599 dp; extra-large 1600 dp and up.
- Height: compact under 480 dp; medium 480–899 dp; expanded 900 dp and up.
- A phone in landscape usually has a compact height.

**Accessibility**
- Targets are 48×48 dp, and the target may extend beyond the visible element.
- Text contrast 4.5:1, non-text 3:1.
- Body text is at least 12 sp, and text sizes are set in sp.
- Android 14 and later scales fonts up to 200%, nonlinearly. It also offers user contrast levels.

**Color roles**
- primary, secondary, tertiary and error, each with on-, container and on-container pairs;
- fixed accent roles;
- surface plus surface-container levels, from lowest to highest;
- outline and outline-variant;
- inverse roles.
- Always pair an on-color with its matching container.

**Elevation**
- Elevation is mainly expressed through tone rather than shadow. In dark themes, the surface-container levels carry it.

**Type roles**
- Display, headline, title, body and label, each in large, medium and small.
- Material 3 Expressive adds emphasized styles.

**State layers** (Compose tokens): hover 8%, focus 10%, pressed 10%, dragged 16%.

**Material 3 Expressive** (announced May 2025): confirm the product has adopted it before applying its styles.

### Enterprise and data-dense UI exemplars
Carbon and Fluent 2 are benchmarks for problems they have already solved: density, data tables, layering and productive type. They are not styles to copy. Consult only one, unless a comparison is the point.

**Carbon**
- Productive type (14 px base) for task UI; expressive type (16 px base) for editorial moments.
- A layering model for surfaces.
- Condensed (1 px) gutters for related dashboard tiles.
- The 2x Grid breakpoints are 320, 672, 1056, 1312 and 1584 px, with 4, 8, 16, 16 and 16 columns.
- Table row sizes are listed in the density section of the hierarchy reference.

**Fluent 2**
- Brand color goes on actions and selected states, not large surfaces.
- Semantic colors are never decorative.
- Shadows combine key and ambient layers by elevation.
- Spacing uses a 4 px base.
- Size classes begin at 320, 480, 640, 1024, 1366 and 1920 px.
- Minimum targets are 44×44 on web and iOS, 48×48 on Android.

**When the product is in the system's own ecosystem**
- Windows apps and Teams or Office add-ins: Fluent becomes platform guidance.
- IBM products: Carbon is product truth.

## 11. Cross-platform consistency

**Keep the same on every platform:**
- brand;
- information hierarchy;
- content;
- the meaning of colors and icons;
- what each state means.

**Adapt per platform:**
- the system type ramp;
- control styling;
- how navigation is presented (an IA/interaction decision);
- target sizes;
- materials and elevation;
- the icon set, e.g. SF Symbols on Apple, Material Symbols or the product's own set elsewhere.

**Never mix two platform design languages within one platform build.**
