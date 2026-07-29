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
(`README.md:399`). It is also the only large cluster whose members **write**: commits, pushes,
PRs, tags, container images, deploys.

Every other pattern condenses things that read. This one condenses things that act, which makes
its failure modes different in kind rather than degree. A panel that loses a voice produces a
worse report. A pipeline that loses a gate pushes to production without asking.

The usage split is the evidence that matters. `/pr` is **39 typed against 1 agent-fired**.
`README.md:172` §3 reads that correctly: for side-effecting skills, heavy manual use is evidence
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
    reversible:  true | false
    external:    true | false          # visible outside this machine
    scope:       string                # what it touches
  preconditions: [<condition>]
  outputs:       [<artifact or state>]
  resumable_from: true | false
```

`effects.reversible` and `effects.external` are the fields that drive §4 ordering and §5
autonomy. They are not documentation; they are inputs to mechanical checks.

`gate: null` is permitted only for a stage that is both reversible and effect-free — running
tests, computing a diff. Every stage that writes anything carries a gate.

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
5. Removing a gate requires the record's "given up" section (policy §10 section 9) to name it,
   with a reason, and requires that the stage behind it be reversible and non-external.

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

---

## 6. Autonomy — this pattern's hard constraint

Policy §6 applies to every pattern. Here it binds hardest, so it is restated concretely:

> **The condensed pipeline's invocation mode is the most restrictive among its stages.**

For ship & VCS, that means the pipeline is **user-invoked**. One stage descended from `/pr`
(39 typed / 1 agent-fired) is sufficient to fix the whole pipeline's mode, because a
model-invoked pipeline can reach that stage autonomously.

Two further constraints specific to sequences:

- **A stage's gate may not be waived by the pipeline.** If a stage requires confirmation
  standalone, it requires confirmation as a stage. Composition does not dilute authority.
- **Partial autonomy is expressible and preferred.** A pipeline may run its reversible,
  effect-free prefix model-invoked and stop at the first gate. That preserves the convenience
  motivating condensation without granting write authority. Where a cluster's stages split
  cleanly at the first irreversible effect, prefer this over making the whole pipeline
  user-invoked.

The last point is the one worth implementing carefully: it is how this pattern delivers value
without the autonomy creep that would otherwise be its price.

---

## 7. Pattern-specific conformance evidence

In addition to policy E1–E7:

| # | Evidence |
|---|---|
| S1 | **Gate inventory diff** — baseline gates from all source skills against condensed gates, demonstrating no many-to-one merge. §3. |
| S2 | **Ordering proof** — no irreversible stage precedes a reversible stage it depends on; blast radius ascending among irreversible stages. §4. |
| S3 | **Gate traversal test** — a run cannot reach any irreversible stage without traversing its gate. Tested by attempting to skip. |
| S4 | **Resume test** — interrupt at each stage boundary, resume, and confirm no completed stage re-runs and every forward gate re-presents. §5. |
| S5 | **Autonomy diff** — the condensed pipeline's invocation mode against the most restrictive source stage's. Policy E2 covers the tool/hook diff; this covers mode specifically because §6 is where this pattern is most likely to regress. |
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
| Ship & VCS | 17 | `ship`, `land-and-deploy`, `canary`, `landing-report`, `setup-deploy`, `/pr`, `/commit`, `/build-push-ecr`, `commit-commands:*`, `changelog`, `document-release`, `resolving-merge-conflicts`, `finishing-a-development-branch`, `using-git-worktrees`, `github` (`README.md:399`). **49 invocations — highest in the map.** `/pr`'s unconfigured Jira MCP (`README.md:165`) is live breakage to fix during condensation, not after. |
| Setup & config | 8 | `setup-aurora-pg-mcp`, `setup-gbrain`, `sync-gbrain`, `update-config`, `keybindings-help`, `fewer-permission-prompts`, `claude-automation-recommender`, `setup-browser-cookies`. Lower risk — effects are local config, mostly reversible. |
| Context & handoff | 5 | `context-save`, `context-restore`, `strategic-compact`, `handoff`, `nowhat`. Sequence is weak here; verify against policy §4 before selecting this pattern rather than keep-separate. |

The ship & VCS row carries a note worth acting on early: `/pr` declares
`mcp__jira__jira_add_comment` against a server that was never configured, and ships no
fallback. It ran 39 times this month and that step could not have worked once. Condensation is
when that gets a fallback (policy P6), not something to schedule afterward.
