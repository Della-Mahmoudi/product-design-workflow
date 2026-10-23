# Research and evidence

Methods for deciding what to learn, judging what is already known, and recommending the least research that could change a decision. Read only the sections your route names.

**Boundary.** Everything here serves discovery: the evidence needed before choosing what to build. Validating a designed or shipped solution (prototype and usability testing, post-launch analytics, instrumentation, experiments, causal analysis) belongs to `prototype-testing-analytics`. Name such a need here, with the decision it serves, and hand it over.

**Contents**
1. Research questions from decisions
2. Existing evidence first
3. Choosing a method
4. Qualitative vs. quantitative, behavioural vs. attitudinal
5. Sampling and inclusion
6. Confidence and limitations
7. The minimum useful research recommendation
8. When a metric moves

Source tags are defined in `source-map.md`. [SYN] marks this skill's own synthesis.

---

## 1. Research questions from decisions

- **Start from the decision and its riskiest assumptions.** Turn each important but unfounded assumption or opinion into a research question. [GOV-P]
- **For each question, write down three things:** [UXR Ch6 "Research Goals"]
  - what will be learned
  - why it matters: which decision it serves, and what you risk by not knowing
  - what you expect to find, stated so that it could be proven wrong
- **Keep only questions whose answers could change the decision.** The test is "what will the results change?" [SPM p.55; GOV-P]
- **Keep two kinds of question apart.** Research questions are what the team needs to learn. Interview or survey questions are what participants are asked. Never ask participants the research question directly ("Would you use X?"). Ask about specific past behaviour instead. [UXR Ch2; SPM pp.51–52; SYN]
- **Don't plan more research than the team can act on.** [GOV-P]
- **Expect questions to change.** In discovery they are broad and shift quickly; they should narrow as the work progresses. [GOV-P]

## 2. Existing evidence first

Before recommending new research, check what already exists:
- analytics and search logs
- support tickets and call logs
- operational or back-office data
- sales and win/loss notes
- previous research
- reviews

[GOV-D; GOV-N; UXR Ch3–4; SPM pp.50, 68]

For each source, note:
- **What it measures, for whom, and how:** the method, sample and period.
- **What it cannot show.** [UXR Ch3; NNG]
  - Analytics show what happened, not why.
  - Analytics depend on correct tracking and cover only what was instrumented.
  - Tickets and feedback come only from people who chose to write in.
- **How old it is.** Products and users change, so old findings are leads, not facts. [UXR Ch15]
- **Who is missing:** segments absent from the data, non-users, people who gave up. [UXR Ch7; GOV-D]

Then sort the research questions by what existing evidence covers: fully answered, partly answered, or not answered at all. Only the gaps need new research. [UXR Ch3]

## 3. Choosing a method

**Choose the method from the question, not from habit.** Use three lenses: [NNG]
- **Behavioural or attitudinal:** what people do, versus what they say.
- **Qualitative or quantitative:** why and how, versus how many and how much.
- **Context of use:** natural, scripted, limited, or no use of the product.

Discovery questions usually call for generative, behaviour-leaning methods. [NNG phase guidance; GOV-D] The table applies those lenses to common discovery questions. [NNG; SYN]

| Question | Usually fits | Weak as primary evidence |
|---|---|---|
| Who has this problem, how they cope today, why | Field visits or contextual inquiry; interviews about a specific recent occurrence; diary studies | Asking people to predict their future use |
| How many, how often, how big | Analytics and logs; closed-question surveys, once the problem is understood | Counting mentions across a handful of interviews |
| Where an existing journey breaks | Funnel or log analysis to locate it; observing real use to explain it | Opinions about the design |
| Whether change X caused outcome Y | Controlled comparison: A/B test, holdout, staged rollout | A before/after comparison on its own |
| Whether people will act on a value proposition | A behavioural test where people commit something (time, sign-up, pre-order), disclosed honestly | "Would you use / pay for it?" answers |
| How people group and name things | Card sorting and similar methods; hand the results to IA work |, |

**Other selection factors** [UXR Ch5]
- What evidence the stakeholders need in order to be convinced.
- How many people you can reach, and where they are.
- Budget and timeline. Make the trade-off between time, budget and scope explicit.

**Combining methods**
- **Pair a qualitative and a quantitative measure for each question, when you can.** The qualitative explains; the quantitative sizes. [UXR Ch5; NNG]
- **Give unrelated goals separate studies.** One study stretched across unrelated goals serves none of them well. [UXR Ch5]

**Usability tests of designed solutions belong to later stages.** In discovery, observe current behaviour, or test the riskiest assumption as cheaply as possible. [NNG; GOV-D]

**Purpose decides ownership.** Evidence for choosing which problem or opportunity to pursue stays here. Evidence about whether a designed or shipped solution works, or whether a change caused an outcome, goes to `prototype-testing-analytics`: name the need and the decision it serves, and hand over the study design.

## 4. Qualitative vs. quantitative, behavioural vs. attitudinal

- **Qualitative findings tell you what exists, how and why, not how common it is.** Report them as counts of participants ("5 of 8"), never as population percentages. [NNG; UXR Ch3–4; SYN]
- **Quantitative findings tell you how much and how often, but only for what was measured.** They do not explain why, and they lose the context of use. [UXR Ch3]
- **Neither is inferior.** They answer different questions and work best together. [UXR Ch4]
- **What people say and what they do often differ.** [NNG; UXR Ch15]
  - Treat stated intentions, preferences and willingness to pay as attitudinal signals.
  - When stated and observed evidence conflict, give more weight to observed or logged behaviour.
- **Self-reports skew positive.** Participants want to be helpful and tend to describe experiences more favourably than they felt them. Leading questions and yes/no questions make this worse. [UXR Ch2, Ch11]
- **Accounts of past behaviour beat predictions of future behaviour.** Ask about the last time it happened, not what the person would do. [UXS Ch3 "The problem interview"; SPM p.52; SYN]

## 5. Sampling and inclusion

- **Define whom you need, and why, before recruiting.** Screen on the behaviour or situation that matters, not only on demographics. "Everyone" is not a user group. [UXR Ch7]
- **Qualitative rounds can be small.** A handful of participants per distinct user group per round is usually enough to surface patterns. GOV.UK suggests 4–8 per round; *UX Research* suggests 3–5 per user group. [GOV-P; UXR Ch7]
  - Prefer several small rounds to one large one.
  - Small rounds reveal issues and needs. They cannot estimate how widespread anything is.
  - Surveys, A/B tests and benchmarks need far larger samples.
- **Include, in every round where feasible:** disabled people, people with low digital skills or confidence, and atypical users. Where that is not possible, plan dedicated rounds for them. Include the staff who deliver or support the service. [GOV-D; GOV-P]
- **Balance your sources.** Listening only to existing customers pushes toward more features for fewer people. Also reach prospective users, people who chose an alternative, and people who stopped using the product. [SPM pp.47–56; UXR Ch7]
- **Watch for recruitment bias.** Each of these groups skews results. Use analytics to spot under-represented groups. [UXS Ch8; UXR Ch7]
  - friends and family
  - participants supplied by the client
  - pop-up volunteers
  - power users
- **Run research ethically.** [SYN; see `source-map.md` §5]
  - Get informed consent.
  - Don't deceive participants about who you are or what is being tested.
  - Handle personal data under applicable privacy law and the organization's policy.

## 6. Confidence and limitations

Rate confidence for every claim a recommendation rests on, and give the reason in a few words. [SYN]

| Level | What it looks like |
|---|---|
| **High** | Direct evidence: behaviour observed or logged from the relevant users. Recent, fit for the claim, and corroborated by an independent source or method. |
| **Medium** | Direct but limited evidence: a small or skewed sample, a single method, or an indirect measure. Or consistent indirect evidence from several sources. |
| **Low** | A single anecdote, a stakeholder belief, attitudinal data only, stale or out-of-segment data, or inference from competitors. |

**Errors to check for**
- **Small-sample generalization:** projecting qualitative results onto a population.
- **Mistaking sequence for cause:** treating correlation, or "it happened after the redesign", as proof.
- **Survivorship:** studying only current users misses those who left or never came.
- **Self-selection:** feedback forms and reviews over-represent strong opinions.
- **Measurement changes:** new tracking, changed definitions or bot traffic can move a metric with no change in behaviour.
- **Novelty and change aversion:** first reactions to a redesign may not last. [HEART]
- **Confirmation bias:** picking the evidence that supports the preferred answer. [UXR Ch13; SYN]

**Record contradictions; don't average them away.** They often point to differences between segments. [UXR Ch13]

## 7. The minimum useful research recommendation

Recommend the smallest activity that could change the decision. Cover these points, as prose or a list:
- the decision it informs
- the riskiest assumption or open question it addresses
- the method, why it fits, and one line on the alternative you did not choose
- who or what data is involved, and how many participants or records
- effort, as a range
- **a decision rule agreed in advance:** which result means proceed, change course, or stop [UXS Ch8]
- what is deliberately not being researched now

**Default order**, skip any step the existing evidence already covers: [SYN; GOV-D; UXR Ch5]
1. Existing evidence.
2. Cheap direct observation or conversations.
3. Targeted quantitative sizing.
4. Controlled tests. Name the need, the hypothesis and the decision rule here; the experiment design itself belongs to `prototype-testing-analytics`.

## 8. When a metric moves

Use this section to **frame** a metric change as a product problem or decision: separate the observation from its possible causes, surface hypotheses, name the discovery unknowns, and say what needs investigating. That one thing happened after another does not prove it caused it.

Running the investigation is not discovery work. Diagnosing the shipped experience, analyzing post-launch performance, defining instrumentation, designing an experiment and establishing cause belong to `prototype-testing-analytics`. Write the frame below, then hand over; do not perform the checks here.

1. **Name measurement as a rival cause.** Tracking changes shipped with the release, changed event or funnel definitions, attribution windows, bot or test traffic, outages and pipeline delays can all move a metric. [HEART; UXR Ch3; SYN]
2. **Ask whether the change is bigger than normal variation.** That needs the metric's usual week-to-week range and the volume behind it: small samples swing. Label any history or volume that wasn't provided as *Unknown*; whether the change is more than noise is then *Unknown* too. [SYN]
3. **Name where to look.** The breakdowns that would locate the change: platform, device, browser, app version, traffic source, new vs. returning users, region and funnel step. A drop confined to one segment points to different causes than a uniform one. [SYN]
4. **Line up the timeline.** Include releases by every team, campaigns and shifts in traffic mix, pricing or policy changes, seasonality, competitor events and performance regressions. Any metric read in isolation can mislead. [EUX Ch3 "Success Metrics"; SYN]
5. **List the rival explanations as hypotheses.** At minimum: the design change itself, a defect, a measurement change, a shift in traffic mix, and external factors. For each, name the cheapest check that would support it or rule it out, and order the checks cheapest first. [SYN]
6. **Note when the mechanism needs explaining.** Observing real users on the affected journey, consented session recordings or moderated sessions, is how the mechanism is found; name it as an investigation need. [NNG; UXR Ch4]
7. **Note when cause must be established:** when the decision is costly or contested. That calls for a controlled comparison (the old and new versions shown to random samples, or a rollback for a random holdout group) with a success metric and a guardrail metric defined in advance. Its design and analysis are handed over. [NNG; HEART; SYN]
8. **Frame the decision.**
   - Say what evidence would justify acting in full right away: a confirmed defect, for example, or confirmed losses large enough that waiting costs more than being wrong.
   - Separate what can be done now and reversed later, a partial rollback run as an experiment, for instance, from what should wait for evidence.
   - Do not redesign the interface as part of discovery; hand the framed problem to design and the investigation to `prototype-testing-analytics`.

   [SYN]
