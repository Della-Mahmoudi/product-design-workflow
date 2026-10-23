# Hierarchy, Layout and Density

This reference covers how to make importance, grouping and sequence visible at screen level. It is about applying the product's own spacing, grid and component primitives, not defining them; defining them is design-system work (Skill 05).

## Contents
1. Diagnose hierarchy before styling
2. Hierarchy levers
3. Grouping: proximity, similarity, region, alignment
4. Flat or fragmented? Detection and repair
5. Composition and scan order
6. Grid and alignment
7. Spacing with tokens
8. Density
9. Surface hierarchy
10. Pattern playbook: tables, lists, cards, forms, dashboards, settings, reading layouts
11. Empty, loading, error and success presentation

## 1. Diagnose hierarchy before styling

1. **Name the job.** In one sentence, say what this screen or region must let the user know or do first. Then list its top 3–5 elements in intended priority, taken from the approved structure and real content. If no priority was given, infer one and mark it `[ASSUMPTION]`.
2. **Read what actually dominates.** Use one of these checks and record the perceived first, second and third:
   - Blur the screen, or squint, until text is unreadable.
   - View it in grayscale.
   - Ask what someone notices first, second and third.
3. **Compare the two orders.** Every mismatch is a hierarchy defect. If several items are tied for "most important", that is a priority decision, not a styling problem, so escalate it.
4. **Fix with the cheapest lever first**, in this order:
   1. Remove or demote competing elements (subtracting usually beats adding).
   2. Change position or order.
   3. Change spacing and grouping.
   4. Change size and weight.
   5. Change contrast and color.
   6. Change surface treatment: fills, borders, elevation.
5. **Check again.** Repeat step 2. Then confirm the emphasis still works in grayscale and that de-emphasized text still meets contrast minimums.
6. **Apply the escalation test.** If the fix needs content added, removed or re-prioritized, a different control, or a different destination, it belongs to IA, interaction or content. Write `[DEPENDENCY: …]` and stop styling that part.

## 2. Hierarchy levers

| Lever | Best at communicating | Symptom of overuse |
|---|---|---|
| Position and order | what comes first; sequence | key item buried at the bottom or the end |
| Size | rank between levels | inflated headings shouting at each other |
| Weight | emphasis within one size | bold everywhere, so nothing stands out |
| Spacing and proximity | grouping and separation | uniform gaps that hide what belongs together |
| Alignment | relationship and order | many ragged start edges that look disorganized |
| Luminance contrast | emphasis and de-emphasis | "secondary" text faded below contrast minimums |
| Hue | category, status, brand accent | rainbow UI; status colors used as decoration |
| Surface (fill, border, elevation) | regions and layering | boxes inside boxes |
| Shape | affordance and identity | static elements that look tappable |
| Icons and imagery | recognition and scanning | decorative icons competing with labels |

**Rules of use:**
- Combine two or three levers for each hierarchy level, e.g. position plus size plus weight. A single lever is fragile, and color alone is the most fragile.
- Make adjacent levels clearly different. Treatments that are almost the same look like mistakes, not hierarchy.
- Budget emphasis. Each region gets one primary focal point and at most one primary action.
- Give each recurring level one treatment and use it everywhere in the product.
- To make a small but critical item findable (a status, a deadline, an error count), give it a prime position, whitespace around it and strong contrast. Don't make it bigger.

## 3. Grouping: proximity, similarity, region, alignment

**Proximity**
- Space inside a group must be clearly smaller than space between groups. If the two differ by only one small step of the spacing scale, the grouping may not read, so use a bigger jump.
- A label sits closer to its own field or value than to the next item.
- A heading sits closer to the content it introduces than to the content above it.

**Similarity**
- Peers share one treatment: size, color, shape and alignment.
- To mark one peer as special, change one attribute, not three.

**Common region**
- A background tint, border or card says "these belong together".
- Use one only when spacing alone can't carry the group:
  - the group has its own actions or identity;
  - content scrolls beneath it;
  - it must stand apart from a busy area.
- Otherwise use spacing and headings.

**Alignment and continuity**
- Items that share an edge read as related, so align only things that belong together.
- An accidental shared edge suggests a relationship that doesn't exist.

## 4. Flat or fragmented? Detection and repair

**Flat**
- Symptoms:
  - one text size and weight carries several levels;
  - every gap is the same;
  - there's no obvious first read;
  - primary and secondary actions look alike.
- Repair:
  - define 3–4 levels with the design system's type roles;
  - regroup with spacing;
  - promote one primary;
  - demote metadata.

**Fragmented**
- Symptoms:
  - cards inside cards;
  - borders, fills and shadows on the same region;
  - a divider between every item;
  - three or more surface levels;
  - several accent colors;
  - icons on every label.
- Repair:
  - remove containers and let spacing do the grouping;
  - keep one surface level per region;
  - use dividers only in dense lists and tables;
  - keep one accent;
  - use icons only where they help recognition.

Both problems can appear on one screen, such as a flat header above a fragmented body. Fix the hierarchy before tuning details.

## 5. Composition and scan order

- People scan before they read, so design for the first scan. What lands first should be what the task needs first.
- Plan a few ranked focal points joined by an implied path. Each region gets one dominant focal point and, at most, a clearly weaker second one.
- Put the primary action where the eye arrives after reading the content that supports it, usually at the end of the form or section, or in the platform's standard location. Don't strand it at a far edge.
- Keep controls that act on the same object next to that object.
- Reading-pattern heuristics such as F and Z describe tendencies, not rules. Start-edge emphasis assumes left-to-right reading, so mirror it for RTL.
- Visual order must match the meaningful order of the content, which is the order assistive technology follows. If they differ, flag `[DEPENDENCY: Engineering]` for source order.
- Give the main content most of the screen. Keep repeated chrome (headers, toolbars, banners) lean, because stacked bands push the task below the first view.

## 6. Grid and alignment

- Use the product's grid, breakpoints and layout tokens.
  - If none exist, derive a `[PROVISIONAL]` grid. Make margins and gutters multiples of the spacing base unit.
  - Increase the column count as width grows; 4, 8 and 12 columns are common.
- Count the distinct start edges. Fewer alignment lines make a calmer screen, and each extra edge needs a reason.
- Align label and value columns.
- In tables, end-align numbers (right-align in LTR) and use tabular figures.
- Recurring elements keep the same size and position on every screen. Decide frame elements (margins, header, title style, label-to-control gaps) once and share them; don't re-decide them per screen.
- Cap the width of reading content (see the typography reference). Data-dense regions can use the full width.
- If real content keeps fighting the grid, revise the grid instead of forcing the content.

## 7. Spacing with tokens

- Map every gap to a spacing token by role:
  - inside a component;
  - between related items;
  - between groups;
  - between sections.
- Write each gap as `token (value)`.
- If the scale lacks a value you need, try the neighboring steps first. If neither works, record the need as a `[DS GAP]` (e.g. "no step between 16 and 24 for compact card padding") and use the nearest token. A missing step is a signal, not permission to invent one.
- Keep a consistent rhythm: section spacing is larger than group spacing, which is larger than item spacing, which is larger than internal padding. Apply it the same way on every screen.
- Don't express hierarchy with one-off spacing values. If a screen needs special spacing, record it as a `[LOCAL EXCEPTION]` with the reason.

## 8. Density

Density is a product decision about who uses the screen, how often and for what. It is not a styling preference.

**When to go denser or lighter**
- Higher density suits frequent, expert, comparison-heavy or monitoring work on pointer devices.
- Lower density suits occasional users, touch input, anxious or high-stakes tasks, and first-run experiences.

**Use the system's density options**
- Prefer the design system's density modes, such as compact and comfortable component sizes or table row sizes.
- Carbon is a useful benchmark: its data-table rows come in 24, 32, 40, 48 and 64 px, and it recommends 64 px only when rows hold two lines of content.

**How to increase density**, in this order:
1. Remove decorative whitespace and chrome.
2. Tighten internal padding.
3. Reduce row height.
4. Condense secondary metadata.
5. Add columns.
6. Reduce type size last, and never below design-system or platform minimums.

**Limits density never crosses:**
- text contrast;
- minimum text sizes;
- target size for the input method;
- visible focus;
- perceivable grouping.

**Dense is not cramped**
- Keep the rhythm consistent and rely on alignment.
- In wide tables, use zebra striping or hairline dividers to help eyes track rows.

**Mixed input**
- If one product serves both touch and pointer, use the design system's density rules for each input mode. If it has none, record a `[DS GAP]` rather than inventing density modes screen by screen.

## 9. Surface hierarchy

- Keep to about three surface levels per screen:
  - base: the page background;
  - container: sections, panels, cards;
  - overlay: menus, popovers, dialogs, sheets.
- Deeper nesting is a sign of fragmentation.
- Express levels with the design system's surface or layer tokens.
  - Light themes usually separate levels with subtle fills, borders or shadows.
  - Dark themes usually show higher layers as lighter surfaces, because shadows fade on dark backgrounds.
  - Use theme tokens; never invert values.
- Use a card when the item is a self-contained object with its own identity or actions, or when the peers are of different kinds.
- Don't use cards just to separate sections; headings and spacing do that.
- A tinted background block can lift one key region. Used everywhere, it becomes noise.

## 10. Pattern playbook

### Tables

**Alignment**
- Start-align text columns.
- End-align numeric columns, with tabular figures and consistent decimals.
- Put units in the column header rather than repeating them in every cell.

**Header**
- Make the header visibly distinct from rows (weight or fill) but quieter than the page title.
- Match header height to the row density.

**Rows**
- In wide tables, help eyes track rows with zebra striping or row dividers, not both at full strength.

**Truncation**
- Truncate low-priority text only.
- Never truncate numbers or identifiers that users compare.
- Wrap headers to two lines before truncating them.
- How users reach the full value is an interaction dependency.

**State cues: more than color**
- Selection: a checkbox or indicator plus a fill.
- Sort: an icon for direction.
- Status: icon, text and color together.

**Empty cells**
- Use one consistent placeholder.
- If a blank could mean zero, unknown or not applicable, flag `[DEPENDENCY: Content]`.

**Narrow widths:** choose by task.
- For comparison, keep the table, with horizontal scrolling and a frozen identifying column. Data tables qualify for the two-dimensional exception to reflow.
- For lookup, turn rows into list items.

### Lists

- Use one row anatomy throughout: optional leading visual, primary text, secondary text, metadata, then a trailing value, action or chevron.
- Match row richness to the task. Names alone suit lookup; previews and thumbnails suit browsing.
- Separate rows of the same kind with spacing or hairlines, not cards.
- Thumbnails share one size and aspect ratio, are cropped to the subject, and sit on the leading side.
- A selected row changes more than its hue, e.g. a fill plus an indicator or a weight change.

### Cards and grids of peers

- Use one template and give every peer equal visual weight. Highlight a peer with a badge or color treatment, never by making it bigger or moving it.
- Set rules for real content and mock up both extremes:
  - line clamp for titles;
  - image ratio and crop;
  - fallback for a missing image;
  - longest and shortest text.
- Make the clickable area obvious. If one card holds several competing actions, flag it as an interaction question.

### Forms

**Layout and labels**
- Default to a single column with labels above fields. This holds up under translation, zoom and narrow widths.
- Every field keeps a visible label. Placeholder text is only a hint, and it still needs text contrast.
- Keep label-to-field spacing smaller than field-to-field spacing.
- Group related fields under section headings, with larger spacing between groups. Don't use tabs to split a form into sections.
- Make field width hint at the expected answer length.

**Required fields and help text**
- Use one required/optional convention across the product. Explain it on the form, and never mark it with color alone.
- Put helper text under or beside its field. It's smaller than the label but keeps full text contrast.
- Reserve or allow space so messages don't overlap neighboring fields.

**Errors**
- Show a text message next to the field, plus an icon and a change in the field's state. Color reinforces the error; it never carries it alone.
- On long forms, add an error summary at the top.
- When validation fires is interaction design.

**Controls and actions**
- Field boundaries must be perceivable. When a border or fill is what identifies the control, it needs 3:1 against adjacent colors.
- Use one prominent submit action at the end of the form or in the platform's standard spot.
- Keep secondary actions quieter, and never style a destructive action as the primary one.
- Read-only values stay fully legible and selectable; disabled controls are dimmed.
- Don't rely on a disabled submit button alone to explain what's missing. Flag it for interaction and content.

### Dashboards

- Start from the decisions the dashboard supports; that's a content/IA dependency.
- Put the most decision-critical metrics at the top start, with the strongest emphasis and the most space.
- Show few metrics, and group them by the question they answer.
- Use one tile anatomy for every tile:
  1. label;
  2. value, set largest;
  3. change indicator: a sign or arrow plus text, with color only reinforcing;
  4. context, e.g. period or comparison.
- Chart visuals:
  - give each data series one color across every chart;
  - use the design system's data-visualization palette;
  - never use status colors for categories;
  - prefer simple forms (lines, bars) to gauges, dials and 3D.
- Choosing the chart type is a data-visualization decision.
- Avoid a wall of separate cards. Related tiles can share one surface, separated by dividers or tight gutters.
- Make the active scope (date range, filters) visible near the title. Where those controls live is an IA/interaction decision.

### Settings screens

- Show each setting's current value at a glance.
- Organize settings into titled groups with one row anatomy: label, optional description, then the control or value. Align controls on the trailing edge.
- Visually separate destructive and account-level actions from routine settings.
- Group order and naming are IA; the visual layer makes the groups legible.

### Reading and content-heavy layouts

- Cap line length and keep paragraph spacing generous and consistent.
- Use frequent headings with distinct levels, each sitting closer to its own section.
- For measure and leading, see the typography reference.

## 11. Empty, loading, error and success presentation

This section covers how these states look. Whether a state exists, when it appears, how long it lasts and what happens next come from the interaction spec, product behavior, platform convention or the component's contract. If one you need is missing, flag `[DEPENDENCY: Interaction]` instead of inventing it.

**Keep the frame.** A state fills the region the content would occupy, so the page doesn't collapse or jump.

**Empty**
- Show an explanation and one next step. The wording is a content dependency and the action is an interaction dependency.
- Add a small illustration if it helps.
- Make "nothing yet", "no results" and "error" look different and say different things.

**Loading**
- Show whatever has already loaded.
- Use skeletons that match the final dimensions, so the layout doesn't shift.
- Show progress in place: inside the region, or in the button that started it.
- Use determinate progress for long tasks of known length and indeterminate indicators for short or unknown waits. Design systems name these differently, so state which one you mean.

**Error**
- Match visual weight to severity: an inline field message is lighter than a section alert, which is lighter than a blocking page state.
- Always combine an icon, text and color.
- Keep the user's content visible.

**Success**
- Keep it proportionate, and quiet in productivity contexts. How long it stays is interaction design.
