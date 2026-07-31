# Astra phase-0 skill design roadmap

**Snapshot:** 2026-07-31
**Status:** Proposed design-document sequence; runtime implementation remains deferred

> **Authority.** `docs/phase-0.md` governs phase scope and ledger ownership.
> `docs/design-requirements.md` governs every per-skill design. This roadmap schedules and
> proposes source allocation; it does not replace either document or make the source-claim
> ledger authoritative by itself.

## 1. Purpose and certainty

This roadmap answers four questions:

1. Which Astra skill design documents remain to be drafted?
2. Which candidate neighborhood is expected to produce each Astra skill?
3. Which original sources would that skill encapsulate if its design validates the proposal?
4. Which other designs must be reconciled before ownership and triggers are final?

The collision map is still evidence, not a predetermined roster. The roadmap therefore uses four
states:

| State | Meaning |
|---|---|
| **Complete** | A reviewed phase-0 design exists. |
| **Confirmed name** | The user approved the skill split and name; source allocation still requires the individual design's inspection. |
| **Provisional** | This roadmap proposes a skill and source allocation so work can be sequenced; the individual design may merge, split, rename, retain, or exclude sources with evidence. |
| **No new Astra skill proposed** | The neighborhood does not currently justify another merged skill; sources are redirected to another design or retained independently. |

In this document, **encapsulates** means *proposed primary source home after successful design,
validation, and later retirement gates*. It does not mean the source is already absorbed or safe
to delete. `docs/phase-0-ledgers.md` remains authoritative until the coordinator reconciles a
completed design.

Sources marked **†** are harness built-ins whose bytes and immutable provenance are unavailable.
They may inform a proposed route, but no design may claim them absorbed until the host-version
provenance rule is resolved.

## 2. Current result

| Measure | Current proposal |
|---|---:|
| Completed design documents | 1 |
| Remaining confirmed-name documents | 4 |
| Remaining provisional documents | 22 |
| Planned revision of an existing design | 1 |
| Neighborhoods producing no Astra document or revision | 1 |
| Proposed Astra roster after all remaining documents | 27 |

The completed design is
[`designs/astra-critique.md`](../designs/astra-critique.md). The 26 remaining documents are
listed below. The proposed final count is not a target: it must shrink, grow, or retain independent
sources if source inspection and trigger comparison require that.

## 3. Dependency semantics

Phase 0 permits designs to be drafted in parallel; peer designs do not need to exist first.
Dependencies in this roadmap are therefore reconciliation edges, not blanket drafting blocks:

| Code | Meaning |
|---|---|
| **R** | **Roster reconciliation:** ownership, trigger, or handoff boundaries must agree before either design is accepted into the final roster. |
| **I** | **Later implementation dependency:** the future runtime skill is expected to consume or hand off to this peer, but its phase-0 design can still be drafted independently. |
| **P** | **Provenance dependency:** unavailable source bytes, host behavior, or an external component must be resolved before absorption or retirement can be claimed. |

All proposed Astra skills are flat peers. Waves express design order, and dependency arrows express
reconciliation or later consumption; neither creates a nested public skill tree or requires
Critique to invoke a chain of child skills.

Every proposed peer that accepts Critique findings also has an **R** edge back to
`astra-critique`: it contributes a compact problem-only handoff profile during the final roster
reconciliation. That common edge is omitted from most table cells below.

Those destination profiles are support data, not a skill registry. Each destination design owns
the job it accepts and contributes only its compact profile during roster reconciliation. At
runtime, Critique selects a destination and reads that one profile directly; it never reads the
destination's full `SKILL.md`. Critique's primary output remains the critique report. Its handoff
describes the observed problem, affected context, evidence, uncertainty, and research gaps—not a
solution. The selected downstream skill owns solution design and execution.

```mermaid
flowchart TD
    critique["astra-critique<br/>complete"]

    product["astra-product-design"]
    brand["astra-brand"]
    interface["astra-interface"]
    presentation["astra-presentation"]

    guard["astra-guard"]
    context["astra-context"]
    understand["astra-understand-code"]
    test["astra-test"]
    delegate["astra-delegate"]
    setup["astra-setup"]

    spec["astra-spec"]
    architecture["astra-architecture"]
    plan["astra-plan"]
    implement["astra-implement"]
    debug["astra-debug"]
    incident["astra-incident"]

    browser["astra-browser"]
    qa["astra-qa"]
    ship["astra-ship"]
    deploy["astra-deploy"]

    research["astra-research"]
    knowledge["astra-knowledge"]
    document["astra-document"]
    skilldesign["astra-skill-design"]
    automate["astra-automate"]
    ios["astra-ios"]

    product --> interface
    brand --> interface
    brand --> presentation
    critique --> interface

    understand --> architecture
    understand --> debug
    spec --> plan
    architecture --> plan
    context --> delegate
    guard --> delegate
    plan --> implement
    delegate --> implement
    test --> implement

    debug --> incident
    context --> incident
    document --> incident

    setup --> browser
    browser --> qa
    test --> qa
    interface --> qa

    implement --> ship
    test --> ship
    critique --> ship
    guard --> ship
    ship --> deploy
    setup --> deploy
    qa --> deploy

    research --> document
    knowledge --> document
    brand --> document
    presentation --> document

    browser --> skilldesign
    test --> skilldesign
    delegate --> automate
    context --> automate
    guard --> automate
    setup --> automate

    interface --> ios
    qa --> ios
    debug --> ios
    test --> ios
    setup --> ios
```

Arrows point from an upstream peer to a likely downstream consumer or reconciler. They show only
the strongest expected relationships. Section 5 records additional reconciliation edges that
would make the graph unreadable if every one were drawn.

## 4. Recommended design waves

### Wave 0 — completed baseline

| Design | Status | Result |
|---|---|---|
| [`astra-critique`](../designs/astra-critique.md) | **Complete** | Owns adversarial critique and the audit/report portion of `design-review`; remains open to source-expansion revisions from later neighborhoods. |

### Wave 1 — current Design tranche

The user selected this tranche next. Draft `astra-product-design` and `astra-brand` first; their
journey and identity boundaries make the `astra-interface` and `astra-presentation` ownership
decisions easier to state.

| Proposed design file | Status | Reconcile with |
|---|---|---|
| `designs/astra-product-design.md` | **Confirmed name** | **R:** `astra-interface`, `astra-brand`, `astra-presentation`; **I:** `astra-critique` handoffs |
| `designs/astra-brand.md` | **Confirmed name** | **R:** `astra-interface`, `astra-presentation`, `astra-document`; **I:** Design-token and asset consumers |
| `designs/astra-interface.md` | **Confirmed name** | **R:** Product/Brand, `astra-critique`, `astra-test`, `astra-qa`; **P:** `artifact-design` and `artifact-capabilities` built-ins |
| `designs/astra-presentation.md` | **Confirmed name** | **R:** `astra-brand`, `astra-document`, Product; **P:** `dataviz` built-in |

### Wave 2 — cross-cutting foundations

| Proposed design file | Status | Reconcile with |
|---|---|---|
| `designs/astra-guard.md` | **Provisional** | **R/I:** every mutation-capable skill; destructive-action boundaries remain local to each consumer |
| `designs/astra-context.md` | **Provisional** | **R/I:** `astra-delegate`, `astra-automate`, `astra-plan`, `astra-incident` |
| `designs/astra-understand-code.md` | **Provisional** | **R:** `astra-architecture`, Critique code lenses, `astra-debug` |
| `designs/astra-test.md` | **Provisional** | **R:** `astra-implement`, `astra-qa`, `astra-ship`, `astra-interface`, Critique verification; **P:** `run` built-in |
| `designs/astra-delegate.md` | **Provisional** | **R:** Context, Guard, `astra-implement`, `astra-automate`; preserve agent delivery shape |
| `designs/astra-setup.md` | **Provisional** | **R:** Browser, Deploy, Automation, iOS, Skill Design; **P:** three setup/config built-ins |

### Wave 3 — core project-development loop

| Proposed design file or revision | Status | Reconcile with |
|---|---|---|
| `designs/astra-spec.md` | **Provisional** | **R:** Critique, `astra-knowledge`, `astra-architecture`, Product Design |
| `designs/astra-architecture.md` | **Provisional** | **R:** `astra-understand-code`, Spec, Plan, Critique, `domain-modeling` |
| `designs/astra-plan.md` | **Provisional** | **R:** Spec, Architecture, Critique, Context, Implement |
| `designs/astra-implement.md` | **Provisional** | **R:** Plan, Delegate, Test, Guard, Critique; receives code-simplification sources from Code review |
| `designs/astra-critique.md` source-expansion revision | **Existing design revision** | **R:** Code review, Understand Code, Test, Architecture; must not create a competing nested code-critique skill |
| `designs/astra-debug.md` | **Provisional** | **R:** Understand Code, Test, Browser/QA, Incident |
| `designs/astra-incident.md` | **Provisional** | **R:** Debug, Context, Document, Guard; keep stabilization distinct from causal diagnosis |

### Wave 4 — browser, quality, and delivery

| Proposed design file | Status | Reconcile with |
|---|---|---|
| `designs/astra-browser.md` | **Provisional** | **R:** Setup, Guard, QA, Skill Design; preserve MCP, browser-daemon, cloud-browser, Electron, and authenticated-session delivery shapes |
| `designs/astra-qa.md` | **Provisional** | **R:** Browser, Test, Interface, Critique; distinguish report-only from fix authority |
| `designs/astra-ship.md` | **Provisional** | **R:** Implement, Test, Critique, Guard, Context, Document; preserve explicit user control over commits, pushes, PRs, and merges |
| `designs/astra-deploy.md` | **Provisional** | **R:** Ship, Setup, Browser/QA, Guard; preserve provider-specific prerequisites and canary degradation |

### Wave 5 — knowledge, meta-work, and autonomy

| Proposed design file | Status | Reconcile with |
|---|---|---|
| `designs/astra-research.md` | **Provisional** | **R:** Browser, Document, Knowledge, Critique evidence requirements |
| `designs/astra-knowledge.md` | **Provisional** | **R:** Spec, Architecture, Document, Context; preserve `domain-modeling` as a cross-role |
| `designs/astra-document.md` | **Provisional** | **R:** Research, Knowledge, Brand, Presentation, Ship, Incident |
| `designs/astra-skill-design.md` | **Provisional** | **R:** Test, Research, Browser, Setup; preserve skill-scoped agents and benchmark delivery shapes |
| `designs/astra-automate.md` | **Provisional** | **R:** Delegate, Context, Guard, Setup, Plan, Ship; **P:** `loop` and `schedule` built-ins |

### Wave 6 — specialized platform decision

| Proposed design file | Status | Reconcile with |
|---|---|---|
| `designs/astra-ios.md` | **Provisional, later** | **R:** Interface, QA, Debug, Test, Setup, Critique; the design may instead retain the iOS pack if a self-contained merger adds no personal value |

The Ops & routine neighborhood currently produces no merged Astra design. Section 5.17 records
why `meeting` and `retro` should remain independent unless later evidence establishes one user job.

## 5. Neighborhood derivation and proposed source allocation

Every source below is an exact collision-map identifier. These are roadmap proposals, not applied
ledger dispositions.

### 5.1 Adversarial critique — complete

**Derived Astra skill:** `astra-critique`.

**Encapsulates:** `grilling`, `grill-me`, `grill-with-docs`, `/diss`, `/diss-api`,
`diss-infra`, `diss-claudemd`, `/elon`, `/trim`, `office-hours`, `plan-ceo-review`,
`plan-eng-review`, `plan-design-review`, `plan-devex-review`, `devex-review`, and `autoplan`.

**Remaining work:** no new design document. Later source-expansion revisions reconcile Code
review sources and any other critique jurisdiction; they do not narrow Critique to Design.

### 5.2 Code review

**Derived Astra skills:** no competing code-critique skill. Revise `astra-critique`, and route
mutation-oriented cleanup into `astra-implement`.

- **`astra-critique` expansion:** `code-review`, `review`, `requesting-code-review`,
  `receiving-code-review`, `superpowers:requesting-code-review`,
  `superpowers:receiving-code-review`, `feature-dev:code-reviewer`,
  `code-review:code-review`, and `security-review`†.
- **`astra-implement`:** `simplify`†, `code-simplifier`, and `health`.

The individual investigation must test whether requesting/receiving review remain lifecycle modes
inside Critique or retain independent entry points. In either case, they do not justify a child
skill tree.

### 5.3 Browser & QA

**Derived Astra skills:** `astra-browser` and `astra-qa`.

- **`astra-browser`:** `agent-browser`, `browse`, `connect-chrome`, `open-gstack-browser`,
  `agentcore`, `vercel-sandbox`, `electron`, `scrape`, `slack`, `setup-browser-cookies`, and
  `playwright` MCP.
- **`astra-qa`:** `webapp-testing`, `benchmark`, `dogfood`, `qa`, and `qa-only`.
- **Cross-neighborhood primary homes:** `skillify` → `astra-skill-design`; `pair-agent` →
  `astra-delegate`. Browser remains a secondary role for both.

`astra-browser` must expose capability and environment selection without making cloud browsers,
Electron, Slack, or authenticated cookies separate public child skills. `astra-qa` owns testing
policy, evidence, and report/fix authority, not browser setup.

### 5.4 Design & visual

**Derived Astra skills:** `astra-product-design`, `astra-interface`, `astra-brand`, and
`astra-presentation`.

- **`astra-product-design`:** `design-consultation` and `design-shotgun`.
- **`astra-interface`:** `design-system`, `design-html`, `ui-styling`, `ui-ux-pro-max`,
  `frontend-design`, `artifact-design`†, `artifact-capabilities`†, and
  `web-artifacts-builder`.
- **`astra-brand`:** `design`, `theme-factory`, `brand`, `brand-guidelines`, `banner-design`,
  `canvas-design`, and `algorithmic-art`.
- **`astra-presentation`:** `slides`, `dataviz`†, and `diagram`.
- **Existing primary home:** `design-review` audit/report → `astra-critique`; Interface owns its
  fix/verify secondary role and Test owns its bootstrap/regression secondary role.

Cross-role behaviors must remain visible: `design-system` also informs Brand and Presentation;
`theme-factory` also informs Interface and Presentation; `ui-ux-pro-max` also informs Product;
and `diagram` also informs Document.

### 5.5 Plan & spec

**Derived Astra skills:** `astra-spec`, `astra-plan`, and `astra-implement`.

- **`astra-spec`:** `superpowers:brainstorming`, `spec`, `to-spec`, and `sdd`.
- **`astra-plan`:** `superpowers:writing-plans`, `planb`, `plan-tune`, `wayfinder`, and
  `to-tickets`.
- **`astra-implement`:** `superpowers:executing-plans`,
  `superpowers:subagent-driven-development`, `implement`, and
  `feature-dev:feature-dev`.
- **Cross-neighborhood primary home:** `feature-dev:code-architect` → `astra-architecture`.
- **Independent candidate:** retain `prototype` unless the Product Design or Architecture
  investigation proves its throwaway-experiment job belongs inside that skill without flattening
  its trigger.

Spec decides what should be built, Plan turns an accepted specification into executable work, and
Implement changes the project. Their user approvals and mutation authority must remain separate.

### 5.6 Ship & VCS

**Derived Astra skills:** `astra-ship` and `astra-deploy`.

- **`astra-ship`:** `ship`, `landing-report`, `/pr`, `/commit`,
  `commit-commands:commit`, `commit-commands:commit-push-pr`,
  `commit-commands:clean_gone`, `changelog`, `document-release`,
  `resolving-merge-conflicts`, `superpowers:finishing-a-development-branch`,
  `superpowers:using-git-worktrees`, and `github`.
- **`astra-deploy`:** `land-and-deploy`, `canary`, `setup-deploy`, and
  `/build-push-ecr`.

Ship owns working-tree-to-reviewed-change publication. Deploy owns landing through production
verification. The designs must keep read-only status/report modes distinct from irreversible
commit, push, merge, deployment, and cleanup effects.

### 5.7 Docs & knowledge

**Derived Astra skills:** `astra-document`, `astra-research`, and `astra-knowledge`.

- **`astra-document`:** `document-generate`, `doc-coauthoring`, `/doc`, `make-pdf`,
  `internal-comms`, `rtfm`, `claude-md-management:revise-claude-md`, and
  `claude-md-management:claude-md-improver`.
- **`astra-research`:** `research`.
- **`astra-knowledge`:** `learn`, `teach`, `domain-modeling`, and `init`†.
- **Cross-neighborhood primary home:** `slack-gif-creator` → `astra-brand`.

Research establishes evidence; Knowledge maintains reusable understanding and domain language;
Document produces or revises an artifact for a reader. Rendering a PDF is a Document delivery
mode, not a separate knowledge job.

### 5.8 Debug & incident

**Derived Astra skills:** `astra-debug` and `astra-incident`.

- **`astra-debug`:** `investigate`, `diagnosing-bugs`,
  `superpowers:systematic-debugging`, `java-leak-resolver`, `staging-debug`, and
  `local-debug`.
- **`astra-incident`:** `rca`, `firefighting`, and `triage`.

Debug owns diagnosis and repair of a bounded failure. Incident owns stabilization, incident-state
navigation, parallel causal investigation, and operational handoff. `rca` and `firefighting`
retain distinct simultaneous roles rather than becoming one synthesized voice.

### 5.9 Codebase comprehension

**Derived Astra skills:** `astra-understand-code` and `astra-architecture`.

- **`astra-understand-code`:** `how`, `code-tracing`, and `feature-dev:code-explorer`.
- **`astra-architecture`:** `codebase-design`, `improve-codebase-architecture`, plus
  `feature-dev:code-architect` from Plan & spec.

Understand Code explains and traces what exists without selecting a new design. Architecture owns
module boundaries, technical-design choices, and implementation blueprints. Critique may review
either result but does not own the solution.

### 5.10 Skill meta

**Derived Astra skill:** `astra-skill-design`.

- **`astra-skill-design`:** `skill-creator`, `skill-creator:skill-creator`,
  `writing-great-skills`, `superpowers:writing-skills`, `skillify`, and
  `benchmark-models`.
- **Cross-neighborhood primary homes:** `prompt-lookup` → `astra-research`;
  `gstack-upgrade` → `astra-setup`.
- **Deferred routing components:** `ask-matt`, `gstack`, and `_gstack-command` do not produce
  another skill design. They remain migration inputs to the separately deferred Astra
  router/tuning decision.

Skill Design owns authoring, validation, forward tests, and skill-specific benchmarking. It must
preserve the installed `skill-creator` component's scoped agents rather than flattening them into
prompt prose.

### 5.11 Delegation & autonomy

**Derived Astra skills:** `astra-delegate` and `astra-automate`.

- **`astra-delegate`:** `coding-agent`, `codex`,
  `superpowers:dispatching-parallel-agents`, and `pair-agent`.
- **`astra-automate`:** `nightnight`, `loop`†, `loop-goal`, and `schedule`†.

Delegate owns a bounded user-authorized delegation. Automate owns recurring, unattended, or
goal-loop execution and therefore has stronger Context, Guard, cancellation, monitoring, and
external-state dependencies.

### 5.12 Testing

**Derived Astra skill:** `astra-test`.

**Encapsulates:** `tdd`, `superpowers:test-driven-development`, `bdd`, `spock`, `nextjs-test`,
`shell-scripting:bats-testing-patterns`, `superpowers:verification-before-completion`, and
`run`†.

Framework-specific material becomes directly selected internal references or retained independent
references if self-containment is not justified. TDD/BDD construction, framework jurisdiction,
test execution, and final verification remain distinguishable modes inside one testing job.

### 5.13 Context & handoff

**Derived Astra skill:** `astra-context`.

**Encapsulates:** `context-save`, `context-restore`, `strategic-compact`, `handoff`, and
`nowhat`.

The design must test whether `nowhat`'s meta-cognitive strategy switching belongs as a
reorientation mode or should remain independent. It may not be silently reduced to context
serialization.

### 5.14 Safety

**Derived Astra skill:** `astra-guard`.

**Encapsulates:** `careful`, `freeze`, `unfreeze`, and `guard`.

Guard combines destructive-action warnings with explicit edit boundaries. Freeze and unfreeze
must remain reversible user-controlled state transitions, not hidden automatic policy.

### 5.15 Setup & config

**Derived Astra skill:** `astra-setup`.

**Encapsulates:** `setup-aurora-pg-mcp`, `setup-gbrain`, `sync-gbrain`,
`setup-matt-pocock-skills`, `update-config`†, `keybindings-help`†,
`fewer-permission-prompts`†, and
`claude-code-setup:claude-automation-recommender`.

**Cross-neighborhood secondary source:** `gstack-upgrade` contributes migration and upgrade
behavior until gstack retirement is complete.

Setup owns configuring and maintaining the agent-development environment. Provider-specific
credentials, MCPs, project mutations, and read-only recommendations stay explicit modes with
separate authority.

### 5.16 iOS

**Derived Astra skill:** `astra-ios`.

**Encapsulates:** `ios-qa`, `ios-fix`, `ios-design-review`, `ios-sync`, and `ios-clean`.

The platform boundary justifies one investigation, not automatically one monolithic workflow.
The design must preserve live-device QA, visual review, autonomous repair, debug-bridge
maintenance, and cleanup as distinct modes or retain the original pack if their coordination
shows no advantage.

### 5.17 Ops & routine

**Derived Astra skill:** none currently recommended.

- `office-hours` is a duplicate occurrence whose primary home is `astra-critique`.
- `retro` is a weekly engineering retrospective.
- `meeting` schedules calendar events and drafts notifications through Google Calendar and Gmail.

`retro` and `meeting` do not share one user job, evidence method, authority, or dependencies.
Keep them independent unless later personal-value evidence justifies separate rename-only Astra
designs; do not create an `astra-routine` grab bag merely to empty the neighborhood.

## 6. Per-design completion contract

For each remaining document:

1. Reserve its exact occurrence claims in `docs/phase-0-ledgers.md`.
2. Inspect every proposed primary source body, registration, component type, invocation,
   immutable revision or hash, authority, dependency, and failure path.
3. Inspect cross-neighborhood evidence without taking another design's primary claim.
4. Write the ten required sections from `docs/design-requirements.md`.
5. State which roadmap allocation was confirmed, changed, split, retained, or excluded and why.
6. Define source-oracle, reference-convener, self-contained-candidate, and source-specific
   retirement gates without claiming they have run.
7. Record a problem-only `astra-critique` handoff profile if the peer accepts critique findings.
8. Self-review, validate Markdown, commit the document, and obtain user review.
9. Let the coordinator apply proposed ledger changes between waves.

A source list in this roadmap is not sufficient evidence for a design and cannot satisfy any
retirement gate.

## 7. Final reconciliation milestones

After all proposed documents and no-new-skill decisions have been reviewed:

1. Compare every trigger and non-trigger across the proposed roster.
2. Resolve every source occurrence to one primary disposition and zero or more explicit secondary
   roles.
3. Reconcile Critique handoff profiles for every accepting peer.
4. Decide whether provisional designs with one weak source should remain Astra skills or retain
   the independent original.
5. Resolve all † built-in provenance gaps.
6. Decide keep/defer/exclude for the reference and cleanup ledger; reference skills do not need
   Astra wrappers merely to appear in the roadmap.
7. Reconcile commands, agents, MCP servers, hooks, and LSP servers by component type.
8. Present the final roster, priorities, exclusions, unresolved questions, and manual bridges to
   the user.

Only after that roster is selected may implementation planning begin. Runtime skill creation,
router/tuning work, plugin packaging, behavioral harnesses, installation, and source retirement
remain outside phase 0.
