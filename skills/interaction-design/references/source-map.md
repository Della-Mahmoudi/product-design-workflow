# Source map

Read when authority or conflicts matter, when the user asks where a rule comes from, or when a recommendation needs more justification than a one-line citation. Routine answers don't need this file.

Sections: 1 Authority order · 2 Sources · 3 Conflict resolution · 4 Known conflicts · 5 Provenance of key principles · 6 Access, verification and copyright

## 1 Authority order

| Tier | What | Role |
|---|---|---|
| 0 | Product truth from the user: verified research and behavior, current requirements, real technical capabilities and limits, existing interaction behavior, the product's design system and component contracts, roles and permissions, platform and devices | Establishes the real conditions. Existing behavior is evidence, not automatically correct. |
| Mandatory | Applicable accessibility, security, privacy, legal and platform requirements; for web, WCAG 2.2 and the relevant semantic and keyboard guidance | Must be met. When a product convention conflicts, flag it rather than copy it. |
| 1 | The product's established interaction patterns and component behavior; Apple HIG for Apple targets; Material 3 for Material products | Prefer established, accessible patterns over new inventions. Platform guidance only where the platform matches. |
| 2 | About Face 4e, The Design of Everyday Things, NN/g heuristics, Designing Interfaces 3e (Don't Make Me Think as a supplement) | Interaction reasoning, behavioral modeling, pattern selection. |
| 3 | Carbon, GOV.UK, other official component documentation | Examples, never universal laws, never a replacement for the product's own system. |
| Conditional | Microsoft HAX Toolkit | AI behavior only (uncertainty, fallback, correction, user control, explanation, feedback on output, model limits, change over time); never for ordinary controls, even inside an AI product. |

## 2 Sources

| Source | Identity (verified) | Tier | Platforms and domains | Competencies | Use when | Skip when |
|---|---|---|---|---|---|---|
| Product materials | Whatever the user supplies | 0 | The product | Everything | Always, first | Never |
| WCAG 2.2 | W3C Recommendation, 12 Dec 2024. https://www.w3.org/TR/WCAG22/ | Mandatory (web) | Web; applied to apps via WCAG2Mobile | Keyboard, focus, timing, targets, errors, status messages | Any web interaction with accessibility consequences | Purely native questions (use platform guidance; WCAG2Mobile informs) |
| WAI-ARIA APG Patterns | W3C WAI. https://www.w3.org/WAI/ARIA/apg/patterns/ (30 patterns) and the Developing a Keyboard Interface practice | Reference for custom web widgets | Web | Widget keyboard behavior, roles, states, focus | Specifying or reviewing a custom widget | A native control already does the job; native platforms |
| NN/g 10 usability heuristics | Jakob Nielsen, 1994 (updated 2020, reviewed 30 Jan 2024). https://www.nngroup.com/articles/ten-usability-heuristics/ | 2 | All | Status visibility, control and freedom, consistency, error prevention, recognition, error recovery | Critiques and framing rationale | As an implementation specification |
| NN/g Toggle-Switch Guidelines (supplementary) | Alita Kendrick, 29 Jul 2018. https://www.nngroup.com/articles/toggle-switch-guidelines/ | 2 | All | Switch vs checkbox; immediate vs submitted settings | Toggle and checkbox decisions | Anything else |
| About Face (primary book) | Cooper, Reimann, Cronin, Noessel. *About Face: The Essentials of Interaction Design*, 4th ed., Wiley, 2014. ISBN 978-1-118-76657-6 | 2 | Desktop, web, mobile; some idioms dated | Goals, mental models, excise, flow, considerate behavior, undo, errors, controls, dialogs, selection, drag | Behavioral reasoning; control, dialog and error decisions | Where current platform guidance supersedes 2014 idioms |
| The Design of Everyday Things | Don Norman. Revised and expanded ed., Basic Books, 2013. ISBN 978-0-465-07299-6 | 2 | All | Discoverability, signifiers, mapping, feedback, conceptual models, constraints, slips and mistakes | Explaining why interactions work or fail; error prevention | Component-level specifics |
| Designing Interfaces | Tidwell, Brewer, Valencia. 3rd ed., O'Reilly, 2020. ISBN 9781492051961 | 2 | Web, mobile, desktop | Concrete patterns: actions and commands, forms and controls, lists, complex data, mobile | Choosing and describing patterns | Voice, chat and gesture interfaces (excluded by its preface) |
| Don't Make Me Think, Revisited | Steve Krug. 3rd ed., New Riders, 2014. ISBN 978-0-321-96551-6 | 2 (supplement) | Web, mobile web | Clarity, conventions, mindless choices, goodwill, concise copy | Clarity, cognitive load, copy | Detailed behavior specifications |
| Apple HIG | https://developer.apple.com/design/human-interface-guidelines/ | 1 for Apple targets | iOS, iPadOS, macOS, watchOS, tvOS, visionOS | Alerts, modality, undo, toggles, feedback, loading, accessibility | Apple platforms | Anything else |
| Material 3 | https://m3.material.io/ | 1 for Material products | Android, Material web | Components | Material products | Anything else |
| IBM Carbon | https://carbondesignsystem.com/ | 3 | Enterprise web | Notifications, loading, empty, disabled and read-only states, remove pattern, modal, toggle, file uploader, data tables | Enterprise gaps in the product's own system | Consumer or mobile products; anywhere the product system already answers |
| GOV.UK Design System | https://design-system.service.gov.uk/components/ and its patterns pages | 3 | Transactional web forms | Validation, error messages and summary, buttons, notification banner, confirmation pages, file upload | Forms, validation, transactional confirmation | Rich-app or enterprise contexts with different conventions |
| Microsoft HAX Toolkit | https://www.microsoft.com/en-us/haxtoolkit/, the 18 guidelines from Amershi et al., "Guidelines for Human-AI Interaction", CHI 2019 | Conditional | AI features on any platform | Expectations, uncertainty, invocation, dismissal, correction, control, change over time | Interactions that involve AI behavior | Ordinary controls, forms, navigation and CRUD, even in an AI product |
| WCAG2Mobile (found during verification, not in the brief) | W3C Group Draft Note, 6 May 2025. https://www.w3.org/TR/wcag2mobile-22/ | Informative | Native and hybrid mobile apps | Applying WCAG 2.2 A and AA to app screens | Native apps | Web |

## 3 Conflict resolution

1. Name the exact interaction decision.
2. Fix the platform and product context.
3. Apply the mandatory constraints.
4. Check the product's existing behavior and design system.
5. Choose the most relevant method source.
6. Consult domain examples only if the question is still open.
7. When options are otherwise equivalent, prefer the accessible, familiar, lower-complexity behavior.
8. Flag unresolved technical or product conflicts instead of resolving them silently.
9. Never invent system capabilities.

Don't mix Carbon, Material, Apple and GOV.UK patterns arbitrarily: pick the one system the product follows and consult only that one. Load APG only for a custom web widget, one pattern page at a time, and HAX only for AI behavior.

## 4 Known conflicts

| Topic | Positions found | Resolution used by this skill |
|---|---|---|
| Confirm or undo for destructive actions | AF CH8, CH12 and CH21 argue for dropping confirmations in favor of undo, while AF CH9 describes mobile modals as mainly for confirming destructive actions; Apple: no alert for common undoable actions, an alert for uncommon irreversible ones; Carbon: confirm medium and high impact, typed name for high; WCAG 3.3.4: reversible, checked or confirmed | Impact tiers (feedback file §7): undo for frequent reversible actions, confirmation for irreversible ones, stronger safeguards for high impact |
| Validation timing | GOV.UK: on submit, not on blur or while typing; Carbon: on blur; DI Ch 10: on leaving the field; AF CH21: near real-time for validated fields | The product's design system first; otherwise on submit for multi-field and transactional forms, never on valid partial input, and errors removed as soon as they're fixed |
| Disabled submit buttons | DI Ch 10 calls disabling until valid the standard solution; GOV.UK advises avoiding disabled buttons; Carbon notes default-disabled controls aren't read by screen readers; APG uses `aria-disabled` to keep controls discoverable | Prefer an enabled control that explains what's missing; if disabled, show why and keep it discoverable |
| Initial focus in a destructive confirmation | APG: least destructive action; Carbon modal: primary button when there are no inputs; Apple: Cancel isn't the default, and omitting a default encourages reading | Web: least destructive control; native: platform convention |
| Latency thresholds | AF CH11: 0.1 / 1 / 10 s; DOET: acknowledge within 0.1 s; DI Ch 8: an indicator beyond about 1–2 s | Heuristics only: acknowledge immediately, an indicator beyond about a second, progress and Cancel beyond about ten |
| Apologizing in errors | DMMT Ch 11: when in doubt, apologize; GOV.UK: avoid "sorry" and "please" in error messages | The product's voice; acknowledge failures the system caused, never in place of the fix |
| Audio feedback | AF CH15: soft sounds for success, silence for problems | Never rely on audio or on silence; use several channels |
| Hover tools, tooltips and drag | AF CH18 and DI Ch 8 describe hover-revealed tools and drag interactions | Focus and tap equivalents plus non-drag alternatives (WCAG 1.4.13, 2.5.7) |
| Timed toasts | Common practice | No critical information and no sole recovery path in timed messages (Carbon, Apple, AF CH16) |

## 5 Provenance of key principles

| Principle in this skill | Grounding |
|---|---|
| Design from goals; remove excise | AF CH1 "Recognizing User Goals"; CH12 "Goal-Directed Tasks versus Excise Tasks" |
| Represented model follows the user's mental model | AF CH1 "Implementation Models and Mental Models"; DOET Ch 1 "The System Image" |
| The two gulfs as a diagnostic | DOET Ch 2 "The Gulfs of Execution and Evaluation"; "The Seven Stages of Action: Seven Fundamental Design Principles" |
| The action contract (trigger → … → exits) | Original structure synthesized from DOET Ch 1–2 (feedback, seven stages), AF CH5 (key-path storyboards of action and response) and AF CH13 (pliant response) |
| Switches act immediately; checkboxes go with Save; don't mix them in one form | NN/g Toggle-Switch Guidelines; Carbon Toggle usage; Carbon Forms "Toggles" |
| Press proposes, release commits | AF CH18 "Mouse-up and mouse-down events"; WCAG 2.5.2 |
| Do, don't ask; make actions reversible | AF CH8 "Considerate products are self-confident"; CH21 "How to eliminate confirmations"; Apple Alerts |
| Confirmations name the object and its implications | DOET Ch 5 "Confirmation and Error Messages"; Apple Alerts; Carbon Remove |
| Impact tiers for destructive actions | Synthesis of Carbon Remove, Apple Alerts, WCAG 3.3.4 and AF CH21 |
| Latency → feedback mapping | AF CH11 "Optimize for responsiveness but accommodate latency"; CH17 "Respond to commands"; DOET Ch 1–2; DI Ch 8 "Spinners and Loading Indicators" |
| Cancel must really stop the work | AF CH8 "Considerate products take responsibility"; DI Ch 8 "Cancelability" |
| Errors: inline plus summary, input kept, focus to summary | GOV.UK Error message, Error summary, Validation; WCAG 3.3.1, 3.3.3 |
| Forgiving formats | DI Ch 10 "Forgiving Format"; GOV.UK Validation; DOET Ch 2; DMMT Ch 11 |
| Slip and mistake countermeasures | DOET Ch 5 "The Classification of Slips", "The Classification of Mistakes" |
| Focus rules for dialogs, removals and updates | APG Dialog (Modal), Button, Developing a Keyboard Interface; WCAG 3.2.1, 3.2.2, 4.1.3 |
| Status announcements | WCAG 4.1.3 Understanding document |
| Alternatives to gestures and dragging | WCAG 2.5.1, 2.5.7; Apple Accessibility |
| Hide, disable or make read-only | Carbon Disabled states; APG; GOV.UK Button |
| AI interaction states and controls | HAX G1–G18; DOET Ch 5 "The Paradox of Automation"; synthesis |
| No invented capabilities (`[confirm]`); capability status as confirmed, assumed, proposed or requires technical validation | The brief's evidence rules; consistent with WCAG's "designed to support" stance |
| Error-type classification (feedback file §5) | Synthesis of GOV.UK Error message ("when not to use"), DOET Ch 5 slips and mistakes, and this skill's async, batch, offline and conflict rules |
| Boundaries with sibling skills (02 where, what, in what order; 03 what happens on action; 04 appearance; 05 reuse; 06 validation; 07 delivery) | The seven-skill Product Design system's division of work (patch brief), not a published source |

## 6 Access, verification and copyright

- **Books** were verified by title and copyright pages and used only while building the skill. The About Face file was named "About Face 2", but its content is the Fourth Edition, as the brief stated. Locations were checked in the text at chapter and section level; page numbers are deliberately omitted. Guidance is paraphrased; only short principle and pattern names are cited. Nothing at runtime depends on the books.
- **Websites** (checked 2026-10-20) were read selectively for verification, not copied:
  - WCAG 2.2: the Recommendation page was only partly machine-readable, so later success criteria were confirmed through the W3C Understanding documents and the "What's New in WCAG 2.2" page.
  - NN/g: the 10 heuristics article and Toggle-Switch Guidelines.
  - APG: Combobox, Listbox, Dialog (Modal), Alert and Message Dialogs, Switch, Button, Menu Button and Developing a Keyboard Interface. No "Read Me First" page exists on the current APG site; the rule that APG examples aren't conformance guarantees comes from the brief.
  - Apple HIG: Alerts, Modality, Undo and redo, Toggles, Feedback, Loading and Accessibility, read through the HIG's Markdown endpoints.
  - GOV.UK: Error message, Error summary, Button, File upload, Notification banner, Validation, Confirmation pages.
  - HAX: guideline names from the HAX Design Library, phase grouping and authors from Microsoft Research's announcement of the CHI 2019 paper. Re-checked on 2026-10-20 during the boundary patch: the toolkit lives at microsoft.com/en-us/haxtoolkit, the 18 guidelines come from the CHI 2019 paper and fall into four groups (initially, during interaction, when wrong, over time), and the sampled names (G1–G3, G10, G11, G14) match this skill.
  - Carbon: the live homepage was readable but its links were not; page content was checked against an offline verbatim copy (carbon-website repository, commit df72353, 27 August 2026).
  - **Material 3 could not be verified**: m3.material.io returned only a JavaScript notice. Material-specific statements in this skill are marked unverified.
- **Before relying on a web detail at runtime**, re-check it: standards and design systems change.
