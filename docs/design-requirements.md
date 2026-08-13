# Astra skill design requirements

**Date:** 2026-07-31
**Status:** Approved structure; six-skill coding-lifecycle authority policy added

## 1. Purpose

This document tells agents how to produce one evidence-grounded design document for each
proposed Astra skill.

It governs design work only. A compliant output explains:

- why the skill should exist;
- which existing artifacts inform it;
- what behavior and distinctions must survive condensation;
- what advantage unification is expected to add beyond selecting the strongest applicable
  source directly;
- what interface the future skill should present;
- which high-level architecture best fits that particular skill; and
- how a later phase can distinguish routing value, coordination value, internalization
  fidelity, and retirement safety.

It does not create the skill. Exact prompts, `SKILL.md` frontmatter, tool declarations,
packaging, tests, tuning, behavioral-preservation claims, and source retirement belong to
later phases.

## 2. Authority and document roles

Apply authority in this order:

1. The user's current instructions.
2. `docs/phase-0.md` for phase scope, global source coverage, coordination, and acceptance.
3. This document for how each Astra skill design is researched, written, and reviewed.
4. A per-skill design for the proposed behavior of that skill.
5. `README.md` as source inventory, usage evidence, and candidate collision neighborhoods.
6. Restored or superseded documents as research evidence only.

When requirements touch the same deliverable, ownership resolves the conflict:
`docs/phase-0.md` decides what phase 0 must cover and when the phase is complete; this
document decides what every per-skill design must contain and how an agent produces it. A
per-skill design may specialize its proposed behavior but may not override either contract.

Per-skill designs live at:

```text
designs/<provisional-astra-name>.md
```

The directory contents form the emerging roster. Names and count remain provisional until
all candidate neighborhoods have been investigated and their triggers compared.

## 3. Governing rule

> Propose one Astra skill only when the user wants one coherent job served through one
> distinguishable interface, without discarding useful behavior, authority, prerequisites,
> or component types from its sources.

One public superskill does not imply one flattened prompt. A deep module may expose one
invocation while preserving source-specific perspectives, playbooks, jurisdictions, authority,
and failure behavior behind internal seams. Condensation removes duplicate interface and
machinery; it does not erase useful specialist behavior merely to make the implementation look
singular.

Every merger proposal must declare its expected positive advantage. If it claims better
judgment, it must name at least one task class on which combining sources should outperform the
best applicable single source. If its advantage is routing or maintenance only, say so
explicitly; those benefits do not establish better output and never excuse behavioral
regression.

The collision map is evidence to investigate, not a list of predetermined skills. A row may:

- become one Astra skill;
- split into several Astra skills;
- merge with part of another row;
- retain some sources as independent references or dependencies; or
- exclude sources with an evidence-backed reason, including that they are not useful to this
  user.

Personal value is not implied by appearing in the inventory. Ground it in an explicit user
instruction, a named project-development need, or a clearly labeled provisional inference.
Usage can inform priority, but it does not decide usefulness.

Under unresolved uncertainty, preserve the distinction and record the open question. A design
may be provisional; an unsupported merger may not be presented as settled.

## 4. Required evidence

### 4.1 Inspect the artifact, not only its label

For every source occurrence, record:

| Evidence | Requirement |
|---|---|
| Identifier | Exact skill, command, agent, tool, prompt, hook, or server name |
| Component type | Skill, command, agent, MCP server/tool/prompt, hook, LSP server, or other |
| Location | Live path, plugin registration, repository reference, or recoverable snapshot |
| Invocation | Exact current slash command, skill name, agent type, or tool action |
| Availability | Live, disabled, missing, dangling, or recovered from history |
| Declaration | Complete frontmatter or manifest fields, including unfamiliar fields |
| Behavior evidence | Relevant instructions, workflow, decision rules, prerequisites, and outputs |
| Provenance | Inspection date plus an immutable revision or content hash for every inspected source |

Read the manifest or registration before assuming a directory represents the complete
component. When descriptions collide, inspect the relevant instruction bodies. Descriptions
alone are insufficient evidence for merging behavior.

### 4.2 Label certainty

Every material statement about a source must be one of:

- **Observed:** directly supported by an inspected artifact.
- **Inferred:** a reasoned interpretation that still needs confirmation.
- **Unavailable:** the source could not be inspected.

An unavailable source cannot be claimed as absorbed or preserved. Recover it from a trustworthy
repository or snapshot, defer it, or exclude it with the limitation stated.

Every inspected source must have reproducible provenance. Hash the bytes used for the analysis
or record an immutable repository revision. If stable bytes cannot be obtained, label the
source unavailable rather than presenting the inspection as reproducible. A later hash
mismatch invalidates the recorded line anchors until the source is re-inspected and those
anchors are regenerated.

### 4.3 Preserve delivery shape

Do not flatten unlike component types into prompt text.

- A command may inform a future user-invoked skill interface.
- An agent remains a separate execution context.
- An MCP server or tool remains an external capability and prerequisite.
- A hook remains lifecycle behavior.
- An LSP server remains language infrastructure.

The design may retain, coordinate, replace, or exclude those mechanisms, but it must name the
choice explicitly.

Usage counts affect prioritization only. They do not establish equivalence, usefulness, or
permission to retire a source.

## 5. Condensation vocabulary

Use the following terms to explain what each source contributes. These are analytical labels,
not mandatory runtime modules.

| Contribution | Meaning |
|---|---|
| **Machinery** | Invocation glue, common setup, formatting, dispatch, or other behavior without an independent judgment policy |
| **Protocol** | Ordering and interaction flow among steps or perspectives |
| **Playbook** | Evidence-gathering method, checklist, test, or investigative technique |
| **Perspective** | Priors or decision policy that can change the recommendation; called a persona in the Astra Critique example |
| **Jurisdiction** | The artifact type or subject area over which a behavior has standing |
| **Reference** | Independently useful knowledge that should remain addressable rather than fused |
| **Prerequisite** | External capability, authority, runtime, credential, agent, or server required by the design |
| **Separate** | A neighboring but distinct user job with its own trigger |
| **Exclude** | A source deliberately omitted because it is unavailable, irrelevant, broken, or not worth retaining |

A source may contribute more than one category. For example, a command can carry machinery,
a prompt-review playbook, a prompt-only jurisdiction, and behavior-bearing authority fields.

## 6. Deciding what must remain distinct

Classify differences before proposing the skill:

| Difference | Usual treatment |
|---|---|
| Tone or register only | Preserve as optional style, not a separate perspective |
| Subject matter only | Jurisdiction |
| Investigative technique with the same decision policy | Playbook |
| Step ordering | Protocol |
| Different user outcome | Separate skill |
| Different decision policy on the same decision | Distinct perspective or mode |
| Different authority, prerequisite, or component type | Preserve explicitly; never waive through prose merger |

A candidate perspective is materially distinct when, with the artifact, evidence, decision,
and standing held constant, its priors can produce an incompatible recommendation.

During this design phase, documentary evidence may establish a provisional distinction. It
does not prove behavioral preservation. Record the later contrastive behavior that would
confirm or disprove the distinction, but do not build fixtures or a harness yet.

Lack of observed disagreement is evidence for further investigation, not proof of equivalence.

Absorption is evaluated against the surviving Astra stack as a whole, not by requiring one
source to match one public skill end to end. A source is a proposed absorption candidate only
when all three of these tests pass:

1. **Problem equivalence:** the source's user job is already owned by one or more surviving
   skills and introduces no independent user outcome or decision authority.
2. **Methodology equivalence:** the source's material protocol, playbooks, perspectives, and
   jurisdictions can be preserved behind those skills' existing interfaces and authority
   sequence. A bundled workflow may be divided across several surviving skills.
3. **Input/output equivalence:** the source's accepted inputs and material outputs can be mapped
   losslessly into the versioned Astra artifact chain, including source-specific evidence,
   degradation, and effect records. The mapping may normalize representation but may not discard
   a source-unique decision or artifact.

A different CLI, agent context, device bridge, framework, provider, or generated delivery shape
does not by itself create a separate public job. Preserve it as an internal profile, adapter,
agent, or prerequisite at the appropriate seam. Conversely, similarity on only one or two axes
is not absorption: a distinct outcome, authority model, or durable output remains independent or
deferred even when the generic coding stack could technically perform some of its steps.

For a coordinator-approved cross-stack bundle, one shared source-evidence record may hold the
canonical hashes and bundle census. Each consuming design must still adopt its exact source IDs,
local authority, secondary roles, preserved distinctions, and source-specific retirement gates;
a shared table cannot centralize or blur per-skill authority.

### 6.1 Three comparison systems

Every later evaluation of a source-merging design distinguishes three systems:

| System | Role |
|---|---|
| **Source oracle** | The strongest applicable original source for the artifact and jurisdiction, selected before outputs are seen |
| **Reference convener** | A temporary adapter that coordinates unchanged originals behind the proposed interface |
| **Self-contained candidate** | The proposed final adapter whose internal modules reproduce the retained behavior without depending on the originals |

The source oracle establishes the quality floor. The reference convener isolates the value of
routing and coordination from the risk of rewriting source behavior. The self-contained
candidate isolates internalization fidelity. A neutral wrapper may normalize input and output
shape for comparison, but it must not add perspective text, expected answers, or decision
policy.

The reference convener is a validation scaffold, not the end state when the approved goal is to
delete the originals. If it beats the source oracle but the self-contained candidate does not
match it, internalization damaged behavior. If better output is claimed and neither combined
system beats the source oracle on the design's declared advantage class, the design has not
established a quality benefit from combination.

## 7. Required per-skill design

Every completed phase-0 design under `designs/` must contain the following sections.
`designs/astra-critique.md` is normalized to this contract and is the reference example of it;
its sections 1–10 map one-to-one onto 7.1–7.10 below. The headings may be adapted for
readability, but the information may not be omitted.

### 7.1 Identity and status

- provisional Astra name;
- `proposed` status for an active roster candidate, or `superseded historical` for a design
  whose public job the user has explicitly merged into another candidate;
- `now`, `next`, or `later` priority, justified by personal project-development value and
  usage only as supporting evidence;
- candidate neighborhood or neighborhoods investigated;
- one-sentence user job beginning, “When I want to …”; and
- a personal-value statement naming why the user wants this job and whether that evidence is
  explicit or inferred.

`proposed` is the only active-candidate phase-0 design status. `superseded historical` is a
non-roster preservation state: it keeps source evidence, distinctions, dependencies, fixtures,
and retirement gates available while naming the surviving designs that inherit its authority.
It is not an implementation, validation, ledger-resolution, source-retirement, or deletion
state. Implementation and validation states belong to later implementation tracking, not to
this design field.

The job must express one outcome. If it needs “or” to join independent outcomes, split the
design or justify why one invocation must coordinate them.

### 7.2 Interface and scope

Define the future skill's small user-facing interface:

- requests that should trigger it;
- nearby requests that should not;
- accepted artifact or context at a conceptual level;
- user-visible result;
- non-goals; and
- decisions that remain with the user.

Treat the proposed skill as a module. Its invocation and behavioral promises form its
interface. Keep implementation complexity behind that interface.

### 7.3 Source evidence table

Account for every source occurrence investigated using the evidence requirements in section 4.
Assign each occurrence:

- a primary disposition;
- exactly one proposed primary home or independent disposition;
- contribution categories from section 5; and
- any secondary role in another design.

Mirror proposed changes to the collision source-claim ledger whose schema and protocol are in
`docs/phase-0.md` section 5 and whose authoritative state is in
`docs/phase-0-ledgers.md`. The phase-0 coordinator, not the design agent, applies those changes.
A claim determines who proposes a source's disposition; it never prevents an agent from
inspecting that source as evidence.

Do not hide overlaps. `pair-agent`, `office-hours`, and `skillify` are known repeated README
occurrences, but they are not the complete overlap set. Record cross-neighborhood semantic
roles as well. In particular, the Astra Critique analysis may inspect `review` and `cso` when
distinguishing code-structure judgment from test-evidence judgment without claiming either as
its primary source home.

### 7.4 Collision analysis

Explain:

- why the sources appeared duplicative;
- which behavior is actually shared;
- which entries are aliases or shallow delegation;
- which apparent duplicates are different jobs;
- where source instructions conflict;
- why the proposed skill is one coherent module; and
- the positive advantage the merger is expected to add over the source oracle.

### 7.5 Preserved distinctions

List every behavior, playbook, perspective, jurisdiction, authority field, prerequisite, and
failure behavior that must survive later implementation.

For each proposed merger, state what evidence supports it. For each retained distinction,
give a concrete decision or artifact on which it matters.

### 7.6 Proposed skill design

Describe the high-level implementation appropriate to this skill:

- internal modules and their responsibilities, if more than one is needed;
- the workflow or information flow;
- how one public interface preserves specialist behavior behind internal seams;
- where user choices occur;
- how factual uncertainty and unavailable prerequisites are represented;
- failure and degradation behavior;
- any internal seam justified by actual variation; and
- which architectural choices remain hypotheses until the later comparison systems are run.

Do not create a seam for hypothetical reuse. One adapter is a hypothetical seam; two justified
adapters make it real. Extract a shared Astra module only after at least two per-skill designs
demonstrate the same interface and variation.

### 7.7 Dependencies and delivery shape

Name agents, commands, tools, servers, hooks, runtimes, credentials, and external references
that remain separate. Explain whether the future skill invokes, reads, coordinates, replaces,
or merely documents each dependency.

For every proposed relation with a peer Astra skill, state its direction and distinguish:

- consuming the peer's output or capability;
- emitting a user-mediated handoff that only names the peer; and
- invoking the peer's workflow.

Name the exact problem or information class that crosses the relation, the minimum payload, who
decides whether the next workflow starts, and what happens when the peer is unavailable. Do not
draw one unlabeled edge for several of these semantics.

Because Astra Critique is a cross-cutting review loop, every peer design other than Critique must
declare `accepts Critique handoff: yes | conditional | no`. A **yes** or **conditional**
declaration must name the post-critique problem class the peer owns and the compact
destination-only payload it needs in addition to Critique's common problem envelope. A **no**
declaration must explain why the peer does not own a post-critique problem. It prevents a
fabricated handoff; it does not narrow Critique's accepted artifacts or review jurisdictions.
Critique handoffs are always user-mediated. Its report must retain every actionable finding and a
traceable route candidate for every independently owned problem class. One run emits zero or one
immediate handoff capsule: the user chooses whether any route continues and, when several
independent routes survive, which one continues now. Unselected routes remain explicit in the
report. If reviewers nominate incompatible destinations for the same problem, the user resolves
that classification before a capsule is emitted. The Critique chair may not invent, prioritize,
or silently drop a route, and Critique stops without reading or invoking the selected peer's full
workflow.

The destination peer's design owns the problem class it accepts and its destination-only payload.
During final roster reconciliation, the coordinator records that accepted profile as the
canonical peer contract and Critique consumes the reconciled snapshot. A missing, unavailable, or
inconsistent profile remains a named reconciliation gap in the report; Critique must not guess a
payload or redirect the problem to an unrelated peer.

Do not express tool pre-approval as tool restriction. Detailed permission design remains
deferred, but known authority requirements and forbidden effects must remain visible.

For every consumed independent reference, propose a `consuming_designs` update to the
reference and cleanup ledger whose schema is in `docs/phase-0.md` section 6 and whose state is
in `docs/phase-0-ledgers.md`. The global ledger, not this design, owns the reference's keep,
defer, or exclude disposition.

### 7.8 Manual bridge

Until implementation exists, give the exact current invocation or ordered manual workflow that
best approximates the proposed skill. State missing or unavailable prerequisites.

### 7.9 Deferred implementation and validation

List only the later decisions and validation obligations specific to this skill. Every design
that merges sources must define:

- its declared advantage class and the behavior that would demonstrate a positive win;
- the source-oracle, reference-convener, and self-contained-candidate comparison;
- a fixed corpus covering each source's home jurisdiction, the claimed advantage class,
  expected-divergence cases, expected-convergence controls, and prerequisite failures;
- paired runs on identical artifacts, with repeated trials and blinded, order-randomized
  evaluation where judgments are subjective;
- quality measures appropriate to the job, including critical-decision or defect recall,
  supported-claim precision, unsupported-claim rate, source-unique supported findings,
  actionability, duplicate/noise load, routing accuracy, cost, and latency where applicable;
- a home-jurisdiction non-regression gate against the source oracle;
- a positive-advantage gate against the source oracle on at least one declared combination
  class whenever better output is claimed;
- an internalization-fidelity gate comparing the self-contained candidate with the reference
  convener; and
- a source-specific retirement gate covering behavior, authority, dependencies, delivery
  shape, degradation, and user approval.

The design must state what a failed gate changes. A failed coordination gate rejects or narrows
the combined architecture. A convener win followed by a self-contained loss blocks
internalization and retirement. Matching final recommendations alone is insufficient when a
source-unique playbook or informative disagreement disappeared.

Do not repeat the global deferred-work list; `docs/phase-0.md` section 8 is authoritative for
phase-wide exclusions. Phase 0 records these obligations but does not build the corpus, wrapper,
convener, candidate, harness, or benchmark.

### 7.10 Provenance and open questions

Record inspected sources, revisions or hashes, evidence gaps, provisional decisions, and
questions that materially affect the design. Do not use `TBD` as a substitute for a described
uncertainty and its consequence.

### 7.11 Six-skill coding-lifecycle reconciliation contract

This subsection governs the minimal coding stack approved on 2026-08-11. It fixes authority,
artifact, consultation, and incremental-delivery policy before the designs absorb the rest of
the relevant source inventory. The policy is authoritative; the six surviving skills' complete
source-derived behavior is still provisional. Nothing here claims that all relevant sources
have been inspected, internalized, validated, or made retirement-eligible.

The lifecycle-authority roster is exactly:

- `astra-critique`;
- `astra-understand-code`;
- `astra-spec`;
- `astra-implement`;
- `astra-test`; and
- `astra-ship`.

`astra-report` is an additional directly invocable reporting surface, not a seventh lifecycle
authority. The six retain user-to-skill intake and approval authority. Under typed
`I(reporting)`, they delegate rich outbound presentation to Report, which returns no lifecycle
determination and starts no peer workflow.

`astra-plan` is divided between Spec's change authority and Implement's delivery authority.
`astra-debug` becomes Critique's diagnostic mode. Their design files remain
`superseded historical` source-accounting records and do not count as public roster members.

The normal change path is forward-only:

```text
astra-critique -> astra-spec -> astra-implement -> astra-test -> astra-ship
```

Greenfield work may begin at Spec. Understand Code is a conditional read-only participant when
a downstream judgment relies on an Understanding Report. Anticipated diagnostic uncertainty is
represented by conditional branches and carried forward by consultants; it does not create a
routine backward loop. Re-entry creates a new immutable change cycle only when evidence falls
outside every approved branch, invalidates an upstream finding, or introduces a new user-owned
decision. That condition is an `authority_gap`.

#### 7.11.1 Lifecycle authority

| Public skill | Owns | Primary authoritative output | Must not own |
|---|---|---|---|
| `astra-critique` | Observed problems, evidence, finding identity, and causal judgment | Finding Set containing evidence-backed review or diagnostic findings | Solution selection, target-repository mutation, or required behavior |
| `astra-understand-code` | Read-only current-state explanation within an explicit question | Optional Understanding Report | Findings, change selection, mutation, or approval |
| `astra-spec` | Intended change, selected solution, and required outcomes | Approved Change Specification | Repository delivery tasks, commit sequencing, or mutation |
| `astra-implement` | Repository-specific delivery planning and execution inside an approved specification | Approved Delivery Roadmap, Execution Ledger, atomic commits, and focused verification evidence | Reinterpreting findings, changing required behavior, independent acceptance, or publication |
| `astra-test` | Independent verification against pinned requirements and delivered revision | Test Evidence Packet | Weakening criteria, repairing production code, or publication |
| `astra-ship` | Publication and integration of a verified revision | Publication Record | Reinterpreting findings, requirements, implementation scope, or test evidence |

Spec accepts either greenfield intent or Critique findings. For critique-driven work, every
in-scope Finding ID must map to an explicit disposition, requirement, and acceptance criterion.
The Approved Change Specification owns the selected solution, rejected alternatives, target
behavior and interfaces, scope, non-goals, constraints, invariants, compatibility and semantic
migration strategy, required semantic ordering, positive and negative acceptance cases,
implementation freedoms, and approved conditional branches. A semantic sequence such as
`expand -> migrate -> contract` belongs to Spec; exact repository tasks and commits do not.

Implement inspects the live repository after receiving an approved Specification. It maps that
contract to exact files, symbols, tasks, dependency ordering, conditional diagnostic branches,
verification commands and working directories, evidence obligations, effects, stop conditions,
recovery and rollback limits, execution mode, bounded agent assignments, atomic commit
boundaries, and PR partitions. The user approves an immutable roadmap version, mutation scope,
execution mode, and commit authority before mutation. Progress, evidence, deviations, branch
selection, and commits are recorded in a separate Execution Ledger; the approved roadmap is
never rewritten.

Critique has three public modes behind its one interface:

- `review` produces evidence-backed judgment findings;
- `diagnose` produces evidence-backed causal findings, competing hypotheses, and proof
  obligations; and
- `consult` checks a downstream artifact against Critique authority.

The coding council remains available in review and diagnosis. In diagnosis, seats may propose
and challenge causal hypotheses, but only observed evidence may establish a cause. Critique may
inspect code, logs, history, and runtime state; run already-authorized existing tests and
diagnostic commands; and retain isolated evidence captures that cannot affect target behavior.
It may not add probes, tests, configuration, instrumentation, or fixes to the target repository.
Required instrumentation becomes a finding and is specified and executed forward through Spec
and Implement.

#### 7.11.2 `C` consultation relation

`C` is explicit, narrow peer consultation inside the six-skill stack. It is neither a seventh
public skill nor a harness dependency. It remains distinct from:

- `R`, roster and authority-ownership reconciliation without runtime invocation;
- `I`, consumption of a peer artifact or capability without invoking its judgment;
- `I(reporting)`, output-only presentation consumption: the producer owns facts, consequences,
  options, evidence, blocking state, and the returned user decision, while Report owns
  organization, density, language, staged disclosure, and evidence links; it returns no `pass`,
  `drift`, or `authority_gap` and is neither a public peer invocation nor an `H` handoff;
- `H`, Critique's user-mediated handoff capsule without automatically starting a peer; and
- `P`, provenance or source-history dependency without runtime permission.

An upstream peer exposes a read-only consultant mode under its existing authority. The
downstream peer decides when to invoke it and owns the active draft or execution. The upstream
peer owns its judgment policy and result schema. Only immutable, explicitly referenced artifacts
cross the relation; a peer may not read sideways into another peer's files. Consultation does
not rerun the upstream workflow and cannot mutate, approve, waive, or expand either contract.

A consultant returns exactly one bounded determination:

- `pass` — the downstream artifact or claim remains within preserved authority;
- `drift` — the active draft or execution conflicts with preserved authority but can still be
  repaired inside the downstream skill's current authority; or
- `authority_gap` — repair requires a new upstream artifact, new approved branch, or new
  user-owned decision.

One fresh, persistent consultant instance represents each required upstream authority for one
downstream invocation; checkpoints reuse that instance rather than spawning a new consultant.
If a required consultant cannot run, the downstream skill fails closed unless the user records
explicit acceptance of reduced assurance. Mechanical identity and hash checks supplement but
never replace consultant judgment.

For pair reconciliation, the complete forward authority order is:

```text
Understand Code -> Critique -> Spec -> Implement -> Test -> Ship
```

The arrow means `upstream consultant -> active downstream skill`. This is an authority order, not
a mandatory chronological workflow: the normal public change path still begins at Critique or,
for greenfield work, at Spec. The order yields exactly 15 admissible directed `C` pairs:

| # | Pair | Activation |
|---:|---|---|
| 1 | Understand Code -> Critique | The Finding Set directly relies on an Understanding Report |
| 2 | Understand Code -> Spec | The Specification directly relies on an Understanding Report |
| 3 | Understand Code -> Implement | The Roadmap or delivered revision directly relies on an Understanding Report |
| 4 | Understand Code -> Test | The Test packet directly relies on an Understanding Report |
| 5 | Understand Code -> Ship | The publication directly relies on an Understanding Report |
| 6 | Critique -> Spec | Finding Set authority is present |
| 7 | Critique -> Implement | Finding Set authority is present |
| 8 | Critique -> Test | Finding Set authority is present |
| 9 | Critique -> Ship | Finding Set authority is present |
| 10 | Spec -> Implement | Approved Change Specification authority is present |
| 11 | Spec -> Test | Approved Change Specification authority is present |
| 12 | Spec -> Ship | Approved Change Specification authority is present |
| 13 | Implement -> Test | Approved Delivery Roadmap and Execution Ledger authority is present |
| 14 | Implement -> Ship | Approved Delivery Roadmap and Execution Ledger authority is present |
| 15 | Test -> Ship | Test Evidence Packet authority is present |

Every Understand Code edge is conditional on direct reliance on the report's current-state
claims. Every Critique edge is conditional on present Finding Set authority. The other upstream
consultants are required only when their authoritative artifacts genuinely participate in the
active cycle; a consultant is never omitted merely to reduce cost.

Critique conditionally consults Understand Code after completing a relied-on Finding Set draft
and before issuing it, and rechecks after new evidence or a repository revision changes a relied-on
fact. Spec conditionally consults Understand Code and then consults Critique, as applicable, after
the complete draft and before whole-revision user approval. Implement consults Critique and Spec
before roadmap approval, at conditional diagnostic branch decisions, and at final implementation
verification, with Understand Code added when applicable. Test and Ship obtain cumulative
determinations before issuing their authoritative artifacts.

#### 7.11.3 Versioned artifact chain and failure behavior

| Skill | Authoritative artifact |
|---|---|
| Understand Code | Optional Understanding Report |
| Critique | Finding Set |
| Spec | Approved Change Specification |
| Implement | Approved Delivery Roadmap and Execution Ledger |
| Test | Test Evidence Packet |
| Ship | Publication Record |

Every artifact carries an immutable identity, revision, content hash, input references,
approval state where applicable, and consultant determinations. Traceability is complete and
machine-checkable through:

```text
finding -> requirement -> acceptance criterion -> roadmap task -> atomic commit
        -> test evidence -> PR
```

Conditional branches retain the same mapping; unselected branches remain recorded but
unexecuted. A stale or mismatched upstream identity stops the active skill. Pre-approval drift
is repaired in the active downstream draft and checked again. Evidence inside an approved
branch proceeds forward. Evidence outside the decision envelope returns `authority_gap` and
starts a new immutable cycle if the user continues.

Test may not weaken acceptance criteria or repair production code. A genuine independent Test
failure becomes a new Critique finding. Ship may repair publication-only defects within its own
authority; code, behavior, or evidence defects create a new cycle. Earlier artifacts remain
immutable and are referenced as superseded or contradicted evidence rather than rewritten.

#### 7.11.4 Atomic commits and narrow PRs

Implement defines commit and PR boundaries in the approved roadmap before mutation. Critique
and Spec consultants check that partitioning retains every finding and requirement; Ship checks
the realized history before publication.

Every implementation commit must:

- contain one logically indivisible change;
- include the tests and durable documentation required to make that change complete;
- exclude unrelated cleanup and metadata;
- pass its relevant focused checks;
- be independently understandable and safely revertible; and
- be created immediately after that atomic change is verified.

Roadmap approval supplies the bounded commit authority for those named changes. Implement owns
the resulting atomic implementation commits. Ship may create publication-owned commits such as
an approved version or changelog update, but it does not silently postpone, squash, reshape, or
rewrite Implement's verified atomic history.

Every PR must:

- serve exactly one functionality, feature, or bug fix;
- target no more than 400–500 authored changed lines;
- stop for repartitioning when it grows beyond that target;
- require explicit justification and user approval before exceeding 500 authored lines;
- place changes in different implementation languages into separate, explicitly ordered or
  stacked PRs;
- include only tests and durable documentation that directly support its functionality; and
- report generated output separately so it cannot conceal authored line count.

#### 7.11.5 Durable in-repository prose

Comments, docstrings, module headers, and durable developer documentation describe the shipped
artifact rather than the delivery sequence that produced it. They state their own subject's
purpose first, then behavior, invariants, effect or integration boundaries, prerequisites, and
stable rationale. Caller behavior belongs at the call site or module boundary; cross-file context
follows the subject's own contract.

Shipped prose must not embed roadmap or PR identifiers, future-commit choreography, temporary
snapshot claims, or language such as `for now` and `later PR` that becomes false as branches land.
An inactive path describes its current integration boundary rather than the future event expected
to activate it. Prose follows the repository's language-specific convention, including PEP 257 for
Python when applicable. Implement checks the authored diff before the atomic commit, and Ship
verifies that the recorded check covers the publication revision.

These are planning and publication constraints, not evidence that a PR is authorized in phase
0. Phase 0 creates or revises design documents only: no runtime skill, harness, installation,
source deletion, retirement, push, or PR is implied.

#### 7.11.6 Shared public trigger surface

Public routing follows the authoritative result requested and the recorded artifact state needed
to produce it. A bare keyword, historical source name, or final verb in a compound request is not
sufficient routing evidence.

| Requested result | Owner | Required state | Result |
|---|---|---|---|
| Explain current repository behavior or structure without changing it | `astra-understand-code` | Bounded code or repository scope; explicit `technical-design` request when applicable | Current-state Code Report |
| Judge an artifact or establish why an observed failure occurs | `astra-critique` | Reviewable artifact or observed failure evidence | Finding Set or causal finding |
| Decide intended behavior, selected solution, and acceptance | `astra-spec` | User intent, or accepted findings for remediation; Critique is not mandatory for greenfield intent | Approved Change Specification |
| Plan and execute exact repository delivery | `astra-implement` | Current Approved Change Specification and effect authority | Approved Delivery Roadmap, Execution Ledger, and atomic implementation commits |
| Construct or run independent proof at a pinned revision | `astra-test` | Accepted behavior, target snapshot, and effect boundary | Test Evidence Packet |
| Prepare and perform publication effects | `astra-ship` | Complete current artifact chain, passing evidence, and explicit effect authority | Publication Record |
| Explain recorded lifecycle artifacts, progress, decisions, or blockers | `astra-report` | Recorded producer artifacts or a producer-owned `ReportEvent` | Human-readable rendering with no lifecycle determination |

Selection obeys these rules:

1. Explicit invocation enters the named surface but enforces every artifact, authority, evidence,
   approval, and effect prerequisite.
2. Implicit routing chooses the **earliest missing authority** required for the requested outcome.
3. Ask one focused question when two plausible routes materially change authority, writable scope,
   external effects, evidence, or cost.
4. Run one public workflow. Required `C` checks occur inside it; `I`, `H`, and `I(reporting)` do
   not start public peers.
5. A compound request retains later outcomes as prospective stages and stops at every artifact or
   approval boundary.
6. The user starts each later public workflow. Report detail selection and
   `Understood, proceed` return control only and cannot start it.

There is **no automatic public peer invocation**. Internal modes, artifact presence, `C`, `I`,
`H`, `I(reporting)`, Report detail selection, and continuation controls may establish eligibility
or expose a next workflow, but cannot start it.

| Request | Canonical partition |
|---|---|
| “Explain this” | Repository or code state -> Understand Code; lifecycle artifact or change state -> Report |
| “Is this architecture right?” | Judge a choice -> Critique; explain current structure or read-only options -> Understand Code; select desired direction -> Spec |
| “Why did this test fail?” / “does it fail?” | Establish cause -> Critique `diagnose`; reproduce or check a pinned revision -> Test |
| “Review this failure” | Cause question -> Critique `diagnose`; evidence or artifact-quality question -> Critique `review`; ask once if the choice changes evidence or cost |
| “Fix this bug” | Cause or finding absent -> Critique; finding present but approved change absent -> Spec; exact Specification approved -> Implement |
| “Write tests” | Evidence-only or uncommitted artifact -> Test; shippable durable test -> Spec if not required, then an Implement Roadmap task; Test independently verifies |
| “Review and ship this” | Critique first for a new judgment; a clean review later crosses only as evidence and grants no publication authority |
| “Commit this” | Approved implementation commit -> Implement; authorized version or changelog publication commit, push, or PR -> Ship |
| “Resolve merge conflicts” | Ship during landing; Implement only for approved Roadmap base synchronization; otherwise stop for scope or authority |
| “Root cause analysis” | Critique `diagnose`; live-outage stabilization remains external `firefighting` |
| “Where are we?” | Artifact or project state -> Report; publication authorization or queue state -> Ship Status |
| “Turn this into an issue” | Spec only for intent or specification projection with separately authorized issue effects; generic roadmap-to-ticket projection remains unowned |
| “Explain, fix, test, and ship” | Earliest missing authority; later outcomes remain non-invoked, user-started stages |

This table supersedes active routes to the historical Plan and Debug peers while preserving their
design files as source and decision evidence.

#### 7.11.7 Producer reporting contract

Each lifecycle authority remains the content owner at every reporting moment. Its authoritative
artifact exposes the following producer-owned fields; an empty collection is `[]`, never an
omitted field.

| Field path | Type and invariant |
|---|---|
| `reporting.supersedes_ref` | `{artifact_id, revision, content_hash}` or `null`; Critique and Spec may map an existing supersession field |
| `reporting.surfaces` | List, empty as `[]`, never omitted |
| `reporting.surfaces[].surface_id` | Stable non-empty producer-owned ID |
| `reporting.surfaces[].claim` | Non-empty artifact-grounded statement |
| `reporting.surfaces[].consequence` | Non-empty producer-assigned impact statement |
| `reporting.surfaces[].blocking` | Boolean |
| `reporting.surfaces[].decision_required` | Boolean |
| `reporting.surfaces[].evidence_refs` | Non-empty stable artifact-field references |
| `reporting.open_decisions` | List, empty as `[]`, never omitted |
| `reporting.open_decisions[].decision_id` | Stable non-empty producer-owned ID |
| `reporting.open_decisions[].question` | Non-empty producer-owned question |
| `reporting.open_decisions[].options` | At least two unique `{option_id, label, consequence}` objects |
| `reporting.open_decisions[].evidence_refs` | Non-empty stable artifact-field references |
| `reporting.open_decisions[].blocking` | Boolean |

At artifact completion, an approval request, a stage boundary, an explicit status request, and a
failure or degradation announcement, the producer emits a `ReportEvent` with this envelope:

| Field | Type and invariant |
|---|---|
| `schema_version` | Literal `astra.report-event/v0` |
| `event_id` | Stable non-empty producer event ID |
| `event_type` | `artifact_completion`, `approval_request`, `stage_boundary`, `status_request`, or `failure` |
| `boundary_kind` | `entry_refused`, `work_stopped`, or `cycle_closed` for `stage_boundary`; otherwise `null` |
| `producer` | One of the six lifecycle identifiers |
| `artifact_ref` | `{artifact_id, revision, content_hash, path}`; `null` only for a pre-artifact `entry_refused` or `failure` with stable event and evidence or failure anchors |
| `outcome` | One non-empty producer-authored sentence |
| `blocking` | Boolean |
| `surface_candidates` | Producer-owned surfaces using the artifact shape above |
| `open_decision_refs` | Producer decision IDs |
| `evidence_refs` | Stable evidence references |
| `decision` | Complete matching open-decision object for `approval_request`; otherwise `null` |

The full approval decision envelope is never staged behind optional detail. Only the producer
records the user's answer against the exact authoritative artifact revision and hash.

If Report is unavailable at a non-decision moment, the producer emits only artifact and event
identity, a one-sentence outcome, blocking state, and an unavailable flag. At an approval request,
the producer presents its complete decision envelope itself. Report failure never changes
lifecycle authority or blocks progress solely because rich rendering is unavailable.

## 8. Architecture is local to each skill

These requirements standardize evidence and design completeness, not implementation shape.

Possible designs include:

- one direct workflow;
- selectable modes behind one interface;
- a sequence of distinct steps;
- a reference-driven procedure;
- coordination with retained agents or tools; or
- a panel of independent perspectives.

Choose the smallest design that preserves the source value. Do not create universal panel,
method-library, adapter-set, pipeline, or composition runtimes during this phase.

Selecting one superskill as the future interface does not settle its internal architecture.
Treat a panel, router, mode set, or direct workflow as a hypothesis until the skill-specific
comparison in section 7.9 establishes its claimed advantage. A temporary reference convener may
be implemented later to test that hypothesis; composition by reference is not an acceptable
final implementation for a source whose retirement requires self-containment.

## 9. Worked example: Astra Critique

The restored design at `designs/astra-critique.md` reproduces the last reviewed unified design
for the future Astra Critique skill from `ff889a4`. The original version is at `f264c20`, and
the later policy/pattern split begins at `ae44a91`.

Despite its historical title, that document is:

- an approach for implementing Astra Critique;
- not a universal condensation policy;
- not the actual skill; and
- not evidence that any source can already be retired.

Its source analysis demonstrates the required reasoning:

| Source group | Design lesson |
|---|---|
| `grill-me`, `grill-with-docs` | Delegating stubs contribute machinery; they do not establish new perspectives. A stub can still carry authority fields |
| `grilling` | An interrogation protocol that returns every decision to the user holds no priors of its own: it contributes protocol and machinery, not a perspective |
| `autoplan` | Fresh specialist contexts, explicit blind filing, dual-model review, consensus tables, degradation tags, decision auditing, and staged auto-decisions contribute protocol and machinery, not another perspective |
| `/diss`, `/diss-api`, `diss-infra` | Shared adversarial behavior can coexist with subject-specific jurisdictions and playbooks; register may vary without splitting the perspective |
| `diss-claudemd` | A name matching a family is not membership in it. Read the body: this one shares `/trim`'s role and playbook, not `/diss`'s voice |
| `/elon` | First-principles reconstruction contributes a distinct perspective |
| `/trim` | Prompt reduction, official-practice review, prompt-only jurisdiction, and authority fields must be classified separately |
| `office-hours` | Problem validation differs from rebuilding a solution from first principles |
| `plan-ceo-review` | Ambition, strategic leverage, and scope policy contribute a perspective |
| `plan-eng-review` | Incrementality, blast radius, reversibility, and production ownership contribute a separate perspective |
| `plan-design-review` | User hierarchy, journey, and interface consequences contribute a perspective and design playbooks |
| `plan-devex-review` | Time to first success and developer friction contribute a developer-experience perspective and playbooks |
| `plan-devex-review`, `devex-review` | One perspective can span a plan and a running artifact: that is two jurisdictions with two playbooks, not two voices |

The example proposes a panel because several sources have overlapping standing but can reach
incompatible recommendations. That architecture remains a hypothesis until its later
source-oracle, reference-convener, and self-contained-candidate comparisons pass. `autoplan`
already implements fresh reviewer contexts, blind filing, dual-model review, degradation, and
decision auditing for plans; those mechanisms are baseline evidence to preserve or improve,
not Astra Critique innovations. Astra Critique's claimed advantage is broader jurisdiction plus
explicit handling of normative conflicts. Other Astra skills must not copy the panel unless
their own source evidence and declared advantage establish the same need.

`designs/astra-critique.md` was normalized in place to section 7 on 2026-07-30, preserving the
condensation and panel reasoning in labeled historical appendices. That normalization resolved the
required ambiguity on evidence: the `/diss` voice is **one** perspective whose register names two
people jointly; test-evidence judgment inside it is a threshold and a filter rather than a rival
prior; and the genuine code-structure-versus-test-evidence conflict is between `/diss` and
`review`, which defines itself as finding *"structural issues that tests don't catch."* Historical
packaging, tiering, tuning, and generic runtime proposals remain labeled historical rather than
becoming phase-0 requirements.

Four of that design's original classifications were disproved by reading the source bodies. Agents
should read the corrections as a warning about label-based clustering, not as settled taxonomy for
their own neighborhoods.

## 10. Agent workflow

The phase-0 coordinator reserves source claims before assigning design work. An assigned agent
must:

1. Read `docs/phase-0.md` and this document completely.
2. Inspect the assigned occurrences in `README.md` section “The collision map,” their
   registrations, and any cross-neighborhood or reference sources needed to understand them.
3. Build the source evidence table before proposing names or architecture.
4. State the shared user job and personal value, then split entries that do not serve it.
5. Map each source contribution, primary disposition, secondary role, and preserved
   distinction.
6. State the merger's expected positive advantage over the source oracle.
7. Propose the smallest coherent interface and a skill-specific high-level design.
8. Define the three comparison systems, skill-specific corpus classes, quality gates, and the
   consequence of failure.
9. Compare its trigger with any available peer designs and record possible collisions for the
   final reconciliation pass.
10. For every design other than Critique, declare Critique handoff acceptance as **yes**,
    **conditional**, or **no** and record any proposed handoff-profile change for roadmap
    reconciliation. A Critique revision instead reconciles destination coverage from its side.
11. Record the current manual bridge and skill-specific deferred work.
12. Record proposed changes to both phase-0 ledgers inside the assigned design.
13. Self-review against section 11.
14. Change only the assigned design file unless given broader authority.

Agents may inspect sources outside their assigned neighborhood; “change only the assigned
design” is an edit boundary, not an evidence boundary. Agents do not assume peers have already
finished. After all draft designs exist, the coordinator performs the authoritative
roster-wide trigger and ownership comparison described in `docs/phase-0.md`.

If a neighborhood yields multiple independent jobs, propose multiple design files through the
coordinator. If two neighborhoods yield one job, record the cross-neighborhood merge and
account for every source without taking an already claimed primary home.

## 11. Review checklist

### Grounding

- [ ] Every investigated occurrence has an exact identifier and component type.
- [ ] Live location, invocation, availability, declaration, and behavior evidence are recorded.
- [ ] Every inspected source has an immutable revision or content hash and inspection date.
- [ ] Observed, inferred, and unavailable claims are distinguishable.
- [ ] No unavailable source is claimed as absorbed.

### Skill scope

- [ ] The design serves one user job through one distinguishable interface.
- [ ] The design states why this user wants the job and labels inferred value as provisional.
- [ ] Trigger, non-trigger, result, non-goals, and user-owned decisions are explicit.
- [ ] The collision-map row was treated as a candidate, not a predetermined skill.
- [ ] Nearby per-skill triggers do not silently collide.

### Preservation

- [ ] Shared machinery is separated from protocols, playbooks, perspectives, and jurisdictions.
- [ ] Authority fields, prerequisites, failure behavior, and component types remain visible.
- [ ] Every occurrence has exactly one proposed primary disposition and primary home.
- [ ] Every overlap or cross-role names its primary home and explicit secondary role or exclusion.
- [ ] Every merger and retained distinction has a written evidence basis.
- [ ] The design states what later behavioral validation must prove.
- [ ] One public interface does not flatten source-specific perspectives, playbooks,
      jurisdictions, authority, or failure behavior.

### Evaluation contract

- [ ] The design names its expected positive advantage over the source oracle.
- [ ] Source-oracle, reference-convener, and self-contained-candidate systems are distinguished.
- [ ] Home-jurisdiction, advantage, divergence, convergence, and prerequisite-failure cases are
      named.
- [ ] Home non-regression, positive advantage, internalization fidelity, and retirement are
      separate gates.
- [ ] Every failed gate has an explicit architectural or retirement consequence.

### Design quality

- [ ] The user-facing interface is smaller than the behavior it exposes.
- [ ] Internal seams correspond to demonstrated variation.
- [ ] The architecture is local to this skill rather than copied from Astra Critique.
- [ ] A minimal-coding-stack design preserves the authority and output boundary in section
      7.11.1 and does not reclaim a peer's judgment.
- [ ] Every peer relation distinguishes output or capability consumption, a user-mediated
      handoff, and workflow invocation.
- [ ] Every `C` relation names the upstream authority, immutable input artifact, checkpoints,
      determination handling, and unavailable-consultant behavior from section 7.11.2.
- [ ] Every design other than Critique declares handoff acceptance as **yes**, **conditional**, or
      **no**; every accepting relation names one owned problem class and compact destination
      payload. Critique revisions reconcile destination coverage instead.
- [ ] Critique preserves every independent route candidate in its report, emits at most one
      user-selected immediate handoff, and consumes only coordinator-reconciled destination
      profiles owned by the accepting peers.
- [ ] Failure, uncertainty, degradation, and user decisions are addressed at design level.
- [ ] A minimal-coding-stack output carries immutable identity and traceability fields and treats
      unapproved evidence as `drift` or `authority_gap` rather than silently rewriting history.
- [ ] Implement and Ship preserve the atomic-commit, one-functionality-per-PR,
      language-partition, and authored-line policies in section 7.11.4.
- [ ] Implement and Ship preserve the durable in-repository prose policy in section 7.11.5.
- [ ] A usable manual bridge exists, or its missing prerequisite and consequence are named.

### Scope discipline

- [ ] No `SKILL.md`, executable prompt, plugin scaffold, or runtime implementation was created.
- [ ] No final tool permissions, cache, telemetry, packaging, or tuning system was designed.
- [ ] No existing source was disabled, uninstalled, deleted, or declared eligible for retirement.
- [ ] Open questions name their consequence instead of using empty placeholders.

## 12. Definition of done

A per-skill design is ready for review when:

1. all assigned source occurrences are accounted for;
2. the job is personally valuable and its interface is distinguishable from the emerging
   roster;
3. source contributions and preserved distinctions are evidence-backed;
4. the proposed architecture is concrete enough to guide later implementation planning;
5. the expected advantage and three-system validation contract can distinguish routing,
   coordination, internalization, and retirement failures;
6. peer relations are explicit, every design other than Critique declares handoff acceptance, no
   relation conflates naming a peer with invoking it, and no independent route is lost merely
   because only one immediate handoff may be emitted;
7. implementation details and behavioral validation remain explicitly deferred;
8. the manual bridge is usable or its missing prerequisite and consequence are named; and
9. every applicable six-skill lifecycle, consultant, artifact, failure, and delivery invariant
   in section 7.11 is specialized without contradiction; and
10. the review checklist passes without placeholders or authority conflicts.

Passing these requirements means the design is grounded. It does not mean the skill is
implemented, validated, installed, or safe to use as a replacement.

## 13. Deferred work

`docs/phase-0.md` section 8 is the single phase-wide deferred-work list. A per-skill design
records only its skill-specific future decisions and validation obligations under section 7.9.
