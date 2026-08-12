# Astra Report — phase-0 design

**Date:** 2026-08-12

**Status:** Proposed phase-0 design awaiting user re-review. Records three user decisions of
2026-08-12 (existence, MVP boundary, delegated voice) and the same-day design-review
resolutions (output-only voice, `I(reporting)` typing, post-MVP adapters); the eight blocking
review findings are applied. One decision remains open: the slice-approval statement in 4.2.
Creates prose only: no runtime skill, harness, installation, retirement, push, or PR.

**Proposed public shape:** `astra-report` — the stack's single human-facing reporting surface.
It is a seventh user-facing entry point but not a seventh lifecycle authority. The roster
formula this design proposes is **six authorities, one voice**.

Astra Report renders the six authoritative artifacts — Finding Set, Understanding Report,
Approved Change Specification, Approved Delivery Roadmap and Execution Ledger, Test Evidence
Packet, Publication Record — into attention-managed communication for the user. It owns how
things are said; it never owns what is true, what is required, or what is approved. Its two
outputs are the ephemeral **Reader Brief** and the durable, append-only **Exposure Ledger**;
neither is an authoritative chain artifact in the 7.11.3 sense.

## 1. Identity and status

**Provisional name:** `astra-report`. **Status:** `proposed`. **Priority:** `now` — justified
by explicit personal value: the user's own 2026-08-12 problem statement (2.1) and three
same-day decisions drove this design; there is no usage evidence yet because the job is new.
**Candidate neighborhoods investigated:** Docs & knowledge (`cm-docs-and-knowledge`); Design &
visual is touched only through the post-MVP `diagram` adapter (`cm-design-and-visual-21`).
**User job:** When I want to act on my project's current state without re-reading the whole
record, I invoke `astra-report` for one budgeted brief of what changed and what needs my
decision. **Personal value:** explicit — quoted user statements, not inference.

### 1.1 Recorded user decisions (2026-08-12)

1. **Existence.** `astra-report` is approved as a user-facing reporting skill alongside the
   six-skill coding lifecycle. It holds no lifecycle authority.
2. **MVP boundary.** The approved scope is: a stateless Reader Brief renderer; one durable
   per-project Exposure Ledger; and reporting hooks on the six artifact contracts. Explicitly
   excluded: recall modeling, cross-project attention scheduling, proactive or self-triggered
   reporting, visual reporting, personalization beyond a verbosity mode, and summarization of
   conversation rather than artifacts.
3. **Delegated voice.** The six skills cease direct user-facing reporting. All human-facing
   reporting output of the six is delegated downstream to `astra-report`. The user's words:
   "the six skills should not be user-facing; all reports should be delegated to astra report.
   So astra report should be the downstream of all the six skills."

These are recorded decisions in the sense of the 2026-08-12 lock convention: they fix design
direction, and they revise two locked claims — the exactly-six public roster in
`docs/design-requirements.md` section 7.11 and the "public interface remains exactly six
skills" statement in `docs/six-skill-source-absorption.md` section 1. Section 12.4 lists the
coordinator reconciliation this requires. Nothing here claims behavioral absorption or
retirement of any source.

### 1.2 Interpretation resolved

Decision 3 operates in the **output direction only** — resolved by the user's design review of
2026-08-12 (**Observed**). The six remain directly invocable control surfaces and own their
intake dialogue and approval records; Report is the sole rich outbound presentation surface.
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
| **State delta** | The difference between the artifact-chain state at the user's last recorded exposure and the chain state now, expressed as change → consequence → next decision |
| **Context capsule** | The minimal opening block that restores the user's mental context: project identity, current stage, standing invariants, last exposure. Always generated fresh; never stored |
| **Attention budget** | A per-brief cap on new reply surfaces, set by mode, enforced mechanically. A rendering parameter, not a measured psychological quantity |
| **Attention escalation** | The single rule deciding when an item must surface regardless of budget: blocking user decisions always render in NOW |
| **Exposure Ledger** | Report's durable, append-only per-project record of what was shown to the user, when, covering which artifact revisions, presenting which surfaces and decisions |
| **Reader Brief** | Report's ephemeral layered output: capsule, NOW, NEXT, DEFERRED, evidence links |

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
GitHub's "changed since your last review" tracks exposure, not memory, and is trusted for
exactly that reason. A later time-decay re-glossing heuristic is admissible because its worst
case is one redundant sentence (section 12.2).

## 3. Interface and scope

### 3.1 Small public interface

One invocation with a scope and an optional mode:

```text
astra-report [scope] [--mode skim|standard|deep]
```

Scope is one artifact, a set of artifacts, or a project (meaning: the current artifact chain).
Default scope is the active project; default mode is `standard`. The same rendering core is
consumed by the six skills at their reporting moments through the typed `I(reporting)`
relation (section 8).

### 3.2 Requests that should trigger it

- "Where are we?", "what changed?", "catch me up", after any absence — resumption brief.
- "Report on X", "explain this Finding Set / spec / test results to me" — artifact brief.
- "What do you need from me?", "what's blocking?" — open-decision brief.
- Any of the six skills reaching a reporting moment (section 8.3) — delegated rendering.

### 3.3 Nearby requests that should not trigger it

- "Explain how this code works" — `astra-understand-code` owns repository state; Report owns
  artifact state.
- "Write documentation for this feature" — durable repository prose belongs to Implement
  (`document-release` disposition); standalone documentation remains the locked five-source
  deferral.
- "Summarize our conversation" — out of scope by recorded decision 2; Report reads artifacts,
  not chat history.
- "Is this finding correct?", "which artifact is right?" — judgment belongs to Critique;
  Report surfaces contradictions and never adjudicates them.
- Deployment changelogs, retros, meeting notes, internal communications with their own durable
  outputs — separate jobs outside the coding stack (absorption design section 8).

### 3.4 Intake contract

| Input | Requirement |
|---|---|
| Artifact scope | Immutable references (identity, revision, hash per 7.11.3) to one or more chain artifacts; sideways reads into peer working files are forbidden |
| Mode | `skim`, `standard` (default), or `deep`; a persisted per-project default may exist in the Exposure Ledger |
| Exposure Ledger | Read if present; absence degrades to full-state rendering (section 7.6) |
| Delegated payload | At an `I(reporting)` moment: the producing skill's ReportEvent envelope (sections 8.3–8.4) |

### 3.5 User-visible result

A Reader Brief (section 7.2), delivered in conversation. After every brief, one Exposure
Ledger append (section 7.3). Nothing else. Format delivery through adapters is post-MVP
(section 4.3).

### 3.6 Effect authority and non-goals

Report is **read-only over the lifecycle**. It never: approves, rejects, or waives anything;
reinterprets, re-grades, repairs, or re-prioritizes a source skill's severity or consequence
judgment; mutates any chain artifact or repository file; hides disagreement between artifacts;
starts, schedules, or interrupts any workflow; ranks anything outside the scope it was invoked
on; or communicates across projects. Its only durable effect is the Exposure Ledger append,
which is Report-jurisdiction bookkeeping in the same sense that the Publication Record is
Ship-jurisdiction bookkeeping — and which is never an approval record (section 8.4). Format
and visual delivery is a post-MVP non-goal (section 4.3).

### 3.7 Decisions that remain with the user

- Answering every decision a brief presents; Report only presents.
- Mode selection and the persisted default.
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
can resolve; for the two post-MVP adapters it is deferred to adapter admission (4.3).

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

**Deferral lock constraint.** `/doc`, `document-generate`, and `rtfm` are three of the five
standalone repository-documentation candidates whose deferral the user locked on 2026-08-12:
"no surviving design may claim one as a primary or secondary home without a new recorded user
decision" (absorption design section 8). Their ledger rows therefore remain **unclaimed** —
the ledger schema has no blocked state, and this design records a proposal only. The exact
decision awaiting the user is:

> Approve `astra-report` as a secondary consumer of only the recorded playbook/perspective
> slices from `/doc`, `document-generate`, and `rtfm`. Their primary jobs and registrations
> remain independent; they do not join the 92 target, become wholly absorbed, retire, or
> decide the separate docs-only-cycle question.

Until that statement is approved verbatim, the three rows stay untouched (12.3 question 1).
If the user declines, Report's plain-language playbook cites only `doc-coauthoring`,
`internal-comms`, `teach`, and the method references in 4.4; the design remains viable with
reduced source grounding. Report claims no source as a primary home in any case.

### 4.3 Post-MVP delivery adapters

`make-pdf` and `diagram` are **excluded from the MVP**: recorded decision 2 excludes visual
reporting, and format delivery defers with it. Neither is absorbed behavior; both remain
independently registered gstack skills. If later admitted: `make-pdf` may re-issue an existing
brief without content change; `diagram` is **supplemental only, never an equivalent
rendering** — the live skill produces editable repository artifacts (Mermaid, Excalidraw,
SVG, PNG) and cannot preserve a prose brief, so its file-writing effect requires explicit
authority treatment before admission. Adapter admission also requires the deferred
resolver/registration inspection (4.1.2) and, for `diagram`, a coordinator amendment to its
already-claimed row (4.5).

### 4.4 Method references: the distilled canon

Books and research enter this design as **method references** — the same class as
`prototype/LOGIC.md` and `UX_PRINCIPLES` in `astra-product-design.md` — never as census
sources: they have no invocable identifier, no entry hash in the source inventory sense, no
I/O contract, and no retirement gate. Distillation records principles with attribution;
**no source expression is reproduced**. Each reference earns its row only through checkable
rules bound to a brief obligation; the model already knows the content — the skill's value is
selection, binding, and precedence, not knowledge transfer.

| Reference | Governs | Distilled into (examples of checkable rules) |
|---|---|---|
| Minto, *The Pyramid Principle* | Brief skeleton | Answer first; before → problem → fix → after is SCQA; a reader stopping after NOW still holds a correct after-state |
| Rogers & Lasky-Fink, *Writing for Busy Readers* | Surface economy | Fewer ideas, not merely fewer words; important information findable in one glance; action effort minimized |
| Redish, *Letting Go of the Words* | Layering | Key message first; scannable chunks; every layer usable without the next |
| Mayer, *Multimedia Learning* | Chunk discipline | Segmenting (one idea per chunk), signaling (NOW/NEXT/DEFERRED headers), coherence (cut seductive detail), pre-training (gloss vocabulary before use), redundancy (exactly one summary layer; sections never restate each other) |
| Williams, *Style: Lessons in Clarity and Grace* | Sentence mechanics | Actors as subjects, actions as verbs; old-before-new information flow. (Douglas, *Writing for the Reader's Brain*, folds into this slot as the evidence-based alternate) |
| Diátaxis (Procida) | Scope refusal | A brief is explanation only: no how-to steps, no reference dumps; those route to their owners |
| Nygard, ADR practice | Decision framing | Why-this-fix and alternatives render only from recorded Critique/Spec fields, never reconstructed |
| Sweller, cognitive load theory; Grice, maxims of Quantity and Manner | Foundations | Cited as grounding for the budget and the completeness rule; not cited operationally |
| Altmann & Trafton, memory for goals; Parnin & DeLine, programmer interruption studies | Resumption | The capsule is a resumption cue; programmer-specific resumption is the closest prior art |
| SITREP/BLUF genre; GitHub "changed since last review" | System precedents | Mature delta-plus-escalation report shape; production exposure-tracking precedent |

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
| `cm-docs-and-knowledge-04` `make-pdf` | independent reference | independent | `astra-report`: post-MVP delivery adapter (4.3) | `unclaimed` → `claimed` |
| `cm-docs-and-knowledge-03` `/doc` | proposed only: independent reference with an `astra-report` slice role | — | — | **no change**: remains `unclaimed` pending the 4.2 decision |
| `cm-docs-and-knowledge-01` `document-generate` | proposed only: independent reference with an `astra-report` slice role | — | — | **no change**: remains `unclaimed` pending the 4.2 decision; the 4.1.2 resolver gap must also close before resolution |
| `cm-docs-and-knowledge-09` `rtfm` | proposed only: independent reference with an `astra-report` slice role | — | — | **no change**: remains `unclaimed` pending the 4.2 decision |
| `cm-design-and-visual-21` `diagram` | already `claimed`: retained independent (roadmap amendment 3 §10) | independent | proposed amendment: add `astra-report` as a post-MVP supplemental-delivery consumer alongside `astra-document` and `astra-interface` | stays `claimed`; amendment reconciles against the amendment-3 record |

## 5. Collision analysis

### 5.1 Why Report looked absorbable and is not

Report resembles the presentation layers scattered through the inventory: `/doc`'s clarity
rules, `internal-comms`' status formats, `landing-report`'s dashboards, each skill's final
summary. The three-part test still fails against every surviving skill: the **problem**
(explaining the artifact chain to a human under an attention budget) is owned by no lifecycle
authority; the **methodology** (trace-preserving simplification, exposure-based deltas,
surface budgeting) exists in no source; the **I/O** (immutable chain plus Exposure Ledger in,
non-authoritative layered brief plus ledger append out) matches no source's contract.
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

1. **Resumption after absence.** No source constructs a capsule plus state delta from an
   exposure record; every oracle re-explains or omits by accident.
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
4. **Decisions are never paced.** Progressive delivery applies to detail, never to decisions;
   a blocking item is never held back for rhythm. Matters when: escalation exceeds the budget
   (7.5).
5. **Briefs are ephemeral; the ledger is durable.** A brief is a view; storing views creates a
   stale quasi-authority that competes with the chain. The only durable Report record is the
   Exposure Ledger. Matters when: someone asks "where is the report?" — the answer is the
   chain plus a regenerated brief.
6. **Delta-first, never delta-only.** The capsule always restates the standing invariants
   (goal, stage, standing decisions) even when unchanged, because deltas over facts cannot see
   drift in the user's model — a fact that changed meaning without changing bytes. Matters
   when: resumption after long absence.
7. **Affordances, not questions.** More detail is offered as a stated affordance ("evidence:
   T-3, T-7 — expand on request"), never as a question, because an offer phrased as a question
   is itself a reply surface. Matters when: composing every layer boundary.
8. **No orchestration.** Report never decides whether or when to interrupt the user, never
   ranks across projects, and never starts a peer workflow. Matters when: a surfaced
   contradiction tempts an automatic Critique invocation — routing is user-mediated (3.7).
9. **Visible deferral.** DEFERRED names what was parked; silent omission is forbidden even
   below the budget line. Matters when: the user wants to veto a deferral cheaply.

## 7. Proposed skill design

### 7.1 Public shape and modes

One entry point (3.1), three modes:

- `skim` — capsule plus the single most consequential surface.
- `standard` — capsule plus budgeted NOW/NEXT/DEFERRED (7.5 defaults).
- `deep` — unbudgeted but still layered, ordered, and fidelity-ruled; for audit sessions.

Mode changes rendering density only; it never changes what exists or what is addressable.

### 7.2 Reader Brief contract

Layered, in order, each layer usable without the next (Redish rule):

| Layer | Content | Binding rules |
|---|---|---|
| **Capsule** | 2–3 lines: project identity, current stage, standing invariants, last-exposure timestamp | Always present; always fresh-generated; delta-first-never-delta-only (6.6) |
| **NOW** | Budgeted surfaces, decisions first, each as claim → consequence → what is asked; ends with the completeness statement ("nothing else requires you") when true | Layer-1 completeness-for-action: a user stopping here is not wrong about anything material. Failure test: if the user must ask "is that everything?", the brief failed |
| **NEXT** | Items that will need attention but block nothing now | Never contains a blocking decision |
| **DEFERRED** | Named parked items, one line each | Visible deferral (6.9); never empty-by-omission |
| **Change Story** | Required whenever the scope covers a change cycle (an Approved Change Specification exists): before → problem → fix → after, why this fix was selected, and the rejected or deferred alternatives | Every element renders only from recorded fields — problem from Finding IDs; why-this-fix and alternatives from the Specification's selected-solution and rejected-alternatives fields; before/after from the Understanding Report, Execution Ledger, and Test Evidence Packet — each trace-linked. A missing element is named as a gap, never invented |
| **Evidence** | Stable-ID links into artifact fields per 7.11.3 traceability | Every NOW claim carries at least one link; no orphan assertions |

Sentence-level rules from the canon bind all layers: actors as subjects; vocabulary glossed on
first use; every abstract claim paired with a concrete artifact excerpt, diff line, or number;
exactly one summary layer in the whole brief; explanation only — no how-to steps, no
reference dumps.

### 7.3 Exposure Ledger contract

One append-only record per project, Report-jurisdiction (3.6). Each entry carries, in the
identity style of 7.11.3: timestamp; brief identity and mode; the artifact identities,
revisions, and hashes covered; the surface identifiers presented, split NOW/NEXT/DEFERRED;
the decisions presented; the decisions answered, each with a pointer to the authoritative
approval record inside the producing skill's artifact; and any degradation flags (7.6).

The ledger is exposure evidence, never approval authority: the producing skill's artifact
remains the only record of what was approved. Entries are never edited; a wrong entry is
superseded by a correcting append. Absence of a ledger entry for an existing artifact revision
is itself the signal "never briefed" — no skill ever writes the ledger except Report (8.5).

### 7.4 Rendering protocol

```text
scope selection -> delta computation (chain vs ledger) -> attention allocation
(source-assigned consequence under budget + escalation) -> composition (7.2 layers,
canon rules, fidelity precedence) -> delivery (conversation; optional adapter) ->
ledger append
```

Delta computation is structural: artifact revisions and supersedes references against ledger
entries — never prose diffing. Attention allocation orders by the producing skills' own
consequence fields; Report contributes ordering and deferral only.

### 7.5 Surface budget and escalation defaults

Proposed defaults, user-adjustable (3.7): `standard` NOW carries at most three surfaces, at
most one of them a decision; NEXT at most two; everything else DEFERRED by name. `skim`: one
surface. `deep`: unbudgeted. **Escalation:** blocking decisions always render in NOW even when
that exceeds the budget; when blockers alone exceed it, NOW contains only blockers. The budget
yields to a blocker; it never hides one (6.4).

### 7.6 Failure and degradation

| Condition | Behavior |
|---|---|
| Exposure Ledger missing or unreadable | Render full-state (no delta), say so in the capsule, append a fresh ledger entry flagged `ledger-reset` |
| Artifact lacks stable identifiers | Quote verbatim with file-line anchors, flag the reporting-hook gap in DEFERRED, never invent identifiers |
| Report unavailable at a non-decision `I(reporting)` moment | The producing skill emits the degraded minimal notice of 8.5; the lifecycle never blocks on Report |
| Report unavailable at an approval request | The producing skill presents its complete minimal decision envelope (8.5) so the user can still decide informed; work stops only while awaiting the user's answer, never because Report is unavailable |
| Contradiction detected between artifacts | Surface as a NOW/NEXT item with both references; never adjudicate; routing to Critique is user-mediated |

Report is deliberately **not** a required consultant in the 7.11.2 fail-closed sense;
rendering unavailability degrades communication, not authority.

### 7.7 Architectural hypotheses

Internal seams — scope selector, delta engine, attention allocator, composer, ledger writer —
are analytical until implementation demonstrates variation. With delivery adapters deferred
post-MVP (4.3), no seam is demonstrated yet; the adapter seam becomes real only if two
adapters are admitted. Whether the delta engine and allocator are separable modules or one
pass remains a hypothesis for the comparison systems (11.1).

## 8. Delegated voice: the `I(reporting)` relation and reporting hooks

### 8.1 Direction rule

Information flowing **user → skill** (invocation, intake answers, approvals being given)
remains direct. Information flowing **skill → user** (artifact presentation, status, progress,
approval requests, failure announcements) routes through Report. Intake dialogue inside an
active skill (one clarifying question at a time) stays direct but obeys the exported contract
rules: one question per message; no unnecessary branches; no offer phrased as a question.

### 8.2 The `I(reporting)` relation

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

### 8.3 Reporting moments and the ReportEvent envelope

The six invoke `I(reporting)` at exactly five moments: authoritative-artifact completion; any
approval request; stage boundaries (entry refused, work stopped, cycle closed); explicit user
status requests; and failure or degradation announcements. Nothing else routes through
Report.

Every moment crosses the relation as one common **ReportEvent envelope**: event type (one of
the five); producing skill; artifact identity, revision, and hash per 7.11.3; a one-sentence
producer-authored outcome; blocking status; surface candidates with their source-assigned
consequence fields (8.6); open-decision references; and evidence references. Approval
requests extend the envelope with the decision payload of 8.4. The envelope is a payload
contract, not an artifact: producer-authored, consumed by Report, and reflected durably only
through the Exposure Ledger entry of the brief that rendered it.

### 8.4 Approval-request rendering

The producing skill owns the decision: its identity, options, consequence fields, and the
authoritative recording of the user's answer in its own artifact (7.11.1 approval machinery is
unchanged). Report owns wording, ordering, budget placement, and evidence links. The decision
payload extending the ReportEvent envelope is: decision identity; options with
source-assigned consequences; evidence references; blocking status. The Exposure Ledger records that the decision was
presented and answered, pointing at the producer's approval record — it is never itself the
approval record (7.3).

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

Partially satisfied by 7.11.3: stable identifiers exist (Finding IDs, requirement and
acceptance identifiers, the machine-checkable traceability chain), and supersession semantics
exist in principle — but explicit supersession **fields** are defined only by Critique and
Spec. **Four additions are required:**

1. **Typed consequence fields** on every user-relevant claim: severity or consequence,
   blocking-or-deferrable, decision-required-or-FYI — assigned by the producing skill (6.3).
2. **A common open-decision shape** across all six, so open decisions are enumerable without
   six parsers.
3. **Explicit supersession fields** for Understand Code, Implement, Test, and Ship, matching
   the Critique and Spec pattern, so delta computation (7.4) is structural across the whole
   chain.
4. **ReportEvent envelope adoption** (8.3) at every reporting moment, including the approval
   extension (8.4).

These are proposed amendments to each sibling design's artifact contract, `claimed` rows for
coordinator migration (12.4).

### 8.7 Impact on the six designs

Each sibling's user-visible-result and approval-flow sections gain an `I(reporting)`
delegation clause;
their content authority sections are untouched. This is wording migration, not authority
change. Rows stay `claimed`, never `resolved`, until the roster-wide review.

## 9. Dependencies and delivery shape

### 9.1 External components that remain separate

`make-pdf` and `diagram` (post-MVP delivery adapters, 4.3); the six slice sources (4.2, independent
registrations retained); the method references (4.4, readable citations, not dependencies);
the artifact chain storage convention (prerequisite: wherever the six persist artifacts,
Report must be able to resolve immutable references; its absence is a 7.6 degradation).

### 9.2 Peer relations

| Peer | Relation | Direction and content |
|---|---|---|
| All six lifecycle skills | `I(reporting)` | Each consumes Report's rendering capability at the 8.3 moments via the ReportEvent envelope |
| All six lifecycle skills | `I` | Report reads their immutable artifacts by reference |
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

1. At any reporting moment, manually compose the 7.2 layers under the 7.5 defaults and the
   section 6 invariants, linking evidence by the identifiers the artifacts already carry.
2. Maintain the Exposure Ledger as a hand-edited append-only file with 7.3 fields; if skipped,
   say "no exposure record — full-state brief" in the capsule and forgo deltas.
3. Use `/doc` (register), `internal-comms` (status shapes), and `doc-coauthoring` (chunking)
   as source oracles for the prose itself, under this design's precedence chain.
4. Never let manual rendering alter, re-grade, or omit-without-deferral any artifact content.

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
2. Full-chain resumption after simulated absence (capsule + delta).
3. Multi-skill overload: an aggregated run producing 30+ findings across artifacts.
4. Approval-request rendering from a typed payload.
5. Blockers exceed budget (escalation must override, 7.5).
6. Contradiction between two artifacts (surface, never adjudicate).
7. Missing ledger (degradation to full-state).
8. Missing identifiers (verbatim-quote degradation).
9. Report unavailable at an `I(reporting)` moment — both 8.5 fallbacks: the non-decision
   minimal notice, and the approval-request complete minimal decision envelope.
10. Fidelity-adversarial: a tempting simplification that would drop a caveat (must demote,
    never delete).
11. Terseness probe: layer-1 completeness — the "is that everything?" test must be answerable
    without asking.
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

### 11.3 Method and measures

Paired runs on identical artifact sets against the applicable source oracle, with repeated
trials; subjective judgments (register, clarity, layer-1 completeness) use blinded,
order-randomized evaluation. Measures: reply-surface count against budget; critical-decision
recall (no blocking decision omitted — required at 100%); supported-claim precision and
unsupported-claim rate against artifact fields; fidelity audit (every omitted or demoted item
addressable by identifier; zero deleted caveats); source-unique supported behaviors (each 4.2
slice observably survives); delta correctness against ledger ground truth; layer-1
completeness judged against the artifact set; duplicate/noise load (redundancy-rule
violations); deferral-routing accuracy (items land in the correct NOW/NEXT/DEFERRED tier
given their source-assigned consequence); actionability of NOW items; register quality
against the source oracle; ledger-append integrity; cost and latency per brief.

### 11.4 Gates and consequences

| Gate | Failure consequence |
|---|---|
| Home non-regression: no brief loses artifact facts or register quality vs the oracle | Narrow the failing playbook slice; re-derive from its source |
| Positive advantage on classes 2, 3, 4 of 11.2 | Withdraw the public interface; Report collapses to an exported style contract consumed by the six (5.4) |
| Internalization fidelity: candidate matches convener on retained behavior | Candidate blocked; convener remains the bridge |
| Invariant preservation (section 6) on classes 10, 11, 13 | Design fault, not tuning: revise this document |

### 11.5 Retirement

**None in this tranche.** No source retires on Report's account; slices leave every original's
registration untouched, and the deferred five remain deferred unless 12.3 question 1 records
otherwise. Because no retirement is proposed, no source-specific retirement gate is created;
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
statement and decisions are conversation records of 2026-08-12, quoted in 1.1 and 2.1 —
**Observed**, including the review resolution recorded in 1.2.

### 12.2 Provisional decisions

- Williams over Douglas for the sentence-mechanics slot; Douglas recorded as the alternate.
- Budget defaults in 7.5 are proposed numbers, expected to be tuned by use.
- Time-decay re-glossing is admitted as a future-safe extension (2.4) but not designed.
- The ledger file format, storage location, and brief identity scheme are later-phase work.
- Resolved by the 2026-08-12 review: the output-only interpretation of decision 3 (1.2); the
  withdrawal of the `V` relation in favor of typed `I(reporting)` (8.2); and the post-MVP
  deferral of both delivery adapters (4.3).
- Ordinary intake dialogue stays outside the Exposure Ledger (review-confirmed deferral;
  12.3 question 2).

### 12.3 Open questions (each names its consequence)

1. **Does the user approve the exact slice statement in 4.2?** Until approved verbatim, the
   `/doc`, `document-generate`, and `rtfm` rows stay `unclaimed` and Report's playbook cites
   the narrower source base (4.2); `document-generate` additionally needs its resolver
   inspection gap closed (4.1.2) before its row can resolve.
2. **Should intake dialogue append to the Exposure Ledger?** Currently no — review-confirmed
   as deferrable: dialogue outcomes land in artifacts, which Report briefs. If
   dialogue-presented facts must someday count as exposure, the six gain a ledger-append
   obligation, weakening "no skill writes the ledger except Report" (7.3).
3. **Are the 7.5 defaults right for this user?** Wrong defaults either annoy (too tight) or
   re-create overload (too loose); tunable at first use, but the shipped default shapes first
   impressions.

### 12.4 Coordinator reconciliation required

All `claimed`, never `resolved`, citing the 2026-08-12 user decisions in 1.1:

1. Amend the exactly-six roster statements: `docs/design-requirements.md` 7.11 and
   `docs/six-skill-source-absorption.md` section 1 — six lifecycle authorities plus one
   non-authoritative reporting surface that owns all rich outbound presentation; the six
   remain directly invocable control surfaces.
2. Record the `I(reporting)` typing convention as a clarifying note in the 7.11.2 relation
   vocabulary; no new relation letter is added.
3. Apply the section 4.5 row changes: four `unclaimed` → `claimed` secondary-role claims;
   the `diagram` secondary-consumer amendment against roadmap amendment 3; the three
   deferral-locked rows untouched pending 12.3 question 1.
4. Add the four reporting hooks (8.6) — consequence typing, the common open-decision shape,
   supersession fields for Understand Code, Implement, Test, and Ship, and ReportEvent
   adoption — to each sibling design's artifact contract.
5. Add the `I(reporting)` delegation clause to each sibling's user-visible-result and
   approval sections (8.7).
6. Include Report in the trigger-surface reconciliation (absorption design section 11,
   remaining-work item 3), ensuring 3.2/3.3 does not collide with Understand Code or the
   deferred documentation candidates.
