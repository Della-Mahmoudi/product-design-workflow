# Search and findability

Read only the sections the task needs. Section 7 is for product catalogs only.

**Contents**
1. Findability and discoverability
2. Browse, search, or both
3. Search architecture
4. Metadata, facets and filters
5. No-results and empty paths
6. Query vocabulary and synonyms
7. Ecommerce module (product catalogs only)
8. Findability checks

**Scope:** what is searchable, how search relates to structure, and the paths around it. Search algorithms, ranking, indexing infrastructure and query parsing are out of scope unless the user explicitly asks. Name them as engineering dependencies. Search-box and filter behavior (autocomplete, keyboard handling, loading and error states) belongs to `interaction-design`, and the look of search and results to `ui-visual-design`.

**Source tags:** as in `ia-navigation-and-taxonomy.md`; full citations in `source-map.md`. **[inference]** marks design reasoning not stated by a source.

---

## 1. Findability and discoverability

- **Findability:** people can find content or functions they assume exist. **Discoverability:** people come across things they didn't know about (NN/g Findability tests). They're different problems with different fixes.
- **Diagnose before redesigning.** Separate structural causes (hierarchy, labels) from interface causes (visibility, placement). Tree tests and closed card sorts examine the structure, click tests examine the interface, and usability tests show how and why people move (NN/g Findability tests).
- **Conflicting results are diagnostic.** Strong category names with poor click results point to layout, not labels (NN/g Findability tests).

## 2. Browse, search, or both

- **Search complements navigation and doesn't replace it.** Many people struggle to form good queries, and the belief that people only search is largely untrue (AF Ch20). Even in ecommerce, Baymard found roughly half of test participants preferred search for finding products, which leaves the other half browsing (Baymard Query types).
- **Offer more than one way** to reach content pages, such as navigation plus search. Steps in a process are exempt (WCAG 2.4.5, AA).
- **Choose the emphasis by content and task** [inference]:

| Situation | Emphasis |
|---|---|
| Known-item lookup in large volumes (orders, records, documents) | Search and filters, with browse for overview |
| Exploration and comparison | Browsable categories with facets; search as an entry point |
| Small product (a few dozen destinations) | Navigation; search optional |
| Mixed content types (objects, people, help, settings) | Scoped search with results grouped by type |

- **Anti-pattern:** search used to hide a structure that doesn't work. If a top task is reachable only by search, fix the structure. Frequent navigational queries in search logs ("billing", "settings") point to a navigation gap [inference].

## 3. Search architecture

Define these at the structural level:
1. **What is searchable:** which object types and content (pages, objects, people, help, settings), and which fields are searched versus only displayed. This is a conceptual index requirement, not an implementation spec.
2. **Scope:** global, within a section, or within an object; the default scope; how people widen or narrow it; and how the current scope is shown. Don't default to a narrow scope without making it visible. In ecommerce, preselected narrow scopes caused abandonment (Baymard Scope). Applying this outside commerce is [inference].
3. **Permissions:** results, counts, suggestions and snippets cover only what the person may access, and tenant or workspace boundaries hold. This is a mandatory constraint.
4. **Results organization:**
   - Group results by type when content is mixed.
   - Show where each result lives in the structure, so people can move up to its parent category (Smashing Ch22).
   - Show counts.
   - Hand presentation details to layout work.
5. **Links between search and navigation:**
   - When a query matches a category or destination exactly, take people there or suggest it.
   - When a query is ambiguous, suggest the likely categories (Baymard Autodirect, for commerce).
   - For other products, suggest matching destinations, for example "Billing settings" for "invoice" [inference].
6. **Refinement:** search within results, and advanced search only where experts need precise queries (Smashing Ch22).
7. **Repeat finding:** saved searches can act as collections people return to (AF Ch14).

## 4. Metadata, facets and filters

- **Derive filter attributes from the task model:** what people compare and decide on (Smashing Ch12, Ch21).
- **Category or filter?** When product or content types share most attributes, one broader list with filters works better than many narrow categories (Baymard Overcategorization, commerce). The same reasoning plausibly applies elsewhere [inference]. Keep separate categories when the useful filters differ substantially (Baymard Overcategorization).
- **Clean values:** facets need controlled, consistent values, units and names. A badly chosen facet does more harm than none (Garrett Ch5).
- **Relevance:** offer filters that fit each category's content, and global filters only for attributes that are truly universal [inference].
- **Zero-result filter combinations:** plan to avoid them, for example by showing result counts (Smashing Ch22). How counts look is a layout detail. Having the data to compute them is a structural requirement.
- **Combinable:** people often can't tell filtering from querying, so make them work together (Tidwell Ch9).
- **Stable schema:** facets and dynamic filters need a stable attribute schema behind them [inference from Tidwell Ch9].

## 5. No-results and empty paths

- **No dead ends:** a no-results page offers related categories, simpler or alternative queries, and a route to help or contact (Baymard No results; Smashing Ch22).
- **Distinguish the empty states**, because each needs a different onward path [inference]:
  - **No match:** suggest alternatives and categories.
  - **Filtered to zero:** offer to remove filters.
  - **No access:** don't reveal that the item exists; give a neutral message and a request path if policy allows.
  - **Empty collection:** offer a way to create the first item.
- **Use zero-result queries as Tier 0 evidence.** For each query decide whether it's a missing synonym, missing metadata, a mislabeled category, or a gap in what's offered. Confirm availability with the product owner rather than assuming it.

## 6. Query vocabulary and synonyms

- **Phrasings to support:** exact names or IDs, product or content types, attributes, use cases and problems, abbreviations and symbols, compatibility, and non-product content such as policies and help (Baymard Query types, commerce; adapting the list to other products is [inference]).
- **Map each phrasing to a structural need:**
  - Variants and misspellings need synonym rings, also called equivalence relationships.
  - Attribute queries need attribute metadata.
  - Use-case and problem queries need use-case tags or curated collections.
  - Non-product queries need help and policy content in the index (NN/g Taxonomy 101; Garrett Ch5 on thesauri redirecting queries).
- **Search logs are Tier 0 evidence** for labels and synonyms. Never invent log data.

## 7. Ecommerce module (product catalogs only)

Baymard's detailed guidelines are part of its paid Premium service and were not accessed. The points below come from its free articles, with dates. Treat the statistics as benchmark context, not facts about the user's store.

- **Weakest areas:** Baymard's public research overview names category taxonomy, main navigation and intermediary category pages as the weakest areas of homepage and category design (Baymard research overview, page undated).
- **Overcategorization:** in Baymard's benchmark, 75% of sites split product types that share attributes into separate categories, which stops people comparing and leads some to assume an item isn't sold. Use combined lists with filters, promote popular filters as category-style links that open prefiltered lists, and review sparse categories (Baymard Overcategorization, 2023).
- **Intermediary category pages:**
  - In broad catalogs they help: use them for the first one or two levels, lead with subcategories, keep promotions secondary and include a "View all" link. 13% of benchmarked sites lack them (Baymard Intermediary, 2023).
  - In small direct-to-consumer catalogs they confused people: 31% of participants struggled to reach the product list. Route category links straight to product lists there (Baymard DTC, 2022).
  - Decide by catalog breadth.
- **Products in several categories:** cross-list only where people look in more than one place, and keep one canonical breadcrumb (NN/g Polyhierarchy).
- **Merchandising groupings:** campaign or merchandising groupings belong in curated collections or promotions, not in the product-type taxonomy. They aren't mutually exclusive product types, and labels that come from brand language lack scent (Tidwell Ch2; Smashing Ch19; the conclusion is [inference]).
- **Search scope:** options include scope suggestions in autocomplete, manual scope selectors for very large catalogs, suggested scopes on the results page, automatic redirection to a perfectly matching category with a way back, and scope prompts when sorting. Never preselect a narrow scope as the default (Baymard Scope, 2014).
- **Category matches:**
  - Redirect automatically when a query matches one category, and suggest categories when it could match several.
  - Keep the query visible after redirecting.
  - Search shouldn't return fewer products than the matching category.
  - 46% of sites did neither (Baymard Autodirect, 2020).
- **Query types:** support exact, product-type, feature, use-case, abbreviation and symbol, compatibility, symptom and non-product searches, and apply searched-for attributes as filters. Baymard reports 56% of sites have issues here (Baymard Query types, 2024, updated 2026).
- **No-results pages:**
  - Linking related categories and suggesting alternative queries are structural fixes.
  - Recommendations, help contacts and popular products are presentation.
  - About half of sites don't help people recover (Baymard No results, 2019, updated 2025).
- **Category pages:** listings support "View all" plus narrowing. The decision process tells you which details each listed item shows and which filters to offer (Smashing Ch21).

## 8. Findability checks

- Every top task's target can be reached by browsing and by search.
- Labels along the browse path carry scent toward that target.
- Search covers the object types people expect, within their permissions.
- Common synonyms and variants of top queries resolve.
- No-results, filtered-to-zero, no-access and empty-collection states each have an onward path.
- Results show where items live, and category-matching queries lead to categories.
- Nothing important is reachable only through search.
