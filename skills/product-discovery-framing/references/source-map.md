# Source map

Where this skill's guidance comes from, how much weight each source deserves, and what to do when sources disagree.

**Read this file only when:**
- the user asks where guidance comes from
- sources seem to conflict
- you need to judge how much weight a framework deserves
- you are maintaining the skill

**Contents**
1. Authority tiers
2. Conflict rules
3. Source register and tags
4. Provenance of key methods
5. Known tensions and how this skill resolves them
6. Access, licensing and limits

The skill works without the original books or websites. Links are for optional verification; do not browse them unless asked.

---

## 1. Authority tiers

**Tier 0, verified product-specific truth.** Current research, interview records, observed behaviour, analytics, existing product behaviour, validated requirements, and business, legal and technical constraints.
- Tier 0 decides what is true for *this* product.
- Judge its credibility (method, sample, recency, instrumentation); Tier 0 is not automatically right.
- But generic sources never override credible Tier 0 evidence.

**Tier 1, standards and authoritative methods, each authoritative only in its own domain:**

| Source | Domain |
|---|---|
| ISO 9241-210 | the human-centred design process |
| NN/g, GOV.UK | research methods and discovery practice |
| ProductTalk | outcome and opportunity framing |
| SVPG | product-risk thinking |
| Google HEART | UX measurement |

None of these outranks another outside its own domain.

**Tier 2, canonical books for deeper reasoning:** Nunnally & Farkas; Lemser; Levy.

**Tier 3, supporting conceptual framework:** Garrett. Used mainly to keep discovery decisions consistent with later stages.

## 2. Conflict rules

1. **Check which source actually applies to the question.** Domain fit matters more than tier number.
2. **Respect mandatory constraints that apply:** law, regulation, contracts, accessibility obligations, documented business constraints. If one conflicts with current product practice, flag the conflict; do not silently pick a side.
3. **Credible product evidence beats generic assumptions about users.**
4. **Relevant research or methodological guidance beats unsupported opinion,** senior opinion included.
5. **Book frameworks are for reasoning,** not for manufacturing product facts.
6. **Competitor observations are context,** not proof of demand.
7. **Mark unresolved conflicts and uncertainty explicitly.**
8. **Never invent** research results, personas, market sizes, metrics or stakeholder decisions.

## 3. Source register and tags

Each entry gives the source's tag, what it is authoritative for, when to use it and when to skip it, and any limits. Web pages were accessed on 2026-10-20.

### Tier 1

**[ISO]** ISO 9241-210:2019, *Ergonomics of human-system interaction, Part 210: Human-centred design for interactive systems* (edition 2, July 2019; the ISO page says it was reviewed and confirmed in 2025). https://www.iso.org/standard/77520.html
- **Verified:**
  - The public abstract: requirements and recommendations for human-centred design principles and activities across the life cycle of interactive systems. It is an overview, not a guide to detailed methods.
  - From publicly available preview pages of BS EN ISO 9241-210:2019, identical text (https://webstore.ansi.org/preview-pages/BSI/preview_30388991.pdf), only the headings of two clauses.
  - Principle headings: design based on an explicit understanding of users, tasks and environments; users involved throughout design and development; design driven and refined by user-centred evaluation; an iterative process; design that addresses the whole user experience; a multidisciplinary team.
  - Activity headings: understanding and specifying the context of use; specifying user requirements; producing design solutions; evaluating the design.
- **Use for:** the general rationale for grounding work in users and their context of use, involving users, iterating, and evaluating with users.
- **Skip or avoid:**
  - Any claim about clause content, definitions or requirements: the normative text was not accessed.
  - Any claim of conformance.

**[NNG]** Christian Rohrer, "When to Use Which User-Experience Research Methods", Nielsen Norman Group (published 2022-07-17; the page says it was last reviewed 2026-07-15). https://www.nngroup.com/articles/which-ux-research-methods/
- **Use for:**
  - The three lenses: attitudinal vs. behavioural, qualitative vs. quantitative, and context of use.
  - The phases: strategize, design, launch and assess.
  - What qualitative methods answer (why, how to fix) versus quantitative ones (how many, how much).
  - The gap between what people say and what they do.
  - Method summaries.
- **Skip when:** no method choice or evidence-type question is involved.

**[GOV-D]** GOV.UK Service Manual, "User research in discovery" (updated 2026-09-09). https://www.gov.uk/service-manual/user-research/user-research-in-discovery
**[GOV-P]** "Plan user research for your service" (updated 2026-10-15). https://www.gov.uk/service-manual/user-research/plan-user-research-for-your-service
**[GOV-N]** "Learning about users and their needs" (updated 2017-03-23). https://www.gov.uk/service-manual/user-research/start-by-learning-user-needs

GOV-P and GOV-N are linked from GOV-D and were read as supporting pages from the same source.
- **Use for:**
  - What discovery research must learn: who the users are, how they cope today, their problems and their needs.
  - Researching with a broad range of users, including disabled people and people with low digital skills, and the staff who deliver or support the service.
  - Existing data and previous research as inputs.
  - The discovery outputs.
  - When research is "enough": you understand the different kinds of users and what they need.
  - Planning: turning assumptions into research questions, prioritizing, 4–8 participants per qualitative round, inclusion in every round, and not doing research the team cannot act on.
  - The user-need format, and treating non-user opinions as assumptions.
- **Limits:** written for UK public services. The research principles transfer; procurement and government specifics do not.

**[PT]** Teresa Torres, "Opportunity Solution Trees", Product Talk (dated 2023-12-06; modified 2026-09-29 per page metadata). https://www.producttalk.org/opportunity-solution-trees/
- **Use for:**
  - The outcome types: business, product and traction.
  - Opportunity as an unmet need, pain point or desire.
  - The alternatives test that separates opportunities from solutions.
  - Mapping and grouping opportunities.
  - Choosing a target opportunity by sizing, market, company and customer factors, with effort excluded.
  - Comparing several solutions; testing assumptions, riskiest first.
  - The prerequisites (an outcome, and story-based interviews) and the anti-patterns.
- **Skip when:** the prerequisites are missing or a problem statement is enough.

**[SVPG]** Marty Cagan, "The Four Big Risks", SVPG (2017-12-04; drawn from *INSPIRED*). https://www.svpg.com/four-big-risks/
- **Use for:**
  - The definitions of value, usability, feasibility and business viability risk.
  - Ownership: the product manager owns value and viability, the designer usability, the lead engineer feasibility.
  - Tackling risks early.
  - Value risk as usually the toughest, and viability as often underestimated.
- **Limits:** the article does not explicitly map the risks to discovery versus delivery; this skill applies them at discovery level.

**[HEART]** Kerry Rodden, Hilary Hutchinson, Xin Fu, "Measuring the User Experience on a Large Scale: User-Centered Metrics for Web Applications", Proceedings of CHI 2010. Publication page: https://research.google/pubs/measuring-the-user-experience-on-a-large-scale-user-centered-metrics-for-web-applications/
- **Paper read at:** https://research.google.com/pubs/archive/36299.pdf, which redirects to Google's static host.
- **Use for:**
  - The categories: Happiness, Engagement, Adoption, Retention, Task success.
  - Goals → Signals → Metrics.
  - The critique of generic PULSE metrics.
  - Signals sensitive and specific to the goal; normalizing raw counts.
  - Using categories selectively.
  - Metrics as a complement to research, not a substitute; triangulating with qualitative studies.
- **Skip when:** no measurement question is involved.

### Tier 2

**[UXR]** Brad Nunnally and David Farkas, *UX Research: Practical Techniques for Designing Better Products*, O'Reilly, first edition, November 2016 (copyright line © 2017).
- **Use for:**
  - Research goals (what, why, a hypothesis to disprove).
  - Writing questions and avoiding bias.
  - Laddering.
  - The strengths and limits of quantitative and qualitative research.
  - Six factors for choosing a method; pairing methods.
  - Recruiting and screening on behaviour.
  - Analysis and contradictions.
  - Treating research as ongoing; findings that go stale.
- **Chapters used:** 2–7, 11, 13, 15.
- **Weak or absent:** causation, validity, statistics beyond the basics, inclusive and accessible recruiting, separating problems from solutions.

**[SPM]** Frank Lemser, *Strategic Product Management according to Open Product Management Workflow™*, proProduktmanagement GmbH, edition "last updated September 2025". Licensed CC BY-SA 4.0.
- **Use for:**
  - Market problems: widespread, urgent, and people willing to pay.
  - Interviewing without proposing solutions.
  - Customer types; segmenting by problem; focusing on a target segment.
  - Personas and scenarios built from interviews.
  - Competitive analysis beyond feature tables; avoiding feature wars and over-engineering.
  - Core competence.
  - KPI discipline (thresholds that trigger action).
  - Roadmaps stated as problems; value expressed as time or money saved.
- **Weak:**
  - A B2B and enterprise slant.
  - Treats interview statements and stated willingness to pay as facts.
  - Thin quantification.
  - No guidance on hypotheses, experiments, accessibility or causation.
  - Its prioritization method is deferred to another book.

**[UXS]** Jaime Levy, *UX Strategy: How to Devise Innovative Digital Products That People Want*, O'Reilly, first edition, 2015. Only this edition was used.
- **Use for:**
  - The value-proposition loop: segment → problem → provisional personas → customer discovery → pivot.
  - Provisional personas as checkable assumptions.
  - Direct and indirect competitors, and the limits of competitive analysis.
  - Value innovation and the "key experience".
  - Experiments and MVPs.
  - Decision thresholds agreed in advance.
  - Actionable versus vanity metrics; one key metric per funnel stage.
  - Stakeholders assuming value instead of verifying it.
- **Risky; do not adopt:**
  - Treating a handful of interviews as validation.
  - No statistics or causal reasoning.
  - Deceptive tactics: fake profiles on competitor products, posing as a customer, undisclosed concierge tests.
  - Dated tools.

### Tier 3

**[EUX]** Jesse James Garrett, *The Elements of User Experience: User-Centered Design for the Web and Beyond*, 2nd edition, New Riders, 2011.
- **Use for:**
  - The five planes and their dependencies, including that decisions flow in both directions.
  - Product objectives versus user needs.
  - Success metrics tied to behaviour that design can shape, and read in context.
  - Segmentation; personas consistent with research.
  - Scope and non-scope; stated versus real requirements.
  - Prioritizing by objectives and feasibility; ranking objectives.
  - Design by default, mimicry or fiat.
  - The boundaries of the handoff to later stages.
- **Weak:**
  - No guidance on risk, hypotheses, experiments, competitive methods or analytics.
  - Web-era examples.
  - The example persona is demographic-heavy and its details are invented.

**[SYN]** This skill's own synthesis. Where no single source covers a topic, confidence grading, metric-change framing, AI-feature checks, research ethics, the method combines the sources above with the skill's evidence rules. Label conclusions based on it as synthesis.

## 4. Provenance of key methods

| Method in this skill | Primary basis | Supporting |
|---|---|---|
| Problem vs. solution, alternatives test | PT | SPM pp.17, 30, 44, 52; EUX Ch4 "Defining Requirements"; UXR Ch2, Ch5 |
| Evidence labels; non-user opinions as assumptions | SYN | GOV-N; NNG (say vs. do); UXR Ch3–4 |
| Users, needs and inclusion | GOV-D, GOV-N | EUX Ch3; SPM pp.62–68, 79–85; UXR Ch7 |
| Provisional personas | UXS Ch3 | EUX Ch3 "Creating Personas" |
| Outcomes | PT | EUX Ch3 "Product Objectives" |
| Opportunity mapping and prioritization | PT | SPM p.58, pp.82–85 |
| Hypotheses and advance decision rules | UXR Ch6; UXS Ch7–8 | PT |
| Research questions | GOV-P; UXR Ch6 | SPM p.55 |
| Method selection | NNG | UXR Ch5; GOV-D |
| Sample sizes and inclusion | GOV-P, GOV-D | UXR Ch7 |
| Confidence grading | SYN | NNG; UXR Ch3–4, Ch13; HEART |
| Framing a metric change | SYN | HEART (log caveats, A/B example); EUX Ch3; NNG (A/B testing) |
| Four risks | SVPG |, |
| AI-feature checks | SYN applying SVPG | HEART |
| Value proposition | UXS Ch3 | SPM pp.121–122 |
| Competitive context | UXS Ch4–5 | SPM pp.40, 73–77 |
| Scope and non-scope | EUX Ch4 | SPM pp.56, 99, 117 |
| MVP reasoning | UXS Ch6–7 | SVPG; SPM p.134 |
| Metrics | HEART | EUX Ch3; SPM pp.100–102; UXS Ch9 |
| Handoff | EUX Ch2, Ch4–5 | ISO (activity headings) |

**Page references:**
- SPM: printed page numbers equal PDF page numbers.
- UXR: printed page = PDF page − 21.
- EUX: printed page = PDF page − 19.
- UXS: the supplied file has no print pagination, so it is cited by chapter and section only.

## 5. Known tensions and how this skill resolves them

- **Sample sizes differ.** GOV.UK suggests 4–8 per round, Nunnally & Farkas 3–5 per user group, Levy about 10 interviews or 5–10 guerrilla users, Lemser 6–10 interviews followed by a survey. **Resolution:** small qualitative rounds establish what exists and why, never how common it is. Size things with quantitative data.
- **What counts as validation.** Levy and Lemser treat a few interviews or stated willingness to pay as validation or "facts". **Resolution:** treat such evidence as attitudinal and directional (Medium or Low confidence) unless behaviour corroborates it. [NNG]
- **Personas.**
  - Garrett invents details consistent with research.
  - Levy uses provisional personas as assumptions.
  - GOV.UK lists personas as a discovery output.
  - Lemser builds them from interviews.

  **Resolution:** personas summarize evidence. Without evidence they are labeled provisional, contain only checkable claims, and carry no invented quotes or statistics.
- **Risk ownership.** SVPG assigns feasibility to engineering and viability to product. **Resolution:** the skill identifies and weights all four risks, but marks feasibility and viability conclusions *Unknown* until the owners weigh in.
- **Effort in prioritization.** Torres excludes effort for opportunities; Garrett adds feasibility at scope. **Resolution:** no conflict; they apply at different stages.
- **Opportunity tree vs. simple framing.** Torres requires an outcome and customer stories first. **Resolution:** without them, do not build a tree; produce a problem statement and a plan to obtain the prerequisites.
- **When metrics apply.** HEART says metrics mainly evaluate launched products and do not replace formative research. **Resolution:** in discovery, define goals, candidate signals and baselines; never present metrics as validating a concept. Evaluating launched products, and the operational measurement plan, belong to `prototype-testing-analytics`.
- **Research ethics.** Levy endorses deceptive tactics, and the other sources say little. **Resolution:** this skill requires informed consent and honest disclosure. Privacy law and organizational policy are Tier 0 constraints.
- **Competitor analysis.**
  - Levy asks analysts to "determine the causes" of competitors' results and to pick the competitors that best support a recommendation.
  - Lemser warns against feature comparison.

  **Resolution:** use competitor data for descriptive claims only, and look for disconfirming cases.
- **UX Research's internal inconsistency.** The book's mapping of its three research focuses to project phases differs between its text and its tables. **Resolution:** use the definitions in the text; ignore the tables.

## 6. Access, licensing and limits

- **Books.**
  - The attached PDFs were read while building the skill (2026-10-20). The skill contains original paraphrase only: no chapters, passages, figures or templates are reproduced.
  - Page references are given only where verified; otherwise chapter and section.
  - The O'Reilly and New Riders titles are all-rights-reserved works. Do not add quotations from them to the skill.
- **Lemser, CC BY-SA 4.0.** Attribution: "Strategic Product Management © last updated September 2025 by Frank Lemser is licensed under CC BY-SA 4.0" (https://creativecommons.org/licenses/by-sa/4.0/).
  - This skill restates ideas in original wording and copies no text, figures or templates.
  - If text from the book is ever adapted into the skill, CC BY-SA's ShareAlike terms would apply to that adapted material.
  - "Open Product Management Workflow" is a trademark of its author. Creative Commons licences do not grant trademark rights, so do not use the name in a way that implies endorsement.
- **GOV.UK.** The site footer states that all content is available under the Open Government Licence v3.0, except where otherwise stated, © Crown copyright.
- **Web sources.**
  - Read through a fetch tool that returns processed text. Key definitions were cross-checked; re-verify wording before quoting externally.
  - Pages change: ProductTalk was modified 2026-09-29, and the GOV.UK planning page was updated 2026-10-15.
  - The ProductTalk, SVPG, NN/g and HEART texts are copyrighted; the skill paraphrases them.
- **HEART link anomaly.** At access time, the "Download" link on Google's publication page pointed to a non-Google host. It was not used; the paper was read from Google's own archive.
- **ISO.** Only the public abstract and the preview's clause headings were accessed. The normative text, definitions and Annex B conformance checklist were not.
