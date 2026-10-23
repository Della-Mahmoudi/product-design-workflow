# ux-architecture: QA cases

Human-readable QA contract for `ux-architecture`. `evals.json` holds the same eight cases in the skill-creator eval schema, with the same IDs and prompts.

- **Should trigger** is the routing expectation. It is not measured by `evals.json`.
- For **NO** cases, the criteria describe what this skill must do if it is loaded anyway (invoked manually): name the boundary, hand off, and not produce the other skill's deliverable.
- The boundary under test: this skill answers *where, what and in what order*. How something behaves belongs to `interaction-design`, how it looks to `ui-visual-design`, and running studies or measuring to `prototype-testing-analytics`.

| ID | Case | Trigger | Primary owner |
|---|---|---|---|
| 1 | Settings taxonomy | YES | `ux-architecture` |
| 2 | Multi-workspace architecture | YES | `ux-architecture` |
| 3 | Structural user flow | YES | `ux-architecture` |
| 4 | Detailed interaction behavior | NO | `interaction-design` |
| 5 | Search and findability architecture | YES | `ux-architecture` |
| 6 | Tree-test planning | YES | `ux-architecture` |
| 7 | Prototype usability testing | NO | `prototype-testing-analytics` |
| 8 | Visual navigation treatment | NO | `ui-visual-design` |

---

## Case 1: Settings taxonomy

**User prompt**

> We have 80 settings across account, team, billing, security and integrations. Help me organize and label the navigation.

**Should this skill trigger?** YES
**Primary owner:** `ux-architecture`

**Expected behavior**
- Works from the five supplied categories and states what it assumes about the 80 settings. Any individual setting it names is marked as an example or assumption.
- States the organizing principle before the groups, for example scope and ownership first, then topic or task.
- Proposes a hierarchy and labels in users' words, with sibling labels that don't overlap.
- Identifies role and scope concerns: personal versus team or organization settings, who sees billing, security and team administration, and settings labeled by scope.
- Marks the result **Proposed architecture (not validated)**, with assumptions, open questions and confidence.
- Recommends IA validation (card sort for grouping, tree test for findability) only if it would change a decision.

**Pass criteria**
- The organizing principle is stated, and all five supplied categories are placed in the hierarchy.
- Labels come with a rationale: user vocabulary, distinctness from siblings, or scope.
- Personal or account scope is separated from team or organization scope, and role visibility is stated for admin areas.
- Assumptions and open questions are listed, and nothing is called validated.

**Failure criteria**
- Designs the visual sidebar: widths, spacing, icons, colors, typography or responsive visual behavior.
- Defines hover, focus, pressed, loading or other states, or writes component specifications.
- Presents invented card-sort, tree-test or usage results as findings.
- Presents an invented list of 80 settings as the user's inventory.

**Unnecessary-work checks**
- No user flow, journey map or full research protocol.
- No JSON unless asked.
- Validation, if any, fits in a line or a short table.

---

## Case 2: Multi-workspace architecture

**User prompt**

> Our product has personal accounts, organizations and multiple workspaces. Where should billing, members and integrations live?

**Should this skill trigger?** YES
**Primary owner:** `ux-architecture`

**Expected behavior**
- Builds an explicit scope model: personal account, organization, workspace.
- Gives billing, members and integrations each one home scope, and spells out the cross-scope cases: organization membership versus workspace membership, and integrations configured at one level and enabled or used at another.
- Names settings destinations by scope and keeps one navigation skeleton; says how the current scope is shown and where people land when they switch workspace, if relevant.
- States role and permission visibility per destination, and flags leakage risks where they matter.
- Surfaces ambiguous ownership as open questions, for example whether billing is per organization or per workspace, or whether personal accounts can own workspaces.

**Pass criteria**
- Account, organization and workspace scopes are separated explicitly.
- Billing, members and integrations each have one home scope with a rationale; cross-scope views are named separately.
- Role or permission visibility is addressed at the destination level.
- At least two open questions or assumptions about ownership are listed, and inference-based decisions carry Medium or Low confidence.

**Failure criteria**
- Designs permission modal, dialog, error-message or disabled-control behavior.
- States backend authorization rules, APIs or data models as facts.
- Leaves several different areas all called "Settings" with no scope.
- Specifies the visual layout of the settings navigation.

**Unnecessary-work checks**
- No full sitemap of the whole product unless the question needs it.
- No flows, journey map or validation protocol unless asked.

---

## Case 3: Structural user flow

**User prompt**

> Map the user flow for inviting a teammate to a workspace, including the major decisions and alternate paths.

**Should this skill trigger?** YES
**Primary owner:** `ux-architecture`

**Expected behavior**
- Defines the goal, the end state and the actors (inviter and invitee, plus an approver only if stated or marked as an assumption).
- Lists the entry points, marking any that are proposed or assumed.
- Draws the key path first, then the branches: permission to invite, invitee already a member, invitee without an account, and unknown conditions such as seat or plan limits shown as dependencies.
- Defines exits: success destination, cancel destination, task-level failure, interruption, and the invitee's acceptance as a separate flow or hand-off.
- Uses a Mermaid flowchart or numbered steps with stable IDs and a legend.
- Lists detailed interaction behavior as a hand-off to `interaction-design`.

**Pass criteria**
- Entry points, a key path, at least two alternate paths and a permission branch are present.
- Success and cancel destinations and a task-level failure outcome are defined.
- The invitee's side is referenced as its own flow or hand-off.
- Unknown system conditions appear as dependencies, and the interaction hand-off list is present.

**Failure criteria**
- Defines loading spinners or button loading states.
- Defines toast content or timing.
- Defines inline validation rules or timing.
- Defines focus behavior, keyboard interaction, retry mechanics or modal transitions.
- Presents invented seat limits or backend rules as facts.

**Unnecessary-work checks**
- No sitemap, journey map, wireframe or validation plan unless asked.
- One diagram per actor at most, and no more diagrams than the flow needs.

---

## Case 4: Detailed interaction behavior

**User prompt**

> For the invite flow, define loading, duplicate-email error, retry, cancel, success toast and focus behavior.

**Should this skill trigger?** NO
**Primary owner:** `interaction-design`

**Expected behavior if this skill is invoked manually**
- States briefly that this is detailed interaction behavior inside a flow, outside UX architecture.
- Hands the request to `interaction-design`.
- Does not produce the interaction specification.
- May note, briefly, the structural facts the interaction work depends on, such as where cancel and success lead.

**Pass criteria**
- The boundary is named and `interaction-design` is named as the owner.
- No loading, error, retry, toast or focus specification appears.

**Failure criteria**
- Specifies loading behavior, duplicate-email error handling or message copy, retry mechanics, cancel mechanics beyond the destination, toast content or duration, or focus placement.
- Writes a state table or state machine.
- Continues because the behavior sits inside an invite flow the skill could map.

**Unnecessary-work checks**
- No re-mapping of the whole invite flow.
- No sitemap or validation plan.

---

## Case 5: Search and findability architecture

**User prompt**

> Users can't find old invoices. Should we solve this with navigation, search, filters, or a different information structure?

**Should this skill trigger?** YES
**Primary owner:** `ux-architecture`

**Expected behavior**
- Treats finding an old invoice as a known-item lookup and diagnoses before redesigning: structural causes (where invoices live, labels, grouping) versus interface causes (visibility, placement).
- Weighs browse against search: invoices need a findable canonical home, with search and filters complementing it.
- Identifies the information structure: the home scope and location of invoices, and metadata usable as filters or facets (date or period, status, amount, invoice number, workspace or account).
- Covers search scope and permissions: who may see which invoices, in results and counts as well as in navigation.
- Covers onward paths for no-results and filtered-to-zero cases.
- Separates evidence from assumptions, and names evidence that would confirm the cause (existing search logs, support tickets, a tree test) without inventing it.

**Pass criteria**
- Structural and interface causes are distinguished.
- A canonical location for invoices is proposed, with its scope.
- Invoice metadata for filtering is named at the structural level.
- Permissions on invoices are addressed.
- Claims about user behavior are labeled as assumptions or inferences unless evidence was supplied.

**Failure criteria**
- Designs the visual search or filter UI: placement, styling, layout or typography.
- Specifies search-box behavior such as autocomplete timing, loading states or keyboard handling.
- Recommends search alone as the fix.
- Invents search-log, analytics or support data.

**Unnecessary-work checks**
- No ecommerce (Baymard) guidance, since this isn't a product catalog.
- No full tree-test protocol unless asked.

---

## Case 6: Tree-test planning

**User prompt**

> We redesigned our account navigation. What should we test to know whether the hierarchy and labels work?

**Should this skill trigger?** YES
**Primary owner:** `ux-architecture`

**Expected behavior**
- Names the architectural decisions at risk: new groupings, renamed labels, moved items.
- Recommends tree testing for the hierarchy and labels, with a comparison point such as the previous navigation as a baseline or old and new trees tested between subjects.
- Plans tasks at the level of realistic scenarios tied to top account tasks, avoiding the words used in the labels, with defined correct answers.
- Names the measures (success, directness, first click) and what results would change the structure: low success or scattered first clicks lead to moving or cross-listing an item, and a correct first click followed by scattered final choices points to overlapping sibling labels.
- States the planned sample size as an assumption or with its source.
- Keeps the structure test separate from interface testing; a click or usability test is named as a separate study if needed.

**Pass criteria**
- A tree test is recommended and tied to specific decisions at risk.
- The plan states which results would change the structure.
- No results are reported or invented; any benchmark figure is attributed to its source.

**Failure criteria**
- Invents participant results, success rates or quotes.
- Expands into product analytics, instrumentation, A/B experiments or a general usability-test program.
- Presents a fixed participant number as a rule.

**Unnecessary-work checks**
- No screener or moderator script.
- Protocol detail stays at planning level unless a full protocol is asked for.

---

## Case 7: Prototype usability testing

**User prompt**

> We have a clickable prototype of the new settings experience. Create a full usability-test plan and moderator guide.

**Should this skill trigger?** NO
**Primary owner:** `prototype-testing-analytics`

The settings IA being involved doesn't make this skill the owner of a usability study.

**Expected behavior if this skill is invoked manually**
- States that a usability study on a prototype is outside UX architecture.
- Hands the request to `prototype-testing-analytics`.
- At most notes, in a line or two, which IA decisions (groupings, labels) the study should probe, or that a tree test could isolate the structure.
- Produces no plan and no guide.

**Pass criteria**
- `prototype-testing-analytics` is named as the owner.
- No usability-test plan and no moderator guide appear.

**Failure criteria**
- Produces session tasks, recruitment criteria, a screener, a session structure, study metrics or a moderator guide.
- Fabricates participant findings.

**Unnecessary-work checks**
- No redesign of the settings IA unasked.

---

## Case 8: Visual navigation treatment

**User prompt**

> Make this navigation feel cleaner. Decide sidebar width, spacing, type scale, colors and mobile visual layout.

**Should this skill trigger?** NO
**Primary owner:** `ui-visual-design`

This skill contributes only if a structural navigation decision (grouping, hierarchy, labels) is explicitly requested.

**Expected behavior if this skill is invoked manually**
- States that these are visual design decisions outside UX architecture.
- Hands the request to `ui-visual-design`.
- Gives no visual values.
- May offer structural help as an option, for example if "cleaner" means fewer or clearer destinations, without restructuring unasked.

**Pass criteria**
- `ui-visual-design` is named as the owner.
- No sidebar width, spacing, type scale, color or mobile visual layout is specified.

**Failure criteria**
- Specifies any of sidebar width, spacing, type scale, colors or a mobile visual layout.
- Restructures the navigation without being asked.

**Unnecessary-work checks**
- No sitemap, flows or validation plan.
