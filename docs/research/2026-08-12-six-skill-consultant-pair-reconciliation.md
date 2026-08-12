# Six-skill consultant-pair reconciliation

**Date:** 2026-08-12

**Scope:** the 15 possible forward `C` relations among the six approved coding-lifecycle skills

**Status:** accepted pair-first audit evidence; canonical amendments applied on 2026-08-12; this
record itself grants no authority

Line anchors in sections 1–5 identify the pre-amendment bytes pinned in section 7. Current
authority lives in the amended policy and designs, with completion recorded in roadmap amendment 8.

## 1. Verdict

The intended topology is the complete forward authority order:

```text
Understand Code -> Critique -> Spec -> Implement -> Test -> Ship
```

Each earlier authority can therefore consult into every later active skill: `6 choose 2 = 15`
directed pairs. This is an authority order, not a mandatory chronological workflow. Understand
Code edges activate only when the later judgment directly relies on an Understanding Report;
Critique edges activate only when a Finding Set and Critique authority are present. The normal
public flow remains `Critique -> Spec -> Implement -> Test -> Ship`, and greenfield work may begin
at Spec (`docs/design-requirements.md:440-451`, `:526-542`).

Thirteen pairs are bilaterally explicit and textually consistent. Two need local repair:

1. **Understand Code -> Critique is absent.** The policy says Understand supplies a consultant
   whenever a downstream judgment directly relies on an Understanding Report, but Understand's
   exhaustive list omits Critique and Critique declares no matching checkpoint.
2. **Understand Code -> Spec is one-sided.** Understand declares the relation and Spec consumes
   Understanding evidence, but Spec's workflow invokes only Critique and names no Understand
   checkpoint.

No other direction, authority boundary, or failure rule needs redesign. Historical reverse
evidence flows are artifact consumption (`I`) or new-cycle input, not backward `C` edges.

## 2. Common contract used for every row

The matrix abbreviates these policy-owned rules:

- **B (base inputs):** exact immutable consultant artifact identity, revision, content hash and
  relevant authority fields, plus the exact active downstream artifact identity, revision and
  content hash. No sideways peer-file reads (`docs/design-requirements.md:506-510`, `:544-556`).
- **P/D/G:** the only determinations are `pass`, `drift`, and `authority_gap`. `drift` is repairable
  only by the active downstream owner inside its current authority. `authority_gap` means a new
  upstream artifact, approved branch, or user-owned decision is required; the active operation
  stops and a new immutable cycle begins if the user continues (`:512-518`, `:564-573`).
- **F (unavailable):** a required consultant fails closed unless the user explicitly records
  acceptance of reduced assurance. Identity and hash checks never substitute for judgment
  (`:520-524`).
- **Persistent instance:** one fresh consultant represents each upstream authority for one
  downstream invocation and is reused at all named checkpoints (`:520-521`).

## 3. All 15 directed pairs

Abbreviations: **U** = Understand Code, **C** = Critique, **S** = Spec, **I** = Implement,
**T** = Test, **Sh** = Ship. `Sh` avoids collision with the canonical `H` handoff relation. `B+`
means the common immutable inputs plus the row-specific material.
Every row uses failure behavior **F**.

| # | Direction | Activation and checkpoints | Immutable inputs and consultant judgment boundary | Drift owner; `authority_gap` consequence; unavailable | Textual agreement |
|---:|---|---|---|---|---|
| 1 | **U -> C** | Only when a Finding Set judgment directly relies on an Understanding Report; selected checkpoint after the Finding Set draft and before issue, repeated after evidence or repository revision changes a relied-on fact. | B+ exact relied-on current-state claims and changed evidence. U judges factual support within the report's bounded question only; it cannot create or waive a finding. | Critique repairs only its interpretation/wording. Stale, contradicted or too-narrow report requires a new report or independently grounded evidence and stops issue. F. | **Absent / policy conflict before amendment.** Policy `:535-537` said “whenever”; U listed only S/I/T/Sh (`astra-understand-code.md:1100-1104`); Critique merely permitted supplied-artifact inspection (`astra-critique.md:963-968`). |
| 2 | **U -> S** | When the Specification directly relies on report claims; after the complete draft and before whole-revision user approval. | B+ relied-on claims and new repository evidence. U judges current-state interpretation only, never intent or solution choice. | Spec repairs its draft. Stale, contradicted or narrow evidence requires a new report or removal/re-grounding of the dependency before approval. F. | **One-sided, compatible, incomplete before amendment.** U expressly included Spec (`astra-understand-code.md:1100-1104`); Spec consumed U evidence (`astra-spec.md:1214-1216`) but its workflow named only C consultation (`:1220-1224`). |
| 3 | **U -> I** | Roadmap directly relies on a report; before Roadmap approval and again at final implementation verification. | B+ Roadmap/delivered-revision identities, exact repository claims and changed evidence. U judges whether those facts remain within the report. | Implement repairs the draft; after approval only a named task/branch can repair drift. Unsupported current state stops planning or mutation for a new report/cycle. F. | **Agreed.** U includes I; I declares activation, judgment and both checkpoints (`astra-implement.md:1242-1265`). |
| 4 | **U -> T** | Relied-on report claims are present; before Test issues its packet. | B+ tested revision, proposed packet and relied-on claims. U judges continued factual support at the tested revision, not evidence sufficiency. | Test repairs only packet interpretation. Stale/narrow report stops packet issue for renewed authority. F. | **Agreed.** `astra-test.md:953-960`, `:972-986`. |
| 5 | **U -> Sh** | Publication relies on report interpretations; during Ship's gate and before any publication effect. | B+ proposed publication/record and current revision. U judges continued factual support only. | Ship repairs only publication-owned representation. Unsupported current state stops publication for a new report/cycle. F. | **Agreed.** `astra-ship.md:1261-1284`, `:1286-1304`. |
| 6 | **C -> S** | Critique authority is present; after the complete draft and before user approval. | B+ Finding IDs, causal obligations and draft dispositions/requirements/criteria. C judges honest coverage, not selected solution. | Spec repairs the draft. Invalidated findings, out-of-envelope evidence or a new decision starts a new cycle. F. | **Agreed.** `astra-critique.md:1002-1007`; `astra-spec.md:1209`, `:1220-1229`, `:1267-1271`. |
| 7 | **C -> I** | Before Roadmap approval, at causal branch decisions, final implementation verification and PR-partition coverage. | B+ Finding Set, Roadmap/branch evidence/delivered revision. C judges Finding coverage, causal proof, instrumentation need, branch completeness and causal evidence—not delivery choices. | Implement repairs a draft or an already named task/branch only. Out-of-envelope evidence or invalid finding stops mutation and starts a new authority cycle. F. | **Agreed.** `astra-critique.md:998-1007`; `astra-implement.md:1242-1265`, `:1330-1332`. |
| 8 | **C -> T** | Before packet issue and before Test closes a Finding ID. | B+ Finding Set and proposed packet. C judges honest representation of Finding IDs, causal claims and proof obligations, not Test methodology or sufficiency. | Test repairs only its representation. Genuine failure or blocking inconclusive evidence becomes a new Critique finding/cycle. F. | **Agreed.** `astra-critique.md:1002-1007`; `astra-test.md:972-1010`. |
| 9 | **C -> Sh** | Before Ship closes a Finding ID and before publication. | B+ Finding Set and proposed publication claims. C judges whether Finding IDs are accurately resolved, contradicted, accepted or open. | Ship repairs only publication wording. Invalid Finding claims stop publication and start a new cycle. F. | **Agreed.** `astra-critique.md:1002-1007`; `astra-ship.md:1261-1284`. |
| 10 | **S -> I** | Before Roadmap approval, at branch selection, final verification and PR-partition coverage. | B+ Approved Change Specification and Roadmap/executed branch/delivered revision. S judges requirements, criteria, constraints, freedoms, semantic order and approved branches—not repository delivery choices. | Implement repairs within its draft, named task or approved branch. New behavior, branch or tradeoff requires a new approved Specification. F. | **Agreed.** `astra-spec.md:1226-1229`, `:1277-1288`; `astra-implement.md:1242-1265`, `:1330-1332`. |
| 11 | **S -> T** | Before Test issues its packet. | B+ Specification and proposed packet. S judges tested claims/outcomes against requirements, criteria, constraints and selected branch, not evidence sufficiency. | Test repairs packet claims but never weakens criteria. Out-of-contract behavior starts a new cycle. F. | **Agreed.** `astra-spec.md:1226-1229`; `astra-test.md:972-986`. |
| 12 | **S -> Sh** | During Ship's gate and before publication. | B+ Specification and proposed PR/publication. S judges one complete approved functionality and preservation of requirements, criteria, constraints, branches and non-goals. | Ship repairs representation only. Missing requirement or new scope stops publication for a new cycle. F. | **Agreed.** `astra-spec.md:1226-1229`; `astra-ship.md:1261-1284`. |
| 13 | **I -> T** | Before Test issues its packet. | B+ Roadmap, Execution Ledger, commit identities, delivered revision and proposed packet. I judges actual delivered scope, task/commit coverage, language partition and Ledger accuracy—not Test sufficiency. | Test repairs its own misstatement only. Delivery/Ledger defects stop packet issue and require a new cycle. F. | **Agreed.** `astra-implement.md:1267-1270`; `astra-test.md:953-986`. |
| 14 | **I -> Sh** | During Ship's gate and before publication. | B+ Roadmap, Ledger, atomic history, delivered revision and proposed publication. I judges delivery coverage, actual scope, language partition, line accounting and Ledger accuracy. | Ship repairs representation only. Delivery or Ledger defects stop publication for a new cycle. F. | **Agreed.** `astra-implement.md:1267-1270`; `astra-ship.md:1261-1284`. |
| 15 | **T -> Sh** | During Ship's gate and before publication; T exposes this mode specifically to Ship. | B+ Test Evidence Packet and proposed publication. T judges packet identity, freshness, adequacy, tested revision, gaps, skips, residue and exactly repeatable claims. | Ship repairs representation only. Stale or inadequate evidence stops publication for renewed Test authority. F. | **Agreed.** `astra-test.md:988-990`; `astra-ship.md:1261-1284`. |

## 4. Topology alternatives and decision

### A. Complete conditional authority DAG — recommended

Admit all 15 forward pairs in the order U -> C -> S -> I -> T -> Sh. U and C edges remain
artifact-presence conditional; later lifecycle authorities accumulate normally.

- **Advantage:** exactly satisfies the policy's “whenever” rule and the coordinator's 15-pair
  obligation; factual interpretations receive the same drift protection at Critique and Spec as
  at later stages.
- **Cost:** Critique gains one conditional checkpoint, and both Critique and Spec must distinguish
  direct reliance from casual context.
- **Why selected:** it changes no authority owner and requires only three local design repairs.

### B. Four-edge Understand star beginning at Spec — rejected

Keep U -> S/I/T/Sh but prohibit C from relying on an Understanding Report; Critique must
independently re-ground every fact it uses.

- **Advantage:** no consultant is needed during Critique.
- **Cost:** only 14 possible `C` pairs remain; repeated inspection can disagree with the report;
  the policy's “whenever a downstream judgment” sentence must gain a Critique exception.
- **Reason rejected:** it contradicts the current unqualified policy and the recorded 15-pair
  coordinator target without an authority benefit.

### C. Finalization-only U -> C gate — viable but not selected

Admit U -> C, but invoke it only once on the final Finding Set draft immediately before issue,
without an earlier draft checkpoint or an additional changed-evidence checkpoint.

- **Advantage:** preserves the 15-pair topology with the smallest invocation surface.
- **Cost:** a stale or misread current-state premise can shape causal work and be discovered only
  at finalization, increasing discarded analysis. It also leaves the policy's persistent-instance
  checkpoint reuse less useful for Critique.
- **Reason not selected:** the recommended two-moment rule invokes no extra consultant instance;
  it reuses one instance and catches factual drift before it compounds.

## 5. Applied coordinator amendments

The coordinator applied these amendments after accepting option A. This record describes their
scope; the governing text remains the cited policy, designs, and roadmap rather than this audit.

1. **`docs/design-requirements.md`, replacing the cumulative table in §7.11.2:** record:

   *“For pair reconciliation, the forward authority order is Understand Code -> Critique -> Spec
   -> Implement -> Test -> Ship, yielding 15 admissible directed consultant pairs. This order does
   not add Understand Code to the chronological lifecycle. Every Understand edge is conditional
   on direct reliance on an Understanding Report; every Critique edge is conditional on present
   Finding Set authority.”*
2. **`designs/astra-understand-code.md` §11.2:** change “It participates in Spec, Implement, Test,
   or Ship” to “It participates in Critique, Spec, Implement, Test, or Ship.” Add that Critique
   consults after its Finding Set draft and before issue, while Spec consults after its complete
   draft and before whole-revision approval, only when each draft directly relies on report claims.
3. **`designs/astra-critique.md` §11.3:** add a conditional U checkpoint before issuing a relied-on
   Finding Set and after changed repository evidence affects a relied-on fact. Pass the report and
   draft identities, exact relied-on claims and changed evidence. State that U judges current-state
   support only; Critique owns any in-authority draft repair, and a stale/contradicted/too-narrow
   report returns `authority_gap`. Broaden the Finding Set's consultant-history field to retain the
   inbound Understand determination and report identity alongside the Finding Set and downstream
   consultation identities.
4. **`designs/astra-spec.md` §11.1:** after compiling the complete draft, conditionally invoke U
   before C whenever the draft directly relies on an Understanding Report; repair U `drift`, stop
   on U `authority_gap`, then run the existing C gate and request whole-revision approval. Add the
   U determination to the exact approved revision's consultant history.

No changes were necessary in Implement, Test, or Ship: their U edges and all remaining cumulative
edges already agreed. The coordinator re-ran the matrix against the amended text and recorded the
accepted topology in roadmap amendment 8 before calling the pair half complete.

## 6. Explicit deferrals

This pair-first record deliberately does **not** reconcile or change:

- the final shared trigger surface;
- `astra-report` or any reporting delegation;
- runtime consultant schema, serialization, process, harness or corpus;
- source allocation, collision/reference ledgers, claim/resolution state or retirement gates;
- runtime skills, installation, source deletion or retirement; or
- pushes, PRs, releases or deployment effects.

The old 2026-08-04 report contributes only its observed/mismatched/one-sided/absent audit method
(`docs/research/2026-08-04-cross-design-reconciliation.md:505-550`). Its eight-peer topology,
artifact-consumption rows and superseded Plan/Debug roles have no present authority.

## 7. Provenance

Full SHA-256 values record the exact pre-amendment workspace bytes inspected for this proposal:

| Role | File | SHA-256 |
|---|---|---|
| Governing policy | `docs/design-requirements.md` | `8a0f4a7574c6eaef4aea4efff6a1ca338648759e61d0907a0972415141f700ac` |
| Consultant authority | `designs/astra-critique.md` | `fc1aa9b8a86cc0b36e4e594ea2f4a60397eb78af3011e4e0f44939281fcb0178` |
| Consultant authority | `designs/astra-understand-code.md` | `bd9fe987a8f5bbf7720dd7eafd57a23453397e51d20585ee221c36cc49b90551` |
| Consultant authority | `designs/astra-spec.md` | `36f53ffd188f21e3941e94fb42909cac7aeeecc59a0cd95fc44dc0424adba0d9` |
| Consultant authority | `designs/astra-implement.md` | `38c7fb294b1de2df677e2beea9aecda42d6d31cdd558ae7bd098a2f3b6317842` |
| Consultant authority | `designs/astra-test.md` | `8ba726c9acb00adecff7a54810501c96086d4b974f1dc62295e9fcc3e09af665` |
| Consultant authority | `designs/astra-ship.md` | `af264431beeb4c1de5c41b7d27ece1ff15a3b868a0b526cdfe75df09e492804e` |
| Coordinator order | `docs/design-roadmap.md` | `a300ed4ee87ff7d6626292c22bed7b21e8f1ef786057fc6f4fce6221b3e8f429` |
| Coordinator work list | `docs/six-skill-source-absorption.md` | `df3b8b763a37d56d25b29de0c555d6e242f31cae1c68fb140fe628e165f27e3c` |
| Historical method only | `docs/research/2026-08-04-cross-design-reconciliation.md` | `b431ddfe350923350eb28765b4b337264ec1c9af44530320ac210e4e68de6182` |

Repository baseline at inspection: `a1369f6881c17ba19db2d28a7d77728873e8bd06`. These are
workspace-byte hashes, not claims that every file was clean or that this proposal was committed.
