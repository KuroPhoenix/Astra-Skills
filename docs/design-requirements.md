# Astra skill design requirements

**Date:** 2026-07-30
**Status:** Approved structure; revised for agent review

## 1. Purpose

This document tells agents how to produce one evidence-grounded design document for each
proposed Astra skill.

It governs design work only. A compliant output explains:

- why the skill should exist;
- which existing artifacts inform it;
- what behavior and distinctions must survive condensation;
- what interface the future skill should present; and
- which high-level architecture best fits that particular skill.

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

## 7. Required per-skill design

Every completed phase-0 design under `designs/` must contain the following sections. The
restored `designs/astra-critique.md` is currently the worked source design and must be
normalized to this contract before it is accepted as complete. The headings may be adapted
for readability, but the information may not be omitted.

### 7.1 Identity and status

- provisional Astra name;
- `proposed` status;
- `now`, `next`, or `later` priority, justified by personal project-development value and
  usage only as supporting evidence;
- candidate neighborhood or neighborhoods investigated;
- one-sentence user job beginning, “When I want to …”; and
- a personal-value statement naming why the user wants this job and whether that evidence is
  explicit or inferred.

`proposed` is the only phase-0 design status. Implementation and validation states belong to
later implementation tracking, not to this design field.

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

Mirror proposed changes to the collision source-claim ledger in `docs/phase-0.md` section 5.
The phase-0 coordinator, not the design agent, applies those changes to the authoritative
ledger. A claim determines who proposes a source's disposition; it never prevents an agent
from inspecting that source as evidence.

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
- where source instructions conflict; and
- why the proposed skill is one coherent module.

### 7.5 Preserved distinctions

List every behavior, playbook, perspective, jurisdiction, authority field, prerequisite, and
failure behavior that must survive later implementation.

For each proposed merger, state what evidence supports it. For each retained distinction,
give a concrete decision or artifact on which it matters.

### 7.6 Proposed skill design

Describe the high-level implementation appropriate to this skill:

- internal modules and their responsibilities, if more than one is needed;
- the workflow or information flow;
- where user choices occur;
- how factual uncertainty and unavailable prerequisites are represented;
- failure and degradation behavior; and
- any internal seam justified by actual variation.

Do not create a seam for hypothetical reuse. One adapter is a hypothetical seam; two justified
adapters make it real. Extract a shared Astra module only after at least two per-skill designs
demonstrate the same interface and variation.

### 7.7 Dependencies and delivery shape

Name agents, commands, tools, servers, hooks, runtimes, credentials, and external references
that remain separate. Explain whether the future skill invokes, reads, coordinates, replaces,
or merely documents each dependency.

Do not express tool pre-approval as tool restriction. Detailed permission design remains
deferred, but known authority requirements and forbidden effects must remain visible.

For every consumed independent reference, propose a `consuming_designs` update to the
reference and cleanup ledger in `docs/phase-0.md` section 6. The global ledger, not this
design, owns the reference's keep, defer, or exclude disposition.

### 7.8 Manual bridge

Until implementation exists, give the exact current invocation or ordered manual workflow that
best approximates the proposed skill. State missing or unavailable prerequisites.

### 7.9 Deferred implementation and validation

List only the later decisions and validation obligations specific to this skill, such as a
contrastive behavior the future implementation must preserve, a prerequisite failure path, or
a source-specific retirement gate. Do not repeat the global deferred-work list;
`docs/phase-0.md` section 8 is authoritative for phase-wide exclusions.

### 7.10 Provenance and open questions

Record inspected sources, revisions or hashes, evidence gaps, provisional decisions, and
questions that materially affect the design. Do not use `TBD` as a substitute for a described
uncertainty and its consequence.

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
| `grill-me`, `grill-with-docs` | Delegating stubs contribute machinery; they do not establish new perspectives |
| `grilling` | Relentless one-at-a-time decision interrogation contributes a decision policy and interaction behavior |
| `autoplan` | Sequencing specialist reviews contributes protocol, not another perspective |
| `/diss`, `/diss-api`, `diss-infra`, `diss-claudemd` | Shared adversarial-review behavior can coexist with subject-specific jurisdictions and playbooks |
| `/elon` | First-principles reconstruction contributes a distinct perspective |
| `/trim` | Prompt reduction, official-practice review, prompt-only jurisdiction, and authority fields must be classified separately |
| `office-hours` | Problem validation differs from rebuilding a solution from first principles |
| `plan-ceo-review` | Ambition, strategic leverage, and scope policy contribute a perspective |
| `plan-eng-review` | Incrementality, blast radius, reversibility, and production ownership contribute a separate perspective |
| `plan-design-review` | User hierarchy, journey, and interface consequences contribute a perspective and design playbooks |
| `plan-devex-review` | Time to first success and developer friction contribute a developer-experience perspective and playbooks |

The example chooses a panel because several sources have overlapping standing but can reach
incompatible recommendations. Blind filing, conflict handling, verification, and procedural
rendering are Astra Critique design decisions. Other Astra skills must not copy them unless
their own source evidence establishes the same need.

Before it counts as a completed phase-0 design, `designs/astra-critique.md` must be normalized
in place to section 7 while preserving the useful condensation and panel reasoning. That
normalization must explicitly resolve any remaining ambiguity in how the `/diss` voice,
code-structure judgment, and test-evidence judgment are separated. Historical packaging,
tiering, tuning, and generic runtime proposals remain labeled historical rather than becoming
phase-0 requirements.

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
6. Propose the smallest coherent interface and a skill-specific high-level design.
7. Compare its trigger with any available peer designs and record possible collisions for the
   final reconciliation pass.
8. Record the current manual bridge and skill-specific deferred work.
9. Record proposed changes to both phase-0 ledgers inside the assigned design.
10. Self-review against section 11.
11. Change only the assigned design file unless given broader authority.

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

### Design quality

- [ ] The user-facing interface is smaller than the behavior it exposes.
- [ ] Internal seams correspond to demonstrated variation.
- [ ] The architecture is local to this skill rather than copied from Astra Critique.
- [ ] Failure, uncertainty, degradation, and user decisions are addressed at design level.
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
5. implementation details and behavioral validation remain explicitly deferred;
6. the manual bridge is usable or its missing prerequisite and consequence are named; and
7. the review checklist passes without placeholders or authority conflicts.

Passing these requirements means the design is grounded. It does not mean the skill is
implemented, validated, installed, or safe to use as a replacement.

## 13. Deferred work

`docs/phase-0.md` section 8 is the single phase-wide deferred-work list. A per-skill design
records only its skill-specific future decisions and validation obligations under section 7.9.
