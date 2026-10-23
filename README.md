# Product Design Workflow

**A design partner for Claude that checks the brief, does the work step by step, and lets you make every call.**

A free, MIT-licensed Claude Code plugin by Della Mahmoudi, product designer. Nine skills plus one independent QA agent. No hooks, no MCP servers, no scripts, nothing to sign up for.

You ask for design work the way you normally would. A Supervisor skill picks it up, checks whether the brief is ready, loads only the design expertise that step needs, reviews the result against design-system and accessibility standards, and then pauses so you decide what happens next. When everything is accepted, a separate Final QA agent gives the finished deliverable a fresh, read-only review.

**Nothing moves forward until you say so.** The plugin advises. You decide.

## Why I built it

Design work slows down for the same few reasons again and again:

- tasks show up **without context**: no goal, no acceptance criteria, no constraints
- **data is missing**, so people guess and redo it later
- **too many rounds of edits**, because problems surface late
- **design-system rules get lost**, so components, tokens and states drift

This plugin builds those checks into the workflow. It asks one focused question only when a real product decision is blocking, applies the domain standards while working, and after each step tells you what it made, what it checked and what is still open.

## Install

**Option 1: paste this into Claude Code**

```text
https://github.com/dellamahmoudi93-max/product-design-workflow

Install this Claude Code plugin from its marketplace, then confirm the product-design-supervisor skill is available.
```

**Option 2: run the commands yourself in Claude Code**

```text
/plugin marketplace add dellamahmoudi93-max/product-design-workflow
/plugin install product-design-workflow@product-design-workflow
```

The first command adds the marketplace. The second installs the `product-design-workflow` plugin from the `product-design-workflow` marketplace (same name for both).

> Already have standalone copies of these skills? Remove them first, otherwise two copies can respond to the same request.

## Your first prompt

Copy this, swap in your own details, and paste it into Claude:

```text
I'm working on [product / feature]. Here's the brief: [paste brief, link or notes].

Before you start, check whether the brief is ready and tell me what's missing.
Then break the work into steps, do the first one, and stop so I can review it.
```

You don't need to name the plugin. The Supervisor is the default entry point for design requests, and it also understands Persian and Finglish.

## What you can ask for

| You say | What happens |
|---|---|
| "Design this settings screen" | Readiness check, then UI and interaction work, reviewed for states, accessibility and responsiveness |
| "Review this checkout flow" | Structural and interaction review with a clear list of misses and a recommendation |
| "Rewrite this button label" | A small request stays a single step, no ceremony |
| "The CEO wants a dashboard, where do we start?" | Discovery framing: users, facts vs. assumptions, risks, MVP scope, success metrics |
| "Is this ready for dev?" | Handoff completeness, acceptance criteria and Definition of Done |
| "Audit our buttons against the design system" | Reuse vs. create decisions, token and variant consistency |
| «این صفحه رو طراحی کن» | Same workflow, in Persian |

## What's inside

| Component | Type | Purpose |
|---|---|---|
| `product-design-supervisor` | Skill | Entry point. Frames scope, checks readiness, splits work into steps, selects domain skills, reviews each result, pauses for a human decision, then hands off to Final QA. |
| `product-discovery-framing` | Skill | Turns vague briefs and "the CEO wants X" into a real problem frame: users, facts vs. assumptions, risk, MVP scope, success metrics. |
| `ux-architecture` | Skill | IA, navigation, taxonomy, labels, sitemaps, structural user flows and journeys, findability. |
| `interaction-design` | Skill | Behavior: states, feedback, validation, errors and recovery, loading/async, focus and keyboard, interaction copy. |
| `ui-visual-design` | Skill | Visual layer: hierarchy, layout, spacing, typography, color and contrast, responsive, dark mode, RTL. |
| `design-systems-consistency` | Skill | Reuse vs. create decisions, component APIs and variants, token architecture, audits, governance, deprecation, Figma ↔ code parity. |
| `prototype-testing-analytics` | Skill | Prototype and usability-test planning, research findings, UX metrics, tracking plans, A/B experiments. |
| `delivery-product-collaboration` | Skill | Ready-for-Dev, handoff completeness, acceptance criteria, Definition of Done, implementation QA. |
| `refresh-capability-index` | Skill | Maintenance only. Runs only when you ask to benchmark or update the Supervisor's capability index. Ships the method and a findings summary; raw pilot data and evaluation kits are not included. |
| `independent-final-qa` | Agent | Fresh, read-only review of the finished deliverable against scope and standards. Returns PASS / FAIL / BLOCKED. |

Each domain skill comes with `references/` (standards, with a `source-map.md` pointing to public sources such as WCAG 2.2, WAI-ARIA APG, NN/g, GOV.UK, Material and Carbon) and `evals/` (test cases).

## How it works

```mermaid
flowchart TD
    A["Designer request"] --> B["Supervisor: frame goal, output, constraints, acceptance criteria"]
    B --> C{"Blocking human decision missing?"}
    C -- "yes" --> D["Ask ONE question + recommendation"]
    D --> B
    C -- "no" --> E{"Simple task?"}
    E -- "yes" --> F["Single step"]
    E -- "no" --> G["Split at real dependency / decision boundaries"]
    G --> F
    F --> H["Load only the needed domain skill(s)"]
    H --> I["Choose route: sources, executor, output, verification"]
    I --> J["Do the step"]
    J --> K["Review: standards, states, a11y, responsive, design-system consistency"]
    K --> L["Report: produced / checked / misses / recommendation"]
    L --> M{"Human decides"}
    M -- "revise / retry / redirect" --> F
    M -- "next step" --> G
    M -- "stop" --> Z["End"]
    M -- "all accepted" --> N["final_ready"]
    N --> O["independent-final-qa agent: fresh, scope-only"]
    O --> P["Report shown unchanged, then Human accepts or revises"]
```

A few ground rules it follows:

- It never invents facts or quietly makes product decisions for you.
- It never retries, repairs or escalates on its own.
- A technical "pass" is advice, not approval. You approve.

## Which model to use

This is guidance based on what each part asks the model to do, not a benchmark. Use whatever your plan offers; quality comes first.

| Component | Main task | Suggested tier |
|---|---|---|
| `product-design-supervisor` | Multi-step judgment: readiness triage, scope control, routing, reviewing other output | **Strong** (your best default model) |
| `independent-final-qa` | Independent check against every criterion, honest FAIL/BLOCKED | **Strong** |
| `product-discovery-framing` | Ambiguous briefs, separating evidence from assumption, risk trade-offs | **Strong** |
| `design-systems-consistency` | Semantic token/component reasoning, migration, governance impact | **Strong** for architecture and migration; **mid/fast** for simple raw-value audits |
| `delivery-product-collaboration` | Handoff and acceptance-criteria checklists; parity QA | **Mid** for checklists and AC; **strong** for complex implementation-QA judgment |
| `ux-architecture` | IA and flow structuring | **Mid**, **strong** for large or permission-heavy IA |
| `interaction-design` | State modeling and edge cases; microcopy | **Mid** for copy and simple states; **strong** for complex async, permission or AI behavior |
| `prototype-testing-analytics` | Study plans, metric definitions, experiment design | **Mid** for plans and tracking specs; **strong** for causal or statistical interpretation |
| `ui-visual-design` | Applying an existing design system to a screen; visual critique | **Mid/fast** for routine specs and critique; **strong** for new hierarchy problems |
| `refresh-capability-index` | Benchmark method and evidence handling | **Strong** (rarely run) |

"Fast" means the cheaper or faster tier in your plan (for example, Haiku-class models). "Mid" means Sonnet-class models and "strong" means your top tier. The agent uses `model: inherit`, so it runs on the session model.

## Optional connectors

Figma, Google Drive and browser tools help with grounding and QA. The QA agent has no fixed tool list: it inherits your session's tools (any connected browser or Figma MCP), with file-writing tools and Bash disabled, and it is told never to submit, save, publish, share, pay or delete. Browser tools can still click and type, so point QA at a safe preview. Without suitable tools, QA marks the affected criteria BLOCKED instead of guessing.

## Known limits

- Skills activate by description matching, not a guaranteed hook.
- Figma reads and writes, document creation, media generation and interactive browser QA have not been quality-tested yet.

## Release notes

Current version: 0.2.5. See [docs/RELEASE-NOTES.md](docs/RELEASE-NOTES.md).

## License and author

MIT, see [LICENSE](LICENSE). Made by [Della Mahmoudi](https://github.com/dellamahmoudi93-max), product designer. If it helps your team, a star or a share means a lot.
