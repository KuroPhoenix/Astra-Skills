# Astra Report stance-bearing mediation — Deep Research handoff

**Date:** 2026-08-19

**Status:** Research brief only. This document does not amend an Astra design, approve an
implementation plan, authorize runtime work, create a skill, change the public roster, or permit
ledger or lifecycle mutation.

## 0. How to use this handoff

Append the supplied 108-question corpus at the marked location in section 7, preserving every
question's identifier, wording, grouping, and priority. Then conduct the research programme in
this handoff and answer every question through the required coverage matrix.

The repository is authoritative for the current approved design state. The user statements in
this handoff identify the new problem to investigate; they are not permission to silently rewrite
the repository. If a research conclusion conflicts with a later user-approved repository decision,
the later decision wins. Report the conflict and its consequence.

## 1. Executive research problem

Astra Report was designed as the non-authoritative human-facing layer downstream of six
authoritative lifecycle skills. The current approved model is output-only: a producing skill owns
facts, consequences, recommendations, options, and lifecycle state; Report owns presentation;
the user remains the sole approval authority; user-to-skill intake and decisions remain direct.

The user's newer insight challenges the assumption that Report can or should be stance-free:

> Report should reflect the originating skill's view when it reports that skill's work, but should
> reflect the user's intent when recording decisions, policy, direction, and feedback. It should
> guide the reader without acquiring independent lifecycle authority, and it should ensure that
> feedback reaches the skill whose work it concerns.

The Hacker–Bernard–Humphrey analogy is an intuition pump for unequal knowledge, guidance,
institutional role, and final political authority. It is not evidence and must not be treated as a
literal organizational specification.

The central research question is therefore:

> **How should a non-authoritative but stance-bearing intermediary mediate between multiple
> domain-authoritative AI skills and a sovereign human decision-maker, switching the represented
> principal across outbound reporting and inbound feedback without laundering authority,
> manipulating the user, losing feedback, or becoming a lifecycle orchestrator?**

This is not primarily a concision question. It is a problem of production roles, attributed
stance, delegated voice, decision sovereignty, feedback closure, and provenance.

## 2. Current repository baseline and the exact conflict

Read the current repository before accepting this summary. At handoff time, the following claims
are load-bearing:

- `designs/astra-report.md` section 1.2 resolves delegated voice in the output direction only and
  explicitly rejects input mediation as orchestration.
- Sections 3.6, 8.1, 8.2, and 8.4 make Report read-only over lifecycle authority. A producer owns
  the decision and records the user's answer; no determination returns through `I(reporting)`.
- The current design treats Report's durable state as exposure bookkeeping, not approval or
  workflow state.
- `docs/research/2026-08-18-astra-report-book-distillation.md` preserves the books' original
  unified-writer advice but currently transfers it as: producer owns the case, Report owns the
  route, user owns the outcome, and the producer records the lifecycle effect.

The new direction potentially changes more than prose style:

- Report would not merely route a producer-authored case; it would speak from an explicitly
  attributed producer stance when briefing the user.
- Report would not merely expose a direct producer decision control; it would faithfully record
  and return user feedback, direction, and policy to the relevant producer.
- An internal Report Artifact would serve as the bounded subject's disclosure and review record,
  rather than requiring one shared per-project attention ledger.
- Report could record user responses, but it could neither alter them autonomously nor treat them
  as producer disposition or lifecycle effect.

Research must determine whether this is a bounded communication loop or an authority-bearing
orchestration loop, and what contract makes the difference. Do not assume that calling it
"reporting" settles the issue.

## 3. Fixed premises and constraints

Treat these as the user's governing premises unless the research demonstrates an unavoidable
contradiction. If so, state the contradiction rather than silently discarding a premise.

1. **The user is sovereign over approval, direction, and policy.** No skill or reporting layer may
   convert guidance into approval.
2. **Each lifecycle skill remains authoritative inside its jurisdiction.** Its facts, findings,
   severity, consequences, options, recommendations, work state, and artifact semantics are not
   re-authored by Report.
3. **Report has no independent substantive programme.** It may be stance-bearing only on behalf of
   an identified principal within an identified scope.
4. **Report should guide.** A purely neutral transcript or formatter does not satisfy the user's
   need; intent, significance, and recommended attention may be present when attributable to the
   source authority.
5. **Principal switching must be explicit.** Producer stance governs producer-to-user reporting;
   user stance governs the capture and return of user decisions, direction, policy, and feedback.
6. **Feedback must close the loop.** "Recorded" is not automatically "delivered," "understood,"
   "accepted," "applied," or "resolved." Those states must not be collapsed.
7. **User language must remain faithful.** Report may preserve an exact response and may offer a
   separately identified normalization or routing summary, but it must not silently rewrite the
   user's intent.
8. **Conflicts remain visible.** Report may not blend two skills' positions, or a skill's position
   with the user's, into false consensus.
9. **The state scope is bounded.** Review and revelation tracking is attached to the particular
   report, artifact, plan, code change, file, or other reported subject—not a speculative global
   model of the user's memory or a universal per-project cognition ledger.
10. **Exposure is not cognition.** Showing, previewing, opening, reviewing, commenting, accepting,
    approving, and producer disposition are distinct claims.
11. **The multi-topic block remains a candidate, not a universal law:** `TOPIC → MOTIVATION →
    WHAT IS IT? → IMPACT → ACTION`. The reporting shape must still fit the producer's job.
12. **Plain explanation remains necessary.** Fidelity does not license unexplained jargon or force
    the user to reconstruct relationships among terms.
13. **No proactive scheduling or cross-project control is in scope.** The inquiry concerns a
    bounded report and its return path.
14. **Research and product evidence remain separate.** A useful personal system need not be novel,
    and a design hypothesis must not be described as established science.

## 4. Distinctions the research must operationalize

Do not use the following words interchangeably. Define and test the boundary of each:

- **authority:** who may establish or change a lifecycle fact or effect;
- **principal:** whose position, commitment, or interests an utterance represents;
- **author:** who selects the substantive sentiments and wording;
- **animator/voice:** who or what delivers the utterance;
- **stance:** the attributed evaluation, orientation, preference, or recommendation expressed;
- **intent:** the outcome a principal is trying to obtain through the communication;
- **guidance:** attention direction or recommended reasoning that does not itself decide;
- **presentation discretion:** wording, ordering, grouping, pacing, and progressive disclosure;
- **advocacy/persuasion:** communication selected to move the receiver toward an outcome;
- **delegation:** a scoped authorization to act or speak on another's behalf;
- **mediation:** faithful movement and clarification of meaning between parties;
- **orchestration:** control over routing, sequencing, invocation, or lifecycle progression;
- **feedback capture, delivery, acknowledgement, interpretation, disposition, and effect;**
- **review, comment, rejection, acceptance, approval, and deferral;**
- **source fidelity, source attribution, and source endorsement.**

The research should consider whether "Report has no stance of its own but always has an explicit
principal" is a sufficient constitutional rule or merely a slogan that leaves difficult cases
unresolved.

## 5. Research objectives

1. Find the strongest existing theories and empirical work for separating the person or system
   that voices a message from the party that authors or stands behind it.
2. Determine when attributed advocacy supports decision quality and when framing becomes
   manipulation or obscures inconvenient evidence.
3. Identify established models for an intermediary that alternates between expert advice and
   faithful decision/feedback capture.
4. Establish a defensible boundary between a bidirectional reporting loop and a lifecycle
   orchestrator.
5. Determine the minimum provenance, role, and acknowledgement data needed to keep every stance
   attributable and every feedback transition auditable.
6. Compare candidate architectures rather than validating a single preferred answer.
7. Translate relevant book advice without erasing the books' original unified-author assumption.
8. Produce an empirical programme that measures decision quality, intent preservation, and
   authority safety—not preference alone.
9. Answer all 108 supplied questions, identify dependencies among them, and state which remain
   product choices rather than research-settled conclusions.

## 6. Unit of analysis

Use a **stance-bearing report act** as the primary unit, not an entire conversation or project.
For each act, identify at minimum:

- reported subject and stable source;
- speech act or purpose;
- principal whose position is represented;
- source authority and its jurisdiction;
- animator and authoring/transformation roles;
- intended audience and intended effect;
- stance or recommendation, if any;
- evidence and material qualifications;
- requested user action, if any;
- permitted response path;
- what counts as delivered, acknowledged, and dispositioned;
- which party may give the response lifecycle effect.

Then examine how roles change across a complete loop:

```text
producer artifact/position
        ↓ delegated, attributed reporting
Report → user
        ↓ exact response plus identified normalization, if any
Report → relevant producer
        ↓ producer-owned interpretation and lifecycle disposition
next authoritative artifact or explicit unresolved state
```

The diagram is a question to investigate, not an approved protocol.

## 7. Open-question corpus

Paste the full corpus below. Preserve all 108 questions; do not summarize away apparently
duplicative questions because subtle differences may expose different authority failures.

> **[PASTE THE 108 OPEN QUESTIONS HERE]**

For every question, the final research output must record:

| Field | Requirement |
|---|---|
| Question ID | Original stable identifier |
| Short answer | Direct answer, not merely relevant literature |
| Evidence class | Direct evidence, institutional analogy, Astra synthesis, product choice, or unresolved |
| Best sources | Precise primary-source citations |
| Confidence | High, medium, or low, with reason |
| Design consequence | What would change if adopted |
| Authority risk | What boundary could be violated |
| Dependencies | Other question IDs that must be settled first |
| Falsifier | Evidence or result that would reverse the answer |

## 8. Preliminary literature review and starting map

This is a scoping review, not the final literature review. It identifies promising bodies of work,
what they currently appear to contribute, and where transfer to Astra remains conjectural.

### 8.1 Production format, footing, and reported speech — strongest conceptual lead

Erving Goffman's **production format** separates an utterance's animator, author, and principal.
That is unusually close to the present problem: Report may deliver and partially compose language
while a skill or the user remains the party whose position is expressed. Goffman's original
*Footing* is the primary starting point; Clark and Gerrig further show that quotation is a
selective demonstration rather than a neutral reproduction. This warns that even faithful
"voicing" selects aspects of the source. [Goffman, *Footing* (1979)](https://doi.org/10.1515/semi.1979.25.1-2.1),
[Clark and Gerrig, *Quotations as Demonstrations* (1990)](https://web.stanford.edu/~clark/1990s/Clark%2C%20H.H.%20_%20Gerrig%2C%20R.J.%20_Quotations%20as%20demonstrations_%201990.pdf)

**Preliminary transfer:** model the skill or user as the explicit principal of each report act;
model Report's animation and wording separately; make footing shifts visible at the smallest
useful boundary.

**Limit:** this literature analyzes social interaction. It does not specify software authority,
artifact contracts, safe feedback routing, or when a delegated writer may add guidance.

### 8.2 Mixed-initiative interaction and adjustable autonomy

Mixed-initiative HCI rejects a crude choice between direct user control and full automation.
Horvitz emphasizes explicit coupling of automated services and direct manipulation, with
attention to uncertainty, timing, costs, and user control. [Horvitz, *Principles of
Mixed-Initiative User Interfaces* (CHI 1999)](https://www.microsoft.com/en-us/research/publication/principles-mixed-initiative-user-interfaces/)
Adjustable-autonomy and automation-level work further distinguishes information acquisition,
analysis, decision selection, and action, rather than treating "assistance" as one indivisible
permission. [Scerri, Pynadath, and Tambe, *Towards Adjustable Autonomy for the Real World*
(2002)](https://doi.org/10.1613/jair.1037), [Parasuraman, Sheridan, and Wickens, *A Model for
Types and Levels of Human Interaction with Automation* (2000)](https://doi.org/10.1109/3468.844354)

**Preliminary transfer:** Report's initiative and discretion should be scoped by the report act,
recoverable by the user, and explicit about uncertainty and consequence. Guidance need not imply
authority.

**Limit:** classic mixed-initiative systems often infer goals, attention, or context. Astra has
rejected inferred recall and should not import cognition modelling merely because the literature
uses it.

### 8.3 Institutional advice: permanent civil service and special advisers

The UK institutional model distinguishes evidence-grounded, politically impartial civil-service
advice from politically committed special advice, while ministers retain decision accountability.
The Civil Service Code requires truthful facts, accurate options, evidence-based advice, and no
suppression of inconvenient considerations. The Special Adviser Code explicitly permits an
authorized adviser to represent a minister's view with a degree of commitment unavailable to
ordinary civil servants. The Ministerial Code places final decision responsibility on ministers
while requiring due weight to informed advice. [Civil Service Code](https://www.gov.uk/government/publications/civil-service-code/the-civil-service-code),
[Code of Conduct for Special Advisers](https://www.gov.uk/government/publications/special-advisers-code-of-conduct/code-of-conduct-for-special-advisers-html),
[Ministerial Code](https://www.gov.uk/government/publications/ministerial-code/ministerial-code)

**Preliminary transfer:** stance is safer when the source, mandate, degree of commitment, and
decision owner are explicit. A system may need different named roles for evidence advice,
producer advocacy, and user-policy capture rather than one falsely neutral voice.

**Limit:** this is an institutional analogy, not evidence that a single AI component should combine
these roles. Real civil-service actors have law, professional norms, hierarchy, and accountability
mechanisms that Astra does not automatically possess.

### 8.4 Interpreting and faithful mediation

Court and government interpreter codes require accurate, complete rendering without autonomous
addition, omission, advice, or altered meaning; they also require interpreters to flag difficulty
and correct errors. [Illinois Supreme Court interpreter ethics](https://www.illinoiscourts.gov/public/find-a-language-interpreter/language-access-policy-and-code-of-ethics/),
[UK Home Office interpreter code](https://assets.publishing.service.gov.uk/media/69a80567b9bd90e63a252269/Interpreter_code_of_conduct_and_guidance.pdf)

**Preliminary transfer:** exact user responses and producer claims need a protected fidelity path;
clarification and normalization should be visibly separate acts, never silent rewriting.

**Limit:** an interpreter's norm of impartiality is deliberately narrower than the user's desired
stance-bearing guide. Interpreter ethics may define the fidelity floor, not the complete Report
role.

### 8.5 Grounding, acknowledgement, and conversational repair

Clark and Brennan describe communication as coordinated action that requires parties to establish
sufficient common ground under medium-specific costs. This makes delivery alone an inadequate
proxy for successful coordination. [Clark and Brennan, *Grounding in Communication*
(1991)](https://www.cs.cmu.edu/~illah/CLASSDOCS/Clark91.pdf)
Clark and Schaefer's presentation-and-acceptance model and conversation-analysis work on repair
also suggest that communication trouble should be locally correctable and, where possible, the
source of the trouble should repair its own contribution. [Clark and Schaefer, *Contributing to
Discourse* (1989)](https://doi.org/10.1207/s15516709cog1302_7), [Schegloff, Jefferson, and
Sacks, *The Preference for Self-Correction in the Organization of Repair in Conversation*
(1977)](https://doi.org/10.2307/413107)

Recent human–AI work is beginning to operationalize common-ground maintenance and repair, but it
should be treated as emerging rather than settled. [Poelitz, Doshi-Velez, and Lindley, *A
Benchmark to Assess Common Ground in Human-AI Collaboration* (2026 preprint)](https://arxiv.org/abs/2602.21337)

**Preliminary transfer:** distinguish sent, delivered, acknowledged, clarified, interpreted,
accepted, and applied. A return path needs repair when the producer or user disputes Report's
representation.

**Limit:** common ground is not proof of comprehension, agreement, or approval. Astra must retain
observable receipt and response facts rather than infer mental state.

### 8.6 Boundary objects and shared report artifacts

Star and Griesemer show how a boundary object can preserve a common identity while remaining
usable by communities with different local viewpoints. A bounded Report Artifact could function
similarly for producer evidence, Report disclosure state, and user feedback. [Star and Griesemer,
*Institutional Ecology, “Translations” and Boundary Objects* (1989)](https://griesemer.net/wp-content/uploads/2020/12/07-star-griesemer-1989-sss19-3387-420-boundary-objects.pdf)

**Preliminary transfer:** keep one stable, addressable reported subject while making role-specific
entries and interpretations explicit.

**Limit:** boundary-object theory does not determine write authority, resolve conflicts, prevent
staleness, or justify one shared mutable file.

### 8.7 Argumentation and decision-rationale records

IBIS models a decision discourse through issues, positions, arguments, and explicit state; QOC
records questions, options, and criteria so later readers can see the design space rather than
only the selected answer. [Kunz and Rittel, *Issues as Elements of Information Systems*
(1970)](https://escholarship.org/uc/item/5cj786v8), [MacLean et al., *Questions, Options, and
Criteria* (1991)](https://doi.org/10.1080/07370024.1991.9667168)
Software design-rationale work similarly links artifacts, issues, alternatives, justifications,
status, assumptions, and implications so later readers can inspect why a decision exists.
[Potts and Bruns, *Recording the Reasons for Design Decisions* (1988)](https://doi.org/10.1109/ICSE.1988.93722),
[Tyree and Akerman, *Architecture Decisions: Demystifying Architecture*
(2005)](https://doi.org/10.1109/MS.2005.27)

**Preliminary transfer:** the internal artifact can retain who advanced a position, what evidence
supports it, what the user said, and how the producer later dispositioned it. The 108 questions
themselves are better treated as an issue network than as one undifferentiated checklist.

**Limit:** a rationale notation can become burdensome and can accidentally turn Report into the
owner of deliberation. Recording discourse does not grant authority to settle it.

### 8.8 Provenance, attribution, and delegated responsibility

The W3C PROV data model distinguishes attribution, association, and delegation. Its delegation
relation explicitly connects a delegate, a responsible principal, and the scoped activity while
recognizing that the represented party retains responsibility. [W3C PROV-DM](https://www.w3.org/TR/prov-dm/)

**Preliminary transfer:** every stance-bearing transformation may need machine-checkable links for
`who said`, `on whose behalf`, `from which source`, `for which activity`, and `under which role`.

**Limit:** PROV supplies vocabulary, not a user experience, ethical rule, authority constitution,
or evidence that all metadata should be shown in every brief.

### 8.9 Agency and common-agency theory

Principal–agent theory studies divergence between a principal and an agent acting on the
principal's behalf. Common-agency work studies one agent influenced by several principals.
[Jensen and Meckling, *Theory of the Firm* (1976)](https://doi.org/10.1016/0304-405X(76)90026-X),
[Bernheim and Whinston, *Common Agency* (1986)](https://bernheim.people.stanford.edu/publications/common-agency)
Public-administration work separately warns that several incompatible meanings of accountability
can make an intermediary less effective rather than more accountable. [Koppell, *Pathologies of
Accountability* (2005)](https://doi.org/10.1111/j.1540-6210.2005.00434.x)

**Preliminary transfer:** an intermediary serving multiple producer authorities and a user can
face conflicting mandates and cannot safely aggregate them without a constitutional ordering.

**Limit:** Astra's parties are not symmetric economic principals. The user owns policy and
approval; skills own bounded epistemic and lifecycle claims. Economic incentive models are a
warning and vocabulary source, not a ready-made architecture.

### 8.10 Human-compatible assistance and explicit feedback channels

Cooperative inverse reinforcement learning formalizes assistance under uncertainty about human
preferences. More recent assistance-game work shows that partial observability can create
perverse incentives to interfere with what the human sees, and that an explicit communication
channel can remove some of those incentives. [Hadfield-Menell et al., *Cooperative Inverse
Reinforcement Learning* (2016)](https://papers.nips.cc/paper_files/paper/2016/hash/c3395dd46c34fa7fd8d729d8cf88b7a8-Abstract.html),
[Emmons et al., *Observation Interference in Partially Observable Assistance Games*
(ICML 2025)](https://proceedings.mlr.press/v267/emmons25a.html)

**Preliminary transfer:** prefer explicit user feedback and correctable representations over
silent inference of intent; examine whether disclosure discretion gives Report incentives or
opportunities to distort the user's information environment.

**Limit:** Astra should not import latent preference or cognition modelling. These formal models
are primarily a source of failure hypotheses, not an implementation prescription.

### 8.11 Framing, persuasion, and epistemic vigilance

Framing research shows that equivalent decision problems can produce different preferences when
formulated differently. Information-design theory goes further: a sender can strategically choose
what information a receiver sees to influence action even when the receiver understands that the
signal was selected. Epistemic-vigilance work explains why receivers attend to both message and
source when guarding against accidental or intentional misinformation. [Tversky and Kahneman,
*The Framing of Decisions and the Psychology of Choice* (1981)](https://doi.org/10.1126/science.7455683),
[Kamenica and Gentzkow, *Bayesian Persuasion* (2011)](https://web.stanford.edu/~gentzkow/research/BayesianPersuasion.pdf),
[Sperber et al., *Epistemic Vigilance* (2010)](https://discovery.ucl.ac.uk/id/eprint/1331363/)

**Preliminary transfer:** Report's ordering, progressive disclosure, and content selection are not
neutral mechanics. Producer stance, omitted material, qualifications, and the sender's objective
must remain inspectable so the user can evaluate both argument and source.

**Limit:** these sources establish risks and mechanisms, not a requirement to dump all information
at once. Research must seek designs that preserve vigilance without recreating overload.

### 8.12 Trust and appropriate reliance

Human-automation research argues that the goal is appropriate reliance calibrated to actual
capability, not maximal trust. [Lee and See, *Trust in Automation: Designing for Appropriate
Reliance* (2004)](https://user.engineering.uiowa.edu/~csl/publications/pdf/leesee04.pdf)
Experiments also show why explanation and fluency are insufficient success measures: an
explanation can increase acceptance or reliance without reliably improving team performance.
[Dzindolet et al., *The Role of Trust in Automation Reliance* (2003)](https://doi.org/10.1016/S1071-5819(03)00038-7),
[Bansal et al., *Does the Whole Exceed its Parts?* (CHI 2021)](https://doi.org/10.1145/3411764.3445717)

Recent decision-support work also questions the narrow accept/reject-advice model and examines
interfaces that cue information gathering, alternatives, and reasoning. [Sivaraman et al.,
*Intelligent Reasoning Cues* (CHI 2026)](https://doi.org/10.1145/3772318.3790953)

**Preliminary transfer:** evaluate whether Report improves discrimination, inspection, and
decision quality. Do not optimize for agreement with the producer, trust in Report, or user
preference alone.

**Limit:** most studies use bounded tasks and one advisor. Transfer to longitudinal software
engineering, multiple authoritative producers, and policy feedback remains unestablished.

### 8.13 Preliminary synthesis

The literature does not yet reveal a single established model matching Astra. It does, however,
support a promising composite hypothesis:

1. Treat **principal, author, and animator** as distinct roles.
2. Make every footing or principal shift **explicit and attributable**.
3. Let a producer supply its conclusion, rationale, recommendation, qualifications, and desired
   action; let Report guide through those supplied semantics without inventing them.
4. Preserve an **exact channel** for user intent and distinguish any Report-authored normalization.
5. Track the communication loop through **observable states**, never inferred understanding.
6. Keep conflicting positions separate and use a stable, bounded artifact as a possible boundary
   object and rationale record.
7. Treat presentation as consequential: ordering and omission can persuade, so progressive
   disclosure requires visible provenance, material completeness, and inspectable deferral.
8. Measure whether the arrangement improves **decision quality and feedback fidelity**, not merely
   whether it feels concise or authoritative.

Every item above is an **Astra synthesis**, not an established finding. Deep Research must try to
falsify it and compare it with simpler alternatives.

## 9. Required search method

Conduct a transparent scoping review followed by targeted deep dives. Do not call it systematic
unless a reproducible protocol and coverage claim are actually satisfied.

### 9.1 Source strategy

- Search through **2026-08-19**.
- Prefer original papers, books, standards, official codes, and empirical studies.
- Use reviews to map a field and snowball citations, but verify important claims in primary
  sources.
- Search ACM Digital Library, IEEE Xplore, ACL Anthology, Springer, ScienceDirect, JSTOR,
  Web of Science or Scopus where available, Google Scholar, institutional repositories, W3C,
  official government sources, arXiv/OpenReview/PMLR for recent work, and relevant HCI, CSCW,
  organizational studies, pragmatics, sociolinguistics, public administration, economics, and AI
  venues.
- Perform backward and forward citation chaining from the strongest anchors in section 8.
- Record search date, query, database, inclusion decision, and version status.

### 9.2 Starting search concepts

Combine terms rather than searching only for `AI report`:

- `footing`, `production format`, `animator author principal`, `reported speech`, `voice`,
  `stance attribution`;
- `mixed initiative`, `adjustable autonomy`, `human control`, `delegated agent`, `authorized
  representative`;
- `common ground`, `grounding`, `acknowledgement`, `repair`, `feedback loop`, `intent
  preservation`;
- `boundary object`, `boundary spanner`, `knowledge broker`, `liaison`, `intermediary`;
- `principal agent`, `common agency`, `multiple principals`, `delegation`, `stewardship`;
- `civil service advice`, `special adviser`, `ministerial responsibility`, `speaking on behalf`;
- `interpreter role`, `faithful mediation`, `role conflict`, `advocacy interpreting`;
- `design rationale`, `IBIS`, `QOC`, `argumentation`, `decision record`, `comment disposition`;
- `framing`, `information design`, `persuasion`, `source credibility`, `epistemic vigilance`;
- `human AI decision support`, `appropriate reliance`, `contestability`, `cognitive forcing`,
  `reasoning support`;
- `multi-agent provenance`, `delegation provenance`, `authorship attribution`, `audit trail`.

### 9.3 Inclusion and exclusion

Include work that directly informs role separation, attributed stance, delegated communication,
feedback closure, authority boundaries, decision support, or their measurable failure modes.

Exclude or downgrade:

- generic writing advice already covered by the local book distillation;
- prompt-engineering lists without evaluation;
- product blogs making unsupported novelty claims;
- systems that merely summarize chat history;
- research whose only outcome is aesthetic preference;
- fictional portrayals offered as organizational evidence;
- claims about user recall, comprehension, or preference inferred only from exposure;
- formal models whose assumptions are incompatible with Astra unless the mismatch is explicit.

### 9.4 Evidence discipline

For each proposed conclusion, preserve four layers:

1. **Source finding:** what the source actually establishes.
2. **Transfer distance:** direct evidence, institutional analogy, or distant analogy.
3. **Astra synthesis:** the mechanism proposed for this architecture.
4. **Product choice:** any concrete default, field, status code, or interaction rule.

Also record contrary evidence, failed transfers, null results, and boundary conditions. Do not
manufacture empirical support for numeric budgets, status vocabularies, or protocol fields.

## 10. Required comparative analysis

At minimum, compare these architectures:

### A. Output-only neutral renderer

Report structures producer facts but claims no stance; user responses remain direct to the
producer. This is close to the current repository model.

### B. Output-only attributed producer advocate

Report may guide from the producer's supplied stance, but the user's return path remains direct.

### C. Bidirectional stance-switching mediator

One Report surface voices the producer outbound, captures the user inbound, and transports the
response under explicit principal switching; producers retain interpretation and lifecycle effect.

### D. Split reporter and feedback secretary

One conceptual skill exposes two sharply separated roles or modules: an attributed producer-facing
reporter and a user-facing recorder/return channel.

### E. Shared bounded Report Artifact

A report-scoped artifact holds source positions, disclosure/review state, exact user responses,
and producer dispositions as separately owned entries. Report renders the artifact but does not
own all fields.

Do not assume these are mutually exclusive. Compare combinations and propose another architecture
if evidence warrants it.

For every candidate, evaluate:

- principal and authority clarity;
- quality and legitimacy of guidance;
- user intent fidelity;
- closed-loop feedback reliability;
- conflict handling across producers;
- risk of stance laundering or manipulation;
- orchestration creep;
- artifact ownership and write contention;
- progressive-disclosure compatibility;
- host/runtime feasibility;
- auditability and testability;
- graceful degradation;
- cognitive and interaction cost.

## 11. Required threat model and hard cases

Analyze at least these failures:

- Report presents its own inference as a producer recommendation.
- A producer uses Report's framing discretion to hide inconvenient evidence.
- Report's concise wording changes the strength or scope of a claim.
- The user comments on one section and the feedback is routed to the wrong skill or revision.
- Exact user words and Report's normalized interpretation diverge.
- The producer receives feedback but never acknowledges or dispositions it.
- Report marks reviewed material as approved, or approval as producer acceptance.
- Two skills recommend incompatible actions within overlapping jurisdictions.
- A user policy conflicts with a skill's evidence or safety constraint.
- One utterance changes principal mid-paragraph without a visible boundary.
- Report claims to speak for "the six skills" when no common position exists.
- A stale Report Artifact continues to guide after the authoritative source changes.
- Concurrent producers write incompatible state into one shared artifact.
- Progressive disclosure delays a material caveat or counterargument.
- The user cannot distinguish persuasion, explanation, and required action.
- Feedback transport implicitly starts work or crosses a lifecycle gate.
- Host limitations remove attribution or acknowledgement controls.
- Report is unavailable during a decision or feedback-return boundary.

For each failure, identify prevention, detection, repair, and the authority that owns repair.

## 12. Contract questions the research must inform

Do not pre-approve a schema, but determine whether a minimal report act needs equivalents of:

- report/subject ID and source revision;
- producer and jurisdiction;
- principal, author, animator, and transformation agent;
- speech-act or intent type;
- source position, recommendation, and requested action;
- evidence, qualifications, alternatives, and conflicts;
- degree and source of stance or commitment;
- exact user response and separately marked normalization;
- target producer and source section/claim;
- delivery, acknowledgement, interpretation, and disposition events;
- lifecycle-effect reference;
- supersession and correction links.

Research whether principal switching should be expressed per message, segment, section, claim, or
field. The answer must balance unambiguous provenance with the user's wish not to be swamped by
terms and metadata.

Likewise investigate the proposed review symbols—such as `UR`, `RV`, `CM`, `RJ`, `AP`, and `DF`—
as a multidimensional state problem rather than accepting one flat enum. Determine which states
belong to disclosure, user review, user decision, producer acknowledgement, producer disposition,
and lifecycle effect.

## 13. Required empirical programme

Propose studies with objective consequences. Suitable tasks include code review, architecture
choice, test-result review, incident response, security findings, plan approval, and revision
feedback.

Compare at least:

- neutral output-only rendering versus attributed producer stance;
- direct feedback versus Report-mediated exact-plus-normalized feedback;
- implicit voice versus explicit principal/stance markers;
- one bidirectional role versus split reporter/secretary roles;
- flat prose versus a bounded Report Artifact with traceable section state;
- progressive disclosure with and without visible counter-position and caveat cues.

Primary outcomes should include:

- correct identification of whose view is being expressed;
- decision and prioritization accuracy;
- material caveats missed;
- user-intent preservation across the round trip;
- routing accuracy to the responsible producer;
- false approval or authority transitions;
- producer acknowledgement/disposition traceability;
- time to correct action;
- evidence inspected before consequential decisions;
- repair frequency and success;
- workload and confidence calibration.

Preference and perceived clarity are useful secondary outcomes only. Pre-register hypotheses where
appropriate and explicitly admit useful negative results—for example, that explicit stance
metadata overwhelms the user, that direct feedback is safer, or that a split role is more
predictable than a unified one.

## 14. Required Deep Research deliverables

Return one coherent research package containing:

1. **Executive answer:** the best current answer to the central question and the most important
   unresolved risk.
2. **Conceptual model:** precise definitions and a mapped User–Report–Producer production format.
3. **Preliminary-review expansion:** a source matrix covering the relevant fields, including
   contrary and null evidence.
4. **108-question coverage matrix:** no omissions; dependencies and P0 questions identified.
5. **Architecture comparison:** at least candidates A–E, with a justified recommendation or an
   explicit reason not to choose yet.
6. **Authority-and-stance matrix:** who may assert, transform, present, record, acknowledge,
   interpret, disposition, and apply each kind of content.
7. **Round-trip state model:** observable events and non-equivalent states from source creation
   through feedback disposition.
8. **Report Artifact options:** ownership, field provenance, mutation rules, concurrency,
   supersession, correction, and degradation.
9. **Threat model:** prevention, detection, repair, and residual risk.
10. **Worked examples:** at least one ordinary report, one approval request, one user comment,
    one policy direction, one disagreement between skills, one rejected recommendation, and one
    corrected misrepresentation.
11. **Empirical evaluation plan:** falsifiable hypotheses, conditions, tasks, objective outcomes,
    and negative-result interpretation.
12. **Repository reconciliation:** exact current clauses that would remain, change, or be
    superseded if the recommendation were later approved. This is analysis only, not an edit.
13. **Research gaps and product choices:** what evidence cannot settle.
14. **Primary-source bibliography:** stable URLs/DOIs, dates, versions, and short annotations.

## 15. Repository reading list

Before recommending changes, read at minimum:

- `README.md`
- `docs/design-requirements.md`
- `docs/design-roadmap.md`
- `designs/astra-report.md`
- `designs/astra-critique.md`
- `designs/astra-understand-code.md`
- `designs/astra-spec.md`
- `designs/astra-implement.md`
- `designs/astra-test.md`
- `designs/astra-ship.md`
- `docs/research/2026-08-12-astra-report-method-canon.md`
- `docs/research/2026-08-17-astra-report-research-to-design-reconciliation.md`
- `docs/research/2026-08-18-astra-report-book-distillation.md`
- `docs/superpowers/plans/2026-08-17-astra-report-v1.md`

When translating the book distillation, always preserve both:

- the book's original advice to a writer who usually owns the case and route; and
- the proposed Astra integration after production roles and principals are separated.

Do not retroactively claim that the books themselves prescribe Astra's eventual solution.

## 16. Quality and authority bar

- Do not treat the Hacker–Bernard–Humphrey analogy as evidence.
- Do not claim novelty for progressive disclosure, executive summaries, attributed speech,
  mixed-initiative interaction, or feedback loops.
- Do not describe Report as neutral if its selection and ordering influence decisions.
- Do not describe Report as authoritative merely because it delivers an authoritative skill's
  position.
- Do not collapse the user's ultimate authority with the producer's domain authority.
- Do not collapse delivery, review, agreement, approval, acknowledgement, disposition, or effect.
- Do not infer user cognition or latent preference when an explicit feedback channel can be used.
- Do not hide inconvenient evidence, qualifications, conflicts, or unreviewed material.
- Do not convert an institutional analogy into a software requirement without marking the
  transfer.
- Do not optimize for agreement, trust, brevity, or preference at the expense of decision quality
  and inspectability.
- Do not silently amend repository designs or implementation plans.
- Do not authorize a runtime, schema, ledger, skill installation, source retirement, roster
  promotion, or lifecycle transition.
- Cite every material research claim near the claim, prefer primary sources, and distinguish
  peer-reviewed, preprint, standard, official code, and theoretical work.
- State when the evidence is absent, mixed, task-specific, or too distant to settle an Astra
  product choice.

## 17. Decision standard

The research succeeds only if it lets the user make a nuanced constitutional decision among
plausible designs. Its recommendation should answer:

> **Can Report lead the communication without owning the underlying truth or decision, and can it
> return the user's stance without becoming the authority that interprets or executes it? If yes,
> what explicit production roles, provenance, state transitions, and failure boundaries make that
> arrangement trustworthy?**

If the evidence does not support a unified stance-switching role, say so and identify the smallest
separation of roles that preserves the user's desired guidance and feedback loop.
