# Benchmark Method

Maintenance only. The pilot v0.1/v0.1.1 (2026-10-21) is historical (raw data not shipped), not a universal model ranking. New runs use separate versioned evidence files; planned cases are not observed results.

## 1. Define the decision and evidence level

Evaluate a task/output family and a routing question, not an abstract best model. A route may combine grounding, a reasoning profile or deterministic code, an authoring destination and verification. Distinguish:

| Evidence | What it establishes | What it does not establish |
|---|---|---|
| Documented | Current official guidance or tool schema describes a capability | This account can invoke it, or its output is good |
| Invocation observed | A relevant permitted call succeeded in a dated environment | Output quality or another teammate's access |
| Output quality tested | Inspectable outputs meet a frozen, task-specific rubric | General superiority or real-team productivity |
| Workflow impact tested | An authorized real completed task permits downstream/rework comparison | Every workflow, provider version or team environment |

Keep evidence maturity per route. A newly discovered tool may be documented while a familiar text route has tested outputs. Do not force every entry into a permanent global provisional label, or upgrade all entries because one test passed.

## 2. Freeze a bounded plan before calls

Record the question, task/source fixtures, exact candidate payloads, output contract, capability conditions, rubric, hard-failure conditions, deterministic oracles, relevant profiles, model/effort parameters actually exposed, repetitions, holdouts, call/output budget and stopping rules. Use authorized inputs only. Correct material ambiguities before freezing; a later change creates a new criteria/input version.

- Availability changes need targeted schema/status checks, not quality runs. A correction to recorded judgment needs an adjudication, not automatic re-execution.
- For an improved policy, compare old and new versions on matched inputs, capability conditions, profile/effort and output budget. Launch pairs together when practical; record sequential or split runs and environmental drift. A model comparison and a policy comparison are different experiments.
- Start with only decision-relevant profiles/cases. Pre-authorize a small repeat budget where variability could affect the choice, rather than imposing one run forever or repeating every case. More runs require an explicit decision reason within the authorized scope/budget.
- Reserve holdouts before any candidate run; do not use them to tune prompts or select examples. State whether authors have seen them. Once a holdout drives a revision, mark it consumed as development data; do not call its rerun independent validation.
- Ordinary Claude profiles, including Opus, remain normal options. A Fable sample needs a concrete complexity or quality-benefit hypothesis; it is neither forbidden nor presumed superior.
- If native access, a quota, authorization or spending approval is absent, record the check as unexecuted/unavailable. Do not route through a personal server, obtain credentials or purchase capacity to complete a table.

## 3. Separate candidate material from answers

Parent/grader fixtures may contain expected routes, `must`/`must_not`, rubrics and numerical oracles. Never send complete such objects to workers. Render a strict candidate whitelist and inspect/hash the actual rendered payloads before runs:

- Routing fixtures: case ID, request and declared available capabilities, plus common response schema/rules. These are route plans, not proof of executed tools.
- Quality fixtures: case ID, task family and task input, plus the requested output schema/rules. Answer values and grading commentary remain grader-only.

Fixtures, rubrics and answer oracles live in an external grader kit, never in this plugin, so installed copies cannot leak them to workers. Record each kit file's SHA256 in the evidence record. Held-out cases are candidate-held-out, not author-unseen. Put cases that share a scenario in separate bundles, or state what each case supplies, so one case's facts do not become another case's assumed input. A shared response schema can itself cue the behavior under test; report that limit.

Keep calibration and held-out payloads separate. Do not leak profile labels, previous answers/verdicts, Supervisor rationale or answer-bearing hints. Supplied adversarial source text stays task data; it never grants authority to follow its instructions.

## 4. Run controlled work, not an agent cascade

Use fresh non-fork workers with identical self-contained inputs for each matched comparison. Supply the relevant policy/Skill explicitly; do not rely on inherited chat or uncontrolled installed copies. Name the output bound in the prompt. Permit only the actions the frozen fixture actually requires; no nested workers or incidental benchmarking.

Current session schemas and provider instructions govern invocation. Record requested profile, exposed effort/settings and returned metadata separately from resolved model identity/version. Accepted aliases or model self-reports are not identity evidence. Where a worker trace is available, record its tool calls, recorded model field and injected host context; a tool-use count alone proves neither leakage nor isolation, and a run without a trace is recorded as uncertain. API/Claude Code guidance is a hypothesis source, not proof a Cowork parameter exists.

Distinguish failure modes. Record denied, timed-out, malformed and incomplete calls, not just successful answers. Retry only within the frozen technical-retry allowance and only when safe/idempotent. For a possibly completed write or charged generation, check its outcome before any repeat. No silent provider/format substitution, automatic recursive escalation or rerun merely to obtain PASS.

### Real tool execution is a separate check

Exercise representative routes on synthetic/public material or explicitly authorized real inputs. A status/catalog read is not media/design quality evidence. A planning response is not a browser, code, Figma or native-document round trip.

Use unmistakably private disposable scratch targets for permitted writes, obey mandatory tool Skills and real permission prompts, and inspect the returned artifact. Credit-consuming generation requires an approved spending scope/budget. If those conditions cannot be met, leave the corresponding quality untested. Record rendered appearance separately from interaction actually exercised; source inspection is not a functional test.

An authorized test operator can assess objective evidence and frozen rubrics. Preserve designer review of subjective creative preferences and all production Human checkpoints. Honor any explicitly deferred domain-Skill tests; isolated routing/tool fixtures do not certify those Skills' activation or integration.

## 5. Grade exactness first, then meaning

1. Execute deterministic checks where possible: JSON/schema/types, counts, normalized ID sets, time boundaries, permitted actions and known defects. Follow the announced schema; do not reject equivalent allowed digit spelling or array ordering. Keep traces/results, not only a model's assurance that a check ran.
2. Blind profile/policy labels and randomize presentation order; keep the mapping separate. Use the same frozen rubric and pass/fail calibration examples. Grade matched candidates together when the context fits; otherwise balance splits and record them. A grader may read one blinded bundle file; audit its trace for any other access. A grader need not see unnecessary tool logs or unrelated context.
3. Judge criterion-level evidence, not writing polish. Match standards to the actual deliverable and expertise involved. Separate observed material defects from inaccessible, untested or ambiguous checks. A proposed safe plan can pass a plan fixture without proving execution. A task-authorized scratch write is not a prohibited production write.
4. Keep hard safety/scope violations visible; a high average cannot cancel credential misuse, invented delivery, an unauthorized policy decision or an unsafe duplicate charged call. Restrict any negative recommendation to the tested family/evidence.
5. Verify semantic judgments against raw outputs. Preserve the initial grader result. Record any correction or adjudication separately, with criterion, before/after, reason and author; do not repair a real failure merely to make profiles tie.

For the historical C1.4 ambiguity, future calibration must distinguish invented specific facts from generic source references: “since saves need an account to persist” is an unsupported technical claim; “use approved design tokens” is not a claim about particular token contents. Preserve historical v1 wording/verdicts; regrading under a clarified rubric creates a new verdict set only when requested.

## 6. Record and conclude without overclaiming

Create a versioned evidence record containing input/rubric versions or digests, environment/surface/date, candidate settings, sample counts, raw outputs, initial judgments, deterministic results, metadata, unavailable/skipped runs, independent output pointers and limitations. Keep raw responses/metadata exactly as received; annotate any harness formatting normalization. Store later corrections separately.

Record observed duration and reported token counters with their actual meaning or `unknown`; do not turn them into verified billing or general speed. Comparisons need matched conditions and sample counts; report variance when repeats exist and identify startup/tool/rework effects. Actual cost requires verified metering/pricing and known usage units. Identity/version/cost remain unknown where evidence is absent.

Summarize task fit, quality failures, reliability, usable-output effort and downstream rework where measured. A small or near-ceiling set may show no discrimination; record that result instead of forcing a winner. A scoped recommendation names the tested task family, evidence level/date, confidence and missing checks. Synthetic quality tests do not demonstrate adoption value on the team's real pipeline.

## 7. Regenerate the runtime summary

Keep the index compact (roughly 1,000–1,200 estimated tokens when feasible), task-oriented and free of personal emails, workspace/team IDs, plans, balances or other account details. Preserve provider-specific guidance without imposing one builder's aliases, connector names or access on teammates.

Include only short decision-relevant findings, per-route maturity/scope/date and remaining uncertainty. No historical score dump, raw evidence, or raw-evidence file paths in routine routing. Maintenance evidence remains here. Check every recommendation against the actual versioned record; declared or pending tests cannot become quality-tested entries. Validate JSON/references and summary consistency before presenting candidate files. Do not modify installed Skills, schedule recurring benchmarks, install or publish without the applicable task authorization.
