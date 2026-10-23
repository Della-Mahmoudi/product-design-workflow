# Problem framing

Methods for turning a request into a problem worth solving. Read only the sections your route names.

**Contents**
1. Find the decision
2. Problem vs. solution
3. Evidence vs. assumptions
4. Users, needs and context
5. Quick risk scan
6. Hypotheses
7. Outcomes
8. Opportunity mapping
9. Prioritizing opportunities
10. Stakeholder alignment

Source tags such as [PT] or [EUX Ch4] are defined in `source-map.md`. [SYN] marks this skill's own synthesis rather than any single source.

---

## 1. Find the decision

Discovery exists to inform a decision. Without one, research produces trivia and framing produces documents.

- Establish, or infer and label: what decision is pending, who makes it and by when, and which options are on the table. Always include "do nothing" and "wait". Then ask what would make the decision-maker choose differently.
- When the input is a solution ("build X"), the decision is usually "should we invest in X, and in what form?" Make that explicit.
- When there is no real decision, say so. The right output may be a short list of questions, not a frame. [SYN; UXR Ch6 "Research Goals"; GOV-P]

**Output:** one sentence. *Decide whether/how to … by … because …*

## 2. Problem vs. solution

Requests usually arrive as solutions. Recover the problem before judging the solution.

1. Record the request as it was given and label it **Stakeholder input**.
2. Ask "what would this make possible, and for whom?" Repeat ("why does that matter?") until you reach a user need or a business outcome. [UXR Ch2 "laddering"]
3. Apply the alternatives test. Could the statement be addressed in more than one way? If not, it is a solution in disguise; go up a level. [PT]
4. Describe the problem in the user's terms. What blocks them, costs them time or money, or frustrates them, and in what situation? [SPM pp.17, 51, 68]
5. Mark what the problem still has to prove. Is it widespread? Is it urgent? Would people pay, switch or change behaviour to solve it? Each stays *Unknown* until there is evidence. [SPM p.58]
6. Keep the original request on the table as **one candidate solution among several**, not as the goal.

**Signs you are holding a solution, not a problem:**
- It names a feature, technology, channel or UI element.
- Success would be "we launched it".
- Asking a user if they have this "problem" would sound absurd ("Do you lack an AI assistant?").

**When users or stakeholders propose a fix,** treat it as a sign that some problem exists. Then find that problem, because the fix may only treat a symptom. [UXR Ch2; EUX Ch4 "Defining Requirements"]

**Problem statement** (adapt freely):
> **[Who]**, trying to **[goal]** in **[situation]**, is blocked or slowed by **[obstacle]**.
> Evidence: **[labeled sources, or Unknown]**.
> It matters because **[user impact]** and **[business impact]**.
> We will know it is addressed when **[observable change]**.
> Requested solution (a candidate, not yet justified): **[…]**

**Avoid:**
- Statements that contain a solution ("users need a chatbot").
- Statements with no affected person ("engagement is low").
- "Problems" that are only the absence of a feature.

## 3. Evidence vs. assumptions

Sort inputs before reasoning from them. A frame that silently mixes beliefs and findings cannot be trusted later.

- Label every input with the SKILL.md labels.
- A claim is a **Fact** only if it can be traced: who collected it, how, when, and from whom. Otherwise it is an **Assumption**, even if it is confident, senior or often repeated.
- Treat opinions and suggestions that do not come from users as assumptions to be proven by research. [GOV-N]
- Stakeholders hold real knowledge of goals, commitments and constraints. Record that knowledge as business context, and keep their beliefs about users labeled as assumptions. [SYN]
- Competitor behaviour is context. It shows what others chose to build, not that users want it or use it. [SPM p.73; UXS Ch5]
- Frameworks and best practices supply questions and structure, never product facts.
- Group assumptions by type to see where uncertainty lies:
  - users (who they are, what they need, how they behave)
  - value (will they choose it or pay for it?)
  - usability
  - feasibility
  - viability (business, legal, operations)
  - ethics and accessibility
  [SVPG; PT; SYN]
- The **riskiest assumptions** are the ones the decision depends on most and that have the least evidence. They are first in line for research. [PT; UXS Ch8]

**Compact ledger,** for when it helps: *Claim | Label | Source or basis | Confidence | What would change it.*

## 4. Users, needs and context

- **Define users by shared problem or behaviour, not demographics alone.** Segments are a means to an end: keep only as many as there are distinct sets of needs. [EUX Ch3 "User Segmentation"; SPM pp.79–81; UXR Ch7]
- **Cover everyone involved:**
  - the people who use the product
  - buyers or decision-makers, if they are different people
  - staff who deliver or support the service
  - atypical users, including disabled people and people with low digital skills or confidence
  [GOV-D; GOV-N; SPM pp.62–66]
- **For each group, capture:**
  - their goal
  - how they achieve it today: tools, workarounds, channels, or doing nothing
  - the obstacles they hit and what those obstacles cost
  - their context: when, where, which device, what constraints
  - what they need in order to reach the goal
  [GOV-D; UXS Ch3; ISO principle heading: explicit understanding of users, tasks and environments]
- **Write needs from the user's side, without a solution in them:** *As a … I need … so that …* [GOV-N]
- **Do not settle conflicting needs silently.** When groups' needs conflict, deciding whom to serve is a strategic choice. Raise it. [EUX Ch3 "User Segmentation"]
- **Personas summarize evidence; they never replace it.** When there is no research, offer at most clearly labeled *provisional* personas:
  - every attribute is an assumption
  - it is written so that it can be checked against the real world
  - it comes with the research that would confirm or replace it, ideally observable behaviour (what people did, paid or accepted) rather than stated intent
  - it carries no invented quotes, demographics or percentages
  [UXS Ch3 "provisional personas"; EUX Ch3 "Creating Personas"]
- **In two-sided or multi-party products, frame each side separately.** Each side is a customer segment with its own problem, and the proposition only works if every side's problem is real. [UXS Ch3 "Two-sided markets"]

## 5. Quick risk scan

For a quick frame, name the risk that dominates and say why in one or two lines. Cover only the risks that matter. Full method: `strategy-scope-and-metrics.md` §4. [SVPG]

- **Value:** will the target users choose it over what they do now?
- **Usability:** can they work out how to use it?
- **Feasibility:** can it be built and run with the time, skills, technology and data available?
- **Viability:** does it work for the business, cost, revenue, channels, legal, brand?

Add accessibility, privacy or ethical risk when relevant. They are not among the four, but they are often hidden. [SYN]

## 6. Hypotheses

Write a hypothesis when a belief is both important to the decision and uncertain.

- **Problem hypothesis:** *We believe [segment] experiences [problem] when [situation], because [basis]. We would be wrong if [observable disconfirming evidence].*
- **Solution hypothesis:** *If we [change], [segment] will [behaviour change], shown by [signal], within [time]. We would be wrong if [threshold not met].*

**Rules**
- Make one claim per hypothesis. It must be falsifiable and tied to a decision. [UXR Ch6; UXS Ch7]
- Agree in advance what result would confirm or refute it. Thresholds chosen after seeing the data invite rationalization. [UXS Ch8 "Planning Phase"]
- Look for evidence that would disprove the favoured hypothesis, not only evidence that confirms it. [UXR Ch6]
- Test the problem before the solution. A good solution to a problem nobody has still fails. [UXS Ch3; PT]
- Break a solution into the assumptions it depends on, and test the riskiest first. [PT; UXS Ch8]

## 7. Outcomes

- **Know the three levels:**
  - business outcome: the health of the business, such as revenue or retention
  - product outcome: a customer behaviour or attitude in the product that drives the business outcome
  - output: what gets shipped
- **Aim discovery at a product outcome the team can influence,** and trace it up to the business outcome. [PT]
- **Write outcomes as conditions for success, not the path to it.** "Make money" is too vague. "Build a recommendation carousel" names a solution. [EUX Ch3 "Product Objectives"]
- **Do not use as the discovery outcome:**
  - a single feature's adoption figure, too narrow
  - "launch X", that is an output
  [PT]
- **When several outcomes compete, ask for a ranking.** Without one, priorities default to politics. [EUX Ch4 "Prioritizing Requirements"]
- **To measure an outcome,** see `strategy-scope-and-metrics.md` §10.

## 8. Opportunity mapping

An opportunity is an unmet customer need, pain point or desire, framed from the customer's side. [PT]

**When to build a full opportunity solution tree.** Only if all three hold; otherwise a problem statement and a short list of opportunities is enough, and say so: [PT prerequisites]
- there is a clear product outcome
- there are real customer stories to draw opportunities from
- several opportunities compete

**Steps**
1. **One outcome at the root.** Build one tree per outcome, never one for a whole company. [PT]
2. **Draw opportunities from evidence**, interview stories, observed behaviour, support logs read in context. Mark any opportunity without evidence as an assumption. Analytics, sales notes or tickets show where to look, but not the need; add story context. [PT]
3. **Group opportunities by moment in the user's experience.** Nest specific ones under broader ones, and keep siblings from overlapping. [PT]
4. **Keep solutions off the map until a target opportunity is chosen.** Then generate several candidate solutions for that one opportunity rather than for the whole tree. [PT]
5. **Under each serious solution, list the assumptions it depends on,** and test the riskiest first. [PT]

**Anti-patterns** [PT]
- A tree built from the team's ideas instead of customer stories.
- Overreacting to a single interview.
- Brainstorming solutions across the whole tree.
- A business or adoption metric at the root.
- Polishing the first draft instead of revising it as evidence arrives.

## 9. Prioritizing opportunities

1. **State the criteria before scoring.** [SYN; EUX Ch4]
2. **Judge each opportunity on:** [PT; SPM p.58, pp.82–85]
   - how many people it affects, and how often
   - how much it matters to them, and how poorly current alternatives serve them
   - how urgent it is, and whether people would pay or switch
   - how well it fits company strategy and strengths
   - its effect on market position
3. **Leave effort and cost out at this stage.** Feasibility is judged later, when comparing solutions. [PT; EUX Ch4]
4. **Show evidence strength next to every rating.** A high score built on an assumption is a research priority, not a build priority. [SYN]
5. **Work on one target opportunity at a time,** to limit work in progress. [PT]
6. **Prefer depth in one segment over shallow coverage of many.** Focus sharpens the problem, the message and the scope. [SPM p.85]

## 10. Stakeholder alignment

The goal is shared understanding of the problem and the decision, without letting seniority stand in for evidence.

**Intake questions for a stakeholder request** [SYN; EUX Ch8 "Asking the Right Questions"]
- What decision is this meant to inform?
- What problem do you believe exists, and for whom?
- What evidence prompted the request?
- What would success look like?
- What constraints apply?
- What happens if we do nothing?

**Working with stakeholders**
- **Steer feature proposals back to the goal behind them,** and show that the goal could be met in more than one way. [EUX Ch4]
- **Record what stakeholders know accurately.** Documented goals, commitments and constraints are often facts about the business. Their beliefs about users stay labeled as assumptions. [GOV-N; SYN]
- **Settle the rules before the results.** Ask for a ranking of objectives, and agree the decision criteria before findings come in. [EUX Ch4; UXS Ch8]
- **Bring stakeholders close to the evidence.** Invite them to observe sessions or read raw findings; first-hand exposure changes minds faster than reports do. [UXR Ch4; UXS Ch8]
- **When evidence and seniority disagree,** present the evidence, its confidence, and the cheapest test that would settle the question. Do not issue a verdict on who is right. [SYN; UXS Ch6]
- **Keep a short, visible decision log** of what was decided, on what evidence, and what would reopen the decision. [UXR Ch6; EUX Ch3]
