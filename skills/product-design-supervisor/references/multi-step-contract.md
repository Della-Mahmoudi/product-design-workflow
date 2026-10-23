# Multi-Step Contract (state + handoff)

Load only for multi-step coordination or an external handoff. One-step in-chat work needs no state block, state file or package.

## State
Keep a compact in-chat block, updated after each Human decision:

```
task_goal:
required_output:
acceptance_criteria:
approved_scope_changes:   # only explicitly approved; omit if none
steps:                    # short list: S1 <name> [accepted|in_review|todo|dropped]
current_step:
accepted_results_summary: # 1-2 lines per accepted step, or output pointers
human_direction:          # latest Human decision in their words (accept, revise, retry, redirect, stop), with any correction
next_action:
```

Rules:
- Never store full chat, raw tool logs or duplicated large deliverables; point to outputs instead.
- Persist one small state file only when continuity genuinely requires it (long gap, likely context loss, multiple sessions). Save it in the user's selected task workspace, never inside the installed Skill or its references. Update the compact current state.
- Steps follow genuine dependency or Human decision boundaries, not a fixed count. Within the agreed goal and output you may reorder technical work or add, merge or drop implementation substeps without a formal Replan; that never skips a result checkpoint, changes scope, redoes accepted work or overrides a Human decision. Material scope, product, priority or output trade-offs need Human direction.

## Step package (external execution only)
Give the executor what the step needs without relying on chat history.

```
goal:
inputs:        # accepted context, sources/files/pointers, actionable feedback and prior findings the step needs
instructions:  # concise method, usable domain Skill; on failure, stop and report without retrying
constraints:   # scope, standards, approved changes, target/permissions, things not to change
required_output: # smallest sufficient format, required native/editable properties
acceptance_criteria: # checkable properties and necessary verification/evidence
```

Exclude full history and unrelated steps; include a rejected draft, earlier finding or Supervisor feedback only when the assigned correction needs it. A Worker may be resumed or reused where the runtime supports it, and a dependent step starts once its prerequisite inputs are ready or accepted. Only Final QA must be fresh and history-free.

Supply the minimum facts and source access the executor needs; a pointer alone is insufficient when the worker cannot open it. Missing required evidence or capability is a gap to report, not permission to invent facts, change the destination or expand access. No packet is needed for direct in-chat execution.

## Human gate
After each meaningful result, including every returned Worker or executor result or failure: say what was produced, your check against the criteria (pass, issues, unchecked), important misses and a recommendation; then wait.

The Human answers in their own words. Read the intent and act on a clear one without a second formal confirmation. Common intents, not required wording:

- Accept: mark the step accepted, summarize it, set next_action; continue only to that step.
- Revise or edit: apply the correction to the affected portion only, keep accepted work, report the revised result.
- Retry or re-run: perform only the specific action authorized.
- Replan or change direction: update steps and record approved scope changes; ask once only if materially ambiguous.
- Stop: halt and leave state accurate.

A bare thanks, or an unclear or mixed reply, is not a go-ahead; ask only what is needed to proceed.

- No repair, retry, re-run or escalation happens without Human direction. Inspecting existing status or results is diagnosis, not re-execution; an uncertain charged or write action is never blindly repeated.
- A general or advance approval does not skip result checkpoints. Routine reads and checks inside an authorized step are not separate gates.
- A request that conflicts with a binding requirement or standard: explain the conflict, offer options (including an approved scope or design change) and let the Human choose. Advisory conventions and style preferences are not conflicts.

## Resume
On a new session or context loss: re-apply the core, rebuild state from the latest in-chat block or the state file, restate current_step and next_action in one line, and wait if a Human decision is pending. Never redo accepted steps.

## Final QA
When all required steps are accepted, set status `final_ready`; it is a technical marker, not project history. Then:
1. Invoke this plugin's agent (listed as `product-design-workflow:independent-final-qa`) with the Agent tool as a new call: not a fork, not a resumed or messaged agent, and never an authoring Worker. The agent's default model is inherit; another supported profile is fine where the runtime exposes one.
2. Send a scope-only packet:
   ```
   invocation_status: final_ready
   initial_scope:                 # original brief, including execution-only constraints
   approved_requirement_changes:  # explicitly Human-approved only, else "none"
   required_output:
   acceptance_criteria:           # applicable criteria observable in the deliverable
   final_deliverable:             # content, or the files/URLs/preview to inspect
   domain_criteria:               # relevant domain standards, if any
   ```
   Scope (brief, approved changes, required output, applicable criteria) and `final_deliverable` are the minimum; the reviewer derives clear criteria from them and the relevant domain Skills instead of blocking on an absent redundant field. These are requirements, not history. Never include chat or workflow history, the state block or file, intermediate drafts, rejected work, Supervisor judgment, earlier verdicts or learned user memory. Keep execution-only constraints in `initial_scope`; list in the criteria only what is observable in the deliverable, unless the Human explicitly made independently evidenced compliance a release condition, in which case list it and supply that evidence with the deliverable.
3. Show the report to the Human unchanged. Put any Supervisor disagreement in a separate, labelled note; never edit, merge or override the verdict. Report execution-only compliance separately, as verified or `unknown`; never call unknown compliance met or silently waive it. If a required execution obligation is unresolved, overall delivery stays pending even when QA is PASS.
4. The Human decides accept, revise or stop. Checking a revised deliverable needs a new fresh invocation.
5. The reviewer is chosen before invocation. If the agent is unavailable, or its fixed tool bindings cannot inspect the required deliverable in this runtime, use an equivalent fresh, non-fork independent reviewer whose actually exposed tools can inspect it, with the identical scope-only packet, domain standards and no-edit, inspection and reporting rules, where the runtime supports it. Judge this only from relevant schema or tool metadata already available: no blanket connector discovery or probes, no assumed access and no expanded permissions. Never review as QA yourself or reuse an authoring Worker. If no real capable equivalent exists, report `final_ready / QA_pending` (BLOCKED: QA unavailable) and never claim PASS. After any returned QA report, BLOCKED or invalid-invocation result, or failed call, show it unchanged and pause for the Human: do not retry, rebuild and resubmit the packet, or switch to a fallback reviewer on your own. Reading existing status to diagnose is allowed. If the Human authorizes a repair or new invocation, rebuild the packet from the requirements and the final deliverable only, never adding forbidden context.
