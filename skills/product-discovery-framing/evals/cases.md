# Evaluation cases for `product-discovery-framing`

Human-readable QA contract for `product-discovery-framing`. Each case states whether the skill should trigger, what it should do, and how to grade the output. Cases 1–4, 9 and 10 should trigger the skill. Cases 5–8 should not; their criteria grade boundary behavior when the skill is invoked manually. Trigger rates are measured separately, in the trigger-testing phase.

Cases 9 and 10 extend the required set. Case 9 supplies the ten feature ideas that Case 3 omits, so that producing scope and non-scope can be graded. Case 10 is the framing half of the metric boundary that Case 5 tests from the diagnosis side.

"Unnecessary-work checks" catch output that is correct but over-built; they fail a case as surely as wrong output does. `evals.json` holds the same cases under the same ids.

---

## Case 1, Competitor-driven AI request

### User prompt

"Our CEO wants AI recommendations because all our competitors have them. We don't have user research yet. What should we build?"

### Should this skill trigger?

YES.

### Expected behavior

- Routes to `problem-framing.md` §1–3, then `strategy-scope-and-metrics.md` §4–5 (the AI-feature row). May use `research-and-evidence.md` §7 for the research recommendation.
- Leads with the reframed decision (whether and how to invest in solving a user problem, with AI recommendations as one candidate), not with a feature plan.
- Labels the CEO's request **Stakeholder input**. Treats competitor adoption as context and, at most, as a business concern to test (positioning, sales objections), never as evidence of user need.
- States the underlying problem as a hypothesis with an affected person and no solution built in; marks user evidence *Unknown*, since no research exists.
- Separates the business context that is known from the assumptions (users struggle to find relevant items; recommendations would help; the data can support them).
- Names value risk (unproven demand) as dominant and gives the AI checks that matter here (data availability and rights, the cost of wrong outputs); leaves feasibility and viability conclusions *Unknown* until their owners weigh in.
- Ranks the riskiest assumptions.
- Recommends the minimum discovery evidence: existing evidence first (search and browse logs, support tickets, sales notes), then a small round of interviews about recent occurrences. Each activity names the decision it informs and a result that would change it.
- Answers "what should we build" honestly: nothing yet; the next step is evidence, and AI recommendations stay one candidate among others (better search, curated collections, doing nothing).

### Pass criteria

1. The CEO's request is labeled Stakeholder input, or is explicitly described as a request rather than evidence of user need.
2. Competitor adoption is treated as context, not user evidence, including in the summary and closing lines.
3. The problem statement contains no solution, and AI recommendations appear as one candidate among at least two.
4. At least two riskiest assumptions are named, and value risk is identified as dominant, with a reason.
5. The recommended discovery evidence names the decision it informs and a result that would change that decision.
6. No user data, percentages, market sizes, competitor results or baselines are invented.

### Failure criteria

- Designs the recommendation experience: placement, UI, ranking algorithm, prompts or conversation.
- States or implies that users want or need AI recommendations.
- Presents a build plan, specification or dated roadmap as if validated.
- Invents numbers or research findings.
- Stops at "do research first" without framing the problem.

### Unnecessary-work checks

- No full competitive matrix (not requested, and the decision does not depend on one).
- No opportunity solution tree (there is no agreed outcome and no customer stories).
- No personas, tracking plan, experiment design or metrics dashboard.
- Stays within a standard frame (roughly 800 words or fewer).

---

## Case 2, Personas without research

### User prompt

"Create personas for our B2B admin product. We don't have any user research yet."

### Should this skill trigger?

YES.

### Expected behavior

- Routes to `problem-framing.md` §4 and `research-and-evidence.md` §5–6.
- Says plainly that without research it can offer only provisional personas or segments, and that they summarize assumptions, not evidence.
- Defines provisional segments by role, responsibility or behaviour (for example, the admin who configures the product, the buyer or approver, the end users affected by admin decisions), keeping buyer and user apart where they differ. Every attribute is labeled Assumption and written so that it could be checked.
- For each provisional persona, names the observable evidence that would confirm or replace it.
- Proposes minimum validation: existing evidence first (support tickets, admin activity logs, sales and onboarding notes), then a small round of interviews per segment, screened on behaviour. Names the decision the personas will serve, or asks for it if it blocks.

### Pass criteria

1. Every persona or segment is explicitly labeled provisional or assumption-based.
2. There are no invented quotes, ages, genders, salaries, percentages or "research shows" claims.
3. Segments are defined by role, behaviour or problem, not by demographics.
4. Each provisional persona lists the evidence that would confirm or replace it.
5. A minimum validation step is proposed and tied to a decision.

### Failure criteria

- Any persona contains a fabricated quote, demographic fact, statistic or claimed finding.
- Personas are presented as research-based.
- Refuses outright without offering provisional segments or a validation path.

### Unnecessary-work checks

- No more segments than there are distinct sets of needs (no batch of five or more near-identical personas).
- No decorative detail: photos, hobbies, life stories.
- No journey maps, flows, IA or UI.
- No research programme beyond the minimum validation.

---

## Case 3, MVP scope

### User prompt

"We have ten feature ideas for the first release. Help me decide what belongs in the MVP."

### Should this skill trigger?

YES.

### Expected behavior

The ten ideas are not in the prompt. Case 9 grades the same request with the ideas supplied.

- Routes to `strategy-scope-and-metrics.md` §1–2 and §6–9, with §10 for success criteria.
- Does not invent the ten ideas or guess their content.
- Asks once, briefly, for the blocking inputs (the ten ideas, the target segment and the intended outcome) while still giving the frame it will apply: intended outcome → target opportunity → riskiest assumptions → in-scope items traced to the opportunity → out-of-scope items with reasons → a "not now" list with what would bring each item back.
- Distinguishes a learning MVP from a first-release MVP, says which one the question implies (first release), and says when a learning MVP should come first.
- Says the prioritization criteria will be agreed before scoring, with evidence strength shown next to each priority.

### Pass criteria

1. No feature ideas, users, numbers or evidence are invented.
2. The missing list (and the outcome and segment, if unknown) is requested as blocking input, in no more than a few questions.
3. The intended outcome and target opportunity are named as the basis for scope.
4. Learning MVP and first-release MVP are distinguished.
5. The response explains how scope and non-scope will be decided: each in-scope item traced to the opportunity, each out-of-scope item given a reason.
6. Any assumption the response proceeds on is labeled.

### Failure criteria

- Fabricates a list of ten features, or ranks imaginary ideas.
- Turns the answer into UI, flows or screen designs.
- Recommends scope by effort alone, or by what is most requested.

### Unnecessary-work checks

- No generic MVP essay beyond what the decision needs.
- No scoring-matrix template, roadmap or opportunity solution tree.

---

## Case 4, Feature request disguised as a problem

### User prompt

"Users need a chatbot in account settings. Help me frame the requirement."

### Should this skill trigger?

YES.

### Expected behavior

- Routes to `problem-framing.md` §1–5, chiefly §2.
- Identifies "chatbot" as a proposed solution: the statement names a technology and can be met only one way.
- Labels "users need" as Stakeholder input or Assumption, since no user evidence was provided.
- Recovers candidate underlying problems as hypotheses: users cannot find or understand a setting, cannot complete a task (billing, cancellation, security), or contact support about settings; the business may want lower support cost.
- Writes a problem statement with an affected person and no solution, with the evidence marked *Unknown*.
- Keeps the chatbot as one candidate among others (clearer settings, search within settings, contextual help, human support), named at frame level only.
- Names the evidence needed and the decision it informs: support tickets and chat logs about settings, search logs within settings, settings-page analytics as existing evidence, then a few observations or interviews about recent occurrences.
- Names the dominant risk (value: is there a real, frequent problem?) and adds AI checks only briefly, if the chatbot stays a serious candidate.

### Pass criteria

1. "Chatbot" is explicitly identified as a proposed solution, not a requirement or need.
2. The problem is restated with an affected person and without the solution.
3. The chatbot is kept as one candidate among at least two.
4. "Users need" is treated as unverified (Stakeholder input or Assumption).
5. The evidence needed is named, together with the decision it informs.

### Failure criteria

- Writes chatbot requirements: intents, conversation flows, UI placement, model or NLP specifications.
- Accepts "users need a chatbot" as a validated requirement.
- Invents ticket volumes, usage figures or user quotes.

### Unnecessary-work checks

- No full AI feasibility analysis; at most a short AI risk note.
- No IA proposal for the settings area.
- No opportunity solution tree or personas.

---

## Case 5, Post-launch analytics diagnosis

### User prompt

"Checkout conversion dropped 18% after our redesign. Analyze the analytics and tell me whether the redesign caused it."

### Should this skill trigger?

NO. Primary owner: `prototype-testing-analytics`.

The description should not capture this diagnostic request. `product-discovery-framing` becomes relevant only if the request is explicitly to frame the product problem before investigating it (Case 10).

### Expected behavior (if invoked manually)

- Recognizes post-launch analytics diagnosis and a causal question: the routing table's diagnose-or-measure row and the validation stop condition.
- Stops and hands the task to `prototype-testing-analytics`, saying why in a sentence or two.
- May note that a drop after a change shows a sequence, not a cause, and may offer to frame the product problem first, but does not produce that frame unasked.
- Does not run `research-and-evidence.md` §8 as a diagnosis.

### Pass criteria

1. Names `prototype-testing-analytics` (or validation and measurement work) as the owner.
2. Does not claim that the redesign did or did not cause the drop.
3. Performs no analytics diagnosis: no segment or funnel-step analysis, no instrumentation audit, no experiment, holdout or sample-size design.
4. Anything offered from this skill is limited to framing (observation vs. cause) and is offered, not produced at length.

### Failure criteria

- Produces a diagnostic plan, a segment analysis, an A/B or holdout design, or a sample-size estimate.
- Asserts or implies causation.
- Invents analytics figures (baseline conversion, traffic, segment numbers).

### Unnecessary-work checks

- No discovery frame, personas, opportunity tree or MVP.
- A short routing response, not a report.

---

## Case 6, Usability test

### User prompt

"We finished our checkout prototype. Create the usability test and moderator guide."

### Should this skill trigger?

NO. Owner: `prototype-testing-analytics`.

### Expected behavior (if invoked manually)

- Recognizes prototype validation and usability-study planning (the validation stop condition).
- Stops and routes to `prototype-testing-analytics`.
- At most, offers the discovery inputs that study would use, if a frame exists: target users, success criteria, riskiest assumptions.

### Pass criteria

1. Routes the task to `prototype-testing-analytics`.
2. Produces no tasks, scenarios, moderator script, screener or study plan.
3. Any discovery input mentioned is limited to the handover items (users, success criteria, assumptions).

### Failure criteria

- Writes any part of the usability test or moderator guide.
- Invents participant results or completion rates.

### Unnecessary-work checks

- Does not re-frame the checkout problem unasked.
- No discovery research plan.

---

## Case 7, Information architecture

### User prompt

"Organize these 80 settings into navigation categories."

### Should this skill trigger?

NO. Owner: `ux-architecture`.

### Expected behavior (if invoked manually)

- Recognizes information-architecture work (the design-work stop condition).
- Stops and routes to `ux-architecture`. May name what discovery would hand over (user groups, top tasks, evidence) if that helps the next stage.

### Pass criteria

1. Names `ux-architecture` (or IA work) as the owner.
2. Proposes no categories, groupings, labels, sitemap or navigation model.
3. Does not design a card sort or tree test.

### Failure criteria

- Groups or labels the settings.
- Produces a navigation structure or sitemap.

### Unnecessary-work checks

- No unrequested discovery frame, personas or research plan.

---

## Case 8, Interaction behavior

### User prompt

"Define loading, retry, error and cancel behavior for this file upload flow."

### Should this skill trigger?

NO. Owner: `interaction-design`.

### Expected behavior (if invoked manually)

- Recognizes an interaction-behavior specification (the design-work stop condition).
- Stops and routes to `interaction-design`.

### Pass criteria

1. Names `interaction-design` (or interaction-behavior work) as the owner.
2. Defines no states, transitions, retry rules, timeouts, error messages or cancel behavior.

### Failure criteria

- Specifies any loading, retry, error or cancel behavior.
- Writes UI copy for upload states.

### Unnecessary-work checks

- No discovery frame or risk analysis of the upload feature.

---

## Case 9, MVP scope with the ideas supplied (extends Case 3)

### User prompt

"We're building an invoicing tool for freelance designers and developers. Launch is in 10 weeks with 3 engineers. Our ten ideas for the first release: 1) create and send invoices, 2) online card payments, 3) automatic payment reminders, 4) recurring invoices, 5) multi-currency, 6) expense tracking, 7) time tracking, 8) client portal, 9) tax reports, 10) a mobile app. We interviewed 6 freelancers: all 6 said chasing late payments is their biggest headache, and 2 asked for time tracking. Help me decide what belongs in the MVP."

### Should this skill trigger?

YES.

### Expected behavior

- Routes to `strategy-scope-and-metrics.md` §1–2 and §6–9, with §10 for success criteria.
- Names the intended outcome and target opportunity from the evidence (getting paid on time, with less effort spent chasing payments) and gives its confidence: 6 of 6 interviews agree, but the sample is small and the evidence attitudinal (Medium at most), so it says nothing about prevalence.
- Treats "2 asked for time tracking" as a request signal, not a validated need.
- Says this is a first-release MVP, and when a learning MVP would come first.
- Traces each in-scope item to the target opportunity (the core get-paid experience). Gives each out-of-scope item a reason and, where useful, the evidence that would bring it back.
- Weights the risks: value (will freelancers switch from their current tools?), viability (payment fees, compliance), and feasibility of payments and reminders in 10 weeks with 3 engineers, which stays *Unknown* or an assumption until engineering confirms.
- States success and failure criteria as behaviour or outcome changes, with baselines *Unknown* and a way to derive targets. Leaves operational measurement (events, tracking plan) to `prototype-testing-analytics`.

### Pass criteria

1. Every in-scope item is traced to the stated target opportunity or outcome.
2. Every out-of-scope item has a reason.
3. Interview evidence is reported as counts ("6 of 6", "2 of 6"), never as percentages or prevalence.
4. Feasibility within 10 weeks and 3 engineers is labeled *Unknown* or Assumption, pending engineering input.
5. Success criteria describe a behaviour or outcome change, not "shipped X"; no baseline or target is invented.
6. The response says which MVP is meant (learning or first-release).

### Failure criteria

- Converts the interviews into a percentage ("100% of freelancers…") or a claim about the market.
- Justifies scope by "most requested" or by competitor parity.
- Invents baselines or targets (for example, "cut days-to-payment from 45 to 30").
- Produces screens, flows or UI.
- Produces a tracking plan or an event list.

### Unnecessary-work checks

- No opportunity solution tree, personas, competitive matrix or dated roadmap.
- No scoring matrix with invented weights.

---

## Case 10, Framing a metric change before investigation (pairs with Case 5)

### User prompt

"Checkout conversion dropped 18% after our redesign last month. Before we spend money investigating, help us frame the product problem: what do we actually know, what are the possible explanations, and what decision are we facing?"

### Should this skill trigger?

YES. The request is explicitly to frame the problem before investigating; diagnosis is not asked for.

### Expected behavior

- Routes to `research-and-evidence.md` §6 and §8 (the routing table's frame row, not the stop row).
- States the observation as reported (an 18% drop after the redesign), labels its source, and notes that a sequence is not a cause.
- Labels the missing inputs *Unknown*: baseline and normal variation, volume, where the drop is concentrated, measurement changes.
- Lists the rival explanations as hypotheses (the design change, a defect, a measurement change, a traffic-mix shift, external factors), each with the cheapest check that would support or rule it out. The checks are named, not run.
- Frames the decision (roll back, partial rollback, wait for evidence) and the evidence that would justify acting in full now.
- Hands the investigation (diagnosis, instrumentation checks, any controlled comparison) to `prototype-testing-analytics`.

### Pass criteria

1. Does not claim that the redesign caused, or did not cause, the drop.
2. Keeps the observation separate from candidate causes, and labels the causes as hypotheses.
3. Names at least four rival explanations, including a measurement change.
4. Labels missing history, volume and segment data *Unknown* instead of estimating them.
5. Frames the pending decision, including reversible options.
6. Hands the investigation itself to `prototype-testing-analytics`.

### Failure criteria

- Performs the diagnosis: analyzes data, computes significance, specifies events, designs an A/B test or holdout, or estimates a sample size.
- Invents baseline conversion rates, traffic volumes or segment numbers.
- Proposes UI fixes for the checkout.

### Unnecessary-work checks

- No personas, opportunity tree, competitive analysis or MVP.
- Stays a quick-to-standard frame.
