# Critique-skill architecture in established ecosystems

**Date:** 2026-07-31
**Scope:** Current primary documentation and upstream source for gstack, obra/superpowers,
OpenAI Codex skills/plugins, Anthropic Claude Code, and the Agent Skills specification.

## Bottom line

The dominant public shape is **not a deep skill tree**. Established systems use one of two
shapes:

1. flat, job-specific review skills connected by an explicit workflow; or
2. one public review entry point whose specialist prompts, rubrics, or agents are internal
   implementation resources.

When an ecosystem composes several complete public reviews, it normally exposes that composition
as a separate, opt-in meta-skill. gstack's `/autoplan` is the clearest example—and also the
closest precedent for the bloat and nesting concern.

## Observations from primary sources

| Ecosystem | Public review surface | Internal composition | Effective topology |
|---|---|---|---|
| **gstack** | Separate peers for CEO-plan, engineering-plan, design-plan, DX-plan, code, and live visual review | Review skills conditionally load internal sections or specialist checklists; `/autoplan` explicitly reads several complete peer skills | Flat specialist catalog plus one explicit meta-skill |
| **obra/superpowers** | Separate lifecycle jobs: request review, receive/evaluate feedback, and run review gates during development | Adjacent reviewer templates and fresh subagents | Flat workflow graph with one-hop resources |
| **Anthropic Claude Code** | One public `/code-review` command in the official plugin | Parallel specialist agents followed by issue-validation agents and a confidence filter | One façade over an internal ensemble |
| **OpenAI Codex** | Guidance says each skill should do one job; the official CodeRabbit plugin exposes one `code-review` skill | On-demand files/scripts or an external reviewer, with a structured result contract | One focused skill with progressive disclosure |

### gstack: public specialists, with an explicit heavy orchestrator

gstack makes review jurisdiction visible to the user. Its catalog distinguishes
`/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review`, `/plan-devex-review`, `/review`,
and `/design-review` by artifact, lifecycle stage, and reviewer job
([skill catalog](https://github.com/garrytan/gstack/blob/main/docs/skills.md)).
The reviews exchange durable state through a shared review-readiness dashboard and downstream
artifacts rather than appearing as children of one generic review command.

`/autoplan` is a separate public meta-skill for users who deliberately want the full gauntlet.
It reads the complete CEO, design, engineering, and DX skill files and follows them at full depth
([autoplan source](https://github.com/garrytan/gstack/blob/main/autoplan/SKILL.md)).
That makes it a two-level composition graph, not an indefinitely nested tree, but it is also the
strongest warning against making ordinary critique work this way.

Within an individual review, gstack also uses a shallower pattern. `/review` selects internal
specialist checklists by diff signals; those checklists are ordinary support files, not
discoverable skills
([review workflow](https://github.com/garrytan/gstack/blob/main/review/SKILL.md),
[security specialist](https://github.com/garrytan/gstack/blob/main/review/specialists/security.md)).
Likewise, plan-design review loads an internal review section rather than exposing each pass as a
separate command
([plan-design review](https://github.com/garrytan/gstack/blob/main/plan-design-review/SKILL.md),
[review sections](https://github.com/garrytan/gstack/blob/main/plan-design-review/sections/review-sections.md)).

### obra/superpowers: split by lifecycle responsibility

Superpowers separates initiating review from evaluating received feedback:
`requesting-code-review` packages precise context and dispatches a reviewer, while
`receiving-code-review` verifies feedback before action
([requesting review](https://github.com/obra/superpowers/blob/main/skills/requesting-code-review/SKILL.md),
[receiving review](https://github.com/obra/superpowers/blob/main/skills/receiving-code-review/SKILL.md)).
The reviewer rubric is an adjacent prompt template, not a child skill
([reviewer template](https://github.com/obra/superpowers/blob/main/skills/requesting-code-review/code-reviewer.md)).

The larger subagent-driven-development workflow schedules task reviews, scoped re-reviews, and a
final whole-branch review, but those reviewer prompts remain files inside that workflow rather
than additional public skill nodes
([SDD process](https://github.com/obra/superpowers/blob/main/skills/subagent-driven-development/SKILL.md),
[task-reviewer template](https://github.com/obra/superpowers/blob/main/skills/subagent-driven-development/task-reviewer-prompt.md),
[re-review template](https://github.com/obra/superpowers/blob/main/skills/subagent-driven-development/re-review-prompt.md)).
Its authoring guidance explicitly keeps skills in one searchable namespace and treats references
as supporting material
([writing-skills guidance](https://github.com/obra/superpowers/blob/main/skills/writing-skills/SKILL.md)).

### Anthropic: one public command over an internal review panel

Anthropic's official code-review plugin exposes one `/code-review` command. Internally it launches
multiple independent reviewers, then separate validators for proposed findings, filters
unvalidated findings, and emits one result
([plugin overview](https://github.com/anthropics/claude-code/tree/main/plugins/code-review),
[command source](https://github.com/anthropics/claude-code/blob/main/plugins/code-review/commands/code-review.md)).
The specialist agents are execution details; users do not navigate a reviewer hierarchy.

Claude Code's authoring documentation reinforces that separation: keep `SKILL.md` focused, move
detailed material into supporting files loaded only when needed, and use a forked subagent when
isolated execution is useful
([skills documentation](https://code.claude.com/docs/en/slash-commands)).
Plugins expose skills and agents as sibling component types rather than requiring skills to form
a parent-child hierarchy
([plugin reference](https://code.claude.com/docs/en/plugins-reference)).

### OpenAI and the shared Agent Skills model: progressive disclosure, not recursive skills

OpenAI's current Codex guidance says skills begin as name-and-description metadata, load their
full instructions only when selected, may then load references or scripts as needed, and should
stay focused on one job
([Build skills](https://developers.openai.com/codex/skills)).
Plugins bundle one or more skills as peer entries
([plugin structure](https://developers.openai.com/plugins/build/plugins)).

The official OpenAI plugin catalog's CodeRabbit integration is a concrete review example: one
`code-review` skill invokes the reviewer, normalizes findings into a report, and does not execute
review-suggested commands unless the user asks
([CodeRabbit skill](https://github.com/openai/plugins/blob/main/plugins/coderabbit/skills/coderabbit-review/SKILL.md)).

The cross-vendor Agent Skills specification is more explicit: load metadata, then one
`SKILL.md`, then resources on demand; keep references focused; and keep file references one level
deep rather than forming deeply nested reference chains
([Agent Skills specification](https://agentskills.io/specification)).

## Recommendations for Astra

These are design recommendations derived from the observations above, not facts about the
upstream systems.

### Use a shallow façade, not critique subskills

Keep all user-facing Astra skills as peers:

```text
astra-critique
astra-product-design
astra-interface
astra-brand
astra-presentation
```

Inside `astra-critique`, use directly selected **review lenses** or **rubrics**, not registered
skills or nested "packs":

```text
user
  -> astra-critique core
       -> selected direct lens file(s)
       -> one attributable report
       -> one typed problem handoff
  -> user chooses whether to continue
  -> a peer Astra skill
```

The important boundary is semantic, not just directory layout:

- a lens is not invocable, cannot invoke another lens, and cannot hand off independently;
- the Critique core owns intake, lens selection, evidence rules, conflict handling, report shape,
  and the common handoff envelope;
- the core loads only the strongest applicable lens by default and adds others only when the
  agenda genuinely crosses jurisdictions;
- each lens is a direct, self-contained reference from the core—no lens-to-lens references;
- Critique never reads or executes the destination skill's full workflow.

### Keep destination-specific handoffs small

A typed handoff need not embed every downstream skill. Use a stable common envelope—artifact,
problem statement, finding IDs and evidence, observed impact, affected scope, user constraints,
open decisions, and context gaps—plus a small destination profile for the selected peer.
Destination profiles are support data, not skills. The handoff contains no proposed remedy,
implementation sequence, tool choice, or Critique-authored success criteria. Critique emits the
problem and stops; the peer skill owns solution exploration and the user decides whether to start
it.

This makes the relation a **handoff edge between peer skills**, not a parent calling a child.

### Treat gstack `/autoplan` as the exception

Do not make normal `astra-critique` operation read and execute complete downstream Astra skills.
If a future user need emerges for "run every review and then carry out the whole chain," that
would justify a separately named, explicitly invoked orchestration skill. It should not be hidden
inside Critique.

### Naming matters

Calling the internal units "skills" or "review packs" makes a nested product surface sound
intentional. Calling them **lenses**, **rubrics**, or **review protocols**, while keeping them
undiscoverable and one level deep, accurately describes the architecture.

## Answer to the concern

Yes: the earlier "Critique core → review packs → destination adapters → destination skills"
wording can read like a deep tree. The stronger precedent is:

> one public Critique skill, one level of on-demand internal rubrics, one report, then a
> user-mediated handoff to a peer skill.

That preserves a single user job without loading every discipline or exposing a hierarchy.
