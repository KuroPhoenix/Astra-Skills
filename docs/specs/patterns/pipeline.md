# Pattern: Pipeline

**Date:** 2026-07-29
**Status:** Draft — no cluster record written yet
**Selected when:** the **sequence** dimension is load-bearing — cluster members are ordered
stages of one procedure, carrying approval gates or irreversible effects.
**Scope:** stage mechanics — gate inventory, irreversibility ordering, resumability, and the
autonomy constraint that governs any pipeline with side effects.

**Governed by** `../condensation-policy.md`. That document owns eligibility, classification,
the six preservation obligations, the autonomy rule, composition and the seven universal
conformance evidence items.

---

## 1. Why this pattern exists, and why it is the dangerous one

Ship & VCS is the highest-usage cluster in the collision map — 17 skills, 49 July invocations
(`README.md`, *"The collision map"* → Ship & VCS row). It is also the only large cluster whose members **write**: commits, pushes,
PRs, tags, container images, deploys.

Every other pattern condenses things that read. This one condenses things that act, which makes
its failure modes different in kind rather than degree. A panel that loses a voice produces a
worse report. A pipeline that loses a gate pushes to production without asking.

The usage split is the evidence that matters. `/pr` is **39 typed against 1 agent-fired**.
`README.md`, Principles §3 (*"Provenance over frequency"*), reads that correctly: for side-effecting skills, heavy manual use is evidence
the user wants to keep control, not evidence they want to hand it over.

---

## 2. Stage interface

```yaml
stage:
  id:            string
  order:         integer
  gate:                                # null only if reversible AND effect-free
    kind:        confirm | choice | review
    prompt:      string
    on_decline:  abort | skip | branch
  effects:
    effect_free: true | false          # changes NO state anywhere, incl. local
    reversible:  true | false          # undoable by this pipeline, if not effect_free
    external:    true | false          # visible outside this machine
    scope:       string                # what it touches
    idempotent:  true | false          # re-running produces the same end state
    reconcile:   <vendored probe>      # required when external AND NOT idempotent
  preconditions: [<condition>]
  outputs:       [<artifact or state>]
  resumable_from: true | false
```

These fields are not documentation; they are inputs to mechanical checks. `effect_free` and
`reversible` drive §4 ordering and the §6.1 split point; `idempotent` and `reconcile` drive §5.

**`effect_free` is a separate field from `reversible`** because §2's gate rule and §6.1's split
both turn on "changes nothing," and `reversible: true` does not mean that. Writing a file and
deleting it again is reversible but not effect-free, and an earlier draft used "reversible AND
effect-free" as a condition while providing no field for the second half — leaving the rule
unevaluable. Running tests is `effect_free: true`; `git commit` is `effect_free: false,
reversible: true`; `git push` is `effect_free: false, reversible: false, external: true`.

`gate: null` is permitted **only** when `effect_free: true`. Every stage that changes any state
carries a gate.

---

## 3. Gate inventory — the central invariant

> **The number of user approval points must not decrease. Gates may not be merged away.**

This is the pattern's defining constraint, and it exists because gate removal is the most
attractive simplification available during a pipeline condensation. Merging `/commit` and
`/pr` and `ship` into one skill invites collapsing three confirmations into one "proceed?" —
which reads as an improvement and is a loss of three separate decisions the user was making.

Mechanically:

1. Enumerate every gate in every source skill, before condensation. This is the **baseline
   inventory**.
2. Every baseline gate maps to a gate in the condensed pipeline. One-to-one, or one-to-many.
   **Never many-to-one.**
3. Two gates may be presented in a single interaction *only if* the user can answer them
   independently — e.g. one `AskUserQuestion` with two questions, not one question covering
   both. Bundling that forces a single yes/no across two decisions is a many-to-one merge.
4. A gate may be *added*. Adding is always permitted.
5. **A gate on a stage that changes state may not be removed.** No record entry excuses it — the
   gate protects a P4 boundary, and policy §5.1 makes P4 non-waivable. An earlier draft permitted
   removal with a "given up" entry, which contradicted this section's own headline and would have
   let the central invariant be written away one record at a time.
6. The single exception is definitional rather than a waiver: a gate on a stage that is
   `effect_free: true` was never protecting anything, and reclassifying it to `gate: null` is
   permitted. The record states the reclassification and the evidence that the stage is
   effect-free. **If in doubt, the stage is not effect-free.**

Rule 3 is the one that gets violated by accident. `plan-ceo-review:874` already establishes the
house norm — *"Present each scope-expanding idea as an AskUserQuestion. The user opts in or
out"* — each decision individually, not a bundle.

---

## 4. Irreversibility ordering

> **Irreversible and external stages come last, and each is immediately preceded by its gate.**

Consequences:

1. Order stages so every reversible stage precedes every irreversible one that depends on it.
   A pipeline that pushes before it tests has ordered wrong regardless of what its gates say.
2. No irreversible stage may be reached without traversing its own gate in the same run. A gate
   satisfied in a *previous* run does not carry forward — §5 resumption must re-gate.
3. Where two stages are both irreversible, order by blast radius ascending: tag before push,
   push before deploy. A failure then leaves the smaller footprint.
4. `effects.external: true` stages additionally require that the pipeline state be durable
   before they run, so a crash mid-stage is recoverable (§5).

---

## 5. Resumability

Source skills in this cluster already do partial work — `ship`, `land-and-deploy` and `canary`
each leave the repository, remote, or deployment in an intermediate state. A condensed pipeline
must therefore be resumable, or condensation makes recovery *harder* than the skills it
replaced.

1. Stage completion is recorded durably as it happens, not at the end.
2. Resumption starts at the first incomplete stage. It does not re-run completed stages.
3. **Resumption re-gates.** Every gate on the path from the resume point forward is presented
   again. A gate approved before the crash is not evidence of approval now — the state the user
   approved against may no longer exist.
4. A stage marked `resumable_from: false` forces resumption to restart from its predecessor.
   Reserved for stages whose partial state cannot be inspected.
5. Resumption is offered, never automatic. An interrupted pipeline that resumes itself on the
   next invocation is acting without being asked.

### 5.1 Mid-stage interruption

Rules 1–5 handle interruption *between* stages. A crash **inside** an external stage is the harder
case and the one that actually happens: the tag may be pushed, the image may be half-uploaded, the
deploy may have started. Stage-boundary bookkeeping cannot tell you which.

1. Every stage with `external: true` declares either `idempotent: true` or a `reconcile` probe.
   There is no third option, and the schema makes its absence a validation failure rather than a
   discovered surprise.
2. **`idempotent: true`** — resumption re-runs the stage. Re-running `git push` of an
   already-pushed ref, or re-tagging with the same value, converges. Declaring idempotence asserts
   the *end state* converges, not that the command is a no-op.
3. **`reconcile`** — resumption runs the probe first. It inspects the external system and reports
   `not_started` / `partial` / `complete`. Resumption then skips, repairs, or re-runs accordingly.
   The probe is vendored inside the plugin like any other script (policy §11).
4. **`partial` with no repair path stops the pipeline and reports.** It does not guess, and it does
   not re-run a non-idempotent external effect on the chance that it did not land. A stopped
   pipeline with an accurate description of the intermediate state is a better outcome than a
   second deploy.
5. The reconcile probe is itself `effect_free: true`. A probe that mutates the system it is
   inspecting cannot be run on an unknown state.

This is where condensation could easily make things *worse* than the source skills. `ship`,
`land-and-deploy` and `canary` each leave a smaller intermediate state because each does less. One
pipeline spanning all three has a wider window in which a crash lands mid-effect, so it owes a
correspondingly better answer for what to do about it.

---

## 6. Autonomy — this pattern's hard constraint

Policy §6 applies to every pattern. Here it binds hardest, so it is restated concretely:

> **A pipeline containing any stage more restrictive than model-invoked is itself
> user-invoked. There is no partial mode.**

For ship & VCS that means the pipeline is **user-invoked**. One stage descended from `/pr`
(39 typed / 1 agent-fired) fixes the whole pipeline's mode, because a model-invoked pipeline can
reach that stage autonomously.

### 6.1 One skill cannot hold two modes

An earlier draft said the pipeline was user-invoked *and* that it "may run its reversible,
effect-free prefix model-invoked." **Those cannot both be true of one skill.** Invocation mode is a
property of the skill, not of a position within it. A skill the model may invoke is a skill the
model may enter — and once entered, only the gates stand between it and the writing stages. That
draft granted autonomous entry into the ship pipeline while claiming to forbid it.

The value that draft was reaching for is real, and the correct expression is **two entry points,
not one skill with a mode**:

```
astra:inspect         Tier 1 or 2a. Model-invoked. Reversible, effect-free stages only.
                      Terminates at the boundary. Cannot reach a writing stage at all —
                      not "is gated from"; the stages are not in it.

astra:ship            Tier 2b. User-invoked. Contains the writing stages, and may
                      re-run or consume astra:inspect's output.
```

The split is at the **first stage with `effects.effect_free: false`**, and it is structural: the
writing stages are absent from the read-only entry point, so no gate is load-bearing for
containing autonomy. A gate that is the only thing preventing an autonomous write is a gate one
bug away from not preventing it.

Where the stages do not split cleanly — a reversible stage that must interleave with writes — the
whole pipeline is user-invoked and no read-only entry point is offered. **The split is an
optimization, not an obligation**, and a forced split is worse than none.

### 6.2 Gates are not diluted by composition

**A stage's gate may not be waived by the pipeline.** If a stage requires confirmation standalone,
it requires confirmation as a stage. This holds regardless of §6.1: a user-invoked pipeline still
gates every writing stage, because being invoked by hand is consent to run the pipeline, not
consent to each of its effects.

---

## 7. Pattern-specific conformance evidence

In addition to policy E1–E7:

**S1 is the RED gate and S2–S8 are GREEN**, per policy E5. An earlier draft specified only checks
against the condensed pipeline, which could confirm internal consistency without establishing what
the source skills did — so a lost gate or a lost resume path would have passed.

| # | Evidence |
|---|---|
| S0 | **Source characterization (RED)** — run **each source skill separately** on a fixed corpus and record, per source: its gate points, its effect classification per stage, its resume behavior under interruption, and its declined-gate behavior. This is the baseline every check below compares against. §3 rule 1 depends on it existing. |
| S1 | **Gate inventory diff (GREEN)** — S0's baseline gates against condensed gates, demonstrating no many-to-one merge and no removal barred by §3 rule 5. |
| S2 | **Ordering proof** — no irreversible stage precedes a reversible stage it depends on; blast radius ascending among irreversible stages. §4. |
| S3 | **Gate traversal test** — a run cannot reach any irreversible stage without traversing its gate. Tested by attempting to skip. |
| S4 | **Resume test, boundaries** — interrupt at each stage boundary, resume, and confirm no completed stage re-runs and every forward gate re-presents. §5. |
| S4b | **Resume test, mid-stage** — interrupt *inside* each `external: true` stage. An `idempotent` stage must converge on re-run; a `reconcile` stage's probe must correctly report `not_started`/`partial`/`complete` against a deliberately induced state of each kind. A `partial` with no repair path must stop and report rather than re-run. §5.1. |
| S4c | **Schema completeness** — every stage declares `effect_free`; every `external: true` stage declares `idempotent: true` or a `reconcile` probe; every `reconcile` probe is itself `effect_free`. Mechanical, checkable before any run. |
| S5 | **Autonomy diff** — the condensed pipeline's invocation mode against the most restrictive source stage's. Policy E2 covers the tool/hook diff; this covers mode specifically because §6 is where this pattern is most likely to regress. |
| S5b | **Split containment** — where §6.1 offered a model-invoked read-only entry point, prove the writing stages are **absent from it**, not merely gated within it. Attempt to reach a writing stage from the read-only entry point; it must be unreachable because it does not exist there. A gate is not evidence for this check. |
| S6 | **Declined-gate test** — for every gate, declining produces the declared `on_decline` behavior and leaves no partial external effect. |

S6 is easy to omit and important: gates are usually tested by approving them. A gate whose
decline path was never exercised is a gate that may not work.

---

## 8. Composition

| With | How |
|---|---|
| **Everything else** | Pipeline is **outermost** (policy §8 rule 2). Panels, method libraries and adapter sets nest inside individual stages. |
| **Panel** | A review stage may convene a panel. The panel's `AskUserQuestion` output is *not* a pipeline gate — it is content the gate then acts on. Conflating them would let a panel's decision count against S1. |
| **Adapter set** | A session held across stages belongs to the pipeline, not the stage — teardown is the pipeline's obligation (`adapter-set.md` A5). |
| **Behavior preservation** | Overlay, and near-certain for this cluster: `/commit`, `/pr` and `build-push-ecr` carry tool and MCP declarations. |

---

## 9. Candidate clusters

| Cluster | n | Note |
|---|---:|---|
| Ship & VCS | 17 | `ship`, `land-and-deploy`, `canary`, `landing-report`, `setup-deploy`, `/pr`, `/commit`, `/build-push-ecr`, `commit-commands:*`, `changelog`, `document-release`, `resolving-merge-conflicts`, `finishing-a-development-branch`, `using-git-worktrees`, `github` (collision map, Ship & VCS row). **49 invocations — highest in the map.** `/pr`'s unconfigured Jira MCP (`README.md`, Principles §2 MCP table — *"no alternative"*) is live breakage to fix during condensation, not after. |
| Setup & config | 8 | `setup-aurora-pg-mcp`, `setup-gbrain`, `sync-gbrain`, `update-config`, `keybindings-help`, `fewer-permission-prompts`, `claude-automation-recommender`, `setup-browser-cookies`. Lower risk — effects are local config, mostly reversible. |
| Context & handoff | 5 | `context-save`, `context-restore`, `strategic-compact`, `handoff`, `nowhat`. Sequence is weak here; verify against policy §4 before selecting this pattern rather than keep-separate. |

The ship & VCS row carries a note worth acting on early: `/pr` declares
`mcp__jira__jira_add_comment` against a server that was never configured, and ships no
fallback. It ran 39 times this month and that step could not have worked once. Condensation is
when that gets a fallback (policy P6), not something to schedule afterward.
