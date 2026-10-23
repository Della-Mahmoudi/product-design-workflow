# Experiments and measurement quality (Mode C, causal claims)

Load this for A/B tests, experiment design, any "did X cause Y" question, sample size or duration questions, and reading experiment results. Metrics used here must already be defined to the standard in `metrics-analytics-and-instrumentation.md`; load that reference when they are not.

## 1. Is this a causal question?

A causal question asks whether a change produces a difference in an outcome compared with not making the change. "Did the redesign cause the drop?", "Will the new onboarding raise activation?" are causal. "How many drop off?" is descriptive. "Which design do users prefer?" is attitudinal and comparative, not causal.

Only a design that controls who gets the change and compares against a concurrent control supports a causal claim. Observational data (before/after, users who used the feature versus those who did not) supports association at best, because the groups differ in ways other than the change.

## 2. Feasibility before any A/B recommendation

Do not recommend an experiment merely because two versions exist. Check:

| Check | Question | If no |
|---|---|---|
| Causal question | is the decision actually about the effect of a change on an outcome? | measure or observe instead |
| Assignable unit | can users (or accounts, sessions, devices) be assigned to arms consistently and kept there? | consider cluster or switchback designs, or a quasi-experiment |
| Enough eligible traffic | will enough units reach the exposure point within a reasonable horizon to detect an effect the business cares about? (requires inputs in section 9) | the experiment cannot answer the question; use qualitative evidence plus pre/post monitoring with explicit caveats |
| Measurable outcome | is the primary metric defined and instrumented in both arms identically? | define and validate instrumentation first |
| Contamination | could units in one arm see or be affected by the other (shared accounts, word of mouth, marketplaces, network effects)? | change the unit or design; interpret with caution |
| Clear exposure | is the moment a unit actually experiences the difference definable and logged? | the experiment will be diluted and underpowered |
| Ethics and risk | is it appropriate to expose real users; is the change reversible; are vulnerable users protected? | do not run it |
| Effect within horizon | will the effect show inside the test period (not months later)? | choose a leading metric with known linkage, or a longer design |
| Seasonality | would the test window be unrepresentative (holidays, campaigns, launches)? | move or lengthen the window |
| Guardrails | could the change harm something else that matters? | define guardrails before launch |

## 3. When an experiment is not feasible

Say so plainly, then recommend the strongest available alternative and its limits: a holdout group if assignment is possible but traffic is low (longer horizon); a staggered or switchback rollout for cluster-level changes; a pre/post comparison with the confounder checks from the analytics reference, presented as association only; a usability study to establish whether the change works for people at all. Never dress an observational comparison as an experiment.

## 4. Experiment specification

| Element | Specify |
|---|---|
| Hypothesis | "If we [change], then [primary metric] will [direction] for [population], because [mechanism]." Falsifiable, one primary outcome |
| Control | the current experience, unchanged for the duration |
| Treatment(s) | the exact change; one difference per treatment if you need to know what worked |
| Experimental unit | user, account, session, device, or cluster; the unit of assignment must be the unit of analysis |
| Eligibility | who can enter (new users, a platform, a country), decided before the data is seen |
| Assignment | random, stable per unit, with the allocation ratio; who holds the assignment logic; how it is logged |
| Exposure | the trigger that marks a unit as having actually experienced the difference; analysis is on exposed units, or on assigned units with the dilution acknowledged |
| Primary outcome metric | one, fully defined (numerator, denominator, population, window) and instrumented identically in both arms |
| Secondary metrics | explanatory metrics that help interpret the primary; not used to declare success |
| Guardrail metrics | outcomes that must not degrade beyond a stated bound |
| Segments | a short pre-registered list the decision needs; anything else is exploratory and labeled so |
| Analysis window | when measurement starts and ends per unit; lag for late outcomes |
| Sample-size dependency | the inputs needed and whether they exist (section 9) |
| Duration dependency | full weekly cycles, novelty wash-out, outcome lag, seasonality (section 9) |
| Stopping rule | fixed horizon, or a named sequential method; no peeking decisions outside it |
| Instrumentation validation | assignment logging, exposure logging, sample-ratio check, metric parity across arms, dry run |
| Risks | contamination, novelty, SRM, outage, concurrent releases, ethical exposure |
| Decision rule | what result leads to ship, iterate, or stop, including guardrail breaches, written before launch |

Instrumentation requirements belong in this specification. Confirming that a build actually logs assignment and exposure as specified is implementation verification (`delivery-product-collaboration`); the sample-ratio and metric-parity checks on collected data stay here, because they decide whether the result can be read.

## 5. Hypothesis quality

A usable hypothesis names the change, the metric, the direction, the population and the mechanism. "The new onboarding will be better" is not testable. "Replacing the five-step onboarding with a two-step version will raise the share of new sign-ups that complete a first project within 7 days, because fewer users abandon before reaching the editor" is.

## 6. Unit, assignment and exposure

- Choose the unit so that the experience is consistent (a user who sees both versions across devices is contaminated) and independent (shared accounts or teams violate independence).
- Assignment happens once and stays stable; re-randomization or opt-in breaks the comparison.
- Exposure is where the arms actually differ. Trigger analysis at exposure where possible; if assignment is logged far upstream of the change, most assigned units never experience it and the measured effect is diluted toward zero.
- A sample-ratio mismatch (the observed split differs from the intended allocation beyond chance) indicates a broken assignment or logging and invalidates the result until explained.

## 7. Metrics in experiments

The primary metric is chosen for sensitivity to the mechanism and relevance to the decision; it is defined and instrumented before launch and not changed afterwards. Guardrails are chosen for plausible harms and given bounds. Secondary metrics explain. Choosing the metric after seeing results, or choosing among many until one "wins", is not evidence.

## 8. Segments

Pre-register the few segments the decision needs (platform, new versus returning, region). Post hoc segment findings are hypotheses for the next experiment, not conclusions; with enough segments something will differ by chance.

## 9. Sample size and duration: inputs, not numbers

A sample-size or duration figure is a calculation that requires:

- the baseline value of the primary metric (rate, or mean and variance) in the eligible population;
- the minimum effect worth detecting, decided by the business (the smallest change that would alter the decision);
- the significance level and statistical power the team accepts;
- the allocation ratio between arms;
- the number of eligible units reaching exposure per day or week;
- the outcome lag (how long after exposure the outcome can occur);
- for variance-based metrics, the variance from historical data.

Without baseline and minimum effect, no figure exists; never invent one, and never quote a generic "1,000 users" or "two weeks". When inputs are missing, say which, how to obtain them (pull the baseline from the defined metric over a comparable period; agree the minimum effect with the decision owner), and that the calculation follows once they exist. A sample-size calculation is a dependency, not an estimate.

Duration also depends on covering whole weekly cycles, letting novelty or change-aversion effects wash out for existing users, allowing the outcome lag to elapse, and avoiding atypical periods. Running until the required sample is reached is a floor, not the only constraint.

## 10. Stopping rules

Decide before launch: a fixed horizon with one analysis, or a sequential method designed for repeated looks. Checking results repeatedly and stopping on a favorable read inflates false positives; so does extending a test because the result is not yet favorable. Pre-register the rule and the decision thresholds.

## 11. Validity threats

| Threat | What it is | Mitigation |
|---|---|---|
| Novelty and change aversion | existing users react to newness, then adapt | run long enough; look at new versus existing users separately |
| Seasonality and events | the window is unrepresentative | avoid or cover whole cycles; check calendar |
| Contamination and interference | units influence each other across arms | choose the unit to contain the effect; cluster designs |
| Sample-ratio mismatch | assignment or logging broken | check daily; halt until explained |
| Instrumentation asymmetry | metric captured differently per arm (a new component firing events differently) | validate parity before launch; reconcile with system of record |
| Concurrent changes | other releases, campaigns, pricing | log them; avoid overlap on the same surface |
| Survivorship and dropout | users leave one arm more than the other before the outcome | analyze on exposed units with dropout reported |
| Multiple comparisons | many metrics or segments inspected | one primary metric; pre-registered segments |
| Outcome lag | outcome occurs after the window | set the window to the lag |

## 12. Boundaries for statistical claims

Do not write "statistically significant", a p-value, a confidence interval, "power", "required sample size" or "minimum detectable effect" unless the data and the calculation exist and are stated. Report observed values with their uncertainty when an analysis was done; report "no analysis performed" when it was not. An observed difference without analysis is an observation, not a result. Small qualitative samples never feed these terms.

## 13. Interpreting results

Confirm validity first: sample-ratio check passed, exposure logged, metric parity confirmed, no concurrent releases, horizon reached as planned. Then read the primary metric against the pre-registered decision rule, check guardrails, and look at pre-registered segments. Then state what the result does and does not support: an experiment shows the effect of this change on this metric for this population in this period; it does not explain the mechanism (use qualitative research for why), and it does not transfer automatically to other populations or seasons. A null result with insufficient sample is "undetermined", not "no effect".

## 14. Output templates

**Quick** (is an experiment appropriate?): the causal question restated; the feasibility checks that pass or fail; the recommendation (experiment, alternative design, or measure first); the one critical caveat.

**Standard** (small experiment proposal): the hypothesis written out in the section 5 form, with placeholders where the user must decide; unit, eligibility, assignment, exposure; at least one concrete candidate primary metric written out in full (numerator, denominator, population, window), even when the final choice belongs to the decision owner, because a definition schema on its own is not a metric and leaves the user with nothing to measure; guardrails, each with its named harm; pre-registered segments; analysis window and stopping rule; instrumentation validation (assignment and exposure logging, metric parity across arms, sample-ratio check); the inputs still needed for sample size and duration, named explicitly; decision rule; risks.

**Deep** (major experiment): the full specification table, an analysis plan (validity checks, primary analysis, guardrail analysis, segment analysis, reporting format), instrumentation validation plan, rollout and rollback plan, and limitations.

## 15. Gates for this mode

Flag when: no causal question exists; the experimental unit, assignment or exposure is undefined; the primary metric is undefined or instrumented asymmetrically; sample size or duration is stated without its inputs; significance is claimed without analysis; guardrails are absent despite plausible harm; feasibility (traffic, contamination, ethics, seasonality) is unaddressed; results are read after peeking without a sequential method; an observational comparison is presented as causal; segment findings are reported as conclusions.
