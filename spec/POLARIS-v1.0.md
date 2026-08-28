# POLARIS: Purpose, Obligations, Loyalties, Alignment, Refusals, Identity, Standards

## Version 1.0

**Specification:** POLARIS/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0, DEFER/1.0, CONFIDE/1.0, TRACE/1.0, RETAIN/1.0, for vocabulary. References to SPEAK/1.0 are informative until that specification locks. Precedence position is not dependency: POLARIS remains the root of the precedence order (section 8).

---

## Abstract

A brain exists for a reason. The owner has a purpose, a set of things they will not do, an order of loyalties, and standards of work, and the brain is an instrument of those or it is an instrument of nothing in particular. Every other document in this stack answers how knowledge is held and moved. POLARIS answers what it is all for, and it sits at the top of the precedence order because a correctly executed act in service of the wrong end is still the wrong act.

Most statements of purpose and values are unenforceable, and that is not a flaw in their sincerity. It is a structural property: a value phrased as a virtue cannot be violated in a way anyone can detect. POLARIS is built around a single test. A declared element that cannot produce a decidable refusal, a measurable obligation, or a recorded tie break is decoration, and it MUST be marked as such so it can never be cited as authority.

POLARIS therefore separates what is normative from what is memorable. Refusals are mechanically decidable and fail closed. Obligations are measured against a declared metric. Loyalties are an ordered list, published, and not reorderable in the moment. Standards break ties between options that are already permitted. Mottos are explicitly non normative, kept because compression aids recall, and forbidden as grounds for any decision.

The document's load bearing rule is asymmetric precedence. POLARIS has the highest precedence for forbidding and no precedence at all for permitting. Purpose may narrow what a brain will do. It may never widen it, and it may never excuse a violation of any other document in the stack. Mission as justification for exception is the specific failure this rule exists to make impossible.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Three requirements are absolute and admit no configuration. A POLARIS element MUST NOT confer a permission, relax a constraint, or excuse a failure under any other specification in this stack. A refusal MUST NOT be amended in the same decision that would have been blocked by it. A motto MUST NOT be cited as the basis of a decision.

---

## Table of Contents

1. Introduction
   1.1 Why the brain needs a reason
   1.2 Why values documents fail
   1.3 The enforceability test
   1.4 Position in the stack
2. Definitions
   2.1 The seven element kinds
   2.2 Normative and non normative
   2.3 Decidable
   2.4 Red check
3. Identity and Purpose
   3.1 The single purpose statement
   3.2 Identity
   3.3 What purpose is used for
   3.4 What purpose may not be used for
4. Refusals
   4.1 Refusals are the load bearing layer
   4.2 Form of a refusal
   4.3 Mechanical decidability, and why a model may not evaluate one
   4.4 Absolute and conditional refusals
   4.5 The dead refusal problem
5. Obligations
   5.1 Form of an obligation
   5.2 Why obligations cannot fail closed
   5.3 Metric and window
6. Loyalties
   6.1 The loyalty order
   6.2 The order is not reorderable
   6.3 Publication and the uncomfortable disclosure
   6.4 Conflicts of interest
7. Standards and Mottos
   7.1 Standards break ties, they do not grant permission
   7.2 Citation and the discrimination test
   7.3 Mottos are non normative on purpose
8. The One Way Precedence Rule
   8.1 Highest precedence to forbid, none to permit
   8.2 Why mission driven exception is the failure mode
   8.3 Interaction with the other documents
   8.4 The ratchet
9. Alignment Checks
   9.1 The five evaluation points
   9.2 Inbound admission
   9.3 Outbound crossings
   9.4 Decision alignment
   9.5 Cost, and what runs on every operation
10. Tension, Precedent, and Resolution
    10.1 When two elements conflict
    10.2 Recorded precedent
    10.3 Precedent never creates permission
11. Amendment and Drift
    11.1 Amendment is the most constitutional act
    11.2 The cooling rule
    11.3 Stated cause
    11.4 Append only character history
    11.5 Measuring drift
12. Alignment Across Boundaries
    12.1 Refusals travel as a floor
    12.2 Peer alignment declarations
    12.3 Purpose is why a boundary exists at all
13. Worked Example: The Four Agreements
14. Failure Classes
15. Conformance
    15.1 Tier requirements
    15.2 Health invariants
    15.3 Self test
    15.4 Note on order of evaluation
16. Versioning and Governance
Appendix A: Refusal and Scope Predicate Grammar (proposed)

---

## 1. Introduction

### 1.1 Why the brain needs a reason

An individual has a life purpose, values, and a relationship to their own conduct. An organization has a charter, tenets, beliefs, and drivers. In both cases these are not ornaments on top of the real work. They are the criteria by which the real work is judged worth doing, and a brain built without them is a well governed instrument with no declared end.

The other documents in this stack are all mechanically excellent and entirely amoral. SPEAK will faithfully sign and transmit an utterance that should never have been said. CONFIDE will correctly catalog the inference call that sent material somewhere the owner would be ashamed of. TRACE will diligently seal the evidence of it. DEFER will route it to an authorized approver, who will approve it under a valid envelope, and the ledger will be clean. Every check passes and the outcome is wrong.

POLARIS is where the ends are declared, so that the machinery has something to be in service of.

### 1.2 Why values documents fail

Nearly every declared value in existence is unfalsifiable. "Integrity" cannot be breached in a way that anyone can point at. "Customer obsession" cannot be measured. "Do your best" has no failing condition. These statements are sincere and they are also inert, and their inertness has a predictable consequence: they get cited on both sides of every hard call, which means they decide nothing while appearing to decide everything.

The second failure is worse. A values statement that cannot be violated can still be invoked, and an invocable statement with no failing condition is a general purpose justification. This is how mission driven organizations produce their most serious breaches. The mission is real, the pressure is real, and the values document offers no resistance because it was never shaped to resist anything.

The third failure is drift. Under pressure, an organization amends its values to match its conduct, and because the amendment is usually a small softening of a phrase nobody could operationalize anyway, it costs nothing and is invisible afterward.

### 1.3 The enforceability test

Every element declared under POLARIS MUST pass one test: it must be able to produce a decidable refusal, a measurable obligation, or a recorded tie break on some concrete act.

An element that passes is normative and may be cited. An element that fails is non normative, MUST be marked as such, and MUST NOT be cited as the basis of any decision. Non normative elements are kept, deliberately, because a compressed and memorable phrase is how a value survives transmission to a new person or a new agent. What they may not do is carry weight in a record.

This single test is the whole design. It does not make a brain more ethical. It makes the brain's ethics legible, testable, and hard to quietly abandon.

### 1.4 Position in the stack

POLARIS is the root of the precedence order. It is the normative content of Layer 0, above the Charter's structural declarations, and it is the first document a brain writes and the last one it is permitted to change casually.

Root is a statement about conflict resolution, not about dependency. POLARIS imports vocabulary it does not redefine: decidability and act classes from DEFER, evidence grades from TRACE, custody classes from CONFIDE, layers and tiers from BLUEPRINT, agent state thresholds and the key holding test from RETAIN. Requiring a document's vocabulary confers no precedence on that document, and sitting at the top of the precedence order removes none of the requirement.

Precedence here means one specific thing, defined in section 8, and it is narrower than it sounds. POLARIS wins every conflict in the direction of refusing, and loses every conflict in the direction of permitting.

---

## 2. Definitions

### 2.1 The seven element kinds

POLARIS defines exactly seven element kinds: Identity, Purpose, Obligations, Loyalties, Refusals, Standards, and Mottos. This enumeration is canonical, and no other count in this document overrides it. Alignment, the A in the name, is not an element kind. It is the set of evaluation mechanisms defined in section 9.

| Kind | Normative | Function |
|---|---|---|
| Identity | No | Who the brain serves and what it is |
| Purpose | Partially | Why the brain exists. Tiebreaker of last resort and the test for amendments |
| Obligations | Yes | What the brain commits to do, with a metric |
| Loyalties | Yes | Ordered precedence of whose interest prevails |
| Refusals | Yes | What the brain will not do, decidably |
| Standards | Yes, weakly | Tie breaks between already permitted options |
| Mottos | No | Compressed recall aids, treated in section 7.3 |

### 2.2 Normative and non normative

A **normative** element may be cited in a decision record, may cause a refusal, and is subject to the amendment rules of section 11. A **non normative** element may be published, quoted, and taught, and MUST NOT appear as grounds in any decision record, gate evaluation, or refusal.

Every element MUST carry its normative status explicitly. An element with unstated status is non normative by default, because the default must be the one that cannot be abused.

### 2.3 Decidable

An element is **decidable** when a predicate over a proposed act returns refuse or permit without appeal to judgement, and the predicate is evaluable by the brain itself. Decidability is the same property DEFER requires of a scope, and for the same reason. What entity counts as the brain for evaluation at each tier is defined in section 15.1.

### 2.4 Red check

A **red check** is a failing health invariant: a condition the conformance sweep detects, reports, and keeps visible until it is cleared. A red check does not block operations. It exists so that a failure with no natural blocking point still has a recorded state the system can be in without anyone watching. DEFER uses the term in the same sense.

---

## 3. Identity and Purpose

### 3.1 The single purpose statement

A brain MUST declare exactly one purpose statement. One, not a list. A list of purposes is a set of tiebreakers that cannot break a tie with each other, which is the state a brain is in when it has no purpose statement at all.

The purpose statement is prose, and it is not directly decidable. Its normative force is narrow and specific: it is the criterion against which every amendment to any POLARIS element is tested, and it is the tiebreaker of last resort when no refusal, obligation, loyalty, or standard resolves a choice.

### 3.2 Identity

Identity declares what the brain is, whom it serves, and what it is not. It is non normative and it is not therefore useless: identity is what makes the purpose statement interpretable by a reader, human or agent, who was not present when it was written.

An organization's identity SHOULD name what it does not do and does not want to become. Negative identity is far more informative than positive identity, because almost every organization's positive identity is interchangeable with its competitors'.

### 3.3 What purpose is used for

Purpose is used for exactly three things. It tests amendments. It breaks ties nothing else breaks. It explains, to a reader who must interpret a refusal in a case its author did not anticipate, what the refusal was for.

That third use is real and load bearing. A refusal is a predicate, predicates have edges, and at the edge someone must decide whether the spirit applies. Purpose is the only thing that can inform that reading, and the reading MUST be recorded as a precedent under section 10.2 rather than made silently and repeatedly.

### 3.4 What purpose may not be used for

Purpose MUST NOT be cited to permit an act. It MUST NOT be cited to relax a refusal, widen a DEFER envelope, lower a CONFIDE custody requirement, exempt a TRACE artifact, or justify a SPEAK emission that would otherwise fail its checks.

A purpose statement invoked in favor of doing something is being used as the general purpose justification described in section 1.2. This prohibition is what makes it safe to write an ambitious purpose statement, and a brain that cannot make this prohibition hold should write a timid one instead.

---

## 4. Refusals

### 4.1 Refusals are the load bearing layer

A refusal is the only POLARIS element that is fully mechanically enforceable, and it is therefore where a brain's values actually live. Everything else in this document supports, explains, or orders refusals.

The practical consequence is that writing POLARIS is mostly the work of converting aspirations into refusals. "Be honest" is not usable. "This brain does not emit a claim it cannot substantiate at the declared evidence grade" is usable, is checkable, and is what "be honest" means when it has to run.

A brain MUST declare at least one refusal. A brain declaring none has written a poster.

### 4.2 Form of a refusal

A refusal MUST carry an identifier, a stated form in plain language, a decidable predicate over acts, the act classes and crossings at which it is evaluated, its strength as absolute or conditional, a stated cause explaining what it exists to prevent, and its adoption record. Act classes are defined by DEFER/1.0 section 4.2 and drawn from the brain's declared act class vocabulary. POLARIS does not define its own.

The plain language form and the predicate are both required and serve different readers. The predicate is what runs. The plain form is what survives, and it is what a person reads in five years when deciding whether the predicate still expresses the intent.

### 4.3 Mechanical decidability, and why a model may not evaluate one

A refusal predicate MUST be evaluable by the brain without invoking a language model.

This is the sharpest rule in the document. If a model decides whether an act violates the brain's values, then the brain's values are the model's values, filtered through a prompt, subject to the provider's own policy, and revisable without any amendment record. A brain that enforces its ethics by asking an external inference provider whether something is ethical has outsourced the one thing it cannot outsource, and it has done so to a party that CONFIDE exists to keep at arm's length.

A brain MAY use a model to draft candidate refusals, to flag acts for human review, or to summarize a tension. It MUST NOT let a model's output be the enforcement.

Where a value genuinely cannot be reduced to a predicate, the correct outcome is not a model evaluated refusal. It is either a narrower refusal that captures the mechanically detectable part, or a standard under section 7, which is honest about being advisory.

### 4.4 Absolute and conditional refusals

An **absolute** refusal admits no exception, no override, and no approval path. Not by the owner in the moment, not under urgency, not under a break glass envelope. The only way past an absolute refusal is amendment under section 11, which is slow by construction.

A **conditional** refusal names the conditions under which the act becomes permissible, and those conditions MUST themselves be decidable. A conditional refusal is not a weaker refusal, it is a more precisely scoped one.

A brain SHOULD keep its absolute set small. Absolutes that are inconvenient get amended, and a pattern of amending absolutes is worse for the brain's integrity than never having declared them, because it establishes that absolutes are negotiable.

### 4.5 The dead refusal problem

A refusal that has never fired is in one of two states. It is perfectly deterrent, and never approached. Or it is broken, misscoped, wired to nothing, and has been inert since the day it was written. From the outside these are indistinguishable, and the second is common.

A brain MUST therefore test every refusal on a declared interval by seeding an act that the refusal should block and confirming that it blocks. This is the same discipline the other documents apply to their own checks, and it is the only way a refusal earns the right to be believed. Interval testing binds at Tier 2 and above (section 15.1); the Tier 1 substitute is checkpoint evaluation as defined there.

A refusal that fails its test is a conformance failure, not a maintenance item. Between the failure and the fix, the brain has no such value.

---

## 5. Obligations

### 5.1 Form of an obligation

An obligation is a commitment to act rather than to abstain. It MUST carry an identifier, a plain statement, a metric, a measurement window, and a declared threshold below which the obligation is unmet.

An obligation without a metric is a standard, and should be declared as one.

### 5.2 Why obligations cannot fail closed

A refusal can be enforced instantaneously, because refusing is always available. An obligation cannot, because there is no moment at which the brain can be stopped from failing to have done something.

Obligations are therefore enforced by measurement over a window and reported as unmet, not by blocking. This is a real and permanent asymmetry between the two kinds, and a brain that phrases its important values as obligations has phrased them in the weaker form. Where a value can be expressed either way, express it as a refusal.

### 5.3 Metric and window

The metric MUST be computable from the brain's own records. An obligation whose satisfaction is attested by the party responsible for it is not measured, per the DEFER evidence grade rule.

An unmet obligation MUST be reported as a red check and MUST NOT block operations, unless a refusal independently forbids the act.

---

## 6. Loyalties

### 6.1 The loyalty order

When interests conflict, something has to give way, and a brain that has not declared which one gives way will decide it differently each time, under pressure, in favor of whoever is present.

A brain MUST declare an ordered list of beneficiaries. Typical entries are the owner, the owner's dependents or the organization's employees, clients, peers under agreement, the subjects of records held in the brain, and the general public. The order is the brain's, not this document's, and it MUST be total. A tie in a loyalty order is an undeclared loyalty order.

One entry is required: the order MUST include the subjects of records held in the brain, ranked explicitly. Every other entry is the brain's to choose. The reason is in section 6.3, and the requirement is what makes `PL-19` decidable.

The order is consulted only when interests genuinely conflict. It is not a ranking of importance and it does not license disregarding anyone below the top.

### 6.2 The order is not reorderable

The loyalty order MUST NOT be reordered for a particular decision, by anyone, including the owner. Reordering is an amendment under section 11.

An order that can be reordered in the moment is not an order. It is a menu, and the function of a menu at decision time is to supply the justification for whatever was going to happen. An agent MUST NOT reorder the loyalty order under any envelope, and `grant` MUST NOT include this act.

### 6.3 Publication and the uncomfortable disclosure

A brain MUST publish its loyalty order to any peer it enters an agreement with, and SHOULD publish it generally. Publication binds at Tier 3 (section 15.1).

This is uncomfortable, because it usually means telling a client they rank below the owner, and every organization's marketing implies the opposite. Publishing it anyway is the more trustworthy act, and it is also the more useful one: a peer who knows where they sit can decide what to share, and a peer who has been implicitly promised primacy will eventually discover otherwise in the worst possible circumstance.

The subjects of records held in the brain deserve particular attention here. They are frequently absent from the conversation, have no representative in the decision, and are the party most affected by a boundary failure. A loyalty order that omits them has not forgotten them, it has ranked them last without saying so.

### 6.4 Conflicts of interest

An actor with an interest in the outcome of a decision MUST have that interest recorded in the decision record, and a brain MUST declare which conflicts disqualify an actor from resolving.

Disclosure without disqualification is not a control, and disqualification without disclosure is not verifiable. Both are required.

A sole owner cannot be disqualified into a vacuum. Where the disqualifying conflict belongs to the owner and the brain has no other actor eligible to resolve, disqualification does not transfer the decision, because there is no one to transfer it to. The owner resolves, the interest MUST be recorded, the decision record MUST be marked as resolved under a sole owner conflict, and the count of such records is a reported health signal under section 15.2. This fallback applies only to the sole owner. Every other conflicted actor remains disqualified.

---

## 7. Standards and Mottos

### 7.1 Standards break ties, they do not grant permission

A standard is a declared disposition used to choose between options that are all already permitted. Standards are where most of what an organization calls its tenets belongs: prefer durability over speed, prefer the simpler mechanism, prefer the reversible option, prefer the explanation the reader can check.

A standard MUST NOT be the basis of a refusal and MUST NOT be the basis of a permission. It operates only on choice among the permitted, which is a smaller job than tenets are usually given and a job they can actually do.

A standard cited in a decision record MUST be recorded as a rationale, never as an authority.

### 7.2 Citation and the discrimination test

A brain SHOULD track how often each standard is cited. Two patterns are defects.

A standard cited in nearly every decision is discriminating nothing; it is a house style, not a tiebreaker, and it should be retired or sharpened. A standard never cited in a long window is either unknown to the actors or inapplicable, and either way it is not in use.

Both signals are computed over the reporting period of section 11.5. The default thresholds are citation in more than 90 percent of the period's decision records for the first signal, and citation in none of them for the second. A brain MAY declare different thresholds, and the declared values are what the health signal of section 15.2 reports against.

This is the standards analogue of the dead refusal problem, and it is the only way a values set stays honest about what it is actually doing rather than what it says.

### 7.3 Mottos are non normative on purpose

A motto is a compressed, memorable phrase. Mottos are valuable and a brain SHOULD have them, because compression is how a value survives being handed to a new employee, a new agent definition, or the owner at the end of a long day.

A motto MUST be marked non normative, and MUST NOT be cited as the basis of a decision, a refusal, an approval, or a gate evaluation. A motto appearing as grounds in a decision record is a defect, and it is a defect worth detecting mechanically, because it is the most natural error in the world: the memorable phrase is exactly the one that comes to mind when a justification is needed.

Every motto SHOULD name the normative element it compresses. A motto compressing nothing is a slogan, which is permitted, and which should be recognized as such.

---

## 8. The One Way Precedence Rule

### 8.1 Highest precedence to forbid, none to permit

POLARIS has the highest precedence in the stack for forbidding an act, and no precedence whatsoever for permitting one.

A POLARIS refusal blocks an act that every other document would allow. No POLARIS element permits an act that any other document forbids. There is no configuration, no owner override, and no urgency under which this reverses.

Concretely: POLARIS may add constraints to SPEAK, CONFIDE, TRACE, DEFER, and BLUEPRINT. It may never remove one, and it may never satisfy one. A purpose statement is not evidence, is not an authorization, is not a custody class, and is not an approval.

### 8.2 Why mission driven exception is the failure mode

The reason for the asymmetry is that the highest layer in any hierarchy is the most dangerous place to put a permission. Whatever sits at the top can be invoked against everything below it, and a purpose statement is the most invocable text an organization will ever write: broad, sincere, and unfalsifiable.

If purpose could permit, then every constraint in this stack would have an override phrased as service to the mission, and the override would be available exactly when the constraint mattered. Every serious mission driven failure has this shape. The mission was real. The constraint was inconvenient. The mission was senior to the constraint. Nobody lied.

The one way rule removes the move entirely, which is cheaper than trying to be the kind of organization that would decline to make it.

### 8.3 Interaction with the other documents

| Document | POLARIS may | POLARIS may not |
|---|---|---|
| BLUEPRINT | Forbid a promotion, a classification change, or a record admission | Substitute for a gate, a check, or a tier requirement |
| SPEAK | Forbid an utterance to a peer, or forbid a peer relationship entirely | Excuse a missing signature, receipt, or provenance chain |
| CONFIDE | Forbid an inference call, or forbid a custody class outright | Raise an endpoint's effective custody class, or excuse expired evidence |
| TRACE | Forbid a harness, an egress, or a sealing decision | Exempt an artifact from classification, sealing, or retention |
| DEFER | Forbid an act no matter who holds a covering envelope | Confer an envelope, widen one, or resolve a decision |
| RETAIN | Forbid the creation or promotion of an agent brain, or forbid a shared agent state store | Substitute for the key holding test, or excuse a residue classification |

The CONFIDE row deserves emphasis. A brain may refuse to send anything to a C4 Open provider, which is a POLARIS refusal doing real work. A brain may not declare that its purpose makes a C4 endpoint effectively C1. The first narrows what is permitted. The second relabels a fact.

### 8.4 The ratchet

The combined effect across all six documents is a ratchet. Constraints accumulate and are removed only by amendment with a stated cause and a recorded history. There is no fast path to a looser brain, and there are several fast paths to a tighter one.

This is the intended asymmetry, and it matches the DEFER rule that revocation and narrowing are delegable while granting and widening are not. A governance system should be easy to tighten and slow to loosen, in every document, at every layer.

---

## 9. Alignment Checks

### 9.1 The five evaluation points

POLARIS adds no new enforcement point. It binds to five that already exist.

| Point | Governing document | POLARIS evaluates |
|---|---|---|
| Record admission | BLUEPRINT Layer 8, SPEAK | Inbound refusals, loyalty implications of holding the material |
| Utterance to a peer | SPEAK | Outbound refusals, published loyalty order, peer alignment floor |
| Inference call | CONFIDE | Refusals on custody class, provider, and content |
| Harness artifact egress | TRACE | Refusals on what may leave inside tooling residue |
| Decision resolution | DEFER | Refusals as a hard precondition, standards as recorded tie break |

Reusing existing gates is deliberate. A separate values gate would be a separate thing to bypass, would run at a different time than the act, and would be the first check disabled when it got in the way.

### 9.2 Inbound admission

Refusals apply on the way in. A brain may decline to hold material, and the reasons are ordinary: material acquired in a way the brain refuses to participate in, material whose subjects did not consent, material the brain cannot classify, material that would create an obligation the brain cannot meet.

Declining admission is the cheapest possible enforcement point and the one most often skipped. Material refused at the boundary creates no retention duty, no classification burden, no sealing cost, and no exposure. Once admitted, it is the brain's problem permanently.

### 9.3 Outbound crossings

Refusals apply at every crossing, and the three crossing documents each define what a crossing is. POLARIS does not redefine them. It supplies additional predicates that a crossing must satisfy, evaluated after the governing document's own checks pass, never instead of them.

Order matters. A crossing that fails SPEAK, CONFIDE, or TRACE is refused on that basis and POLARIS is not consulted, because there is nothing to add to a refusal. A crossing that passes is then evaluated against refusals, and may still be refused.

### 9.4 Decision alignment

Every DEFER decision record MUST record which refusals were evaluated and their results, and MAY record standards cited as tie breaks with their reasoning. This recording binds at Tier 2 and above (section 15.1).

A refusal evaluation is `observed` evidence under the TRACE grades, because the brain computed it. A standard citation is a rationale and carries no grade, because it is not a claim about the world.

### 9.5 Cost, and what runs on every operation

Refusal predicates run on every crossing and every decision, so they MUST be cheap. That constraint is the practical reason for section 4.3: a predicate over the act's own metadata costs nothing, and a model evaluation costs money, latency, an inference call to catalog, and a dependency on the thing being constrained.

Standards are evaluated only where a genuine choice exists among permitted options, which is a small fraction of operations, and they are evaluated by whoever is deciding, human or agent, as recorded reasoning rather than as a gate.

---

## 10. Tension, Precedent, and Resolution

### 10.1 When two elements conflict

Two refusals can point opposite ways on a single act. An obligation can conflict with a refusal. A loyalty order can put two declared beneficiaries in genuine opposition. These are not authoring errors, they are the normal condition of any value set rich enough to be useful.

Resolution order, applied in sequence: an absolute refusal wins over everything. A conditional refusal wins over an obligation. The loyalty order resolves conflicts between beneficiaries. Standards resolve what remains. Where nothing resolves it, the purpose statement is the tiebreaker of last resort.

A tension resolved by the purpose statement MUST be resolved by the owner and MUST NOT be resolved by an agent, because it is by definition a case the declared rules do not cover. This is the same reservation DEFER makes for the constitutional class, and it is the correct amount of the owner's attention to spend: only on the cases nothing else reaches.

### 10.2 Recorded precedent

A tension resolved at the purpose level MUST be recorded as a precedent, carrying the act, the elements in tension, the resolution, and the reasoning.

Precedents are citable in later decisions. This prevents the same tension being re litigated from scratch every time, which is the failure mode of a values set with no memory: the same hard call arrives repeatedly and is decided differently depending on who is present and how tired they are.

A pattern of precedents around one element is the signal that the element should be amended to say what practice has settled on. Precedent is a queue of pending amendments, and a brain SHOULD report it as one.

### 10.3 Precedent never creates permission

A precedent records how a tension was resolved. It MUST NOT be cited to permit an act that a refusal forbids, and it MUST NOT accumulate into a de facto amendment.

Precedent is subject to the one way rule exactly as purpose is. Otherwise a values set is loosened by a sequence of individually defensible resolutions, none of which was an amendment, and no one can identify the moment the value changed. That is how drift actually happens, and it never happens by amendment.

---

## 11. Amendment and Drift

### 11.1 Amendment is the most constitutional act

Amendment of any normative POLARIS element is the highest consequence act in the brain. It is DEFER class K4, reserved to the owner, never delegable, never covered by any envelope including a break glass envelope, and never resolvable by an agent identity.

An agent MAY draft a proposed amendment, and SHOULD, since noticing that a refusal no longer fits reality is exactly the kind of observation an agent operating under it is well placed to make. An agent MUST NOT resolve one.

### 11.2 The cooling rule

A refusal MUST NOT be amended, narrowed, or removed in the same decision as the act it would have blocked, and MUST NOT be amended within a declared cooling period after such an act was refused.

This is the concrete anti rationalization control and it is the single most important rule in this section. The moment a refusal actually costs something is the moment its removal looks most reasonable, and it is the moment the reasoning is least trustworthy. Separating the amendment from the blocked act by a declared interval does not prevent the amendment. It ensures the amendment is made by someone not currently holding the invoice.

The blocked act does not become permitted retroactively when the refusal is later amended. It was refused. If it still matters, it is re proposed.

The cooling period is declared once, as `cooling_period_days` in the charter frontmatter of the brain's POLARIS declaration, and applies to every normative element. An element MAY declare a longer period for itself and MUST NOT declare a shorter one. The value MUST be a whole number of days, at least 1. Where no declaration exists the period is 30 days, because the default must be the one that cannot be abused. Declaring the period binds at Tier 1; mechanical enforcement binds at Tier 2 and above (section 15.1). An amendment inside the period is failure `PL-12` at every tier, whether or not machinery existed to block it.

### 11.3 Stated cause

Every amendment MUST record what prompted it, which act or tension exposed the problem, what the element failed to capture, and how the amendment is consistent with the purpose statement.

An amendment that cannot articulate its cause is drift with a signature on it. An amendment that cannot be reconciled with the purpose statement is a signal that the purpose statement is the thing that has changed, which is permitted and which should be done explicitly rather than by narrowing everything underneath it.

### 11.4 Append only character history

POLARIS elements are append only. A removed refusal MUST remain in the record, marked withdrawn, with its cause and date.

The consequence is that the brain retains a permanent, readable history of what it used to refuse and stopped refusing. That history is the only real record of an organization's character over time, and it is the record every organization would prefer not to keep.

### 11.5 Measuring drift

A brain MUST report, per period: refusals withdrawn or narrowed, absolute refusals downgraded to conditional, loyalty reorderings, obligations whose thresholds were lowered, and amendments made inside a cooling period. This report binds at Tier 2 and above (section 15.1).

Any nonzero count in the last category is a conformance failure. The rest are not failures; they are the numbers by which the owner can see the shape of their own drift, which is not visible from inside any single amendment, all of which felt reasonable.

---

## 12. Alignment Across Boundaries

### 12.1 Refusals travel as a floor

A refusal attached to a record MUST travel with that record across a boundary, as a floor, in the same manner as a CONFIDE custody floor. The clauses of this section, 12.1 through 12.3, bind at Tier 3 (section 15.1).

If a brain refuses to submit client material to a model, and a peer brain admits that material, the peer inherits the refusal for that material. A brain MUST enforce inherited refusal floors on admitted records and MUST report a violation to the speaking brain.

Without this, a boundary launders values. Two brains, each with a refusal, exchange records and each finds the other's material unencumbered. The refusal was attached to a brain rather than to the material, and copying the material stripped it.

### 12.2 Peer alignment declarations

A peer agreement MUST declare each party's published refusals bearing on the exchange, each party's loyalty order, and which of the other's refusals it will honor as a floor.

A brain MAY decline a peer agreement on alignment grounds alone. It MUST be able to state which refusal or loyalty conflict is the basis, because "not aligned" without a citable element is the failure mode this whole document is built to prevent, appearing at the boundary.

### 12.3 Purpose is why a boundary exists at all

Boundaries are usually justified on security grounds, and that justification is incomplete. A brain maintains a boundary because it has a purpose distinct from the purpose of what is on the other side, and it will make different choices as a result.

Two brains with identical purpose, loyalties, and refusals have no reason to maintain a boundary between them beyond operational convenience. Two brains with different loyalty orders have every reason, and the boundary is where the difference is enforced. This is why a peer agreement's alignment declaration is not a formality: it is the statement of what the wall is for.

---

## 13. Worked Example: The Four Agreements

The Four Agreements are a well known personal value set and a good test of whether this taxonomy does any work. Applied honestly, it sorts them into three different kinds and rejects one as written.

**Be impeccable with your word** becomes a refusal, and a strong one. The brain does not emit an assertion it cannot substantiate at the declared evidence grade, and does not record an attested claim as observed. This is mechanically decidable, and most of its machinery already exists: it is the SPEAK provenance requirement and the TRACE evidence grades, which means this agreement was already half implemented before it was declared. That is a good sign about both.

**Don't make assumptions** becomes a refusal. An unverified inference MUST NOT be recorded at the same grade as a verified one, and an inference MUST carry the basis it rests on. Also decidable, also largely present in the stack already.

**Don't take anything personally** is not a refusal and cannot be made into one. It is a disposition about how to weight incoming criticism, it has no decidable predicate over any act, and any attempt to write one would produce something absurd. It is a standard: where a critique and a defense are both available responses, prefer evaluating the critique on its merits. Advisory, citable as a rationale, never a gate.

**Do your best** fails the enforceability test as written. It has no failing condition, which makes it exactly the kind of unfalsifiable virtue described in section 1.2, and it is the most likely of the four to be invoked as a general justification.

It survives in one narrow, decidable form: the brain does not present work at a stage that implies review it did not perform. That is not "do your best" in full. It is the mechanically detectable part, which is the refusal to misrepresent effort, and it is the part that can be enforced. The remainder stays as a motto, marked non normative, compressing the refusal it came from.

One value set, four members, and the outcome is two refusals, one standard, one refusal recovered by restatement plus a motto. The taxonomy earns its keep by refusing to accept all four as equivalent, which is what a poster on a wall would have done.

---

## 14. Failure Classes

| Code | Failure |
|---|---|
| `PL-01` | POLARIS element cited to permit an act |
| `PL-02` | POLARIS element cited to relax or satisfy a requirement of another document |
| `PL-03` | Purpose statement cited in favor of an act rather than against one |
| `PL-04` | Motto cited as grounds in a decision record |
| `PL-05` | Element with unstated normative status treated as normative |
| `PL-06` | Refusal predicate requiring a language model to evaluate |
| `PL-07` | Refusal declared without a decidable predicate |
| `PL-08` | Absolute refusal overridden by approval, urgency, or break glass |
| `PL-09` | Refusal not exercised by its declared interval test |
| `PL-10` | Refusal test failing, with the brain continuing to assert the value |
| `PL-11` | Refusal amended in the same decision as the act it blocked |
| `PL-12` | Refusal amended inside its cooling period |
| `PL-13` | Amendment recorded without a stated cause |
| `PL-14` | Amendment recorded without the purpose consistency statement section 11.3 requires |
| `PL-15` | Normative element removed rather than marked withdrawn |
| `PL-16` | Blocked act treated as permitted after a later amendment |
| `PL-17` | Amendment resolved by an agent identity |
| `PL-18` | More than one purpose statement declared |
| `PL-19` | Loyalty order absent, tied, or missing the required record subjects entry |
| `PL-20` | Loyalty order reordered for a single decision |
| `PL-21` | Loyalty order not published to a peer under agreement |
| `PL-22` | Conflict of interest disclosed without a disqualification rule, or applied without disclosure |
| `PL-23` | Obligation declared without a metric or window |
| `PL-24` | Obligation satisfaction attested by the responsible party |
| `PL-25` | Standard used as the basis of a refusal or a permission |
| `PL-26` | Precedent cited to permit an act a refusal forbids |
| `PL-27` | Precedent accumulating into a de facto amendment |
| `PL-28` | Purpose level tension resolved by an agent |
| `PL-29` | Inherited refusal floor not enforced on an admitted record |
| `PL-30` | Refusal floor stripped by a boundary crossing |
| `PL-31` | Peer agreement without an alignment declaration |
| `PL-32` | Alignment based peer refusal with no citable element |

---

## 15. Conformance

### 15.1 Tier requirements

Body requirements bind at every tier unless a clause carries an explicit tier tag or is scoped here. The complete set of tier scoped body clauses: interval testing (4.5), crossing evaluation beyond record admission (9.1 through 9.3), decision record recording (9.4), cooling period enforcement (11.2), and drift reporting (11.5) bind at Tier 2 and above; loyalty order publication (6.3) and refusal floors, alignment declarations, and boundary alignment (section 12) bind at Tier 3. A clause binding above the brain's declared tier is not waived, it is deferred: the brain MUST NOT report it as satisfied.

**Tier 1.** A brain MUST declare exactly one purpose statement, at least one refusal with a decidable predicate, a total loyalty order carrying the required record subjects entry, and the normative status of every declared element. Refusals MUST be evaluated on record admission and MUST fail closed. Amendments MUST be owner resolved, append only, and carry a stated cause.

At Tier 1 the evaluating entity is defined as follows: a conformance tool executing the refusal predicate at the declared checkpoints, which are record admission and every conformance check run, is the brain evaluating, and satisfies the admission clause. Tier 1 demonstrates refusal by that check refusing a seeded violating admission. Continuous hook enforcement on every admission path is a Tier 2 property, exercised where BLUEPRINT's phase ladder installs enforcement.

**Tier 2.** A brain MUST additionally evaluate refusals at every crossing governed by SPEAK, CONFIDE, and TRACE, MUST record refusal evaluations in every DEFER decision record, MUST enforce the one way precedence rule mechanically, MUST declare and enforce cooling periods, MUST test every refusal on its declared interval, MUST declare metrics and windows for every obligation, and MUST report the drift measures of section 11.5.

A Tier 2 brain MUST NOT permit an agent identity to resolve an amendment, reorder the loyalty order, resolve a purpose level tension, or evaluate a refusal by inference.

**Tier 3.** A brain MUST additionally publish its refusals and loyalty order, MUST attach refusal floors to emitted records, MUST enforce inherited floors on admitted records and report violations to the speaking brain, MUST include an alignment declaration in every peer agreement, and MUST publish a self test a peer can execute before entering one.

### 15.2 Health invariants

An invariant derived from a tier scoped clause binds at that clause's tier under the scoping rule of section 15.1.

| Invariant | Target |
|---|---|
| POLARIS elements cited to permit | 0 |
| Mottos cited as grounds | 0 |
| Refusals without a decidable predicate | 0 |
| Refusals whose evaluation requires inference | 0 |
| Refusals overdue for their interval test | 0 |
| Failing refusal tests | 0 |
| Amendments inside a cooling period | 0 |
| Amendments without a stated cause | 0 |
| Amendments resolved below the owner | 0 |
| Elements with unstated normative status | 0 |
| Loyalty order ties or gaps | 0 |
| Obligations without a metric | 0 |
| Inherited refusal floors unenforced | 0 |
| Unmet obligations | reported |
| Refusals withdrawn or narrowed, per period | reported |
| Decisions resolved under a sole owner conflict | reported |
| Standards cited above the declared ceiling, or not at all, in the window (7.2) | reported |
| Precedents per element, ranked | reported as an amendment queue |

### 15.3 Self test

A conformant brain MUST provide a self test that seeds each item binding at its declared tier and below, and asserts refusal or detection. Each item is tagged with the lowest tier at which it binds; an untagged item binds at Tier 1. An item binding above the brain's tier is reported as out of tier, never as passing.

1. An act forbidden by a refusal but permitted by every other document, asserting refusal
2. A purpose statement cited to permit an act, asserting rejection
3. A purpose statement cited to satisfy a CONFIDE custody requirement, asserting rejection
4. A motto cited as grounds in a decision record, asserting rejection
5. An element declared without normative status, asserting it is treated as non normative
6. A refusal whose predicate calls an inference provider, asserting rejection at declaration
7. An absolute refusal with an approval attached, asserting the approval is void (Tier 2)
8. A break glass envelope invoked against an absolute refusal, asserting refusal (Tier 2)
9. Every declared refusal exercised against a seeded violating act, asserting each blocks
10. A refusal amendment submitted in the same decision as the act it blocked, asserting refusal
11. The same amendment submitted inside the cooling period, asserting refusal (Tier 2)
12. An amendment with no stated cause, asserting rejection
13. An amendment resolved by an agent identity, asserting rejection
14. A withdrawn refusal, asserting it remains in the record marked withdrawn
15. A previously blocked act re presented after amendment, asserting it requires a fresh decision
16. A second purpose statement, asserting rejection
17. A loyalty order with a tie, asserting rejection
18. A loyalty reorder attempted within a single decision, asserting refusal
19. A standard cited as the basis of a refusal, asserting rejection
20. A precedent cited to permit a refused act, asserting rejection
21. An admitted record carrying a peer refusal floor, asserting the floor is enforced locally (Tier 3)
22. An emitted record, asserting its refusal floor is attached (Tier 3)
23. A peer agreement with no alignment declaration, asserting refusal to enter (Tier 3)

### 15.4 Note on order of evaluation

Where a self test asserts both a POLARIS refusal and another document's check, the other document's check MUST be shown to run first, per section 9.3. A brain that refuses on POLARIS grounds an act that should have been refused on CONFIDE grounds is producing the right outcome for the wrong reason, and will produce the wrong outcome as soon as the refusal is amended.

---

## 16. Versioning and Governance

Semantic versioning applies. MAJOR when a conformant implementation of the previous version ceases to be conformant. MINOR for backward compatible additions. PATCH for clarifications.

The element kinds are closed. A brain MUST NOT add an eighth element kind, because each existing kind is defined by what it may and may not do, and a new kind would arrive without those limits, which is how a permission gets into the top of the stack.

Substantive changes proceed by RFC with a 30 day comment period. MAJOR changes require a two thirds supermajority of listed authors. While Status is Draft, this section is governed by the Draft status clause of BLUEPRINT/1.0 section 14.

---

## Appendix A: Refusal and Scope Predicate Grammar (proposed)

This appendix is proposed, not adopted. [spec_basis: proposed. No existing text defined a predicate surface form; this grammar is new and enters the Draft docket to RFCs loop of BLUEPRINT/1.0 section 14, where implementation experience under the reference tooling decides its adoption, revision, or replacement.] Nothing in it relaxes any body requirement, and a brain MAY declare predicates in another decidable form until an adopted grammar binds.

The grammar exists so that the `predicate.expression` string of the declaration schema, and the scope predicates DEFER/1.0 section 4.3 requires, have one parseable form: enough for the Phase 0 declaration check to parse a predicate at adoption time and for the Tier 1 checkpoints of section 15.1 to evaluate one at record admission and on every conformance check run.

### A.1 Design constraints

Four constraints are load bearing, and any amendment to this grammar MUST preserve them.

1. **Decidable.** Evaluation terminates on every input, in time linear in the length of the expression plus the length of the values it inspects. There is no recursion into data, no loop, and no unbounded search.
2. **No inference.** The language contains no construct that invokes a language model, so `requiresInference` is false by construction for every expression this grammar admits (section 4.3).
3. **No regex.** The only substring operation is literal prefix. Matching is a character by character scan and never backtracks.
4. **Fail closed.** An operand that cannot be resolved at the evaluating gate drives the predicate to the outcome that confers less: a refusal predicate evaluates to refuse, a scope predicate evaluates to not covered (DEFER/1.0 section 4.3).

### A.2 Productions

Twelve productions in EBNF. Terminals are quoted, `{ }` is repetition, `|` is alternation. Keywords are lowercase and reserved.

| # | Production | Definition | Example |
|---|---|---|---|
| 1 | `predicate` | `expr` | `act.class = "publish"` |
| 2 | `expr` | `term { "or" term }` | `record.sensitivity >= "confidential" or record.type = "credential"` |
| 3 | `term` | `factor { "and" factor }` | `act.class = "emit" and record.consentToRecord absent` |
| 4 | `factor` | `"not" factor \| "(" expr ")" \| test` | `not (record.stage = "capture")` |
| 5 | `test` | `comparison \| presence` | `record.authorship = "agent"` |
| 6 | `comparison` | `field op literal` | `act.meter.currency > 100` |
| 7 | `presence` | `field "present" \| field "absent"` | `record.custodyFloor present` |
| 8 | `field` | `name { "." name }` | `record.type` |
| 9 | `op` | `"=" \| "!=" \| "<" \| "<=" \| ">" \| ">=" \| "^=" \| "in"` | `act.target.path ^= "brain-root/System/"` |
| 10 | `literal` | `string \| number \| list` | `"confidential"` |
| 11 | `list` | `"[" literal { "," literal } "]"` | `record.type in ["decision", "charter"]` |
| 12 | `string`, `number`, `name` | `string` is double quoted UTF-8 with `\"` and `\\` as the only escapes; `number` is a decimal integer or fraction; `name` is `[a-z][a-zA-Z0-9_-]*` | `"C3"`, `250.00`, `sensitivity` |

`and` binds tighter than `or`, `not` binds tightest, and parentheses group. A string an implementation cannot parse under these productions is not a predicate in this grammar, and a declaration check MUST report it rather than guess.

### A.3 Evaluation context and semantics

Names resolve against a context the evaluating gate assembles. The `record` namespace binds the frontmatter of the record under evaluation (BLUEPRINT/1.0 section 5.1). The `act` namespace binds the act under classification: its act class at `act.class`, its anchor relative target path at `act.target.path`, its meter readings under `act.meter`. At the admission checkpoint of section 15.1 the `record` namespace is always bound; the `act` namespace is bound at the DEFER decision gate and the crossing gates. A name in a namespace the evaluating gate does not bind is unresolvable, and constraint A.1.4 applies.

`=`, `!=`, and `in` compare values by equality. The order operators compare numbers numerically, and compare values of a property whose declared vocabulary is ordered, such as sensitivity classes, custody classes, and consequence classes, by position in the declared vocabulary registry (BLUEPRINT/1.0 section 5.2). An order comparison over values with no declared order is unresolvable, not false. `^=` compares an anchor relative path literal against the field's value character by character, per the path anchors of BLUEPRINT/1.0 section 3.4, which DEFER/1.0 section 4.3 already requires of every scope.

### A.4 What the grammar omits, and why

There are no regular expressions, no arithmetic, no string concatenation, no user defined functions, no access to anything outside the evaluation context, and no construct that performs input or output. Each omission removes a way for evaluation to become slow, undecidable, or dependent on state the auditor cannot reproduce. A value that cannot be expressed in this grammar is handled per section 4.3: narrowed to its mechanically detectable part, or declared as a standard under section 7.
