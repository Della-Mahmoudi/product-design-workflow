# Feedback, errors and recovery

Load for feedback and status, loading and latency, asynchronous operations, validation and error messages, undo/cancel/back/retry, destructive or high-consequence actions, partial failure, offline behavior, stale data and conflicts, sessions and lost permissions, interruptions, and interaction copy. Focus and announcement mechanics are in `accessibility-and-platform.md` §3–5.

Sections: 1 Feedback · 2 Latency and progress · 3 The async contract · 4 Validation and input errors · 5 Prevention before messages · 6 Undo, cancel, back, retry · 7 Destructive and high-consequence actions · 8 Partial failure and batches · 9 Offline and unreliable networks · 10 Stale data and conflicts · 11 Sessions, permissions, interruptions · 12 Choosing edge cases · 13 Interaction copy

## 1 Feedback

- **Every meaningful action gets perceivable feedback** that is immediate, informative and proportionate. Too much feedback trains people to ignore it, so prioritize. (DOET Ch 1 "Feedback")
- **Match the interruption to the significance.** Status belongs in passive, in-context indicators; interrupt only for unexpected, irreversible loss or a decision the user must make now. (Apple Feedback, Alerts; AF CH11 "Avoid unnecessary reporting"; AF CH21 "Don't use dialogs to report normalcy")
- **Put feedback where the action happened**, and keep ongoing status persistently visible rather than in dialogs. (AF CH15 "Using Rich Modeless Feedback"; Apple Feedback)
- **Confirm significant completions only.** People expect routine actions to work and mainly need to hear when they don't. (Apple Feedback)
- **When a command can't run, say so and why**, at the point of action. (Apple Feedback)
- **Use more than one channel**: text plus icon or shape, never color alone; on native platforms pair sound with haptics. Don't use silence as the failure signal. (WCAG 1.4.1; Apple Accessibility; the conflict with AF CH15's audio advice is in the source map)
- **Timed messages lose people.** Don't put critical information, or the only route to recovery, in a message that disappears on a timer. Prefer persistent or user-dismissed messages; if one must time out, make the time generous or adjustable and keep the action reachable elsewhere. (Carbon Notifications "Accessibility"; Apple Accessibility "Minimize use of time-boxed interface elements"; AF CH16 "Use response times that support all users")

## 2 Latency and progress

These are perceptual heuristics, not requirements; a design system may set its own values. (AF CH11 "Optimize for responsiveness but accommodate latency"; AF CH17 "Respond to commands"; DOET Ch 1 "Feedback", Ch 2 "Blaming the Wrong Things"; DI Ch 8 "Spinners and Loading Indicators")

| Expected wait | Behavior |
|---|---|
| Up to about 0.1 s | Feels instant: show the result, no indicator |
| About 0.1–1 s | Acknowledge on the control itself (pressed or busy state) |
| More than about 1–2 s | An indicator in place, next to what is working; the rest of the interface stays usable |
| Up to about 10 s | A progress indicator, determinate when progress can be measured |
| More than about 10 s | Determinate progress and an estimate where possible, Cancel, and freedom to do other work while it runs, with a completion notice `[confirm: engineering]` |

- **Show something as soon as possible**: render what is ready; use placeholders or skeletons for container and data components on initial load, not for buttons, inputs, toasts, menus or the modal itself. (Apple Loading; Carbon Loading "Skeleton states")
- **Indeterminate when the duration is unknown, determinate when known.** (Apple Loading)
- **Background refresh** keeps the current content visible and signals new content without shifting the layout under the user.
- **Scope the busy state** to the component that is working. Block the whole interface only when the action really makes the app unusable meanwhile. (Carbon Loading "Full-screen loading", "Inline loading")
- **Slow feedback makes people repeat the action**, which can double or cancel the request, so design for repeated activation (§3). (DOET Ch 2 "Blaming the Wrong Things")

## 3 The async contract

Default lifecycle for any request the user waits on: **Idle → Pending → Succeeded | Failed | Unknown (timed out) | Cancelled** (the last only if cancelling is supported). For each state, specify the control's state, the indicator, the text, the announcement and the exit.

- **Pending**: acknowledge immediately; prevent or ignore repeat activation and show that the request is in progress; keep the inputs.
- **Duplicates**: client-side prevention is a courtesy; the server must still deduplicate `[confirm: engineering]`. On slow connections show progress before blocking repeat clicks. (GOV.UK Button, on preventing double submission)
- **Failure**: keep everything the user entered; say what failed in their terms and what they can do; offer Retry only when repeating is safe.
- **Unknown outcome** (timeout, dropped connection): don't guess. Say the result is unknown and offer "Check status" or a refresh rather than a blind retry, unless the operation is known to be safe to repeat `[confirm: engineering]`.
- **Retry**: a user-initiated retry keeps inputs and context; automatic retries only for operations engineering confirms are safe to repeat (idempotent).
- **Cancel** must really stop the work, or the interface must say what it couldn't stop ("Files already sent stay sent"). Put Cancel next to the progress it cancels; it should take effect quickly and confirm that it did; parallel operations get individual cancels. Whether the server can abort is `[confirm: engineering]`. (AF CH8 "Considerate products take responsibility"; DI Ch 8 "Cancelability")
- **Cancel and Remove are different intents.** For items in a batch, cancelling must not silently discard what the user chose: keep the item as Cancelled with a way to start it again, or remove it with a brief undo, and offer Remove as its own action.
- **Optimistic updates** (showing success before the server confirms) only when success is very likely, the change is low-stakes and reversible, and the rollback and its message are designed `[confirm: engineering]`. Never for payments, deleting shared data, or anything other people will act on immediately. This trades against "persist before acknowledging receipt". (AF CH8 "Considerate products fail gracefully")
- **Leaving mid-operation**: if work continues on the server, say so and where the result will appear; if it would be lost, guard the exit (§11) `[confirm: engineering]`.

## 4 Validation and input errors

- **Prevent first** (§5): constraints, forgiving formats, good defaults, clear hints. (GOV.UK Validation; AF CH21 "Making errors impossible")
- **Timing.** Follow the product's design system. Without one, validate multi-field and transactional forms when the user submits or continues, not on blur and not while typing, and never flag valid input that is still being entered. Live checks only where they clearly help (a remaining-character count) and are announced accessibly. If the system validates on blur, remove each error as soon as it is fixed. (GOV.UK "Recover from validation errors"; DI Ch 10 "Error Messages"; Carbon Dialogs and Modal "Validation"; the conflict is resolved in the source map)
- **Show**: a message beside each failing field naming the problem and the fix; beyond one or two fields, also an error summary at the top that links to each field and receives focus after a failed submit; in page-based flows, prefix the page title with "Error:". (GOV.UK Error summary, Error message; WCAG 3.3.1, 3.3.3)
- **Keep every answer the user entered**, valid or not, so they can see what went wrong and fix it without retyping. (GOV.UK Error message)
- **Mark errors with text plus an icon or shape**, not color alone, and tie each message to its field programmatically (accessibility file §4). (WCAG 1.4.1, 3.3.1)
- **Prefer an enabled submit that explains what's missing** over a submit that stays disabled until everything is valid. If the design system disables it, show the requirements visibly next to it. (GOV.UK Button, on disabled buttons; DI Ch 10 "Error Messages" recommends disabling; see the source map)
- **Server-side validation is authoritative**; client-side validation is a convenience `[confirm: engineering]`. (GOV.UK Validation)
- **Not validation errors**: eligibility, permission and service failures. Explain on the page or in the state what happened and what to do next. (GOV.UK Error message, when not to use)

## 5 Prevention before messages

Prefer the earliest layer that works:

1. **Design the error out**: constraints, forcing functions, bounded inputs where the valid set is small, good defaults, values the system can supply itself. (DOET Ch 4 "Constraints That Force the Desired Behavior"; AF CH21 "How to eliminate error messages")
2. **Make it reversible**: undo, restore, versions. (AF CH21 "Make all actions reversible"; DOET Ch 5 "Undo")
3. **Warn without blocking** before commit: flag a likely slip inline and still let the user proceed. (AF CH8 "Considerate products help you avoid awkward mistakes"; AF CH21 "Provide modeless feedback to help users avoid mistakes")
4. **Confirm** only when the action is irreversible or costly and not routine (§7).
5. **Detect, explain, and support recovery** (§4, §6).

In short: prevent, then explain, then recover, wherever each applies. Not every failure can be prevented, and prevention that costs more friction than the error it stops is a bad trade.

**Classify the failure before designing the response**; each type has its own handling.

| Type | Example | Handling |
|---|---|---|
| User slip or mistake | Deleted the wrong item; misread a plan | The prevention layers above; undo where it really exists (§6) |
| Validation issue | Required field empty; date in the past | Message at the field plus a summary; input kept (§4) |
| Permission or eligibility | Role lacks the right; plan doesn't include the feature | Not a validation error: explain why and the available path (§11; behavior file §7) |
| Network or system failure | Timeout, server error, connection lost | Keep the input; say what is known; Retry only if repeating is safe; "Check status" when the outcome is unknown (§3, §9) |
| Partial failure | 17 of 20 files uploaded | Per-item and aggregate result; keep the successes (§8) |
| Conflict or stale data | Changed or deleted by someone else | Never overwrite silently (§10) |
| Unavailable capability | No undo, restore or offline support exists | Say so plainly; never imply a recovery the system can't perform (§6, §7) |

Whatever the type: keep what the user entered, say what happened and what they can do next, and keep raw technical detail (codes, stack traces) out of the message unless it helps them act (§13).

Slips and mistakes need different fixes. (DOET Ch 5 "The Classification of Slips", "The Classification of Mistakes")

| Failure | What happens | Countermeasure |
|---|---|---|
| Capture slip | A familiar sequence takes over | Make sequences differ from their first step |
| Description-similarity slip | Similar controls get confused | Distinct appearance and separation; keep destructive controls away from frequent ones |
| Mode error | Input means different things in different modes | Remove modes, or make the current mode unmistakable |
| Memory-lapse slip | A step is forgotten, often after an interruption | Fewer steps, reminders, a forcing function |
| Rule- or knowledge-based mistake | The plan itself is wrong | A clearer conceptual model, visible state, previews, sensibility checks on unusual values |

**Confirmations are ill-timed**: people asked to confirm are usually already sure, and they attend to the action rather than the object. A confirmation helps when the action was an unintended slip (the surprise alerts them) and is ignored when the plan was a mistake. If you confirm, make the action, the object and the implications prominent, and still prefer undo. (DOET Ch 5 "Confirmation and Error Messages"; DI Ch 1 "Habituation")

**Forcing functions** (interlocks enforce order, lock-ins prevent premature exit, lockouts block danger) work only while their nuisance stays low; otherwise people defeat them. (DOET Ch 4 "Constraints That Force the Desired Behavior")

## 6 Undo, cancel, back, retry

| Exit | Means | Requires |
|---|---|---|
| Undo | Reverse a completed action | The system keeps reversible state `[confirm: engineering]` |
| Cancel | Abandon an operation or dialog in progress without committing | The work can actually be stopped (§3) |
| Back | Return to the previous step with entries intact | State preserved per step |
| Retry | Repeat a failed attempt with the same inputs | Repeating is safe (§3) |
| Discard or revert | Throw away unsaved changes | A warning when it destroys the user's work; ideally undoable (AF CH14 "Fixing data storage: a unified file model") |

- **Undo rules**: allow multiple levels; say what will be undone ("Undo Move"); show the result even if it is off screen; undo covers content changes, not selection, scrolling or navigation. (Apple Undo and redo; DI Ch 8 "Multilevel Undo"; AF CH15 "Undo, Redo, and Reversible Histories")
- **A timed "Undo" in a toast** needs deferred commit or a real reversal path `[confirm: engineering]`, plus an accessible duration and another route to the same undo (§1). Once something has reached other people or external systems (sent, paid, synced), undo may be impossible: say so rather than implying it.
- **Choosing**: frequent and reversible → act at once and offer undo, without confirmation. (AF CH8 "Considerate products are self-confident"; AF CH21 "Do; don't ask"; Apple Alerts "Avoid displaying alerts for common, undoable actions") Uncommon and irreversible → confirm. (Apple Alerts) Submissions that create legal commitments or financial transactions, or that modify or delete user-controllable data, must be reversible, checked, or confirmed. `[required: WCAG 3.3.4]`

## 7 Destructive and high-consequence actions

**Assess first.** Is it reversible, by what mechanism, for how long `[confirm]`? Who else is affected: collaborators, shared data, integrations, billing? How much is lost? Is it frequent (habituation) or rare? Did the user choose it deliberately, or is it a side effect of something else? Rate by the worst of these: a restore window lowers the tier only if restoring is complete and self-service `[confirm]`, and losing other people's access or work keeps it high.

| Impact | Typical case | Behavior |
|---|---|---|
| Low | Reversible or trivial; the user's own data | Act at once; offer undo or restore; no modal (Carbon Remove "Low-impact deletion"; Apple Alerts) |
| Medium | Irreversible but limited, or reversible but affects others | A confirmation naming the object and consequences; a specific verb button and Cancel (Carbon Remove "Medium-impact deletion") |
| High | Irreversible and significant, shared impact, financial or legal | A review of consequences and blockers before the confirmation; a confirmation listing what will be lost and who is affected; typing the resource name for the most severe cases; re-authentication if policy calls for it `[confirm: security]` (Carbon Remove "High-impact deletion"; WCAG 3.3.4) |

- **Blockers first.** Check preconditions (ownership, active billing, running jobs, legal holds `[confirm]`) before the confirmation step; explain each blocker and how to resolve it. Never let someone complete a confirmation only to be refused afterwards.
- **Offer less destructive alternatives** that meet the same goal (archive, leave, transfer ownership, export first) only where the product supports them `[confirm: product]`.
- **Confirmation content**: title = action + object; body = concrete consequences; "This can't be undone" only when that is established; buttons = the specific action ("Delete workspace") and "Cancel", never "OK" or "Yes". Color must not carry the warning alone. (Apple Alerts; GOV.UK Button, on warning buttons; Carbon Remove)
- **Typed confirmation**: the destructive button stays unavailable until the typed name matches. This is the one place a disabled button is right; expose it with `aria-disabled` and state the requirement next to it.
- **Focus**: on the web, initial focus goes to the least destructive control, or to the confirmation field in a typed-confirmation dialog (accessibility file §3). (APG Dialog (Modal)) On Apple platforms, Cancel is never the default button, and leaving out a default makes people read. (Apple Alerts)
- **Separate destructive controls from frequent ones** and don't give dangerous commands quick shortcuts. (AF CH11 "Hide the ejector seat levers"; AF CH16 "Memorization vectors")
- **Execution**: if deletion isn't immediate, show a "deletion requested" or "in progress" state and tell the user when it completes or fails. Failure part-way follows §8. (Carbon Remove "Optional passive modal", "Notification")
- **Afterwards**: define where the user lands, and what affected people see at their next action, including someone who is inside the resource at the moment it disappears (§10, §11).
- **Never invent** retention periods, backups, restore windows or legal consequences. Mark them `[confirm: product]` or `[confirm: legal]`, and design both branches when they change the behavior.

## 8 Partial failure and batches

- **Report per item and in aggregate** ("17 of 20 uploaded, 3 failed"). Keep the successes. Keep failed items in place with their specific reason and an individual Retry; offer "Retry failed" when there are many; let users remove items they no longer want.
- **All-or-nothing vs best-effort** is a product and engineering decision `[confirm]`. Design the one that is true, or both.
- **Announce the aggregate result once** when the batch settles, with sparse milestones only for long batches, never every item. (WCAG 4.1.3; accessibility file §5)
- **Large batches**: let users filter to failed items, and keep failures visible if they leave and return `[confirm]`.
- **Interrupted transfers**: resuming an upload or download where it stopped exists only if engineering confirms it `[confirm: engineering]`; otherwise Retry restarts that item, and the interface says so.
- **Never present partial success as success.**

## 9 Offline and unreliable networks

- **Show connectivity problems passively and in context**, with cached content where available, rather than blocking alerts. (Apple Alerts: show cached or placeholder data with a nonintrusive label; avoid alerts at launch)
- **Decide per action**: block with an explanation, queue for later, or keep a local draft. Queuing and local drafts exist only if engineering builds them `[confirm: engineering]`; never imply offline support that doesn't exist.
- **Never discard what the user entered** because a request failed. (GOV.UK Error message; AF CH8 "Considerate products fail gracefully")
- **On reconnection**, say what synced and what didn't, and handle conflicts (§10).

## 10 Stale data and conflicts

Detection (versions, timestamps), real-time sync and merging belong to engineering and exist only if confirmed `[confirm: engineering]`; design the moments:

- **Before saving**: if the item changed since it was opened, say so before overwriting.
- **At conflict**: show what changed and offer only supported options (review and merge, keep theirs, keep mine). Never silently overwrite someone else's work; on collisions, keeping both versions is the considerate default. (AF CH8 "Considerate products are conscientious")
- **Lists**: offer "3 new updates, show them" instead of reordering content under the user's pointer.
- **Target gone** (deleted or moved by someone else): explain, keep the user's unsent input, and offer a sensible next step.
- Locking vs last-write-wins vs merging is a product decision within engineering constraints `[confirm]`.

## 11 Sessions, permissions, interruptions

- **Time limits**: let users turn off, adjust or extend them; when extending, warn before expiry and allow at least 20 seconds to extend with a simple action, unless an exception applies (real-time events, essential limits, over 20 hours). `[required: WCAG 2.2.1]`
- **After re-authentication**, continue without data loss and return to the same place. (WCAG 2.2.5, AAA: target it where feasible)
- **Permission lost mid-task** (role changed, resource unshared): explain what changed, keep the user's input, and offer the available path (request access, contact the owner) `[confirm: product]`.
- **Unsaved changes**: track a dirty state; guard an exit only when leaving would really lose work; prefer autosave or drafts `[confirm: engineering]`. When closing a modal that contains user content, explain and offer save, discard or keep editing. (Apple Modality; DOET Ch 4 "Lock-ins"; AF CH14 "Automatic save")
- **Interruptions**: keep the goal, the user's place and the system state visible so they can resume. (DOET Ch 5 "Understanding Why There Is Error")

## 12 Choosing edge cases

Include a case only if it is plausible for this interaction and failing it would lose data, money, trust or access, or block the task. If the user might expect others, list them as not covered.

| Category | Ask about |
|---|---|
| Input | Empty, invalid, too long or too large, wrong type, duplicate, pasted or autofilled |
| Timing | Slow, timeout, double activation, user leaves part-way, responses arriving out of order |
| Network | Offline, flaky, reconnecting |
| Data | Empty, very large, stale, changed by someone else, deleted elsewhere |
| People | Others affected, concurrent editors, who gets notified |
| Access | Missing permission, permission changes mid-task, session expiry, re-authentication |
| Consequence | Irreversible, shared, financial, legal |
| Recovery | Which undo, cancel and retry paths really exist |

## 13 Interaction copy

- **Labels**: a verb that names the outcome ("Delete workspace", "Send invite"), in the design system's casing; the final step uses the specific verb, not "Submit" or "OK". (GOV.UK Button; Apple Alerts; DI Ch 8 "Prominent 'Done' Button or Assumed Next Step")
- **Confirmations**: a question naming the action and the object; a body stating consequences; buttons that repeat the action verb, plus "Cancel". (Apple Alerts)
- **Errors**: what happened and how to fix it, specific to the field and the cause, in plain language, without blame, bare codes or words like "invalid". (GOV.UK Error message; NN/g heuristic 9; DOET Ch 2 "Positive Psychology"; AF CH21 "Improving error messages: the last resort")
- **Status and success**: what changed and what happens next, worded the same way everywhere. (GOV.UK Notification banner, Confirmation pages)
- **Empty states**: what will appear here, why it is empty, and the one most useful next action; no dead ends. (Carbon Empty states)
- **Cut words** until meaning would suffer; instructions that must be read are a sign the design needs fixing. (DMMT Ch 5 "Omit needless words")
- **Own system failures**: acknowledge an inconvenience the product caused, but never apologize in place of the fix. (DMMT Ch 11 "When in doubt, apologize"; GOV.UK avoids "sorry" in input errors; follow the product's voice)
