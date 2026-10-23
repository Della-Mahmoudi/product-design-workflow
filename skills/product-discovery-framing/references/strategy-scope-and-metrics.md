# Strategy, scope and metrics

Methods for connecting a problem to business goals, judging risk, setting scope and defining success. Read only the sections your route names.

**Contents**
1. Business goals and user outcomes
2. Value proposition
3. Competitive context
4. The four product risks
5. AI features at discovery level
6. Constraints and dependencies
7. Scope and non-scope
8. MVP reasoning
9. Prioritization
10. Goals → Signals → Metrics
11. Handoff to later design work

Source tags are defined in `source-map.md`. [SYN] marks this skill's own synthesis.

---

## 1. Business goals and user outcomes

- **Answer two questions explicitly.** What does the organization want from this product, and what do users want from it? Many product failures trace back to nobody answering one of them. [EUX Ch3]
- **Make product objectives explicit.** They should be specific enough to judge success by, but must not name the solution. [EUX Ch3]
- **Trace the chain.** Each link should connect to the one above it: [PT; SYN]
  - business outcome
  - product outcome (a user behaviour or attitude)
  - opportunity (a need)
  - candidate solutions

  A solution that cannot be traced up this chain needs a stated reason.
- **Label business goals by where they come from.** Goals written down (OKRs, strategy documents) are business facts. Goals that are only voiced are stakeholder input. [SYN]
- **When objectives conflict, ask for a ranking.** That ranking will drive every later trade-off. [EUX Ch4]

## 2. Value proposition

- **State it as one short sentence a customer could repeat:** what it is, for which segment, and which problem it solves. A value proposition without a severe, real problem behind it is worthless. [UXS Ch3]
- **Express value in the customer's terms:** time, money, risk or effort saved, or a new capability they want. Compare it with what they do today, including doing nothing. [SPM pp.121–122; UXS Ch6]
- **Check "why us".** Does it build on something this organization is unusually well placed to do, and can it keep doing so? [SPM pp.34, 71–72]
- **Treat it as a hypothesis** until people with the problem have shown that they value it. Validate the segment and the problem before the solution: [UXS Ch2–3]
  - If the segment is wrong, change the segment.
  - If the pain is wrong, change the problem.
- **Narrow the segment first.** A proposition aimed at "everyone" cannot be tested. [UXS Ch3; SPM p.85]

## 3. Competitive context

Use this section only when the user asks, or when the decision depends on it (differentiation, market entry, pricing). Otherwise one line about the relevant alternatives is enough.

**Who counts as a competitor** [UXS Ch4–5; SYN]
- **Direct:** the same proposition for the same users.
- **Indirect:** a similar proposition for other users, or a side offering that reaches the same users.
- **The current workaround, or doing nothing:** often the real competitor.
- **Non-competitors** can still suggest a differentiator.

**What competitor evidence can and cannot show** [UXS Ch5; SPM pp.73–74]
- **Can show:** what exists, positioning, pricing models, the baseline expectations users bring, public complaints in reviews, and gaps.
- **Cannot show:** whether users value a feature, whether it works for the competitor, or why the competitor built it. Treat competitors' traffic estimates and claims as unverified.

**Reasoning from a competitor's move**
- A competitor launching X is a reason to ask whether *our* users have the problem X addresses. It is not evidence that they do.
- Feature-by-feature parity races tend to produce over-engineering, and usually favour the market leader. [SPM pp.73, 77; UXS Ch10]
- Look for gaps beyond features: problems solved, segments served, business model, channels and message. [SPM pp.73–74]

**How much to do**
- **Light version (default):** 3–5 alternatives; what each solves and for whom; the gap; open questions.
- **Full competitive matrix and findings brief:** only on request. [SPM p.40; UXS Ch4–5]

## 4. The four product risks

**Definitions** [SVPG]
- **Value:** will customers buy it, or users choose to use it?
- **Usability:** can users figure out how to use it?
- **Feasibility:** can it be built with the time, skills and technology available?
- **Business viability:** does it also work for the business, sales and go-to-market, legal and contractual limits, acquisition and serving costs, monetization, brand?

**Assessing risk at discovery level**
1. **Rate each risk.** For the problem and each serious candidate direction, give High / Medium / Low, with the reason and the evidence, or the lack of it.
2. **Weight the risks for this context; they are rarely equal.** Value risk is usually the hardest, and viability is often underestimated. [SVPG; SYN] Typical patterns:
   - new behaviour or unproven demand → value
   - complex tasks or new interaction models → usability
   - new technology, data, integrations or AI → feasibility
   - regulated domains, pricing, channels, brand promises → viability
3. **Tackle the highest risks first,** before building anything, with the cheapest credible test. [SVPG; UXS Ch7]
4. **Respect who owns each risk.** Product leads own value and viability, design owns usability, and engineering owns feasibility. A designer can raise feasibility and viability questions, but conclusions need the owners' input; mark them *Unknown* until you have it. [SVPG]
5. **Add cross-cutting risks when relevant:** [GOV-D; SYN]
   - accessibility: excluding disabled users
   - ethics and harm: manipulative patterns, misuse
   - privacy
   - operational and support load

## 5. AI features at discovery level

Treat "add AI" as one candidate solution. Frame the user problem first (`problem-framing.md` §2), then check each area below. This section applies SVPG's four risks and this skill's evidence rules; no single source covers AI features, so label conclusions drawn from it as synthesis.

- **User value:** which task or decision does it improve, for whom, and by how much compared with a non-AI alternative? Is there evidence that users have the problem? [SVPG; SYN]
- **Uncertainty:** what happens when the output is wrong, inconsistent or unexplainable? What does an error cost the user and the business, and who catches it? Is a human review step or a fallback needed? [SYN]
- **Data and privacy:** what data is needed, does the organization have the right to use it, and what about consent and retention? Note the applicable regulation, and refer it to legal or privacy owners rather than concluding yourself. [SVPG; SYN]
- **Feasibility and operations:** data availability and quality, how well models perform on this task, latency, cost per use, monitoring, support and escalation. [SVPG; SYN]
- **Viability:** unit economics at expected usage, brand trust, liability and vendor dependence. [SVPG; SYN]
- **Evaluation:** how output quality would be judged and measured, alongside user outcomes. [HEART; SYN]
- **Competitive pressure:** competitors shipping AI is not evidence of user value. It may still be a real business concern, such as positioning or sales objections. Record it as stakeholder input and test it. [SYN]

**Stop at the frame.** Prompts, conversation flows and AI interface design belong to later stages.

## 6. Constraints and dependencies

Surface constraints early; hidden ones decide outcomes late. Check each area below and label every constraint *Fact*, *Assumption* or *Unknown*.

- **Technical:** platforms, legacy systems, integrations, data availability, performance.
- **Legal and regulatory:** privacy, consumer protection, sector rules, contracts.
- **Accessibility:** obligations and inclusion.
- **Business:** budget, deadlines, pricing, channels, partnerships, brand promise.
- **Operational:** support, content creation and upkeep, moderation, fulfilment. Content or features that nobody owns become gaps. [EUX Ch4 "Content Requirements"]
- **Organizational:** team skills, ownership, competing priorities.
- **Dependencies:** on other teams, vendors or decisions.

**Two warning signs** [EUX Ch8]
- **Design by default:** the experience mirrors internal structure or technology rather than user needs.
- **Design by fiat:** personal preference overrides needs and objectives.

**Separate real constraints from historical habits.** People close to a product often treat past choices as fixed. [EUX Ch4]

## 7. Scope and non-scope

- **Define what you are building, and what you are not.** Knowing what is out lets you judge new ideas against the scope instead of absorbing them. [EUX Ch4]
- **Trace every in-scope item to the target opportunity and outcome.** Anything that does not fit the strategy is out of scope. If a strong idea falls outside it, the strategy may need revisiting; say so explicitly. [EUX Ch4]
- **Write scope items as needs and success criteria, not interface mechanisms.** Each must be testable: it should be possible to show that it has not been met. [EUX Ch4 "Writing It Down"; SYN]
- **Keep a "not now" list.** For each item, give the reason it is out and the evidence that would bring it back. [EUX Ch4]
- **Solve with as little technology and as few features as possible.** Offering more of everything to everyone is over-engineering. [SPM pp.56, 99, 117]
- **Watch for scope creep.** Each addition looks small; together they break the timeline and the budget. [EUX Ch4]

## 8. MVP reasoning

**Be clear which MVP is meant.**

**Learning MVP:** an experiment that tests the riskiest assumption as cheaply as possible, often without building the product. [UXS Ch7; SYN]
- Common forms: a concept, a landing page, a concierge or manual service, a prototype.
- It needs a hypothesis, a measurable result, a time limit, and a decision rule agreed in advance.
- Be honest with participants. If a manual back end could mislead people, disclose it.
- If it becomes a controlled experiment (randomized comparison, sample size, exposure), hand its design to `prototype-testing-analytics`; discovery keeps the hypothesis and the decision rule.

**First-release MVP:** the smallest product that delivers the core value to the target segment and is usable, feasible and viable enough to learn from real use. [UXS Ch6–7; SVPG]
- It contains the differentiating "key experience" and little else.
- If you find yourself listing many "key" experiences, you have written a feature list.

**Justify any MVP with:**
1. The target segment and opportunity, from evidence or labeled as an assumption.
2. The riskiest assumptions, and how the MVP tests them.
3. What is in scope, each item traced to the opportunity and outcome.
4. What is out of scope, each item with a reason.
5. Success and failure criteria, set in advance (§10).
6. What result would make you expand, change course or stop.

**When asked for an MVP roadmap without validated evidence,** deliver an assumption-driven learning plan, not a dated feature schedule presented as if validated. [SYN; SPM p.134; UXS Ch3]
- State roadmap items as problems to solve, not features.
- Give every phase a signal and a decision rule agreed in advance, not just a question.
- Candidate scope may still be listed, as labeled hypotheses tied to the assumptions they test.

## 9. Prioritization

- **Agree the criteria, and their ranking, before scoring.** Otherwise priorities default to politics. [EUX Ch4]
- **Match the criteria to the stage:**
  - **Opportunities:** size and frequency, importance, dissatisfaction with current alternatives, urgency, strategic fit and market effect. Leave effort out at this stage. [PT; SPM p.58]
  - **Solutions and scope:** fit with objectives and user needs, feasibility, cost, risk reduction and dependencies. [EUX Ch4; SVPG]
  - **Research:** rank assumptions by how much the decision depends on them, weighed against how weak their evidence is. [PT; SYN]
- **Show evidence strength next to every priority.** A scoring model is only as reliable as its inputs. [SYN]
- **Prefer a short ranked list with reasons** to a large matrix.

## 10. Goals → Signals → Metrics

Use this to define what success should mean before a solution is chosen: the intended outcome, the success criteria, and a high-level goal → signal → metric chain. [HEART]

**Stop at that level.** Exact metric definitions, event taxonomies, instrumentation and tracking plans, funnel and retention reporting, experiment metrics and post-launch evaluation belong to `prototype-testing-analytics`. Hand the chain over (§11) instead of specifying it here.

1. **Goals:** what success means for users and for the product. Gather differing views and reach agreement. Goals for a feature can differ from goals for the whole product.
2. **Signals:** which user behaviour or attitude would show success or failure, and where the data comes from (logs, surveys). Choose signals that move only when the experience gets better or worse. Failure signals, abandonment, undo, errors, repeated attempts, are often easier to detect.
3. **Metrics:** turn the signals into trackable metrics. Normalize them (rates, per-user averages, cohorts) so that growth in user numbers does not look like improvement.

**HEART categories.** Use only those that fit, and decide on each explicitly:
- **Happiness:** attitudes such as satisfaction and perceived ease of use.
- **Engagement:** depth or frequency of involvement.
- **Adoption:** new users of a product or feature.
- **Retention:** users who keep coming back.
- **Task success:** effectiveness, efficiency and errors.

**Rules**
- **Avoid vanity metrics.** Page views, raw sign-ups, time on site and active-user counts do not show whether the experience improved. [HEART; UXS Ch9]
- **Set each metric's desired direction from the strategy.** Time spent should rise for an exploration product and fall for a quick task. [EUX Ch3]
- **In a funnel, pick the one key metric for each stage.** [UXS Ch9]
- **Pair each success metric with a guardrail** that would reveal harm elsewhere, for example, conversion up while refunds also rise. [SYN]
- **Use a baseline.** If none exists, say so, and make establishing one part of the plan. Never invent baselines or targets; propose a direction and a review date instead. [SYN]
- **Show how to set a number you don't have.** When a target or gate needs one, explain how the team can derive it, from break-even price, margin, runway or current rates, rather than supplying a figure. [SYN]
- **Decide in advance the threshold and the action it triggers.** If nobody would act on a metric, do not track it. [SPM p.102]
- **Metrics complement research; they do not replace it.** They are mainly for judging launched products, and should be triangulated with qualitative evidence. [HEART] Judging a launched product is `prototype-testing-analytics` work; in discovery, metrics only define what success should mean.

**Success criterion template:**
> **[Segment]** shows **[behaviour or attitude change]**, measured by **[metric]**, from **[baseline, or Unknown]** toward **[target or direction]** by **[time]**, without worsening **[guardrail]**.

## 11. Handoff to later design work

A discovery frame should give later stages (IA, flows, interaction, visual design, usability testing) what they need, and should leave them the decisions that are theirs. [EUX Ch2, Ch4–5]

**Hand over**
- The decision and the problem statement.
- Target users and their needs.
- The evidence, with confidence levels.
- The outcome, the success criteria and the ranked objectives.
- Scope, non-scope and the "not now" list.
- Constraints and dependencies.
- Open assumptions, and the research or tests planned for them.

**Leave to later stages:** navigation and categories, flows and screen sequences, layout, components and visual style. Discovery says what must be true and why; it does not say how the screens work. [EUX Ch4–5] Validation and measurement go to `prototype-testing-analytics`: usability-test plans, instrumentation and tracking plans, experiment designs and post-launch evaluation. Hand it the success criteria and the goal → signal → metric chain (§10).

**Mark the frame as revisable.** Later work may expose problems in strategy or scope, and those decisions should flow back. [EUX Ch2 "Building from Bottom to Top"; EUX Ch3; ISO principle heading: the process is iterative]
