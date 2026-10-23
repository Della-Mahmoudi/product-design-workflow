# IA, navigation and taxonomy

Read only the sections the task needs.

**Contents**
1. Working definitions
2. Content inventory and audit
3. Conceptual model and content model
4. Organization schemes and structures
5. Taxonomy, controlled vocabulary and metadata
6. Labeling
7. Navigation systems
8. Sitemaps and hierarchy documentation
9. Role-based and permission-aware architecture
10. Multi-workspace and multi-tenant structures
11. Cross-platform and responsive consistency
12. Enterprise-scale navigation
13. Deep linking, wayfinding and continuity

**Source tags:** (Garrett Ch5) *The Elements of User Experience*; (Tidwell Ch3) *Designing Interfaces*; (Smashing Ch15) *Smashing UX Design*; (AF Ch12) *About Face*; (NN/g *short title*), (GOV.UK *pattern*), (WCAG *SC*) as listed in `source-map.md`. **[inference]** marks design reasoning that no source in the set states directly, so treat it as Medium confidence at most.

---

## 1. Working definitions

- **Information architecture (IA):** what content and functions exist, how they're grouped and named, and how they relate. IA is invisible and shapes the interface (NN/g IA vs Nav; Garrett Ch5).
- **Navigation:** the interface elements people use to reach parts of the IA. Draft the IA, at least a first pass, before designing navigation, so a navigation pattern chosen for looks doesn't force a worse structure (NN/g IA vs Nav). One IA can be expressed through different navigation on different platforms [inference].
- **Taxonomy:** a controlled, usually hierarchical list of terms used to describe and classify content. It works behind the scenes. A faceted taxonomy combines several hierarchies, one per aspect of an item (NN/g Taxonomy 101).
- **Architecture diagram vs sitemap:** Garrett uses *architecture diagram* for the internal structure drawing and keeps *site map* for a page users see (Garrett Ch5, Ch6). Many teams say "sitemap" for both, so state which one you mean.
- **Node:** any unit placed in the structure, from one field to a whole section. Choose the node level of each diagram on purpose (Garrett Ch5).
- **Structure vs layout:** structure decides which content and functions belong to which destination and how people move between destinations. Where things sit on a screen is layout work (Garrett Ch2, Ch6).

## 2. Content inventory and audit

Use this when restructuring, merging products, or when nobody knows exactly what exists, which is common (Smashing Ch15).

**Inventory** (what exists). Capture for each item:

| Field | Why it matters |
|---|---|
| ID | Stable reference for sitemaps, audits and tree tests |
| Name and current location (URL or screen path) | Shows duplicates and orphans |
| Type (page, object type, feature, document, tool) | Separates content from functionality |
| Audience or roles | Feeds role and permission decisions |
| Owner, update frequency, size | Content requirements and governance (Garrett Ch4) |
| Scope (public, organization, workspace, personal) | Needed for multi-tenant products [inference] |
| Top tasks served | Ties the item to user value |
| Usage, only if supplied | Tier 0 evidence. Never estimate it |

**Audit** (how good it is). Give each item a verdict: Keep, Revise, Merge, Remove or Missing. Use ROT (redundant, outdated, trivial) as the quality lens (Smashing Ch15). Flag one thing with two names and two things sharing one name.

For large estates, inventory every first- and second-level destination, then sample deeper content by type and say what you sampled [inference]. For more than about 50 items, summarize by type and level and list only the problem items.

## 3. Conceptual model and content model

For object-heavy products (SaaS, tools, enterprise), build this before the sitemap. Destinations follow from objects. For content-heavy products, apply the same method to content types (article, guide, product, policy): define each type's attributes and its links to other types, so templates, related-content links and facets come from the model rather than from individual pages [inference; the Rosenfeld contents list names content models as a documentation topic].

1. List the objects users talk about, in their words. Mine research for nouns, verbs and first mentions (AF Ch4).
2. For each object, note key attributes, the actions people take on it, and who can take them.
3. Map relationships: containment (a project belongs to one workspace) versus association (a report draws on many projects), plus cardinality and scope (AF Ch5).
4. Decide which objects get their own destinations (a collection view plus an object view) and which live inside another object [inference].
5. Represent the product the way users think of it, not the way it's built. Structures that mirror database tables, services or departments are an implementation model (AF Ch1). Garrett calls this "design by default" (Garrett Ch8).
6. Use one conceptual model consistently. The model implies actions and wording: a cart suggests add and remove, an order form suggests edit and submit (Garrett Ch5). Depart from a familiar model only for a significant gain (AF Ch12).

Output: an object table (Object | Key attributes | Actions | Contained in | Related to | Scope | Who can see or act). Add a Mermaid diagram only when there are more than about six objects.

## 4. Organization schemes and structures

**Schemes** (the principle that groups items) (Tidwell Ch2; Garrett Ch5):
- Exact schemes (alphabetical, number, time, location) work when people know the item and the attribute.
- Ambiguous schemes (topic, task, audience, category or facet) suit exploratory finding but depend on good labels.

Choose the scheme for the audience. Garrett's example: sorting cars by weight helps shippers, not buyers (Garrett Ch5). Upper levels usually follow product goals and user needs, lower levels follow the content (Garrett Ch5).

**Structures** (how nodes connect) (Garrett Ch5):

| Structure | Use when | Watch for |
|---|---|---|
| Hierarchy (tree) | Clear parent-child relationships; most products | Excess depth, vague labels deep down |
| Matrix or facets | People approach items along two or more dimensions | More than about three dimensions strains primary navigation (Garrett's heuristic) |
| Organic (hypertext) | Evolving topics, exploration | Weak sense of place, hard to find things again |
| Sequential | Order matters (tasks, instruction) | Wrong for reference content |

Real products mix structures. Say which one is primary in each area [inference].

**Top-down and bottom-up:** top-down splits categories derived from strategy and can miss content detail. Bottom-up groups real content and can become too rigid to grow. Do both and reconcile them (Garrett Ch5).

**Rules:**
- **Mutually exclusive, collectively exhaustive:** sibling categories shouldn't overlap and together should cover everything (Tidwell Ch2).
- **Polyhierarchy:** when an item honestly fits two parents, cross-list it only if a substantial share of users look for it in both places. Otherwise give it one home. With heavy overlap, prefer facets (NN/g Polyhierarchy; NN/g Tree results). Keep one canonical location for breadcrumbs (NN/g Polyhierarchy).
- **Breadth versus depth:** don't count clicks. Judge each level by clarity and scent. A clear longer path beats a confusing shorter one (Garrett Ch5). Favor broader levels when categories are distinct, and add shortcuts, intermediate overview pages and orientation aids when depth is unavoidable (NN/g Flat vs deep). About Face reports novices struggling at three levels (AF Ch20), which reflects the authors' experience rather than a rule.
- **Audience-based splits:** avoid them unless the content really is unique to each audience. People don't know which group to pick, wonder whether a section is about or for that group, and worry they're missing content. Lead with topics or tasks and keep audience sections secondary (NN/g Audience nav).
- **Org charts:** don't mirror departments, teams or internal systems (Garrett Ch8).
- **Growth:** a structure should absorb new content. When it can't, reorganize it, for example from date to topic as volume grows (Garrett Ch5). A "Miscellaneous" or "Other" bucket signals a structure that doesn't scale (Smashing Ch19).
- **Frequency:** keep frequent destinations within easy reach. Rare but necessary ones (settings, help) can sit deeper but must stay findable (Tidwell Ch2, Ch3).

## 5. Taxonomy, controlled vocabulary and metadata

- **Inputs:** the content itself, existing metadata, subject experts and user data such as search logs. Check for an existing industry taxonomy first (NN/g Taxonomy 101).
- **Preferred terms:** choose the users' term. Map jargon, synonyms, abbreviations, misspellings and regional variants to it (equivalence). Record broader, narrower and related terms (NN/g Taxonomy 101; Garrett Ch5).
- **Thin terms:** avoid terms that classify very little content (NN/g Taxonomy 101).
- **Facets:** give each aspect (type, material, status, owner) its own hierarchy (NN/g Taxonomy 101). Expose only the facets people care about. Showing every facet burdens them (Garrett Ch5).
- **Metadata:** metadata lets you restructure and cross-link without rework (Garrett Ch5). For each object type, define required fields, allowed values and who assigns them [inference].
- **Tags:** user tags (folksonomy) suit fast-growing, user-generated collections where a controlled taxonomy isn't practical (AF Ch14; Tidwell Ch2). Uncontrolled tags fragment vocabulary, so pair them with synonym control or curation [inference].
- **Governance:** name an owner and a review cadence for adding, renaming, merging and removing terms, and spot-check tagging. Automated classification needs human correction (NN/g Taxonomy 101).

Output: a term table (Preferred term | Scope note | Broader | Narrower | Related | Variants | Where the term came from).

## 6. Labeling

**Where labels should come from, best first:** the users' own words (research transcripts, support tickets, search logs, which are Tier 0), then domain conventions used by comparable products, then the team's proposals (Smashing Ch19; NN/g Taxonomy 101).

Rules:
- Use users' words, not brand language, internal codenames or department names (Smashing Ch19; Garrett Ch5).
- Make siblings distinct. When two labels could hold the same item, people split between them. In tree tests this shows as a correct first click followed by scattered final choices (NN/g Tree results).
- Prefer specific labels to clever or generic ones. Treat "Resources", "Solutions", "More" and "Click here" as warning signs (Smashing Ch19 on "Click here"; [inference] for the others).
- Use one term per concept across navigation, headings, page titles, search, notifications and URLs (Garrett Ch5). Components with the same function must be identified consistently (WCAG 3.2.4, AA).
- Headings and labels must describe their topic or purpose (WCAG 2.4.6, AA). Every destination needs a unique, descriptive title (WCAG 2.4.2, A).
- For audience sections, make clear whether the content is for that group (NN/g Audience nav).
- **Localization:** German often needs about 50% more space than English, and short menu items can need up to 300% more in some European languages. Right-to-left scripts generally mirror the design. Vocabulary can differ between markets that share a language (US "dress shirts", UK "formal shirts") (Smashing Ch32). So avoid labels that only work when short, don't rely on alphabetical order surviving translation (AF Ch16), treat language and market as separate dimensions [inference], and give translators the structure and context (Smashing Ch32). The language of each page and of passages in another language must be identifiable (WCAG 3.1.1, 3.1.2).
- Test labels before committing to them (`validation-and-quality.md` section 4).

Output: a label table (Current | Proposed | Why | Evidence label | Confidence).

## 7. Navigation systems

Decide what each system exposes and leave placement and visual form to layout work (Garrett Ch6; Tidwell Ch3).

| System | Exposes | Watch for |
|---|---|---|
| Global | Product-wide top-level destinations, usually persistent | Not everything needs it: immersive modes may need only next, back and an exit (Tidwell Ch3) |
| Local | Parent, siblings and children of the current area | Works best when the structure matches how users think (Garrett Ch6) |
| Contextual (associative) | Links from inside content or objects to related items, including shortcuts to related content (Garrett Ch6 calls these supplementary navigation) | Not a patch for missing structure; too many become clutter (Garrett Ch6) |
| Utility | Secondary tools: sign-in, account, settings, help, language or region, notifications, cart (NN/g Utility nav) | Don't park primary content categories here. Tools hidden behind icons are often missed, so test them (NN/g Utility nav) |
| Remote or supplemental (sitemap, index, guides) | Overview of large or varied estates. Garrett Ch6 calls sitemaps and indexes remote navigation; the Rosenfeld contents list files them under supplemental navigation | Needing a deep sitemap to cope signals a weak top level (Garrett Ch6) |
| Breadcrumbs | Location in the hierarchy, not browsing history | Use the canonical path for cross-listed items (NN/g Polyhierarchy) |
| Footer or sitemap footer | Secondary or complete listing (Tidwell Ch3) | Unreachable on infinite-scroll pages (AF Ch20) |
| Progress or step navigation | Position in a linear sequence (Tidwell Ch3) | Only for real sequences. Hierarchies use breadcrumbs |

**Navigational models** (Tidwell Ch3). Mixing them is normal, so state which applies where.
- **Hub and spoke:** a home lists the areas and people return to it between tasks. Simple and mobile products.
- **Fully connected:** any top-level destination reachable from anywhere.
- **Multilevel (tree):** sections with their own sub-navigation.
- **Step by step:** linear processes such as checkout or onboarding.
- **Pyramid:** a sequence browsed from a hub (galleries, result sets) with next, previous and up.
- **Pan and zoom:** one large space, such as a map or canvas.
- **Flat:** tool-dense apps where finding the tool is the problem.

Rules:
- Navigation shows where people are, where they can go, and how the options relate to the current location (Garrett Ch6; Tidwell Ch3).
- Assume people arrive anywhere, from search, links or notifications, and remember nothing from earlier pages (Garrett Ch6).
- Keep repeated navigation in the same relative order everywhere (WCAG 3.2.3, AA). Keep help in a consistent place (WCAG 3.2.6, A). Offer more than one way to reach a page, except for steps in a process (WCAG 2.4.5, AA).
- For each level decide what's shown, whether it persists, whether parents and siblings stay visible, and how the longest label fits (Smashing Ch19).
- **Global versus local:** global items are product-wide and stable, local items change with the area. If one area's items appear in global navigation, check that they're top tasks across the product [inference].
- Keep landmarks stable and don't change menus unexpectedly (AF Ch12). Personalize inside content areas or with pinned favorites, not by reshuffling the skeleton [inference].

## 8. Sitemaps and hierarchy documentation

- A sitemap fixes the top-level sections, the depth and the labels, and becomes the shared reference for scoping later work (Smashing Ch15).
- **Formats:** an outline is fast but hard to annotate; a spreadsheet sorts well and suits large estates and tree-test tools; a diagram communicates relationships best (Smashing Ch15). Diagrams should show conceptual relationships, not every link (Garrett Ch5).
- **Annotate each node** with a stable ID, label, destination type or template, logged-in-only or role visibility, and current or later release (Smashing Ch15), plus scope (organization, workspace, personal) where relevant [inference].
- Mark nodes Existing, Proposed, Moved, Merged or Removed.
- Show cross-links and cross-listed items differently from parent-child lines (dashed or marked "also in"), and add a legend.
- Keep flows out of the sitemap. Link to them by flow ID.

Example of the notation:

```
1      Home                         [all roles]
1.1    Projects                     [scope: workspace]
1.1.1    Project (object view)      [Existing]
1.2    Reports                      [scope: workspace] [Proposed: merges "Analytics" and "Insights"]
1.2.1    Report (object view)       also in: 1.1.1 > Reports tab
U.1    Help                         [utility, consistent position]
Legend: [scope] home scope · [Proposed] new or changed · "also in" = cross-listed, canonical path shown first
```

## 9. Role-based and permission-aware architecture

None of the books in this skill's source set treats permission architecture in depth. The rules below are design inference built on the cited principles, so give resulting decisions Medium confidence unless Tier 0 evidence supports them. Security and legal requirements are mandatory constraints.

1. **Matrix first.** Before drawing role-specific navigation, fill a role × destination matrix with one state per cell: Full, Read-only, Hidden, Locked (visible, with a request or upgrade path), or Not applicable.
2. **One skeleton.** Keep the same skeleton for every role and vary what's inside it. People who change roles or help a colleague should find things in the same places, and repeated navigation stays in the same relative order (WCAG 3.2.3).
3. **Hide or lock.** Hide destinations a role can never use. Show them locked only when there's a legitimate path (request access, upgrade) and the label itself reveals nothing protected.
4. **Check for leakage** in every surface that names things: navigation labels, breadcrumbs, search results and suggestions, counts and badges, recent items, notifications, activity feeds, URLs and error pages for deep links. Someone without access shouldn't learn that a resource exists unless policy allows it.
5. **Don't duplicate destinations per role** ("Admin reports" next to "Reports") unless the content really differs. Scope one destination by permission instead. Audience-specific sections are justified only when the content is unique to the audience (NN/g Audience nav).
6. **Separate administration** (members, roles, billing, security) from daily work, usually as a settings or admin area scoped to the level it administers.
7. **Plan for changes mid-task.** Define where people end up when permissions change during a task, or when someone opens a link they can't access: a "no access" destination with a way back and, where allowed, a request path. How the interface responds in the moment (disabled controls, messages, unsaved work) belongs to `interaction-design`.
8. **Guests and external collaborators** usually see only what was shared with them. Give them a deliberately small skeleton rather than an emptied-out full one.
9. **Roles versus audiences:** role-based visibility in an app follows permissions. Self-selected audience labels on a website are a different pattern, with the problems listed in section 4.

Output: the matrix, a list of leakage risks, assumptions and open questions.

## 10. Multi-workspace and multi-tenant structures

This section is also design inference. *Designing Interfaces*' "Many Workspaces" pattern is about parallel views and windows, not tenant workspaces (Tidwell Ch2).

1. **Model scopes explicitly:** organization or account → workspace → container (project, folder) → object, plus a personal scope (profile, notifications, preferences).
2. **One home scope per destination.** Give every destination exactly one home scope. Name the cross-scope aggregates separately (for example "My work across workspaces").
3. **Show and name the scope.** Always show the current scope. Label settings by scope ("Organization settings", "Workspace settings", "My preferences") rather than three things called "Settings".
4. **Switching scope.** Define a landing rule: the equivalent destination in the new workspace if it exists, otherwise the workspace home. Never drop people on an unrelated page without saying where they are.
5. **Deep links carry the scope.** Opening a link to another workspace switches context visibly. Without access, follow section 9 item 7.
6. **Search and notifications** default to the current scope, offer an explicit way to widen, and show each result's scope (`search-and-findability.md` section 3).
7. **Things configured at one level and used at another** (for example, an integration installed for the organization and switched on per workspace): put configuration where it's administered and a status or enablement view where it's used, with the same name in both places.
8. **Open questions to raise every time:** can objects move or be shared across workspaces? Do people belong to several workspaces with different roles? Which settings can workspaces override?

## 11. Cross-platform and responsive consistency

- Keep one canonical IA (objects, destinations, labels) across platforms. Navigation patterns may differ by platform (tab bar, sidebar), but destinations should map one to one or through a documented subset [inference]. Reprioritize for small screens rather than removing content, and keep the same content present or linked (Smashing Ch33).
- Put essentials first and move the rest deeper, still reachable (Tidwell Ch6; Smashing Ch33).
- The same deep link should open the same destination on every platform, including native apps (Tidwell Ch3).
- Navigation that depends on hover fails on touch screens (Smashing Ch33). Flag it as a constraint for `interaction-design` and layout work.
- Alternative views of one content set (map and list, for example) are views of one destination, not separate destinations (Tidwell Ch2).
- Content must remain usable at narrow widths without two-dimensional scrolling (WCAG 1.4.10, AA). This is an implementation constraint to pass on.
- For native apps, the W3C's draft WCAG2Mobile note maps "set of web pages" to "set of screens". It's informative, not normative.
- Older sources recommend separate mobile sites (Smashing, 2012; About Face, 2014). Treat that as superseded unless the products really are separate.

## 12. Enterprise-scale navigation

- Global navigation lists the product areas relevant to the person's roles. Each area has local navigation, and object views look and work alike across areas [inference].
- For many settings, use a settings-editor structure: groups derived from card sorting, a conventional location, search, and current values visible (Tidwell Ch2).
- Dashboards are overview destinations with drill-down to objects (Tidwell Ch2). Don't make them the only route to objects [inference].
- Fat menus or a sitemap footer can make a deep tree reachable in one step, with an accessible fallback (Tidwell Ch3).
- Use wizards for rare, long, branched tasks, not for experts or frequent work (Tidwell Ch2). Long multi-session transactions belong in a task list (`flows-and-journeys.md` section 4).
- Layer help from on-screen text to full documentation and community (Tidwell Ch2), and keep it in a consistent place (WCAG 3.2.6).
- Let people pin or favorite items as an addition to the stable skeleton, not a replacement for it (AF Ch12; [inference]).

## 13. Deep linking, wayfinding and continuity

- Every meaningful location should be linkable, plus useful state such as filters or a selected tab. Keep personal settings out of shared links (Tidwell Ch3).
- Orient people on arrival with the page title, the active navigation state, and breadcrumbs in hierarchies (Tidwell Ch3; WCAG 2.4.2; WCAG 2.4.8 Location, AAA).
- Never break the browser back button. For one-time actions such as payments, back should show a sensible message rather than repeat the action (GOV.UK Question pages).
- Give an escape hatch from wizards, dialogs, errors and out-of-context arrivals to a safe place (Tidwell Ch3).
- Define destinations for not found, no access, deleted or archived, and moved items, each with a way onward (GOV.UK provides a page-not-found pattern; the others are [inference]).
- Returning users should see where they left off in multi-session tasks (GOV.UK Task list). Work should survive an expired session where possible (WCAG 2.2.5, AAA). Flag this as a dependency for later stages.
