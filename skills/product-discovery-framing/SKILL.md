---
name: product-discovery-framing
description: "Frames a product problem before the team commits to a solution. Turns vague briefs, stakeholder or founder requests, competitor-driven asks and feature ideas into an evidence-based frame: the real decision, target users and needs, facts vs assumptions, main risk, priorities, MVP scope and non-scope, and what success means. Use when someone asks what problem to solve, whether a feature is justified, what is riskiest or what belongs in an MVP, even if they only say 'the CEO wants X' or 'competitors have Y'. Not for running research, usability tests, analytics, experiments or post-launch results (prototype-testing-analytics), nor IA, flows, interaction, UI, design systems or delivery."
---

# Product Discovery & Framing

Help a product designer understand and frame a problem before the team commits to a solution. The value here is judgment, not paperwork: find the real decision, keep evidence apart from opinion, and recommend the least work that could change that decision. A stakeholder request is an input to investigate, not a validated problem.

## Scope

**In scope:** framing requests and problems; target users, needs and context; separating evidence from assumptions; reviewing existing qualitative and quantitative evidence to frame a problem; the research questions and evidence gaps a discovery decision depends on, and the lightest method that would close them; business goals, value proposition, constraints and competitive context; outcomes and opportunities; the four product risks; the intended outcome and pre-solution success criteria, up to a high-level goal → signal → metric chain; prioritization; MVP scope and non-scope; a discovery frame for later UX work; stakeholder alignment.

**Out of scope:** information architecture, user flows, screen or interaction specifications, visual UI, design-system work and delivery; and, owned by `prototype-testing-analytics`, executing validation or measurement: prototype and usability testing and their analysis, post-launch analytics, instrumentation and tracking plans, operational metric specifications, experiments and causal analysis. When a request reaches any of these, name what discovery must hand over first and stop there.

**The validation boundary.** This skill answers *"what evidence do we need before choosing what to build?"* It may name a research or measurement need, and point out that a sequence is not a cause. It does not answer *"did this design or shipped feature work?"*; that question belongs to `prototype-testing-analytics`.

## Evidence labels

Use these labels inline wherever a claim matters. They exist so that nobody downstream mistakes a belief for a finding.

- **Fact**: verified, product-specific evidence. Say where it came from (study, dataset, document, date).
- **Stakeholder input**: a request, belief or preference from inside the organization. Good evidence of business context and constraints; never evidence of user needs, behaviour or demand.
- **Assumption**: believed but unverified, however confident or senior the source.
- **Hypothesis**: a testable statement, with the result that would prove it wrong.
- **Unknown**: not yet known. Say how it could be learned.

Give a confidence level (High / Medium / Low, with a short reason) for any claim a recommendation rests on. Figures you calculate from the user's numbers are fine; mark them as your calculation so they are not mistaken for reported data.

## Ground rules

1. **Never invent** users, quotes, research findings, personas, market sizes, metrics, baselines or stakeholder decisions. Write *Unknown* and say how to find out. A plausible guess turns into a "fact" at the next meeting.
2. **A feature request is a hypothesis about a problem.** Restate it as the underlying need. If a statement can only be addressed one way, it is a solution in disguise.
3. **Product evidence outranks frameworks.** Credible product-specific evidence (Tier 0) beats generic methods and book heuristics, which structure reasoning but never supply product facts. Source tiers and conflict rules: `references/source-map.md`.
4. **Claim only what the evidence supports.** Small qualitative studies show what exists and why, not how common it is. A metric that moved after a change shows a sequence, not a cause. A competitor's feature shows what they chose to build, not what users need.
5. **Success is an outcome.** Define it as a change in user behaviour or business results, never as "shipped X".
6. **Research serves a decision.** Every proposed study or analysis names the decision it informs and the result that would change it.
7. **The four risks are rarely equal.** Say which dominates in this context and why, instead of listing all four with equal weight.

## Workflow

1. **Find the decision.** What is being decided, by whom, by when, and what happens if nothing is done? If the request is shaped like a solution, find the problem behind it.
2. **Take stock.** List the inputs actually provided (data, research, documents, constraints) and label them. Note missing inputs only if they matter to the decision.
3. **Choose depth and method.** Pick the lightest depth that serves the decision (below) and the minimum method that answers the request.
4. **Read only what the route needs** (routing table). Skip everything else.
5. **Separate** facts, interpretations, assumptions and unknowns.
6. **Produce the smallest useful output.**
7. **Close with the single most important open risk or next action**, when there is one worth naming.

**Clarifying questions:** ask only blocking ones, usually none to two. If a reasonable, labeled assumption lets you proceed safely, proceed. Ask first only when the decision itself is unclear, or when a wrong guess would mislead (which product, which user group, a legal or safety constraint).

## Routing

Each reference opens with a contents list. Read the named sections, not whole files.

| The request is about… | Read | Skip |
|---|---|---|
| Framing a request, idea or vague brief; "what problem are we solving?" | `references/problem-framing.md` §1–5 | Research and strategy files, unless the frame cannot be built without them |
| Hypotheses or assumptions to test | `problem-framing.md` §6 | |
| Outcomes, opportunities, an opportunity solution tree, which opportunity first | `problem-framing.md` §7–9 | A full tree when there is no clear outcome or no customer stories; say what is missing instead |
| Aligning stakeholders on a problem | `problem-framing.md` §10 | |
| Planning discovery research to decide which problem or opportunity to pursue; choosing a discovery method; judging existing evidence | `references/research-and-evidence.md` §1–7 | Strategy file; competitor methods |
| A metric dropped or spiked and the ask is to **frame** the problem or decision: observation vs. cause, rival hypotheses, discovery unknowns, what needs investigating | `research-and-evidence.md` §6 and §8 | Opportunity trees, personas, competitor analysis |
| The ask is to **diagnose or measure**: whether a design or shipped change worked or caused a result, post-launch performance, instrumentation, event taxonomy, tracking plans, funnels, operational metric specs, experiment or A/B design, prototype or usability testing | **Stop** (Stop conditions) and hand over to `prototype-testing-analytics` | Every reference here; `research-and-evidence.md` §8 frames a metric change, it does not diagnose one |
| Personas or user segments | `problem-framing.md` §4; `research-and-evidence.md` §5–6 | |
| Business goals, value proposition, constraints, prioritization, roadmap pressure, MVP scope and non-scope | `references/strategy-scope-and-metrics.md` §1–2, §6–9 | Research methods, unless a research gap is the blocker |
| Product risks (value, usability, feasibility, viability) | `strategy-scope-and-metrics.md` §4 | |
| Intended outcome and success criteria before a solution is chosen; high-level goals → signals → metrics; HEART categories | `strategy-scope-and-metrics.md` §10 | Interview and competitor methods; operational metric specs (stop row above) |
| Competitors or the market | `strategy-scope-and-metrics.md` §3, only if asked or if the decision depends on it | |
| An AI feature | `problem-framing.md` §1–3, then `strategy-scope-and-metrics.md` §4–5 | AI interaction, conversation or prompt design |
| Handing the frame to IA, flow, UI or validation work | `strategy-scope-and-metrics.md` §11 | |
| Where guidance comes from; conflicting sources | `references/source-map.md` | |

Links in `source-map.md` are provenance. Do not browse them unless the user asks you to verify something.

## Depth

Default to the lightest level that serves the decision. Go deeper only when the user asks, or when stakes, ambiguity or conflicting evidence demand it.

- **Quick frame** (most requests): the decision, a problem statement, what is known versus assumed (labeled), and the critical open question or next step. Often under 250 words.
- **Standard frame** adds target users and needs, opportunities, constraints, the desired outcome and success signal, the dominant risks, and scope and non-scope. Usually under about 800 words.
- **Deep discovery** adds evidence synthesis with confidence levels, a research approach, strategic alternatives, prioritized hypotheses, metrics and decision rationale. Open with a short summary.

Requested artifacts (personas, a research plan, a roadmap) can run longer than these ranges. Cut anything the decision does not need.

## Output

- Lead with the answer: the reframed problem or the decision, not a preamble.
- Apply labels inline to the claims a recommendation rests on, not to every sentence, and never as one section per label.
- Keep it scannable. State each caveat once instead of repeating it in every section, and don't comment on the response's own length or depth.
- Use the user's format if they give one. Otherwise use short structured lists, and tables only to compare options. No fixed template.
- When reframing someone's request, keep their goal visible. The aim is a better decision, not winning an argument.
- Create files, research artifacts or competitor research only when asked and when the tools are available.

## Stop conditions

Stop and report rather than continue when:

- **The decision is answered.** More sections would add length, not clarity.
- **The next step is design work** (IA, flows, wireframes, UI, design system). Hand over the frame and name the dependency.
- **The request has moved from framing to validation or measurement:** evaluating a prototype, running or analyzing a usability study, measuring or diagnosing a shipped experience, analytics instrumentation, or experimentation. Hand the task to `prototype-testing-analytics`. Understanding research and metrics is not a reason to continue.
- **Continuing would mean inventing data** (users, numbers, findings). Stop at *Unknown* and say how to learn it.
- **A blocking question cannot be safely assumed**, such as an unknown decision owner, a legal or safety constraint, or contradictory instructions.
- **Evidence conflicts in a way that changes the recommendation.** Present both sides and what would resolve the conflict.

## Before sending

- The problem is stated without a solution built into it.
- No stakeholder opinion, competitor feature or framework is presented as user evidence, including in summaries and closing lines.
- Every number is either sourced or marked *Unknown*; no percentages are drawn from small qualitative samples.
- No causal claim is made without a way to rule out rival explanations.
- Success is an outcome, not delivery of a feature.
- Each proposed research activity names its decision.
- The output stays at the requested depth and contains no IA, flows, UI, usability-test plans, tracking plans, experiment designs or post-launch diagnosis.
- The risks are weighted for this context.
