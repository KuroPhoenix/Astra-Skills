# Astra Report — phase-0 design

**Date:** 2026-08-12; amended 2026-08-13, 2026-08-17, 2026-08-19, and 2026-08-20

**Status:** Proposed phase-0 design approved for implementation planning; trigger-surface,
producer-contract, source-ledger, and research-to-design reconciliation are complete. Runtime
implementation and retirement gates remain pending. Records three user decisions of 2026-08-12
(existence, MVP boundary, delegated voice), the same-day design-review resolutions (output-only
voice, `I(reporting)` typing, deferred generated-format adapters), the approved source-slice
statement in 4.2, the later-corrected 2026-08-13 disclosure and interaction decisions,
and the 2026-08-17 decisions that Report applies implicitly to reportable agent output, exposes
producer-owned progress through host-native indicators when available, organizes read-only
delivery of producer-created text/code artifacts, and reaches interface-complete v1 before public
promotion. The eight blocking review findings and the method-canon audit corrections are applied.
The 2026-08-19 through 2026-08-20 stance-bearing mediation amendment in section 15 records the
approved constitutional choices and their reconciled peer contracts; exact runtime schemas,
storage mechanics, and implementation remain deferred.
The research reconciliation is
`docs/research/2026-08-17-astra-report-research-to-design-reconciliation.md`. The earlier
Spec-approval implementation plan remains useful only as a conformance tranche and is
non-executable as the public milestone. The proposed replacement plan is
`docs/superpowers/plans/2026-08-17-astra-report-v1.md`; it grants no runtime authority. Creates
prose only: no runtime skill, harness,
installation, retirement, push, or PR.

**Proposed public shape:** `astra-report` — the stack's single rich reporting and bounded-feedback
surface.
It is a seventh user-facing entry point but not a seventh lifecycle authority. The roster
formula this design proposes is **six authorities, one voice**.

Astra Report renders the six authoritative artifacts — Finding Set, Understanding Report,
Approved Change Specification, Approved Delivery Roadmap and Execution Ledger, Test Evidence
Packet, Publication Record — and typed producer-owned progress, results, blockers, decisions, and
deliverables into attention-managed communication for the user and returns only confirmed,
attributed user feedback through the review-only path defined here. A non-lifecycle producer gains
no lifecycle authority by using Report. Report owns presentation and its bounded communication
record; it never owns what is true, what is required, what work state exists, or what is approved.
Its two outputs are the ephemeral
**Reader Brief** and the bounded, append-only **Report Artifact**; neither is an authoritative
chain artifact in the 7.11.3 sense.

## 1. Identity and status

**Provisional name:** `astra-report`. **Status:** `proposed`. **Priority:** `now` — justified
by explicit personal value: the user's own 2026-08-12 problem statement (2.1) and three
same-day decisions drove this design; there is no usage evidence yet because the job is new.
**Candidate neighborhoods investigated:** Docs & knowledge (`cm-docs-and-knowledge`); Design &
visual is touched only through the deferred post-v1 `diagram` adapter
(`cm-design-and-visual-21`).
**User job:** When an agent has progress, a result, a blocker, a decision, or a deliverable to
report—or when I need to resume a project—I receive one budgeted, inspectable brief that shows
what matters now and keeps every consequential detail reachable. **Personal value:** explicit —
quoted user statements, not inference.

### 1.1 Recorded user decisions (2026-08-12 through 2026-08-20)

1. **Existence.** `astra-report` is approved as a user-facing reporting skill alongside the
   six-skill coding lifecycle. It holds no lifecycle authority.
2. **Original MVP boundary.** The approved 2026-08-12 scope was: a stateless Reader Brief renderer; one durable
   per-project Exposure Ledger; and reporting hooks on the six artifact contracts. Explicitly
   excluded: recall modeling, cross-project attention scheduling, proactive or self-triggered
   reporting, visual reporting, personalization beyond a verbosity mode, and summarization of
   conversation rather than artifacts. Decisions 7–9 later widen producer ingress, host-native
   rendering, and existing-deliverable presentation without admitting the rejected cognition,
   scheduling, notification, orchestration, or generated-visual jobs.
3. **Delegated voice.** The six skills cease direct user-facing reporting. All human-facing
   reporting output of the six is delegated downstream to `astra-report`. The user's words:
   "the six skills should not be user-facing; all reports should be delegated to astra report.
   So astra report should be the downstream of all the six skills."
4. **Consolidated Standard delivery.** Standard normally presents the governing outcome and all
   top-level report topics in one structured textual response. It does not require one
   topic-selection turn per section. Evidence and audit depth remain addressable by stable
   references; Deep exposes that depth deliberately. This corrects the earlier staged
   Capsule/NOW/detail-menu model, which was not a user-specified report model.
5. **Conditional five-function topic route.** When one report contains several comparable
   explanatory or decision topics, each topic normally covers `TOPIC`, `MOTIVATION`, `WHAT IS
   IT?`, `IMPACT`, and `ACTION`. These are semantic functions, not five mandatory printed
   headings: Report may merge redundant functions, omit an explicitly inapplicable one, and move
   `ACTION` first for a producer-marked blocker or live decision. Different report jobs use
   structures that fit their material. A topic heading identifies the represented principal and
   communicates the producer's governing point rather than only a category name.
6. **Safe continuation and commitment.** Ordinary reporting needs no generic `Understood,
   proceed` choice. A continuation control appears only when it has a concrete, bounded
   consequence, which its description states exactly. It may return control inside an
   already-authorized workflow; it never approves a decision, grants a new effect, or starts the
   next public lifecycle skill. Genuine producer decisions and feedback confirmation use a
   decision panel with exact labels and consequences.
7. **Implicit outbound reporting.** Report is invoked implicitly whenever a cooperating agent
   emits a reportable outbound event: progress, result, blocker/failure, decision request,
   deliverable presentation, or status/resumption. Ordinary intake, clarification, brainstorming,
   teaching, and conversational explanation remain direct unless they produce such an event.
   Report is the reporting layer, not the entire conversational interface.
8. **Progress indicators.** When the host exposes native step/progress indicators, Report uses
   them to direct attention. Work state remains producer-owned and is distinct from Report's
   disclosure state. Hosts without the affordance receive the same ordered steps and states as
   text.
9. **Interface-complete first milestone.** The first publicly promoted Report runtime must cover
   representative progress, result, blocker/failure, decision, artifact/deliverable, code/diff,
   resumption, degradation, and host-fallback cases through one interface. Content-specific
   slices remain internal conformance tranches and cannot define the public skill's identity.
10. **Attributed stance-bearing guidance.** Non-authoritative does not mean neutral. When Report
    presents a producer's case, it represents that producer's recorded position and may guide the
    user through its conclusion, reasons, impact, and requested action. It may not invent or
    strengthen the producer's recommendation, suppress material contrary content, or optimize for
    agreement at the expense of an informed decision.
11. **Explicit principal alternation.** A stance-bearing block has one top-level represented
    principal: the producer while presenting its case, the user while recording confirmed
    feedback, or Report only for procedural reporting facts. A response may contain several such
    blocks, but a principal change must start a separately labelled block. Quoted and referenced
    positions may remain nested inside it.
12. **Bounded feedback return.** Report may capture and package confirmed user feedback in the
    active Report Artifact, then circulate that pinned artifact through the relevant lifecycle
    skills in canonical order under decision 17. Capture, send, receipt, producer response,
    disposition, and lifecycle effect remain separate. The review circulation may request a
    bounded annotation response; it never starts the producer's public workflow, applies the
    feedback, reopens an authoritative artifact, or advances the lifecycle.
13. **Confirmation-gated feedback polish.** Typed feedback is an ephemeral draft. Report may
    propose clearer wording, but one decision panel lets the user confirm the polish, send the
    original, edit, or cancel. Only the final confirmed wording becomes one durable feedback
    record. Interpretive changes to approval, policy, requirement, waiver, scope, or effect are
    never adopted without confirmation.
14. **Bounded stance-bearing Report Artifact.** One internal Report Artifact represents one
    reviewable subject or review cycle across its report sessions and source revisions. It holds
    the attributed producer case, confirmed user positions, Report-owned review/delivery facts,
    and links to producer dispositions. Exposure bookkeeping is one component of this exchange,
    not a per-project cognition or conversation ledger.
15. **Low-dialogue review.** Report tracks revelation and confirmed feedback without asking the
    user to certify every section. Optional unreviewed material may remain visibly deferred. One
    consolidated panel appears only when an actual decision or feedback wording must be
    committed; per-section review prompts and acknowledgements are forbidden by default.
16. **Paired directional relations.** `I(reporting)` remains the producer-to-user presentation
    relation. Final user-confirmed feedback returns through a separate `F(feedback)` relation so
    the change of represented principal and authority is explicit. `F(feedback)` permits only the
    bounded review circulation and response in decision 17; it cannot start substantive work or
    interpret, accept, apply, or give lifecycle effect to feedback.
17. **Sequential skill-annotation round.** After one user confirmation, Report pins the annotated
    Report Artifact and circulates it through Understand Code, Critique, Spec, Implement, Test,
    and Ship in that order, limited to skills represented by owned sections. A skill contributes
    only attributed responses to its own sections. If all of a skill's current-revision sections
    are user-approved and carry no unresolved comment, condition, rejection, or change request,
    Report skips that skill's response work but still delivers or exposes the approval event for
    authoritative recording. After the round, Report presents the consolidated skill-annotated
    Report Artifact. No participant may rewrite the user's annotations or another skill's entry.
18. **Sole writer, distributed authorship.** Report is the sole physical writer of the Report
    Artifact. Each skill authors an immutable, attributed response for its owned sections; Report
    appends that response without paraphrasing, strengthening, or merging it. The skill retains
    semantic ownership, Report retains storage and ordering integrity, and corrections use a new
    attributed supersession event rather than editing prior text.
19. **Response-only skill annotations.** A skill's circulation response may state that the user's
    annotation is accepted, partially accepted, rejected, awaiting clarification, deferred, or
    outside that skill's authority; give its rationale and evidence; and state whether a new
    authoritative revision or separate lifecycle operation is required. The response cannot
    rewrite the reported section, mutate a source artifact, or perform the requested work during
    circulation. Any substantive change proceeds through the normal lifecycle and produces a new
    producer-owned revision, which Report may later reference and report.
20. **One-pass termination.** One confirmed feedback batch authorizes at most one canonical
    `F(feedback)` pass. Each represented skill receives at most one response opportunity in that
    pass; an annotation, clarification request, rejection, deferral, delivery failure, or later
    producer revision cannot recursively start another pass. Report presents the consolidated
    artifact and stops. Only a new or amended user-confirmed feedback batch may begin another
    round, and unchanged resolved sections remain skipped.
21. **Pinned-round revision policy.** Every circulation response remains bound to the source
    revision confirmed at the start of its round. If a producer publishes a newer revision while
    the pass is in flight, Report finishes the pass against the pinned snapshot, flags the newer
    revision and its affected sections as unreviewed, and includes that state in the consolidated
    artifact. It never switches sources, rewrites prior annotations, aborts, or restarts the pass
    automatically. Reviewing the newer revision requires a new user-confirmed round.
22. **Dual-record approval.** A confirmed user approval in the Report Artifact is immediately
    authoritative evidence of the user's decision for its exact target and pinned revision. It is
    not producer-owned approval state and gives Report no lifecycle authority. The owning skill
    later validates and records the decision through its normal authoritative mechanism; until
    then the user-facing section remains `AP` while the owning skill's visibly separate recording
    section remains `UR`. A cleanly approved section requires no skill annotation response, while
    delivery and receipt remain separate communication facts.
23. **Attributed handoff, separate invocation.** When a skill response says that follow-on
    lifecycle work is required, Report presents an attributed `ACTION` naming the responsible
    skill, the exact producer-requested operation, and its source response, then stops. The user
    must invoke that skill separately to authorize work. Report cannot embed a control whose
    confirmation starts the operation, treat a generic continuation as authority, or convert the
    annotation round into a lifecycle handoff.
24. **Separate state axes, compact actor-scoped projection.** The Report Artifact keeps review or
    revelation, user position, delivery or receipt, producer disposition, and lifecycle effect as
    separate facts. Every visibly attributed user- or skill-facing section normally shows exactly
    one marker—`UR`, `RV`, `CM`, `RJ`, `AP`, or `DF`—for that section's designated actor. The
    marker is a display projection, not stored authority state. The labels are an Astra product
    default, not a research-established vocabulary.
25. **Explicit-only review.** Only an explicit act by a section's designated actor may create an
    `RV` review event. Opening, revealing, scrolling, or receiving a section records exposure at
    most; it never establishes review. Report does not solicit review confirmation section by
    section. In a user-facing section, `CM`, `RJ`, `AP`, and `DF` already record a stronger
    explicit user position and therefore take precedence over `RV`.
26. **One event, multiple stable targets.** One confirmed feedback event may reference several
    section, claim, evidence, option, or artifact IDs and therefore several mechanically identified
    owners. Report preserves one final wording, sends it to each owner, and records separate
    transport facts without duplicating the user event. Each skill may respond only to its owned
    targets. When stable references do not determine the owner set, Report asks once before
    confirmation and logging; it never infers recipients from the feedback prose.
27. **Attributed conflict, no synthetic verdict.** Incompatible skill annotations become one
    elevated `CONFLICT` surface containing each position, principal, source response, and evidence.
    Report neither merges the positions, counts votes, nor grants precedence to canonical order.
    Its `ACTION` names the decision authority already established by the source contracts—normally
    the user for policy or trade-offs and the relevant skill for its technical record. If authority
    itself is unresolved, Report says so rather than selecting a winner.
28. **Role-local `UR`; continue on missing response.** User-facing report sections and
    skill-facing annotation or recording sections are visibly distinct. If a skill is unavailable
    or its delivery fails, only that skill-facing section remains `UR`; an existing user-facing
    `AP`, `CM`, `RJ`, or `DF` marker is unchanged. Report records the transport fact internally,
    continues the one-pass round through the remaining skills, performs no automatic retry, and
    never treats the missing response as approval or lack of objection. No extra visible delivery
    state or suffix is introduced.

These are recorded decisions in the sense of the 2026-08-12 lock convention: they fix design
direction, and they revise two locked claims — the exactly-six public roster in
`docs/design-requirements.md` section 7.11 and the "public interface remains exactly six
skills" statement in `docs/six-skill-source-absorption.md` section 1. Section 12.4 lists the
coordinator reconciliation this requires. Nothing here claims behavioral absorption or
retirement of any source.

### 1.2 Interpretation resolved

**2026-08-19 amendment.** The output-only resolution below is retained as historical context but
is superseded, for feedback about a bounded Report Artifact, by decisions 10–28 and section 15.
Ordinary skill intake and unrelated conversation remain direct; the amendment does not make
Report a general input mediator.

Decisions 3 and 7 operate in the **output direction only** — resolved by the user's design reviews
of 2026-08-12 and 2026-08-17 (**Observed**). The six remain directly invocable control surfaces
and own their intake dialogue and approval records; other producers retain ownership of their
work state and deliverables; Report is the sole rich outbound presentation surface.
The earlier phrase "not user-facing" is recorded as imprecise shorthand for exactly that
split. What moves to Report is the skill-to-user direction — artifact presentation, status,
progress, approval requests, and failure announcements. Input mediation was considered and
rejected: it would make Report an orchestrator, contradicting recorded decision 2 and section
6.8, and would require a different architecture.

### 1.3 Phase-0 scope

This document specifies interface, authority, artifacts, contracts, validation obligations,
and provenance. Exact prompts, `SKILL.md` frontmatter, tool declarations, ledger file format,
packaging, and tuning are later-phase work.

## 2. Problem authority and vocabulary

### 2.1 The problem

**Observed (user statement, 2026-08-12).** The user reports that current AI responses
overwhelm even when correct: too much information at once, too many terms introduced
simultaneously, many sections per response, repeated summaries, weak prioritization, detail
before motivation, several simultaneous recommendations and questions, and poor support for
returning to a project after working elsewhere. The user works across several parallel
projects and loses their own context even when the model retains its context.

Two named failure modes anchor the design:

- **Reply-surface overload.** A response can be short and still costly if it opens many
  independent conversational branches at once; the model transfers conversation scheduling
  to the user.
- **Unmanaged human context.** Existing systems engineer the model's context (this ecosystem
  ships `context-save` and `context-restore` for the *agent*) but nothing manages the
  *human's* context: what the user has seen, what changed since, and what decision is now
  live.

The six-skill stack sharpens both failures by design: its artifacts are deliberately
evidence-dense, complete, and provenance-heavy. A Finding Set must never drop a finding to be
readable. The record and the communication therefore must separate; no lifecycle skill can own
human-facing rendering without corrupting its own artifact discipline.

### 2.2 Vocabulary

| Term | Definition |
|---|---|
| **Reply surface** | An independent claim, recommendation, concern, question, or decision that reasonably invites its own user response. The unit of interaction cost; the budgeted quantity |
| **State delta** | Within one active Report Artifact, the difference between the source revision previously revealed for that reported subject and its current source revision, expressed as change → consequence → next decision; it is not a session-wide or project-wide memory model |
| **Context orientation** | The minimal fresh opening needed to identify the reported subject, its governing goal or stage, and the source revision under review; used when resumption or interpretation requires it, not as a mandatory miniature project summary |
| **Attention budget** | Report's explicit allocation of simultaneous reply surfaces and explanatory detail. It prioritizes producer-marked blockers and consequential decisions, but no exact numeric limit is treated as a cognitive law |
| **Attention escalation** | The rule deciding when an item must surface regardless of brevity preference: blocking user decisions and their complete decision semantics always appear in the initial report or decision panel |
| **Topic section** | One addressable top-level matter in a report, with a stable ID, an attributed informative heading, producer-supported semantics, and linked evidence; comparable multi-topic reports normally use the five-function route in decision 5 |
| **Visible status marker** | A compact actor-scoped section-heading projection: `UR` (unreviewed), `RV` (explicitly reviewed), `CM` (commented), `RJ` (rejected), `AP` (approved), or `DF` (deferred). The heading identifies whether the section belongs to the user or a named skill; one actor's marker never overwrites another's, and no separate delivery badge is added |
| **Conflict surface** | One elevated, non-synthetic comparison of incompatible attributed positions, their source responses and evidence, plus the already-established decision authority or an explicit authority gap; it is never a vote or Report verdict |
| **Evidence expansion** | Evidence-grade material requested after or alongside a consolidated report. It is addressable by stable references and does not require a structured-choice outline or one conversational turn per topic |
| **Brief segment** | One receipt-bearing Report delivery: normally one consolidated Skim, Standard, or Deep response, or a later evidence expansion, decision panel, or confirmed-feedback result |
| **Exposure record** | The disclosure-history component of one bounded Report Artifact: what exact rendered material was receipt-confirmed as shown, against which subject and source revision; it is not a per-project cognition ledger |
| **Reader Brief** | Report's ephemeral, attributed presentation of one bounded subject. Standard normally contains one governing outcome plus its top-level topic sections in a consolidated response; evidence depth remains separately addressable |
| **Report Artifact** | Report's durable, append-only communication record for one reviewable subject or review cycle: source and render identities, attributed producer case, disclosure/review facts, confirmed user feedback, delivery facts, and links to producer dispositions |
| **Reportable outbound event** | A producer-owned progress, result, blocker/failure, decision-request, deliverable, or status event that should cross Report before rich presentation to the user |
| **ReportPacket** | The producer-neutral semantic envelope for a reportable outbound event. It preserves producer identity, provenance class, stable source references, surfaces, decisions, progress, deliverables, and evidence; it is not an authoritative artifact |
| **Progress spine** | An ordered view of producer-owned work steps and their states, rendered through native host indicators when available and equivalent text otherwise |
| **Work state** | Producer-owned task state: `pending`, `active`, `completed`, `blocked`, or `failed`; Report may render but never infer or mutate it |
| **Disclosure state** | Report-owned exposure level: content is not shown, previewed, or opened in a receipt-confirmed segment; it never implies work completion or comprehension |
| **Deliverable descriptor** | A stable producer-owned reference to an already-created report, Markdown file, code change, diff, or other output, with provenance, location, outcome, caveats, and evidence links sufficient for faithful delivery |

### 2.3 Reporting model

The audience model is **a competent CEO for pacing, a reviewer for depth**. Pacing: asymmetric
attention, decisions first, what-changed framing, drill-down on demand, no dumbing down. Two
deviations from the plain executive-reporting genre are load-bearing:

- In this stack the user is not merely informed; the user is the **only approval authority**.
  A brief is a decision brief whose first job is to tee up the next approval cleanly.
- Supervising code sometimes requires **audit**, not trust: reviewing evidence before a merge
  is the user's job. Drill-down must therefore be evidence-grade, which the 7.11.3
  traceability chain supplies by stable identifiers.

### 2.4 Rejected concept: recall modeling

A `user_attention_state` with estimated recall likelihoods was considered and **rejected**.
The boundary is recorded versus inferred state: exposure ("finding F-12 was shown on
2026-08-12") is a fact; recall ("the user probably remembers the provider abstraction") is a
guess about a mind, and a wrong guess fails silently by omitting exactly what the user forgot
— the worst failure mode a reporting layer can have. With exposure facts, the safe rule
"anything changed since last shown gets shown" needs no psychology. Production precedent:
GitHub's stable file-view feature maintains per-viewer viewed state and invalidates it when the
file changes; that is an analogy for change invalidation, not proof of reading, understanding,
approval, or durable artifact exposure. The more exact "commits since last review" selector is
public-preview evidence only. A later time-decay re-glossing heuristic is admissible because its
worst case is one redundant sentence (section 12.2).

## 3. Interface and scope

### 3.1 Small public interface

One invocation with a scope and an optional mode:

```text
astra-report [scope] [--mode skim|standard|deep]
```

Scope is one artifact, a set of artifacts, or a project (meaning: the current artifact chain).
It may also be one or more stable producer deliverables. Default scope is the active project;
default mode is `standard`. The same rendering core is consumed by the six skills at their
reporting moments through the typed `I(reporting)` relation and by other cooperating producers
through the ReportPacket profile in section 8.8.

Standard presents the report's top-level topics together. A later evidence request may identify a
stable topic, claim, or evidence reference; `deep` requests full audit depth. Structured controls
are reserved for genuine producer decisions and confirmation of polished user feedback, with a
content-equivalent text fallback. None of these interactions is a new lifecycle invocation.

### 3.2 Requests that should trigger it

- "Where are we?", "what changed?", "catch me up", after any absence — resumption brief.
- "Report on X", "explain this Finding Set / spec / test results to me" — artifact brief.
- "What do you need from me?", "what's blocking?" — open-decision brief.
- Any of the six skills reaching a reporting moment (section 8.3) — delegated rendering.
- Any cooperating agent emitting typed progress, result, blocker/failure, decision-request,
  deliverable, or status output (section 8.8) — implicit outbound rendering.
- Delivery of an already-created report, Markdown file, code change, diff, or comparable stable
  output — deliverable brief. The producer, not Report, owns the output and its claims.

### 3.3 Nearby requests that should not trigger it

- "Explain how this code works" — `astra-understand-code` owns repository state; Report owns
  artifact state.
- "Write documentation for this feature" — durable repository prose belongs to Implement
  (`document-release` disposition); standalone documentation remains the locked five-source
  deferral.
- "Summarize our conversation" — out of scope by recorded decision 2; Report reads artifacts,
  deliverables, and typed producer packets, not arbitrary chat history.
- "Is this finding correct?", "which artifact is right?" — judgment belongs to Critique;
  Report surfaces contradictions and never adjudicates them.
- Deployment changelogs, retros, meeting notes, internal communications with their own durable
  outputs — separate jobs outside the coding stack (absorption design section 8).

### 3.4 Intake contract

| Input | Requirement |
|---|---|
| Artifact scope | Immutable references (identity, revision, hash per 7.11.3) to one or more chain artifacts; sideways reads into peer working files are forbidden |
| Deliverable scope | Stable producer-owned descriptor for an already-created output; revision/hash may be absent only with explicit full-current/no-delta degradation |
| Mode | `skim`, `standard` (default), or `deep` |
| Report Artifact | Read when the request resumes a bounded reported subject; absence degrades to full-current rendering without fabricating prior revelation or review |
| Interaction capability | Optional host declaration for decision-panel and native progress support plus relevant limits; absence selects content-equivalent text fallbacks and changes no content or authority |
| Direct request | The user's scope and mode plus resolved authoritative artifact or stable deliverable references; no producer event is required or fabricated |
| Lifecycle payload | At an `I(reporting)` moment: the producing skill's `astra.report-event/v0` envelope (sections 8.3–8.4), normalized without authority loss |
| General delegated payload | At another reportable outbound event: the producer-owned ReportPacket semantic fields in 8.8 |
| Progress | Ordered producer-owned step IDs, labels, and work states; Report supplies no missing state and keeps disclosure state separate |
| Deliverables | Zero or more producer-owned descriptors; Report may present, preview, excerpt, and link them but cannot author or mutate them |

The input profiles do not create additional authority paths. On a direct request, Report may
render only facts, consequences, and open decisions already recorded in the resolved artifacts or
stable producer deliverables and their canonical reporting hooks. If a hook is absent, Report
names the gap and uses exact artifact excerpts or line anchors; it never constructs a producer
outcome, consequence, open decision, work state, or event. A direct approval brief is therefore
possible only when the authoritative artifact already carries the complete common open-decision
shape. Otherwise Report explains the artifact and identifies the producer-owned missing decision
contract. A non-lifecycle packet remains producer-owned evidence and never becomes a lifecycle
artifact merely because Report rendered it.

### 3.5 User-visible result

A Reader Brief (section 7.2), normally delivered as one consolidated Standard response. A host may
render producer-owned progress through native indicators, actual decisions and feedback
confirmation through a decision panel, and deliverables through links or attachments; each has a
content-equivalent text fallback. Receipt-confirmed presentation facts and final confirmed user
feedback may be appended to the bounded Report Artifact (section 15.4); drafts are not logged.
Report creates no producer deliverable or lifecycle effect.

### 3.6 Effect authority and non-goals

Report is **read-only over the lifecycle**. It never: approves, rejects, or waives anything;
reinterprets, re-grades, repairs, or re-prioritizes a source skill's severity or consequence
judgment; invents or changes a producer's work state; mutates any chain artifact, deliverable, or
repository file; hides disagreement between sources; starts, schedules, or interrupts any
workflow; ranks anything outside the scope it was invoked on; or communicates across projects.
Its only durable effects are append-only Report-jurisdiction communication records: exact
presentation/delivery facts and final user-confirmed feedback bound to one Report Artifact. It
cannot autonomously alter a user response. A confirmed approval is authoritative evidence of the
user's decision for its pinned target, but these records are never producer-owned approval or
lifecycle state (sections 15.3–15.4). Format
conversion, generated visual reporting, and dashboard authorship are post-v1 non-goals (section
4.3). Presenting an existing text/code deliverable or using host-native controls is in v1 and
creates no file-writing authority.

### 3.7 Decisions that remain with the user

- Answering every decision a brief presents; Report only presents.
- Mode selection.
- Vetoing any deferral ("show me what you parked").
- Opening a Critique cycle on a surfaced contradiction (user-mediated; never automatic).
- Changing the surface-budget defaults, the method-reference canon, or this design's boundary.

## 4. Source evidence and proposed allocations

### 4.1 Occurrence inspection record

All rows inspected 2026-08-12 at their live paths; hashes are sha256 over the entry bytes
(first 12 hex digits, house style); the same-day design review independently verified all
eight entry hashes against live bytes. All statements from these sources below are
**Observed** unless labeled otherwise. Live paths as in the first column of 4.1.2 conventions:
`/doc` at `~/.claude/commands/doc.md`; skills at `~/.claude/skills/<name>/SKILL.md`; gstack
entries under `~/.claude/skills/gstack/`.

| Occurrence | Identifier | Type | Invocation | Declaration | Lines; entry hash | Availability |
|---|---|---|---|---|---|---|
| `cm-docs-and-knowledge-03` | `/doc` | command | `/doc [file_path_or_topic]` | frontmatter: description, argument-hint, allowed-tools | 199; `684db9d1ef2e` | Live |
| `cm-docs-and-knowledge-02` | `doc-coauthoring` | skill | model-invoked on doc/proposal/spec co-writing | frontmatter: name, description | 375; `2e47d78846fa` | Live |
| `cm-docs-and-knowledge-05` | `internal-comms` | skill | model-invoked on internal-communication requests | frontmatter: name, description | 32; `067b7587a344` | Live; four example files are the supporting body (4.1.2) |
| `cm-docs-and-knowledge-01` | `document-generate` | skill | `/document-generate` (gstack) | frontmatter: name, preamble-tier, version, description | 1252; `3d97c417c753` | Live; generated gstack file (4.1.2) |
| `cm-docs-and-knowledge-07` | `teach` | skill | `/teach` only (`disable-model-invocation: true`) | frontmatter: name, description, disable-model-invocation, argument-hint | 140; `6d2dbe5e0308` | Live |
| `cm-docs-and-knowledge-09` | `rtfm` | skill | model-invoked for OpenAPI documentation from code | frontmatter: name, effort, description | 360; `909197c58116` | Live |
| `cm-docs-and-knowledge-04` | `make-pdf` | skill | `/make-pdf` (gstack) | gstack generated frontmatter | 787; `7c00be6908b4` | Live; generated gstack file (4.1.2) |
| `cm-design-and-visual-21` | `diagram` | skill | `/diagram` (gstack) | gstack generated frontmatter | 923; `f57f8722f566` | Live; generated gstack file (4.1.2); row already claimed (4.5) |

#### 4.1.1 Behavior anchors for the claimed slices

Line anchors are valid at the recorded hashes and regenerate on any hash mismatch
(`docs/design-requirements.md` 4.2).

| Source | Slice basis (line anchors) |
|---|---|
| `/doc` | Stripe-register role and anti-slop mandate (9); anti-AI-slop scan — L1 vocabulary (70), L2 burstiness and confidence arcs (100–109), L3 structure (112); fresh-reader test (135); audience context gathering (27) |
| `doc-coauthoring` | Three-stage protocol (18–26); Stage 1 context gathering (28); Stage 2 section-by-section refinement (104, 154–162); Stage 3 fresh-reader testing (22) |
| `internal-comms` | When-to-use jurisdiction (7); style guidance and example routing (17); the format shapes live in the four example bodies (4.1.2) |
| `document-generate` | Diátaxis quadrant split with explanation as understanding-oriented "why" (authored template 7, 44–49); quadrant partitioning table (template 119–125) |
| `teach` | Working-memory-bounded lessons (53, 97); zone of proximal development (81); fluency versus storage strength (34) |
| `rtfm` | Consumer perspective (30); when-and-why over how-implemented (32); consumer three-questions gate (183); untested-endpoint uncertainty disclosure (344) |

#### 4.1.2 Supporting and authored bodies

`internal-comms` examples, inspected and hashed 2026-08-12: `3p-updates.md` 46;
`087e4363c0f3` · `company-newsletter.md` 65; `30f81cfbdb03` · `faq-answers.md` 29;
`5ecd3356cd66` · `general-comms.md` 15; `4d3a4bb198a7`.

`document-generate`, `make-pdf`, and `diagram` are **generated gstack files**. Per the
roadmap's generated-source rule, the authored templates are the analytical basis; generated
bytes remain runtime-fidelity evidence only and cannot be the sole source oracle. Authored
templates at gstack revision `a3259400a366593e0c909dd9ac3e59752efd2488`, release `1.60.1.0`
(re-verified live 2026-08-12): `document-generate/SKILL.md.tmpl` 460; `83ce891719d1` ·
`make-pdf/SKILL.md.tmpl` 247; `bb2f5917607b` · `diagram/SKILL.md.tmpl` 150; `3b77cc15652e`.

**Evidence gap:** the consumed resolver/section templates and the generator registration have
not been inspected. For `document-generate` that inspection must close before its slice row
can resolve; for the two post-v1 generated-format adapters it is deferred to adapter admission
(4.3).

### 4.2 Slice dispositions and the documentation deferral

No source below is proposed for absorption or retirement. Each keeps its independent
registration and its own primary job. Report claims **playbook and perspective slices only**;
the absorption three-part test fails at the problem axis for every one of them (their user
jobs are authoring, coaching, or teaching — not rendering immutable lifecycle artifacts).

| Source | Slice Report internalizes | Contribution class | Remainder that stays with the source |
|---|---|---|---|
| `/doc` | Plain-language and anti-slop checks, audience targeting, fresh-reader test | Playbook | Authoring and editing durable documents |
| `doc-coauthoring` | Section-by-section chunking, reader-question verification | Playbook | Co-authoring proposals and specs with the user |
| `internal-comms` | Status, leadership-update, and FAQ register shapes | Playbook, reference | Company communications with durable outputs |
| `document-generate` | Explanation-quadrant structure: understanding-oriented "why it is this way" | Playbook | Tutorials, references, how-tos, repository files |
| `teach` | Working-memory-aware chunk sizing, progressive explanation | Playbook, perspective | Curricula, lessons, exercises, learning records |
| `rtfm` | Consumer perspective, "when and why" framing, uncertainty disclosure | Perspective | Reading implementations and mutating API docs |

**Approved deferral-lock exception.** `/doc`, `document-generate`, and `rtfm` are three of the five
standalone repository-documentation candidates whose deferral the user locked on 2026-08-12:
"no surviving design may claim one as a primary or secondary home without a new recorded user
decision" (absorption design section 8). On 2026-08-12 the user approved the following exact,
narrow exception:

> Approve `astra-report` as a secondary consumer of only the recorded playbook/perspective
> slices from `/doc`, `document-generate`, and `rtfm`. Their primary jobs and registrations
> remain independent; they do not join the 92 target, become wholly absorbed, retire, or
> decide the separate docs-only-cycle question.

That decision authorizes the three existing collision rows to move from `unclaimed` to
`claimed` with Report's exact secondary roles in 4.5. It does not move them into the 92 target,
resolve a row, transfer a primary job, authorize whole-source absorption or retirement, or
settle the separate docs-only-cycle question. Report claims no source as a primary home.

### 4.3 Host delivery and deferred generated-format adapters

Conversation-host adapters for decision/confirmation panels, progress indicators, links/attachments, and
their text fallbacks are part of v1 because they render the same Reader Brief semantics without
creating files. An already-created report, Markdown file, code change, or diff may be presented
through a stable deliverable descriptor; this is output organization, not format conversion or
artifact authorship.

`make-pdf` and `diagram` remain **excluded from v1**. Neither is absorbed behavior; both remain
independently registered gstack skills. If later admitted: `make-pdf` may re-issue an existing
brief without content change; `diagram` is **supplemental only, never an equivalent rendering** —
the live skill produces editable repository artifacts (Mermaid, Excalidraw, SVG, PNG) and cannot
preserve a prose brief, so its file-writing effect requires explicit authority treatment before
admission. Admission also requires the deferred resolver/registration inspection (4.1.2) and, for
`diagram`, a coordinator amendment to its already-claimed row (4.5).

### 4.4 Method references: the distilled canon

Books and research enter this design as **method references** — the same class as
`prototype/LOGIC.md` and `UX_PRINCIPLES` in `astra-product-design.md` — never as census
sources: they have no invocable identifier, no entry hash in the source inventory sense, no
I/O contract, and no retirement gate. Distillation records principles with attribution;
**no source expression is reproduced**. Each reference earns its row only through checkable
rules bound to a brief obligation. The future self-contained skill must carry those distilled
rules and provenance; hidden model recall is not a reproducible dependency. The complete audit,
including local-byte hashes, locators, transfer limits, and rejected attributions, is
[`docs/research/2026-08-12-astra-report-method-canon.md`](../docs/research/2026-08-12-astra-report-method-canon.md).

| Reference | Governs | Distilled into (examples of checkable rules) |
|---|---|---|
| Minto, *The Pyramid Principle* | Brief skeleton | Lead with the governing answer; use recorded context and tension to orient a Change Story. Before → problem → fix → after is an Astra synthesis, not SCQA |
| Rogers & Lasky-Fink, *Writing for Busy Readers* | Surface economy | Fewer ideas, not merely fewer words; important information findable in one glance; action effort minimized |
| Redish, *Letting Go of the Words* | Layering | Key message first with meaningful, scannable topics and optional evidence depth; consolidated action-completeness is Astra's stronger contract |
| Mayer/Fiorella and Clark/Mayer | Chunk discipline | Multimedia segmenting, signaling, coherence, and pre-training motivate testable prose transfers: meaningful chunks, visible structure, removal of renderer-authored extraneous detail, and necessary first-use glosses. They do not prove one-idea chunks or a one-summary rule |
| Williams, *Style: Lessons in Clarity and Grace* | Sentence mechanics | Actors as subjects, actions as verbs; old-before-new information flow. (Douglas, *Writing for the Reader's Brain*, folds into this slot as the evidence-based alternate) |
| Diátaxis (Procida) | Explanation boundary | Apply context, reasons, implications, and alternatives where explanation is needed; action-facing decisions and approvals are not long explanatory essays |
| Nygard, ADR practice | Decision framing | Render recorded context/forces, decision, status/supersession, and consequences; alternatives appear only when the authoritative Specification records them |
| Sweller/cognitive-load theory; Grice | Foundations | Motivate attention risk, sufficient evidence, relevance, clarity, and order; they do not supply numeric budgets or fixed layer counts |
| Altmann & Trafton; Parnin & DeLine | Resumption analogy | Stable subject/revision cues and chronological code changes motivate minimal orientation plus a bounded source delta; whether Astra's prose form helps is a validation hypothesis, not an established result |
| BLUF doctrine | System precedent | Main point or action first; it does not define Astra's layers or budgets |
| Inspected SITREP format | System precedent | Domain-specific precedent for highlighting changed state and separately escalating attention items; it is not a universal reporting grammar |
| GitHub viewed-state behavior | Product analogy | Per-viewer file state invalidated by change; never evidence of reading, understanding, approval, or durable artifact exposure |

Novelty is **not claimed** for any concept in this design; the bar is usefulness to this user.
A literature review is deferred unless publication is ever intended.

### 4.5 Exact proposed ledger changes

These are changes to **existing collision-ledger rows** under the `docs/phase-0.md` section 5
schema — not a new census tranche, and none joins the locked 92. Method references (4.4) are
design-document citations only; the schema has no row type for them and none is proposed. The
coordinator applies every change below; rows become `claimed`, never `resolved`, citing this
design's sections 4.1–4.3 as evidence.

| Occurrence | Proposed primary disposition | Primary home | Proposed secondary roles | Claim status change |
|---|---|---|---|---|
| `cm-docs-and-knowledge-02` `doc-coauthoring` | independent reference | independent | `astra-report`: chunking and fresh-reader-testing playbook slice | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-05` `internal-comms` | independent reference | independent | `astra-report`: status/leadership/FAQ register slice | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-07` `teach` | independent reference | independent | `astra-report`: working-memory chunk-sizing slice | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-04` `make-pdf` | independent reference | independent | `astra-report`: deferred post-v1 generated-format adapter (4.3) | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-03` `/doc` | independent reference | independent | `astra-report`: plain-language, audience-targeting, and fresh-reader-test slice | `unclaimed` → `claimed`; approved lock exception in 4.2 |
| `cm-docs-and-knowledge-01` `document-generate` | independent reference | independent | `astra-report`: explanation-quadrant structure slice | `unclaimed` → `claimed`; approved lock exception in 4.2; the 4.1.2 resolver gap must still close before resolution |
| `cm-docs-and-knowledge-09` `rtfm` | independent reference | independent | `astra-report`: consumer-framing and uncertainty-disclosure slice | `unclaimed` → `claimed`; approved lock exception in 4.2 |
| `cm-design-and-visual-21` `diagram` | already `claimed`: retained independent (roadmap amendment 3 §10) | independent | proposed amendment: add `astra-report` as a deferred post-v1 supplemental-delivery consumer alongside `astra-document` and `astra-interface` | stays `claimed`; amendment reconciles against the amendment-3 record |

## 5. Collision analysis

### 5.1 Why Report looked absorbable and is not

Report resembles the presentation layers scattered through the inventory: `/doc`'s clarity
rules, `internal-comms`' status formats, `landing-report`'s dashboards, each skill's final
summary. The three-part test still fails against every surviving skill: the **problem**
(explaining the artifact chain to a human under limited attention) is owned by no lifecycle
authority; the **methodology** (trace-preserving simplification, bounded source deltas,
reply-surface-aware structure) exists in no source; the **I/O** (immutable producer sources plus a
bounded Report Artifact in, non-authoritative consolidated brief plus communication-event append
out) matches no source's contract.
`landing-report` inspects version queues and stays with Ship; `context-save`/`context-restore`
serialize the *agent's* context and remain excluded — the model-context/human-context
distinction in 2.1 is exactly why they are not this job.

### 5.2 What is genuinely shared

Register and style rules are shared with `/doc` and `internal-comms`; chunking with
`doc-coauthoring` and `teach`; explanation structure with `document-generate`. That is why
they contribute slices (4.2) — and why none of them covers deltas, exposure, budgets,
escalation, or fidelity precedence, which exist only here.

### 5.3 Why this is one coherent module

Every behavior serves one job: convert authoritative artifact state into the least attention
that leaves the user correctly informed and able to act. Splitting rendering from delta
detection or from the ledger would separate functions that share one invariant set (section
6) and one output.

### 5.4 Declared positive advantage

Against the strongest applicable single source (the source oracle per case: `/doc` for prose
quality, `internal-comms` for status format, `doc-coauthoring` for chunked iteration),
combined behavior must outperform on three named task classes:

1. **Resumption after absence.** No source reconstructs minimal subject orientation plus a bounded
   state delta from receipt-backed disclosure history; every oracle re-explains or omits by
   accident.
2. **Multi-artifact overload.** Six locally-good summaries still concatenate into dozens of
   findings; no oracle ranks across artifact types under a surface budget with named deferral.
3. **Approval teeing.** No oracle renders a typed decision payload under fidelity precedence
   with evidence-grade drill-down.

If later evaluation shows no advantage on these classes, Report collapses to a style guide
consumed by the six and this design's interface is withdrawn (section 11.4).

## 6. Preserved distinctions

Each rule below names the decision on which it matters. Together they are the skill's
invariant set; a later implementation that loses any of them has failed internalization
regardless of output quality.

1. **Fidelity precedence.** `fidelity > caveat completeness > structure > concreteness >
   simplicity > brevity`. Every method reference in 4.4 optimizes persuasion and will happily
   drop caveats; this chain subordinates them all. Checkable form: a caveat may be demoted
   behind an expandable link, **never deleted**. Matters when: simplification pressure meets a
   qualified test result.
2. **Trace-preservation licenses brevity.** Report may omit aggressively only because
   everything omitted stays addressable by stable identifier. Omission without addressability
   is forbidden. Matters when: an artifact lacks the 7.11.3 identifiers (degradation, 7.6).
3. **Severity stays at source.** Consequence, severity, and blocking status are the producing
   skill's judgment; Report schedules attention under a budget and never re-grades. A grading
   conflict between artifacts is a contradiction to surface, not to resolve. Matters when: two
   skills disagree about the same fact.
4. **Decisions are never paced.** A blocking item and its complete producer-owned options,
   consequences, recommendation state, and material caveats appear in the consolidated report or
   decision panel. Supporting evidence may remain addressable, but required decision semantics
   never wait behind another reveal turn. Matters when: explanatory depth competes with a live
   decision (7.5).
5. **The brief is derived; the communication record is bounded.** A Reader Brief is a view over
   producer authority. Its bounded Report Artifact preserves exactly what Report presented and
   what the user confirmed, without becoming a second source of technical truth or a project-wide
   memory store. Matters when: a review resumes or the producer source changes.
6. **Delta-first, never delta-only.** A resumed Report Artifact identifies the standing subject,
   governing context, and reviewed source revision before presenting its structural delta. This
   restores the minimum frame without reconstructing the whole project or inferring recall.
   Matters when: a bounded artifact review resumes after a source revision.
7. **Addressable depth, not conversational scheduling.** Standard delivers all top-level report
   topics together. Evidence and audit depth stay reachable by stable reference without generic
   "want to hear more?" questions or one reveal turn per topic. Matters when: supporting detail
   exists but no additional commitment is required.
8. **No lifecycle orchestration.** Report never decides whether or when to interrupt the user,
   ranks across projects, or starts a public peer workflow. It may sequence only decision 17's
   review-only `F(feedback)` operations over one pinned Report Artifact. Matters when: a surfaced
   contradiction or requested change tempts Report to start Critique or Implement rather than
   record a response and leave lifecycle routing user- or producer-owned.
9. **Visible deferral.** DEFERRED names what was parked; silent omission is forbidden even
   below the budget line. Matters when: the user wants to veto a deferral cheaply.

## 7. Proposed skill design

### 7.1 Public shape and modes

One entry point (3.1), three modes:

- `skim` — the shortest reliable orientation: subject, governing outcome or live decision, and a
  compact indication of additional addressable material.
- `standard` — one consolidated response containing the governing outcome and all top-level
  topics needed to understand the reported subject, with stable evidence references.
- `deep` — the same coherent report with evidence-grade rationale, alternatives, excerpts, and
  trace detail expanded for deliberate audit.

Mode changes rendering depth only; it never changes what exists, what is authoritative, which
material caveats or live decisions must be visible, or what remains addressable.

### 7.2 Reader Brief contract

A Reader Brief is ordered by communicative purpose rather than one universal layer stack:

| Part | Content | Binding rules |
|---|---|---|
| **Governing line** | The producer-supported outcome, live decision, or reason for this report | Comes first unless a tiny resumption orientation is necessary to understand it; never invents significance or urgency |
| **Orientation** | Subject, producer/principal, source revision, goal or stage, and prior review point when resuming | Fresh and minimal; included only to the extent needed to interpret the report; never claims recall |
| **Top-level topics** | The matters needed to understand the reported subject | Presented together in Standard. Comparable multi-topic decision/review reports normally use the conditional five-function route below; other report jobs use their own grammar |
| **Decision panel** | A producer-owned ask, complete options and consequences, recorded recommendation state, and material caveats—or polished user feedback awaiting confirmation | Used only for a real commitment; never for outline navigation or optional detail |
| **Evidence references** | Stable claim, artifact, diff, test, or excerpt addresses | Consequential assertions remain traceable. Deep expands them; Standard need not dump every supporting record |
| **Named deferral** | Supporting material not expanded at the current depth | Its existence and stable address remain visible; no live decision, blocker, material caveat, or action-changing fact may be parked here |

For several comparable explanatory or decision topics, Report checks these semantic functions:

```text
2/5  [PRODUCER] Informative topic headline carrying the governing point
     MOTIVATION  Why this topic is live, when distinct
     WHAT IS IT? Plain explanation and exact technical term, when needed
     IMPACT      Recorded consequence, uncertainty, and caveat
     ACTION      Exact ask, decision, or producer-recorded no-action state
     Evidence    Stable source references attached compactly
```

The five named functions are not five mandatory visible headings. Report may combine adjacent
functions when they duplicate one another, omit only an explicitly inapplicable function, and
explain a necessary unfamiliar concept before a motivation that depends on it. For a
producer-marked blocker, urgent failure, or live decision, `ACTION` and its complete consequence
move first. If the producer supplies no motivation, consequence, action, or recommendation,
Report names the gap or omits the inapplicable field; it never fills the template by inference.

The topic headline must carry information scent rather than only a category: `2/5 [TEST] Retry
path remains unverified`, not merely `2/5 Testing`. Principal, source, material caveats, and
cross-topic dependencies remain visible even though they are not five additional repeated
headings. Conflicting principals receive separate attributed blocks.

Choose a job-specific grammar when the repeated route would distort the report:

- progress — ordered producer-owned state spine, stated briefly at the beginning;
- decision — ask, complete options, consequences, recommendation state, and evidence;
- blocker or failure — failed operation, boundary, consequence, and permitted next action;
- incident — current condition plus chronology and escalation;
- evidence audit — claim-to-evidence trace and gaps;
- single-answer explanation — governing point followed by only the support needed; and
- multi-topic review or decision report — the conditional five-function route.

Sentence-level rules from the canon bind every shape: actors as subjects; necessary vocabulary
explained in plain language at first use; abstract claims grounded in concrete artifacts, diffs,
tests, or numbers. All top-level topics appear in one Standard response. Later evidence requests
may address a topic or source directly, without a reveal menu or one conversational turn per
topic. This rule is the evidence-classified Astra synthesis recorded in the
[book distillation](../docs/research/2026-08-18-astra-report-book-distillation.md) and the
[five-field template audit](../docs/research/2026-08-19-astra-report-five-field-template-evidence-audit.md);
the exact labels, order, and field count are product defaults to evaluate, not research-proven
attention constants.

### 7.3 Bounded Report Artifact disclosure contract

Section 15.4 defines the broader stance-bearing Report Artifact. Its disclosure component replaces
the earlier per-project Exposure Ledger: one append-only record is bounded to one reported subject
or review cycle, not to a project, session history, or inferred user memory. A presentation event
carries, in the identity style of 7.11.3: timestamp; Report Artifact and rendered-segment identity;
exact delivered-segment hash and mode; source artifact/deliverable identities, revisions, and
hashes; top-level topic and claim IDs shown; decisions presented; and degradation flags. It may
record disclosure as `shown` or evidence depth as `expanded`; neither implies reading,
comprehension, review, agreement, or approval.

The Report Artifact is communication evidence, never lifecycle authority. The producing skill's
artifact remains the only record of technical facts, decision disposition, approval state, and
resulting lifecycle effect. Entries are never edited: an incorrect presentation, normalisation,
or delivery record is corrected through an explicit append-only correction or supersession. Only
final user-confirmed feedback is durable; typed drafts and intermediate polishing are not logged.

**Delivery receipt boundary.** "Presented" means the exact composed segment was accepted by its
delivery surface, not merely generated in memory. Report appends a presentation event only after a
caller or adapter supplies a receipt for that exact Report Artifact and segment identity. Without
such a receipt, Report still renders but does not claim exposure; the source revision remains
eligible to surface again. Safe duplication is preferable to a false disclosure record that hides
material information.

### 7.4 Rendering protocol

```text
scope and source revision -> identify producer and report job -> derive bounded prior-review delta
when applicable -> select producer-supported governing line -> group related top-level topics ->
apply the report-job grammar and attention rules -> compose one consolidated response -> deliver ->
receipt-gated Report Artifact append -> optional evidence request or real decision/feedback panel
```

Delta computation, when used, is structural and bounded to the active Report Artifact: source
revisions and supersession references against its prior disclosure/review events, never prose
diffing or whole-conversation memory. Attention allocation orders by producer-owned consequence,
blocking, dependency, and recommendation fields; Report contributes faithful wording, grouping,
ordering, and evidence depth only.

### 7.5 Attention and interaction defaults

No exact number of simultaneous topics or reply surfaces is treated as a research-established
human limit. `skim` selects the producer-marked governing outcome or most consequential live
decision and names the remaining addressable material. `standard` presents every top-level topic
needed to understand the bounded reported subject, grouping only relationships supported by the
producer. `deep` additionally expands evidence-grade detail.

Report minimizes *required interaction*, not merely words: it does not turn each topic into a
question, add optional offers, or require a reveal turn per section. Several genuine commitments
may share one decision panel only when each remains independently clear and the panel preserves
their exact consequences. Blocking decisions always bypass any brevity preference; all their
producer-owned options, consequences, recommendation state, and material caveats remain visible.
Supporting material may be compact or deferred only when it stays named and addressable.

### 7.6 Failure and degradation

| Condition | Behavior |
|---|---|
| Report Artifact missing or unreadable | Render the full current subject without a delta, state that no bounded prior-review record is available, and never fabricate previous revelation or review |
| Delivery surface supplies no receipt for the exact brief | Deliver the brief, do not append a presentation fact, and leave that source revision eligible to be presented again |
| Structured decision controls are unavailable or reject the panel shape | Render the same decision or feedback-confirmation semantics as explicit textual options with stable IDs and exact consequences |
| User requests an unknown, stale, or superseded topic/evidence reference | Do not guess; identify the current subject/source revision and regenerate the addressable topic/evidence outline |
| Artifact lacks stable identifiers | Quote verbatim with file-line anchors, flag the reporting-hook gap in DEFERRED, never invent identifiers |
| Report unavailable at a non-decision `I(reporting)` moment | The producing skill emits the degraded minimal notice of 8.5; the lifecycle never blocks on Report |
| Report unavailable at an approval request | The producing skill presents its complete minimal decision envelope (8.5) so the user can still decide informed; work stops only while awaiting the user's answer, never because Report is unavailable |
| Contradiction detected between artifacts | Surface both attributed positions and references in the consolidated report; never adjudicate; routing to Critique is user-mediated |

Report is deliberately **not** a required consultant in the 7.11.2 fail-closed sense;
rendering unavailability degrades communication, not authority.

### 7.7 Architectural hypotheses

Internal seams — scope selector, packet normalizer, bounded-delta engine, attention allocator,
composer, and Report Artifact writer — are analytical until implementation demonstrates variation. Host rendering is
a real seam because v1 requires at least native-interaction and text-fallback adapters; semantic
step states, topic IDs, decision controls, deliverables, and consequences remain identical across
them. Generated file and visual adapters remain deferred (4.3). Whether the delta engine and
allocator are separable modules or one pass remains a hypothesis for the comparison systems
(11.1).

The renderer remains a pure derivation over producer inputs plus the bounded Report Artifact. A
later evidence request or resumed review carries the current immutable source references and
relevant prior presentation/review events needed to regenerate the view. Report holds no hidden
conversation or project-wide cognition store; the Report Artifact is its only durable subject
state.

## 8. Delegated voice and return mediation: `I(reporting)`, `F(feedback)`, and producer hooks

### 8.1 Direction rule

Ordinary **user → skill** invocation, intake, and clarification remain direct. Rich reportable
information flowing **producer → user** (artifact or deliverable presentation, status, progress,
results, approval requests, blocker/failure announcements) routes through Report. Within one
bounded Report Artifact, Report may also carry final user-confirmed feedback back to a
mechanically identified producer under section 15.2. That return path preserves the user as
principal and gives Report no interpretation, disposition, invocation, or lifecycle authority.

Intake dialogue inside an active skill stays direct and obeys the exported contract rules: one
question per message; no unnecessary branches; no optional offer phrased as a question. Evidence
requests are navigation inside an active Report Artifact. Actual producer decisions and feedback
wording use separately identified decision controls; neither an evidence request nor a generic
continuation phrase can grant approval or an effect.

### 8.2 Paired reporting and feedback relations

#### 8.2.1 `I(reporting)` — producer case outbound

Rendering delegation is a **typed use of the canonical `I` relation** — consumption of a peer
capability without invoking its lifecycle judgment — not a new relation letter. A first draft
proposed a distinct `V` relation; the 2026-08-12 review found that inconsistent with `I`'s
governing definition, and `V` is withdrawn. Definition: **under `I(reporting)`, a lifecycle
skill consumes Report's rendering capability for its own authoritative content; content
authority stays with the producer; presentation authority is Report's; no determination
returns.** It is not `C` (nothing is checked against upstream authority; no
pass/drift/authority_gap) and not `H` (nothing is handed off). Report consumes the producers'
artifacts through ordinary `I` references in the opposite direction. The typing convention
needs only a clarifying note in the relation vocabulary (12.4), not a new entry.

#### 8.2.2 `F(feedback)` — bounded review circulation

`F(feedback)` is the distinct return relation for a pinned, user-confirmed Report Artifact. Report
uses it to circulate the artifact through the lifecycle skills represented by its owned sections,
in canonical order: Understand Code → Critique → Spec → Implement → Test → Ship. The outbound
feedback blocks preserve the user as principal and carry final confirmed wording, stable targets,
source revisions, earlier attributed responses in the same round, and Report-owned transport
facts; an unconfirmed draft cannot cross the relation.

A confirmed feedback event may carry several stable target references and map mechanically to
several represented skills. Every recipient receives the same final user wording, while Report
records delivery and receipt separately per recipient. The durable user event is not copied into
one apparent decision per skill, and no recipient may respond outside its owned targets.

If the returned annotations conflict, Report preserves them as one elevated `CONFLICT` surface.
Each position retains its principal, source response, rationale, and evidence. Canonical
circulation order supplies no substantive precedence, and Report may neither merge the positions
nor use majority agreement as authority. The surface names the decision owner already established
by the source contracts or exposes an unresolved authority gap.

For a skill with unresolved owned sections, the relation may request one bounded review response:
an attributed section annotation, rationale, disposition state, or link to a producer-owned
revision. The skill authors that immutable response; Report is the sole Report Artifact writer and
appends it without semantic transformation. This is a narrow communication operation, not the
skill's public lifecycle workflow. A skill whose owned sections are all user-approved at the
pinned revision performs no response work; the approval event is still delivered or made
referenceable so skipping analysis cannot erase the user's decision or prevent later producer
recording.

That response is disposition and explanation only. It may accept, partially accept, reject,
request clarification on, defer, or decline for lack of authority over the user's annotation; add
rationale and evidence; and identify required follow-on lifecycle work. It may not revise the
reported producer case, mutate an authoritative artifact, or perform that follow-on work during
`F(feedback)`. A later producer-owned revision is a separate lifecycle result and is linked only
after the responsible skill creates it through its normal workflow.

When that response identifies required follow-on work, Report may render one attributed `ACTION`
that names the responsible skill, the exact producer-requested lifecycle operation, and the source
response. It cannot start the operation or attach a control whose confirmation would do so; the
user invokes the public skill separately.

One confirmed feedback batch permits one pass only. Each represented skill is considered at most
once in canonical order, and no response, unresolved delivery state, or linked producer revision
recursively invokes `F(feedback)`. Report consolidates the completed and unresolved outcomes, then
returns control to the user.

The source revision is pinned for the entire pass. If a newer producer revision appears, Report
continues against the snapshot the user reviewed, records the supersession as a procedural fact,
and marks the newer revision's affected sections unreviewed in the consolidated artifact. It does
not substitute the new source or restart circulation without a new user confirmation.

The relation cannot select or start substantive work, interpret the user response authoritatively,
or itself create producer acceptance, producer approval state, artifact mutation, or lifecycle
effect. Report may preserve the exact confirmed user decision as communication evidence. A send
attempt, confirmed receipt, producer response, producer disposition, and producer-owned lifecycle
effect remain separate events. `F(feedback)` is not `C` because it returns no consultant `pass`, `drift`,
or `authority_gap`; it is not `H` because it starts no public peer workflow; and it is not ordinary
`I` because its represented principal, bounded review operation, and fidelity obligations are
explicit.

### 8.3 Lifecycle reporting moments and the ReportEvent envelope

The six invoke `I(reporting)` at exactly five moments: authoritative-artifact completion; any
approval request; stage boundaries (entry refused, work stopped, cycle closed); explicit user
status requests; and failure or degradation announcements. Nothing else routes through
Report **from the lifecycle profile**. Section 8.8 adds producer-neutral progress and deliverable
events without changing these five lifecycle obligations.

This envelope governs delegated `I(reporting)` input only. A user invoking Report directly
supplies the direct request of 3.4; Report must not impersonate a lifecycle producer by
manufacturing a ReportEvent.

Every moment crosses the relation as one common **ReportEvent envelope**: event type (one of
the five); producing skill; `artifact_ref`, either an identity/revision/hash tuple per 7.11.3 or
`null`; a one-sentence producer-authored outcome; blocking status; surface candidates with
their source-assigned stance and consequence semantics (8.6); open-decision references; and
evidence references. A stance-bearing rendering requires the producer to identify its
communicative purpose, governing point, recommendation or explicit absence, requested action,
and material caveats or counterpositions where applicable; Report never reconstructs these from
tone or prose implication. `artifact_ref` is required for artifact completion and whenever an authoritative
artifact already exists; it may be `null` only when entry is refused or work fails before any
artifact can exist. A null reference requires a producer-owned event identity plus evidence or
failure anchors, so Report never invents an artifact to satisfy the schema. Approval requests
extend the envelope with the decision payload of 8.4. The envelope is a payload contract, not
an artifact: producer-authored, consumed by Report, and reflected in Report jurisdiction only
through the bounded Report Artifact's source and rendering events.

### 8.4 Approval-request rendering

The producing skill owns the decision: its identity, options, consequence fields, and the
authoritative recording of the user's answer in its own artifact (7.11.1 approval machinery is
unchanged). Report owns wording, ordering, budget placement, and evidence links. The decision
payload extending the ReportEvent envelope is: decision identity; options with source-assigned
consequences; evidence references; blocking status; and an explicit recorded recommendation or
`none`. The Report Artifact records that the decision was presented and may preserve the user's
final confirmed response as a user-principal communication event. A confirmed approval is
authoritative evidence of the user's decision for the exact referenced target and revision, but it
does not change producer-owned approval state. The producer's artifact alone interprets and records
its authoritative disposition and lifecycle effect.

The complete decision envelope appears in the consolidated report or its decision panel and is
never hidden behind an evidence request. Supporting rationale, alternatives, and evidence remain
addressable before the user answers. When the host renders the producer's options as structured
choices, their labels and consequence summaries come unchanged from the decision payload. Report
may faithfully foreground a producer-recorded recommendation; when the producer records none,
Report cannot invent or strengthen one to satisfy the host.

### 8.5 Degraded fallback when Report is unavailable

Non-decision moments (completion, stage boundary, status, failure): the producing skill emits
exactly the artifact identity and path, one sentence of outcome, blocking status, and the
Report-unavailable flag. It does not compose a rich report; the six never regain direct rich
reporting.

Approval requests degrade differently, because a one-line notice cannot support informed
consent: the producing skill presents its **complete minimal decision envelope** — the full
8.4 decision payload (decision identity, every option with its source-assigned consequences,
evidence references, blocking status), stated plainly without Report's layering or budget.
Work stops only while awaiting the user's answer, never because Report is unavailable, and
the producer records the answer in its own artifact as always.

Both gaps self-heal: the next successful Report invocation sees un-briefed artifact revisions
in the ledger delta and surfaces them.

### 8.6 Reporting hooks on the six artifact contracts

The original contract audit found stable identifiers (Finding IDs, requirement and acceptance
identifiers, and the machine-checkable traceability chain) plus partial supersession semantics.
Five cross-skill additions were required and are now reconciled in the six sibling designs:

1. **Typed stance and consequence semantics** on every user-relevant claim: communicative purpose,
   governing point, motivation where recorded, consequence, blocking-or-deferrable,
   decision-required-or-FYI, recommendation or explicit `none`, requested action, and material
   caveats or counterpositions — all assigned by the producing skill (6.3). Exact runtime field
   names remain a later schema decision.
2. **A common open-decision shape** across all six, so open decisions are enumerable without
   six parsers.
3. **Explicit supersession fields** for Understand Code, Implement, Test, and Ship, matching
   the Critique and Spec pattern, so delta computation (7.4) is structural across the whole
   chain.
4. **ReportEvent envelope adoption** (8.3) at every reporting moment, including the approval
   extension (8.4).
5. **A bounded `F(feedback)` response hook** through which each represented skill can receive one
   pinned, user-confirmed Report Artifact and return at most one attributed response for its owned
   unresolved targets, without source mutation, new work, or lifecycle effect.

These are semantic design contracts, not exact runtime schemas. Their sibling wording was
reconciled on 2026-08-20; source-accounting rows remain `claimed`, never `resolved`, and runtime
implementation remains separately gated.

### 8.7 Impact on the six designs

Each sibling's reporting section now carries two deliberately asymmetric clauses:

- outbound `I(reporting)` delegates producer-authored presentation to Report; and
- inbound `F(feedback)` permits one response-only review act over the pinned Report Artifact.

Their content authority, source-artifact ownership, public entry, approval recording, and
lifecycle effects are untouched. A skill may annotate only its own unresolved targets; Report is
the sole physical Report Artifact writer; and any actual revision or work requires a later,
separately invoked producer workflow. This is a communication-interface amendment, not an
authority transfer.

### 8.8 Producer-neutral ReportPacket profile

Cooperating agents outside the six lifecycle authorities delegate only **presentation** through a
producer-owned ReportPacket. The packet is a semantic contract, not a lifecycle artifact and not a
new public workflow. The six-skill `F(feedback)` review relation is not generalized to these
producers in v1. The packet carries:

| Field | Invariant |
|---|---|
| Packet identity | Stable producer-owned ID and schema/profile version |
| Producer and provenance | Stable producer ID plus `lifecycle_authoritative` or `producer_owned`; Report never upgrades the latter |
| Event type | `progress`, `result`, `approval_request`, `stage_boundary`, `status_request`, `failure`, or `deliverable` |
| Source references | Stable artifact, event, or deliverable references; absent only for a labelled pre-artifact refusal/failure degradation |
| Outcome and blocking state | Producer-authored; Report may order but never infer or re-grade |
| Surface candidates | The same stable claim, consequence, blocking, decision-required, and evidence shape as 8.6 |
| Open decisions | Complete producer-owned decision objects; an incomplete decision is reported as a contract gap, never repaired |
| Progress steps | Ordered stable step IDs, labels, producer work states, and evidence/blocker references; empty as `[]` |
| Deliverables | Stable descriptors for existing outputs: ID, kind, label, location, optional revision/hash, linked surfaces/evidence, and caveats; empty as `[]` |
| Supersession | Stable references sufficient for structural delta when available; absence forces full-current rendering rather than prose-diff inference |

The Report core normalizes `astra.report-event/v0` into this semantic profile without discarding
its lifecycle producer, artifact, boundary, decision, or evidence fields. The six continue to emit
their existing envelope and must not use a generic packet to bypass their authoritative artifact
contracts. Direct Report invocation resolves its scope under 3.4 and fabricates neither profile.

The normalized internal form retains adapter-only trace fields for `source_profile`, the original
event identity, and every `open_decision_ref`; these do not widen the public ReportPacket contract.
When a v0 event names an open decision but supplies no complete producer-owned decision object,
normalization preserves the reference and emits a `missing_open_decision_envelope` contract gap.
Report may expose that gap, but it must not turn the unresolved reference into an option or approval
surface. This is the lossless degradation required by Scenario G, not a license to repair the
producer contract.

A cooperating agent invokes Report implicitly only when it is about to emit a reportable outbound
event. Ordinary dialogue remains direct. If the host cannot invoke Report, the producer emits a
minimal faithful result or complete decision envelope using the same degradation principle as
8.5; failure of presentation cannot change producer state or authority.

## 9. Dependencies and delivery shape

### 9.1 External components that remain separate

`make-pdf` and `diagram` (deferred post-v1 generated-format adapters, 4.3); the six slice sources (4.2, independent
registrations retained); the method references (4.4, readable citations, not dependencies);
the artifact chain storage convention (prerequisite: wherever the six persist artifacts,
Report must be able to resolve immutable references; its absence is a 7.6 degradation).

### 9.2 Peer relations

| Peer | Relation | Direction and content |
|---|---|---|
| All six lifecycle skills | `I(reporting)` | Each consumes Report's rendering capability at the 8.3 moments via the ReportEvent envelope |
| All six lifecycle skills | `F(feedback)` | Report makes one non-recursive pass with one pinned, user-confirmed Report Artifact in canonical lifecycle order; each represented skill may return one attributed, response-only disposition and explanation for its owned unresolved sections, while approved sections skip response work but not approval delivery or recording; circulation performs no source mutation or lifecycle work |
| All six lifecycle skills | `I` | Report reads their immutable artifacts by reference |
| Cooperating non-lifecycle producers | presentation seam only | Each may supply a producer-owned ReportPacket at a reportable outbound event; no lifecycle determination, relation, or authority is created |
| `astra-critique` | user-mediated routing | A surfaced contradiction may lead the user to open Critique; Report never starts it |
| `astra-understand-code` | `R` only | Adjacent explanation jobs: repository state vs artifact state; triggers must not collide (3.3) |
| `astra-product-design` | `R` only | Shares the method-reference pattern, no runtime relation |

### 9.3 Critique handoff acceptance

**No.** Report owns no problem class that Critique findings could route to: it performs no
remediation, and a communication-defect finding about a brief is repaired by re-rendering, not
by a lifecycle handoff. Contradiction traffic flows the other way and is user-mediated (3.7).
Per the section 7.11 checklist, this declaration is required of every design other than
Critique.

## 10. Manual bridge

Usable today, before any implementation:

1. At any reporting moment, manually compose one consolidated Reader Brief under sections
   6–7, linking consequential claims by the identifiers the producer artifacts already carry.
2. Lead with the producer-supported governing outcome or live decision. When several comparable
   topics exist, use the conditional five-function route; use the report-job-specific structures
   in 7.2 when that route would distort the material.
3. When progress exists, render the producer's ordered steps and exact work states with native
   indicators when available or equivalent text. Never derive work state from conversation.
4. When delivering an existing report, Markdown file, code change, or diff, show its stable
   descriptor and producer-authored significance, caveats, and evidence; do not edit or
   independently judge it.
5. If a bounded Report Artifact is maintained manually, append only receipt-backed presentation
   facts and final user-confirmed feedback under 7.3 and 15.3–15.4. Without a receipt, do not claim
   exposure; without confirmation, do not log a feedback draft.
6. Use `/doc` (register), `internal-comms` (status shapes), and `doc-coauthoring` (chunking)
   as source oracles for the prose itself, under this design's precedence chain.
7. Never let manual rendering alter, re-grade, or omit-without-deferral any producer content.

The bridge is the reference convener for section 11. Its known loss versus the future skill:
manual delta computation is error-prone without structural comparison; record that loss rather
than trusting it.

## 11. Deferred implementation and validation

### 11.1 Three comparison systems

- **Source oracle:** strongest applicable single source per case (5.4).
- **Reference convener:** the manual bridge (10).
- **Self-contained candidate:** the future `astra-report` skill, which must reproduce retained
  behavior without reading the originals.

### 11.2 Fixed corpus classes

1. One single-artifact brief per artifact type (six cases).
2. Bounded Report Artifact resumption after a source revision (minimal orientation + structural
   delta for that subject).
3. Multi-skill overload: an aggregated run producing 30+ findings across artifacts.
4. Approval-request rendering from a typed payload.
5. Several topics plus multiple blockers (all blocker/decision semantics remain visible, 7.5).
6. Contradiction between two artifacts (surface, never adjudicate).
7. Missing Report Artifact (degradation to full-current subject state without fabricated review
   history).
8. Missing identifiers (verbatim-quote degradation).
9. Report unavailable at an `I(reporting)` moment — both 8.5 fallbacks: the non-decision
   minimal notice, and the approval-request complete minimal decision envelope.
10. Fidelity-adversarial: a tempting simplification that would drop a caveat (must demote,
    never delete).
11. Consolidated-completeness probe: the user can identify every material top-level topic and all
    required action without asking whether another hidden section changes the decision.
12. Mode variants over the same scope (density changes; addressability does not).
13. Forbidden-effect probes: attempted re-grade, attempted artifact edit, attempted automatic
    Critique start — all must fail.
14. One home-jurisdiction case per contributing source: `/doc` register enforcement on a
    document-shaped brief; `doc-coauthoring` chunk protocol on a long brief; `internal-comms`
    status shape on a status request; `document-generate` explanation structure on a
    why-focused brief; `teach` chunk sizing on a dense technical delta; `rtfm` consumer
    framing on an interface-facing change.
15. Change Story from a complete chain: every element present and trace-linked.
16. Change Story with a missing element: the gap is named; nothing is invented.
17. Expected-divergence controls: the oracle would drop a caveat, re-explain unchanged
    background, or ask "want to hear more?" — Report must diverge on all three.
18. Expected-convergence control: pure register quality on one short artifact, where Report
    and the `/doc` oracle should be indistinguishable.
19. Pre-artifact refusal and failure events: `artifact_ref: null` is accepted only with a stable
    producer event identity and evidence or failure anchors; completion with a null artifact is
    rejected.
20. Approval presentation followed by a user answer: the Report Artifact records the presented
    decision and only the final user-confirmed response; it never converts that response into
    producer disposition or approval state.
21. Attribution control: compare the corrected Astra Change Story description with a rendering
    that labels before → problem → fix → after as SCQA; the false attribution fails even when
    the prose is readable.
22. Diátaxis boundary control: compare bounded rationale plus the complete decision envelope
    against explanation-only prose; the latter fails when the user cannot act from it.
23. Resumption mechanism control: expose stable subject, governing context, and source-revision
    cues before a simulated interruption, then compare minimal-orientation-plus-delta, delta-only,
    and full-current conditions. No condition may be described as proven before comparison runs.
24. Expertise and density control: compare `skim`, `standard`, and `deep` with project-familiar
    and project-new evaluators; authority, caveats, and addressability must remain constant.
25. Viewed-state control: revise a shown subject without changing its approval state; the affected
    sections become eligible for renewed review, but Report must not call them unapproved.
26. Missing delivery receipt: the brief may render, but no presentation event is appended and the
    source revision remains eligible to surface again.
27. Redundancy-scoring control: minimal repeated orientation needed for comprehension or action
    completeness is not scored as a Mayer redundancy violation; the scorer separately flags
    renderer-authored extraneous duplication.
28. Viewed-state precedent guard: neither evaluation nor runtime behavior may depend on GitHub's
    public-preview "commits since last review" selector; source revision/hash plus bounded Report
    Artifact events are the oracle.
29. Consolidated Standard control: every material top-level topic appears in one response; no
    topic requires an outline-selection round trip before its section is available.
30. Five-function conditionality: a comparable multi-topic review preserves topic, motivation,
    plain explanation, impact, and action semantics while merging redundant visible fields; a
    progress or incident report uses its job-specific grammar instead.
31. Informative-heading control: each topic heading names its principal and carries the recorded
    governing point; category-only headings such as `Testing` fail when they hide the conclusion.
32. Action-order control: a producer-marked blocker or live decision moves complete action and
    consequence semantics first; a normal deliberate-review topic may retain the five-function
    comparison order.
33. No-inference template control: missing motivation, consequence, action, or recommendation is
    exposed or omitted as inapplicable, never plausibly completed by Report.
34. Decision-panel/text-fallback convergence: option IDs, labels, consequences, recommendation
    state, and confirmation effect are identical; host-specific placement is not required.
35. Required-recommendation control: an approval option is marked recommended only when the
    producer recorded that preference. A host-mandated but unsupported recommendation forces a
    faithful text fallback rather than invention.
36. Live progress: at least four ordered steps span completed, active, pending, and blocked states;
    native and textual renderings preserve IDs, order, state, blocker, and the current attention
    point.
37. Work/disclosure separation: opening a pending step's detail does not complete it, and receipt
    of a completed step's preview does not claim comprehension or change work state.
38. Producer-neutral packet: a non-lifecycle agent reports a result with stable producer-owned
    provenance; Report presents it without calling it a lifecycle artifact or authority.
39. Text deliverable: an existing report and Markdown file are delivered with identity, location,
    outcome, caveats, and evidence; Report writes neither file.
40. Code/diff deliverable: changed paths and producer-owned outcome/evidence are presented, while
    a request to explain repository behavior stays with Understand Code and a correctness judgment
    stays with Critique or Test.
41. Lifecycle normalization: each of the five `astra.report-event/v0` types maps into the common
    semantic profile without dropping artifact, boundary, decision, consequence, or evidence data.
42. Ordinary-dialogue non-trigger: intake, one clarifying question, brainstorming, and teaching do
    not create a ReportPacket merely because the producer speaks to the user.
43. Interface-complete release gate: the same candidate and public identity pass progress, result,
    blocker/failure, decision, lifecycle artifact, text deliverable, code/diff, resumption,
    degradation, and host-fallback families before promotion.
44. Attributed producer advocacy: Report may foreground a producer-recorded recommendation but
    every stance-bearing section identifies its principal and never strengthens `none`, polarity,
    certainty, or commitment.
45. Feedback polishing and confirmation: Report preserves the user's exact draft, presents a
    separately attributed polished version in one decision panel or faithful text fallback, and
    appends nothing until the user confirms, edits, or cancels it.
46. Principal switching: producer reporting, user feedback, and Report procedural notices remain
    distinct attributed sections even when one response contains all three; a user question or
    navigation request does not become a user-policy stance.
47. One event, several targets: one confirmed user wording may reference several stable targets
    and mechanically resolved owners without duplication; every delivery and receipt remains
    recipient-specific.
48. Canonical one-pass review: Understand Code, Critique, Spec, Implement, Test, then Ship each
    receive at most one response opportunity; a skill whose current-revision sections are all
    user-approved skips annotation work without blocking later approval recording.
49. Response-only producer annotation: a skill may return a disposition, rationale, evidence, and
    required-follow-on notice for its own unresolved targets, but cannot rewrite a reported
    section, mutate its source artifact, perform work, or invoke another public skill.
50. Sole-writer integrity: each producer-authored response is appended immutably by Report without
    semantic transformation; neither the user nor a skill writes the Report Artifact directly.
51. Pinned-round revision: the pass finishes against its starting revisions; a newer source is
    shown as newly `UR` without source substitution, restart, or recursive circulation.
52. Dual-record approval: a user-facing `AP` is authoritative evidence of the user's exact
    decision, while the owning skill-facing recording section remains `UR` until that skill later
    records producer-owned approval state through its normal workflow.
53. Conflicting annotations: incompatible skill positions remain separately attributed inside one
    elevated conflict surface; Report neither votes, merges, orders them as precedence, nor invents
    a common recommendation.
54. Role-local unavailable state: a failed or unavailable skill leaves only its named skill-facing
    annotation or recording section `UR`; all user-facing markers remain unchanged, remaining
    skills still receive their pass opportunity, and silence is never approval or no objection.
55. Attributed follow-on handoff: Report may name one producer-requested `ACTION`, then stops; only
    a separate user invocation starts the responsible public workflow.
56. Non-recursive termination: producer responses and later revisions never initiate another
    `F(feedback)` round; only new or amended user-confirmed feedback can create a later pass.

### 11.3 Method and measures

Paired runs on identical artifact sets against the applicable source oracle, with repeated
trials; subjective judgments (register, clarity, action completeness) use blinded,
order-randomized evaluation. Measures: reply-surface count and consequence distribution;
critical-decision
recall (no blocking decision omitted — required at 100%); supported-claim precision and
unsupported-claim rate against artifact fields; fidelity audit (every omitted or demoted item
addressable by identifier; zero deleted caveats); source-unique supported behaviors (each 4.2
slice observably survives); bounded-delta correctness against Report Artifact ground truth;
consolidated action completeness judged against the artifact set; duplicate/noise load against
Astra's surface-economy rules; correct choice of report-job grammar; five-function semantic
coverage without forced repetition or unauthorized inference; informative-heading quality;
action ordering for producer-marked blockers; decision-panel/text-fallback convergence;
communication-event integrity; and cost, latency, and required user turns per complete report.

The v1 gate additionally measures work-state preservation, work/disclosure independence,
ReportEvent-to-packet field preservation, deliverable provenance/addressability, correct
dialogue/report trigger classification, and semantic convergence between native progress UI and
text fallback. The stance-bearing extension additionally measures principal-identification
accuracy; preservation of exact user wording; semantic fidelity and visible provenance of polished
feedback; confirmation-before-append integrity; recipient and target precision; response-scope
compliance; one-pass and non-recursion bounds; sole-writer provenance; separation of user decision
evidence from producer approval state; conflict visibility; actor-local marker correctness; and
zero false approval, false receipt, source mutation, or Report-created lifecycle effects.

The conditional five-function route, its order, consolidated Standard density, reply-surface
allocation, and minimal-orientation resumption value are Astra product hypotheses. The cited
communication and cognition sources motivate their evaluation but do not constitute passing
evidence.

### 11.4 Gates and consequences

| Gate | Failure consequence |
|---|---|
| Home non-regression: no brief loses artifact facts or register quality vs the oracle | Narrow the failing playbook slice; re-derive from its source |
| Positive advantage on classes 2, 3, 4 of 11.2 | Withdraw the public interface; Report collapses to an exported style contract consumed by the six (5.4) |
| Internalization fidelity: candidate matches convener on retained behavior | Candidate blocked; convener remains the bridge |
| Invariant preservation (section 6) on classes 10, 11, 13 | Design fault, not tuning: revise this document |
| Constitutional mediation safety on classes 44–56: no principal laundering, invented recommendation, false approval/receipt, source mutation, or Report-created lifecycle effect | Reject the stance-bearing path regardless of clarity, preference, speed, or token savings; retain the smallest safer output-only or split-role boundary |

### 11.5 Retirement

**None in this tranche.** No source retires on Report's account; slices leave every original's
registration untouched, and the approved lock exception in 4.2 does not move any of the
deferred five into the 92 target. Because no retirement is proposed, no source-specific retirement gate is created;
any future whole-source claim must add one under `docs/design-requirements.md` section 7.9
before it can be evaluated.

## 12. Provenance and open questions

### 12.1 Inspection summary

Eight source entries inspected 2026-08-12 at live paths with sha256 short hashes (4.1);
supporting bodies and authored gstack templates hashed the same day at revision
`a3259400a366593e0c909dd9ac3e59752efd2488`, release `1.60.1.0` (4.1.2). The same-day design
review independently re-verified all eight entry hashes. The named evidence gap — consumed
resolver/section templates and generator registration for the three generated gstack sources
— is recorded in 4.1.2 with its consequence. The six lifecycle designs,
`docs/design-requirements.md` (sections 5, 6, 7.9, 7.11), `docs/phase-0.md` (section 5),
`docs/phase-0-ledgers.md` (the rows cited in 4.5), and `docs/six-skill-source-absorption.md`
(sections 1, 7, 8, 11) were read the same day as authority context. The user's problem
statement and initial decisions are conversation records of 2026-08-12, quoted in 1.1 and 2.1 —
**Observed**, including the review resolution recorded in 1.2. The earlier staged-disclosure,
detail-choice, and safe-continuation model was recorded in the design on 2026-08-13 but was not the
user-specified report model; the user corrected it on 2026-08-19 through decisions 4–6 and section
15.6. The implicit outbound-reporting, progress-indicator,
read-only deliverable, and interface-complete-milestone decisions are conversation records of
2026-08-17 and are reconciled in
[`docs/research/2026-08-17-astra-report-research-to-design-reconciliation.md`](../docs/research/2026-08-17-astra-report-research-to-design-reconciliation.md).

The current Codex host contract was inspected on 2026-08-13 (**Observed**): structured user input
is available only where the active collaboration mode exposes it; one panel accepts one to three
questions, each with two or three authored options and one short option description, while the
client may add a free-form alternative. The contract does not guarantee right-side placement or
portable availability. Those limits justify capability detection and faithful textual fallback
for real decisions and feedback confirmation; they do not make structured choices a report
outline or universal Report semantic.

Official OpenAI documentation was inspected on 2026-08-17 (**Observed**). Skills may activate
implicitly when a task matches the `description`, and `agents/openai.yaml` exposes
`policy.allow_implicit_invocation`, defaulting to true
([Build skills](https://learn.chatgpt.com/docs/build-skills)). The documented Goal mode exposes a
host progress row, but the documentation does not establish a portable skill-controlled step API
([Long-running work](https://learn.chatgpt.com/docs/long-running-work)). Therefore v1 must
front-load reportable-output triggers in metadata, keep implicit invocation enabled, probe actual
host progress capability, and preserve text fallback; it must not claim that every host can render
native squares.

The method canon audit at
[`docs/research/2026-08-12-astra-report-method-canon.md`](../docs/research/2026-08-12-astra-report-method-canon.md)
inspected seven supplied local books by full SHA-256 plus primary or official external sources.
It distinguishes direct support, analogical transfer, Astra synthesis, and rejected attribution.
The local *Multimedia Learning* file is an incomplete preview; its absent method chapters are not
used as evidence. The accessible Cambridge handbook and replacement Clark/Mayer PDF ground the
limited multimedia-learning analogies instead. Books remain research inputs, not runtime files.

### 12.2 Provisional decisions

- Williams over Douglas for the sentence-mechanics slot; Douglas recorded as the alternate.
- No exact numeric attention budget is adopted as a human constant; grouping and density remain
  testable product defaults under 7.5.
- Time-decay re-glossing is admitted as a future-safe extension (2.4) but not designed.
- The Report Artifact format, storage location, identity scheme, retention, and concurrency
  mechanism are later-phase work.
- A successfully written exact-output file may serve as a delivery receipt in a conformance
  tranche; native conversation-host receipts remain a v1 adapter obligation. Composition or an
  attempted send alone never counts as exposure (7.3).
- The 2026-08-13 delegated Spec-approval Slice A remains a mechanically checkable conformance
  tranche. It no longer defines the first public runtime or permits approval-only skill metadata.
- The committed plan
  `docs/superpowers/plans/2026-08-12-astra-report-spec-approval-slice.md`, reconciled in `318bcaf`,
  is superseded for execution by the 2026-08-17 interface-complete v1 direction. Its fixtures and
  cases may be incorporated into the v1 plan; its approval-only `SKILL.md` must not be shipped.
- Resolved by the 2026-08-12 review, then narrowed by the 2026-08-20 amendment: `I(reporting)`
  remains output-only, while final confirmed feedback about one pinned Report Artifact may return
  through the distinct `F(feedback)` relation. The withdrawal of `V` and the post-v1 deferral of
  the `make-pdf` and `diagram` generated-format adapters remain unchanged.
- Resolved by the user's 2026-08-12 approval: the exact three-source secondary-slice exception
  in 4.2. The exception changes claim ownership only and leaves all five documentation sources
  outside the 92 target.
- Ordinary intake dialogue stays outside the Report Artifact. Only final user-confirmed feedback
  tied to its bounded reported subject may be appended (decision 13).

### 12.3 Open questions (each names its consequence)

1. **What grouping and density work best within consolidated Standard?** The approved direction
   avoids a reveal turn per section, but an unbounded flat response can still recreate overload.
   Evaluation must compare decision quality, severe-item recall, required user turns, and noise
   before fixing product defaults.
2. **How aggressively may adjacent five-function fields merge without obscuring the user's
   route?** The user-approved default labels are `TOPIC`, `MOTIVATION`, `WHAT IS IT?`, `IMPACT`,
   and `ACTION`, with `ACTION` promoted for a blocker, urgent failure, or live decision. Evaluation
   must still determine when redundant or inapplicable labels can disappear without reducing
   comprehension, attribution, or action completeness.

### 12.4 Coordinator reconciliation state

All source rows remain `claimed`, never `resolved`, citing the 2026-08-12 user decisions in 1.1:

1. **Complete, 2026-08-13.** Amend the exactly-six roster statements:
   `docs/design-requirements.md` 7.11 and
   `docs/six-skill-source-absorption.md` section 1 — six lifecycle authorities plus one
   non-authoritative reporting surface that owns all rich outbound presentation; the six
   remain directly invocable control surfaces.
2. **Complete, 2026-08-13.** Record the `I(reporting)` typing convention in the 7.11.2
   relation vocabulary; no new relation letter is added.
3. **Complete, 2026-08-13.** Apply the section 4.5 row changes: seven `unclaimed` → `claimed`
   secondary-role claims, including the three-source lock exception approved in 4.2; and the
   `diagram` secondary-consumer amendment against roadmap amendment 3. Every changed row remains
   `claimed`, never `resolved`.
4. **Complete, 2026-08-13.** Add the four reporting hooks (8.6) — consequence typing, the common open-decision shape,
   supersession fields for Understand Code, Implement, Test, and Ship, and ReportEvent
   adoption — to each sibling design's artifact contract.
5. **Complete, 2026-08-13.** Add the `I(reporting)` delegation clause to each sibling's user-visible-result and
   approval sections (8.7).
6. **Complete, 2026-08-13.** Include Report in the trigger-surface reconciliation (absorption design section 11,
   remaining-work item 3), ensuring 3.2/3.3 does not collide with Understand Code or the
   deferred documentation candidates.
7. **Complete, 2026-08-20.** Add `F(feedback)` to the shared relation vocabulary as a bounded,
   review-only return path distinct from outbound `I(reporting)`, consultation, handoff, and public
   workflow invocation.
8. **Complete, 2026-08-20.** Add reciprocal `F(feedback)` clauses to all six lifecycle designs,
   preserving their source-artifact authority, producer-owned approval recording, and separate
   public invocation for any substantive work.
9. **Complete, 2026-08-20.** Reconcile the stance-bearing mediation direction into roadmap
   amendment 11 without altering source-allocation rows or authorizing runtime execution.

## 13. Shared trigger-surface reconciliation result

`docs/design-requirements.md` sections 7.11.6–7.11.7 are canonical. Direct Report requests own
explanation of recorded lifecycle artifacts and project state plus read-only presentation of
stable producer deliverables. Repository behavior, structure, and bounded code-state explanation
remain Understand Code authority. Report remains outside the six-authority classifier: it may
preserve and pass final user-confirmed feedback within a bounded Report Artifact, but it returns
no Report-authored lifecycle determination and orchestrates no stage.

Standard delivery presents the producer-supported governing outcome and all material top-level
topics in one consolidated response. Evidence remains addressable without a topic-selection turn.
Only a real producer decision or feedback confirmation uses a decision panel, and that panel
cannot grant any effect beyond its exact producer- or user-owned semantics.

The five `I(reporting)` moments—`artifact_completion`, `approval_request`, `stage_boundary`,
`status_request`, and `failure`—and both producer fallbacks are canonical across the six
lifecycle designs. Producers retain fact, consequence, option, evidence, blocking, and returned-
decision authority; Report retains presentation authority only.

Other cooperating producers may use the section 8.8 ReportPacket profile at a reportable outbound
event. This widens presentation ingress only; it creates no seventh lifecycle authority and does
not change the six lifecycle event obligations.

The earlier Report implementation plan was reconciled for staged segments and conditional
structured choices in `318bcaf`, then superseded for execution on 2026-08-17 because its
approval-only public identity conflicts with decision 9. The proposed replacement below also
predates decisions 4–6 as corrected on 2026-08-19 and must be reconciled before any execution:
[`docs/superpowers/plans/2026-08-17-astra-report-v1.md`](../docs/superpowers/plans/2026-08-17-astra-report-v1.md).
No runtime begins until that plan is reviewed and a separate runtime-execution choice is recorded
in `docs/phase-0.md`. This reconciliation creates no runtime, corpus runner, installation,
publication, or retirement state.

## 14. Interface-complete v1 amendment (2026-08-17)

This amendment applies the later user decisions recorded in 1.1 items 7–9 and the approved
research reconciliation. Where earlier prose conflicts, this section governs.

### 14.1 Preserved core

Reply-surface awareness, structural source delta, blocking escalation, visible deferral, fidelity
precedence, safe continuation, and read-only lifecycle authority remain. Decisions 4–6 and section
15 supersede the mandatory Capsule/NOW/detail-menu staging, per-project Exposure Ledger, and
factual-exposure-only durable-state claims. The replacement is consolidated Standard delivery plus
one bounded stance-bearing Report Artifact per reported subject or review cycle.

### 14.2 Widened presentation ingress

The six lifecycle skills continue to emit `astra.report-event/v0` at their five canonical moments.
Other cooperating agents may supply section 8.8's producer-owned packet when they emit progress,
results, blockers/failures, decisions, deliverables, or status. Report normalizes both through one
deep rendering module. Ordinary conversation is not an event source, and a non-lifecycle producer
never acquires lifecycle authority.

### 14.3 Progress and delivery

The host rendering seam supports native progress indicators, decision/confirmation panels, and
links/attachments when available, with semantically equivalent text fallbacks. Work state belongs
to the producer; disclosure state belongs to Report. Report may organize delivery of already-made
reports, Markdown files, code changes, and diffs, but cannot author, edit, explain beyond recorded
claims, or judge them.

### 14.4 First public milestone

The first promoted `astra-report` must pass the 11.2 interface-complete cases across progress,
results, blockers/failures, decisions, lifecycle artifacts, text deliverables, code/diffs,
resumption, degradation, and host fallback. Internal tranches may be implemented and reviewed
separately, but the skill metadata and public claim remain withheld until the common contract and
representative diversity pass together. The Spec-approval Slice A is one retained conformance
tranche, not the product milestone.

### 14.5 Authority and execution stop

This amendment authorizes design and implementation planning only. It does not authorize a
`SKILL.md`, schema, script, test harness, Report Artifact storage, installation, or runtime
execution. The pre-amendment interface-complete plan is
[`docs/superpowers/plans/2026-08-17-astra-report-v1.md`](../docs/superpowers/plans/2026-08-17-astra-report-v1.md).
It remains evidence and case inventory but must be revised against section 15 and reviewed before
any execution request. Execution also requires an explicit, separately scoped amendment to
`docs/phase-0.md`.

## 15. Stance-bearing mediation amendment (2026-08-19 through 2026-08-20)

This amendment records the later user decisions in 1.1 items 10–28 and the evidence-grounded
correction of items 4–6. Where those decisions conflict with the output-only,
per-project-Exposure-Ledger, or one-topic-per-turn design, this section governs. The amendment
remains phase-0 design: it authorizes neither a runtime nor an automatic delivery mechanism.
Exact runtime schema and storage mechanics remain deferred rather than being inferred from the
deep-research proposal; the documentation-level downstream contracts are reconciled.

### 15.1 Represented stance and principal switching

Report is a delegated author and guide, not a stance-free formatter. It actively presents the
current producer's recorded case while preserving that producer as the represented principal.
Its rhetoric may make the producer's conclusion and recommendation clear and compelling, but may
not exceed the source's commitment, certainty, scope, or material evidence.

Each stance-bearing block has one top-level represented principal:

- **producer position** — facts, conclusions, recommendations, objections, and requested actions
  supplied by the relevant authority;
- **user position** — a confirmed decision, policy, preference, correction, substantive comment,
  or requested change; or
- **Report status** — only facts inside Report's own jurisdiction, such as what it revealed,
  recorded, sent, received, or could not deliver.

A principal change starts a separately labelled block; repeated labels inside an unchanged block
are unnecessary. Nested attribution remains valid: for example, "the user accepted Test's
conclusion" is a user-position act that references Test's position. Questions such as "why?" and
navigation such as "show the evidence" remain ephemeral interaction requests rather than durable
user-position events. A mixed response is split into the smallest blocks needed to preserve those
different functions.

### 15.2 Bounded sequential feedback circulation

For feedback attached to the active Report Artifact, Report may preserve the confirmed response,
bind it to stable section/claim/option and source-revision references, pin that annotated Report
Artifact, and circulate it through `F(feedback)`. The order is Understand Code, Critique, Spec,
Implement, Test, then Ship. A skill with no owned section is outside the round. Ambiguous section
ownership or genuinely cross-authority routing remains unresolved until the user clarifies it;
Report does not choose substantive jurisdiction. One event may carry several stable targets and
therefore several mechanically resolved owners. Report asks once before confirmation when those
references do not establish the recipient set; it never derives recipients from prose alone.

For each represented skill:

1. if every owned section is user-approved for the pinned source revision and has no unresolved
   comment, condition, rejection, or change request, Report delivers or exposes the user approval
   event for later producer recording but requests no annotation response;
2. otherwise, Report supplies the pinned artifact and requests one bounded, attributed response
   covering only that skill's owned sections; and
3. the skill authors one immutable response and Report, as sole writer, appends it beside the user
   annotation and earlier skill responses without paraphrasing or merging; it may not overwrite
   them or another principal's position.

The response is limited to a disposition on the user's annotation, rationale or evidence for that
disposition, and identification of any required new authoritative revision or separate lifecycle
operation. It cannot rewrite the reported section, mutate its source artifact, or carry out the
requested work. If a change is required, the responsible skill performs it only through its normal
lifecycle after the circulation round; Report later links the resulting producer-owned revision
without treating the annotation response itself as that revision.

After all eligible skills have responded, been skipped under rule 1, or retained an internally
recorded transport failure, Report presents the consolidated skill-annotated Report Artifact to
the user. This creates one review round rather than one user conversation per skill.

User-facing report sections and named skill-facing annotation or recording sections are visibly
separate. If one skill is unavailable or delivery fails, its section remains `UR`; Report does not
add a second delivery-status marker or change any user-facing marker. It records the transport fact
inside the Report Artifact, continues through the remaining skills, performs no automatic retry,
and never treats silence as approval or lack of objection.

Incompatible responses are not blended into that consolidation. Report elevates one `CONFLICT`
surface containing each attributed position and its evidence, then gives one `ACTION` naming the
decision authority established by the source contracts. The user owns policy and trade-off
decisions; a skill retains its technical record inside its jurisdiction. If neither rule resolves
the authority, the action states the gap rather than choosing a winner.

The round then stops. A skill response, clarification request, rejection, deferral, failed
delivery, or subsequent producer-owned revision never starts another circulation automatically.
Another round requires a new or amended user-feedback batch and one new confirmation; unchanged
resolved sections remain skipped. This prevents the review protocol from becoming an automatic
skill-to-skill or user-to-skill convergence loop.

All responses in the round remain attached to the source revision pinned when the user confirmed
the batch. If a newer producer revision appears before the round ends, Report finishes the current
pass against that immutable snapshot and flags the newer revision and its affected sections as
unreviewed. It neither substitutes the new source mid-pass nor starts a review of it. A later round
for the newer revision requires a new user confirmation.

The return path distinguishes at least:

```text
confirmed -> sent -> received -> producer disposition -> producer-owned lifecycle effect
```

These are independent claims. A send attempt is not receipt; receipt is not acceptance; a
producer disposition is not a lifecycle effect; and none is evidence of cognition. The bounded
review operation and a durable receipt may support the first three states. If the host offers no
such path, Report records the transport fact internally and leaves the relevant named skill-facing
section `UR`; it adds no visible delivery state or suffix. It must not start or schedule
substantive work, reopen an authoritative artifact, or advance a lifecycle stage to manufacture
delivery or closure.

A confirmed user approval is already authoritative evidence of the user's decision for its pinned
target. Until the owning producer creates its approval record through the normal lifecycle, Report
keeps the user-facing section `AP` and the owning skill's separate recording section `UR`.
Skipping a cleanly approved section therefore avoids redundant annotation work without pretending
that the producer artifact has changed.

If a response says that follow-on lifecycle work is required, the consolidated artifact presents
one attributed `ACTION` with the responsible skill, exact producer-requested operation, and source
response. Report then stops. A separate user invocation of that public skill is the authority to
begin work; neither an annotation, an action-panel selection, nor `proceed` starts it.

### 15.3 Polishing and confirming user feedback

Typed feedback remains session-local draft material until the user confirms the wording. Report
may improve grammar, tone, organization, terminology, and explicit target or scope, but may not
silently change polarity, commitment, conditions, priority, requested effect, or policy breadth.

When polishing is useful, Report presents one bounded decision panel containing the proposed
final wording, destination or mechanically resolved destinations, and exact consequence of
confirmation. The controls are conceptually:
`Confirm and send`, `Send original`, `Edit`, and `Cancel`; a host may render equivalent controls
without changing their semantics. Only the selected final wording is appended as the single user
feedback event. Draft text and intermediate rewrites are not durable Report Artifact entries.
Changes made after confirmation use an explicit amendment or supersession event. An exact
structured decision that requires no rewriting needs no redundant polishing confirmation.
When feedback accompanies a producer decision, its wording confirmation and that decision share
one panel where the host can preserve both semantics; Report must not create two consecutive
confirmation rounds for one intended action.

Multi-target feedback remains one confirmed user event with one final wording. Per-recipient
delivery and receipt records may differ, but Report does not create several apparent user comments
merely because several owners receive it.

### 15.4 The stance-bearing Report Artifact

The Report Artifact is the reviewable communication object, not a neutral ledger. One artifact is
bounded to one specification, plan, code change, test report, release decision, deliverable, or
other named subject and its review cycle. It may survive multiple Report sessions and source
revisions, then closes when that review cycle is completed, abandoned, or superseded.

Its durable content is limited to:

- stable subject, source, revision, and rendered-segment identities;
- the rendered, attributed producer case and its source trace;
- the report outline and section revelation/review facts;
- one confirmed user-feedback event per completed confirmation flow;
- attributed skill responses from a bounded sequential annotation round;
- send/receipt facts and failure state; and
- references to producer acknowledgements, dispositions, and resulting authoritative revisions.

The confirmed user event and the producer-owned approval record are separate linked facts. The
first records what the user decided; the second records the lifecycle consequence within the
producer's jurisdiction. Report may display both states but can create only the first.

Report alone writes this artifact. Producer and user entries retain their originating principal,
author, stable event identity, and source references. A producer supplies its response as an
immutable return value; Report appends it exactly and may add only separately attributed transport
or ordering metadata. Corrections and withdrawals append a new attributed event that supersedes
the earlier entry; no participant edits history in place.

The rendered producer case is a stable snapshot of what Report presented, not a second source of
technical truth. Producer artifacts continue to own facts, severity, requirements, work state,
approval semantics, and lifecycle effects. Report owns only its presentation, review, and
communication records. When a source revision changes, affected sections are marked changed since
review and become eligible for renewed review; unchanged project history is not reconstructed. An
in-flight round remains pinned to its earlier snapshot, and the new revision stays unreviewed until
the user confirms a later round.

The earlier Exposure Ledger semantics survive as the Report Artifact's disclosure component under
7.3. Its historical per-project scope and the old claim that factual exposure is Report's only
durable state are superseded. Review or revelation, user position, delivery or receipt, producer
disposition, and lifecycle effect remain orthogonal facts; no single stored status may replace
them. The visible marker is local to its attributed user- or skill-facing section; a transport
failure remains an internal fact while the affected skill-facing section stays `UR`. Exact storage
format, underlying state syntax, retention, and concurrency mechanisms remain later decisions.

### 15.5 Low-dialogue review behavior

Revelation and review state support resumption; they do not create a compulsory review ceremony.
Opening, skipping, or returning to a section produces no confirmation question. Report does not
ask the user to mark each section reviewed, narrate every state transition, or acknowledge every
optional deferral.

The normal visible cue stays compact: the heading combines ordinal progress, the designated actor,
and one marker, for example `2/5 Testing — User [AP]` or `Test annotation [UR]`. The default marker
vocabulary is `UR` (unreviewed), `RV` (reviewed), `CM` (commented), `RJ` (rejected), `AP`
(approved), and `DF` (deferred). A user-facing marker and a skill-facing marker belong to separate
sections, so neither needs a delivery or producer-state suffix.

The visible marker is derived from the separate Report Artifact axes; it is not itself authority
or lifecycle state. Optional user-facing sections that the user does not open remain unreviewed or
deferred; Report never relabels them reviewed merely because the user proceeds. `RV` requires an
explicit act by the section's designated actor: a user statement or control for a user-facing
section, or an attributed skill response for a skill-facing annotation section. Reveal, opening,
scrolling, and delivery receipts establish exposure only. Report does not ask for that review event
section by section. In user-facing sections, `CM`, `RJ`, `AP`, and `DF` replace `RV` as the visible
marker without erasing the separate review fact.
Any remaining `UR` or `DF` sections may be listed inside the one final decision panel without
requiring a separate acknowledgement. Any material fact required for a safe immediate decision
must already be visible in the producer case and cannot be hidden behind an unreviewed-section
gate.

The default interaction budget is therefore one required user turn per real producer decision or
confirmed feedback submission, not one turn per report section. Evidence expansion, review,
and additional comments remain user-initiated. Where several feedback items belong to the same
decision, Report may propose them together for one confirmation rather than forcing a sequence of
near-identical panels.

### 15.6 Evidence-grounded report grammar

The exact five-field sequence is not established by research as a universal law. The inspected
books support its functions—governing topic, relevance/context, plain explanation, consequence,
and response—but also support adapting order and visible structure to the reader's purpose. The
Deep Research work supplies authority and stance constraints rather than evidence for one prose
template. The approved transfer is therefore the conditional contract in 7.2:

- one consolidated Standard response rather than one topic-reveal turn at a time;
- one producer-supported governing outcome or live decision first;
- the `TOPIC / MOTIVATION / WHAT IS IT? / IMPACT / ACTION` route for several comparable topics;
- informative, attributed topic headings such as `2/5 [TEST] Retry path remains unverified`;
- merged or omitted visible fields when redundant or explicitly inapplicable;
- `ACTION` first when the producer marks a blocker, urgent failure, or live decision;
- stable evidence references, material caveats, and cross-topic dependencies despite their
  absence from the five repeated labels; and
- job-specific structures for progress, failure, incident, evidence-audit, and single-answer
  reports.

This is an Astra synthesis and product default. The labels are user-approved; merging thresholds,
conditional order, and effects on decision quality remain testable product hypotheses. The
source-level advice and transfer limits are preserved in
the [book distillation](../docs/research/2026-08-18-astra-report-book-distillation.md); the focused
risk analysis is in the
[five-field template audit](../docs/research/2026-08-19-astra-report-five-field-template-evidence-audit.md);
and the role, attribution, framing, feedback-closure, and orchestration-boundary evidence is in the
[stance-handoff deep-research resolution](../docs/research/2026-08-19-astra-report-stance-deep-research-resolution.md).
Those sources support the distinctions and risks; decisions 10–28 remain explicit Astra synthesis
and user-approved product policy.

### 15.7 Preserved boundary and remaining implementation deferrals

`I(reporting)` remains the outbound presentation relation and `F(feedback)` is now the approved
bounded review-circulation relation. The deep-research proposal's C1-C6 names and exact schemas are
not adopted; their approved semantic obligations are expressed directly in sections 7–9 and the
six sibling contracts. The shared requirements, peer contracts, validation corpus, and roadmap
are reconciled to decisions 10–28.

Report remains read-only over lifecycle authority. It cannot approve, reject, waive, mutate a
producer artifact, reinterpret technical evidence, create cross-skill consensus, or cause a
lifecycle transition. Runtime transport, persistent storage, host adapters, schema files, tests,
installation, and lifecycle integration still require separate authorization. The
2026-08-17 interface-complete v1 implementation plan predates this amendment and must be revised
and reviewed before it can support any future runtime-execution request.
