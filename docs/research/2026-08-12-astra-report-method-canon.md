# Astra Report method canon — source audit and contract bindings

**Date:** 2026-08-12

**Scope:** the method-reference claims in `designs/astra-report.md` §§4.4, 6, 7.2,
and 11

**Status:** research record; method corrections applied to `designs/astra-report.md` on
2026-08-12; creates no runtime or source disposition

---

## 1. Bottom line

The sources support a useful Astra Report canon, but they do not support the whole
current attribution table as written. The strongest retained rules are: lead with the
material outcome or requested decision; keep the first surface complete enough for the
immediate action; separate and label optional detail; explain recorded context, reasons,
consequences, and alternatives without inventing any; preserve stable cues across exposure
and resumption; and show both what changed and what still needs attention.

Four boundaries control every use of that canon:

1. **Repository authority wins.** The design's fidelity order remains controlling:
   `fidelity > caveat completeness > structure > concreteness > simplicity > brevity`.
   No communication principle licenses Report to delete, re-grade, or invent producer-owned
   content.
2. **Direct evidence and transfer are different.** Minto, Redish, Williams, Rogers and
   Lasky-Fink, Diátaxis, Nygard, Grice, and military writing doctrine directly address forms
   of communication. Multimedia-learning and interruption studies are useful analogues, not
   direct demonstrations of an Astra Reader Brief.
3. **The contract contains the innovation.** `NOW/NEXT/DEFERRED`, the Change Story,
   `ReportEvent`, the Exposure Ledger, the numeric attention budget, and the
   delta-first-never-delta-only rule are Astra-specific syntheses. Their sources can motivate
   them; only repository validation can establish them.
4. **Several current claims must be narrowed or removed.** Before→problem→fix→after is not
   SCQA; Mayer's redundancy principle does not entail one summary layer; Diátaxis does not
   make the whole brief explanation-only; Nygard does not require rejected alternatives; and
   neither cognitive-load theory nor Grice supplies the proposed numeric budget.

This report uses short paraphrases only. The supplied books were inspected locally as
research inputs. They are not copied, linked, staged, or modified here.

## 2. Evidence method and authority labels

Each canon entry carries one of these labels:

- **D — direct support:** the source addresses the same communication operation or a close
  instance of it.
- **A — analogical support:** the source demonstrates a relevant mechanism in another medium,
  task, or population. The Astra behavior remains a hypothesis.
- **S — Astra synthesis:** the rule is a repository-specific contract assembled from source
  ideas plus Astra's authority and artifact model.
- **R — rejected attribution:** the named source does not support the claimed rule at the
  required precision.

`D` does not make a source authoritative over producer artifacts. It only establishes that a
presentation rule is faithfully attributed. Every validation reference below points to the
fixed corpus classes in `designs/astra-report.md` §11.2.

### 2.1 Local book provenance

The full SHA-256 values bind these findings to the bytes inspected. Page locators below use
the page numbers printed in the work when available; where an ebook-derived PDF has no stable
printed pagination, the locator explicitly says `local PDF page`.

| ID | Work inspected | Edition / year | SHA-256 | Access result |
|---|---|---:|---|---|
| **L1** | Barbara Minto, *The Minto Pyramid Principle* | 2003 edition | `33b90b896ee646c67214ab31973151ba5fcd9fa192b7a9354455fb7e55f4d093` | Complete enough for Part I, chapters 1 and 4 |
| **L2** | Todd Rogers and Jessica Lasky-Fink, *Writing for Busy Readers* | 2023 | `b179eaca65366e8dd8ea23d8a351cb99c3867b13c55421132b1664cb7329e8f1` | Complete; ebook-derived PDF pagination |
| **L3** | Janice (Ginny) Redish, *Letting Go of the Words* | 1st ed., 2007 | `8d2093e27bdaa55605e14b48c3f3e11b467db7366a40b8c625e48e6be5e6d920` | Complete EPUB with page markers |
| **L4** | Joseph M. Williams, revised by Joseph Bizup, *Style: Lessons in Clarity and Grace* | 12th ed., 2017 | `d9ce0d47e074412fb8bf851d545cc88581a5172c8cf4aecd117aedc8901bb343` | Complete EPUB with page markers |
| **L5** | Richard E. Mayer and Logan Fiorella, eds., *The Cambridge Handbook of Multimedia Learning* | 3rd ed., 2022 | `ea2529b884d7fed84ef05e76078ad872d501bdd494b3d188e1fbfd362c785a28` | Complete PDF; used for the multimedia principles |
| **L6** | Richard E. Mayer, *Multimedia Learning* | 3rd ed., 2021 | `57a3f43547935710dc62f3cedd2d46c5202e1ec022717dd9bab444bdb5870165` | **Incomplete preview:** opens normally but ends after early theory material; the chapters needed for segmenting, signaling, coherence, pretraining, and redundancy are absent |
| **L7** | Ruth Colvin Clark and Richard E. Mayer, *e-Learning and the Science of Instruction* | 2nd ed., 2008 | `e6f0e934e764681b2ef9d579e8bb804e0b4b7c35fab90aa086e17b58dcaabfdc` | Complete replacement PDF; corroborates the multimedia principles |

The incomplete *Multimedia Learning* file is not treated as evidence for chapters it does not
contain. The Handbook and *e-Learning* supply accessible, precisely locatable versions of the
relevant principles.

### 2.2 External primary and official sources

| ID | Source | Precise locator used | Access result |
|---|---|---|---|
| **E1** | [Diátaxis — Explanation](https://diataxis.fr/explanation/) | “Explanation and its boundaries”; “Provide context”; “Talk about the subject”; “Keep explanation closely bounded” | Accessible official source |
| **E2** | [Michael Nygard, “Documenting Architecture Decisions”](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) | “Context,” “Decision,” “Status,” and “Consequences” | Accessible original essay |
| **E3** | [H. P. Grice, “Logic and Conversation”](https://web.stanford.edu/class/psych205/papers/Grice-1975.pdf) | Original pp. 45–46, maxims of Quantity, Quality, Relation, and Manner | Accessible scan of the primary text; paraphrase only |
| **E4** | [Erik M. Altmann and J. Gregory Trafton, “Memory for Goals: An Activation-Based Model”](https://gregtrafton.com/papers/s15516709cog2601_2.pdf) | *Cognitive Science* 26 (2002), pp. 39–40 and 74–75; DOI `10.1207/S15516709COG2601_2` | Accessible author copy; publisher page exposed limited text |
| **E5** | [Chris Parnin and Robert DeLine, “Evaluating Cues for Resuming Interrupted Programming Tasks”](https://chrisparnin.me/pdf/cues-chi09.pdf) and [Microsoft Research record](https://www.microsoft.com/en-us/research/publication/evaluating-cues-for-resuming-interrupted-programming-tasks/) | CHI 2010, pp. 93–102; survey pp. 95–96, study pp. 97–100, limitations/conclusion pp. 100–101 | Accessible author copy and institutional record; ACM full text was not required |
| **E6** | [Army Regulation 25-50, *Preparing and Managing Correspondence*](https://ig.army.mil/Portals/101/Documents/CRG%20files/ARN42124-AR_25-50-007-WEB-13.pdf?ver=mw9fMy3aUKXA_RYv7pdL8g%3D%3D) | 10 Oct. 2020, §1-38(a–b), p. 7 | Official Army copy; searchable, full PDF too large for the web extractor |
| **E7** | [Marine Corps Order 3000.2J](https://www.marines.mil/portals/1/Publications/MCO%203000.2J.pdf?ver=2012-10-11-163819-940) | 1 Apr. 2011, enclosure (2), pp. 9–10, especially ¶¶1.A, 1.B, and 3.A | Accessible official directive, marked current by the Marine Corps publication page |
| **E8** | [GitHub Docs — “Marking a file as viewed”](https://docs.github.com/en/pull-requests/how-tos/review-pull-requests/reviewing-proposed-changes-in-a-pull-request#marking-a-file-as-viewed) and [GitHub product announcement](https://github.blog/news-insights/product-news/mark-files-as-viewed/) | Docs section named above; announcement “How it works” | Accessible stable official behavior |
| **E9** | [GitHub changelog — commit filtering](https://github.blog/changelog/2025-12-11-review-commit-by-commit-improved-filtering-and-more-in-the-pull-request-files-changed-public-preview/) | “Review commit-by-commit,” including the “commits since last review” selector shown in the product image | Accessible official **public-preview** evidence, not a stable contract |

## 3. Retained method canon

Every entry below includes the requested provenance, behavior, prohibition, contract field,
and validation binding. “Forbidden” means forbidden as a consequence of adopting the rule; it
does not enlarge Report's overall authority.

### C-01 — Lead with the material outcome or decision

- **Support:** **D + S.** **L1** (edition and immutable hash in §2.1), Part I, chapter 1,
  “Ordering from the Top Down,” printed pp. 5–8 (local PDF pp. 22–25); **E6** (direct official
  link in §2.2), Army Regulation 25-50 §1-38(a–b), p. 7.
- **Source principle:** Put the governing idea or main point before its supporting detail so a
  busy reader can orient quickly.
- **Astra Report behavior:** Start `NOW` with a blocking decision when one exists; otherwise
  start with the producer-authored outcome and its material consequence. Supporting evidence
  follows by stable reference.
- **Forbidden behavior:** Do not begin with process narration, background, or a generic
  “report generated” sentence while a decision or consequential outcome waits below it.
- **Contract binding:** Reader Brief `NOW`; `ReportEvent` fields `producer-authored outcome`,
  `blocking status`, and `open-decision references`.
- **Validation:** In §11.2 cases 4, 5, and 11, a blinded reader must identify the requested
  decision or material outcome from the first `NOW` item without opening Evidence. Fidelity is
  audited against the event, not judged by rhetorical force.

### C-02 — Use context–tension–answer structure only where the evidence supplies it

- **Support:** **D + S.** **L1** (edition and immutable hash in §2.1), Part I, chapter 4,
  “The Story Form,” printed pp. 34–40 (local PDF pp. 51–57).
- **Source principle:** A concise opening can move from a reader-relevant situation through a
  complicating tension to the question that the answer resolves.
- **Astra Report behavior:** In a Change Story, use recorded before-state and Finding evidence
  to establish context and problem, then present the selected fix and tested after-state.
  Treat this as an Astra mapping informed by Minto—not as SCQA itself.
- **Forbidden behavior:** Do not label `before → problem → fix → after` “SCQA,” infer what the
  reader already knows, or manufacture a dramatic complication or question.
- **Contract binding:** Reader Brief `Change Story`; `ReportEvent` fields `artifact_ref` and
  `evidence references`.
- **Validation:** In cases 15 and 16, each story element must resolve to its required artifact
  field. A missing element is named as a gap; the scorer rejects any connective claim that has
  no trace.

### C-03 — Reduce ideas, requests, and navigation effort—not merely word count

- **Support:** **D.** **L2** (edition and immutable hash in §2.1), chapter 4 “Less Is More,”
  especially local PDF pp. 49–66; chapter 6 “Design for Easy Navigation,” pp. 86–121; chapter
  9 “Make Responding Easy,” especially pp. 133–138.
- **Source principle:** Busy readers benefit when a communication limits competing ideas and
  requests, makes priority visible, groups related material, and reduces the steps needed to
  act.
- **Astra Report behavior:** Merge duplicate surfaces that share authority and consequence;
  keep distinct decisions distinct; put decision identity, options, consequences, and the ask
  together in one `NOW` unit.
- **Forbidden behavior:** Do not chase brevity by deleting a caveat or identifier, split one
  action across distant layers, or hide several requests inside one vague bullet.
- **Contract binding:** Reader Brief `NOW`, `NEXT`, and `DEFERRED`; `ReportEvent` fields
  `surface candidates`, `open-decision references`, and source-assigned consequences.
- **Validation:** In cases 3, 4, 5, and 11, count distinct reply surfaces and retrieval steps.
  The brief must reduce duplicates while retaining 100% of blocking decisions and preserving
  an address for every omitted or demoted item.

### C-04 — Put the key message in the first layer; let later layers add optional detail

- **Support:** **D + S.** **L3** (edition and immutable hash in §2.1), chapter 6, pp. 102–106
  (key-point-first and short, chunked prose) and pp. 114–121 (layering); chapter 10,
  pp. 235–240 and p. 256 (headings and grouping).
- **Source principle:** A first layer can carry the key message while links or later sections
  hold details; headings and coherent chunks help scanning.
- **Astra Report behavior:** Make `NOW` materially complete for immediate action, then use
  `NEXT`, `DEFERRED`, Change Story, and Evidence for progressively less urgent or more detailed
  material. This action-completeness requirement is Astra's extension of Redish.
- **Forbidden behavior:** Do not claim that Redish proves every layer can stand alone. Do not
  put a prerequisite fact or blocking consequence only in an optional layer.
- **Contract binding:** all Reader Brief layers, especially `NOW`; `ReportEvent` fields
  `blocking status` and source-assigned consequences.
- **Validation:** Cases 3 and 11 test stopping after `NOW`; cases 5 and 10 verify that
  progressive disclosure never suppresses a blocker or caveat.

### C-05 — Prefer visible actors, concrete actions, and familiar-to-new flow

- **Support:** **D.** **L4** (edition and immutable hash in §2.1), lesson 3, “Telling Stories:
  Characters and Actions,” pp. 28–31; lesson 5, “Managing Information: Old before New,”
  pp. 66–69.
- **Source principle:** Readers usually understand prose more easily when important actors are
  grammatical subjects, important actions are verbs, and sentences begin from familiar
  context before introducing new or complex information.
- **Astra Report behavior:** Name the producing skill or artifact as the actor when ownership
  matters; express its recorded action as a verb; connect a new consequence to the already
  named artifact or decision.
- **Forbidden behavior:** Do not turn every passive construction into active voice
  mechanically, invent an actor, or reorder information so the source-owned causal or
  chronological relationship changes.
- **Contract binding:** sentence mechanics across the Reader Brief; `ReportEvent` fields
  `producing skill`, `producer-authored outcome`, and `artifact_ref`.
- **Validation:** In cases 1, 4, and 15, a register rubric checks whether ownership and action
  are explicit and whether each new concept has an antecedent. The fidelity audit overrides
  stylistic preference.

### C-06 — Confine Diátaxis explanation rules to rationale, not the whole brief

- **Support:** **D + S.** **E1** (direct official link in §2.2), “Explanation and its
  boundaries,” “Provide context,” “Talk about the subject,” and “Keep explanation closely
  bounded”; compare its official how-to and reference categories.
- **Source principle:** Explanation develops understanding through reasons, context,
  implications, choices, and alternatives. Instruction and technical description serve
  different reader needs and should not sprawl into it.
- **Astra Report behavior:** Use explanation discipline for the Change Story and explanatory
  parts of Evidence. Render recorded reasons, constraints, consequences, and alternatives;
  route procedural detail and full reference material to their owning artifacts.
- **Forbidden behavior:** Do not describe the whole Reader Brief as “explanation only.” `NOW`
  and the approval envelope are action-facing. Do not remove the minimum instruction needed to
  identify what decision the user is being asked to make.
- **Contract binding:** Reader Brief `Change Story` and `Evidence`; `ReportEvent` field
  `evidence references` and the approval decision payload.
- **Validation:** Cases 4, 14, 15, and 18 distinguish a bounded rationale from a how-to dump or
  reference transcription while retaining every option and consequence needed to decide.

### C-07 — Render decision history from recorded context, status, and consequences

- **Support:** **D + S.** **E2** (direct original-essay link in §2.2), sections “Context,”
  “Decision,” “Status,” and “Consequences.”
- **Source principle:** A small decision record preserves the forces around one decision, the
  selected response, its status, its positive/negative/neutral consequences, and any
  supersession without rewriting prior history.
- **Astra Report behavior:** Render producer-recorded context or forces, decision, status,
  supersedes references, and consequences. Render rejected or deferred alternatives only when
  the authoritative Specification records them.
- **Forbidden behavior:** Do not attribute a mandatory rejected-alternatives field to Nygard;
  do not reconstruct rationale or alternatives from the implementation diff; do not overwrite
  a superseded decision's history.
- **Contract binding:** Reader Brief `NOW` approval unit and `Change Story`; `ReportEvent`
  fields `open-decision references`, `artifact_ref`, and `evidence references`, plus the
  approval extension's options and source-assigned consequences.
- **Validation:** Cases 4, 15, 16, and 20 compare every rendered decision fact to the producer
  artifact. Missing alternatives must appear as a gap, not as a plausible reconstruction, and
  the Exposure Ledger must not copy the user's answer.

### C-08 — Supply the information the exchange requires, with evidence, clarity, relevance, and order

- **Support:** **D as theoretical background; S operationally.** **E3** (direct primary-text
  link in §2.2), original pp. 45–46, maxims of Quantity, Quality, Relation, and Manner.
- **Source principle:** Cooperative communication supplies enough information for its purpose,
  uses adequate evidence, stays relevant, and avoids unnecessary obscurity, ambiguity, and
  disorder. Grice himself questions whether “not more than required” deserves independent
  maxim status.
- **Astra Report behavior:** Include all material facts needed for the immediate reporting
  purpose, trace claims to evidence, and order them by source-owned consequence. Let the
  fidelity order decide any conflict with brevity.
- **Forbidden behavior:** Do not derive numeric surface limits, fixed layer counts, or the
  100% decision-recall threshold from Grice. Do not use concision to erase qualifications.
- **Contract binding:** Reader Brief `NOW` and `Evidence`; `ReportEvent` fields
  `producer-authored outcome`, `surface candidates` with consequences, `blocking status`, and
  `evidence references`.
- **Validation:** Cases 10 and 11 separately score supported-claim precision, critical-decision
  recall, caveat preservation, and clarity. Passing one metric cannot compensate for failing
  another.

### C-09 — Remove extraneous material and signal organization, subject to fidelity

- **Support:** **A + S.** **L5** (edition and immutable hash in §2.1), chapter 14,
  pp. 185–198 (coherence and signaling); coherence corroborated by **L7**, chapter 7,
  pp. 133–150.
- **Source principle:** In multimedia instruction, excluding material unrelated to the
  instructional goal and adding cues to organization can improve learning under specified
  conditions.
- **Astra Report behavior:** Use stable layer headers and remove genuinely extraneous
  renderer-authored commentary. Keep producer-owned caveats and addressable deferred items.
- **Forbidden behavior:** Do not call inconvenient evidence “seductive detail,” generalize an
  instructional-media result into a universal prose law, or claim that the headers themselves
  have been empirically validated for Astra.
- **Contract binding:** Reader Brief `NOW/NEXT/DEFERRED` headers and all prose; `ReportEvent`
  fields `surface candidates` and `evidence references`.
- **Validation:** Cases 3, 10, 17, and 18 compare duplicate/noise load with fidelity. An output
  that is cleaner only because it dropped an addressable caveat fails.

### C-10 — Segment dense material and introduce necessary vocabulary before relying on it

- **Support:** **A + S.** **L5** (edition and immutable hash in §2.1), chapter 19,
  pp. 243–260 (learner-paced segmenting and pretraining); corroborated by **L7**, chapter 9,
  pp. 183–195.
- **Source principle:** In multimedia lessons, learner-controlled segments and prior knowledge
  of core component names or characteristics can help with complex material.
- **Astra Report behavior:** Break a dense brief into meaningful, labeled units and gloss a
  necessary project term on first use. Regard both as hypotheses whose value must be measured
  in Report's prose setting.
- **Forbidden behavior:** Do not equate segmenting with “exactly one idea per static prose
  chunk,” front-load a glossary unrelated to the immediate brief, or treat pretraining as a
  license to repeat the same summary in several sections.
- **Contract binding:** all Reader Brief layers, especially first-use terms in `Capsule` and
  `NOW`; the corresponding `ReportEvent` field `surface candidates`.
- **Validation:** Cases 3, 12, and the `teach` home-jurisdiction portion of case 14 compare
  comprehension and retrieval with and without the proposed chunk/gloss, while checking that
  the denser mode changes detail rather than authority.

### C-11 — Treat cognitive-load constraints as a risk model, not a numeric budget source

- **Support:** **A + S.** **L5** (edition and immutable hash in §2.1), chapter 6, pp. 73–80
  (working-memory limits and element interactivity). The evidence is strongest for complex,
  novel instructional material and is moderated by learner expertise.
- **Source principle:** Processing unfamiliar, interacting elements can exceed limited
  working-memory capacity, so presentation choices matter most for complex material and less
  for an expert's familiar material.
- **Astra Report behavior:** Use mode, ordering, layering, and explicit deferral as
  testable ways to manage dense material; allow the user-adjustable budget to remain an Astra
  product hypothesis.
- **Forbidden behavior:** Do not cite cognitive-load theory as the source of “three NOW, one
  decision, two NEXT,” or assume one density suits novices and experts equally.
- **Contract binding:** Reader Brief `NOW/NEXT/DEFERRED`; `ReportEvent` fields `surface
  candidates` with consequences and `blocking status`.
- **Validation:** Cases 3, 5, and 12 compare recall, actionability, cost, and latency across
  modes. Blocking-decision recall remains 100% regardless of the chosen density.

### C-12 — Reuse stable goal cues across exposure and resumption

- **Support:** **A + S.** **E4** (direct author-copy link in §2.2), pp. 39–40 and 74–75; the
  model requires a cue associated with the goal before suspension and available again at
  resumption.
- **Source principle:** Goal retrieval can benefit from cue continuity across interruption;
  intervening goals create interference.
- **Astra Report behavior:** Repeat stable project identity, stage, standing decisions, and
  artifact identities in a fresh Capsule when those cues were present in the earlier brief or
  authoritative chain. Treat the Capsule's benefit as a validation hypothesis.
- **Forbidden behavior:** Do not claim that any after-the-fact capsule is an experimentally
  established resumption cue. Do not replace stable IDs with paraphrases that cannot be matched
  across exposures.
- **Contract binding:** Reader Brief `Capsule`; `ReportEvent` fields `producing skill`,
  `artifact_ref`, and `open-decision references`.
- **Validation:** Case 2 must include both an earlier exposure and a later resumption. Compare
  goal/stage/decision reconstruction with stable repeated cues versus a no-cue control; a
  capsule generated only after an unanticipated interruption is recorded as a different case.

### C-13 — Combine standing context with chronological, artifact-grounded recent changes

- **Support:** **A + S.** **E5** (direct author-copy and institutional links in §2.2),
  pp. 93–102, especially survey pp. 95–96, study pp. 97–100, and limitations pp. 100–101.
- **Source principle:** Developers reconstruct both working and mental context. In a small
  controlled study, automatic chronological code-content cues improved completion success over
  notes alone and participants preferred them; resumption- and edit-lag differences were not
  statistically significant.
- **Astra Report behavior:** Pair the Capsule's standing goal/stage/decisions with a
  trace-linked chronological delta and an explicit next step. Treat this as the closest
  programmer-specific analogue, not proof that prose Capsules improve resumption.
- **Forbidden behavior:** Do not cite the 15-participant code-timeline study as validation of
  the Exposure Ledger, a lifecycle summary, or delta-only reporting. Do not reduce resumption
  to a generic recap without artifact cues.
- **Contract binding:** Reader Brief `Capsule`, `NOW`, and `NEXT`; `ReportEvent` fields
  `artifact_ref`, `producer-authored outcome`, `surface candidates`, and `evidence references`.
- **Validation:** Cases 2 and 7 compare reconstructed state and delta correctness against the
  chain and ledger ground truth. Include a standing-context-plus-delta condition and a
  delta-only control.

### C-14 — Separate BLUF from SITREP: main point first versus delta plus escalation

- **Support:** **D + S.** BLUF: **E6** (direct official link in §2.2), Army Regulation 25-50
  §1-38(a–b), p. 7. SITREP: **E7** (direct official link in §2.2), Marine Corps Order 3000.2J,
  enclosure (2), pp. 9–10, especially ¶1.A (issues requiring senior attention), ¶1.B (new
  organizations or changes only; otherwise report no change), and ¶3.A (actions completed
  since the last report).
- **Source principle:** BLUF places the main point first. This specific operational SITREP
  format separately calls out noteworthy attention items, changed state, and completed recent
  actions.
- **Astra Report behavior:** Use BLUF to order `NOW`; use the SITREP precedent to motivate a
  standing-state Capsule plus structural delta and separately visible blockers or unresolved
  attention items.
- **Forbidden behavior:** Do not call BLUF and SITREP one method, import a military reporting
  schema wholesale, or attribute Astra's modes, budget, layers, or escalation algorithm to
  either doctrine.
- **Contract binding:** Reader Brief `Capsule`, `NOW`, and `NEXT`; `ReportEvent` fields
  `producer-authored outcome`, `blocking status`, and `surface candidates` with consequence
  fields.
- **Validation:** Cases 2, 5, and 6 assert that unchanged standing state remains visible, the
  computed delta matches revisions, and every producer-marked blocker surfaces in `NOW` even
  when it exceeds the ordinary budget.

### C-15 — Invalidate prior viewed state when its underlying artifact changes

- **Support:** **D for the product behavior; S for Astra's use.** **E8** (stable official links
  in §2.2): a viewer may mark a file viewed, and a later file change removes that state and
  marks the file changed since the viewer's last view. **E9** is official evidence for a
  December 2025 “commits since last review” selector, but it was announced in public preview.
- **Source principle:** A production code-review system keeps per-viewer progress state and
  invalidates it when the underlying unit changes.
- **Astra Report behavior:** Treat a newly revised artifact as not yet exposed at that revision
  until Report appends a matching ledger entry; show its structural delta relative to the last
  exposed revision.
- **Forbidden behavior:** Do not describe GitHub's viewed flag as proof of reading,
  understanding, approval, or durable artifact exposure. Do not call the preview
  “since-last-review” selector a stable GitHub contract.
- **Contract binding:** Reader Brief `Capsule` field `last-exposure timestamp` and
  delta-bearing `NOW/NEXT/DEFERRED`; `ReportEvent` field `artifact_ref`
  (identity/revision/hash).
- **Validation:** Cases 2, 7, and 20 mutate an artifact after one logged exposure. Delta
  computation must mark the new revision unexposed, must not infer approval, and must append
  exactly one new presentation record after delivery.

## 4. Rejected or narrowed claims found by the audit

These are the source-audit findings that the same-day design revision now cites and applies. The
table preserves the audited wording and its required replacement so the correction remains
traceable.

| Current claim | Verdict | Required replacement |
|---|---|---|
| “the model already knows the content” (§4.4) | **R.** Hidden parametric recall is neither reproducible provenance nor a self-contained runtime dependency. | Carry the distilled, checkable rules in the skill, or load a pinned permitted reference. Do not depend on unversioned model memory. |
| “before → problem → fix → after is SCQA” | **R.** Minto's sequence is situation–complication–question–answer. | Call the Change Story an Astra synthesis informed by context–tension–answer ordering. |
| “a reader stopping after NOW still holds a correct after-state” attributed to Minto | **R as attribution; retain as S.** | Ground it in Astra's material-completeness and fidelity invariants, then validate it with cases 10–11. |
| Redish: “every layer usable without the next” | **Narrow.** Redish supports key-message-first layering and optional detail, not the stronger universal independence claim. | Require the first layer to carry the key message; keep `NOW` action-complete as an Astra contract. |
| Mayer segmenting means “one idea per chunk” | **R at that precision.** Segmenting research concerns learner-paced multimedia segments. | Retain meaningful prose chunks only as an analogical, testable transfer. |
| Mayer signaling directly validates `NOW/NEXT/DEFERRED` | **Narrow.** Signaling supports visible organizational cues in multimedia learning. | Treat the three headers as an Astra implementation of signaling and test them against alternatives. |
| Mayer coherence licenses cutting “seductive detail” | **Narrow.** | Remove only renderer-authored extraneous material; fidelity forbids deleting producer caveats or traceable deferred surfaces. |
| Mayer pretraining requires every term be glossed before use | **Narrow.** | Gloss only necessary project vocabulary on first use; validate prose comprehension. |
| Mayer redundancy means “exactly one summary layer; sections never restate” | **R.** The principle studies overlapping spoken, printed, and graphical instructional content, with boundary conditions. | Remove the attribution. If one-summary-layer remains, label it an Astra surface-economy hypothesis and allow deliberate standing-context repetition in the Capsule. |
| “a brief is explanation only” from Diátaxis | **R for the whole brief.** Diátaxis describes explanation as understanding-oriented and removed from direct action. | Apply explanation boundaries only to Change Story and rationale; retain minimal action and decision presentation in `NOW`. |
| Nygard requires why-this-fix and rejected alternatives | **Narrow.** Nygard requires context/forces, decision, status, and consequences, not a rejected-alternatives field. | Render alternatives only from the Specification's authoritative field. Attribute non-reconstruction to Astra fidelity. |
| Sweller and Grice ground the numeric budget | **R.** Neither source yields the proposed counts. | Keep the budget as a user-adjustable Astra hypothesis and measure it in cases 3, 5, and 12. |
| “the capsule is a resumption cue” as established fact | **Narrow to hypothesis.** The closest studies concern cue continuity and code timelines. | Say the Capsule is designed as a resumption cue; require cue exposure before interruption and validate it. |
| “SITREP/BLUF genre” supplies one mature report shape | **Narrow and split.** | BLUF grounds main-point-first ordering. The inspected SITREP format grounds recent-change reporting and attention escalation in one operational domain. |
| GitHub proves production exposure tracking or stable “changed since last review” | **R at that breadth.** Stable docs support per-viewer file state invalidated by change; the exact commit filter is preview evidence. | Cite the stable viewed-state precedent narrowly and leave the Exposure Ledger as Astra's own authority-preserving mechanism. |

## 5. Resulting binding hierarchy

The sources are consistent once their domains are kept separate:

1. **Artifact truth:** producer fields, stable IDs, consequences, blocking status, and caveats.
2. **Immediate orientation:** C-01 and C-14 put the outcome or decision first.
3. **Action completeness:** Astra's `NOW` contract retains every material decision and
   consequence even when a communication source would prefer a shorter surface.
4. **Explanatory framing:** C-02, C-06, and C-07 construct only the rationale that the chain
   records.
5. **Readable form:** C-03 through C-05 and C-08 through C-11 govern grouping, sequence,
   sentences, density, and headings subject to levels 1–3.
6. **Resumption and delta:** C-12 through C-15 motivate stable cues and change invalidation;
   the Capsule and Exposure Ledger remain Astra-specific and must earn their place through the
   §11 comparisons.

This hierarchy resolves the main collision among the references: concise-writing methods can
reduce surface area, but they cannot overrule fidelity, caveat completeness, or producer-owned
decision authority.

## 6. Validation additions implied by the audit

The current §11 corpus is broad enough to host the canon, but these controls should be explicit
when the cases are implemented:

1. **Attribution controls:** compare the current `before→problem→fix→after is SCQA` wording
   against the corrected Astra-synthesis wording; evaluators must reject the false attribution
   even if both outputs are readable.
2. **Redundancy control:** repeat standing invariants once in the Capsule and nowhere else
   unless action completeness requires them. A scorer must not mark the intentional Capsule
   repetition as a Mayer violation.
3. **Diátaxis boundary control:** present the same approved decision as (a) bounded rationale
   plus a complete action envelope and (b) explanation-only prose. The latter must fail if the
   user cannot decide from it.
4. **Resumption mechanism control:** expose stable cues before a simulated interruption, then
   compare resumption with repeated stable cues, a delta-only brief, and an after-the-fact-only
   capsule.
5. **Expertise/density control:** run `skim`, `standard`, and `deep` over the same artifact set
   with both a project-familiar and a project-new evaluator. Authority and addressability must
   remain constant.
6. **Viewed-state control:** revise an already exposed artifact without changing approval
   state. The system must invalidate exposure for the new revision and must not say that the
   decision was unapproved merely because the artifact changed.
7. **Preview-precedent guard:** no test may depend on GitHub's preview commit-filter semantics.
   The oracle is Astra's artifact revision/hash and Exposure Ledger ground truth.

## 7. Access limitations and unresolved evidence

- The supplied *Multimedia Learning*, 3rd edition, is an incomplete preview. The relevant
  method chapters are inaccessible in those local bytes. No claim in this report relies on
  absent pages.
- The Wiley and ACM publisher surfaces exposed limited text. Author-hosted or institutional
  copies supplied the precise Altmann–Trafton and Parnin–DeLine locators.
- Grice's primary text is available as a scan; this report uses paraphrase rather than
  reproducing its copyrighted expression.
- The inspected SITREP directives are authoritative but domain-specific. They do not establish
  a universal SITREP genre grammar for software reporting.
- GitHub's stable official documentation does not establish a durable, artifact-level
  “changed since last review” contract. The exact commit selector located in official material
  was announced as public preview. The stable precedent is only per-viewer viewed-state
  invalidation when a file changes.
- No empirical source directly evaluates Astra's Reader Brief, ReportEvent, Exposure Ledger,
  Change Story, surface budget, or six-skill lifecycle. Those remain repository-specific
  hypotheses subject to the §11 gates.

## 8. Recommendation

The same-day design revision corrects §§2.4, 4.4, 7.2, 11.2–11.3, and 12.1 before implementation.
The future skill must carry the fifteen retained rules above with their `D/A/S` boundaries while
preserving fidelity precedence and validation gates. No book or external source becomes a runtime
dependency merely because it informed this canon; the self-contained implementation carries only
the distilled rules and their provenance.
