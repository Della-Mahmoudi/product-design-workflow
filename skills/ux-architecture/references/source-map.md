# Source map

Load this file only for source questions: which source governs, how to resolve conflicting advice, citation details, or whether something was verified. The tier order and the conflict procedure are in `SKILL.md`. This file records each source's identity, status, applicability and limits.

**Contents**
1. Verification status at a glance
2. Books
3. Online sources
4. Provenance of derived methods
5. Known conflicts and how they resolve
6. Copyright and access limits
7. Verification log

---

## 1. Verification status at a glance

| Source | Tier | Status |
|---|---|---|
| Product-specific evidence supplied by the user | 0 | Always highest for that product |
| *Information Architecture* 4th ed. (Rosenfeld, Morville, Arango) | 1, canonical reference only | **Attachment rejected as evidence.** Identity and publisher contents list verified; no content attributed, and no operational claim depends on it |
| NN/g IA articles (14 listed below) | 1 | Fetched and read |
| *The Elements of User Experience* 2nd ed. (Garrett) | 2 | Verified copy; relevant chapters read |
| *Smashing UX Design* (Allen, Chudley) | 2 | Verified copy (file was named `ux_fundamentals.pdf`); relevant chapters read |
| *Designing Interfaces* 3rd ed. (Tidwell, Brewer, Valencia) | 2 | Verified copy; relevant chapters read |
| *About Face* 4th ed. (Cooper, Reimann, Cronin, Noessel) | 2, optional | Verified 4th edition (file was named "About Face 2.pdf"); selected sections read |
| Baymard Institute | 3, ecommerce only | Public pages and free articles only; Premium not accessed |
| GOV.UK Design System patterns | 3, services and transactions only | Fetched and read |
| W3C WCAG 2.2 and Understanding documents | Mandatory constraint | Fetched and read, except the gaps noted in section 7 |

## 2. Books

### Information Architecture: For the Web and Beyond, 4th edition
- **Identity:** Louis Rosenfeld, Peter Morville, Jorge Arango. O'Reilly Media, October 2015. ISBN 9781491913529, 483 pages, according to the O'Reilly catalog page.
- **Attachment status: rejected.** The attached 76-page PDF is not the book. It's an ebookgrade.com download advertisement whose own listing gives different details (year 2008, 925 pages), followed by filler text in mixed English and Hungarian and unrelated excerpts about the history of photography. It contains no IA content.
- **What was verified instead:** the chapter and section titles, from the O'Reilly catalog page.
  - Ch 6 Organization Systems: exact and ambiguous schemes, hierarchy, database model, hypertext, social classification.
  - Ch 7 Labeling Systems.
  - Ch 8 Navigation Systems: embedded global, local and contextual navigation; supplemental sitemaps, indexes and guides.
  - Ch 9 Search Systems: choosing what to index, determining search zones, presenting results, "When Users Get Stuck".
  - Ch 10 Thesauri, Controlled Vocabularies, and Metadata: synonym rings, authority files, classification schemes, polyhierarchy, faceted classification.
  - Ch 11 Research: content analysis, search log analysis, card sorting.
  - Ch 12 Strategy.
  - Ch 13 Design and Documentation: sitemaps, content mapping and inventory, content models, controlled vocabularies.
- **How the skill uses it:** as the canonical IA work, named for identity and, from the verified contents list only, to say where a topic or term is covered. It is not an operational authority in this build. No rule, method, figure, quotation or page number in this skill comes from its content, and none may be added from the rejected attachment or from memory, or reconstructed from chapter titles. NN/g, Garrett and Tidwell carry the IA grounding instead.
- **Next step:** check a legitimate copy (for example through O'Reilly Learning), then extend the labeling, search-anatomy and content-model guidance with chapter citations.

### The Elements of User Experience, 2nd edition
- **Identity:** Jesse James Garrett. New Riders, 2011. ISBN 978-0-321-68368-7.
- **Chapters used:**
  - Ch 2 Meet the Elements: planes, dependencies, the duality of functionality and information.
  - Ch 4 The Scope Plane: content requirements.
  - Ch 5 The Structure Plane: interaction design versus IA, conceptual models, top-down and bottom-up, architectural approaches, organizing principles, language and metadata, team roles.
  - Ch 6 The Skeleton Plane: navigation design, information design, wayfinding.
  - Ch 8 The Elements Applied: design by default, aiming tests at one element.
- **Use for:** the difference between structure and layout, architectural structures, organizing principles, controlled vocabulary, navigation types, conceptual-model consistency.
- **Skip for:** mobile, roles and permissions, search detail, research methods, journeys. The book doesn't cover them.
- **Caveats:**
  - Framed around the web in 2011.
  - Some heuristics come without evidence: the limit of about three matrix dimensions, two-level site maps.
  - "Site map" means a page users see, which differs from common usage.
  - One paragraph in Ch 6 (Wireframes) assigns skeleton elements to the structure plane, contradicting Ch 2. Follow Ch 2.

### Smashing UX Design: Foundations for Designing Online User Experiences
- **Identity:** Jesmond Allen, James Chudley. John Wiley & Sons, 2012. The attachment was named `ux_fundamentals.pdf`, and all 33 chapters are present.
- **Chapters used:**
  - Ch 12 task models and user journeys.
  - Ch 13 customer experience maps.
  - Ch 15 designing usable IAs: process, card sorting, sitemap documentation.
  - Ch 19 navigation.
  - Ch 21 category pages.
  - Ch 22 search.
  - Ch 32 internationalization.
  - Ch 33 mobile.
- **Use for:** practical methods and documentation conventions, journeys and task models, localization effects on labels.
- **Skip for:** layout and wireframe chapters (16-18, 20, 23-31), which are outside this skill.
- **Caveats:**
  - Written in 2012 with an ecommerce bias.
  - Recommends separate mobile sites (dated).
  - Its card-sort sample guidance (five or six sessions) conflicts with NN/g (section 5).
  - Endorses rollover menus in Ch 21 while warning about hover on touch screens in Ch 33.

### Designing Interfaces, 3rd edition
- **Identity:** Jenifer Tidwell, Charles Brewer, Aynne Valencia. O'Reilly Media, 2020. ISBN 978-1-492-05196-1.
- **Chapters used:**
  - Ch 2 Organizing the Content: IA definition, MECE, ways to organize, screen types, application-structure patterns.
  - Ch 3 Getting Around: signposts, wayfinding, navigation types and models, navigation patterns.
  - Ch 6 Mobile Interfaces: navigation and structure parts only.
  - Ch 9 Showing Complex Data: searching and filtering only.
- **Use for:** application structure, navigation models and patterns, structural mobile considerations.
- **Skip for:** layout, visual style, lists, actions, forms and UI systems (Ch 4, 5, 7, 8, 10, 11). They're interaction or visual detail.
- **Caveats:**
  - Some mobile figures are dated.
  - Local navigation is mentioned but never defined.
  - "Many Workspaces" means parallel views, not tenant workspaces.

### About Face, 4th edition (optional)
- **Identity:** Alan Cooper, Robert Reimann, David Cronin, Christopher Noessel. Wiley, 2014. ISBN 978-1-118-76657-6. The attachment was named "About Face 2.pdf", but its contents are the 4th edition.
- **Sections used:**
  - Ch 1 implementation, mental and represented models; user goals.
  - Ch 4 context scenarios and requirements.
  - Ch 5 functional and data elements, groups and hierarchy, key path and validation scenarios.
  - Ch 12 navigation excise, signposts, "Avoid hierarchies".
  - Ch 14 storage versus retrieval, attribute-based retrieval.
  - Ch 16 localization and accessibility.
  - Ch 20 web navigation, search, footers and infinite scroll.
- **Use for:** goal-directed scenario modeling, when a product is new or complex.
- **Skip for:** routine IA requests, and Part III interaction details.
- **Caveats:**
  - Desktop-era framing.
  - "Avoid hierarchies" is argued by analogy. Read it as a warning against deep abstract nesting.
  - The three-level difficulty claim rests on the authors' experience.
  - Doesn't reference WCAG.
  - Its claim that natural-language query parsing is infeasible is obsolete.

## 3. Online sources

All accessed 20 October 2026. Short names match the tags used in the reference files.

**NN/g (Tier 1)**

| Short name | Title, author, date | URL |
|---|---|---|
| NN/g IA study guide | Information Architecture: Study Guide, Page Laubheimer, 2022 (reviewed Aug 2026) | https://www.nngroup.com/articles/ia-study-guide/ |
| NN/g IA vs Nav | The Difference Between Information Architecture (IA) and Navigation, Jen Cardello, 2014 | https://www.nngroup.com/articles/ia-vs-navigation/ |
| NN/g CS vs TT | Card Sorting vs. Tree Testing, Samhita Tankala, 2024 | https://www.nngroup.com/articles/card-sorting-tree-testing-differences/ |
| NN/g Tree testing | Tree Testing: Evaluate Menu Labels and Categories, Page Laubheimer, 2023 (reviewed Aug 2026) | https://www.nngroup.com/articles/tree-testing/ |
| NN/g Tree results | Tree Testing Part 2: Interpreting the Results, Page Laubheimer, 2024 | https://www.nngroup.com/articles/interpreting-tree-test-results/ |
| NN/g Card sorting | Card Sorting: Uncover Users' Mental Models, Samhita Tankala and Katie Sherwin, 2024 | https://www.nngroup.com/articles/card-sorting-definition/ |
| NN/g Card sort sample | Card Sorting: How Many Users to Test, Jakob Nielsen, 2004 | https://www.nngroup.com/articles/card-sorting-how-many-users-to-test/ |
| NN/g Polyhierarchy | Polyhierarchies Improve Findability for Ambiguous IA Categories, Page Laubheimer, 2018 | https://www.nngroup.com/articles/polyhierarchy/ |
| NN/g Audience nav | Audience-Based Navigation: 5 Reasons to Avoid It, Katie Sherwin, 2015 | https://www.nngroup.com/articles/audience-based-navigation/ |
| NN/g Taxonomy 101 | Taxonomy 101, Page Laubheimer, 2022 | https://www.nngroup.com/articles/taxonomy-101/ |
| NN/g Findability tests | Low Findability and Discoverability: Four Testing Methods, Jen Cardello, 2014 | https://www.nngroup.com/articles/navigation-ia-tests/ |
| NN/g Flat vs deep | Flat vs. Deep Website Hierarchies, Kathryn Whitenton, 2013 | https://www.nngroup.com/articles/flat-vs-deep-hierarchy/ |
| NN/g Utility nav | Utility Navigation: What It Is and How to Design It, Susan Farrell, 2015 | https://www.nngroup.com/articles/utility-navigation/ |
| NN/g Fix IA | 6 Ways to Fix a Confused Information Architecture, Jakob Nielsen, 2006 | https://www.nngroup.com/articles/fixing-information-architecture/ |

- **When to use:** IA methods, navigation considerations, and planning and interpreting card sorts and tree tests.
- **When to skip:** visual or interaction detail.
- **Limits:** older articles (2004-2015) still reflect NN/g's IA guidance, but check them against newer NN/g articles when they conflict.

**Baymard Institute (Tier 3, ecommerce product finding only)**

| Short name | Title, author, date | URL |
|---|---|---|
| Baymard research overview | E-Commerce Homepage & Category Navigation (research overview, undated) | https://baymard.com/research/homepage-and-category-usability |
| Baymard search overview | E-Commerce Search (research overview, undated) | https://baymard.com/research/ecommerce-search |
| Baymard Query types | 8 Search "Query Types" UX Best Practices, Edward Scott, 2024, updated Apr 2026 | https://baymard.com/blog/ecommerce-search-query-types |
| Baymard Overcategorization | Overcategorization of the Product Catalog Can Lead to Abandonment, Edward Scott, 2023 | https://baymard.com/blog/ecommerce-over-categorization |
| Baymard Intermediary | Consider Providing "Intermediary Category Pages", Edward Scott, 2023 | https://baymard.com/blog/ecommerce-sub-category-pages |
| Baymard DTC | DTC UX: Avoid Intermediary Category Pages, Edward Scott, 2022 | https://baymard.com/blog/dtc-avoid-intermediary-category-pages |
| Baymard Scope | E-Commerce Sites Need Multiple of These 5 "Search Scope" Features, Christian Holst, 2014 | https://baymard.com/blog/search-scope |
| Baymard Autodirect | Autodirect or Guide Users to Matching Category Scopes, Rebecca Hugo-Terrey, 2020 | https://baymard.com/blog/autodirect-searches-matching-category-scopes |
| Baymard No results | 5 Proven UX Strategies for "No Results" Pages, Sonia Sousa, 2019, updated Feb 2025 | https://baymard.com/blog/no-results-page |

- **When to use:** product catalogs: category taxonomy, category navigation, product search, filters.
- **When to skip:** SaaS, enterprise, content, or service architecture, unless a catalog is part of the product.
- **Limits:**
  - The detailed guidelines are Premium and weren't accessed.
  - The overview pages contradict themselves on counts ("40+" guidelines against topic totals of 75; "31 guidelines" against report totals of 51). Cite only article-level findings, with their dates.

**GOV.UK Design System (Tier 3, service and transactional patterns only)**

| Short name | Pattern | URL |
|---|---|---|
| GOV.UK Patterns | Patterns index | https://design-system.service.gov.uk/patterns/ |
| GOV.UK Task list | Complete multiple tasks | https://design-system.service.gov.uk/patterns/complete-multiple-tasks/ |
| GOV.UK Question pages | Question pages | https://design-system.service.gov.uk/patterns/question-pages/ |
| GOV.UK Check answers | Check answers | https://design-system.service.gov.uk/patterns/check-answers/ |
| GOV.UK Service nav | Navigate a service (introduced Aug 2024) | https://design-system.service.gov.uk/patterns/navigate-a-service/ |
| GOV.UK Step by step | Step by step navigation (prototype-only on GOV.UK) | https://design-system.service.gov.uk/patterns/step-by-step-navigation/ |

- **When to use:** transactional services, multi-session applications, end-to-end journeys across services.
- **When to skip:** don't import GOV.UK visual or component conventions into other design systems.
- **Limits:** the patterns are written for UK government services, so apply their reasoning, not their branding.

**W3C (mandatory constraint where web or app accessibility applies)**

| Short name | Document | URL |
|---|---|---|
| WCAG 2.2 | Web Content Accessibility Guidelines 2.2, W3C Recommendation, first published 5 Oct 2023; current version 12 Dec 2024 | https://www.w3.org/TR/WCAG22/ |
| What's new | What's New in WCAG 2.2 | https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/ |
| Understanding | Understanding docs for 3.2.3, 3.3.7, 3.1.2 (WCAG 2.2) and 3.2.4 (WCAG 2.1, text unchanged), and Understanding Conformance | https://www.w3.org/WAI/WCAG22/Understanding/ |
| WCAG2Mobile | Guidance on Applying WCAG 2.2 to Mobile Applications, W3C Group Draft Note, 6 May 2025 (informative) | https://www.w3.org/TR/wcag2mobile-22/ |

- **Limits:** a design proposal can't establish conformance. Treat these as requirements for later stages.

## 4. Provenance of derived methods

| Method in this skill | Grounded in | Confidence |
|---|---|---|
| IA before navigation; IA is invisible and shapes the UI | NN/g IA vs Nav; Garrett Ch5, Ch6 | High |
| Structure versus layout boundary | Garrett Ch2, Ch6 | High |
| Architectural structures; top-down versus bottom-up | Garrett Ch5 | High |
| Organization schemes (alphabetical, number, time, location, hierarchy, category or facet) | Tidwell Ch2; Garrett Ch5 | High |
| Mutually exclusive, collectively exhaustive categories | Tidwell Ch2 | High |
| Rule for cross-listing (polyhierarchy) | NN/g Polyhierarchy; NN/g Tree results | High |
| Avoid audience-based top levels | NN/g Audience nav | High |
| Breadth versus depth: no click rule | Garrett Ch5; NN/g Flat vs deep | High |
| Taxonomy, synonyms, facets, governance | NN/g Taxonomy 101; Garrett Ch5 | High |
| Content inventory fields and ROT audit | Smashing Ch15; Garrett Ch4; scope field [inference] | Medium-High |
| Conceptual model built from objects; content model for content types | AF Ch1, Ch4, Ch5; Garrett Ch5, Ch8. The content-model extension is [inference]; the Rosenfeld contents list only names the topic | Medium-High (objects); Medium (content types) |
| Labeling sources and rules | Smashing Ch19, Ch32; Garrett Ch5; NN/g Tree results; WCAG 2.4.6, 3.2.4 | High |
| Navigation systems table | Garrett Ch6; Tidwell Ch3; NN/g Utility nav; NN/g IA vs Nav | High |
| Navigational models | Tidwell Ch3 | High |
| Sitemap formats and annotation | Smashing Ch15; Garrett Ch5 | High |
| Role × destination matrix, leakage surfaces, hide versus lock | [inference] from established practice; WCAG 3.2.3; NN/g Audience nav | Medium |
| Scope model and switching rules for workspaces | [inference]; no source in the set covers multi-tenant IA | Medium |
| Cross-platform canonical IA | Smashing Ch33; Tidwell Ch2, Ch3, Ch6; [inference] | Medium |
| Task-model method | Smashing Ch12; AF Ch1 | High |
| Scenario-based architecture (key path, validation scenarios) | AF Ch4, Ch5 | High (method); Medium (tier mapping) |
| Flow construction and continuity rules | GOV.UK Task list, Question pages, Check answers; WCAG 3.3.7, 3.3.8; Tidwell Ch2 | High |
| Boundary between flow and interaction detail | Garrett Ch5, Ch6; AF Ch5; [inference] | Medium-High |
| Journey and experience maps | Smashing Ch12, Ch13 | High |
| Service journey lanes | [inference]; GOV.UK Step by step | Medium |
| Findability versus discoverability; separating structure and interface tests | NN/g Findability tests | High |
| Search complements navigation | AF Ch20; WCAG 2.4.5; Baymard Query types | High |
| Search scope, permission-aware results, search-to-category links | Baymard Scope, Autodirect (commerce); Smashing Ch22; [inference] outside commerce | Medium-High |
| Facets from the task model; category versus filter | Smashing Ch12, Ch21; Baymard Overcategorization; Garrett Ch5 | High (commerce), Medium (elsewhere) |
| No-results and empty-state paths | Baymard No results; Smashing Ch22; [inference] for the four empty states | Medium-High |
| Card-sort planning figures | NN/g Card sorting; NN/g Card sort sample; NN/g CS vs TT | High |
| Tree-test metrics, diagnosis, benchmarks | NN/g Tree testing; NN/g Tree results | High |
| Fixes for confused IA | NN/g Fix IA | High |
| Accessibility requirements for architecture | WCAG 2.2 and Understanding docs | High (text verified, except the 3.1.1 level) |

## 5. Known conflicts and how they resolve

1. **Card-sort sample size.** *Smashing UX Design* says five or six moderated sessions are enough for a draft; NN/g recommends about 15, and 30 to 50 for quantitative work. NN/g governs for planning. Use the Smashing figure only for informal early rounds, labeled Low confidence.
2. **Click counts and depth.** Garrett prefers a clear seven-step path to a confusing three-step one, and NN/g says the three-click rule is false (title listed in the NN/g IA study guide) and that balance matters. *About Face* reports novices struggling at three levels, from the authors' experience. Don't use click counts as a rule. Judge clarity and scent, and keep critical paths shallow where categories are distinct.
3. **Hierarchies.** *About Face* says to avoid hierarchies. NN/g relies on well-labeled hierarchies, polyhierarchy and facets. Read *About Face* as a warning against deep abstract nesting.
4. **Audience as an organizing principle.** Garrett lists audience without caveats, while NN/g advises against audience-based navigation unless the content is unique. NN/g governs.
5. **The word "sitemap".** Garrett means a page users see; Smashing and common practice mean the structure diagram. Define the term in every deliverable.
6. **"Supplementary" or "supplemental" navigation.** Garrett's supplementary navigation means shortcuts to related content. The Rosenfeld contents list uses supplemental navigation for sitemaps, indexes and guides. Define the term when you use it.
7. **Separate mobile sites.** *Smashing* (2012) and *About Face* (2014) assume them. One canonical IA with navigation patterns per platform supersedes this. Partly [inference].
8. **Intermediary category pages.** Baymard recommends them for broad catalogs (2023) and advises against them for small direct-to-consumer catalogs (2022). The deciding factor is catalog breadth.
9. **Wizard or task list for long tasks.** Use a wizard (Tidwell) for long, unfamiliar, branched tasks done in one sitting, and a task list (GOV.UK) for multi-session transactions with separable tasks.
10. **Closed card sort as evaluation.** NN/g in 2014 lists it as an IA evaluation method; NN/g in 2024 says tree testing is usually preferred. Use tree tests for findability and closed sorts for checking fit to fixed categories.
11. **Infinite scroll.** *About Face* notes it makes footers unreachable and hurts keyboard and screen-reader use. Don't put required navigation in footers of infinite lists.
12. **Baymard overview counts** contradict themselves (section 3). Cite article-level findings only.

## 6. Copyright and access limits

- Everything in this skill is original synthesis. Direct quotes are limited to short terms. No page numbers are given, and no passages are reproduced.
- Works without the original books; links are for optional verification.
- Baymard Premium content wasn't accessed or copied. Free articles are summarized with dates.
- The online sources change. Re-check the figures before citing them in a deliverable that will be shared.

## 7. Verification log (20 October 2026)

- **Books:**
  - All five attachments were inspected with `pdfinfo` and `pdftotext`, and their identity was confirmed from the copyright pages and contents lists.
  - Relevant chapters were extracted with chapter and section provenance.
  - About 20 extracted claims were spot-checked against the text, and all matched. Examples: Garrett's structure types and navigation types, Smashing's card-sort figure and localization figures, and About Face's validation scenario types and infinite-scroll notes.
- **Rejected:** the *Information Architecture* attachment (section 2).
- **Not fully verified:**
  - The conformance level of WCAG 3.1.1 Language of Page wasn't shown in the fetched text. It is believed to be Level A; check before citing.
  - NN/g's tree-testing articles give no fixed participant numbers, so none are stated.
- **Online sources** were fetched on the date above. Where a fetched page was cut short (the main WCAG 2.2 page), the matching Understanding documents were used instead.
- **v2 patch check (20 October 2026):** every mention of *Information Architecture* in `SKILL.md` and the references was re-checked. Each one gives the book's identity, records the rejected attachment, or uses the publisher contents list to name a topic or term. None supports an operational rule.
