# Wave 1 Design Architecture Research

> Date: 2026-07-31 · Status: research input, not a roster or retirement decision
>
> **Superseded roster recommendation:** the user subsequently folded `astra-presentation` into
> `astra-interface`; roadmap amendment 3 owns that decision. References below to four peers or a
> Presentation home preserve the source-audit result at the time it was written and are not current
> roster state. The source evidence remains usable, with Presentation obligations read as Interface
> obligations unless a later design splits them again.

## Bottom line

**The four flat peers survive source inspection as the right public core, but the current source allocation does not.** Keep `astra-product-design`, `astra-interface`, `astra-brand`, and `astra-presentation` as peers; do not force every visual source into them. This follows the “one coherent job through one distinguishable interface” rule ([requirements](../design-requirements.md#3-governing-rule)) and Phase 0's permission to split or retain sources (`docs/phase-0.md:L41-L66`).

Required corrections:

- move `theme-factory` from Brand to Presentation;
- split the umbrella behavior of `design`, `design-system`, and `ui-styling` across the peers it actually serves;
- retain `canvas-design`, `algorithmic-art`, `diagram`, and `prototype` independently;
- treat `brand-guidelines` as an Anthropic-specific profile, not a generic workflow;
- defer built-ins `artifact-design`, `artifact-capabilities`, and `dataviz`;
- keep `design-review` split across Critique, Interface, Test, and Ship/VCS authority.

The recommended architecture is therefore **four core peers plus explicit retained jobs**, not four catch-all buckets.

## Method and provenance

All 21 Design & visual occurrences and cross-neighborhood `prototype` were inspected from their bodies, frontmatter/registration, material references, dependencies, outputs, and failure paths. Claims below use **O** = observed, **I** = inferred disposition, and **U** = source unavailable, matching the required certainty labels ([requirements](../design-requirements.md#42-label-certainty)).

- gstack sources: commit `a3259400a366593e0c909dd9ac3e59752efd2488`; active registrations point into `~/.claude/skills/gstack/`.
- Anthropic vendor sources: detached nested-repo commit `98669c11ca63e9c81c11501e1437e5c47b556621`; active entries are symlinks into that tree.
- Direct personal/ClaudeKit sources lack a containing immutable revision; exact inspected `SKILL.md` SHA-256 values are recorded in the disposition table.
- `prototype` source: `/home/kurophoenix/.agents/skills/prototype/SKILL.md`; body SHA
  `03074862d4b6e4eaf472aa75146e1d193dd9e3bba0e4303a9b2425562d1d44cc`.
  `agents/openai.yaml` is three lines of interface metadata, not an independently invocable agent.
- Built-ins have no path or manifest, so they cannot satisfy reproducible provenance (`README.md:L92-L100`).

The roadmap allocations are provisional and none of the 21 rows is resolved (`docs/design-roadmap.md:L359-L376`; `docs/phase-0-ledgers.md:L84-L104`, `L431-L441`).

## Correct peer boundaries

| Peer | One public job | Owns | Does not own |
|---|---|---|---|
| `astra-product-design` | Establish an approved product experience and visual direction | product context, aesthetic direction, exploratory variants, integrated `DESIGN.md` | brand jurisdiction, production components, broad product strategy |
| `astra-interface` | Materialize approved direction as an accessible interface system | token mappings, component specs, implementation, responsive behavior, interface verification | brand voice/logo policy, deck narrative, open-ended art |
| `astra-brand` | Define and apply durable brand identity | voice, messaging, logo rules, brand primitives, asset governance, campaign activation | generic themes, unbranded art, UI implementation |
| `astra-presentation` | Create a coherent persuasive deck | deck strategy, slide narrative/layouts, charts, themes, responsive deck output | arbitrary diagrams, product UI, brand definition |

`astra-product-design` is accurate only with this narrower promise. Its sources establish design direction and explore screen variants; they do not provide full product discovery or strategy. If a broader promise is intended, rename it `astra-design-direction` or add appropriate sources.

## Layered artifact authority

Inspection found competing source-of-truth claims: consultation writes `DESIGN.md` (`/home/kurophoenix/.claude/skills/gstack/design-consultation/sections/proposal-and-preview.md:L324-L394`), Brand calls `docs/brand-guidelines.md` authoritative (`/home/kurophoenix/.claude/skills/brand/SKILL.md:L42-L55`), and Interface sources can create token files or a competing `design-system/MASTER.md`.

Use this authority stack:

1. User decisions are final.
2. `docs/brand-guidelines.md` owns voice, messaging, logo rules, and intended brand primitives.
3. Root `DESIGN.md` is the human integration contract. Product Design is its editor/chair, not judge over peer jurisdictions; it records product context, approved direction, layout/motion principles, and references Brand and tokens.
4. `assets/design-tokens.json` is the canonical machine projection. Brand owns primitive meaning; Interface owns primitive→semantic→component mappings and validation.
5. `assets/design-tokens.css` is generated output, never independently authoritative.
6. Presentation-specific tokens extend the projection without overwriting Brand or Interface authority.

`design-system/MASTER.md` should be a generated/read-only view or removed as a competing authority. Normative conflicts return to the user.

## Source disposition

| Source | Observed job | Recommended home/disposition | Evidence |
|---|---|---|---|
| `design` | Umbrella router: logo, CIP, slides, banners, icons, social assets | **Split**: Brand coordinates logo/CIP/activation; Presentation takes slides; Interface takes token/UI routing | O/I; `/home/kurophoenix/.claude/skills/design/SKILL.md:L26-L38`, `L243-L289`; SHA `413f4ab9…603b6` |
| `design-system` | Tokens, component specs, substantial slide subsystem | Interface primary; Presentation strong secondary; Brand input | O/I; `/home/kurophoenix/.claude/skills/design-system/SKILL.md:L25-L105`, `L108-L180`; SHA `655468bb…1ae3f` |
| `design-consultation` | Research, proposal/preview, user decisions, `DESIGN.md` | Product Design; `DESIGN.md` editorial owner | O/I; `/home/kurophoenix/.claude/skills/gstack/design-consultation/SKILL.md:L47-L53`; SHA `44379ed9…967` |
| `design-html` | Approved direction/mockup → one production page and refinement loop | Interface implementation adapter | O/I; `/home/kurophoenix/.claude/skills/gstack/design-html/SKILL.md:L961-L1028`, `L1438-L1511`; SHA `ed44f14e…eb0` |
| `design-shotgun` | Distinct UI variants, approval, `approved.json` | Product Design; Interface consumes output | O/I; `/home/kurophoenix/.claude/skills/gstack/design-shotgun/SKILL.md:L1315-L1373`; SHA `513d9e18…9e7` |
| `design-review` | Audit/report, test bootstrap, source fixes, verification, commits | Critique + Interface + Test + Ship/VCS; retain until all modes replaced | O/I; `/home/kurophoenix/.claude/skills/gstack/design-review/SKILL.md:L812-L850`, `L978-L1042`, `L1801-L1887`; SHA `a7fb587d…0e5` |
| `ui-styling` | shadcn/Tailwind implementation plus unrelated canvas-art reference | Interface; split out canvas-art slice | O/I; `/home/kurophoenix/.claude/skills/ui-styling/SKILL.md:L33-L55`, `L196-L200`; SHA `f8b6c383…c62d` |
| `ui-ux-pro-max` | UI intelligence, system generation, implementation/review rules | Interface primary; Product secondary; map/remove `MASTER.md` | O/I; `/home/kurophoenix/.claude/skills/ui-ux-pro-max/SKILL.md:L338-L421`; SHA `adcc153b…d7a` |
| `frontend-design` | Distinctive production frontend implementation | Interface | O/I; `/home/kurophoenix/.claude/skills/frontend-design/SKILL.md:L1-L42`; vendor SHA `b81e2ff8…5a0` |
| `theme-factory` | User-selected preset/custom themes applied mainly to decks | **Move Brand → Presentation**; Brand supplies constraints | O/I; `/home/kurophoenix/.claude/skills/theme-factory/SKILL.md:L12-L59`; vendor SHA `c35893e2…552` |
| `brand` | Voice, identity, messaging, asset governance, token sync | Brand; generic brand source oracle | O/I; `/home/kurophoenix/.claude/skills/brand/SKILL.md:L14-L55`; SHA `6a450ee1…d44` |
| `brand-guidelines` | Fixed Anthropic colors and typography | Brand profile/reference; retain until source-specific fidelity passes | O/I; `/home/kurophoenix/.claude/skills/brand-guidelines/SKILL.md:L1-L71`; vendor SHA `1120b376…9fe` |
| `banner-design` | Multi-format campaign creative and export | Brand activation mode; retain pending dependency/output fidelity | O/I; `/home/kurophoenix/.claude/skills/banner-design/SKILL.md:L28-L143`; SHA `913d9c4b…acc` |
| `canvas-design` | Static original art plus philosophy, PNG/PDF | **Retain**; future Visual Art static mode candidate | O/I; `/home/kurophoenix/.claude/skills/canvas-design/SKILL.md:L1-L130`; vendor SHA `a1f28807…44b` |
| `algorithmic-art` | Seeded interactive p5.js generative art | **Retain**; future Visual Art generative mode candidate | O/I; `/home/kurophoenix/.claude/skills/algorithmic-art/SKILL.md:L101-L217`, `L221-L405`; vendor SHA `3bc4092c…eef` |
| `slides` | Thin router to presentation references | Presentation, but not sole oracle; preserve richer `design-system` slide behavior | O/I; `/home/kurophoenix/.claude/skills/slides/SKILL.md:L21-L40`; SHA `2b90bdaf…ccb` |
| `dataviz` | Built-in name only | **Defer** | U; `README.md:L92-L100` |
| `artifact-design` | Built-in name only | **Defer** | U; `README.md:L92-L100` |
| `artifact-capabilities` | Built-in name only | **Defer** | U; `README.md:L92-L100` |
| `web-artifacts-builder` | React/Tailwind/shadcn scaffold and single-HTML bundler | Interface delivery adapter, not design judgment | O/I; `/home/kurophoenix/.claude/skills/web-artifacts-builder/SKILL.md:L7-L70`; vendor SHA `81c5002c…10f8` |
| `diagram` | Offline Mermaid + editable Excalidraw + SVG/PNG triplet | **Retain**; likely Document/Architecture primary, Presentation consumer | O/I; `/home/kurophoenix/.claude/skills/gstack/diagram/SKILL.md:L800-L923`; SHA `f57f8722…0412` |
| `prototype` | Throwaway logic/UI experiment that promotes only its learned decision | **Retain**; Product/Interface/Architecture may consume findings but do not own its lifecycle | O/I; `/home/kurophoenix/.agents/skills/prototype/SKILL.md:L8-L26`, `LOGIC.md:L1-L79`, `UI.md:L1-L112` |

## Roadmap and validation implications

Revise roadmap §5.4 with the moves/splits/retains above; mark the three built-ins as provenance dependency `P`. Do not add `astra-visual-art` until static/generative selection or continuity demonstrates positive advantage beyond routing.

The four peers remain hypotheses until source-oracle → reference-convener → self-contained-candidate comparisons pass ([requirements](../design-requirements.md#61-three-comparison-systems)). No source is retirement-eligible from this research, especially unavailable built-ins, split umbrellas, source-specific brand guidance, or retained artifact jobs.
