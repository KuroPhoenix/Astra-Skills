# Astra phase 0

**Date:** 2026-07-30
**Status:** Scope approved; revised for agent review

## 1. Authority and ownership

Phase 0 derives a personalized Astra roster from the current inventory. This document owns:

- phase scope and completion criteria;
- global accounting for collision-map occurrences;
- global dispositions for reference and dangling entries; and
- coordination between independently produced skill designs.

`docs/design-requirements.md` is the sole contract for the content, evidence, workflow, and
review of each per-skill design. It intentionally does not repeat those requirements here.

The README remains source inventory. Its collision-map rows are candidate neighborhoods, not
decided skills. Restored and superseded documents are evidence, not governing interfaces.
The authority order and the rule for resolving scope-versus-content conflicts are defined in
`docs/design-requirements.md` section 2.

## 2. Outcome

Phase 0 resolves the inventory into a personalized, non-colliding roster for project
development. It answers:

- which skill jobs the user actually wants;
- which sources inform each job;
- which apparent clusters should merge, split, remain separate, or be excluded;
- which live reference skills should remain independently addressable; and
- what the user can invoke manually until an Astra skill is implemented.

The collision map is evidence to investigate. The final roster count must emerge from the
analysis; it is not required to match the README's 17 neighborhoods.

Phase 0 produces designs only. It does not create a `SKILL.md`, implement a router or runtime,
retire a source, or claim behavioral preservation.

## 3. Selected approach

Use the README's collision map as candidate evidence, then derive the roster from inspected
sources and the user's project-development needs.

This approach preserves traceability without predetermining the answer. A neighborhood may
produce one skill, several skills, part of a cross-neighborhood skill, no personalized skill,
or a set of retained independent sources.

## 4. Active repository layout

```text
README.md
docs/
  design-requirements.md
  phase-0.md
designs/
  astra-critique.md
skills/
```

| Path | Owns |
|---|---|
| `README.md` | Source inventory, usage observations, and the candidate collision map |
| `docs/design-requirements.md` | The normative contract for every per-skill design |
| `docs/phase-0.md` | Phase scope, global ledgers, coordination, and acceptance |
| `designs/<astra-name>.md` | One proposed Astra skill's evidence, interface, distinctions, and high-level design |
| `designs/astra-critique.md` | Restored critique condensation plan and worked design, pending normalization against the design requirements |
| `skills/` | Reserved for later implementation; empty during phase 0 |

No other active specification or pattern directory is required. Superseded material remains
recoverable through Git history.

## 5. Collision source-claim ledger

This document owns the authoritative ledger for all 179 collision-map occurrences in
README.md section “The collision map.” The ledger is populated during phase-0 execution and
must contain one row per occurrence, including repeated appearances of the same source.

The occurrences span four delivery mechanisms, enumerated in README section “Four source
categories, not three.” Two of them are invisible to a directory scan: 54 personal skills nest
under the single `gstack/` entry, and 12 harness built-in skills have no path and no manifest at
all. **Open:** a built-in cannot produce the immutable revision or content hash that
`docs/design-requirements.md` section 4.1 requires, so the provenance rule needs either a
version-pinning alternative or an explicit exception before those 12 rows can resolve.

Each row records:

| Field | Rule |
|---|---|
| `occurrence_id` | Stable identifier for this README occurrence, including its candidate neighborhood |
| `source_id` | Exact skill, command, agent, tool, server, hook, or other identifier |
| `component_type` | Preserve the actual delivery shape |
| `availability` | Live, disabled, missing, dangling, or recovered |
| `candidate_neighborhoods` | Every README neighborhood in which the source occurs |
| `primary_disposition` | Proposed Astra design, independent reference, defer, exclude, or duplicate occurrence |
| `primary_home` | Exactly one design or independent disposition when resolved; `unassigned` while open |
| `secondary_roles` | Zero or more other designs the source informs without transferring ownership |
| `claim_status` | `unclaimed`, `claimed`, or `resolved` |
| `evidence` | Link to the design and its source-evidence row |

### 5.1 Claim and reconciliation protocol

One phase-0 coordinator edits this ledger. Design agents do not concurrently edit this
document.

1. Before assigning a neighborhood, the coordinator reserves its occurrences as `claimed` and
   records the provisional design owner.
2. An agent may inspect any source needed to understand its job, including sources outside the
   assigned neighborhood. A ledger claim controls disposition ownership, not read access.
3. The agent records proposed ledger changes in its assigned design: primary dispositions,
   primary homes, secondary roles, and cross-neighborhood dependencies.
4. Between work waves, the coordinator applies those changes, rejects conflicting primary
   claims, and records unresolved conflicts.
5. After all draft designs exist, the coordinator performs one roster-wide trigger and
   ownership reconciliation. Only then are rows marked `resolved`.

The known repeated occurrences—`pair-agent`, `office-hours`, and `skillify`—are not the whole
overlap set. Semantic evidence can cross neighborhoods even when an identifier appears only
once. For example, Astra Critique may inspect `review` and the independent `cso` reference to
test whether code-structure and test-evidence judgments represent distinct decision policies.
That secondary role does not silently move either source's primary home.

Every resolved occurrence has exactly one primary disposition. A source may have several
secondary roles, but those roles must be explicit.

## 6. Reference and cleanup ledger

This document also owns the disposition ledger for entries outside the collision map:

- every live reference skill in the README's Language / stack, Shell, and Hugging Face groups;
  and
- every one of the 133 dangling science-collection symlinks.

The coordinator expands grouped inventory such as `huggingface-skills:*` into exact source
identifiers before marking phase 0 complete. Each row records:

| Field | Rule |
|---|---|
| `source_id` | Exact reference or dangling entry |
| `component_type` | Actual delivery shape |
| `location` | Live registration, path, or dangling path |
| `availability` | Live, missing, or dangling |
| `disposition` | `keep`, `defer`, or `exclude` |
| `reason` | User value and evidence supporting the disposition |
| `consuming_designs` | Designs that use it as a reference or secondary input |
| `evidence` | Inspected revision or content hash, or an explicit unavailable record |

Per-skill designs mention only the references they consume. This ledger provides global
coverage and keeps retained reference skills independently addressable. An exclusion means
“not included in the personalized roster”; it does not authorize deletion.

## 7. Phase workflow

1. The coordinator inventories both ledgers and reserves a bounded work assignment.
2. Each agent produces or revises one file under `designs/` according to
   `docs/design-requirements.md`.
3. The coordinator reconciles proposed ledger changes between work waves.
4. After all drafts exist, the coordinator compares triggers and source ownership across the
   whole roster.
5. The user reviews the resulting roster, exclusions, priorities, and unresolved questions.

Assignments may run in parallel after claims are reserved. They do not assume peer designs
already exist; roster-wide comparison is a coordinator pass over the completed drafts.

## 8. Deferred work

Phase 0 excludes:

- creating or editing Astra `SKILL.md` files;
- exact prompts, schemas, hooks, agents, scripts, or tool declarations;
- plugin packaging, installation, namespacing, or host-version pinning;
- routers, autonomous invocation, tiers, caches, promotion, tuning, or telemetry;
- persistent runtime state or universal composition/error interfaces;
- conformance harnesses and runtime preservation fixtures; and
- disabling, uninstalling, deleting, or retiring existing sources.

Implementation begins only after the user selects a reviewed design. Shared runtime modules
are extracted only after at least two implementations demonstrate the same seam.

## 9. Acceptance criteria

Phase 0 is complete when:

1. **The ledgers reconcile against the measured inventory.** Every invocable skill, command,
   agent, MCP server, hook, and LSP server present on this machine appears in the collision
   source-claim ledger, the reference and cleanup ledger, or an explicit out-of-scope record.
   Coverage is established by diffing the ledgers against the machine — the procedure in README
   section “Coverage check” — never by reading these documents alone. A source absent from the
   collision map is not thereby out of scope; it is unaccounted for.
2. Every collision-map occurrence has a resolved row in the collision source-claim ledger.
3. Every live reference and every dangling entry has a `keep`, `defer`, or `exclude` row in the
   reference and cleanup ledger.
4. Every occurrence has exactly one primary disposition, and every secondary role names its
   primary home.
5. Every proposed Astra skill complies with `docs/design-requirements.md`, including
   `status: proposed`, a `now` / `next` / `later` priority, and evidence of personal value.
6. Every proposed skill has one distinguishable job and survives the roster-wide trigger
   comparison.
7. Every manual bridge is usable, or its missing prerequisite and consequence are named.
8. No agent, MCP server, hook, LSP server, command, or other component is flattened into
   prompt text without an explicit disposition.
9. Reference skills remain independently addressable.
10. The final roster count emerges from the evidence rather than being forced to equal 17.
11. No implementation, runtime infrastructure, behavioral-preservation claim, or source
    retirement is required to use the roster.
12. README and the active documents use the layout and authority model in section 4.
13. Existing skills, plugins, and unrelated `.idea/` files remain untouched.
