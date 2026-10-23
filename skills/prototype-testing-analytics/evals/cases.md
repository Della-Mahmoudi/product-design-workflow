# Evaluation cases for `prototype-testing-analytics`

Eight cases. A to C target real failure modes of validation work: leading tasks and over-production (A), the causation trap in analytics (B), and invented statistics in experiment planning (C). D to H are boundary cases against neighbouring skills: opportunity framing that belongs elsewhere (D), generative research that belongs here (E), redesign after findings that belongs elsewhere (F), a measurement contract that belongs here (G), and implementation QA that belongs elsewhere (H). Run each prompt with the skill available, then grade against the criteria. "Unnecessary-work checks" catch outputs that are correct but over-built; they fail the case just as surely as wrong outputs do.

| Case | Topic | Should this skill trigger? | Primary owner |
|---|---|---|---|
| A | clickable checkout prototype validation | YES | `prototype-testing-analytics` |
| B | analytics causation trap | YES | `prototype-testing-analytics` |
| C | A/B sample size and duration without the required inputs | YES | `prototype-testing-analytics` |
| D | product opportunity framing | NO | `product-discovery-framing` |
| E | generative interview study for a set research question | YES | `prototype-testing-analytics` |
| F | redesign after usability findings | NO | `interaction-design` |
| G | tracking-plan definition | YES | `prototype-testing-analytics` |
| H | tracking implementation QA | NO | `delivery-product-collaboration` |

For cases where the skill should not trigger, grade the response as if the skill had been invoked manually: it routes to the primary owner, keeps any contribution of its own inside this skill's boundary, and does not do the owner's work.

---

## Case A: prototype usability test (Mode A → B)

### User prompt

"We finished a clickable prototype for a new checkout flow. Can you create a usability test? I mainly want to know whether users can complete checkout and understand delivery options."

### Expected behavior

- Classifies the request as evaluative, behavioral prototype validation with a comprehension component (delivery options), and names the decision it informs.
- Loads `prototype-and-method-selection.md` for fidelity and testability, then `usability-testing-and-evidence.md` for the study artifacts. Does not load the metrics or experiments references.
- Recommends a session format proportionate to the question (moderated sessions are the natural fit because comprehension probing is needed; remote or in person stated with a reason) and confirms that a clickable prototype is sufficient fidelity, provided it supports the full checkout path, all delivery options as real branches, and realistic content (prices, dates, addresses).
- Defines realistic participant criteria based on behavior (people who buy this kind of product online, device mix, returning versus new) and asks for or assumes the product context where it is missing, saying so.
- Writes scenario-based, non-leading tasks: the participant is given a buying goal and the information they would have; delivery options are probed through expectation-before-choice and understanding-after-choice questions, without naming the option labels or the steps.
- Defines success criteria and measures before testing: what "completed checkout" means in the prototype (the observable end state), critical versus non-critical errors, assistance levels, and the comprehension match for delivery options. Confidence and satisfaction, if included, are labeled attitudinal.
- Lists prototype limitations to check before sessions (dead ends, fake inputs, missing states such as address validation errors or payment failure, hotspot coverage) and a neutral moderator script for dead ends; states that failures caused by these will be logged against the prototype, not the participant.
- Gives moderation rules (no leading, clarification versus assistance, logging assistance) and an observation note structure, and specifies the evidence chain the findings will use.
- Ends with limitations (small qualitative sample, think-aloud effects, prototype realism) and a stop: the study plan is the deliverable; no analytics, no experiment, no redesign.

### Pass criteria

1. Tasks never reveal the target label, navigation item, feature name or step sequence (a task set that walks the participant step by step, "stop when it asks where to send it", "change the delivery and carry on to payment", leaks the sequence even without naming a label); delivery options are tested by comprehension probes, not by instructions to "select Express delivery".
2. Success criteria, including the definition of completion in the prototype and the comprehension measure, are stated before any mention of results.
3. Participant criteria are behavioral and plausible for an online checkout, with any assumption flagged.
4. Prototype limitations are enumerated and explicitly separated from user failures.
5. The session format and fidelity recommendation each carry a reason tied to the research question.
6. No participant results, quotes or percentages are invented; where results are discussed at all, they are described as a template.
7. The output is proportionate (Standard mode): a usable study plan, task set, criteria, moderation notes and limitations; not a multi-document research programme.

### Failure criteria

- Any task says exactly where to click or names the delivery option to pick.
- Participant results, quotes or completion rates are invented.
- The response generates analytics events, a tracking plan, or an A/B test.
- The response redesigns the checkout UI or proposes UI fixes before any evidence exists.
- Sample size is justified statistically or presented as population coverage.
- Satisfaction ratings are presented as the usability measure.

### Unnecessary-work checks

- Did it build a tracking plan, metric definitions or HEART mapping? (fail)
- Did it produce a full screener document, consent form text, and multi-week schedule when a one-feature study was asked for? (over-built; flag)
- Did it load or cite Baymard benchmarks as evidence about this product? (fail if presented as evidence; acceptable only as optional probe hints clearly labeled)
- Did it fetch Figma documentation or online sources without being asked? (flag)

---

## Case B: analytics causation trap (Mode C, interpretation)

### User prompt

"Checkout conversion dropped 18% after our redesign. Analytics prove the redesign caused it. Tell me what went wrong."

### Expected behavior

- Declines the causal conclusion politely and precisely: the data shows a temporal change associated with the release; it cannot by itself establish that the redesign caused the drop, and it cannot say what went wrong.
- Restates the 18% drop as a descriptive observation and asks what it is a drop in (metric definition: numerator, denominator, population, window; relative versus absolute; against which baseline and variability).
- Loads `metrics-analytics-and-instrumentation.md`; does not produce a usability-study plan or an experiment spec as the main output (may recommend a small observation study as the next step for why).
- Works through the interpretation discipline in order: instrumentation validity (did events, triggers, platforms or identity change with the release; reconcile against orders in the system of record), traffic composition (channel, campaign, device, country, new versus returning, bots), timing confounders (seasonality, pricing, promotions, outages, other releases), location of the drop (funnel stage and segment), magnitude against normal variability.
- Identifies the segmentation needed and the specific questions each cut answers.
- Distinguishes what analytics can show (where and for whom the drop is concentrated) from what explains it (observation of users on the affected step, session replays if available, error logs, support contacts), and recommends the minimum evidence to investigate why.
- Notes the possibility of a temporary post-redesign dip as one hypothesis among several, not as the answer.
- Explicitly avoids proposing UI fixes; states that design changes wait for evidence of the cause, and that if a cause is found in a stage this skill does not own, it routes there.

### Pass criteria

1. The response never states or implies that the redesign definitely caused the drop; it labels the claim as an association or temporal change.
2. It asks for or specifies the metric definition and baseline variability before interpreting the 18%.
3. It checks instrumentation validity as a first-order explanation.
4. It names concrete confounders and the segment cuts that would test them.
5. It separates "what happened" (analytics) from "why" (explanatory research) and recommends the minimum next evidence.
6. It proposes no UI changes.

### Failure criteria

- States the redesign caused the drop, or accepts "analytics prove" without challenge.
- Invents a UX cause ("users can't find the delivery options") as fact.
- Treats the before/after comparison as an experiment.
- Proposes specific UI fixes or a redesign.
- Invents numbers (segment percentages, baseline values) the user did not supply.
- Quotes benchmark or industry statistics from memory (for example an abandonment-survey percentage) as support; an external benchmark may appear only as a labeled probe hint without an unverified figure.
- Catalogues generic design "suspects" (or product-specific guesses the user did not supply) before the instrumentation, composition, timing, location and magnitude checks are done.

### Unnecessary-work checks

- Did it write a full usability test plan with tasks and screener? (over-built; a brief recommendation of an observation study on the affected step is appropriate)
- Did it draft an A/B experiment specification? (fail unless framed as a later option after the cause is understood, in one or two sentences)
- Did it generate a complete tracking plan or event taxonomy? (over-built; asking for the existing event definitions is appropriate)

---

## Case C: A/B test without enough inputs (Mode C, experimentation)

### User prompt

"We have version A and B of onboarding. Tell me how many users we need and how long to run the test. We don't have baseline conversion or expected effect size yet."

### Expected behavior

- Refuses to produce a sample size or duration, explaining that both are calculations whose inputs are missing: baseline value and variability of the primary metric, the minimum effect worth detecting, significance level and power, allocation ratio, eligible exposed units per week, and outcome lag; duration additionally depends on weekly cycles, novelty wash-out and seasonality.
- Loads `experiments-and-measurement-quality.md` (and may reference the metrics reference for metric definition). Does not produce a usability-study plan.
- Checks feasibility briefly: is there a causal question (yes), what is the unit, can users be assigned stably, is contamination plausible, is the change reversible, are there ethical concerns.
- Defines the experimental hypothesis in testable form with placeholders where the user must decide (the primary metric and its direction, population, mechanism).
- Proposes candidate primary metrics for onboarding with full definitions (for example, share of new sign-ups reaching a defined activation outcome within a window) and asks the user to choose; proposes guardrails (for example, early churn, support contacts, time to first value) with reasons.
- Identifies the experimental unit (new user or account), eligibility (new sign-ups from launch onwards, platform scope), assignment (random, stable, logged) and exposure (the point where A and B actually differ), and notes the dilution risk if exposure is logged upstream.
- Explains concretely how to obtain the missing inputs: pull the baseline from the defined metric over a comparable recent period; agree the minimum effect with the decision owner; then run the calculation, which the skill will do once the inputs exist.
- Produces the minimum useful experiment specification (hypothesis, unit, eligibility, assignment, exposure, primary metric, guardrails, segments, analysis window, stopping rule, decision rule) with the sample-size and duration rows marked as pending inputs.
- Mentions instrumentation validation (assignment and exposure logging, metric parity across arms, sample-ratio check) and the stopping rule (no peeking).

### Pass criteria

1. No numeric sample size and no duration is given, not even as a "rough" or "typical" figure.
2. Every missing input is named, with how to obtain it.
3. A testable hypothesis, candidate primary metric with a full definition, and at least one justified guardrail are present.
4. Experimental unit, eligibility, assignment and exposure are each specified.
5. The spec is minimal and marked where inputs are pending; statistical terms appear only as dependencies, never as claims.
6. The stopping rule and instrumentation validation are mentioned.

### Failure criteria

- Gives any arbitrary number such as "1,000 users per arm" or "about 5,000 users".
- Gives a duration such as "two weeks" or "one month" as the answer (describing duration constraints such as whole weekly cycles is fine; a figure is not).
- Claims or implies statistical confidence, power or significance for the proposed test.
- Omits exposure, unit or metric definition.
- Treats baseline and effect size as optional details rather than prerequisites.

### Unnecessary-work checks

- Did it produce a usability test plan or moderator guide? (fail)
- Did it generate a full tracking plan for all of onboarding? (over-built; defining the events for the primary metric and guardrails is appropriate)
- Did it write a long statistics tutorial? (over-built; a short explanation of why the inputs are required is appropriate)
- Did it fetch analytics vendor documentation without a platform being named? (fail)

---

## Case D: product opportunity framing (boundary, routes out)

### User prompt

"Our CEO wants AI recommendations because competitors have them. We don't know whether users need this or whether it belongs in the MVP. What should we do?"

### Should this skill trigger?

NO

### Primary owner

`product-discovery-framing`. The unresolved question is whether the opportunity is justified and whether it belongs in the MVP, not how to collect or evaluate a defined body of evidence. No research or measurement question exists yet.

### Expected behavior (if this skill is invoked manually)

- Identifies that the product decision must be framed first (problem, target users, evidence versus assumptions, product risks, MVP scope) and routes that work to `product-discovery-framing`.
- States in a sentence or two what this skill can contribute later: once framing produces an explicit research question (for example, how users currently find relevant items and where that fails them), it can design the study; once an outcome is chosen, it can define how to measure it.
- If it comments on the inputs at all, notes that competitor presence and an executive request are inputs to framing, not evidence of user need.
- Does not create an interview study, survey, usability test, tracking plan, metric definitions or experiment, and does not decide whether the feature belongs in the MVP.

### Pass criteria

1. Names `product-discovery-framing` as the owner and gives the reason (feature justification and MVP scope are framing decisions).
2. Contains no study plan, discussion guide, screener, task set, metric definition, tracking plan or experiment specification.
3. Does not answer whether AI recommendations belong in the MVP, in either direction.
4. Any mention of later evidence work is conditional on a framed research or measurement question and stays brief.
5. Invents no user needs, research findings, usage data or competitor facts.

### Failure criteria

- Produces an interview study or survey "to validate the need" before the decision is framed.
- Recommends an A/B test of AI recommendations, or defines engagement or conversion metrics for them.
- States that users need, or do not need, AI recommendations.
- Treats "competitors have them" as evidence of user need, or dismisses the request without routing it.

### Unnecessary-work checks

- Did it write the discovery frame itself (problem statement, opportunity map, risk matrix, MVP scope)? (fail: that is the owner's deliverable)
- Did it list several research methods "to consider"? (over-built; one conditional sentence is enough)
- Did it fetch competitor information or online sources? (fail)

---

## Case E: generative interview study (boundary, stays here)

### User prompt

"We've already decided that our next discovery question is: How do freelance designers currently find and evaluate project-management tools? Create the interview study to answer that question."

### Should this skill trigger?

YES

### Primary owner

`prototype-testing-analytics`. The research question is explicit, so designing, running and interpreting the study is this skill's work, even though the study serves discovery.

### Expected behavior

- Classifies the question as exploratory and generative, qualitative and descriptive, built on self-reported past behavior anchored in concrete recent episodes; confirms semi-structured interviews as the minimum valid method and says why a survey or a usability test would not answer it.
- Loads `usability-testing-and-evidence.md` (section 20, with the section 1 plan rows that apply) and, at most, `prototype-and-method-selection.md` for the classification. Does not load the metrics or experiments references.
- Asks for or states the decision the findings will inform, without making that decision.
- Defines behavioral participant criteria: freelance designers who searched for, evaluated, adopted or abandoned a project-management tool within a recent window, with quotas for the variation that matters; flags assumptions (the window, platforms, whether current customers are included).
- Provides an interview structure built around reconstructing recent episodes (what prompted the search, where they looked, whom they asked, what they compared, how they decided, what happened next), with open, neutral probes; every block traces to the research question or a learning goal.
- Keeps our product out of the guide: no naming, pitching or concept reactions, and no "would you use" or price questions.
- Defines evidence capture (participant codes, verbatim quotes, behaviors and artifacts kept apart from interpretation, recording consent) and analysis (observation cards, clustering across participants, counts within the study, contradicting cases).
- States the limits: findings describe the people interviewed; no prevalence, population frequency, willingness-to-pay or causal claims; recall is imperfect; if magnitude matters, it names the follow-up instrument instead of stretching the interviews.
- Stops at the study plan; findings go back to whoever owns the product decision.

### Pass criteria

1. Generative or exploratory qualitative classification, and interviews as the minimum valid method, with a reason.
2. Participant criteria are behavioral and recent, with assumptions flagged.
3. Questions are open, neutral and about past behavior; none leads toward our product or a feature, and no hypothetical-intent or yes/no question sits at the core of the guide.
4. Each question block maps to the research question or a learning goal.
5. Evidence capture and analysis are defined, with counts reported within the study only.
6. The qualitative limits are explicit, including that "several participants mentioned X" does not become "users generally want X".
7. No findings, quotes, themes or participant data are invented.
8. The output is proportionate (Standard mode).

### Failure criteria

- Decides whether the product should pursue the opportunity, or recommends features.
- Invents interview findings, quotes, personas or percentages.
- Replaces interviews with a survey "to validate" needs, or turns the study into a usability test of our product.
- Guide questions mention our product, pitch a concept, or ask "Would you use a tool that...?"
- Promises population-level conclusions (how common something is among freelance designers) from the interviews.

### Unnecessary-work checks

- Did it build a multi-method programme (diary study, survey and analytics) the request did not need? (over-built; naming one follow-up instrument conditionally is fine)
- Did it produce full consent-form text, incentive budgets and a multi-week recruiting schedule? (over-built; flag)
- Did it produce metrics, a tracking plan or an experiment? (fail)
- Did it fetch online sources? (flag)

---

## Case F: redesign after usability findings (boundary, routes out)

### User prompt

"Our usability study found that users repeatedly lose uploaded-file progress after one file fails. Redesign the upload interaction and define retry behavior."

### Should this skill trigger?

NO

### Primary owner

`interaction-design`. The evidence already exists; what is requested is new behavior (state logic, recovery, retry), which this skill does not own.

### Expected behavior (if this skill is invoked manually)

- May restate the supplied evidence in the Observation, Finding, Interpretation, Recommendation, Confidence chain, labeling what was supplied (a summarized finding, not raw observations) and what is missing (session counts, tasks, whether a prototype limitation was involved).
- Bases confidence only on what was supplied and does not turn "repeatedly" into a count or a percentage.
- Routes the redesign to `interaction-design`, with the recommendation in problem terms (for example, that preserving completed uploads and making recovery discoverable after a partial failure need revisiting).
- May offer, in one sentence, to plan validation of the redesigned behavior once interaction design has produced it.
- Does not define retry behavior, states, a state machine, error copy, focus handling or layout.

### Pass criteria

1. Names `interaction-design` as the owner of the redesign.
2. Contains no new behavior specification: no retry rules, state table, state machine, error messages or focus rules.
3. Any evidence summary keeps observation, finding, interpretation, recommendation and confidence separate.
4. No participant counts, percentages or quotes are invented, and confidence is not overstated.
5. Any follow-up offered by this skill is limited to validating the redesign later.

### Failure criteria

- Specifies how retry should work (per-file retry, automatic retries, queue persistence) or provides a state machine.
- Writes UI copy or error messages for the new design.
- Reports the finding as "most users" or with a percentage.
- Proposes an A/B test as the next step without a causal question.

### Unnecessary-work checks

- Did it write a full new usability test plan? (over-built; a one-sentence offer is enough)
- Did it define upload-error events or a tracking plan? (over-built unless asked)

---

## Case G: tracking-plan definition (boundary, stays here)

### User prompt

"Define how we should measure successful creation of a Saved Search. Give me the metric, event trigger and required properties."

### Should this skill trigger?

YES

### Primary owner

`prototype-testing-analytics`. Defining the measurement contract (metric, event, trigger, properties) is this skill's work; verifying a build against it is not.

### Expected behavior

- Works along Goal, Signal, Metric, Event, Property, Decision and loads `metrics-analytics-and-instrumentation.md` only.
- Defines the success event on confirmed creation (for example `saved_search_created`, fired when the system of record confirms the saved search exists) and separates it from the attempt (the submit action) when attempt-to-success is to be measured, naming both clearly.
- States the trigger precisely, including the confirming source; where that source is unknown, marks it as a dependency to confirm with engineering instead of assuming a server-side event.
- Defines at least one metric with numerator, denominator, population or eligibility, and time window (for example, creation success rate as confirmed creations over creation attempts for eligible users within a window, or adoption among users who ran a search with the feature available), and names the decision it serves.
- Lists required properties with a reason for each (an identifier for the saved search, entry point, platform, a filter count rather than raw query text), a deduplication rule for retries and double submits, and privacy notes (no raw search text, email or other personal data without justification).
- Specifies how the event should be validated as part of the contract, without claiming it exists.
- Does not invent baselines or targets; marks the target "to be set after baseline".

### Pass criteria

1. The success event fires on confirmed creation, not on a click; attempt and success are distinct if both are named.
2. The trigger is precise, and the system of record is named or explicitly marked as an open dependency.
3. The metric has numerator, denominator, population or eligibility, and time window.
4. Required properties are justified; there is no unbounded free text or personal data without justification; a deduplication rule is present.
5. The chain ends in a decision.
6. There is no claim that the event or properties are already implemented, and no invented baseline or target.

### Failure criteria

- Uses `save_search_clicked` (or any click) as the success measure.
- Includes raw query text, email or user names as properties without justification and constraints.
- Invents a target ("aim for 30% adoption") or a baseline.
- Reads, or claims to have inspected, implementation code or staging.
- Leaves "engagement" or "usage" undefined.

### Unnecessary-work checks

- Did it map all five HEART categories? (over-built)
- Did it produce an experiment specification or a usability test? (fail unless asked)
- Did it produce a tracking plan for all of search rather than for saved-search creation? (over-built)

---

## Case H: tracking implementation QA (boundary, routes out)

### User prompt

"The developer says `saved_search_created` is implemented on staging. Check whether the built implementation matches our approved tracking plan."

### Should this skill trigger?

NO

### Primary owner

`delivery-product-collaboration`. This skill defines the measurement contract; checking that the build implements it is implementation verification.

### Expected behavior (if this skill is invoked manually)

- Routes the verification to `delivery-product-collaboration`.
- If the approved tracking plan is supplied, restates the contract the build must meet for this event (trigger moment, source, required properties, deduplication); if it is not supplied, says the plan is needed and does not reconstruct or redefine it.
- Does not claim to have checked staging, code or event payloads, and does not report the implementation as correct or incorrect.
- Changes the tracking plan only if the request is to revise the contract itself, which is this skill's work and is stated as such.

### Pass criteria

1. Names `delivery-product-collaboration` as the owner of implementation verification.
2. Makes no verification claim and invents no observed payloads, property values or staging results.
3. Restates the contract only from what the user supplied; otherwise asks for the approved plan.
4. Does not redesign the event or the metric.

### Failure criteria

- States or implies "the implementation matches" or "verified" without inspection.
- Fabricates staging observations, logs or payloads.
- Rewrites the tracking plan or invents new properties.
- Produces a full implementation QA report (severity-rated parity findings), which is the owner's deliverable.

### Unnecessary-work checks

- Did it produce new metric definitions? (over-built)
- Did it propose a usability study or an experiment? (fail)

---

## Grading notes

- Grade on the final response the user would see, not on internal reasoning.
- "Invented" means any specific participant, quote, number, percentage, date or result the prompt did not supply and the response presents as actual rather than illustrative. Clearly labeled examples ("for example, if the baseline were 30%...") are acceptable only when used to explain a mechanism, never as the answer.
- A response that is correct but produces artifacts the request did not need fails the proportionality criterion; token efficiency is part of the skill's contract.
- Boundary cases are graded twice: whether the skill is selected at all (D, F and H should not select it; E and G should), and what it does if it runs anyway. Routing to the named owner while doing that owner's work still fails the case.
