# Metrics, analytics and instrumentation (Mode C, measurement)

Load this when the request is about UX or product metrics, HEART, goal-signal-metric mapping, analytics events and properties, tracking plans, funnels, retention, segmentation, guardrails, instrumentation quality, or reading analytics. For experiments and causal claims, load `experiments-and-measurement-quality.md` as well. Do not produce usability-study artifacts from here.

This reference defines the measurement contract: what should be measured, by which event, with which trigger and properties, and how it will be validated. If the intended product outcome is itself undecided (what success means for the product), settle that with `product-discovery-framing` first; this reference turns a chosen outcome into operational metrics. Verifying that a build implements the contract (inspecting staging, code or live payloads against the approved tracking plan) belongs to `delivery-product-collaboration`.

## 1. What analytics can and cannot answer

Analytics describes what happened, for whom, when and how often, at scale. It does not say why. It can locate a drop in a funnel and the segment where it is concentrated; it cannot distinguish confusion from disinterest from a broken button. Every analytics conclusion is therefore one of: a descriptive observation, an association, a segment difference, a temporal change, or a hypothesis for explanatory research. A causal claim requires an experimental design (experiments reference).

## 2. HEART, used selectively

HEART is a prompt list for user-centered goals, not a dashboard template:

| Category | Measures | Typical signals | Use only if |
|---|---|---|---|
| Happiness | attitudes: satisfaction, perceived ease, likelihood to recommend | in-product or post-task survey responses | the decision concerns how people feel, and behavioral measures alone would mislead |
| Engagement | frequency, intensity, depth of use per user | sessions per user per week, actions per session, breadth of features used | voluntary, repeated use is part of the value; often meaningless for tools used because work requires them |
| Adoption | new users starting to use a product or feature in a period | first successful use of the feature, accounts created and activated | the decision is about uptake of something new |
| Retention | users from one period still present in a later period | return within a window, cohort survival | ongoing value is the goal and the window is defined |
| Task Success | effectiveness, efficiency, errors | completion rate of a defined task, time to complete, error or retry rate | there is a definable task with an observable end state |

Start from the UX goal, then choose the categories that help the decision. One or two categories are normal. Producing five metrics because there are five letters is a failure of the method.

## 3. Goal, Signal, Metric, Event, Property, Decision

Every metric is built along this chain, and anything missing a link is not instrumented.

| Link | Write | Example |
|---|---|---|
| Goal | what users should be able to do or experience, and the product outcome it serves | users can efficiently return to useful saved searches |
| Signal | the behavior or attitude that would show success or failure; sensitive and specific to the goal; failure signals are often easier to see | saved searches are reopened and lead to results that are acted on; failure: created and never reopened, reopened and immediately abandoned |
| Metric | the normalized, trackable expression of the signal | saved-search revisit rate within 14 days of creation (users with at least one reopen / users who created a saved search) |
| Event | the precisely triggered record that feeds the metric | `saved_search_opened`, triggered when the server returns results for a saved-search request |
| Property | the attributes needed to compute, segment and validate the metric | `saved_search_id`, `age_days`, `result_count`, `entry_point` |
| Decision | what the team will do with the number | decide whether saved search creates repeat-use value worth investing in, or should be simplified or removed |

Do not instrument an event that has no decision at the end of its chain.

## 4. Metric definition specification

A metric without these fields is a word, not a measure. Fill what is relevant:

| Field | Content |
|---|---|
| Name | unambiguous, versioned if the definition changes |
| Purpose | the goal and decision it serves |
| Numerator | the counted outcome, with its event and conditions |
| Denominator | the eligible population or opportunity count |
| Population | who is included (all users, new users, a platform, a plan) |
| Eligibility | the condition that makes a unit countable (reached the step, had the feature available, was exposed) |
| Time window | per event, per session, rolling 7 or 28 days, cohort week; and the lag before a value is final |
| Event or source | the events, tables or surveys used, with their trigger definitions |
| Segmentation | the dimensions the decision needs (platform, new versus returning, acquisition channel, country, plan), chosen for purpose, not exhaustively |
| Baseline | the current value and its normal variability over a comparable period |
| Target | only if legitimately derived from baseline, variability and business need; otherwise "to be set after baseline" |
| Guardrails | metrics that must not degrade while this one improves |
| Known limitations | sampling, bot traffic, client-only events, identity gaps, attribution rules |

Vague metrics to reject until defined: "engagement", "usage", "conversion", "activation", "stickiness". Each needs the numerator, denominator, population and window stated.

Example:

- Name: checkout completion rate (v2)
- Purpose: effectiveness of the checkout flow; decision: whether changes to checkout help or harm completion
- Numerator: sessions with `order_confirmed` (server-side, payment authorized) within 60 minutes of `checkout_started`
- Denominator: sessions with `checkout_started` (first checkout step rendered with a non-empty cart)
- Population: all web and app sessions; exclude internal and bot traffic
- Window: daily, reported as 7-day rolling; final after 24 hours (late payment confirmations)
- Segmentation: platform, new versus returning customer, payment method, delivery option, country
- Baseline: last 8 weeks, weekday and weekend separately, with the observed range
- Guardrails: payment failure rate, refund rate within 30 days, support contacts tagged checkout
- Limitations: cross-device journeys break the session link; cart edits during checkout re-trigger `checkout_started` unless deduplicated per session

## 5. Funnels

A funnel is only as good as its stage definitions.

- Define each stage by an event with a precise trigger and an eligibility condition (a user is "in" stage 2 only if they were in stage 1).
- Fix the window between stages and the handling of re-entry, backward moves and multiple attempts (count by first attempt per session, by last, or by any).
- Decide the unit (session, user, order) and stick to it across stages.
- Separate "left the funnel" from "completed by another path" (for example, paid via saved payment shortcut).
- Report stage-to-stage drop with counts, not only percentages, and with the segment split the decision needs.
- A drop locates a problem; it does not explain it. Pair the location with session replays (if available and consented), error logs, and a small observation study.

## 6. Retention

State the cohort definition (what event makes someone a member, in which period), the activity definition that counts as "retained" (a meaningful action, not merely an app open, where the goal is value), the window (day 1, day 7, week 4, month 3) and whether it is strict (active in that period) or rolling (active at any point since). Compare cohorts of the same age. Retention changes lag the change that caused them; do not read a week-one shift as a verdict.

## 7. Segmentation

Segment for the decision: platform, new versus returning, acquisition source, plan or tier, country or language, accessibility settings when available and permitted, feature exposure. Segments that are too small produce noise; say so rather than reading patterns into them. A difference between segments is an association, not an explanation.

## 8. Guardrails

Add a guardrail where optimizing the primary metric could plausibly cause harm elsewhere: speed of checkout versus payment failures and refunds; sign-ups versus activation quality; engagement versus support contacts or unsubscribes; conversion versus returns. Define guardrails with the same rigor as the primary metric. Do not add them mechanically; each needs a named harm.

## 9. Baselines and variability

Before any target or threshold: obtain the baseline over a comparable period, look at its day-of-week and seasonal pattern, note the range of normal fluctuation, and check for instrumentation or release changes within the period. A change smaller than normal variability is not a change. A target without a baseline is a guess; say so.

## 10. Events and properties

Each event in a tracking plan needs:

| Field | Requirement |
|---|---|
| Name | consistent convention (`object_action`, past tense for completed outcomes), no synonyms for the same thing |
| Trigger | the exact condition, including where it fires (client or server) and the confirmation it waits for |
| Actor and context | user or account identifier where permitted; anonymous identifier otherwise; session and device context |
| Entity | the object acted on (order, saved search, document) with its identifier |
| Required properties | those the metric and its segmentation need |
| Optional properties | useful but not required; justified individually |
| Source | client, server, third party; which one is the system of record; if it is unknown, list it as a dependency to confirm with engineering rather than assuming one |
| Privacy constraints | no personal data unless justified and permitted; no free text that could contain personal data |
| Deduplication | rule for retries, double submits, re-renders |
| Related metric(s) | which metric consumes it; an event with none is removed |
| Validation | how it will be verified in QA and after release |

Measure the outcome, not the click, whenever the outcome is observable:

| Prefer | Over | Because |
|---|---|---|
| `saved_search_created` on server confirmation | "clicked Save Search" | the click can fail, double-fire or be abandoned; the metric is about searches that exist |
| `order_confirmed` on payment authorization | "clicked Place Order" | the decision is about completed purchases |
| `document_shared` when the share link is active | "opened share dialog" | opening is an attempt, not success |

Instrument the click too only when the attempt itself is the measurement (for example, attempt-to-success ratio as an error signal), and then name both clearly.

These examples assume a confirming system exists. When it is not known where success is confirmed (server, client after a success response, a third party), write the trigger as "when the system of record confirms creation", name the source as an open dependency, and do not invent server-side events or capabilities.

## 11. Tracking plan template

| Event | Trigger | Source | Required properties | Optional properties | Feeds metric | Privacy notes | Dedup rule | Validation |
|---|---|---|---|---|---|---|---|---|
| `checkout_started` | first checkout step rendered with non-empty cart | client, confirmed by server session | `session_id`, `cart_value`, `item_count`, `platform`, `is_returning` | `entry_point` | checkout completion rate | none personal | once per session unless cart emptied | QA script; daily count reconciliation with server sessions |

Keep the plan small enough that every row is owned, validated and consumed.

## 12. Tracking-plan quality checks

Reject or flag: click-only events where the outcome is observable; ambiguous triggers ("when the user engages"); duplicate events under different names; unbounded free-text properties; properties nobody will analyze; personal data without explicit justification and permission; client-only success events where server confirmation exists; metrics built on events known to be unreliable; events with no metric or decision; naming inconsistent with the existing taxonomy. Do not invent implementation details (SDK calls, schemas, identity stitching); state them as engineering dependencies to confirm.

## 13. Instrumentation validation

Before trusting any number: confirm each event fires once per intended trigger in QA across platforms; reconcile event counts against a system of record (orders in the database versus `order_confirmed`); check identity resolution across login and devices; filter bots and internal traffic; mark release dates and tracking changes on every chart; verify that properties are populated, not null; check sampling settings. A metric built on instrumentation that fails these checks is reported as unverified.

Specify these checks in the tracking plan's validation column as part of the contract, and apply the data checks (reconciliation, bot and internal-traffic filtering, null properties, sampling) when judging whether a number can be trusted. Confirming in staging or code that a build fires the approved triggers with the required properties is implementation verification for `delivery-product-collaboration`; never report an event as implemented or verified without that inspection.

## 14. Reading analytics: the discipline

Label every statement as one of: descriptive observation ("completion fell from X to Y between weeks 10 and 11"), association ("lower completion coincides with higher mobile share"), segment difference, temporal change, hypothesis ("the new address form may be failing on mobile"), or causal claim (allowed only with an experiment or a defensible quasi-experimental design).

When a metric moves after a change, work through before concluding anything:

1. **Instrumentation**: did the event definitions, triggers, platforms, sampling, identity or eligibility rules change with the release? Did a tag break? Compare against the system of record.
2. **Composition**: did the traffic mix change (channel, campaign, device, country, new versus returning, bots)? Recompute within segments.
3. **Timing**: seasonality, day of week, holidays, pricing or promotion changes, outages, platform or browser updates, competitor actions, other releases in the same window.
4. **Location**: which funnel stage and which segment carries the change; is it concentrated or diffuse?
5. **Magnitude versus baseline variability**: is the move outside the normal range?
6. Only then: hypotheses about the design, ranked, each with the explanatory evidence that would test it (session replays, error logs, a small usability study on the affected step, support tickets).

Valid: "Checkout completion fell after the release, concentrated in mobile sessions at the address step." Not valid without more: "The redesign caused checkout completion to fall." Never claim why from analytics alone.

## 15. Data quality

Document known gaps: ad blockers and consent refusals (under-reporting that differs by segment), cross-device breaks, late-arriving events, retries, time-zone handling, bot traffic, sampling in the analytics tool, schema drift. Report numbers with these caveats attached where they could change the decision.

## 16. Privacy

Collect the minimum; prefer identifiers over personal data; no free text that may carry personal data; respect consent state and regional rules; define retention; restrict access. Do not state legal conclusions; flag what needs privacy or legal confirmation (for example, tracking accessibility settings as a property).

## 17. Output templates

**Metric definition (Standard mode)**: the specification table in section 4, filled for each important metric, with guardrails and limitations, and the decision each serves.

**Measurement plan**: goals, then the goal-signal-metric-event-property-decision chain per goal (section 3), then the tracking plan rows (section 11), then validation steps (section 13) and engineering dependencies.

**Analytics interpretation**: the observation in descriptive terms; instrumentation check status; composition and timing checks; location of the change; magnitude against baseline; ranked hypotheses with the explanatory evidence needed for each; what the data cannot say.

Stop when the decision has its metrics defined or its observation correctly characterized. Do not build a usability study or an experiment unless the request asks for it.
