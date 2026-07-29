# Pattern: Adapter Set

**Date:** 2026-07-29
**Status:** Draft — no cluster record written yet
**Selected when:** the **substrate** dimension carries ≥2 distinct values — cluster members require
different runtime prerequisites, distinguishable by a capability probe. This pattern addresses the
substrate difference only; where the same cluster also differs at judgment or method, those select
their own patterns and all of them compose (policy §8). Nothing here assumes the priors or methods
are identical.
**Scope:** adapter mechanics — the adapter interface, the capability parity matrix, detection
ordering, and how absence is made loud.

**Governed by** `../condensation-policy.md`. That document owns eligibility, classification,
the six preservation obligations, the autonomy rule, composition and the seven universal
conformance evidence items.

---

## 1. Why this pattern exists

Two skills in the browser cluster declare themselves as another skill plus a runtime, in their
own descriptions:

| Skill | Lines | Description says |
|---|---:|---|
| `agent-browser` | 779 | the base capability |
| `electron` | 236 | *"Automate Electron desktop apps **using agent-browser via** Chrome DevTools Protocol"* |
| `agentcore` | 115 | *"**Run agent-browser on** AWS Bedrock AgentCore cloud browsers"* |
| `webapp-testing` | 95 | *"...using **Playwright**"* |

`agentcore` is not a different tool, a different method, or a different prior. It is
`agent-browser` with an AWS-hosted browser underneath, and it costs 115 lines to say so against
the base skill's 779. `electron` is the same tool reaching a running process over CDP.

This is a dimension the panel and method-library patterns cannot represent. It covers eighteen
skills in browser & QA and eight in delegation & autonomy.

---

## 2. The substrate/subject distinction

`electron` is the case that tests the classification, because it looks like both.

- **Its subject** is which application — VS Code, Slack, Figma. That varies per invocation and
  the behavioral contract does not change with it, so under policy §4 it is a **parameter**.
- **Its substrate** is a CDP connection to an already-running process. That changes the
  prerequisites (a live debug port), changes which operations are available (you cannot
  navigate a desktop app to an arbitrary URL), and is distinguishable by probe. That is an
  **adapter**.

The test from policy §4: a differing subject collapses to a parameter *only when the behavioral
contract is otherwise identical*. Here the contract does change — so `electron` is
substrate-distinct, and "which app" rides along as a parameter.

---

## 3. Adapter interface

```yaml
adapter:
  id:            string
  substrate:     string                    # what it runs on
  prerequisites: [ { name, probe, on_absent } ]
  capabilities:  [<operation>]             # what this adapter CAN do
  unsupported:   [ { operation, reason } ] # what it cannot, and why
  session:
    acquire:     <vendored script or command>
    teardown:    <vendored script or command>
  cost_class:    local | remote | metered   # informs detection order
```

`unsupported` is mandatory and may not be empty by omission. An adapter that declares no
unsupported operations is asserting full parity, and §4 will test that assertion.

`teardown` is mandatory for any adapter whose `cost_class` is `remote` or `metered`. An
AgentCore session left open bills.

---

## 4. The capability parity matrix

**This is the pattern's central mechanic, and the reason an adapter set is not a trivial
indirection.**

> Adapters are not interchangeable. The set declares, for every operation × adapter pair,
> whether it is supported — and a request for an unsupported operation **fails loudly**.

Silent degradation is the failure mode this matrix exists to prevent. A user who asks for a
local file upload through a cloud-hosted browser must be told the operation is unavailable on
that substrate, not handed a plausible-looking result from a different code path.

```
operation            agent-browser  agentcore  electron  playwright
navigate(url)              ✓            ✓          ✗         ✓
attach(pid|port)           ✗            ✗          ✓         ✗
upload(local_path)         ✓            ✗          ✓         ✓
screenshot                 ✓            ✓          ✓         ✓
```

Rules:

1. The matrix is **complete** — every operation in the union of all adapters' `capabilities`
   has a verdict for every adapter.
2. An unsupported operation raises. It never falls back to a different adapter without saying
   so, and never returns a partial result shaped like a successful one.
3. **Fallback across adapters is permitted only when the operation is supported on both and the
   substitution is announced.** Policy P6 requires absence to be loud; a substitution is a form
   of absence.
4. The matrix is generated from the adapters' declarations and checked against §6 A3, not
   hand-maintained. A hand-maintained matrix drifts, and a drifted matrix is worse than none —
   it promises parity that does not hold.

---

## 5. Detection is declared, not inferred

Detection order is a fixed, declared sequence — not a per-invocation judgment:

1. **Explicit** — the user or skill named an adapter. Nothing is probed except that adapter's
   prerequisites; if they fail, it raises. It does not silently pick another.
2. **Precondition elimination** — run each adapter's `probe`. Adapters whose prerequisites are
   absent are removed from consideration. Mechanical.
3. **Cost order** — among survivors, prefer `local`, then `remote`, then `metered`. A metered
   substrate is never selected automatically when a local one can do the job.
4. **Operation requirement** — among survivors, eliminate any adapter whose matrix marks a
   required operation unsupported.
5. **Ambiguity** — if more than one adapter survives, the declared default wins; if there is
   no declared default, ask.

Probe results are cached per session. Probing an AWS endpoint once per operation is its own
cost.

Rule 3 is an autonomy-adjacent constraint: an agent that quietly escalates to a metered cloud
browser has spent the user's money without asking. Policy §6 forbids condensation from
increasing autonomy; selecting a billable substrate by default would do exactly that under the
cover of convenience.

---

## 6. Pattern-specific conformance evidence

In addition to policy E1–E7:

| # | Evidence |
|---|---|
| A1 | Every adapter's `probe` is runnable **without its substrate present**, and returns absent rather than erroring. A probe that crashes when AWS is unreachable cannot be used for elimination. |
| A2 | Every adapter declares `unsupported` explicitly. Empty by assertion is permitted; empty by omission is not. |
| A0 | **Source capability baseline (RED)** — run a fixed operation corpus against **each original source skill** before any adapter exists, and record which operations each one actually supports on its own substrate. §6.1. |
| A3 | **Parity matrix validation (GREEN)** — every operation attempted on every condensed adapter; the observed success/failure pattern must match both the declared matrix **and** A0's baseline. A declared-supported operation that fails, a declared-unsupported operation that succeeds, or an operation a source supported that no adapter now supports, is a defect. |
| A4 | Every unsupported operation raises with the substrate named. Tested, not asserted. |
| A5 | Every `remote` or `metered` adapter has a teardown, and a run that acquires a session and exits leaves no live session behind. |
| A6 | **No automatic escalation to metered** — a run whose requirements a `local` adapter satisfies never selects a `metered` one. §5 rule 3, tested. |

### 6.1 Why A3 alone is not sufficient

A3 is this pattern's GREEN gate. Note what it compares: not conclusions (panel) and not findings
(method library), but **which operations succeed**. Substrates are distinct exactly when the matrix
rows differ, so the matrix *is* the distinctness claim.

But an earlier draft specified A3 without A0, and that is a real hole: validating the matrix
against the condensed adapters proves the matrix is honest about the **new** code. It says nothing
about what parity existed before. An adapter set could drop `agent-browser`'s local file upload
entirely, declare it unsupported everywhere, pass A3 perfectly — matrix matches observed behavior —
and have silently violated P1.

A0 supplies the baseline that makes the loss visible. Concretely: run `upload(local_path)` against
`agent-browser`, `electron` and `webapp-testing` separately first. Two support it, one does not.
That three-way result is what the condensed matrix must reproduce.

---

## 7. Composition

| With | How |
|---|---|
| **Method library** | Beneath. A playbook declares prerequisites; any adapter satisfying them runs it. `spock` (JVM) is the live case. Policy §8 rule 4. |
| **Panel** | Beneath. A seat's playbook runs on whichever adapter was selected; the persona is substrate-blind. |
| **Pipeline** | Inside a stage, or spanning stages with one session held across them — in which case teardown belongs to the pipeline, not the stage. |
| **Behavior preservation** | Overlay. `agentcore` and `vercel-sandbox` may carry credential-touching frontmatter. |

---

## 8. Cost

One adapter is active per invocation: `chassis + adapter + playbook`. Unselected adapters are
files on disk and cost nothing.

The cost that *is* real for this pattern is not context — it is **probe latency and metered
substrate spend**. §5 rule 3 and A5 exist because those are the bills this pattern can run up,
and neither appears in a token count.

---

## 9. Candidate clusters

| Cluster | n | Note |
|---|---:|---|
| Browser & QA | 18 | `agent-browser`, `browse`, `agentcore`, `electron`, `webapp-testing`, `vercel-sandbox`, `connect-chrome`, `playwright` MCP, plus QA skills. **Not all 18 are substrate** — `dogfood`, `qa`, `qa-only` are method or judgment and must be classified separately before this pattern is applied to them. |
| Delegation & autonomy | 8 | `coding-agent`, `codex`, `dispatching-parallel-agents`, `loop`, `loop-goal`, `schedule`, `nightnight`, `pair-agent`. Substrate here is the *agent runtime* — Codex vs Claude Code vs Pi. Same caution: `loop` and `schedule` are sequence, not substrate. |

Both notes make the same point. A cluster containing substrate differences is not therefore
*only* substrate differences. Policy §4 classification runs over the whole cluster first, and a
mixed cluster receives composed patterns (policy §8), not this one alone.
