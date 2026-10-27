---
name: prototype-testing-analytics
description: Plans and judges evidence for product-design decisions. Three modes - prototype validation (what to prototype, at what fidelity, testing a flow before build); usability tests and research studies (method choice, study plans, non-leading tasks, success criteria, generative or exploratory interviews once a research question is set, running scoped card sorts or tree tests, findings with severity and confidence); product measurement (UX and HEART metrics, goal-signal-metric, events, properties and tracking plans, funnels, retention, guardrails, A/B experiment design, causal claims). Use whenever someone asks "can users do X", "should we test this", "how do we measure", "which events do we need", "did the change cause", "how many users or how long for an A/B test", or hands over study findings or analytics to interpret, even without the word research. Not for choosing which problem or opportunity to pursue, redesigning IA, interactions or visuals, design systems, or QA of built tracking or UI.
---

# Prototype, Testing & Analytics

This skill decides what needs validating, what evidence would settle it, the smallest method that produces that evidence, and what the resulting evidence can and cannot support. It covers three kinds of work and keeps them distinct, because each produces evidence with different limits.

## Start from the question, not the method

Before proposing anything, write down the decision the evidence must inform, the question itself, and the question's type. Classify on the dimensions that matter: exploratory / generative / evaluative; behavioral / attitudinal; qualitative / quantitative; descriptive / comparative / causal; one-off / longitudinal. The type fixes the minimum valid method:

| Question | Type | Minimum valid method |
|---|---|---|
| What words do people naturally use for this? | generative, qualitative | interviews or open sorting in their own words, not a survey of our labels |
| Can people complete checkout with this prototype? | evaluative, behavioral, qualitative | task-based usability test on the prototype |
| How many people abandon checkout, and at which step? | descriptive, behavioral, quantitative | funnel analytics with precisely defined stages |
| Why are they abandoning? | explanatory | observation or interviews; analytics alone cannot answer it |
| Did the new checkout cause conversion to change? | causal, comparative | a valid experiment, or an explicit statement that no causal claim is possible |

Do not reach for usability testing, surveys, analytics or A/B tests because they are familiar. Pick the smallest method that can answer the question at the confidence the decision needs, and say what that confidence is.

A request that arrives as a method ("we should run a survey", "let's A/B test it") is a proposal, not a decision: recover the decision and the question, classify it, then confirm or replace the method. One question gets one method unless the decision truly needs more; do not inflate it into a multi-method programme.

## Three validation modes

| Mode | Question | Typical outputs | What it is not |
|---|---|---|---|
| A. Prototype validation | Can users understand and use the proposed experience before it is built? | prototype scope and fidelity, required paths and states, scenarios, tasks, comprehension checks, documented prototype limitations | product analytics |
| B. Usability evaluation | Where, how and why do users struggle with an experience? | study plan, participant criteria, task set, success criteria defined up front, moderation guidance, observation capture, findings with severity and confidence | causal experimentation |
| C. Product measurement and experimentation | What is happening at scale after release, and does a change affect the desired outcome? | goal-signal-metric map, metric definitions, event and tracking plan, funnels, retention, segmentation, guardrails, experiment spec and decision rule | an explanation of why (analytics shows what); a causal claim unless the design supports one |

One decision may need more than one mode, but every piece of evidence keeps the limits of the mode that produced it.

Generative and exploratory studies (needs, workflows, motivations, mental models, language, context of use) are planned with Mode B's study discipline once an explicit research question exists. Their findings describe the people studied; they never establish prevalence, population frequency or causes.

## Workflow

1. **Frame.** Name the decision, the question, its type and the mode. If the question is undefined, say so and propose the sharpest version you can; never pick a method for an undefined question. If what is unresolved is which problem or opportunity to pursue, or whether a feature belongs in the roadmap or MVP, that is framing, not an evidence question: route it (see Boundaries) and resume once it yields a research or measurement question.
2. **Inventory existing evidence.** Prior research, analytics, baselines, findings, constraints. Assess their quality before adding anything; valid existing evidence may already answer the question.
3. **Route.** Load the one reference the mode needs (table below). Load a second only when the request truly spans modes.
4. **Choose the minimum method**, the lowest prototype fidelity that still answers the question (Mode A), or the lightest study or instrument (B, C). Define success criteria, metric definitions or hypotheses before any result is interpreted.
5. **Produce only the artifacts the decision needs**, at the depth set in Adaptive output.
6. **State the limits**: what this evidence supports, what it cannot, what would raise confidence, and which other stage (IA, interaction design, visual design, engineering) must act on it.
7. **Stop** when the requested decision is sufficiently supported (see Stop conditions).

## Reference routing: load only what the question needs

| Request is about | Read | Do not load |
|---|---|---|
| what to prototype, which fidelity, how to validate a flow or concept, which method fits an unclear question | `references/prototype-and-method-selection.md` | analytics or experiment references |
| planning or moderating a usability or interview study, including generative or exploratory interviews and IA validation studies another stage has scoped; turning observations into findings; reviewing an existing study or its findings | `references/usability-testing-and-evidence.md` (add method selection only if the method itself is in doubt) | metrics or experiment references |
| analyzing supplied feedback, reviews, survey comments or feature-request records | `references/usability-testing-and-evidence.md` §22 | metrics or experiment references unless the evidence question also needs them |
| UX or product metrics, HEART, events, properties, tracking plans, funnels, retention, instrumentation requirements, reading analytics | `references/metrics-analytics-and-instrumentation.md` | usability-study artifacts |
| A/B tests, experiment design, causal claims, sample size or duration, reading experiment results | `references/experiments-and-measurement-quality.md` (add the metrics reference when the metrics are undefined) | moderator guides, prototype plans |
| which external source is authoritative, or the user wants citations | `references/source-map.md` | anything else |

Conditional sources: Baymard only for ecommerce flows, and only as risk hints or domain benchmarks, never as evidence about this product. Figma documentation only when prototype construction or capability matters. Storybook only for component-level implementation checks; it is not user research. Analytics-vendor documentation only when implementation syntax on a platform the product actually uses is required; never assume a platform. Do not browse any online source at runtime unless the user asks for current citations, tool syntax matters, or currentness materially changes the answer. Works without the original books; links are for optional verification.

## Source hierarchy and conflicts

- **Tier 0, product evidence**: real observations, existing research, verified event data, baselines, real experiment results, product, technical and privacy constraints. Highest authority for this product, but only after its quality is assessed. Product-specific is not the same as reliable.
- **Tier 1, normative methodology**: ISO 9241-11 (usability as effectiveness, efficiency and satisfaction for specified users, goals and context of use), NN/g method selection and usability-testing fundamentals, Google HEART and goal-signal-metric.
- **Tier 2, operational practice**: research planning, lightweight testing and study workflow, distilled into the references.
- **Tier 3, domain and tool sources**: Baymard, Figma, Storybook, analytics platforms. Loaded only when the context requires them.

When sources or evidence conflict: identify the decision; check whether the sources answer the same question; separate method guidance from product evidence; prefer direct, valid evidence about this product over generic advice, but never let product preference override a methodological validity problem; surface the uncertainty and name the minimum additional evidence that would resolve it. Do not average conflicting evidence into a fake consensus.

## Evidence rules

Never invent participants, quotes, observations, task outcomes, analytics figures, event data, experiment results or statistical significance. When evidence is missing, say what is missing and how to obtain it.

Keep these distinct and labeled: behavioral observation versus self-report; observed frequency in a small study versus population prevalence (4 of 5 participants is not 80% of users); association or a change over time versus causation; what happened (analytics) versus why (explanatory research); satisfaction versus usability; a prototype limitation versus a user failure; participant opinion, stakeholder opinion, heuristic judgment, benchmark data and generic best practice versus direct evidence about this product.

Findings follow Observation, then Finding, then Interpretation, then Recommendation, then Confidence. Measurement follows Goal, then Signal, then Metric, then Event, then Property, then Decision. Statistical terms (significant, p-value, confidence interval, power, required sample size, detectable effect) appear only together with the data and calculation that justify them.

## Adaptive output

- **Quick** ("should we test this now or wait?"): the question being answered, the recommended method, the minimum prototype or evidence needed, the critical caveat. No plan.
- **Standard** (one feature's usability test, a prototype validation, a metric definition, instrumentation for one feature, a small experiment proposal): only the artifacts that decision needs, each proportionate.
- **Deep** (formal study, usability benchmark, analytics redesign, instrumentation architecture, major experiment, cross-method validation): full plans, screener requirements, moderator guide, task set, success criteria, evidence templates, metric tree, tracking plan, experiment and analysis plans, limitations. Only when the stakes justify it.

Match depth to the request. A long document is not more rigorous than a correct short one.

## Critical quality gates

Flag or stop when any of these holds: the research question is undefined; the method cannot answer the question; a task reveals the target label, navigation item, feature or sequence; participants or results are fabricated; participant criteria do not match target users; success criteria are set after results; prototype dead ends would create artificial failures; observations are mixed with interpretation; qualitative counts are reported as population percentages; analytics are used to explain why; correlation is described as causation; a metric lacks numerator, denominator, population or time window; funnel stages are ambiguous; an event measures a click where the successful outcome could be measured; instrumentation cannot distinguish attempt from success; a plausible harm has no guardrail; experiment feasibility, exposure or unit is unaddressed; a sample size or duration is invented; significance is claimed without analysis; tracking relies on events known to be unreliable; privacy, consent or sensitive data is ignored; an automated accessibility scan is presented as accessibility validation; an implementation is reported as verified without being inspected; another stage's decision or redesign is done here instead of being routed.

## Boundaries and stop conditions

This skill owns the evidence question: what would answer it, how to collect it, and what the result can support. That includes generative and exploratory research once an explicit research question or decision exists, executing IA validation studies that `ux-architecture` has scoped, and the measurement contract (events, triggers, properties, metric definitions, tracking plans, experiment instrumentation requirements). It does not own implementation, engineering estimates, release coordination or product-management decisions.

When evidence shows another stage's work must change (users cannot find Billing because the hierarchy is unclear), report the evidence, recommend that stage review it, and do not redesign it here. Route instead of continuing when the unresolved work is:

| Unresolved work | Route to | This skill may still |
|---|---|---|
| which problem or opportunity to pursue; whether a feature idea is justified or belongs in the roadmap or MVP; pre-solution product-risk framing | `product-discovery-framing` | design and run the study once a research question exists |
| hierarchy, navigation, taxonomy, labels or findability structure must change; which IA question is risky enough to test | `ux-architecture` | write the protocol, criteria, tasks, capture and analysis for a card sort or tree test it scoped; report findings |
| behavior, state logic, feedback, recovery or async interaction must change | `interaction-design` | report the evidence chain and say what that stage should revisit |
| visual hierarchy, presentation or styling must change | `ui-visual-design` | the same |
| reusable component or token architecture must change | `design-systems-consistency` | the same |
| checking that a build, staging or code implements the approved tracking plan or design; Ready for Dev; handoff | `delivery-product-collaboration` | state the measurement contract the build must meet |

A recommendation names the owning stage and the problem to revisit ("interaction design should revisit how discoverable Retry is after an upload fails"); it never specifies the new behavior, state machine, focus order, hierarchy, layout or component. Never report an implementation as verified without inspecting it.

Stop when the requested validation or measurement decision is answered with its limits stated; when the inputs needed to go further are missing and have been named (for example baseline rate and expected effect before any sample-size figure); or when the next step belongs to another stage. Do not generate a research programme, a tracking plan, a moderator guide or an experiment plan the request did not need.
