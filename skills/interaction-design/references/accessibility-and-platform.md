# Accessibility and platform behavior

Load for keyboard and focus behavior, screen-reader names, states and announcements, custom widgets, pointer, touch and gesture behavior, platform-specific conventions, design-system reuse, the Carbon and GOV.UK exemplars, and AI-powered interactions. Read only the section the request needs.

Sections: 1 Ground rules · 2 Keyboard · 3 Focus management · 4 Names, roles, states · 5 Announcements · 6 WCAG 2.2 quick reference · 7 APG pattern router · 8 Pointer, touch, gestures · 9 Platform conventions · 10 Design-system reuse · 11 Carbon and GOV.UK (conditional) · 12 AI-powered interactions (conditional)

## 1 Ground rules

- **Native elements and platform controls first.** They bring keyboard support, focus handling and semantics that a custom widget has to rebuild. Standard HTML controls used as specified already meet Name, Role, Value. (WCAG 4.1.2, Understanding document) When a native element does the job, specify it and stop: no ARIA or APG behavior on top.
- **ARIA only changes what assistive technology is told.** Every role you add commits you to the matching keyboard behavior, focus handling and state updates.
- **APG patterns are design references.** They describe expected keyboard behavior, roles and states; their example pages summarize assistive-technology support where it is known, and that support varies. Treat them as guidance rather than a conformance guarantee, and call for testing with real assistive technology. (APG About)
- **Write what users can do and perceive.** Never state that a design "is WCAG compliant" or "has been tested"; name the success criteria the behavior is designed to support and what remains to verify.
- **Default target**: WCAG 2.2 Level AA for web unless the product says otherwise `[assumption]`. For native apps use the platform's guidance and accessibility APIs; W3C's WCAG2Mobile (Group Draft Note, May 2025) explains how WCAG 2.2 A and AA apply to app screens. It is informative, not normative.

## 2 Keyboard (web)

- All functionality works from the keyboard without timing-dependent keystrokes, and focus can always leave a component. (WCAG 2.1.1, 2.1.2)
- **Tab and Shift+Tab move between components; arrow keys move within a composite** (menu, listbox, tabs, grid, radio group, toolbar), and each composite takes one tab stop. (APG Developing a Keyboard Interface)
- **Composite focus**: roving tabindex moves real focus between items and the browser scrolls them into view; `aria-activedescendant` keeps DOM focus on the container or input, so you must draw the focus indicator and scroll the active item. Comboboxes keep DOM focus in the input this way. (APG Developing a Keyboard Interface; APG Combobox)
- **Focus is not selection.** Selection may follow focus only when the change is instant (no network request); otherwise select with Enter or Space. In multi-select widgets, arrows move focus without changing the selection. (APG Developing a Keyboard Interface)
- **Activation keys**: Enter or Space activates a button; Space toggles a checkbox or switch (Enter is optional on a switch); Escape closes popups and dialogs; Home and End are strongly recommended in lists longer than five options; type-ahead is recommended in listboxes, especially beyond seven options. In an editable combobox, Home and End may instead return to the input and move the text cursor. (APG Button, Switch, Listbox, Combobox)
- **Disabled but discoverable**: menu items, listbox options, tabs and toolbar buttons can stay focusable with `aria-disabled` so people learn they exist. (APG Developing a Keyboard Interface)
- **Shortcuts supplement navigation and never replace it.** Avoid conflicts with operating-system, browser and screen-reader keys. Single-character shortcuts must be switchable off, remappable, or active only while the component has focus. (APG Developing a Keyboard Interface; WCAG 2.1.4)

## 3 Focus management

Specify each moment that applies:

| Moment | Focus rule |
|---|---|
| A modal dialog opens | Focus moves into it: to the first focusable element by default; to a static element at the top (title or first paragraph) when the content is long or structured; to the least destructive action in an irreversible confirmation; to the most-used button in a purely informational dialog. Tab cycles inside, Escape closes, and a visible close or Cancel control is present. (APG Dialog (Modal)) |
| A typed-confirmation dialog opens (type the name to delete) | To the confirmation field: the destructive button stays unavailable until the text matches, so typing can't trigger it. Without such a guard, use the least destructive control. (Synthesis of APG Dialog (Modal) and Carbon Modal "Focus") |
| A dialog closes | Back to the control that opened it; if that no longer exists, to the next logical place, such as the item that replaced it or the list. (APG Dialog (Modal), Button) |
| An item in a list is removed | To the next item itself (the previous one if it was last), not to that item's own remove or cancel control, so a repeated key press can't remove a second item. If the list is now empty or disappears, to the list's heading or the control that owns it (for example the input of a multiselect). Never to the page body. (APG Developing a Keyboard Interface) |
| The focused control disappears because the state changed (Cancel becomes Remove when an upload finishes) | To the control that replaced it in the same item, or to the item itself, and announce the new state. Never let focus fall to the page body. (APG Developing a Keyboard Interface) |
| Content updates (results load, an item is added, status changes) | Don't move focus; announce instead (§5). Move focus only when the user's action starts a new context, such as the next wizard step or an opened dialog. (WCAG 3.2.1, 3.2.2, 4.1.3; APG Button) |
| A submit fails validation | To the error summary on multi-field forms; to the first invalid field on very short ones. (GOV.UK Error summary) |
| A popup (menu, listbox) closes | Back to its button or input. (APG Combobox, Menu Button) |
| A page loads | Don't set initial focus unless the page has one primary task most users need right away. (APG Developing a Keyboard Interface) |
| A confirmation step on its own page (review, then delete) | Focus starts at the page heading, or at the error summary after a failed attempt. Never auto-focus the destructive control; in focus order it comes after the consequences and any typed confirmation field. (Synthesis of APG Developing a Keyboard Interface and GOV.UK Error summary) |

- Focus stays visible and isn't hidden behind sticky headers, cookie bars or toasts (WCAG 2.4.7, 2.4.11); focus order follows meaning (2.4.3); focus indicators and control states have at least 3:1 contrast (1.4.11; 2.4.13 at AAA sets a stronger indicator).
- Single-page app view changes: move focus to the new view's main heading or announce the new title. This is common practice that the checked sources don't cover; confirm the product's routing approach.

## 4 Names, roles, states

- The accessible name contains the visible label (WCAG 2.5.3). Icon-only controls need a name; repeated controls need distinguishing names ("Remove invoice.pdf", not five identical "Remove" buttons).
- **Expose state, don't just draw it**: `aria-pressed` for a toggle button; `aria-checked` for a checkbox or switch; `aria-expanded` for a disclosure, menu button or combobox; `aria-selected` or `aria-checked` for options, used consistently within a widget (APG recommends `aria-checked` for multi-select listboxes); `aria-describedby` to tie an error or hint to its field, with `aria-invalid` on the field; `aria-disabled` when a disabled control should stay discoverable. The labels of toggle buttons and switches don't change with their state. (APG Button, Switch, Listbox, Combobox; GOV.UK Error message; WCAG 4.1.2)
- Structure and relationships are programmatic: labels tied to fields, groups with legends (WCAG 1.3.1, 3.3.2). Personal-data fields identify their purpose for autofill (WCAG 1.3.5).
- **Respect what a role may contain.** A listbox holds only options and groups, so "Loading", "No results", error text and buttons such as Retry go outside it, in a status region next to it. (APG Listbox; WAI-ARIA owned-element rules)

## 5 Announcements

- **Status messages** (results, success, waiting, progress, and errors that don't take focus) must be exposed programmatically so assistive technology announces them without moving focus. (WCAG 4.1.3)
  - `role="status"` (polite) for results, counts, success and "Saving…"; `role="alert"` for important, time-sensitive problems; `role="log"` for sequential updates; progress through a live region or status. (WCAG 4.1.3 Understanding document: techniques ARIA22, ARIA19, ARIA23, ARIA25)
  - WCAG requires the outcome (the message is exposed without moving focus); these roles are documented ways to achieve it, not the only ones.
  - An error shown in a dialog that takes focus is announced by the focus move and is not a status message. Expanding menus, accordions or tabs is a state change (4.1.2), not a status message.
- Practice that the checked sources don't spell out: the live region must exist before its content changes. Announce when a long operation starts, at sparse milestones if it runs long, and the final outcome once ("17 uploaded, 3 failed"); never every item or percentage. Keep routine updates polite.

## 6 WCAG 2.2 quick reference

Interaction-relevant success criteria, checked against W3C documents on 2026-10-20. Paraphrases only; read the normative text before relying on an exception.

| SC | Level | What it means for behavior |
|---|---|---|
| 1.3.1 Info and Relationships | A | Structure and relationships are available programmatically |
| 1.3.5 Identify Input Purpose | AA | Personal-data fields expose their purpose (autofill) |
| 1.4.1 Use of Color | A | Color is never the only signal of state, action or error |
| 1.4.11 Non-text Contrast | AA | Control boundaries, states and focus indicators reach 3:1 |
| 1.4.13 Content on Hover or Focus | AA | Hover and focus popups are dismissible, hoverable and persistent |
| 2.1.1 Keyboard | A | All functionality works from the keyboard |
| 2.1.2 No Keyboard Trap | A | Focus can always leave by keyboard |
| 2.1.4 Character Key Shortcuts | A | Single-key shortcuts can be turned off, remapped, or limited to focus |
| 2.2.1 Timing Adjustable | A | Time limits can be turned off, adjusted or extended (warning, at least 20 s) |
| 2.2.5 Re-authenticating | AAA | No data loss after logging back in |
| 2.2.6 Timeouts | AAA | Warn about inactivity timeouts that lose data |
| 2.3.3 Animation from Interactions | AAA | Motion triggered by interaction can be turned off |
| 2.4.3 Focus Order | A | Focus order preserves meaning and operability |
| 2.4.6 Headings and Labels | AA | Labels describe purpose |
| 2.4.7 Focus Visible | AA | Keyboard focus is visible |
| 2.4.11 Focus Not Obscured (Minimum) | AA | The focused item isn't entirely hidden by author content |
| 2.5.1 Pointer Gestures | A | Multipoint and path gestures have a single-pointer alternative |
| 2.5.2 Pointer Cancellation | A | Activation on release, with a way to abort or undo |
| 2.5.3 Label in Name | A | The accessible name contains the visible label |
| 2.5.4 Motion Actuation | A | Shake or tilt actions have a UI alternative and can be turned off |
| 2.5.7 Dragging Movements | AA | Dragging has a single-pointer alternative without dragging |
| 2.5.8 Target Size (Minimum) | AA | Targets at least 24 × 24 CSS px, or spaced enough (exceptions: equivalent control, inline, user agent, essential) |
| 3.2.1 On Focus | A | Focus alone never changes context |
| 3.2.2 On Input | A | Changing a setting doesn't change context unless the user was told |
| 3.2.6 Consistent Help | A | Repeated help mechanisms keep the same relative order |
| 3.3.1 Error Identification | A | Detected errors are identified and described in text |
| 3.3.2 Labels or Instructions | A | Inputs have labels or instructions |
| 3.3.3 Error Suggestion | AA | Known corrections are suggested unless that compromises security or purpose |
| 3.3.4 Error Prevention (Legal, Financial, Data) | AA | Such submissions are reversible, checked, or confirmed |
| 3.3.7 Redundant Entry | A | Information already entered in a process is prefilled or selectable |
| 3.3.8 Accessible Authentication (Minimum) | AA | No cognitive-function test without an alternative or assistance (paste, password managers) |
| 4.1.2 Name, Role, Value | A | Name, role and state are exposed, and changes are notified |
| 4.1.3 Status Messages | AA | Status messages are announced without moving focus |

4.1.1 Parsing is obsolete and removed in WCAG 2.2.

## 7 APG pattern router

For custom web widgets only, when no native element does the job. Open only the pattern page you need: https://www.w3.org/WAI/ARIA/apg/patterns/

| Need | APG pattern | Carry into the spec |
|---|---|---|
| An action | Button | Enter and Space; an opened dialog takes focus; an Apply-type button keeps it |
| An on/off state in a toolbar | Button (toggle, `aria-pressed`) | The label stays constant; state lives in `aria-pressed` |
| An immediate on/off setting | Switch | Space toggles (Enter optional); `aria-checked`; the label stays constant |
| One of a few options | Radio Group | Arrows move and select; one tab stop |
| Choosing from a list by typing | Combobox | DOM focus stays in the input with `aria-activedescendant`; Down opens; Escape closes; the autocomplete mode is declared |
| One or many from a visible list | Listbox | For multiple: Space toggles, `aria-multiselectable`, and `aria-selected` or `aria-checked` used consistently |
| A command menu from a button | Menu Button with Menu | Enter, Space or Down opens and focuses the first item; for application actions rather than ordinary site links |
| A modal task or a confirmation | Dialog (Modal); Alert and Message Dialogs | Focus rules in §3; `alertdialog` for urgent confirmations |
| Show and hide | Disclosure; Accordion | `aria-expanded` |
| Views in place | Tabs | Arrows between tabs; selection may follow focus when panels render instantly |
| Grouped controls | Toolbar | One tab stop, arrows inside |
| Interactive tabular data | Grid; Treegrid | Cell-level navigation |
| Hierarchies | Tree View | Arrows expand and collapse |
| Transient help | Tooltip | Appears on keyboard focus as well as hover and can be dismissed (WCAG 1.4.13) |
| Ranges and numbers | Slider; Spinbutton | Arrow, Page, Home and End keys |
| **Searchable multi-select** | **No APG pattern**: APG Combobox is single-select | Compose an editable Combobox with a multi-select Listbox popup (`aria-multiselectable`, with `aria-checked` as APG recommends for multi-select; cite both patterns). DOM focus stays in the input, so Space types a character: toggle the active option with Enter and keep the popup open for more choices. Escape closes the popup and keeps the selections. `aria-controls` needs to be set only while the popup is visible. Loading, no-results and error messages sit outside the listbox; any Retry button sits outside the popup altogether (for example below the input), because APG keeps popup content out of the Tab sequence. Show selections outside the popup as removable items with distinguishing names. Test with assistive technology. When the option set is small, prefer a native checkbox group. |

## 8 Pointer, touch, gestures

- **Target size**: web AA is at least 24 × 24 CSS px or sufficient spacing (WCAG 2.5.8); 44 × 44 is AAA (2.5.5). Apple: default 44 × 44 pt, minimum 28 × 28 pt on iOS and iPadOS, with about 12 pt of padding around bezeled elements (HIG Accessibility, checked 2026-10-20). Android and Material: 48 × 48 dp (DI Ch 6 "Touch Screens"; m3.material.io could not be checked).
- **Activate on release**; moving off before release cancels. (WCAG 2.5.2; AF CH18 "Mouse-up and mouse-down events")
- **Every gesture-only, drag-only or motion-only action needs a visible single-pointer alternative**: swipe-to-delete also gets a Delete button or an edit mode; drag-to-reorder also gets "Move up", "Move down" or "Move to". (WCAG 2.5.1, 2.5.4, 2.5.7; Apple Accessibility "Offer alternatives to gestures")
- **A file drop zone** always comes with a native file input or a button that opens the file picker. (WCAG 2.5.7)
- **There is no hover on touch**: never hide essential actions or information behind hover, and make hover or focus content dismissible, hoverable and persistent. (DMMT Ch 10 "No cursor = no hover = no clue"; WCAG 1.4.13)
- **Long-press and multi-finger gestures are hard to discover**: back them with a visible control. (AF CH19 "Multi-Touch Gestures")
- **Keep standard platform gestures** (back swipe; shake or three-finger swipe to undo on iPhone) and don't redefine them. (Apple Undo and redo)

## 9 Platform conventions

Load only the block that matches the product. Web products use §1–7 (WCAG, native semantics, APG when needed). A product with its own documented design system follows it first (Tier 0); Carbon or GOV.UK serve only as exemplars where it is silent (§11).

**Apple (iOS, iPadOS, macOS; HIG checked 2026-10-20)**
- Alerts sparingly, only for critical and actionable information: not purely informational, not for common undoable actions, not at launch. (Alerts)
- On iOS, choices about an intentional action (discard or save a draft) go in an action sheet, not an alert. (Alerts)
- Alert buttons: short verbs; a cancelling button is always titled "Cancel"; "OK" only in informational alerts; destructive style only when the destruction wasn't what the person deliberately chose; Cancel is never the default; leaving out a default encourages reading; Escape or Command-Period cancels. (Alerts)
- Modality only with a clear benefit; short, simple tasks; an obvious way to dismiss; confirmation before a dismissal that would lose user content; no stacked modal views and never more than one alert. (Modality)
- Undo: help people predict the result and show it; support multiple levels; macOS Edit menu with Command-Z and Shift-Command-Z; on iPhone, shake or three-finger swipe, described briefly ("Undo Address Change"). (Undo and redo)
- Toggles: on iOS a switch only in list rows, elsewhere a button that behaves like a toggle; on macOS checkboxes for hierarchies of settings and switches for emphasized or group settings; state never by color alone. (Toggles)
- Feedback and loading: integrate status near the items it describes; warn only about unexpected, irreversible data loss; show content as soon as possible with placeholders; determinate or indeterminate progress as appropriate. (Feedback, Loading)
- Accessibility: VoiceOver labels, Dynamic Type, Reduce Motion, Full Keyboard Access, Switch Control and Voice Control support; few time-boxed elements; alternatives to gestures; in Assistive Access, confirm twice before actions that are hard to recover from. (Accessibility)

**Material and Android**
- Apply only when the product uses Material. m3.material.io renders only with JavaScript and could not be checked while building this skill, so open the specific component page (snackbar, dialog, progress indicator, chips, menus) before asserting a Material-specific rule. Unverified conventions: snackbars carry brief, non-critical messages with at most one action such as Undo, and dialogs are for decisions that must interrupt. Touch targets of 48 × 48 dp are corroborated by DI Ch 6.

**Desktop applications**
- Menus list commands with their shortcuts, disabled items stay visible but inactive, keyboard and mouse have parity, and icon-only controls have tooltips (which must also appear on focus). (AF CH18 "Menus", "Toolbars, Palettes, and Sidebars") Some of AF's idioms are Windows-era; follow the current operating-system guidelines where they differ.

## 10 Design-system reuse

- **Inventory first**: the product's components and their documented behavior (states, keyboard, events, copy rules). Reuse whole components with their documented behavior. (DI Ch 11 "Atomic Design: A Way of Designing Systems")
- **This skill specifies behavior; `design-systems-consistency` decides the system.** Whether an existing component already supports a behavior; whether to extend it, add a variant or build a new component; and its properties, API, tokens, contribution and versioning are Skill 05's decisions.
- **When the system lacks a behavior**, specify the behavior the interaction needs (keyboard, focus, selection, loading, empty, error) as a proposed addition and flag it as a design-system dependency `[confirm: design system]` rather than inventing a one-off or designing the component.
- **Follow the product's conventions** unless a clearly superior alternative exists; then propose it as a product-wide change for the design system's owners rather than changing one screen. (AF CH17 "Obey standards unless there is a truly superior alternative"; DOET Ch 4 "Conventions, Constraints, and Affordances"; DMMT Ch 3 "Conventions are your friends")
- **An existing component that breaks a mandatory requirement** is flagged, with the compliant behavior specified.
- **One system per product**: don't combine conventions from different design systems.

## 11 Carbon and GOV.UK (conditional exemplars)

Use them only when the product's own system is silent and the context matches. Cite them as examples, not rules.

**Carbon** (enterprise and data-dense products; checked against an offline copy of carbondesignsystem.com at repository commit df72353, 27 August 2026)
- Notifications: inline (contextual), toast (system events, three lines at most, stacked), actionable, callout, banner, notification panel, modal. No timer-dismissed notifications for critical messages; let users limit non-critical ones.
- Loading: skeletons only for container and data components on initial load; inline loading for a single component; full-screen loading only when the app is temporarily unusable; progressive loading for slow pages.
- Disabled, read-only and hidden variants. Default disabled isn't read by screen readers, so prefer read-only when the content matters.
- Remove pattern: high, medium and low impact tiers; typing the resource name for high-impact deletion; a passive "requested" modal or a notification when deletion isn't immediate.
- Modal: initial focus on the first input (or the primary button when there are none); focus trapped; validation before closing; inline loading on the primary button; a danger variant for destructive confirmations.
- File uploader: per-file loading, success and uploaded states; errors per file or for the uploader as a whole; the drop zone and button operate with Space or Enter; each file's remove control is focusable; focus returns after the file dialog closes.
- Data table: checkbox selection with a three-state "select all"; a batch action bar with Cancel.

**GOV.UK** (transactional public-service forms; checked 2026-10-20)
- Validate on submit; an error summary at the top that receives focus and links to fields; messages beside fields; answers kept; "Error:" prefixed to the page title; specific message templates per problem.
- Buttons: verb labels; avoid disabled buttons; warning (destructive) buttons only for serious consequences, with a confirmation step; double-click prevention backed by server-side duplicate protection.
- Success notification banner for confirming an action on a previous page, at most one per page and never for validation errors; confirmation pages state what happened, the reference, what happens next and how to get help.
- File upload: specific errors for too big, wrong type, empty, virus found, upload failed and too many files.

## 12 AI-powered interactions (conditional)

Use only when the interaction involves AI behavior: uncertainty, fallback, correction, user control, explanations, feedback on output, failure or model limits, or behavior that changes over time. Ordinary controls in an AI product don't qualify. Microsoft's 18 Guidelines for Human-AI Interaction (Amershi et al., CHI 2019), names and grouping checked on 2026-10-20:

- **Initially**: G1 make clear what the system can do; G2 make clear how well the system can do what it can do.
- **During interaction**: G3 time services based on context; G4 show contextually relevant information; G5 match relevant social norms; G6 mitigate social biases.
- **When wrong**: G7 support efficient invocation; G8 support efficient dismissal; G9 support efficient correction; G10 scope services when in doubt; G11 make clear why the system did what it did.
- **Over time**: G12 remember recent interactions; G13 learn from user behavior; G14 update and adapt cautiously; G15 encourage granular feedback; G16 convey the consequences of user actions; G17 provide global controls; G18 notify users about changes.

Translating them into behavior (synthesis, not HAX text):
- **States for generated output**: idle, generating (streaming partial output where available), stopped by the user, complete, failed, low-confidence, declined or out of scope. For actions an AI takes: proposed → awaiting confirmation → executing → done or failed → undone.
- **Cheap to invoke, dismiss and correct** (G7–G9): every output can be edited, discarded or regenerated, and Stop works during generation.
- **When uncertain, narrow the scope** (G10): ask, offer options, or hand back to a manual path instead of acting.
- **Before the AI does anything consequential** (send, buy, delete, share), show what will happen and require confirmation, and make the result reversible where possible (G16). Automation that changes mode or acts silently leaves people out of the loop, so make its state visible. (DOET Ch 5 "The Paradox of Automation")
- **State reliability honestly at the point of use** (G1, G2) and never imply more capability or accuracy than the team has established `[confirm: product]`.
- **Explain why** a suggestion or action happened when it matters (G11); give global controls over memory and personalization (G12, G13, G17); tell people when AI behavior changes (G18); keep feedback controls granular and optional (G15).
