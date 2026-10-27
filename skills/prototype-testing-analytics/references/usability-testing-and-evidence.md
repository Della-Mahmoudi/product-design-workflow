# Usability testing and evidence (Mode B, and the testing half of Mode A)

Load this when planning or moderating a usability study, writing tasks and success criteria, turning observations into findings, or reviewing an existing study. It also covers generative and exploratory interview studies once a research question exists (section 20) and executing IA validation studies scoped by `ux-architecture` (section 21). Keep observation, finding, interpretation, recommendation and confidence as separate statements throughout; the value of a study depends on that separation.

## 1. Study plan, proportionate to the decision

A plan exists to make the study answer a question. Fill in only the rows that matter; a one-page plan is normal for a single feature.

| Element | What to write |
|---|---|
| Decision to inform | the design or roadmap decision that depends on the result |
| Research question(s) | specific, evaluative, behavioral where possible ("can target users complete X and understand Y?") |
| Target participants and recruitment criteria | behaviors and context first, demographics only where they change behavior (section 2) |
| Context of use | device, environment, account state, data state, time pressure |
| Method and session format | moderated / unmoderated, remote / in person, think-aloud or not, lightweight or formal; why this is the minimum valid method |
| Test material | prototype or product, fidelity, the path map and the limitation log |
| Tasks and scenarios | section 3 |
| Success criteria and measures | section 4, defined before any session |
| Behavioral observations to capture | what counts as hesitation, error, assistance, recovery, comprehension signal |
| Moderator behavior and assistance rules | section 6 |
| Evidence capture | recording consent, note structure, observer roles |
| Session count and schedule | stated as "what we expect to learn from this many sessions", never as statistical coverage |
| Risks and limitations | prototype limits, recruitment risks, environment, observation effects |
| Ethics | consent, recording, sensitive data, incentives (section 14) |

Dry-run the whole protocol with someone outside the team before the first participant. Fix tasks that were misread, timings that overran, and prototype gaps found in the dry run.

## 2. Participants

- Recruit for **behaviors and context**, not demographics: does this person do the task in real life, with what frequency, on what device, with what prior exposure to our product or competitors? Demographics enter only where they change behavior.
- Write a short screener: multiple-choice, a few minutes long, with disqualifiers and quotas. Screen out people whose knowledge would distort results (team members, designers of similar products, recent participants) unless they are the target.
- For a single user group and a qualitative aim (find the main problems), a handful of sessions, commonly around five, usually surfaces the frequent problems; add sessions when groups differ materially, when the product is complex, or when the goal is coverage of edge paths. Never present this as statistical coverage, and never let a session count be used to produce a population percentage.
- For lightweight rounds, recruiting loosely and grading on a curve is legitimate: note where a participant differs from target users and ask, for each problem, whether a target user would have had it. State this in the limitations. Do not use loose recruiting when domain knowledge, assistive-technology use or a specific account state is central to the question.
- Over-recruit for no-shows. Pay participants regardless of task outcome, and say so at the start.
- Accessibility: when the product will be used with assistive technology, or any claim about accessibility will be made, recruit participants who use screen readers, magnification, switch or keyboard-only input, as appropriate. Automated scans do not substitute (section 18).

## 3. Scenarios and tasks

A scenario gives the participant a reason and the information they would have in real life. A task is what they try to achieve. Together they must be realistic, self-contained and non-leading.

Rules:

- Phrase tasks as goals in the participant's world, not as instructions in ours.
- Never reveal the target label, the target navigation item, the intended feature, or the correct sequence, unless that knowledge is exactly what is under test (for example, testing whether users who know the feature name can find it).
- Include any information the participant would have but the prototype cannot supply (credentials, an order number, a budget, a deadline).
- Let participants choose details where the choice is theirs in real life ("a product you would actually buy"); it raises engagement and surfaces real content needs.
- Order tasks from simple to complex, and keep independent tasks independent so one failure does not cascade.
- Read tasks aloud or have participants read them aloud; keep each short enough to hold in mind.
- Prepare the neutral response for every dead end in the prototype limitation log.

| Avoid | Prefer |
|---|---|
| "Go to Settings, click Billing, then change the payment method." | "An invoice arrived and you want the next payment to be charged to a different card. Show me what you would do." |
| "Use the Compare feature to compare two phones." | "You are choosing between two phones you saw earlier. Decide which one you would buy." |
| "Find the Help Center." | "Something went wrong with your last order and you want to get it sorted out." |
| "Do you like the new checkout?" | "You decided to buy these. Go ahead as you would at home." then observe |

Comprehension probes are tasks too: "Before you choose, what do you expect will happen with each of these options?" then observe, then "What happened?"

## 4. Success criteria and measures, fixed before testing

Define what counts before the first session, in writing. Changing criteria after seeing results turns the study into storytelling.

Measures menu (use only what the research question needs):

| Measure | Definition to fix in advance |
|---|---|
| Task completion | the observable end state that counts (for example, order confirmation screen reached with the intended delivery option), with "complete", "complete with assistance", "partial", "abandoned", "wrong outcome believed complete" as distinct codes |
| Critical error | an action that makes the goal unachievable without assistance, or produces a wrong outcome the participant does not notice |
| Non-critical error | a wrong turn or slip the participant recovers from unaided |
| Assistance | any moderator input beyond neutral prompting that changes the course of the task; log level: clarification of the task, hint, direct instruction |
| Time on task | from task read-out to end state; only meaningful with a consistent protocol and without think-aloud narration, or compared only within this study |
| Path deviation | steps outside the expected path(s); record the deviation and whether it was recovered |
| Comprehension | match between stated expectation, choice made, and stated understanding afterwards |
| Confidence | a single post-task rating, labeled attitudinal |
| Satisfaction | post-session rating or standardized questionnaire, labeled attitudinal; never used as a usability score |

Set the threshold for the decision at the same time (for example: "proceed if no critical errors remain on the checkout path after fixes; a critical error observed in more than one session blocks"). Thresholds are about this study's observations, not population rates.

## 5. Session formats and structure

A moderated session usually runs: welcome and consent (purpose, recording, "we are testing the design, not you", you can stop at any time), a few warm-up questions about their real behavior, an optional first-impression tour of the starting screen (what is this, what can you do here, no clicking yet), the tasks, probing questions saved until after the tasks, wrap-up and thanks. Keep sessions to about an hour; attention and data quality drop after that. Unmoderated sessions are shorter and need tasks that cannot be misread, since nobody can clarify.

Think-aloud gives diagnostic richness and slows people down; use it for diagnosis, drop it or use retrospective think-aloud when timing is a measure. Observers watch from elsewhere, write down the few most serious problems they saw per session, and send questions to the moderator for the probing phase rather than interrupting.

## 6. Moderation rules

The moderator's job is to obtain valid behavior, which means not influencing it.

- Do not lead: no hints about where to look, no "did you see the button?", no questions that contain the answer.
- Do not teach the interface during a task. Do not defend the design, explain intent, or react to failures (no sighs, no "interesting").
- Use neutral prompts: "What are you thinking?", "What are you looking at?", "What would you do next?", "What did you expect to happen?", "Keep going as you would at home."
- When asked for help, reflect it back: "What would you do if I weren't here?" Offer assistance only when the participant is stuck beyond what the study can learn from, and record it.
- Distinguish **clarification** (restating the task without new information, allowed and logged) from **assistance** (any information about the interface, logged with its level and its effect on the outcome). An outcome reached after assistance is coded "complete with assistance", never "complete".
- Handle prototype dead ends with the scripted neutral line and log the event against the limitation, not the participant.
- Save probing and "why" questions for after the task. Avoid "would you use this?"; ask about what they did and expected.
- Account for observation effects when interpreting: people try harder, persist longer and complain less when watched.

## 7. Observation capture

Notes are the raw data. Structure them so that behavior and quotes are separable from interpretation:

`participant code | task | timestamp | what happened (behavior, verbatim quote in quotes) | code (hesitation / wrong path / critical error / assistance level / recovery / comprehension mismatch) | prototype limitation hit? | observer's note (clearly marked as interpretation)`

Keep a moderator and a note-taker where possible; moderating and recording at once degrades both. Record screen and audio with consent so disputed observations can be checked. Debrief immediately after each session or day: what each observer saw as the most serious problems, in observed terms only.

## 8. From observations to findings

Work in order and keep the labels:

1. **Observation**: what happened, with participant code and task. No interpretation.
2. **Finding**: the pattern across observations (one strong observation can still be a finding if the consequence is severe).
3. **Interpretation**: the most plausible explanation, stated as an interpretation, with alternatives if they are live.
4. **Recommendation**: what to change, test or investigate next; routed to the stage that owns it (copy, interaction design, IA, visual, engineering, or further research). Write it as the problem that stage should revisit ("interaction design should revisit how discoverable Retry is after an upload fails"), never as the new behavior, states, focus order, hierarchy or layout.
5. **Confidence**: how much the evidence supports the interpretation (section 10).

Example:

- Observation: 4 of 6 participants opened Account and scanned it before looking under Organization for Billing; two said "I thought it would be under my account".
- Finding: participants initially expected Billing at the account level.
- Interpretation: the distinction between personal and organization billing is not conveyed by the current hierarchy or labels. Alternative: the Organization entry point is visually under-weighted.
- Recommendation: route to IA review: test an alternative label or placement before changing the hierarchy; also check the visual weight of the Organization entry.
- Confidence: moderate, repeated qualitative observation within this study; not an estimate of how many users would be affected.

Analysis practice: put every observation on its own card with its participant code, cluster across sessions, then write findings from clusters. Report frequency as a count within the study. Separate problems from requests: a participant's suggested feature is an attitudinal data point, not a finding. Ignore slips corrected immediately without help unless they recur or cost confidence. When a finding points at something another stage owns (hierarchy, visual system, copy), say so and stop; do not redesign.

## 9. Severity

Rate each issue on the dimensions below, then assign a level by judgment. Do not compute a numeric score unless the team has an established, agreed model.

| Dimension | Consider |
|---|---|
| Impact on task | prevents completion, causes a wrong outcome, delays, or merely irritates |
| Recoverability | unaided recovery, recovery only with assistance, no recovery |
| Criticality of the task | core goal, frequent, financially or legally consequential, or peripheral |
| Recurrence | hit by several participants, repeated by the same participant, or once |
| Affected users and contexts | all users, a segment (new users, assistive technology, mobile), or an edge case |

Levels: **Critical** (blocks the goal or produces an unnoticed wrong outcome for core tasks; fix before release), **Serious** (major difficulty or frequent errors; recoverable with effort), **Moderate** (noticeable friction; recovered unaided), **Minor** (cosmetic or momentary). State the level and the dimensions that drove it.

## 10. Confidence

| Level | Typical basis |
|---|---|
| High | consistent behavioral observation across most sessions, under a valid task, not attributable to a prototype limitation, consistent with other evidence (analytics, prior studies) |
| Moderate | repeated observation in this study, or a single severe observation with a clear mechanism, with minor doubts about task realism or participant fit |
| Low | single or ambiguous observation, possible prototype or moderator effect, participants not matching target, or interpretation rests mainly on self-report |

Confidence is about the interpretation, not about how many users are affected. "High confidence that the label is misunderstood" is possible from a small study; "80% of users misunderstand it" is not.

## 11. Findings template

For each issue: Observation(s) with participant codes; Issue (what is wrong, in design terms); Impact (what it does to the user's goal); Evidence (behavioral, self-report, both); Frequency within study (n of N sessions); Severity and the dimensions behind it; Confidence; Recommendation and owning stage; Related prototype limitation (if any).

## 12. Limitations to report every time

Prototype limitations hit during sessions; participant fit against target users; session count and what it can support; observation and moderator effects; environment (remote, lab, device); any protocol change mid-study; tasks that proved ambiguous; what remains unknown and what evidence would resolve it.

## 13. Reporting

Lead with what the decision-maker needs: the question, the answer the evidence supports, the critical and serious issues, what to do next, and the limits. Keep the full observation log as an appendix or linked file. For small rounds, a short written debrief with an ordered issue list is the deliverable; a slide deck is not more rigorous. Use clips and quotes to carry findings, labeled as examples rather than proof. Never write a population percentage from a qualitative study, and never merge participant opinion, stakeholder opinion, heuristic judgment and benchmark data into one unlabeled "insight".

## 14. Ethics, consent and privacy

Obtain informed consent for participation and separately for recording and for quoting; say who will see recordings and for how long they are kept. Minimize personal data in notes (participant codes, not names). Flag sensitive contexts (health, finance, minors, vulnerable groups) for privacy or legal confirmation rather than deciding alone. Incentives are for time, not outcomes. Participants can stop at any time without losing the incentive.

## 15. Lightweight usability testing

For fast rounds (a few participants, a morning, a sketch or prototype): keep the same discipline on tasks, non-leading moderation and observation notes; relax recruiting with explicit grading on a curve; have observers note the few most serious problems; triage together immediately; fix the most serious issues first; and treat the result as problem discovery, never as proof or measurement. Frequent small rounds beat one late large round.

## 16. Benchmark and quantitative usability studies

Justified when the decision is a comparison against a baseline, a prior version or a competitor, and when the protocol can be held constant. Requirements: fixed tasks and wording, fixed success definitions, no think-aloud during timed tasks, consistent environment and device, enough valid sessions for the comparison the decision needs (the number depends on the measure's variability and the difference that matters; it cannot be stated without those inputs), and no changes mid-study. Report effectiveness (completion), efficiency (time, steps) and satisfaction (standardized questionnaire) separately. Do not describe differences as statistically significant unless an appropriate analysis was actually run on the data; otherwise report the observed values and their limits.

## 17. Heuristic and expert evaluation

An expert walkthrough against recognized principles is fast and useful for catching obvious problems before testing, for scoping a study, and when no participants are available. It is expert judgment, not user evidence: label its output as heuristic findings, give it lower confidence than observed behavior, and never report it as "users struggled".

## 18. Accessibility in studies

Include assistive-technology users when the product will be used that way or any accessibility claim is made. Validate keyboard-only completion of each core path. Check zoom and text enlargement, screen-reader order and announcements, reduced motion, and alternative input. Automated checks find a subset of defects (contrast, missing names, structure); they cannot show whether a person can complete the task. Report accessibility findings with the same chain and severity model, and route code-level defects to engineering.

## 19. Evidence quality gates for this mode

Flag when: tasks leak the answer; success criteria were written after results; a prototype limitation is reported as a user failure; assistance is not logged or assisted completions are counted as completions; observations and interpretations are mixed; counts become percentages of users; satisfaction is reported as usability; participants were invented or results extrapolated beyond the sessions; accessibility is claimed from automated checks alone; findings redesign a stage this skill does not own instead of routing to it.

## 20. Generative and exploratory interview studies

Use when an explicit research question exists about needs, workflows, motivations, mental models, language or context of use ("How do freelance designers currently find and evaluate project-management tools?"). If the question is still whether an opportunity deserves pursuit, that framing belongs to `product-discovery-framing`; this section starts once the question is set, and its findings go back to whoever owns the product decision.

- **Plan**: the decision the findings will inform, the research question broken into a few learning goals, and the rows of the section 1 plan that apply.
- **Participants**: recruit on the behavior in the question (people who did the thing recently, in the relevant context), with quotas for the variation that matters (for example, people who adopted a tool and people who abandoned one). Decide deliberately whether current customers are included; recruiting only them biases findings toward people who already chose the product.
- **Guide structure**: consent and purpose; brief context about the participant's work; reconstruction of one or two recent, concrete episodes ("Tell me about the last time you looked for a tool to manage a project. What prompted it?"), followed step by step (where they looked, whom they asked, what they compared, how they decided, what happened next); probes that ask for examples and reasons ("What made that matter?", "Can you show me?"); wrap-up. Map every question block to a learning goal and drop questions that serve none.
- **Question rules**: open and neutral; past behavior over opinion or prediction; no yes/no questions at the core; never name or pitch our product, a concept or a feature before the participant raises it; no "would you use..." or "how much would you pay" questions, which produce stated intent, not behavior; follow the participant's words rather than introducing ours.
- **Capture**: participant codes, verbatim quotes in quotation marks, behaviors and artifacts shown kept apart from interpretation (section 7 structure); recording and quoting only with consent (section 14).
- **Analysis**: one observation per card, clustered across participants into patterns; keep contradicting and negative cases; report counts within the study ("n of N participants"); keep need statements in the participants' terms.
- **Limits**: findings describe the people interviewed. "Several participants mentioned X" never becomes "users generally want X". Interviews do not establish prevalence, population frequency, willingness to pay or causal effects, and recall of past episodes is imperfect. If the decision needs magnitude, name the follow-up instrument (a survey designed from these findings, or analytics) instead of stretching the interviews.

Flag when: the guide leads toward our product or a feature; questions ask participants to predict their own behavior; counts become percentages; themes are reported as the needs of users in general; findings are used to make the opportunity decision instead of informing whoever owns it.

## 21. IA validation studies scoped by `ux-architecture`

`ux-architecture` decides which IA question is risky enough to test, whether a card sort or tree test fits, and owns the structure under test. When asked to turn that into a study, this skill supplies the protocol and the evidence discipline:

- **Inputs required from IA**: the question, the tree or card set under test, and the destinations that count as correct for each task. Never invent the hierarchy, the labels or the correct answers.
- **Participants**: behavior-based criteria as in section 2, matched to the people who will use the structure.
- **Tasks**: goal-phrased and non-leading as in section 3. A tree-test task never contains the label of its target node; an open card-sort brief never suggests category names.
- **Success criteria fixed in advance** (section 4): the correct destination or destinations, and whether direct paths are distinguished from paths with backtracking.
- **Capture**: per task, the path, first choice, final destination and any skip; per card sort, the groupings and participant-created labels.
- **Analysis and limits**: report results within the study. A quantitative tree test needs enough participants for the claim the decision needs, and that number depends on inputs that must be stated, not assumed. Findings that the structure is wrong go back to `ux-architecture` with their evidence chain; do not redesign the hierarchy here.

## 22. Supplied feedback and request corpora

Use this only when asked to analyze supplied tickets, reviews, survey comments or feature requests. Reviewing existing findings to frame a product decision remains discovery work; this section governs analysis of the underlying records.

- Preserve source/record identifiers and the original wording in a non-destructive working view. State the records available, analyzed and excluded, with reasons; do not imply full coverage after sampling.
- Distinguish mentions from distinct respondents or accounts where supplied identifiers permit. Repeated tickets are not additional users; similar wording alone is not proof of duplicate identity. Leave unique-requester counts Unknown when they cannot be established.
- Group requests by the underlying need while retaining the original ask and its evidence. Allow multiple themes per record and disclose overlapping counts. Keep contradictory needs and low-frequency severe issues visible rather than ranking only by volume.
- Use supplied segment metadata, not guessed demographics or personas. Counts describe this corpus, not prevalence in the user population.
- Treat sentiment as an approximate analyst label: retain mixed or uncertain readings and flag language ambiguity or sarcasm. Do not manufacture an NPS score or substitute sentiment for demand, satisfaction measurement or observed behavior.
- Link each material theme to source records. Keep quoted observation, inferred need or cause, and recommendation distinct; a stated churn threat is not observed churn. Report missing context and counter-evidence that could change the decision.

Use the smallest output that serves the request; no required theme count, persona, chart or enriched export. Create an export only when needed for the requested deliverable, preserving raw data and privacy constraints. Hand product priorities back to discovery and design changes to their existing owners. No supplied evidence means hypotheses or an evidence request, not synthesized research findings.
