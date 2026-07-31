# Astra phase-0 ledgers

**Snapshot:** 2026-07-31

**Inventory baseline:** `README.md` at `07fcbdf` plus the live registrations named below

**State:** Seeded for coordination; unresolved values are explicit workflow states, not completed dispositions.

## Ownership and authority

| Role | Current assignee | Authority |
|---|---|---|
| Phase-0 coordinator | Codex primary agent (`/root`) for the active phase-0 run | Sole editor of this file; reserves claims, applies design proposals, rejects conflicting primary homes, and performs final reconciliation |
| Approval authority | User | Approves job boundaries, exclusions, priorities, final roster, and every retirement decision |

A coordinator handoff must replace the assignee above before another agent edits this file.
Design agents propose changes in `designs/<astra-name>.md`; they do not edit these tables.

## State vocabulary

- `unassigned` means no disposition or primary home has been proposed; it is valid only while
  `claim_status` is `unclaimed` or `claimed`.
- `claimed` reserves disposition ownership for a design; it does not approve or resolve that
  disposition.
- `resolved` is reserved for the coordinator's roster-wide reconciliation after all draft
  designs and the user's review.
- `Pending source inspection` is an explicit evidence state for an unclaimed skeleton row.
  It cannot support absorption, preservation, exclusion, or retirement.

## 1. Collision source-claim ledger

**Expected and present:** 179 occurrences across 17 candidate neighborhoods; 176 distinct
source identifiers. Rows follow README order. Repeated identifiers retain one row per
occurrence and list every candidate neighborhood.

| Occurrence ID | Source ID | Component type | Availability | Candidate neighborhoods | Primary disposition | Primary home | Secondary roles | Claim status | Evidence |
|---|---|---|---|---|---|---|---|---|---|
| `cm-adversarial-critique-01` | `grilling` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-02` | `grill-me` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-03` | `grill-with-docs` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Docs & knowledge: `domain-modeling` | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-04` | `/diss` | command | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-05` | `/diss-api` | command | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-06` | `diss-infra` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-07` | `diss-claudemd` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-08` | `/elon` | command | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-09` | `/trim` | command | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: prompt or skill remediation | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-10` | `office-hours` | skill | live | Adversarial critique; Ops & routine | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-11` | `plan-ceo-review` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: plan revision | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-12` | `plan-eng-review` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: plan revision | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-13` | `plan-design-review` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: plan revision | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-14` | `plan-devex-review` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: plan revision | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-15` | `devex-review` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | — | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-adversarial-critique-16` | `autoplan` | skill | live | Adversarial critique | proposed Astra design | `astra-critique` | Plan & spec: plan revision | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-code-review-01` | `code-review` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-02` | `review` | skill | live | Code review | unassigned | unassigned | `astra-critique` (secondary evidence) | unclaimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-code-review-03` | `requesting-code-review` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-04` | `receiving-code-review` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-05` | `superpowers:requesting-code-review` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-06` | `superpowers:receiving-code-review` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-07` | `feature-dev:code-reviewer` | agent | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-08` | `code-review:code-review` | command | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-09` | `security-review` | built-in skill | live | Code review | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-code-review-10` | `simplify` | built-in skill | live | Code review | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-code-review-11` | `code-simplifier` | agent | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-code-review-12` | `health` | skill | live | Code review | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-01` | `agent-browser` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-02` | `browse` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-03` | `connect-chrome` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-04` | `open-gstack-browser` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-05` | `agentcore` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-06` | `vercel-sandbox` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-07` | `electron` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-08` | `webapp-testing` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-09` | `scrape` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-10` | `skillify` | skill | live | Browser & QA; Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-11` | `slack` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-12` | `pair-agent` | skill | live | Browser & QA; Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-13` | `setup-browser-cookies` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-14` | `benchmark` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-15` | `dogfood` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-16` | `qa` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-17` | `qa-only` | skill | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-browser-and-qa-18` | `playwright` | MCP server | live | Browser & QA | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-design-and-visual-01` | `design` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-02` | `design-system` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-03` | `design-consultation` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-04` | `design-html` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-05` | `design-shotgun` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-06` | `design-review` | skill | live | Design & visual | proposed Astra design | `astra-critique` | `astra-interface`: fix and verify; Testing (future design): bootstrap and regression | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `cm-design-and-visual-07` | `ui-styling` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-08` | `ui-ux-pro-max` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-09` | `frontend-design` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-10` | `theme-factory` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-11` | `brand` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-12` | `brand-guidelines` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-13` | `banner-design` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-14` | `canvas-design` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-15` | `algorithmic-art` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-16` | `slides` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-17` | `dataviz` | built-in skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source bytes unavailable and host-version provenance unresolved. |
| `cm-design-and-visual-18` | `artifact-design` | built-in skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source bytes unavailable and host-version provenance unresolved. |
| `cm-design-and-visual-19` | `artifact-capabilities` | built-in skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source bytes unavailable and host-version provenance unresolved. |
| `cm-design-and-visual-20` | `web-artifacts-builder` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-design-and-visual-21` | `diagram` | skill | live | Design & visual | unassigned | unassigned | — | claimed | Reserved by the phase-0 coordinator for the Design & visual investigation; source inspection pending. |
| `cm-plan-and-spec-01` | `superpowers:brainstorming` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-02` | `superpowers:writing-plans` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-03` | `superpowers:executing-plans` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-04` | `superpowers:subagent-driven-development` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-05` | `spec` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-06` | `to-spec` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-07` | `sdd` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-08` | `planb` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-09` | `plan-tune` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-10` | `wayfinder` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-11` | `to-tickets` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-12` | `implement` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-13` | `prototype` | skill | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-14` | `feature-dev:code-architect` | agent | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-plan-and-spec-15` | `feature-dev:feature-dev` | command | live | Plan & spec | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-01` | `ship` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-02` | `land-and-deploy` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-03` | `canary` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-04` | `landing-report` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-05` | `setup-deploy` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-06` | `/pr` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-07` | `/commit` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-08` | `/build-push-ecr` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-09` | `commit-commands:commit` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-10` | `commit-commands:commit-push-pr` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-11` | `commit-commands:clean_gone` | command | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-12` | `changelog` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-13` | `document-release` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-14` | `resolving-merge-conflicts` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-15` | `superpowers:finishing-a-development-branch` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-16` | `superpowers:using-git-worktrees` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ship-and-vcs-17` | `github` | skill | live | Ship & VCS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-01` | `document-generate` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-02` | `doc-coauthoring` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-03` | `/doc` | command | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-04` | `make-pdf` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-05` | `internal-comms` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-06` | `learn` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-07` | `teach` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-08` | `research` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-09` | `rtfm` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-10` | `init` | built-in skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-docs-and-knowledge-11` | `claude-md-management:revise-claude-md` | command | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-12` | `claude-md-management:claude-md-improver` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-13` | `domain-modeling` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-docs-and-knowledge-14` | `slack-gif-creator` | skill | live | Docs & knowledge | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-01` | `investigate` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-02` | `diagnosing-bugs` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-03` | `superpowers:systematic-debugging` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-04` | `rca` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-05` | `firefighting` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-06` | `java-leak-resolver` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-07` | `staging-debug` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-08` | `local-debug` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-debug-and-incident-09` | `triage` | skill | live | Debug & incident | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-codebase-comprehension-01` | `how` | skill | live | Codebase comprehension | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-codebase-comprehension-02` | `code-tracing` | skill | live | Codebase comprehension | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-codebase-comprehension-03` | `codebase-design` | skill | live | Codebase comprehension | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-codebase-comprehension-04` | `improve-codebase-architecture` | skill | live | Codebase comprehension | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-codebase-comprehension-05` | `feature-dev:code-explorer` | agent | live | Codebase comprehension | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-01` | `skill-creator` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-02` | `skill-creator:skill-creator` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-03` | `writing-great-skills` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-04` | `superpowers:writing-skills` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-05` | `skillify` | skill | live | Browser & QA; Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-06` | `ask-matt` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-07` | `gstack` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-08` | `_gstack-command` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-09` | `prompt-lookup` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-10` | `benchmark-models` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-skill-meta-11` | `gstack-upgrade` | skill | live | Skill meta | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-01` | `coding-agent` | skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-02` | `codex` | skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-03` | `superpowers:dispatching-parallel-agents` | skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-04` | `nightnight` | skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-05` | `loop` | built-in skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-delegation-and-autonomy-06` | `loop-goal` | skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-delegation-and-autonomy-07` | `schedule` | built-in skill | live | Delegation & autonomy | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-delegation-and-autonomy-08` | `pair-agent` | skill | live | Browser & QA; Delegation & autonomy | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-01` | `tdd` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-02` | `superpowers:test-driven-development` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-03` | `bdd` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-04` | `spock` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-05` | `nextjs-test` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-06` | `shell-scripting:bats-testing-patterns` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-07` | `superpowers:verification-before-completion` | skill | live | Testing | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-testing-08` | `run` | built-in skill | live | Testing | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-context-and-handoff-01` | `context-save` | skill | live | Context & handoff | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-context-and-handoff-02` | `context-restore` | skill | live | Context & handoff | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-context-and-handoff-03` | `strategic-compact` | skill | live | Context & handoff | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-context-and-handoff-04` | `handoff` | skill | live | Context & handoff | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-context-and-handoff-05` | `nowhat` | skill | live | Context & handoff | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-safety-01` | `careful` | skill | live | Safety | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-safety-02` | `freeze` | skill | live | Safety | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-safety-03` | `unfreeze` | skill | live | Safety | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-safety-04` | `guard` | skill | live | Safety | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-setup-and-config-01` | `setup-aurora-pg-mcp` | skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-setup-and-config-02` | `setup-gbrain` | skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-setup-and-config-03` | `sync-gbrain` | skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-setup-and-config-04` | `setup-matt-pocock-skills` | skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-setup-and-config-05` | `update-config` | built-in skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-setup-and-config-06` | `keybindings-help` | built-in skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-setup-and-config-07` | `fewer-permission-prompts` | built-in skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Unavailable bytes: harness built-in; host-version provenance rule unresolved. |
| `cm-setup-and-config-08` | `claude-code-setup:claude-automation-recommender` | skill | live | Setup & config | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ios-01` | `ios-qa` | skill | live | iOS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ios-02` | `ios-fix` | skill | live | iOS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ios-03` | `ios-design-review` | skill | live | iOS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ios-04` | `ios-sync` | skill | live | iOS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ios-05` | `ios-clean` | skill | live | iOS | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ops-and-routine-01` | `retro` | skill | live | Ops & routine | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ops-and-routine-02` | `meeting` | skill | live | Ops & routine | unassigned | unassigned | — | unclaimed | Pending source inspection. |
| `cm-ops-and-routine-03` | `office-hours` | skill | live | Adversarial critique; Ops & routine | duplicate occurrence | `astra-critique` | Ops & routine candidate role | claimed | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |

## 2. Reference and cleanup ledger

**Expected and present:** 174 rows — 41 exact live reference entries (12 language / stack,
4 shell, and 25 Hugging Face) plus 133 dangling skill registrations.

| Source ID | Component type | Location or registration | Availability | Disposition | Reason | Consuming designs | Evidence |
|---|---|---|---|---|---|---|---|
| `java` | skill | `~/.claude/skills/java/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `python-patterns` | skill | `~/.claude/skills/python-patterns/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `nextjs` | skill | `~/.claude/skills/nextjs/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `claude-api` | skill | `~/.claude/skills/claude-api/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `mcp-builder` | skill | `~/.claude/skills/mcp-builder/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `awssdk` | skill | `~/.claude/skills/awssdk/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `security` | skill | `~/.claude/skills/security/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `cso` | skill | `~/.claude/skills/cso/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | `astra-critique` | [Astra Critique §3](../designs/astra-critique.md#3-source-evidence) |
| `design-api` | skill | `~/.claude/skills/design-api/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | `astra-critique` | Consumption proposed by [Astra Critique §3.3](../designs/astra-critique.md#33-proposed-ledger-changes); source inspection pending. |
| `design-db` | skill | `~/.claude/skills/design-db/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `agent-harness-construction` | skill | `~/.claude/skills/agent-harness-construction/SKILL.md` | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `karpathy-guidelines` | skill | andrej-karpathy-skills@karpathy-skills/1.0.0 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `shell-scripting:bash-defensive-patterns` | skill | shell-scripting@claude-code-workflows/1.2.3 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `shell-scripting:shellcheck-configuration` | skill | shell-scripting@claude-code-workflows/1.2.3 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `shell-scripting:bash-pro` | agent | shell-scripting@claude-code-workflows/1.2.3 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `shell-scripting:posix-shell-pro` | agent | shell-scripting@claude-code-workflows/1.2.3 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cli` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-aws-context-discovery` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-python-env-setup` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-sagemaker-deployment-planner` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-sagemaker-iam-preflight` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-sagemaker-production-defaults` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-cloud-serving-image-selection` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:hf-mem` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-best` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-community-evals` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-datasets` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-gradio` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-llm-trainer` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-local-models` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-lora-space-builder` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-paper-publisher` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-papers` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-spaces` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-tool-builder` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-trackio` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-vision-trainer` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:huggingface-zerogpu` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:train-sentence-transformers` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:transformers-js` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `huggingface-skills:trl-training` | skill | huggingface-skills@claude-plugins-official/1.0.20 | live | unassigned | Awaiting user `keep` / `defer` / `exclude` decision. | — | Pending source inspection. |
| `adaptyv` | skill | `~/.claude/skills/adaptyv` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `aeon` | skill | `~/.claude/skills/aeon` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `anndata` | skill | `~/.claude/skills/anndata` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `astropy` | skill | `~/.claude/skills/astropy` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `bgpt-paper-search` | skill | `~/.claude/skills/bgpt-paper-search` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `biopython` | skill | `~/.claude/skills/biopython` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `bioservices` | skill | `~/.claude/skills/bioservices` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `cellxgene-census` | skill | `~/.claude/skills/cellxgene-census` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `cirq` | skill | `~/.claude/skills/cirq` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `citation-management` | skill | `~/.claude/skills/citation-management` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `clinical-decision-support` | skill | `~/.claude/skills/clinical-decision-support` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `clinical-reports` | skill | `~/.claude/skills/clinical-reports` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `cobrapy` | skill | `~/.claude/skills/cobrapy` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `consciousness-council` | skill | `~/.claude/skills/consciousness-council` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `dask` | skill | `~/.claude/skills/dask` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `database-lookup` | skill | `~/.claude/skills/database-lookup` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `datamol` | skill | `~/.claude/skills/datamol` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `deepchem` | skill | `~/.claude/skills/deepchem` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `deeptools` | skill | `~/.claude/skills/deeptools` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `depmap` | skill | `~/.claude/skills/depmap` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `dhdna-profiler` | skill | `~/.claude/skills/dhdna-profiler` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `diffdock` | skill | `~/.claude/skills/diffdock` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `dnanexus-integration` | skill | `~/.claude/skills/dnanexus-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `docx` | skill | `~/.claude/skills/docx` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `esm` | skill | `~/.claude/skills/esm` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `etetoolkit` | skill | `~/.claude/skills/etetoolkit` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `exploratory-data-analysis` | skill | `~/.claude/skills/exploratory-data-analysis` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `find-skills` | skill | `~/.claude/skills/find-skills` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `flowio` | skill | `~/.claude/skills/flowio` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `fluidsim` | skill | `~/.claude/skills/fluidsim` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `generate-image` | skill | `~/.claude/skills/generate-image` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `geniml` | skill | `~/.claude/skills/geniml` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `geomaster` | skill | `~/.claude/skills/geomaster` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `geopandas` | skill | `~/.claude/skills/geopandas` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `get-available-resources` | skill | `~/.claude/skills/get-available-resources` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `gget` | skill | `~/.claude/skills/gget` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `ginkgo-cloud-lab` | skill | `~/.claude/skills/ginkgo-cloud-lab` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `glycoengineering` | skill | `~/.claude/skills/glycoengineering` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `gtars` | skill | `~/.claude/skills/gtars` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `histolab` | skill | `~/.claude/skills/histolab` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `hugging-science` | skill | `~/.claude/skills/hugging-science` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `hypogenic` | skill | `~/.claude/skills/hypogenic` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `hypothesis-generation` | skill | `~/.claude/skills/hypothesis-generation` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `imaging-data-commons` | skill | `~/.claude/skills/imaging-data-commons` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `infographics` | skill | `~/.claude/skills/infographics` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `iso-13485-certification` | skill | `~/.claude/skills/iso-13485-certification` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `labarchive-integration` | skill | `~/.claude/skills/labarchive-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `lamindb` | skill | `~/.claude/skills/lamindb` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `latchbio-integration` | skill | `~/.claude/skills/latchbio-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `latex-posters` | skill | `~/.claude/skills/latex-posters` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `literature-review` | skill | `~/.claude/skills/literature-review` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `markdown-mermaid-writing` | skill | `~/.claude/skills/markdown-mermaid-writing` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `market-research-reports` | skill | `~/.claude/skills/market-research-reports` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `markitdown` | skill | `~/.claude/skills/markitdown` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `matchms` | skill | `~/.claude/skills/matchms` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `matlab` | skill | `~/.claude/skills/matlab` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `matplotlib` | skill | `~/.claude/skills/matplotlib` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `medchem` | skill | `~/.claude/skills/medchem` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `modal` | skill | `~/.claude/skills/modal` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `molecular-dynamics` | skill | `~/.claude/skills/molecular-dynamics` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `molfeat` | skill | `~/.claude/skills/molfeat` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `networkx` | skill | `~/.claude/skills/networkx` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `neurokit2` | skill | `~/.claude/skills/neurokit2` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `neuropixels-analysis` | skill | `~/.claude/skills/neuropixels-analysis` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `omero-integration` | skill | `~/.claude/skills/omero-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `open-notebook` | skill | `~/.claude/skills/open-notebook` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `opentrons-integration` | skill | `~/.claude/skills/opentrons-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `optimize-for-gpu` | skill | `~/.claude/skills/optimize-for-gpu` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `paper-lookup` | skill | `~/.claude/skills/paper-lookup` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `paperzilla` | skill | `~/.claude/skills/paperzilla` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `parallel-web` | skill | `~/.claude/skills/parallel-web` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pathml` | skill | `~/.claude/skills/pathml` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pdf` | skill | `~/.claude/skills/pdf` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `peer-review` | skill | `~/.claude/skills/peer-review` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pennylane` | skill | `~/.claude/skills/pennylane` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `phylogenetics` | skill | `~/.claude/skills/phylogenetics` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `polars` | skill | `~/.claude/skills/polars` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `polars-bio` | skill | `~/.claude/skills/polars-bio` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pptx` | skill | `~/.claude/skills/pptx` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pptx-posters` | skill | `~/.claude/skills/pptx-posters` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `primekg` | skill | `~/.claude/skills/primekg` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `protocolsio-integration` | skill | `~/.claude/skills/protocolsio-integration` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pufferlib` | skill | `~/.claude/skills/pufferlib` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pydeseq2` | skill | `~/.claude/skills/pydeseq2` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pydicom` | skill | `~/.claude/skills/pydicom` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pyhealth` | skill | `~/.claude/skills/pyhealth` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pylabrobot` | skill | `~/.claude/skills/pylabrobot` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pymatgen` | skill | `~/.claude/skills/pymatgen` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pymc` | skill | `~/.claude/skills/pymc` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pymoo` | skill | `~/.claude/skills/pymoo` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pyopenms` | skill | `~/.claude/skills/pyopenms` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pysam` | skill | `~/.claude/skills/pysam` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pytdc` | skill | `~/.claude/skills/pytdc` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pytorch-lightning` | skill | `~/.claude/skills/pytorch-lightning` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `pyzotero` | skill | `~/.claude/skills/pyzotero` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `qiskit` | skill | `~/.claude/skills/qiskit` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `qutip` | skill | `~/.claude/skills/qutip` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `rdkit` | skill | `~/.claude/skills/rdkit` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `research-grants` | skill | `~/.claude/skills/research-grants` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `rowan` | skill | `~/.claude/skills/rowan` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scanpy` | skill | `~/.claude/skills/scanpy` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scholar-evaluation` | skill | `~/.claude/skills/scholar-evaluation` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-brainstorming` | skill | `~/.claude/skills/scientific-brainstorming` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-critical-thinking` | skill | `~/.claude/skills/scientific-critical-thinking` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-schematics` | skill | `~/.claude/skills/scientific-schematics` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-slides` | skill | `~/.claude/skills/scientific-slides` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-visualization` | skill | `~/.claude/skills/scientific-visualization` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scientific-writing` | skill | `~/.claude/skills/scientific-writing` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scikit-bio` | skill | `~/.claude/skills/scikit-bio` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scikit-learn` | skill | `~/.claude/skills/scikit-learn` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scikit-survival` | skill | `~/.claude/skills/scikit-survival` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scvelo` | skill | `~/.claude/skills/scvelo` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `scvi-tools` | skill | `~/.claude/skills/scvi-tools` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `seaborn` | skill | `~/.claude/skills/seaborn` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `shap` | skill | `~/.claude/skills/shap` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `simpy` | skill | `~/.claude/skills/simpy` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `stable-baselines3` | skill | `~/.claude/skills/stable-baselines3` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `statistical-analysis` | skill | `~/.claude/skills/statistical-analysis` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `statsmodels` | skill | `~/.claude/skills/statsmodels` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `sympy` | skill | `~/.claude/skills/sympy` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `tiledbvcf` | skill | `~/.claude/skills/tiledbvcf` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `timesfm-forecasting` | skill | `~/.claude/skills/timesfm-forecasting` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `torch-geometric` | skill | `~/.claude/skills/torch-geometric` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `torchdrug` | skill | `~/.claude/skills/torchdrug` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `transformers` | skill | `~/.claude/skills/transformers` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `treatment-plans` | skill | `~/.claude/skills/treatment-plans` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `umap-learn` | skill | `~/.claude/skills/umap-learn` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `usfiscaldata` | skill | `~/.claude/skills/usfiscaldata` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `vaex` | skill | `~/.claude/skills/vaex` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `venue-templates` | skill | `~/.claude/skills/venue-templates` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `what-if-oracle` | skill | `~/.claude/skills/what-if-oracle` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `xlsx` | skill | `~/.claude/skills/xlsx` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |
| `zarr-python` | skill | `~/.claude/skills/zarr-python` | dangling | unassigned | Broken symlink; awaiting user cleanup disposition. | — | Unavailable: symlink target missing on 2026-07-30. |

## 3. Separate component records

These installed components are not superskill source rows. Recording them here prevents a
plugin-level deletion from silently removing a capability with a different lifecycle.

| Component ID | Component type | Parent or registration | Phase-0 treatment | Reason | Evidence |
|---|---|---|---|---|---|
| github:mcp-server | MCP server | github@claude-plugins-official | Out of scope — retain | External capability, not a prompt skill; later component-level migration must decide it separately. | plugin `.mcp.json` |
| huggingface-skills:mcp-server | MCP server | huggingface-skills@claude-plugins-official/1.0.20 | Out of scope — retain | External capability, not a prompt skill; later component-level migration must decide it separately. | plugin `.mcp.json` |
| superpowers:SessionStart | hook | superpowers@claude-plugins-official/6.2.0 | Out of scope — retain | Lifecycle behavior cannot be flattened into a superskill; later hook ownership must decide it separately. | plugin `hooks/hooks.json` |
| explanatory-output-style:SessionStart | hook | explanatory-output-style@claude-plugins-official/1.0.0 | Out of scope — retain | Lifecycle behavior cannot be flattened into a superskill; later hook ownership must decide it separately. | plugin `hooks/hooks.json` |
| clangd-lsp:clangd | LSP server | clangd-lsp@claude-plugins-official/1.0.0 | Out of scope — retain | Language infrastructure is orthogonal to superskill condensation. | marketplace manifest `lspServers.clangd` |
| skill-creator:analyzer | skill-scoped agent | skill-creator:skill-creator | Tracked with parent | Not independently registered; preserve with the parent skill until that design decides its delivery shape. | skill-creator plugin `skills/skill-creator/agents/analyzer.md` |
| skill-creator:comparator | skill-scoped agent | skill-creator:skill-creator | Tracked with parent | Not independently registered; preserve with the parent skill until that design decides its delivery shape. | skill-creator plugin `skills/skill-creator/agents/comparator.md` |
| skill-creator:grader | skill-scoped agent | skill-creator:skill-creator | Tracked with parent | Not independently registered; preserve with the parent skill until that design decides its delivery shape. | skill-creator plugin `skills/skill-creator/agents/grader.md` |

## 4. Coordinator checks

- Collision rows: **179**.
- Collision distinct source identifiers: **176**.
- Live reference rows: **41**.
- Dangling cleanup rows: **133**.
- Separate installed-component records: **8**.
- Astra Critique occurrences are `claimed`, not `resolved`.
- All 21 Design & visual occurrences are `claimed` for one investigation wave. `design-review`
  is assigned to `astra-critique` with explicit secondary roles; the remaining 20 stay
  `unassigned` pending the user-approved split into primary homes.
- Every other collision occurrence remains `unclaimed` and `unassigned`.
- No `keep`, `defer`, `exclude`, or retirement decision is inferred from this skeleton.
