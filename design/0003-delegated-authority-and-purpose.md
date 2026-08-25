# 0003: Delegated Authority and Declared Purpose

**Status:** Draft for author decision
**Date:** 2026-08-25
**Produces:** `spec/DEFER-v1.0.md`, `spec/POLARIS-v1.0.md`, six schemas
**Source citations:** This note cites specific machine absolute paths as evidence of the survey that grounded the design. Normative text uses path anchors only.

---

## 1. What prompted this

Two requests, one session. First: the spec must address agent authority delegation, with the org chart, RACI, and reporting structure at `/Users/sthornock/code/epic/epic-flowstate-community/.flowstate/agents/ORG_CHART.md` as the reference, a Tim Ferriss style monetary threshold for friction removal, and the Eisenhower matrix for priority and delegation. Second: the brain needs a declared purpose, values, tenets, mottos, beliefs, and drivers, sitting above all other specs, consulted on every decision and every crossing, with the Four Agreements as a model and "Guiding Light" or "Morning Star" as the naming instinct.

These produced two documents. They are separate because one is a mechanism and one is a reason, and collapsing them would let the reason be used as a mechanism, which is section 8 of POLARIS.

---

## 2. What the reference implementation already has

Read from `epic-flowstate-community` before designing anything.

- 109 role files in `.flowstate/agents/`, one JSON per org role, each with `capabilities`, `tools`, `permissions.mode`, `metadata.orgRole`, and a `hooks.PreToolUse` matcher on `*` invoking `compliance-audit-log.mjs` and `agent-policy-block.mjs`
- `ORG_CHART.md`, 490 lines, a rendered reporting tree from CEO down through five C level branches to individual contributors
- `packages/flowstate-coordinator/src/seeds/default-policies.ts`: an `approval_tiers` policy with `low_risk` through `critical_risk`, each mapping step kinds to a strategy of `auto_approve`, `agent_approve`, or `human_approve`, plus `minApproverLevel`, `approverChain: 'reporting_hierarchy'`, and `escalationTimeoutMinutes`. Also `agent_daily_quota` at 20 proposals, `circuit_breaker` at 3 consecutive failures, `step_timeout`, and a disabled `reaction_matrix`
- `packages/flowstate-coordinator/src/ApprovalResolver.ts`, 242 lines: walks the reporting hierarchy for a manager with `level <= minLevel && level > 0`, excludes level 0 system agents, and falls back to `medium_risk` for an unknown step kind
- `packages/flowstate-runner/src/handlers/approval.rs`: builds approval records with escalation metadata and a quorum mode assigning one row per approver

This is a working approval system. Most of what DEFER requires exists here in some form, which is why DEFER is written as a correction rather than an invention.

Also read: the personal brain at `/Users/sthornock/code/obsidian/brain/AGENTS.md` line 381 carries a **change authority table** with four levels, Mechanical, Structural, Substantive, Factual, each with a stated agent authority, and the rule "when classification is uncertain, use the more conservative level." Seven agents in `.claude/agents/` operate under it, and `groundskeeper.md` states plainly that it holds mechanical authority only and that "deletion is never yours."

That table is the seed of the whole design. It is already the right shape: authority scoped by kind of change rather than by rank. DEFER generalizes it from four levels over text edits to four axes over every act class.

---

## 3. The two compressions

The reference implementation compresses the problem twice.

**Act kind as a proxy for consequence.** A `code_change` to a draft and a `code_change` to the constitution are the same kind and route identically. Kind names the verb and says nothing about the target, so every decision maps to the nearest tier and the distinctions that matter vanish exactly where they matter.

**Seniority level as a proxy for authority.** A single scalar compared against a per tier minimum makes authority a total order, which makes every sufficiently senior role eligible to approve everything. The CFO sits at level 2 and is therefore eligible to approve a production deploy. Authority is not a total order; it is a set of overlapping bounded regions.

Two smaller consequences follow. An unknown step kind falls back to `medium_risk`, which is agent approvable, so an act nobody anticipated is authorized by an agent rather than refused. And there is no magnitude bound anywhere in the system, so the single most useful delegation control in practice, a numeric ceiling under which an agent simply acts, cannot be expressed at all.

---

## 4. The central claim of DEFER

**The reporting chain and the delegation chain are different graphs.** The reporting chain is a tree and it answers who must be informed. The delegation chain is a forest of signed grants and it answers who may decide. `approverChain: 'reporting_hierarchy'` conflates them, which makes the correct approver structurally unreachable whenever competence does not track seniority, and it never does.

From that follow the four axes. An envelope is an act class set, a decidable scope predicate, a magnitude bound, and a condition set. All four required; a missing axis is malformed rather than unbounded. Coverage between envelopes is mechanically computable, and coverage is the basis of both routing and the redelegation subset rule.

Routing goes to the **least authorized covering holder**, not the most senior. This is the operational inversion. Routing upward by default fills the owner's queue with decisions three roles below were authorized to make.

---

## 5. The Ferriss threshold, generalized

The refund limit instinct is correct and its general form is: high volume, low consequence, bounded magnitude, no approval, full logging.

The generalization has two parts the original does not.

**Non monetary meters.** Currency is one meter and rarely the important one. The six required meters are `currency`, `records-affected`, `reversibility`, `exposure-delta`, `authority-delta`, and `external-recipients`. The last two carry the most weight, because their effects survive reversing the act: restoring a sensitivity label does not unpublish, and revoking a grant does not un decide what was decided under it. A meter MUST be computable before the act, which disqualifies most tempting ones.

**The refund fallacy.** An agent authorized to approve refunds up to one hundred is authorized to disburse an unlimited amount in units of one hundred. Every bound therefore needs a per act ceiling and a windowed aggregate. And the aggregate MUST be computed per delegation chain, not per actor, because a per actor quota is escaped by provisioning more agents, which an agent org does trivially. The existing `agent_daily_quota: 20` is per agent and unweighted, so it is escapable on both counts.

---

## 6. The Eisenhower correction

The matrix cannot be used as drawn. Its top cell prescribes do it yourself for important and urgent work, which in an agent org reads as: the more consequential and the more pressing, the more the owner personally handles. That is the exact curve the system exists to flatten, and it concentrates the owner where there is least time to think. The matrix also uses "importance" for two things, how much the outcome matters and how bad it is if the decision is wrong, and delegation only cares about the second.

The correction keeps both axes and gives each one job. **Consequence determines who may decide.** **Urgency determines what happens while the decision waits.** Nothing else, either way.

The resulting rule is the one worth defending: **urgency MUST NOT widen an envelope**, substitute an available approver for an authorized one, or convert a human required decision into an agent resolvable one. A brain where urgency raises the ceiling has an escalation path any actor can open by asserting urgency, and urgency is an input supplied by the proposer.

The dangerous quadrant, high consequence and high urgency, is handled by pre authorization instead. A **break glass envelope** is narrow, magnitude bounded, granted in calm conditions, notifies the owner on use, and self suspends pending review. What can be pre authorized for urgent use is the act that reduces exposure: roll back, quarantine, revoke, halt. Never the act that increases it. Frequent break glass use is the signal to widen an envelope deliberately, not the signal that the system is working.

---

## 7. Timeouts

`escalationTimeoutMinutes: 60` on a `human_approve` tier raises the question the reference implementation does not answer: what does the timeout resolve to. Three dispositions exist and no brain may define a fourth.

`lapse` resolves denied and is the default, because its cost is latency and its failure mode is visible. `default-safe` executes a pre declared alternative that is itself independently authorized, so a timeout cannot execute an act nobody granted. `hold-open` keeps the request pending and turns a health check red, which is the honest option where doing nothing is also a decision.

A timeout MUST NOT resolve as approved, at any class, under any urgency. And escalation goes up, never around: reassigning to a less authorized or laterally positioned role because the authorized holder is unavailable is the most common real failure, because it is indistinguishable from availability management while silently relocating authority to whoever is awake. Unavailability is a vacancy, and a vacancy times out rather than reroutes.

This is also how Blueprint principle 8 and the no approval by timeout rule hold at once. Nothing waits on the owner indefinitely and silently, and every waiting decision becomes a denial, a safe act, or a red check, none of which is an unauthorized act.

---

## 8. RACI with teeth

Accountable holds the envelope, exactly one, and a RACI matrix assigning Accountable to a role with no covering envelope is describing an organization that cannot make the decision it claims to own. Responsible performs and usually holds no authority at all, which is the correct shape for most agents.

Consulted is where RACI usually rots. Two rules fix it. Consultation MUST be evidenced by a response or a recorded non response, or it documents an intention rather than a control. And a non responsive consulted party is recorded and the decision proceeds, because otherwise Consulted becomes a veto held by someone with no envelope, exercisable by inaction, invisible in the policy. That is how approval workflows stall without anyone having denied anything.

This looks like it contradicts the vault rule that approval is never inferred from silence. It does not. Silence never grants, absolutely, for an Accountable party. Silence may fail to block, for a Consulted party. The distinction is that A holds an envelope and C does not.

---

## 9. The owner load budget

The measure of whether any of this works is not the quality of the approvals. It is the size and age of the owner's queue.

A long owner queue is normally read as diligence. It is more often evidence that envelopes are too narrow, coverage gaps went unclosed, roles sit vacant, or classification overstates consequence. All four are fixable and none gets fixed while the queue is read as a sign of care.

So the Charter declares an owner load budget, a maximum decision count per period and a maximum age pending, and exceeding it is a **governance defect** reported as one, not a busy week. The actionable output is the ranked list of coverage gaps at the owner: the top of that list is the next grant that should be written.

---

## 10. Why POLARIS is a separate document

Every other document in the stack is mechanically excellent and entirely amoral. SPEAK will faithfully sign an utterance that should never have been said. CONFIDE will correctly catalog a call the owner would be ashamed of. TRACE will seal the evidence. DEFER will route it to an authorized approver who approves it under a valid envelope, and the ledger will be clean. Every check passes and the outcome is wrong.

POLARIS declares the ends. It required its own document because the reasoning that governs a purpose statement is the opposite of the reasoning that governs a mechanism: a mechanism should be as capable as possible, and a purpose statement should be as inert as possible in the direction of permitting.

---

## 11. The enforceability test

Nearly every declared value in existence is unfalsifiable. Integrity cannot be breached in a way anyone can point at. This is not a flaw in sincerity, it is a structural property, and it has a predictable consequence: unfalsifiable values get cited on both sides of every hard call, deciding nothing while appearing to decide everything.

So one test governs the whole document. An element must be able to produce a decidable refusal, a measurable obligation, or a recorded tie break on some concrete act. Passing makes it normative and citable. Failing makes it non normative, marked, and forbidden as grounds for any decision.

That test yields the tiering, in descending order of force:

- **Refusals** are decidable predicates that fail closed. This is where values actually live, and writing POLARIS is mostly the work of converting aspirations into refusals.
- **Obligations** are measured over a window and reported, because there is no moment at which the brain can be stopped from failing to have done something. This asymmetry is permanent, so where a value can be phrased either way, phrase it as a refusal.
- **Loyalties** are a total published order.
- **Standards** break ties among options already permitted, which is a smaller job than tenets usually get and a job they can do.
- **Mottos** are non normative on purpose, kept because compression is how a value survives being handed to a new agent definition, and forbidden as grounds because the memorable phrase is exactly the one that comes to mind when a justification is needed.

---

## 12. The one way precedence rule

POLARIS holds the highest precedence for forbidding and none for permitting. It may add constraints to every other document. It may never remove or satisfy one.

The reason is that the top of any hierarchy is the most dangerous place to put a permission, and a purpose statement is the most invocable text an organization will ever write: broad, sincere, unfalsifiable. If purpose could permit, every constraint in the stack would acquire an override phrased as service to the mission, available exactly when the constraint mattered.

Every serious mission driven failure has this shape. The mission was real, the constraint was inconvenient, the mission was senior to the constraint, and nobody lied. The rule removes the move entirely, which is cheaper than being the kind of organization that would decline to make it.

The concrete version: a brain may refuse to send anything to a C4 Open provider, which is a refusal doing real work. A brain may not declare that its purpose makes a C4 endpoint effectively C1. The first narrows what is permitted. The second relabels a fact.

---

## 13. Two more rules worth defending

**A refusal predicate may not require inference to evaluate.** If a model decides whether an act violates the brain's values, the values are the model's, filtered through a prompt, subject to the provider's policy, revisable with no amendment record. A brain that enforces its ethics by asking an external provider whether something is ethical has outsourced the one thing it cannot outsource, and outsourced it to the party CONFIDE exists to hold at arm's length. Where a value truly cannot be reduced to a predicate, the answer is a narrower refusal capturing the mechanically detectable part, or a standard, which is honest about being advisory.

**Amendment cannot happen in the same decision as the act it would have blocked.** The moment a refusal costs something is the moment its removal looks most reasonable and the reasoning is least trustworthy. A cooling period does not prevent the amendment; it ensures the amendment is made by someone not currently holding the invoice. And the blocked act does not become retroactively permitted; it is re proposed.

Two supporting mechanisms. Elements are append only, so a withdrawn refusal stays visible with its cause and date, which makes the brain's character history readable and is the record every organization would prefer not to keep. And precedents are subject to the one way rule exactly as purpose is, because otherwise a values set is loosened by a sequence of individually defensible resolutions, none of which was an amendment, and nobody can identify the moment the value changed. That is how drift actually happens. It never happens by amendment.

---

## 14. The dead refusal problem

A refusal that has never fired is either perfectly deterrent or broken and inert since the day it was written, and from outside these are indistinguishable. So every refusal is tested on a declared interval by seeding an act it should block. A failing test is a conformance failure, not a maintenance item: between the failure and the fix, the brain does not have that value.

The standards analogue: a standard cited in nearly every decision discriminates nothing and should be retired or sharpened, and one never cited is not in use. Both are reported.

---

## 15. Loyalties

The best new idea in POLARIS and the one absent from the source material. When interests conflict, something gives way, and a brain that has not declared which will decide it differently each time, under pressure, in favor of whoever is present.

The order MUST be total, because a tie is an undeclared order. It MUST NOT be reordered for a single decision by anyone including the owner, because an order that can be reordered in the moment is a menu, and the function of a menu at decision time is to supply the justification for whatever was going to happen.

And it MUST be published to peers. This is uncomfortable, since it usually means telling a client they rank below the owner while all marketing implies otherwise. Publishing anyway is both more trustworthy and more useful: a peer who knows where they sit can decide what to share, and a peer implicitly promised primacy discovers otherwise in the worst circumstance.

Record subjects deserve specific attention. They are absent from the conversation, unrepresented in the decision, and most affected by a boundary failure. A loyalty order omitting them has not forgotten them; it has ranked them last without saying so.

---

## 16. The Four Agreements, sorted

Applied honestly, the taxonomy splits them three ways and rejects one as written, which is the evidence it does any work.

| Agreement | Kind | Form |
|---|---|---|
| Be impeccable with your word | Refusal | Do not emit an assertion unsubstantiated at the declared evidence grade |
| Don't make assumptions | Refusal | Do not record an unverified inference at the grade of a verified one |
| Don't take anything personally | Standard | Where critique and defense are both available, prefer evaluating the critique |
| Do your best | Refusal, restated, plus a motto | Do not present work at a stage implying review not performed |

Two observations. The first two agreements were already half implemented before being declared, as the SPEAK provenance requirement and the TRACE evidence grades, which is a good sign about both. And "do your best" fails the test as written, having no failing condition, making it the member most likely to be invoked as general justification. It survives only as the mechanically detectable part, which is the refusal to misrepresent effort. The remainder stays as a motto, marked non normative.

---

## 17. Naming

`DEFER` for the authority document. The double meaning is exact: an agent defers to authority, and a decision is deferred upward. Loose expansion: Delegated Envelopes, Fiduciary duty, Escalation, Records. Plain alternative if the acronyms are getting thick: `ADP/1.0`, Agent Delegation Protocol.

`POLARIS` for the purpose document, chosen against the Guiding Light and Morning Star instinct. Polaris is specifically the star you orient by rather than travel to, which is the correct relationship to a purpose statement: you never arrive at it. It is a noun where the others are verbs, which signals correctly that it is a reference frame rather than an action. The expansion is honest, each word being a real section: Purpose, Obligations, Loyalties, Alignment, Refusals, Identity, Standards. Plain alternative: `PVS/1.0`, Purpose and Values Specification. Morning Star remains available as the motto for the document, which is the correct place for it, being non normative by construction.

---

## 18. Open decisions

1. `DEFER` versus plain `ADP/1.0`. `POLARIS` versus plain `PVS/1.0`
2. Was splitting purpose from authority right, or should refusals have lived inside DEFER as a special envelope kind. The recommendation is the split, on the grounds in section 10, but it is two more documents to maintain
3. Six required meters, or fewer. `authority-delta` and `exposure-delta` are the load bearing pair; `external-recipients` may be redundant with the CONFIDE and SPEAK ledgers
4. Should `reversibility` be a meter or a separate axis. It behaves differently from the others, being a floor rather than a sum
5. Whether the strict subset rule on redelegation is too strict in practice. It guarantees chain termination, but it means a role cannot hand a peer role its exact authority during leave
6. Owner load budget numbers for the personal brain and for D7R. This is the one number that determines whether the system is judged to be working
7. Whether break glass envelopes ship in v1 or wait for evidence of need
8. The actual loyalty order for the personal brain, and separately for D7R. These are author decisions and cannot be drafted
9. The actual first refusal set. Recommendation is to start with three and grow, since an untested refusal is worse than an absent one
10. Whether absolute refusals ship in v1 at all. A pattern of amending absolutes is worse than never declaring them
11. Cooling period length. Long enough to matter, short enough not to be routed around
12. How the existing four level change authority table in the vault maps onto act classes. The proposal is Mechanical to `apply-mechanical`, Structural and Substantive to `apply-substantive` split by scope and magnitude, Factual to `apply-substantive` with a verification condition. That is a real change to a working table and should be an explicit author decision
13. Whether the 109 role files in `epic-flowstate-community` get envelopes, or whether a much smaller subset is the real org

---

## 19. Suggested build order

DEFER first, because POLARIS refusals are evaluated at DEFER decision points and the ledger has to exist before it can carry them.

1. Define roles for the seven existing agents in the personal brain. Envelopes come later; the role objects and the vacancy report come first
2. Port the four level change authority table to act classes and scopes. This is the smallest real envelope set and it already works informally
3. Build the classifier for the six meters, seeded to fail on an unclassifiable act. Classification before routing, and classification is the brain's job
4. Two sided reconciliation over the existing `System/Logs/` entries, which will find acts without decision records immediately
5. Grants with human root verification and digest pinning. Cheap, and everything depends on it
6. Routing to the least authorized covering holder, with the coverage gap report as the primary output
7. Timeout dispositions, with `lapse` everywhere until there is a reason for anything else
8. The owner load budget, declared honestly and then measured

Then POLARIS.

9. Write the purpose statement. One statement, author only, cannot be drafted by an agent
10. Write the loyalty order for the personal brain. Total, published, uncomfortable
11. Convert three aspirations to refusals with decidable predicates. Start with the two Four Agreements members that map cleanly, since their machinery already exists in SPEAK and TRACE
12. Wire refusal evaluation into the five existing gates, in the order of section 9.3: governing document first, POLARIS second
13. Build the interval test harness and run it before believing any refusal
14. Declare the standards, and start counting citations so the discrimination test has data
15. Only then consider absolutes, and only for things already survived without exception for a year
