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
| User | Cold answers, consequential architecture choices, approval of the calibration pack, the final decision record, evidence review, and the promotion decision | Source paraphrases or Codex's execution claims |
| Assistant | The semantic and pedagogical standard, source-grounded cards, grounded assessment, targeted teaching, and transfer challenge | The user's architecture decision, implementation effects, or Mentor's promotion |
| Codex | Private-source hashing, repository scaffolding, and—only after a user-owned decision—implementation and execution evidence for one approved narrow mechanism | Book-derived pedagogy, mastery declarations, roster changes, or phase-zero ledger changes |

The five PDFs remain outside Git. `ASTRA_MENTOR_SOURCE_ROOT` must point to their private directory;
[`sources.yaml`](sources.yaml) records only bibliographic metadata, selected chapters, stable paths,
and hashes. [`workplan.yaml`](workplan.yaml) is the sole persistent execution-state file. A source's
`canonical` or `superseded` value is source metadata, not task state.

## Card semantics

> **Pending semantic review — MENTOR-002.** This scaffold fixes only the card record shape. The
> assistant and user must still define claim-versus-synthesis boundaries, locator requirements,
> caveat preservation, scope calibration, mastery evidence, and vocabulary-only anti-patterns.

A card is one source-grounded calibration unit, not proof that a book or corpus has been covered.
The proposed record shape is:

```yaml
id:
title:

source_claims:
  - source_id:
    chapter:
    section:
    printed_pages:
    pdf_pages:
    paraphrase:

mentor_synthesis:
astra_application:
scope:
limitations:
failure_pattern:

cold_questions:
artefact_questions:
adversarial_question:
transfer_challenge:
mastery_evidence:

status: source_checked
```

No card is source-checked merely because it matches this shape.

## Pilot protocol

The first session is manual and has no `SKILL.md` runtime:

1. The user gives a cold answer without seeing the cards.
2. The assistant compares it with current Astra Critique artefacts, the five source-grounded cards,
   and concrete design contradictions or ambiguities.
3. The assistant teaches only the concepts missing from the answer.
4. The user answers a transfer challenge involving a dependency violation between individually
   valid decision units.
5. The user owns a short architecture decision record: selected model, rejected alternatives,
   authoritative state, invariants, evidence contract, unresolved risk, and reopen condition.
6. Codex implements only the approved narrow mechanism and provides code, tests, traces, evidence,
   and known limitations.
7. The user and assistant return after implementation to inspect predictions, failed assumptions,
   insufficient tests, the revised mental model, and diagnosis of a seeded failure.

Grounded assessment classifies claims as `supported`, `partially_supported`, `unsupported`,
`contradicted`, or `too_vague_to_test`. The definitions and evidence thresholds for those labels
remain part of MENTOR-002.

## Success criteria

Promotion may be considered only if the pilot yields evidence that:

- Mentor identifies at least one genuine misunderstanding or unjustified assumption;
- the user states an invariant absent from the AI proposal;
- the architecture or test strategy materially changes;
- the user can explain the final mechanism without reopening the generated specification;
- the user can diagnose an unfamiliar failure from a trace;
- Mentor reduces epistemic outsourcing rather than producing more prose; and
- the ceremony cost is acceptable.

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
- authority to create `designs/astra-mentor.md`, `skills/astra-mentor/`, schemas, Mentor tools,
  generated corpora, fixtures, or CI; or
- evidence of success merely because it asks many questions, summarizes books, produces polished
  prose, or declares understanding.
