# Astra Mentor pilot

**Status:** bounded experiment; not an approved Astra skill

## Experiment objective

Test whether a manually invoked, source-grounded apprenticeship protocol can expose a real gap in
the user's understanding, improve one Astra architectural decision, and help the user interpret
the resulting implementation.

Mentor v0 tests whether the user understands and owns one consequential technical decision before
AI executes it. The pilot is limited to this question:

> How should Astra Critique represent and reconcile dependency-aware decision units without
> creating a bloated, opaque convener?

The pilot must make the user state the system boundary, authoritative and derived state, module
responsibilities, invariants, dependency semantics, failure modes, evidence, observability, and
conditions for escalation or abandonment.

## Roles and authority

| Role | Owns | Does not own |
|---|---|---|
| User | Cold answers, consequential architecture choices, card approval after the cold answer, the final decision record, evidence review, and the promotion decision | Source paraphrases, source-check certification, or Codex's execution claims |
| Assistant | The semantic and pedagogical standard, source-grounded cards, grounded assessment, targeted teaching, and transfer challenge | Source-checking its own claims, the user's architecture decision, implementation effects, or Mentor's promotion |
| Source-fidelity reviewer | Claim locators, paraphrase fidelity, material caveats, and the recorded independence limit of the check | Card pedagogy, Astra decisions, or user approval |
| Codex | Private-source hashing, repository scaffolding, and—only after every external lifecycle gate is met—implementation and execution evidence for one approved narrow mechanism | Book-derived pedagogy, mastery declarations, change approval, roster changes, or phase-zero ledger changes |

The five PDFs remain outside Git. `ASTRA_MENTOR_SOURCE_ROOT` must point to their private directory;
[`sources.yaml`](sources.yaml) records only bibliographic metadata, selected chapters, stable paths,
and hashes. [`workplan.yaml`](workplan.yaml) is the sole persistent task-workflow status file. A
source's `canonical` or `superseded` value is source metadata; a card's `status` is card lifecycle
state; and the later `pilot-001.md` is session evidence. None may redefine task dependencies or
completion state.

## Card semantics

> **Status — MENTOR-002:** implemented for review, not approved. This standard and the companion
> [card template](drafts/card-template.yaml) remain non-authoritative teaching material until an
> assistant source-and-semantics review and explicit user approval are recorded in
> [`workplan.yaml`](workplan.yaml).

The five sources ground engineering concepts, not the pedagogy. Unless a future card ties a
statement to a checked claim and locator, the cold-answer sequence, question design, assessment,
provisional mastery distinctions, and lifecycle rules below are Mentor pilot policy—not validated
learning-science findings or claims attributed to the five sources.

### Purpose and granularity

A Mentor card is a source-grounded teaching unit for one transferable engineering concept. It is
justified only when the concept can change how the user reasons about a consequential technical
decision, failure, or evidence claim.

A card is not a chapter summary, a compressed replacement for the source, an Astra design
decision, a universal rule, proof of understanding, or proof that a source has been fully covered.
Its target granularity is one concept that can be stated, bounded, challenged, applied to an
artefact, and transferred to a different context.

A card is too broad when its parts have different applicability, counterexamples, or mastery
tests. It is too narrow when it merely restates a term, example, or implementation detail without
requiring transferable engineering judgement.

### Current Astra authority boundary

The pilot question does not establish that dependency-aware decision units are part of current
Critique. In `designs/astra-critique.md`, the current six-skill contract takes precedence over the
historical and deferred catalogue, panel, and chair schemas in Appendix A. Cards may use those
schemas as evidence of an unresolved design hypothesis, but may not promote them into authority.

The superseded `astra-plan` design is historical evidence, not a current public peer. Spec owns
approved change intent, Implement owns approved repository delivery, and Report may change only
presentation. Exposure to a card or report is never evidence of understanding or approval.

### Semantic layers

Every card keeps these layers separate:

1. **Source-supported claim.** A conservative, original paraphrase of what a cited passage
   supports. It identifies the exact source, chapter, section, and printed and PDF pages when
   available; preserves material qualifications; and never strengthens a heuristic into a law or
   attributes an Astra interpretation to the author. Opinionated, experience-based, contextual,
   or contested passages retain that character.
2. **Cross-source relationship.** An optional, directed relationship between two source claims.
   Allowed values are `supports`, `refines`, `limits`, `contradicts`, `operationalizes`, and
   `applies_at_different_scale`. Read each record as `from_claim_id relationship to_claim_id`; both
   IDs must exist in `source_claims`, and the explanation states how the `from` claim changes
   interpretation of the `to` claim. Semantic differences are recorded before support or
   contradiction is claimed; disagreement is not flattened into consensus.
3. **Mentor synthesis.** A derived teaching rule based on one or more source-supported claims. It
   is explicitly Mentor's interpretation, states the judgement it helps the user make, bounds
   where it is useful, and names at least one limitation or reopen condition. It should normally
   be a question, decision principle, or proof obligation rather than an absolute command.
4. **Astra application.** A concrete application to the current Astra system. It may propose an
   invariant, failure pattern, or design question absent from the sources, but must never imply
   that a source endorses Astra's architecture.

### Source fidelity

A card may carry `source_checked` status only when every source claim satisfies all of the
following:

1. The cited source section was inspected directly.
2. The paraphrase is supported by that section.
3. Nearby caveats and counterexamples that could materially change the claim were checked.
4. The edition and source ID match [`sources.yaml`](sources.yaml).
5. The locator is specific enough to reopen the passage.
6. Source content, Mentor synthesis, and Astra application remain visibly separate.

A YAML file is not source-checked merely because it parses. Cards use short original paraphrases
and do not reproduce substantial copyrighted passages. Both printed- and PDF-page locators are
available and required for the five pilot PDFs; a future source may use `null` only when it lacks a
stable corresponding locator and the limitation is recorded.

A source claim's `role` is `primary`, `supporting`, or `counterpoint` within that card.
`source_character` describes the passage (for example, a principle, heuristic, empirical finding,
example, author opinion, or competing view). Neither field silently changes evidentiary strength.
The source-fidelity reviewer must differ from the author and record the degree and limits of their
independence; otherwise the card remains `draft`. For the pilot, a fresh Codex context that did not
author the card is a practical second pass, not a claim of full independence.

### Scope, limitations, and counterpoints

Every card records `scope.applies_when`, `scope.does_not_establish`, `limitations`, and a concrete
`failure_pattern`. `does_not_establish` trains the user to state what the available evidence does
not prove. For example, passing specified tests can support those cases without establishing that
the architecture is correct, the specification is complete, or production failure modes are
covered.

A material counterpoint is retained when it changes applicability, offers a credible competing
principle, exposes a trade-off, shows a failure of the primary rule, or makes the abstraction
inappropriate at another scale or context. A card may remain useful amid unresolved disagreement;
Mentor surfaces the choice instead of making it silently.

### Grounded assessment labels

Before assigning a label, identify the claim class and apply evidence that can establish that kind
of claim:

- a source claim requires its cited passage;
- an artefact claim requires the governing artefact;
- a decision-provenance claim requires the user-owned decision record, which establishes only
  what was selected or authorized;
- an execution claim requires executable evidence from the pinned revision; and
- a predicted consequence requires an explicit argument and remains provisional until observed.

When a declared contract and runtime behaviour diverge, preserve both facts and label the narrower
claims separately: the artefact may support what should happen while execution evidence supports
what did happen. The divergence is itself a finding, not permission to ignore either source.

During a session, each consequential user claim receives exactly one label:

- `supported`: the claim is testable and its declared scope is supported by evidence appropriate
  to its claim class. It does not mean globally correct.
- `partially_supported`: a meaningful core is supported, but an important condition, boundary,
  dependency, or consequence is missing or overstated; accepting it unchanged would create a
  misleading mental model.
- `unsupported`: the claim is precise enough to evaluate, but available artefacts or evidence do
  not establish it. Missing evidence is not automatically contradiction.
- `contradicted`: evidence appropriate to the claim class demonstrates the opposite. A source
  principle qualifies only when its applicability is established and no unresolved material
  counterpoint prevents that conclusion. The contradiction must be cited or demonstrated.
- `too_vague_to_test`: the claim lacks enough precision to evaluate, such as an undefined quality,
  missing system boundary or state owner, or absent observable comparison or failure criterion.
  Mentor sharpens it before judging correctness.

### Evidence of understanding

Mentor never infers mastery from showing a card, recognition of terminology, repetition of source
wording, agreement with AI, selection of the AI recommendation, or a large number of passing
tests. Its provisional evidence ladder is:

1. `exposed` — the concept was presented;
2. `restated` — the user explains it accurately in their own words;
3. `applied` — the user uses it on the active artefact;
4. `defended` — the user handles a counterexample or competing design;
5. `operational` — the user uses execution evidence to diagnose a failure involving it; and
6. `transferred` — the user applies it to a materially different system or component.

`exposed` records an event, not mastery. The remaining terms are assessment distinctions, not
persistent analytics states. A card's `mastery_evidence` contains behaviour-based assessment
criteria, not observations about a learner; the actual observations belong in `pilot-001.md`.
Every card declares criteria for `restated` and `applied`, plus at least one of `operational` or
`transferred`; `defended` is optional at card level but may be assessed during the session.
Uncertainty is recorded when evidence is incomplete. “The user identifies a valid state that
violates the invariant and explains where it should be detected” is evidence; “the user understands
invariants” is not.

### Cold-answer rule

The user's first substantive answer is collected before targeted teaching. Before it, Mentor may
identify the decision and authoritative artefacts, define only neutral terminology needed to
understand the question, and clarify the requested output shape. It may not reveal the preferred
architecture, expose the relevant card, give answer-bearing hints, or convert the exercise into
recognition.

If the user asks for the answer instead of attempting the checkpoint, Mentor may teach it but
records no cold mastery evidence.

### Question standards

A diagnostic question tests a causal model or engineering judgement. Strong questions require the
user to identify authoritative state, state an invariant, predict a failure, distinguish similar
mechanisms, name falsifying evidence, explain what passing tests do not establish, reason about
partial recovery, place authority, or predict the result of changing a constraint. Weak questions
test definitions, memorised lists, recognition, or agreement. Every pilot card includes at least
one question grounded in the current artefact.

An adversarial question searches for a plausible case where the architecture appears to work and
ordinary generated tests pass while a critical claim or invariant is violated. It exposes a proof
gap rather than testing obscure trivia.

A transfer challenge changes at least one material property: component, state owner, failure mode,
scale, authority boundary, or evidence source. Renaming variables is not transfer. A successful
answer explains why the concept remains applicable or why its scope boundary has been crossed.

### User-owned decision and post-implementation return

After targeted teaching and challenge, the user owns the consequential architecture decision. Its
record includes the selected approach, rejected alternatives, authoritative state, critical
invariants, evidence contract, unresolved risk, and reopen condition. AI may propose or polish
these items, but the user must be able to explain them without the generated prose.

Mentor's evidence loop is not complete until separately authorized implementation evidence exists.
The Mentor decision record is not an Approved Change Specification, an Approved Delivery Roadmap,
or mutation authority. If phase-zero runtime authorization, an Approved Change Specification, an
Approved Delivery Roadmap, or explicit approval of mutation scope, execution mode, and commit
authority is absent, the decision is persisted and work stops before implementation.

When those external gates are later satisfied and Codex implements the approved narrow mechanism,
the pilot compares predicted and actual behaviour, passing tests, uncovered failure modes,
execution traces, and changed assumptions. The user diagnoses at least one unfamiliar or seeded
failure from evidence before `operational` is claimed. Implementation evidence may downgrade an
earlier assessment.

Observability-specific teaching is deferred until executable pilot behaviour exists; before
trace-diagnosis is evaluated, the canonical *Observability Engineering* source must be added and
the applicable teaching claims must be source-checked rather than inferred from general model
knowledge. SRE, security, and human-centred-AI teaching are likewise deferred until there is actual
runtime behaviour to inspect and their sources are separately authorized.

### Anti-circularity and risk-directed depth

One AI-generated chain is not sufficient proof when it proposes the architecture, implements it,
writes the tests, labels expected behaviour, evaluates the result, and declares success. Where
feasible, consequential claims use evidence with some independence: executable invariants,
specification-derived or property-based tests, mutation tests, failure injection, external
benchmarks, separate labels, runtime traces, or user-observed outcomes. Different model names
alone do not establish independence.

Mentor spends more effort where error would invalidate the system's claims: source-of-truth and
state-transition decisions, authority and security boundaries, irreversible migrations,
reconciliation, evaluation, persistent memory, retry or replay, recovery, and diagnosis-critical
observability. Routine implementation details do not receive the same ceremony. The pilot remains
manually invoked.

### Card lifecycle and approval

`status` is the sole authoritative card-lifecycle field:

- `draft`: candidate content; not teaching authority;
- `source_checked`: source fidelity has been independently reviewed; before user approval, only
  the card's checked `source_claims` and their qualifications may be used as concealed assessment
  evidence, while its synthesis and pedagogy remain non-authoritative;
- `user_approved`: explicitly approved by the user for pilot sessions; and
- `retired`: historically traceable, but unavailable for new sessions.

The records under `review` are audit metadata, not parallel state. `source_checked` requires a
completed independent `review.source_check`; `user_approved` additionally requires completed
`review.user_approval` metadata; and `retired` requires a retirement record and prohibits future
use. A substantive content change returns the card to `draft`, clears current source-check,
user-approval, and retirement metadata, and requires review again; Git retains the historical
events. A retired card may return only as a newly reviewed draft. No additional lifecycle states
are introduced during the pilot.

A card may become `user_approved` only when source fidelity is checked; the semantic layers remain
separate; caveats, counterpoints, scope, and `does_not_establish` are adequate; at least one
diagnostic question is artefact-grounded; the adversarial question probes a plausible proof gap;
the transfer challenge materially changes context; mastery evidence is observable; the card is
non-duplicative within the five-card set; and the user explicitly approves it after the cold answer
but before the card is used for teaching.

User approval authorizes the card as a teaching unit; it does not establish that its checked source
claims are true. If the user rejects a card, relevant checked source claims may still be cited
directly, but the rejected card's `mentor_synthesis`, `astra_application`, question design, and
mastery criteria are not used.

## Pilot protocol

The first session is manual and has no `SKILL.md` runtime:

1. Independently `source_checked` cards are kept hidden while the user gives and persists a cold
   answer.
2. The assistant compares it only with independently checked `source_claims` and their
   qualifications from the hidden cards, independently authoritative Astra artefacts, and concrete
   design contradictions or ambiguities. Unapproved `mentor_synthesis`, `astra_application`,
   question design, and mastery criteria may be inspected as candidate pedagogy, but may not
   support any assessment classification or mastery determination, including `supported` or
   `contradicted`.
3. The relevant cards are revealed. The user explicitly approves each card before it becomes
   teaching authority; an unapproved card is not used.
4. The assistant teaches only concepts missing from the cold answer.
5. The user answers a transfer challenge involving a dependency violation between individually
   valid decision units.
6. The user owns a short architecture decision record: selected model, rejected alternatives,
   authoritative state, invariants, evidence contract, unresolved risk, and reopen condition. This
   record does not authorize repository mutation.
7. Work stops unless the separate phase-zero, Spec, Implement, mutation, execution, and commit
   gates described above are satisfied. Only then may Codex implement the approved narrow
   mechanism and provide code, tests, traces, evidence, and known limitations.
8. Once implementation evidence exists, the user and assistant inspect predictions, failed
   assumptions, insufficient tests, the revised mental model, and diagnosis of a seeded failure.

Grounded assessment classifies claims as `supported`, `partially_supported`, `unsupported`,
`contradicted`, or `too_vague_to_test`. The definitions and evidence thresholds for those labels
remain part of MENTOR-002.

## Success criteria

Promotion may be considered only when every mandatory hygiene condition holds and at least one
positive advantage is supported.

### Mandatory hygiene conditions

All must hold:

- the cold answer is captured before targeted teaching;
- consequential assessment is grounded in evidence appropriate to the claim;
- the user remains owner of the consequential decision;
- exposure or agreement with AI is not treated as mastery;
- the user can explain the final mechanism without relying on generated prose;
- the pilot does not increase epistemic outsourcing;
- ceremony cost is acceptable; and
- no authority or mutation boundary is bypassed.

### Positive-advantage evidence

At least one must be supported:

- Mentor exposes and repairs a genuine misunderstanding or unsupported assumption;
- Mentor causes the user to add, sharpen, or reject a consequential invariant, evidence
  obligation, failure model, or authority boundary;
- Mentor provides defensible evidence that the user's existing mental model survives an
  adversarial challenge rather than changing it merely for the sake of change;
- Mentor enables diagnosis of an unfamiliar or seeded failure from execution evidence; or
- Mentor enables transfer of a concept to a materially different component or failure mode.

A changed architecture or test strategy is useful positive evidence when it occurs, but it is not
mandatory.

Meeting individual criteria does not promote Mentor. The user owns the final decision after
`MENTOR-005` evidence review.

## Non-goals

This pilot is not:

- a general software-architecture tutor;
- a substitute for Astra Critique;
- an automatic reviewer on every coding task;
- a complete curriculum or fourteen-book distillation;
- a runtime with persistent mastery analytics;
- an approved Astra superskill;
- authority to reopen phase-zero ledgers;
- a bypass around phase zero, Spec, Implement, Test, or their approval boundaries;
- authority to create `designs/astra-mentor.md`, `skills/astra-mentor/`, schemas, Mentor tools,
  generated corpora, fixtures, or CI; or
- evidence of success merely because it asks many questions, summarizes books, produces polished
  prose, or declares understanding.
