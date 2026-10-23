# Multi-Step Work and Final QA

Use this for work with more than one step. One-step work in chat needs no state block.

## State
Keep a compact block in chat and update it after each decision from the designer:

```
task_goal:
required_output:
acceptance_criteria:
approved_scope_changes:   # omit if none
steps:                    # S1 <name> [accepted|in_review|todo|dropped]
current_step:
accepted_results_summary: # 1-2 lines per accepted step, or pointers to outputs
human_direction:          # latest decision, in the designer's words
next_action:
```

- Do not store full chat, raw logs or large deliverables. Point to outputs instead.
- Save a small state file only when work spans sessions. Put it in the designer's task workspace, not inside the plugin.
- You may reorder or merge technical substeps within the agreed goal. Changes to scope, product decisions or priorities need the designer's direction.

## Applying the designer's reply
- Accept: mark the step accepted, summarize it and set the next action.
- Revise: change only the affected part and keep accepted work.
- Retry: do only the specific action approved.
- Change direction: update the steps and record the approved scope change.
- Stop: halt and leave the state accurate.

## Resume
After a new session or context loss, rebuild state from the latest block or file, restate the current step and next action in one line, and wait if a decision is pending. Do not redo accepted steps.

## Final QA
When all required steps are accepted, set status `final_ready` and call `product-design-workflow:independent-final-qa` with the Agent tool as a new call, not a fork or resumed agent. QA agent tool access: Instructed not to write. Edit, Write, MultiEdit, NotebookEdit and Bash are blocked; it still inherits MCP tools from your session, so connected write tools (e.g. Figma, Gmail) are not technically blocked.

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

Show the report to the designer unchanged. Put any disagreement in a separate labelled note. Constraints on how the work was done cannot be checked from the deliverable, so report them separately as verified or unknown. The designer decides to accept, revise or stop. A revised deliverable needs a new QA call.
