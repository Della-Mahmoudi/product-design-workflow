# Multi-Step Work and Final QA

Use this for work with more than one step. One-step work in chat needs no state block.

## State
Keep a compact block in chat and update it after each decision from the designer:

```
task_goal:
required_output:
acceptance_criteria:
approved_scope_changes:   # omit if none
steps:                    # S1 <name> [todo|in_progress|awaiting_review|accepted|dropped]
current_step:
accepted_results_summary: # 1-2 lines per accepted step, or pointers to outputs
human_direction:          # latest decision, in the designer's words
next_action:
```

- Do not store full chat, raw logs or large deliverables. Point to outputs instead.
- Save a small state file only when work spans sessions. Put it in the designer's task workspace, not inside the plugin.
- You may reorder or merge technical substeps within the agreed goal. Changes to scope, product decisions or priorities need the designer's direction. Preserve approved scope and manual edits; revisions affect only the necessary portion. Completed technical work is not automatically accepted.

## Progress within a stage
- Within the current stage, continue authorized execution, self-review and safe objective in-scope repair without a new approval for every internal result.
- Present the checked coherent stage result and wait for the designer's direction before the next stage. Do not manufacture gates for technical substeps.
- Also pause for a consequential product, intent or taste choice, material scope trade-off, missing authority or unresolved side effects.
- Retries need a concrete diagnosis, safe idempotent execution and expected progress within authority. Check the outcome of an uncertain write or paid call first. Stop recurring cycles without a new useful diagnosis; never lower criteria to manufacture completion.

## Applying the designer's reply
- Accept: mark the step accepted, summarize it and set the next action.
- Revise: change only the affected part and keep accepted work.
- Retry: do only the specific action approved.
- Change direction: update the steps and record the approved scope change.
- Stop: halt and leave the state accurate.

## External handoff
When delegating, give the worker the accepted context, sources and relevant feedback it needs, not full history. Instruct it to read relevant domain standards, check its output, correct clear authorized defects, and stop on missing decisions, authority, uncertain side effects or lack of progress. Inspect returned work before presenting the coherent stage result.

## Resume
After a new session or context loss, rebuild state from the latest block or file, restate the current step and next action in one line, and wait if a decision is pending. Do not redo accepted steps.

## Final QA
When all required steps are accepted, set status `final_ready` and call `product-design-workflow:independent-final-qa` with the Agent tool as a new call, not a fork or resumed agent. Self-review is never a substitute. QA agent tool access: Instructed not to write. Edit, Write, MultiEdit, NotebookEdit and Bash are blocked; it still inherits MCP tools from your session, so connected write tools (e.g. Figma, Gmail) are not technically blocked.

Send only scope and the deliverable:

```
invocation_status: final_ready
initial_scope:                 # original brief, including how-to-work constraints
approved_requirement_changes:  # only those the designer approved, else "none"
required_output:
acceptance_criteria:           # criteria observable in the deliverable
final_deliverable:             # content, or files/URLs/preview to inspect
domain_criteria:               # optional
```

Do not include chat history, the state block, drafts, rejected work, your own judgment or earlier verdicts.

Show every report to the designer unchanged. Put any disagreement in a separate labelled note. Constraints on how the work was done cannot be checked from the deliverable, so report them separately as verified or unknown. If a required one is still unknown, overall delivery stays pending even when QA passes. After every QA report or failed call, pause for the designer: do not automatically repair, retry, resubmit or switch reviewers. The designer decides to accept, revise or stop. A revised deliverable needs a new fresh QA call with requirements and the revised deliverable only.
