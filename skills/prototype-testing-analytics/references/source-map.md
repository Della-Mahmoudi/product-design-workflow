# Source map: what each source is for, and what it is not

Read this when deciding which source is authoritative for a question, when the user asks for citations, or when sources appear to conflict. Four kinds of source are kept apart because they carry different kinds of authority:

- **Product evidence (Tier 0)**: observations, data and constraints from *this* product. Authoritative for this product once its quality is assessed. Never a substitute for method validity.
- **Methodology sources (Tier 1)**: normative frameworks. They say how to reason about usability, method fit and metrics. They say nothing about your users.
- **Operational practice (Tier 2)**: practitioner books, distilled into this skill's references at build time. Useful for planning and execution; not authority for population or statistical claims.
- **Domain benchmarks and tool documentation (Tier 3)**: context-specific. Loaded only when the context matches.

**Runtime policy.** The references in this skill are self-contained. Do not fetch any source below unless (a) the user explicitly asks for current citations, (b) platform or tool syntax matters for implementation, or (c) currentness materially affects the answer. The build-time books are not bundled and are never required. Online sources list a canonical **URL** for citation and for those exceptions; listing a URL is not a reason to fetch it.

---

## Tier 0: product evidence

| Field | Content |
|---|---|
| Source | Real participant observations and recordings, existing research reports, current analytics and verified event data, actual product behavior, baseline metrics, real experiment data, product constraints, technical and instrumentation constraints, privacy and legal requirements |
| Type | Product evidence |
| Authority | Highest for this product, conditional on quality |
| Modes | A, B, C |
| Use when | Any question about this product. Inventory it first; it may already answer the question |
| Do not use when | Its quality is unknown or known to be poor (unreliable events, unrepresentative participants, undefined metrics, stale baselines). Then treat it as a hypothesis to check, not a fact |
| Limitations | Product-specific does not mean reliable. Assess sample, instrumentation, definitions, recency, and whether it addresses the same question being asked now |
| Load policy | Ask for it or read what the user supplies. Never invent or extrapolate it |
| Access notes | Internal; may contain personal data. Minimize what is handled and flag privacy requirements |

---

## Tier 1: methodology (normative)

### ISO 9241-11:2018, Ergonomics of human-system interaction, Part 11: Usability: definitions and concepts

- **Type**: international standard (concepts and definitions)
- **Authority**: the normative framing of what "usability" means
- **Modes**: B primarily; A and C when framing goals and metrics
- **Use when**: stating what a study or metric actually measures. Usability is an outcome of use: the extent to which specified users achieve specified goals with effectiveness (accuracy and completeness of goal achievement), efficiency (resources expended in relation to results) and satisfaction (the user's attitudes and responses) in a specified context of use (a paraphrase of the widely cited definition, not the standard's wording; do not quote it as such). Use it to check whether a "usability" claim names its users, goals and context, and whether satisfaction is being passed off as usability
- **Do not use when**: a procedure is needed. The standard explicitly provides a framework, not methods, and it is not a usability-testing script
- **Limitations**: the full text is a paid standard. The public catalogue page supports identity, edition, status and high-level scope only; its abstract says the standard provides a framework and does not describe specific processes or methods. Do not invent clauses, numbered requirements, measures, procedures, sample sizes, study protocols or exact normative text attributed to it
- **Load policy**: never at runtime; the concepts are embodied in the references
- **Copyright and access**: paid (ISO store). Cite by number and title. Edition 2 (2018), confirmed at ISO's 2023 systematic review. ISO reviews standards on a five-year cycle, so check the catalogue page before describing it as current in a formal citation
- **URL**: https://www.iso.org/standard/63500.html

### Nielsen Norman Group, "When to Use Which User-Experience Research Methods" (Christian Rohrer)

- **Type**: methodology article
- **Authority**: widely used framework for matching methods to questions
- **Modes**: A and B (method choice); C for the summative placement of analytics and A/B testing
- **Use when**: classifying a question on three axes: attitudinal (what people say) versus behavioral (what people do); qualitative (direct observation, answers why and how to fix) versus quantitative (indirect instruments, answers how many and how much); and context of use (natural, scripted, limited or no product use). Use it to place a question in a generative, formative or summative phase
- **Do not use when**: tempted to invoke every method the framework lists. It is a map for choosing, not a checklist for doing
- **Limitations**: placements are general guidelines; most projects mix methods; self-report is limited by what people notice and are willing to say
- **Load policy**: never at runtime
- **Copyright and access**: free article (Christian Rohrer; published 2022 and periodically re-reviewed by NN/g). Use it for general method-selection guidance, not for claims that depend on a review date
- **URL**: https://www.nngroup.com/articles/which-ux-research-methods/

### Nielsen Norman Group, "Usability (User) Testing 101" (Kate Moran)

- **Type**: practical fundamentals
- **Authority**: baseline definition and practice of usability testing
- **Modes**: A, B
- **Use when**: defining the three elements (facilitator, realistic tasks, representative participant); writing realistic tasks whose wording does not prime behavior; think-aloud; separating qualitative testing (find problems) from quantitative testing (benchmark with task success and time); choosing remote moderated versus remote unmoderated formats
- **Do not use when**: someone wants a universal sample-size law. Its guidance of about five participants per user group for a qualitative study is about finding the common problems of one group; it is not a statistical rule and never supports a population percentage
- **Limitations**: does not cover assistance rules, severity or statistical claims
- **Load policy**: never at runtime
- **Copyright and access**: free article (Kate Moran; published 2019 and periodically re-reviewed by NN/g). Use it for usability-testing fundamentals
- **URL**: https://www.nngroup.com/articles/usability-testing-101/

### Google, "Measuring the User Experience on a Large Scale: User-Centered Metrics for Web Applications" (Rodden, Hutchinson, Fu; CHI 2010)

- **Type**: peer-reviewed metrics framework (HEART and the Goals-Signals-Metrics process)
- **Authority**: primary source for user-centered large-scale metrics
- **Mode**: C
- **Use when**: converting a user-experience goal into signals and then metrics; choosing which of Happiness (attitudinal), Engagement (frequency, intensity, depth of use), Adoption (new users starting), Retention (users still present later) and Task Success (effectiveness, efficiency, errors) serves the decision; normalizing raw counts into rates and per-user averages; choosing signals that are sensitive and specific to the goal; noticing that failure signals (abandonment, undo, frustration) are often easier to detect than success signals
- **Do not use when**: it would mean producing one metric per category regardless of the decision. The paper itself says not every category applies; engagement can be meaningless for tools people use as part of their job
- **Limitations**: metrics are for launched products, must be triangulated with qualitative research, and do not replace formative research. PULSE-style measures (page views, uptime, latency, active users, earnings) are too indirect to evaluate interface changes. Log data needs bot filtering and complete event capture before it is trusted
- **Load policy**: never at runtime
- **Copyright and access**: free. The Google Research publication page gives authors, venue (Proceedings of CHI 2010) and abstract, with a download link. Cite the publication page rather than a mirrored copy
- **URL**: https://research.google/pubs/measuring-the-user-experience-on-a-large-scale-user-centered-metrics-for-web-applications/

---

## Tier 2: operational practice (build-time books, distilled; never required at runtime)

### UX Research: Practical Techniques for Designing Better Products, Brad Nunnally and David Farkas (O'Reilly, first edition November 2016)

- **Type**: practitioner book; the primary build-time operational source
- **Modes**: A, B (planning, recruiting, facilitation, analysis, reporting)
- **What was distilled**: good research starts with good questions (leading questions, yes/no questions, personal and unconscious bias, laddering, tying every question to a goal); insight-driven, evaluative and generative focus; when quantitative methods fit (measurable outcomes at scale) and when to avoid them (motivation, comprehension, small or new populations); when qualitative methods fit and why both are used together; choosing methods by question, stakeholder needs, sample size, location, budget and timeline; screeners built on behaviors rather than demographics, quotas, three to five participants per user group as a qualitative norm; moderator and note-taker as separate roles, observer ground rules, dry runs, session arc from simple to complex, failure is acceptable, debriefs; affinity clustering of discrete data points; lean reporting that answers "so what"
- **Do not use for**: statistical procedures, analytics implementation, or any population claim
- **Copyright and access**: copyrighted; not bundled; no passages reproduced
- **URL**: none; a book, not an online source. Cite by title, authors, publisher and year

### Don't Make Me Think, Revisited, Steve Krug (New Riders, 2014)

- **Type**: pragmatic usability guidance
- **Modes**: B (lightweight testing), A (test early with sketches and prototypes)
- **What was distilled**: small frequent rounds beat one big late test; usability tests observe one person using something, which focus groups and surveys do not; this kind of testing yields actionable insight, not proof; recruit loosely and grade on a curve, except where domain knowledge is required; the facilitator never leads or rescues ("what would you do if I weren't here?"); observers each note the few most serious problems; fix the most serious problems first; ignore slips the participant corrects at once; be sceptical of feature requests; resist adding explanations when removing noise would do; remote and unmoderated options; accessibility begins with clarity for everyone and is confirmed by watching assistive-technology users
- **Do not use for**: rigorous quantitative or population claims. The book is explicit that its method is qualitative
- **Copyright and access**: copyrighted; not bundled; no passages reproduced
- **URL**: none; a book, not an online source. Cite by title, author, publisher and year

### Smashing UX Design: Foundations for Designing Online User Experiences, Jesmond Allen and James Chudley (Wiley, 2012)

- **Type**: practical supporting source
- **Modes**: A (prototype fidelity), B (planning, conducting, analyzing tests; lab, remote and guerrilla formats), C (analytics shows what, qualitative research supplies why; A/B tools find what performs, not why)
- **What was distilled**: objectives first and signed off; test plan as the structure of the report; recruitment brief, screener, over-recruit for no-shows; think-aloud versus retrospective think-aloud; sessions no longer than about an hour; always a dry run; sticky-note clustering into issue categories; each issue described with severity and a suggested fix, plus a severity-ordered appendix; lab (observable, unnatural, slow), remote (scale, own environment, technology risk, cannot probe unmoderated), guerrilla (fast, cheap, wrong participants risk); paper, low-fidelity digital, high-fidelity digital and coded prototypes, and the warning against building the whole product just because the tool allows it; expect a temporary dip after a redesign as existing users relearn
- **Do not use for**: current tool specifics (the tools it names are dated)
- **Copyright and access**: copyrighted; not bundled; no passages reproduced. Supplied file was titled "ux_fundamentals.pdf"; content verified as this book
- **URL**: none; a book, not an online source. Cite by title, authors, publisher and year

---

## Tier 3: domain and tool sources (conditional)

### Baymard Institute, ecommerce UX research

- **Type**: domain benchmark and guideline library, ecommerce only
- **Modes**: A, B, C for ecommerce flows (homepage and category, search, product list and page, cart and checkout, accounts, mobile)
- **Use when**: an ecommerce flow is being validated and known risk areas would sharpen what to probe or instrument, or a domain benchmark is wanted for context
- **Do not use when**: the product is not ecommerce; as a substitute for testing or analytics on this product; or to generalize to unrelated products
- **Limitations**: findings come from other sites and other participants. Most guidelines sit behind a paid tier; free articles exist. A Baymard benchmark is never this product's evidence and never settles a question about this product's users: use its findings as risk hypotheses, probe ideas or domain context, never as "your users do X". Do not quote its statistics from memory; cite a current page when a figure matters
- **Load policy**: only for ecommerce validation questions, and only if domain risk hints or benchmarks are wanted
- **Copyright and access**: mixed free and paid
- **URL**: https://baymard.com/research

### Figma, "Guide to prototyping in Figma" (official help center)

- **Type**: tool documentation
- **Mode**: A (prototype construction only)
- **Use when**: prototype capability affects testability: flows and starting points, hotspots with triggers and actions, overlays, scrolling and overflow, variables and conditionals, sharing a flow link, viewing on a device
- **Do not use when**: choosing a research method; it contains no methodology
- **Limitations**: a Figma Design prototype is a network of linked frames, not a functioning product: no real data, limited text entry and validation, fixed content. These are prototype limitations to document, not user failures to report. Variables, expressions and conditionals can simulate some state; anything simulated is a limitation of the same kind. Code-based prototypes have different limitations; document whichever kind is used
- **Load policy**: only when prototype construction or a capability question arises
- **Copyright and access**: free. Feature names change between releases; check the page only when a construction question depends on them
- **URL**: https://help.figma.com/hc/en-us/articles/360040314193-Guide-to-prototyping-in-Figma

### Storybook, writing tests (interaction, accessibility, visual, snapshot)

- **Type**: tool documentation (component testing)
- **Mode**: adjacent to B and C; implementation validation, not user research
- **Use when**: the question is component-level: does the component render and behave across states, do interaction tests pass, do automated accessibility checks pass, is there regression protection
- **Do not use when**: the question is about users. Storybook tests produce no usability evidence, and automated accessibility checks catch only the subset of issues rules can detect; they do not replace evaluation with people who use assistive technology
- **Load policy**: only for component implementation validation. Verifying that a built component meets its spec as part of implementation QA belongs to `delivery-product-collaboration`
- **Copyright and access**: free. The documentation is versioned and test setup changes between major versions; check the version the project uses only when syntax matters
- **URL**: https://storybook.js.org/docs/writing-tests

### Analytics platform documentation (Amplitude, Mixpanel, GA4, PostHog, or whatever the product actually uses)

- **Type**: tool documentation
- **Mode**: C, implementation syntax only
- **Use when**: the platform is confirmed and event or property syntax, identity resolution, sampling, retention of raw data or export mechanics are needed
- **Do not use when**: designing metrics conceptually. Metric design precedes platform mechanics. Never assume a platform
- **Load policy**: only when the platform is confirmed and syntax is required
- **Copyright and access**: free vendor documentation; not verified at build time because no platform was specified
- **URL**: none listed by design. Use the official documentation of the platform the product actually uses, once it is confirmed

---

## Build-time verification record

Identity details and canonical URLs were re-checked against the official pages in October 2026. Volatile details such as page review dates and tool version numbers are deliberately not recorded.

| Source | Verified | Status |
|---|---|---|
| UX Research (Nunnally, Farkas) PDF | yes: title, authors, foreword, full table of contents, 255 pages | complete, matches claimed book |
| Don't Make Me Think, Revisited (Krug) PDF | yes: title, author, 2014 copyright, full table of contents, 184 pages | complete, matches claimed book |
| Smashing UX Design (Allen, Chudley) PDF | yes: title, authors, 2012 Wiley copyright, full table of contents, 222 pages | complete; file name "ux_fundamentals.pdf" does not carry the title, content does |
| ISO 9241-11:2018 catalogue page | yes | identity, edition and status checked; URL verified; full text paid, not consulted |
| NN/g method selection article | yes | accessible; URL verified |
| NN/g Usability Testing 101 | yes | accessible; URL verified |
| Google HEART paper (Google Research publication page) | yes | accessible; URL verified |
| Baymard research page | yes | accessible; free articles, paid guidelines and benchmarks; URL verified |
| Figma prototyping guide | yes | accessible; URL verified |
| Storybook writing-tests docs | yes | accessible; URL verified |
| Analytics vendor docs | no | platform unspecified; fetch only if needed |

## Conflict resolution, in order

1. Identify the decision being made.
2. Inspect the actual research or measurement question.
3. Assess the quality of the product evidence.
4. Check whether the conflicting sources address the same question.
5. Separate method guidance from product evidence.
6. Prefer direct, valid evidence about this product over generic assumptions.
7. Never override a methodological validity problem with product preference.
8. Surface the uncertainty explicitly.
9. Recommend the minimum additional evidence that would resolve it.

Never average conflicting evidence into a fake consensus.
