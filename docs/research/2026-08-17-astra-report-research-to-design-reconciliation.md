# Astra Report research-to-design reconciliation

**Date:** 2026-08-17

**Baseline:** `2044595` (`main` and `origin/main` at inspection time)

**Scope:** Reconcile the complete Astra Report research handoff with the current approved
repository design and the user's later decisions about implicit outbound reporting, progress
indicators, artifact delivery, and the first public milestone.

**Status:** Design-direction record only. This document does not amend the canonical Report or
lifecycle contracts, authorize a runtime skill, create a universal runtime interface, install a
skill, mutate a lifecycle artifact, change a ledger, or retire a source. The current authority
remains `docs/design-requirements.md`, `docs/design-roadmap.md`, `docs/phase-0.md`,
`designs/astra-report.md`, and the six sibling lifecycle designs until their text is amended.

## 1. Verdict

The research handoff mostly **confirms**, rather than replaces, the approved Astra Report design.
The repository already encodes the distinctive semantic core:

- reply-surface budgeting rather than word-count optimization;
- exposure-aware state delta with a fresh Context Capsule;
- an append-only Exposure Ledger that records exposure rather than inferred cognition;
- staged Standard delivery, named deferral, blocker escalation, and evidence-grade drill-down;
- producer-owned truth, consequences, severity, options, evidence, and workflow authority; and
- Report-owned presentation with no lifecycle determination or orchestration.

The development direction nevertheless changes in two material ways because later user decisions
are broader than the current execution plan:

1. **The first public milestone becomes an interface-complete Report v1.** The delegated Spec
   approval slice remains valuable as a conformance tranche, but it no longer defines the public
   identity or release boundary of `astra-report`.
2. **The reporting seam must accept reportable outbound events beyond the six lifecycle skills.**
   The six remain the only Astra lifecycle authorities. A more general producer may delegate
   presentation of progress, results, blockers, decisions, or deliverables without gaining
   lifecycle authority and without turning Report into a conversation summarizer.

This is a change to **ingress breadth and release strategy**, not to Report's authority.

## 2. Authority and evidence discipline

### 2.1 Precedence used in this reconciliation

1. Later explicit user decisions win when they conflict with an older repository direction.
2. The repository remains the current implemented and approved design authority until those later
   decisions are encoded through explicit amendments.
3. The research handoff explains and evaluates the design; it does not itself authorize runtime.
4. Historical slice documents remain evidence unless a canonical amendment gives them a new role.

### 2.2 Evidence states remain separate

| Evidence state | Meaning for development |
|---|---|
| Established surrounding result | May motivate a design rule, but does not prove Astra's specific mechanism |
| Astra synthesis | An architecture or interaction hypothesis that must be stated as Astra's own |
| Product default | A configurable initial choice, not a human-attention constant |
| Validation result | Runtime evidence obtained later against a fixed version and explicit baseline |

The fidelity order remains controlling:

> **fidelity > caveat completeness > structure > concreteness > simplicity > brevity**

The current `skim` one-surface default and Standard three-surface/one-decision defaults remain
testable product defaults. No literature source proves those numbers.

## 3. Research-to-design classification

### 3.1 Already encoded

| Handoff conclusion | Current repository encoding | Reconciliation consequence |
|---|---|---|
| Report is a reporting layer, not a generic summarizer | `designs/astra-report.md` sections 1–3 | Retain |
| Six authorities, one voice | Report sections 1.1–1.2 and 8; requirements 7.11.6–7.11.7 | Retain the authority split |
| Reply surface is the interaction-cost unit | Report sections 2.2 and 7.5 | Retain and expose as a measurable parameter |
| State delta is change → consequence → next decision | Report sections 2.2, 6.6, and 7.4 | Retain structural revision/supersession computation |
| Delta-first, not delta-only | Report sections 6.6 and 7.2 | Retain the fresh Context Capsule |
| Exposure is not recall | Report sections 2.4 and 7.3 | Retain; no cognitive inference |
| Stateless renderer plus a small append-only ledger | Report sections 1.1, 7.3, and 7.4 | Retain as the minimal durable-state model |
| Stable IDs, consequence typing, supersession, and common decisions belong to producers | Report section 8.6 and all six sibling section 13 amendments | Retain producer ownership |
| `skim`, staged `standard`, and `deep` | Report sections 3.1 and 7.1–7.2 | Retain |
| Blocking decisions bypass the budget | Report sections 6.4 and 7.5 | Retain without exception |
| Initial layer is complete for action | Report section 7.2 | Retain |
| Affordances and meaningful previews replace optional questions | Report sections 1.1, 7.2, and 7.5 | Retain |
| Deferred consequential detail stays named and addressable | Report sections 6.9 and 7.2 | Retain |
| Safe continuation is not approval | Report sections 1.1 and 8.4 | Retain exact producer option semantics |
| Host capability changes mechanics, not content | Report sections 3.4, 7.2, and 7.6 | Retain |
| Contradictions and missing metadata degrade visibly | Report section 7.6 | Retain |
| Research attribution must distinguish source, Astra synthesis, and default | Method canon sections 1, 8–11 | Retain in design and future runtime references |

### 3.2 Partially encoded

| Handoff or later decision | Present coverage | Missing part |
|---|---|---|
| One outbound reporting voice | Covers the six lifecycle producers | Does not cover other agents producing reportable results or deliverables |
| Implicit reporting | Covers exactly five `I(reporting)` moments | Lacks a producer-neutral definition of a reportable outbound event |
| Progress reporting | Named as delegated output | Lacks typed step state and host rendering semantics |
| Host adaptation | Structured choices and text index | Lacks native progress-indicator mapping and equivalent textual fallback |
| Artifact delivery | Direct lifecycle-artifact briefs are supported | Lacks a general read-only deliverable descriptor for reports, Markdown, code, and diffs |
| Experimental separability | Section 7.7 names analytical internal seams | Does not yet make the principal treatment choices independently selectable |
| Stable addressability | Strong for lifecycle artifacts | Non-lifecycle deliverables need stable producer-owned IDs or an explicit degraded mode |

### 3.3 Absent from the current canonical design

1. A producer-neutral base reporting envelope that preserves the provenance class of its source.
2. A progress spine with producer-owned `pending`, `active`, `completed`, `blocked`, and `failed`
   states.
3. A separate Report disclosure axis such as `not_shown`, `previewed`, and `opened`.
4. Host-native progress indicators with a content-equivalent textual fallback.
5. Read-only delivery descriptors for reports, Markdown files, code changes, diffs, and other
   producer-created artifacts.
6. An interface-complete v1 gate exercised across multiple report families.
7. A release rule that keeps internal content-specific increments private until the common
   interface and representative diversity pass together.

### 3.4 Intentionally rejected and still rejected

- inferred recall, comprehension, attention, or psychological state;
- arbitrary chat-history summarization;
- cross-project ranking or scheduling;
- proactive notifications or autonomous interruption;
- lifecycle orchestration or automatic peer invocation;
- Report-owned severity, truth, requirements, decisions, or approval;
- silent artifact repair or contradiction resolution;
- a second source of truth or a lossy replacement for authoritative artifacts;
- a giant dashboard, visual-reporting system, or elaborate personalization model; and
- a research harness built before a stable product interface exists.

Native square progress indicators are not the rejected visual-reporting system. They are a host
affordance for a small typed work-state contract and must have a textual equivalent.

### 3.5 Superseded by later user decisions, pending repository amendment

The following statements remain present in canonical files but should no longer govern the next
public milestone:

1. `designs/astra-report.md` section 12.2: the first implementation slice covers delegated Spec
   approval only and must not advertise direct requests.
2. `docs/design-roadmap.md` amendments 7 and 9: select one non-retiring vertical slice, implement
   and dogfood it, then widen.
3. `docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md`: the first
   `SKILL.md` advertises delegated approval rendering only and explicitly excludes catch-up,
   artifact explanation, and project status.
4. The plan's six fixed Spec topic sections as the first runtime's operative content catalog.

These artifacts are not discarded. They become a **Spec-approval conformance tranche** under the
broader v1 acceptance matrix. Their fidelity, approval, receipt, and ledger cases remain useful.

## 4. Exact design conflicts to resolve

### 4.1 Producer universe

The current `ReportEvent` contract names one of the six lifecycle skills as producer. The later
decision is that an agent should invoke Report implicitly whenever it emits a reportable outbound
update. Making every producer impersonate one of the six would corrupt provenance and authority.

**Required resolution:** define a producer-neutral base envelope with an explicit provenance
class. Preserve the existing six-skill `astra.report-event/v0` as a lifecycle-authoritative
profile or adapter until migration is justified.

### 4.2 Trigger breadth

The current five moments are suitable lifecycle triggers but are not a complete agent-neutral
trigger vocabulary.

**Required resolution:** define a reportable outbound event as one of:

- progress or stage-state update;
- completed result;
- blocker, refusal, failure, or degradation;
- decision or approval request;
- deliverable presentation; or
- status/resumption request.

Ordinary intake, clarification, brainstorming, teaching, and conversational explanation remain
direct unless they produce one of those reportable outputs. This prevents implicit invocation from
turning Report into the whole conversational interface.

### 4.3 Work state versus disclosure state

The producer currently owns facts and consequences, but the shared contract does not model a
step's work state. Report's ledger models exposure, but it must not be mistaken for task progress.

**Required resolution:** keep two independent axes:

| Axis | Owner | Example states |
|---|---|---|
| Work state | Producer | `pending`, `active`, `completed`, `blocked`, `failed` |
| Disclosure state | Report | `not_shown`, `previewed`, `opened` |

Report may render a square, check, spinner, warning, or textual label for producer state. It may
not infer or mutate that state. Opening a topic never completes a work step; completing a work step
never proves that the user saw it.

### 4.4 Deliverable reporting versus neighboring authority

The user wants Report to organize delivery of reports, artifacts, code, and Markdown files. The
current design limits direct requests to lifecycle artifacts and excludes file/visual adapters.

**Required resolution:** v1 may present a producer-created deliverable through a stable descriptor:
identity, kind, revision or hash when available, location/link, producer-authored outcome and
consequence, validation/evidence references, and any caveat. Report may order, preview, excerpt,
and link that material. It may not author or edit the deliverable, invent its significance, or
turn a producer claim into lifecycle authority.

The neighboring job boundary remains:

- delivering a code change or diff already produced by an authorized workflow → Report;
- explaining how repository code behaves or is structured → Understand Code;
- judging whether a code change is correct → Critique or Test, according to the requested result;
- writing durable documentation or code → the producer that owns that effect.

Visual dashboards and generated presentation artifacts remain outside v1. Host-native progress
controls, links, attachments, and structured choices are delivery mechanics, not a new visual
reporting authority.

### 4.5 Runtime milestone

The current plan is internally coherent but publicly too narrow. Its metadata would cause agents
to learn that Astra Report means “delegated Spec approval renderer,” recreating the specialization
the later user decision rejects.

**Required resolution:** internal increments may remain small, but no content-specific increment
is released or described as the completed Report skill. The first public milestone must pass one
common interface across representative report families.

### 4.6 Phase-0 execution authority

`docs/phase-0.md` explicitly excludes Astra `SKILL.md` creation, runtime state, and universal
composition/error interfaces. The broader direction does not waive that gate.

**Required resolution:** amend the canonical design and roadmap first. Runtime work begins only
after a separate explicit execution choice is recorded in `docs/phase-0.md` with its exact scope.

## 5. Recommended v1 module and seams

### 5.1 External seam

Report should be a deep presentation module with one conceptual operation:

```text
render(report input, mode, exposure facts, host capabilities) -> Reader Brief segments
```

The interface includes its invariants and error modes, not merely a function signature. Callers
must provide stable provenance and producer-owned semantics; Report guarantees staged,
trace-preserving presentation without changing those semantics.

Two input profiles cross the same seam:

1. **Direct scope:** resolved authoritative artifacts or stable producer deliverables.
2. **Delegated packet:** a producer-owned reportable outbound event.

The current lifecycle `ReportEvent` maps into the delegated profile. A non-lifecycle packet never
becomes an Astra authoritative artifact merely by passing through Report.

### 5.2 Implementation hidden behind the seam

```text
producer work state and stable source references
                    │
                    ▼
        direct scope or delegated packet
                    │
                    ▼
             Astra Report core
   provenance validation · Capsule · delta
   attention allocation · staging · previews
   visible deferral · fidelity preservation
                    │
           ┌────────┴────────┐
           ▼                 ▼
     host rendering     receipt-gated
       adapter          Exposure Ledger
```

Scope selection, delta computation, attention allocation, composition, host rendering, and ledger
append may be internal seams for testing. They should not become public interfaces unless actual
variation demonstrates the need. Host rendering is a real seam because at least native UI and
text fallback adapters are required.

### 5.3 Degradation rules for the broader ingress

- Missing stable source references: render a labelled full-current brief only when fidelity can be
  preserved; do not claim delta.
- Missing producer consequence or decision fields: state the contract gap; do not infer them.
- Non-authoritative producer packet: retain that provenance label; do not compare it as if it were
  a lifecycle artifact.
- Missing host progress UI: render the same ordered steps and states textually.
- Missing exact delivery receipt: do not append exposure.
- Changed or superseded source: invalidate prior exposure for the changed revision.
- Contradictory sources: expose both references and the contradiction; do not adjudicate.

## 6. Meaning of an interface-complete Report v1

“Whole Report” means the public interface and its invariants work across representative diversity.
It does not mean every future producer, file format, host, visualization, or research treatment is
implemented.

The release gate should cover at least these report families through the same module:

| Family | Required behavior |
|---|---|
| Live progress | Native or textual step spine; producer state preserved; current attention point clear |
| Completion/result | Outcome, consequence, evidence, and remaining action presented without reopening unrelated branches |
| Blocker/failure | Blocking content bypasses the budget; failure provenance and next permitted action remain exact |
| Decision/approval | Full producer-owned decision envelope in NOW; Report records presentation only |
| Lifecycle artifact | Capsule, current chain state, visible deferral, stable drill-down |
| Text deliverable | Report/Markdown identity, location, significance, caveats, and validation links |
| Code deliverable | Changed code/diff locations and producer-owned outcome/evidence without code-authority expansion |
| Resumption | Fresh Capsule plus exposure-aware structural delta; full-state fallback without a usable ledger |
| Contradiction/degradation | Both sides or exact missing contract named; no invented repair |
| Host fallback | Semantically equivalent structured and text delivery, including progress and detail navigation |

The existing 25-case delegated Spec approval design remains one row set inside this matrix. The
handoff scenarios covering absence, 33 findings, contradictions, missing ledger/receipt, revised
artifacts, incomplete decisions, and optional detail remain mandatory cross-family cases.

## 7. Development direction

### 7.1 Documentation sequence before runtime

1. Approve this reconciliation record.
2. Amend `designs/astra-report.md` with the broader user job, reportable-event boundary, generic
   ingress profile, progress semantics, deliverable descriptors, and interface-complete milestone.
3. Amend `docs/design-requirements.md` sections 7.11.6–7.11.7 without moving any of the six
   lifecycle authorities.
4. Amend `docs/design-roadmap.md` so “slice-first” describes internal construction rather than the
   first public product identity.
5. Preserve the six sibling reporting hooks. Change them only as needed to map the existing
   lifecycle profile into the broader envelope; do not make them generic agents.
6. Reclassify the Slice A design and implementation plan as a Spec-approval conformance tranche,
   or supersede the executable plan with a v1 plan that incorporates it.
7. Record a separately approved runtime scope in `docs/phase-0.md` before creating `SKILL.md`,
   schemas, scripts, tests, or ledger storage.

### 7.2 Runtime construction after authorization

Use one Report v1 integration branch. Internal changes may be reviewed in bounded increments:

1. common input contract and pure renderer;
2. progress/work-state and disclosure semantics;
3. Exposure Ledger and structural delta;
4. native-host and text adapters;
5. diverse acceptance matrix and dogfooding.

An increment may land on the integration branch without being advertised as a usable public
`astra-report`. Promotion occurs only after the interface-complete gate passes. This preserves
small reviewable changes without specializing the skill around the first fixture.

## 8. Research separability without a premature harness

The product implementation should avoid entangling these treatment choices:

- flat versus staged presentation;
- full-state versus state-delta resumption;
- word budget versus reply-surface budget;
- stateless versus Exposure-Ledger-aware rendering; and
- user-selected versus automatically selected depth.

Configuration or internal strategy selection is sufficient initially. Do not build participant
management, experimental telemetry, or a general study platform into Report v1.

The strongest initial research candidates remain:

1. whether reply-surface count predicts supervision burden better than word count; and
2. whether exposure-fact-conditioned state delta improves technical task resumption over a full
   recap without requiring recall inference.

Objective outcomes such as decision accuracy, severe findings missed, prioritization, time to
correct action, and resumption accuracy take precedence over preference alone. Negative results
must be allowed to change the product defaults.

## 9. Repository amendment map

| File | Required disposition |
|---|---|
| `designs/astra-report.md` | Canonical design amendment; preserve core and widen ingress/delivery/milestone |
| `docs/design-requirements.md` | Reconcile reporting trigger and payload policy while preserving six authorities |
| `docs/design-roadmap.md` | Replace public slice-first release direction with interface-complete v1 and internal increments |
| Six sibling lifecycle designs | Preserve authority and current hooks; add only an adapter/profile clarification if required |
| Slice A acceptance design | Retain as a conformance tranche, no longer the complete first milestone |
| Slice A implementation plan | Mark superseded for execution or rewrite beneath the v1 milestone |
| `docs/phase-0.md` | Leave unchanged until a separate runtime authorization decision |
| `README.md` | No current normative change required; it remains inventory/research context |

## 10. Stop condition

This reconciliation stops before canonical design amendment and runtime. The next approval
boundary is the user's review of this classification, conflict set, v1 meaning, and amendment map.
Approval authorizes the documentation amendments in section 7.1 items 2–6 only. It does not
authorize section 7.2 runtime work or a `docs/phase-0.md` execution amendment.
