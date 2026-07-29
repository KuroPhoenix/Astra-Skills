# Astra personal skill roster design

**Date:** 2026-07-29
**Status:** Scope approved; written-spec review pending

## 0. Authority

This document is the authoritative phase-0 design. It supersedes the README's earlier runtime,
packaging, tiering, and retirement proposals and the policy/pattern specification family.

The README remains source inventory until phase 0 rewrites it. Its collision-map rows are
candidate neighborhoods, not decided personalized skills. When this design conflicts with the
README or a superseded specification, this design governs.

## 1. Outcome

Phase 0 resolves the existing collision map into a personalized, non-colliding roster of skills
for project development. It also decides which live single-purpose reference skills remain
available beside that roster.

This phase answers:

- Which skill jobs does the user actually want?
- Which existing skills inform each job?
- Which apparent clusters must split because they contain different jobs?
- Which entries are true duplicates, complementary methods, references, dead entries, or not
  useful to this user?
- What should each personalized skill eventually be called and when should it be invoked?

It does not implement those skills or claim that any source skill can be retired. Until a
personalized skill is implemented and validated, the roster tells the user which existing skill
or skills to invoke manually.

## 2. Why the earlier design was too large

The earlier design treated Astra as a runtime framework before it had a roster. It specified
tiers, cache promotion, telemetry, persistent pipeline state, universal pattern composition,
typed runtime errors, and a conformance harness.

None of those are required to decide which personalized skills should exist. They are deferred
until a concrete skill implementation demonstrates the need.

## 3. Approaches considered

### A. Make one personalized skill per existing collision-map row

This is fast, but it assumes the current 17 rows are already correct. Several rows mix distinct
jobs: planning and execution, browsing and QA, committing and deploying, or creation and review.
It would preserve collisions inside oversized skills.

### B. Ignore the collision map and design a roster from scratch

This is highly personal, but it discards useful inventory and makes silent omissions likely.
There would be no trace from the existing 176 entries to the new roster.

### C. Use the map as candidate evidence, then derive the roster

This is selected. Each row is a candidate neighborhood, not a predetermined merge. Source
evidence may merge it, split it, keep entries separate, exclude entries, or assign one source to
more than one personalized skill when it genuinely serves different jobs.

## 4. Minimal document layout

The active design surface becomes:

```text
README.md
docs/
  condensation-guide.md
  skill-roster.md
  superpowers/specs/
    2026-07-29-personal-skill-roster-design.md
```

Ownership is deliberately small:

| Document | Owns |
|---|---|
| `README.md` | Purpose, phase-0 scope, headline inventory, and links |
| `docs/condensation-guide.md` | The lightweight decision procedure used to resolve candidates |
| `docs/skill-roster.md` | Source accounting, per-cluster decisions, and the final personalized roster |
| This design | Scope and acceptance criteria for producing those documents |

The current policy and five pattern specifications are superseded research history, not phase-0
interfaces. Useful rules are extracted into `condensation-guide.md`; those documents are removed
from the active tree rather than patched or archived beside the authoritative design. Git history
preserves them.

## 5. Collision-resolution procedure

For every candidate cluster:

1. **Identify the source artifact.** Read the plugin manifest or filesystem registration before
   reading content. Record whether the entry is a skill, command, agent, MCP server/tool/prompt,
   hook, LSP server, or another artifact type, plus its exact invocation mechanism and live
   location.
2. **Verify membership.** Read the live source description and, where descriptions collide,
   inspect the source instructions and the complete frontmatter or manifest declaration. Preserve
   unknown fields rather than assuming they are inert.
3. **Name the user job.** Write one sentence beginning, “When I want to …”. Two entries that
   cannot complete the same sentence without “or” do not belong in one personalized skill.
4. **Classify each relationship:**
   - **Duplicate:** same job and materially equivalent behavior.
   - **Complement:** same job, distinct useful method or perspective.
   - **Sequence:** different jobs that may be invoked one after another.
   - **Reference:** stack, framework, or domain knowledge used by another skill but not fused
     into it.
   - **Separate:** neighboring jobs with distinct triggers.
   - **Exclude:** unavailable, broken, irrelevant, or not worth retaining for this user.
5. **Choose the disposition:**
   - duplicates share one future entry point;
   - complements become named modes or internal references only when one invocation benefits
     from choosing between them;
   - sequences and separate jobs receive separate roster entries;
   - references remain independently addressable;
   - exclusions remain in the accounting table with a reason.
6. **Preserve delivery shape.** A command may inform a future user-invoked skill, but an agent,
   MCP server, hook, or LSP server is not flattened into prompt text. Record it as a retained
   execution mechanism, prerequisite, or out-of-scope artifact.
7. **Check the new roster for collisions.** Every personalized entry needs a distinct trigger.
   If two descriptions would both match the same ordinary request, refine or merge them.
8. **Record the manual bridge.** Give the exact current invocation: slash command, skill name,
   agent type, or MCP tool/server action. If a bridge depends on several artifact types, state
   their order and prerequisites.

Usage frequency affects implementation priority only. It does not prove that two skills should
merge or that an unused skill has no value.

## 6. Personalized roster interface

Each planned roster entry has these fields:

| Field | Meaning |
|---|---|
| `name` | Provisional personalized skill name |
| `job` | One user outcome, phrased as “When I want to …” |
| `trigger` | Requests that should select this skill and nearby requests that should not |
| `delivery_shape` | Future skill, retained reference, or manual workflow |
| `sources` | Existing artifacts that contribute behavior or guidance |
| `source_roles` | Duplicate, complement, sequence input, or reference |
| `manual_bridge` | Exact invocation mechanism to use today before the personalized skill exists |
| `dependencies` | Agents, MCP servers/tools, hooks, LSP servers, credentials, or runtimes that remain distinct |
| `behavior_notes` | Complete frontmatter/manifest snapshot and prerequisites; no declared or unknown field omitted |
| `priority` | `now`, `next`, or `later`, informed by project-development value and usage |
| `status` | `planned`, `implemented`, or `validated` |

All entries begin as `planned`. Invocation is manual. There are no hot/cold tiers, autonomous
router, cache, or promotion score in phase 0.

Names are provisional until the whole roster passes the collision check. Packaging and command
namespacing are separate later decisions.

## 7. Source accounting

`docs/skill-roster.md` contains one source-accounting table covering every occurrence in the
current collision map, plus a separate keep/defer/exclude table for the live reference-skill
groups already identified in the README. Each source row records:

- source identifier and artifact type;
- source location and exact invocation mechanism;
- availability and evidence inspected;
- complete frontmatter or manifest declaration;
- primary disposition and personalized roster home;
- retained non-skill dependencies and secondary roles.

Each occurrence receives exactly one primary disposition:

- mapped to a personalized roster entry;
- kept as an independent reference;
- deferred for later investigation;
- excluded with a reason; or
- marked as a duplicate occurrence caused by a known overlap.

The three current overlaps—`pair-agent`, `office-hours`, and `skillify`—must be resolved
explicitly. A source may inform more than one roster entry, but one entry is named as its primary
home so totals remain auditable.

Dead or unavailable skills cannot be claimed as absorbed. They may be excluded or investigated
from a recoverable source, but the roster must distinguish inference from inspected evidence.
The known dangling science symlinks remain a cleanup inventory rather than condensation inputs;
phase 0 records that disposition but does not remove them.

## 8. Evidence standard

This phase uses documentary evidence only:

- live source location;
- source artifact type and invocation mechanism;
- source description and relevant instructions;
- complete frontmatter or manifest declaration, including unknown fields;
- existing invocation counts for prioritization;
- a written rationale for each merge, split, keep, or exclusion.

Runtime RED/GREEN preservation testing is intentionally deferred because no personalized skill
is implemented or replacing a source. It becomes mandatory before a roster entry changes from
`implemented` to `validated` or any source is retired.

## 9. Deferred work

The following are explicitly outside phase 0:

- implementing `SKILL.md` files;
- plugin packaging and namespacing;
- router behavior or autonomous discovery;
- tier assignment, cache promotion, `/astra:tune`, and telemetry;
- persistent state and resumable pipelines;
- general panel, method, adapter, pipeline, or behavior-preservation runtimes;
- a universal composition interface or error taxonomy;
- conformance harness implementation;
- uninstalling, disabling, or deleting existing skills and plugins.

When implementation begins, start with one high-priority roster entry. Extract a shared module
only after at least two implementations demonstrate the same seam.

## 10. Acceptance criteria

Phase 0 is complete when:

1. Every collision-map occurrence is accounted for.
2. Every live reference entry in the README inventory has a keep, defer, or exclude decision.
3. Every overlap has a primary home and an explicit secondary role or exclusion.
4. Every personalized skill has one distinguishable job and trigger.
5. Every planned skill has a usable manual bridge.
6. Every manual bridge names an invocation mechanism that exists; no agent, MCP server, hook, or
   LSP server is flattened into a skill.
7. Complete source declarations are recorded without claiming their behavior has been preserved.
8. The final roster count emerges from the analysis; it is not forced to equal 17.
9. Reference skills remain independently addressable rather than being fused into broad skills.
10. No tier, cache, telemetry, persistence, composition-runtime, or retirement design is required
   to use the roster.
11. README and active docs contain one consistent phase-0 scope.
12. Existing skills, plugins, and unrelated `.idea/` files remain untouched.
