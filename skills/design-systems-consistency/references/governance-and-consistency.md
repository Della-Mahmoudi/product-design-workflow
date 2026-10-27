# Governance and consistency, executable guidance

Load for: library or product consistency audits, duplicate detection, contribution process, ownership, review,
exceptions, deprecation, migration, breaking changes, adoption measurement and system-debt management.
Do not load token-format or parity detail from here; route to the other references if the issue involves them.

Contents: 1 Proportionality · 2 Audit procedure · 3 Finding classification · 4 Duplicate detection ·
5 Contribution tiers · 6 Ownership and review · 7 Exceptions · 8 Deprecation · 9 Migration · 10 Breaking changes
and versioning · 11 Documentation minimums · 12 Adoption and consistency metrics · 13 System-debt register ·
14 Output shapes

## 1. Proportionality (read first)

Governance exists to keep the system coherent at the lowest cost that achieves it. Match the process to the
blast radius, reuse, breaking risk, cross-team impact and migration impact: a token value fix for one role needs
an owner's review and a changelog line; a new component needs evidence, three reviews and a migration note. Do
not generate an RFC template for a two-person team or for a question that a reuse decision answers. Answering a
decision is not running a process: "Should we create DangerButton?" is answered with the decision (EXTEND Button
with a semantic destructive intent); name the contribution tier only when the user asks how to land the change or
the impact warrants it. For governance questions, say explicitly which tier applies and why.

## 2. Audit procedure (library or product)

1. **Scope**: which files/pages/packages, which library version, which date. Unscoped audits produce noise.
2. **Inventory** what exists: components (library vs. local), variants/properties, styles, variables/tokens,
   documented patterns, deprecated items, code components and their props.
3. **Scan** for the issue classes in section 3 using the evidence available (Figma library analytics or
   instance inspection, lint/usage data in code, Storybook story list, docs).
4. **Classify** every finding (section 3) and attach evidence: location, count, screenshot/node id or file path,
   the rule it violates (from Tier 0 docs, or a Tier 1 requirement).
5. **Prioritize** by consumer count × user impact (accessibility and broken parity first, naming last).
6. **Recommend** the smallest fix per finding: migrate to existing object / extend / document exception /
   verify. Group fixes into batches with owners.
7. **Prevent** recurrence: lint rule, Figma library restriction, review checklist item, docs update.
8. Stop at the findings and recommendations; do not redesign screens or implement fixes.

**Coverage when an audit uses extracted or sampled evidence**
- State what was requested and what was actually inspected: relevant routes, components/states, themes and
 viewports. Retain failed, skipped, inaccessible and out-of-scope portions separately from successful samples;
 lack of observation is not proof that a token, component or state is absent. Reuse supplied valid evidence;
 this record does not require a full-site crawl or authorize clicks, authenticated access or other actions.
- Keep each route/artifact independently identifiable even when several have the same page type. If reporting
 coverage or frequency, name the numerator, denominator and sampling limit; failed samples must not silently
 become successful or disappear from the reported scope. Use “shared in the inspected sample,” not “canonical.”
- Page-local or uncommon does not mean off-system; common does not mean approved. A DOM/style cluster is a
 candidate grouping, not proof of a reusable component, variant API or semantic equivalence. Verify purpose,
 actual system identity and relevant states before merging or classifying a defect; preserve valid exceptions.
- Keep extraction failure, measured difference and confirmed rule violation distinct. Counts, similarity and
 aggregate design scores can describe a sample, but cannot establish quality, accessibility conformance or
 severity. Use the finding labels below and the product's approved rules, not an external score threshold.

## 3. Finding classification (mandatory labels)

| Label | Meaning | Action |
|---|---|---|
| Confirmed issue | Evidence shows a rule violation (detached instance of a library component, hard-coded value where a token exists, missing focus state on an interactive component) | Fix or schedule |
| Probable issue | Looks like a violation but intent is unverified (local component resembling a library one, token with no visible consumers) | Verify with owner, then fix |
| Intentional exception | Documented deviation with reason and owner, or clearly product-specific | Keep; check expiry |
| Unknown / requires verification | Evidence insufficient (no access to code, unclear library version) | List explicitly; never guess |

Not every difference is a defect: two semantic tokens with equal values, a product-specific size scale, or an
older-but-supported variant are differences, not findings, until a rule says otherwise.

Issue classes to scan for: detached components; local duplicates of library components; wrong component for the
job (Link styled as Button, Tag used as Button); wrong variant/property values; hard-coded colours, spacing,
radii, type; token bypass or wrong category binding (a spacing token on a radius); undefined or duplicate styles;
missing states; inconsistent naming between library, code and docs; variant explosion; inconsistent anatomy
across members of a family; Figma/code drift (route to design-code-sync); deprecated usage; accessibility gaps
(contrast, focus, names); theme/mode gaps (missing mode values, light-only styles); localization/RTL breakage.

## 4. Duplicate detection

Candidates for "duplicate" (verify before merging):
- Same purpose sentence, different names (`Pill`, `Chip`, `Tag` all for read-only labels).
- Same name, different behaviour (two `Card` components with different anatomy).
- Local components or styles that mirror a library object with small deviations (the deviation is often the
  real finding: a missing variant or token).
- Styles that duplicate variables, or two variables with the same role.
- Patterns re-implemented per team (empty states, confirmation dialogs) with divergent anatomy.
Merge rule: keep the object with the clearer semantics and the larger consumer base; alias/deprecate the other;
carry over any genuinely missing capability as an EXTEND. Do not merge semantically distinct roles because they
look alike today.

## 5. Contribution tiers (proportional)

| Tier | Change | Minimum process |
|---|---|---|
| T1 Patch | Doc fix, token *value* correction within an existing role, bug fix with no API change | Owner review; changelog entry; parity check if both Figma and code exist |
| T2 Extension | New property value, variant, state, size, slot; new semantic token role; non-breaking rename with alias | Short proposal (need, evidence of repetition, alternatives considered, invalid combos); design + engineering review; accessibility check; docs and stories updated in the same change |
| T3 Structural | New component, breaking API change, token layer restructure, deprecation/removal of a widely used object | Proposal meeting the CREATE evidence bar; design, engineering and accessibility review; migration plan; release communication; adoption follow-up |

A request arrives as "make a component" more often than it deserves; classify by what the smallest viable
change is, not by how it was phrased.

## 6. Ownership and review

- Every component, token collection and pattern has a named design owner and a named code owner (or an explicit
  "design-only, implementation pending" status). Orphaned objects are findings.
- Review checklist (apply the relevant lines): purpose sentence unique; REUSE/COMPOSE considered first;
  properties orthogonal, semantic, with defaults; invalid combinations handled; states complete with
  precedence; accessibility contract filled; tokens used (no raw values); naming consistent with the library and
  code; Figma/code parity or an explicit divergence record; docs and stories updated; breaking changes named
  with migration; owner assigned.
- Reviews are proportional to tier; T1 is asynchronous.

## 7. Exceptions

An exception is a documented, owned, time-boxed deviation: object, reason, scope (which product/surface), owner,
review date, and the system change that would retire it (if any). Exceptions without a retirement path accumulate
into a shadow system; review them in the audit. "Marketing needs its own button" is an exception only if the
need is real, scoped and expiring; otherwise it is an EXTEND request in disguise.

## 8. Deprecation

Lifecycle: **proposed** (replacement identified, consumers counted) → **deprecated** (still works; marked in
Figma, code and docs with the replacement and the planned removal condition) → **removed** (consumers at zero or
owner-accepted break; changelog and release note). Rules: never deprecate without a replacement or an explicit
"no replacement, here is why"; keep the deprecated object functional during the window; surface the deprecation
where people pick things (Figma description/name prefix, code warning, docs banner); track remaining consumers.

## 9. Migration

1. Count and locate consumers in design (library analytics, instances per file) and code (usage search, package
   dependents, generated token outputs).
2. Map old → new one-to-one where possible (variant value → property value, token → token). Many-to-one and
   one-to-many mappings need a decision table.
3. Automate what can be automated: Figma variable/component rename and swap-library flows; codemods or token
   alias layers in code. Manual steps get an owner and a deadline.
4. Stage: ship the new object, migrate high-traffic consumers, verify (visual regression, accessibility checks,
   mode checks), migrate the long tail, remove.
5. Document the migration alongside the deprecation notice, with before/after examples.
A widely used token or component is never deleted on the basis of an audit alone.

## 10. Breaking changes and versioning

Breaking in design and/or code: removing or renaming a component, property, value, slot, token or variable
without an alias; changing a default; changing anatomy or dimensions in a way that shifts consumer layouts;
changing a token's semantics or a value in a way that alters contrast or layout; changing keyboard/focus
behaviour; changing event semantics. Non-breaking: additive values, new optional slots, aliased renames,
documentation. Use semantic versioning for code packages; for Figma, use library versions/branches with a
changelog entry that mirrors the code release. One changelog, two channels.

## 11. Documentation minimums per reusable object

Purpose sentence; when to use / when not to use (naming the alternatives); anatomy with region names;
properties with values and defaults; states (matrix or list) ; accessibility contract; content guidance; do/don't
pairs that show the most common misuse; token mapping or link; code reference (package, props, Storybook or
Code Connect link); status (experimental / stable / deprecated) and owners; changelog link. Tokens: role
statement, layer, alias target, mode values, usage examples, deprecation state.

## 12. Adoption and consistency metrics (signals, not targets)

Component coverage (share of UI built from library components), detached-instance count and trend, local
component count per file, hard-coded value count per surface, token adoption in code (share of styling values
resolved from tokens), variant/property counts per component (watch growth), deprecated-usage trend, parity
mismatch count, open accessibility findings by severity, time-to-adopt a new library version. Report trends and
outliers; do not set numeric quotas that invite gaming (a "100 % coverage" target produces fake instances).

## 13. System-debt register

One row per debt item: object, debt type (duplicate, missing state, token bypass, drift, undocumented exception,
orphaned owner), evidence, consumers affected, user impact, proposed fix class (REUSE/COMPOSE/EXTEND/CREATE/
deprecate), effort band, owner, status. Review in each audit; close rows with a changelog link.

## 14. Output shapes

Audit → scope, inventory summary, findings table with labels and evidence, prioritized fixes with the smallest
change each, prevention rules, unknowns. Governance question → applicable tier, minimum process, owners, and
what would escalate it. Deprecation/migration → lifecycle state, replacement, consumer counts (or "unknown"),
mapping, staged plan, breaking-change list, communication.

Sources synthesized here: the product's own rules (Tier 0); Carbon's documentation structure, component status
labels and contribution lifecycle as an exemplar of proportional governance; Storybook as the engineering
documentation surface; *Designing Interfaces* 3e (consistency prevents UX debt; a visual framework defined once
and reused; frameworks as a floor, not a ceiling). See `source-map.md`.
