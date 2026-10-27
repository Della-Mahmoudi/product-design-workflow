# Prototype planning and method selection (Mode A, and method choice for any mode)

Load this when the request is about what to prototype, at what fidelity, how to validate a flow or concept before build, or which method fits a question that is not yet clear. It does not cover running a study (see `usability-testing-and-evidence.md`) or measurement (see the metrics and experiments references).

## 1. Classify the question first

Write the decision, then the question, then its type. A question that cannot be classified is not ready for a method; sharpen it first (what would change in the design or roadmap depending on the answer?).

Two checks come before classifying. If the request arrives as a method ("we should run a survey", "let's A/B test it"), treat the method as a proposal: recover the decision and the question, then confirm or replace it. If the unresolved question is whether a problem or opportunity is worth pursuing at all (whether a feature is justified, whether it belongs in the roadmap or MVP), it is a framing question for `product-discovery-framing`, not yet an evidence question. Method selection resumes here once framing yields a research question ("how do power users currently discover relevant products, and where does that fail them?").

| Dimension | Ask | Consequence for method |
|---|---|---|
| Exploratory / generative / evaluative | Are we trying to understand a space, generate options, or judge a specific design? | Exploratory and generative questions need open methods (interviews, contextual observation, open sorting). Evaluative questions need something concrete to evaluate against tasks |
| Behavioral / attitudinal | Do we need what people do, or what they think and say? | Behavioral questions need observation or behavioral data. Attitudinal questions can use interviews or surveys, but opinions never substitute for observed behavior |
| Qualitative / quantitative | Do we need why and how to fix, or how many and how much? | Qualitative for diagnosis and comprehension; quantitative for prevalence, magnitude and comparison, which needs enough valid observations to support the claim |
| Descriptive / comparative / causal | Describe a state, compare alternatives, or attribute an effect to a change? | Descriptive needs measurement; comparative needs a controlled comparison; causal needs an experimental or quasi-experimental design (experiments reference) |
| One-off / longitudinal | Is the answer about first contact, or about change over time and repeated use? | Longitudinal questions (learnability, habit, retention) cannot be answered in one session |

Worked examples:

- "What terminology do users naturally use for saved filters?" Generative, qualitative, attitudinal with a behavioral check. Minimum: short interviews or an open card sort in the participant's own words; a survey offering our labels would only test recognition of our words.
- "How do freelance designers currently find and evaluate project-management tools?" Exploratory and generative, qualitative, self-reported past behavior anchored in concrete recent episodes. Minimum: semi-structured interviews (`usability-testing-and-evidence.md`, section 20); not a survey of feature ideas and not a usability test of our product.
- "Can users complete checkout with this prototype?" Evaluative, behavioral, qualitative. Minimum: task-based usability test on a prototype that supports the whole checkout path.
- "Do users understand the three delivery options?" Evaluative, comprehension. Minimum: in-task comprehension checks (ask what they expect to happen before they commit, observe the choice, then ask what they understood after), not a preference question.
- "How many users abandon checkout?" Descriptive, quantitative, behavioral. Minimum: funnel analytics with defined stages; a usability test cannot answer it.
- "Why are users abandoning?" Explanatory. Analytics can locate where; observation or interviews are needed for why.
- "Did the new checkout cause conversion to improve?" Causal. Needs a valid experiment or an honest statement that only an association can be shown.
- "Which of two layouts do users prefer?" Attitudinal preference, which is often the wrong question. Ask instead which layout they can use to reach the goal, then collect preference as secondary.

## 2. From question type to minimum valid method

| Question type | Minimum valid method | Stronger alternative (when the decision warrants it) | Not valid for this question |
|---|---|---|---|
| Needs, workflows, mental models, context of use (generative) | semi-structured interviews built on recent concrete episodes | contextual observation, field or diary study | surveys of our feature ideas; usability tests of our product; analytics |
| Concept comprehension ("do they get what this is for?") | concept test with a sketch or static screen, open questions before any explanation | moderated sessions across segments | surveys with leading descriptions; stakeholder review |
| Terminology / labels | open-ended elicitation, open card sort | tree test on the proposed structure | surveys of our labels; analytics |
| Flow completion ("can they get through it?") | task-based usability test on a clickable prototype covering the full path | benchmark study with defined metrics on a coded prototype | heuristic review alone; satisfaction surveys |
| Interaction behavior (gesture, control, micro-interaction) | prototype with that interaction working realistically (often coded or high-fidelity) | component-level checks plus moderated sessions | static wireframes |
| Where people struggle in the live product | moderated usability test on production | unmoderated remote at larger scale, plus session replays if available | analytics alone (shows where, not why) |
| Prevalence or magnitude ("how many, how often") | behavioral analytics with defined metrics | instrumented benchmark study | small qualitative samples |
| Comparison of two designs on an outcome | controlled experiment (experiments reference) | sequential experiments with guardrails | pre/post comparison presented as causal |
| Change over time (learnability, habit) | diary study or repeated sessions | cohort analytics after release | single session |

The minimum is the lightest method that produces evidence valid for the claim. Choosing lighter than that produces evidence that cannot support the decision; choosing heavier spends time and anchors the team on a false sense of rigor.

## 3. Behavioral versus attitudinal evidence

Behavioral evidence is what people did: paths taken, errors, hesitation, recovery, completion. Attitudinal evidence is what people report: expectations, preferences, satisfaction, confidence. Both are useful; they answer different questions and must be labeled as what they are.

- Self-report is limited by awareness, memory and social desirability. A participant who says "that was easy" after three recoveries supplies a happiness data point, not a usability one.
- Behavior observed under think-aloud and a facilitator's presence is not identical to natural unobserved behavior. Treat it as behavioral evidence with observation effects noted.
- Preference between designs is attitudinal. It is weak evidence of which design works. Collect it after task performance, never instead of it.
- Stated intent ("I would buy this") is not behavior and does not forecast conversion.

## 4. Qualitative versus quantitative

Qualitative methods observe directly, with small numbers, and explain why and how to fix. Quantitative methods measure indirectly at scale and say how many and how much. Rules that follow:

- A qualitative study's counts describe that study only ("4 of 6 participants"). They are never population estimates and never carry percentages into recommendations.
- A quantitative method needs definitions (population, eligibility, window, numerator, denominator) before any number means anything.
- Quantitative usability measurement (task success rates, times) is justified when a benchmark or comparison is the decision and the protocol can be held constant across enough valid sessions. It is not justified to make a five-participant study look scientific.
- Mixing is normal: analytics to find where, observation to find why, then measurement to confirm the fix at scale.

## 5. Moderated, unmoderated, lightweight

| Format | Choose when | Costs and risks |
|---|---|---|
| Moderated (in person or remote) | you need to probe, the prototype is fragile, tasks are complex, comprehension matters, or participants are hard to brief | slower per session; moderator effects; fewer sessions |
| Unmoderated remote | tasks are self-explanatory, the prototype is robust to free exploration, you need more sessions or geographic spread, or you need consistent protocol for metrics | cannot probe or rescue; technology failures; participants misread tasks; prototype dead ends become failures; quality screening of recordings needed |
| Lightweight / guerrilla / hallway | early, cheap, frequent rounds to catch major problems; the decision is "what is obviously broken?" | participants may not match the target; limited task depth; no observer access; grade findings on a curve and say so |
| Lab / in person | observation of physical context, devices or assistive technology; stakeholders must observe live | unnatural setting; cost; slow |
| Benchmark study | measuring effectiveness, efficiency and satisfaction against a baseline or competitor with a fixed protocol | needs enough valid sessions for the comparison, strict consistency, and no mid-study protocol changes |

Think-aloud suits moderated diagnosis. For timing-sensitive measures, prefer retrospective probing or silent completion with a post-task interview, because narration slows people down.

## 6. Prototype fidelity: lowest that answers the question

| Fidelity | Answers | Cannot answer | Typical cost of being wrong |
|---|---|---|---|
| Sketch / paper | concept comprehension, mental model, rough flow order, terminology reactions | interaction feel, visual hierarchy under real density, error handling | cheap; redraw |
| Static wireframe | layout priority, content needed, label comprehension, expectation at each step | navigation across steps, system responses | cheap |
| Clickable wireframe (low-fi linked screens) | flow completion, navigation, step sequencing, where people hesitate, branch choices | realism of content, visual affordance, data entry behavior | moderate |
| High-fidelity clickable prototype | affordance, visual hierarchy, trust and credibility reactions, near-real flow completion, comprehension of real content | real input validation, performance, real data variability, edge cases unless built | moderate to high; expensive to change |
| Coded prototype | real interaction mechanics, input handling, responsiveness, accessibility with assistive technology, data-driven states | scale behavior, long-term effects | high |
| Production experiment | effects at scale on real outcomes under real conditions | why anything happened | highest; real users affected |

Fidelity effects to account for:

- Rough visuals invite comments about polish and can hide affordance problems; realistic visuals invite feedback about color and brand and can make participants assume everything works.
- Lorem ipsum or obviously fake content prevents comprehension testing. Use realistic content wherever comprehension or decision-making is under test.
- Fake inputs (a field that accepts anything, a search that always returns the same result) change behavior. If data entry is part of the question, the prototype must handle at least the inputs participants are likely to try.
- A polished prototype of an unvalidated concept wastes effort and creates sunk-cost resistance to findings. Validate the concept at low fidelity first.

## 7. Prototype scope: only the routes and states the questions need

Do not prototype the entire product. Derive scope from the task list:

1. List the research questions and the tasks that test them.
2. For each task, enumerate the happy path, the plausible wrong paths participants will try, and the branches that materially change the experience (for example, delivery option chosen, guest versus signed-in).
3. For each screen on those paths, list the states required by the questions: empty, loading, error, validation, success, edge content (long names, many items, zero results). Include a state only if a question depends on it or its absence would create an artificial failure.
4. Decide how dead ends are handled: a neutral "not part of this prototype" screen is better than silence, and must be logged as a prototype limitation, not a failure.
5. Build and record a path map: which routes exist, which do not, which states are faked.

## 8. Prototype testability checklist (run before any session)

- Does it support every task end to end, including the step where success is confirmed?
- Are the critical branches represented, and do plausible wrong turns lead somewhere sensible rather than to nothing?
- Will fake limitations alter behavior (no typing, fixed search results, no back navigation, hotspots only on one element)?
- Are loading, error and system states present where a question depends on them?
- Is content realistic enough for comprehension to be tested? Are prices, names, dates, counts plausible?
- Is navigation realistic enough (global navigation present, not only the test path)?
- Could participants be tested on prototype limitations rather than the design (for example, failing because a hotspot is missing)?
- Is fidelity sufficient for the question and no higher?
- Do participants need credentials, sample data or a scenario to make sense of it, and is that provided in the task?
- Has someone outside the team completed the tasks in a dry run?

Document every meaningful limitation in the study notes before testing, and carry the list into the findings so that observed failures can be checked against it.

### Requested live comparison of alternatives

When a live comparison is requested and authoring is authorized, use an isolated prototype surface rather than modifying production. Name the meaningful difference between directions and compare them at their real scale in equivalent surrounding context, with comparable task, data and starting state unless that difference is itself under study. Keep harness controls distinct from the candidate UI; variant-switch effects must not bias the comparison. A replay control is useful only when motion needs inspection. Keep comparison controls keyboard-accessible and avoid unscoped character shortcuts that interfere with the prototype.

Verify the interactions being claimed, disclose fake paths, and preserve the requested fidelity and scope. No fixed variant count, prescribed picker styling, automatic integration or cleanup is required. The Human's selection is a direction choice, not evidence of usability superiority; use the existing stage checkpoint rather than adding a gate for each internal build or repair.

## 9. Concept, flow, interaction and comprehension validation

- **Concept validation**: show the least detailed artifact that conveys the idea; ask what it is, who it is for, what they could do here, what they would expect to happen next, before any explanation. Record expectations verbatim. Preference and desirability come last and are labeled attitudinal.
- **Flow validation**: a clickable path with realistic content; tasks phrased as goals; observe sequencing, hesitation, wrong turns, recoveries, and where people expect something that is not there.
- **Interaction validation**: the specific interaction must work for real (gesture, drag, inline edit, multi-step control). Static or linked screens cannot validate it; a coded or high-fidelity interactive prototype can.
- **Comprehension checks**: ask what a label, option or message means and what will happen if they choose it; ask before the commit step, then observe what they choose, then ask afterwards what happened. Disagreement between stated expectation and actual outcome is the finding.

## 10. Minimum valid evidence per decision

| Decision | Minimum valid evidence |
|---|---|
| Proceed to interaction design on this concept | concept comprehension observed with target users at low fidelity; the main misunderstanding, if any, is named |
| Proceed to build this flow | flow completion observed with target users on a prototype that supports the full path; critical failures resolved or consciously accepted; prototype limitations listed |
| Choose between two flows | both tested with comparable tasks and participants, order counterbalanced where feasible, judged on observed completion and errors first and preference second |
| Ship a change to a live flow | usability evidence on the change plus post-release measurement defined before launch (metrics reference); a causal claim only with an experiment |
| Claim an accessibility outcome | sessions with assistive-technology users and keyboard-only flows, in addition to any automated checks |

## 11. Documenting prototype limitations

Keep a limitation log with four columns: limitation, which tasks it touches, how a participant might hit it, how the moderator will handle it (neutral redirect script). Every finding later cites this log so that a failure caused by the prototype is never reported as a design failure.

## 12. Output template for a method recommendation (Quick mode)

- **Decision this informs**
- **Question** and its type
- **Mode** (A, B, C) and **recommended method**, with the reason it is the minimum valid one
- **Minimum prototype or evidence needed** (fidelity, paths, states, content realism; or the existing data that already answers it)
- **What this will and will not tell you**
- **Critical caveat** (the one thing most likely to invalidate the result)

Stop there unless the request asked for a plan.
