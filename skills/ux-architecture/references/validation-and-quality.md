# Validation and quality

Read only the sections the task needs.

**Contents**
1. What counts as evidence
2. Choosing a validation method
3. Card sorting essentials
4. Tree testing essentials
5. Navigation and label evaluation
6. Findability assessment without participants
7. Architecture quality checklist
8. Accessibility checks for architecture (WCAG 2.2)
9. Role and permission checks
10. Validation plan output

**Source tags:** as in `ia-navigation-and-taxonomy.md`; full citations in `source-map.md`. **[inference]** marks design reasoning not stated by a source.

---

## 1. What counts as evidence

- Only results the user supplies, or that come from a study they ran, count as validation. Expert review, heuristics and source principles are not user evidence.
- This skill plans IA studies and interprets results the user supplies. It never runs a study, simulates participants or analyzes participants who don't exist.
- **Word claims by their evidence:**
  - Say "users expect X" only when you have Observed evidence. Otherwise write "we assume users expect X" or "principle: ... (source)".
  - Say "validated" only for decisions a real study tested, and name the study.
  - Expert review findings are "expert assessment", not "users struggle".
- **No user evidence:** title the deliverable **Proposed architecture (not validated)** and list which decisions are most at risk.
- **Confidence:** see `SKILL.md`. Raise a decision's confidence only when new evidence arrives, never because sources agree with each other.

## 2. Choosing a validation method

| Question to answer | Method | What it tells you | What it doesn't |
|---|---|---|---|
| How do people group and name this content? | Open card sort | Groupings and vocabulary from people's mental models (NN/g Card sorting) | A final structure, subcategories, or navigation UI |
| Does our content fit these fixed categories? | Closed card sort | How strong the category names are (NN/g Findability tests). Tree testing is usually preferred for this (NN/g Card sorting) | Findability through several levels |
| Can people find X in this hierarchy? | Tree test | Findability, label clarity, placement (NN/g Tree testing) | Visual design, layout, scent from the interface |
| Do people notice and use the navigation UI? | Click or first-click test | Where people click on the interface (NN/g Findability tests) | Quality of the structure |
| How and why do people move through a flow? | Usability test with a prototype | Behavior and reasons (NN/g Findability tests) | Reliable statistics from small samples |
| Which of two labelings works better? | Tree test, between-subjects: each person sees one tree (NN/g Tree testing) | Comparative findability | Why one wins, without follow-up |
| Where should one item live? | One tree; compare clicks across candidate parents (NN/g Tree testing) | Where people look first | |
| What do people do today? | Analytics and search logs, only if they exist (Tier 0) | Real behavior at scale | Reasons |

- **Combine methods.** Card sorting generates structure and tree testing evaluates it, so always tree test a hierarchy that came out of a card sort (NN/g Tree testing; NN/g CS vs TT).
- **Hybrid card sorts:** NN/g generally discourages them because predefined categories bias people (NN/g Card sorting).
- **Aim each study at one question,** for example whether a navigation problem comes from wording or from visibility (Garrett Ch8).
- **What stays here:** planning card sorts, tree tests, closed sorts and label or structure evaluation. For click tests, usability or prototype tests, analytics, instrumentation and experiments, name the method and the architectural decision it would inform, then hand off to `prototype-testing-analytics`.

## 3. Card sorting essentials

This is planning guidance, not a protocol. Write a protocol only if asked.
- **Type:** open to generate groupings; closed to check how content fits categories you already have.
- **Cards:** about 30 to 50 representative items. Beyond about 50, people tire and start dumping cards into a "Miscellaneous" pile (NN/g Card sorting). Write cards in plain language that doesn't reuse candidate category names, applying NN/g's warning about priming in tree tasks to cards [inference].
- **Participants:**
  - NN/g recommends about 15 per distinct user group for most projects. That figure comes from a study in which 15 people reached a 0.90 correlation with the full results.
  - Use 30 or more when you need quantitative confidence (NN/g Card sort sample; NN/g Card sorting gives 30 to 50 for quantitative studies).
  - *Smashing UX Design* says five or six moderated sessions are enough for a draft (Smashing Ch15). Use that only for early, informal rounds and mark the result Low confidence.
- **Moderated or not:** moderated sessions reveal reasons, unmoderated ones scale. A few moderated sessions alongside an unmoderated study work well (NN/g Card sorting).
- **Analysis** of a sort the user ran: use a similarity matrix and dendrogram, and read the reasons, not just the scores (NN/g Card sort sample; NN/g Card sorting).
- **Limits:** card sorts produce ideas, not the final structure. People group the same items differently, so the designer decides (NN/g CS vs TT). A card sort shows only one level and reveals nothing about subcategories or paths (NN/g Card sorting).

## 4. Tree testing essentials

- **Tree:** a text-only hierarchy from global navigation (and utility navigation if relevant) down to the lowest level that holds the targets. In spreadsheet-based tools, put one category per row (NN/g Tree testing).
- **Tasks:** realistic scenarios tied to top tasks and known problem areas.
  - Avoid words that appear in the labels.
  - Define the correct answers. Many tools accept only bottom-level items, so plan for branches that have their own landing pages.
  - Add a warm-up task, and include tasks that test whether parent labels carry scent (NN/g Tree testing).
- **Metrics:** success rate; directness (reaching the answer without backtracking); time; first click; and the spread of paths and final destinations (NN/g Tree testing; NN/g Tree results).
- **Diagnosis** of results the user supplies (NN/g Tree results):
  - A correct first click followed by scattered final choices means sibling labels overlap.
  - Scattered first clicks across the top level mean the item is misplaced, so move it or cross-list it.
  - Cross-list only if many people look in both places.
- **Benchmarks:** a review of 98 studies by Albert and Tullis found a median task success rate of 62%. Their rubric runs from poor (below 40%) to excellent (above 90%). Your own earlier results are the best comparison, and critical tasks need very high success (NN/g Tree results).
- **Sample:** qualitative tree tests need only a few participants, quantitative ones need larger samples. NN/g gives no fixed number, so state your planned number as an assumption (NN/g Tree testing).
- **Limits:** there's no visual context or interface scent, and unmoderated sessions miss reasons. Pilot with a few moderated sessions (NN/g Tree testing).
- **Before and after:** test the current tree before a redesign to get a baseline (NN/g Tree testing).

## 5. Navigation and label evaluation

- **Study the structure and the interface separately.** A good tree test with a poor click test points to layout or visibility, not structure (NN/g Findability tests).
- **Label questions** [inference, synthesizing section 6 of the IA reference]:
  - Is it the users' word?
  - Is it distinct from its siblings?
  - Does it predict what's inside?
  - Is it the same everywhere?
  - Does it survive translation length?
- **Fixes when people confuse sections** (NN/g Fix IA):
  - Merge similar sections.
  - Rename them.
  - Add short explanations.
  - Restructure.
  - Move content to where people look.
  - Add cross-reference links sparingly.

  Combine fixes and retest.

## 6. Findability assessment without participants

This is an expert assessment, so label it that way and never as user evidence.
- For each top task, list the target, the entry points, each decision point and its label, alternative routes (search, contextual links), and the risks.
- Rate each path Clear, Ambiguous or Broken.
- Use Tier 0 signals only if supplied: zero-result queries, navigational queries in search logs, support tickets asking "do you sell..." or "where is...", backtracking in analytics. Never invent them.

## 7. Architecture quality checklist

Run the rows that fit what you produced.

| Area | Check | Typical fix |
|---|---|---|
| Structure | Orphaned or unreachable destinations: does every node have a route from navigation or a defined entry point? | Add a parent, cross-link or entry point, or remove the node |
| Structure | Ambiguous or overlapping categories: are siblings mutually exclusive? | Merge, rename, re-split by a single principle, or cross-list with a canonical home |
| Structure | Duplicate concepts: two names for one thing, or one name for two things? | One concept, one name; differentiate or merge |
| Structure | Unnecessary complexity: levels or sections with little content, parallel structures doing one job? | Flatten, merge, or convert to filters |
| Labels | Internal-only terms or org-chart groupings? | Use user vocabulary; regroup by task or topic |
| Labels | Same concept named differently in navigation, headings, titles, search or notifications? | Pick a preferred term; add the rest as synonyms |
| Labels | Localization and right-to-left resilience: 50% to 300% text expansion, mirrored layouts, alphabetical order, market vocabulary? | Labels that survive expansion, structure not tied to alphabet, market variants |
| Navigation | Global and local navigation confused? | Global = product-wide and stable; local = current area |
| Navigation | Missing entry or exit paths; dead ends in critical flows? | Add entries, exits, escape hatches |
| Navigation | Hidden or unpredictable role-specific navigation? | One skeleton for all roles; a role matrix |
| Navigation | Deep links and back navigation undefined? | Define deep-link targets, back behavior, not-found and no-access pages |
| Search | Search covering for poor organization? | Fix the structure for top tasks |
| Search | No no-results or empty-state paths? | Add onward paths (search reference, section 5) |
| Search | High-priority content hard to find? | Shorter path, better scent, more than one route |
| Roles and scope | Permission leakage through names, counts, search, breadcrumbs, notifications or URLs? | Permission-aware surfaces; neutral no-access page |
| Roles and scope | Cross-workspace assumptions unclear (home scope, switching, links across workspaces)? | Scope model, landing rule, scoped deep links |
| Continuity | No recovery for abandoned or interrupted tasks? | Resume points, task list, saved progress |
| Continuity | Destinations differ across platforms? | Map destinations one to one or document the subset |
| Evidence | Claims of validation or user preference with no evidence? | Relabel as Assumption, or plan validation |

## 8. Accessibility checks for architecture (WCAG 2.2)

A design proposal can't claim conformance. List these as requirements for later stages.

| Success criterion | Level | What the architecture must provide |
|---|---|---|
| 1.3.1 Info and Relationships | A | A defined heading and section hierarchy, so structure can be determined programmatically later |
| 1.3.2 Meaningful Sequence | A | A logical order of content within each destination |
| 2.4.1 Bypass Blocks | A | A way past repeated navigation (handed to implementation) |
| 2.4.2 Page Titled | A | A unique, descriptive title for every destination; put titles in the sitemap |
| 2.4.4 Link Purpose (In Context) | A | Link labels that make sense in context |
| 2.4.5 Multiple Ways | AA | More than one way to reach a page, except steps in a process |
| 2.4.6 Headings and Labels | AA | Headings and labels that describe topic or purpose |
| 2.4.8 Location | AAA | Location information such as breadcrumbs or active state. Recommended for deep products |
| 2.4.10 Section Headings | AAA | Sections organized under headings |
| 3.1.1 Language of Page | A* | The language of each localized destination is identifiable |
| 3.1.2 Language of Parts | AA | Passages in another language, such as language-switcher names, are identifiable |
| 3.2.3 Consistent Navigation | AA | Repeated navigation in the same relative order on every page |
| 3.2.4 Consistent Identification | AA | Same function, same name |
| 3.2.6 Consistent Help | A | Help mechanisms in the same relative order across pages |
| 3.3.7 Redundant Entry | A | No asking again for information already given in the same process |
| 3.3.8 Accessible Authentication (Minimum) | AA | Sign-in steps that don't depend on solving, recalling or transcribing |
| 2.2.1 Timing Adjustable | A | Adjustable time limits in flows |
| 2.2.5 Re-authenticating | AAA | Continuing without data loss after a session expires |
| Conformance: complete processes | | Every step of a process conforms, or the process doesn't |

\* The level of 3.1.1 was not re-verified in this build. Check it in `source-map.md` before citing.

For native apps, the W3C's draft WCAG2Mobile note (informative) reads "set of web pages" as "set of screens".

## 9. Role and permission checks

- **Matrix:** every destination × role cell has a defined state.
- **Leakage surfaces checked:** navigation, breadcrumbs, search and suggestions, counts and badges, recent items, notifications, activity feeds, URLs, deep-link error pages.
- **Skeleton:** the same skeleton and relative order for every role.
- **Unauthorized deep links:** they reach a neutral no-access page with a way back and, if allowed, a request path.
- **Changes mid-session:** role and permission changes during a session are handled.
- **Guests:** invitations and guest access have a deliberately small skeleton.
- **Administration:** admin areas are separate from daily work, and settings are labeled by scope.
- **Mandatory constraints:** compliance, audit or legal constraints are flagged as mandatory.

## 10. Validation plan output

Use this minimal format unless the user asks for a full protocol:

| Decision at risk | Method | Why this method | Who, and a rough sample size with its source | Result that would change the design |
|---|---|---|---|---|

Add one or two lines on sequence, for example "tree test the current structure as a baseline, then the proposed tree". No screeners, scripts or invented results. Usability-test plans, moderator guides, analytics and experiment designs belong to `prototype-testing-analytics`.
