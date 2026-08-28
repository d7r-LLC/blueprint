# DEFER: Delegated Envelopes, Fiduciary duty, Escalation, and Records

## Version 1.0

**Specification:** DEFER/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 1, TRACE/1.0 (evidence grades, protected artifact)

---

## Abstract

A brain that requires its owner to decide everything does not scale, and a brain that lets its agents decide everything is not owned. Between those two failures sits a design problem that every agent operated organization eventually hits: how much authority can be handed to an agent, on what, bounded by what, revocable by whom, and provable afterward.

DEFER governs that. It defines a role as a bounded set of authority envelopes rather than a rank, requires that every envelope trace through a signed chain of delegation grants to a human signature, classifies every act by consequence and magnitude before it executes, routes each decision to the least authorized holder whose envelope covers it, and records the outcome in the brain ledger bound to the bytes that were approved.

DEFER separates two graphs that are commonly treated as one. The reporting chain says who must be informed. The delegation chain says who may decide. They are different shapes, and conflating them produces a system in which seniority substitutes for competence and an approval can be obtained from whoever happens to be senior enough.

DEFER inverts the usual measure of success. A governance system is not working when the owner reviews a great deal. It is working when the owner reviews almost nothing and can still prove what was done on their behalf. The size and age of the owner's decision queue is therefore a conformance invariant, not an operational statistic.

The other three protocols govern crossings. SPEAK governs knowledge crossing to another brain, CONFIDE governs content crossing to a model, TRACE governs content crossing into the tooling. DEFER governs the act of deciding to cross at all.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Four requirements are absolute and admit no configuration. A delegation chain that does not terminate in a human signature MUST NOT confer authority. A redelegated envelope MUST NOT be wider than the envelope it derives from. An actor MUST NOT approve a decision it requested. A timeout MUST NOT resolve a pending decision as approved.

---

## Table of Contents

1. Introduction
   1.1 The delegation problem
   1.2 Two graphs that are not the same graph
   1.3 What the progenitor system gets right, and the two compressions
   1.4 Relationship to Blueprint layers
   1.5 Fiduciary duty
2. Definitions
   2.1 Owner, actor, role
   2.2 Authority envelope
   2.3 Delegation grant and delegation chain
   2.4 Decision request and decision record
   2.5 Meter
3. Roles and the Org Chart
   3.1 A role is not an agent and not a person
   3.2 Reports to, and why it confers nothing
   3.3 Discovery of the chart
   3.4 Vacancy and the unheld role
4. Authority Envelopes
   4.1 The four axes
   4.2 Act classes
   4.3 Scope
   4.4 Conditions
   4.5 Envelope arithmetic and the subset rule
   4.6 What an envelope may never contain
5. Meters and Magnitude
   5.1 The measurable before rule
   5.2 Required meters
   5.3 Windowed aggregates and the refund fallacy
   5.4 Declaring a meter
6. Consequence Classification
   6.1 The five consequence classes
   6.2 Boundary crossings are never low consequence
   6.3 The constitutional class
   6.4 Classification is prior to routing
   6.5 The unclassifiable act
   6.6 Standing pre-classification
7. Urgency and the Eisenhower Correction
   7.1 Why the matrix cannot be used as drawn
   7.2 Consequence routes authority, urgency routes waiting
   7.3 The dangerous quadrant
   7.4 Break glass envelopes are granted in advance
8. Delegation Grants
   8.1 Contents of a grant
   8.2 The human root invariant
   8.3 Redelegation and monotone narrowing
   8.4 Validity intervals, revocation, and history
   8.5 Suspension and the compromised actor
9. Routing and Resolution
   9.1 The least authorized holder rule
   9.2 Resolution outcomes
   9.3 Prohibited resolutions
   9.4 Quorum
   9.5 Approval binds to bytes
   9.6 Approval expiry
10. Timeout and Escalation
    10.1 The three timeout dispositions
    10.2 Escalation goes up, never around
    10.3 The terminal approver
    10.4 Fail closed without standing attention
11. RACI Binding
    11.1 Accountable holds the envelope
    11.2 Responsible performs the act
    11.3 Consulted must be evidenced, and must not become a veto
    11.4 Informed is an obligation with a deadline
    11.5 Silence, and the two things it never means
12. The Decision Ledger
    12.1 Required fields
    12.2 Two sided reconciliation
    12.3 After the fact verifiability
    12.4 Evidence grade
13. Delegation Across a Boundary
    13.1 Envelopes never cross
    13.2 Peer requests
    13.3 One human holding two owner roles
14. Failure Classes
15. Conformance
    15.1 Tier requirements
    15.2 Health invariants
    15.3 The owner load budget
    15.4 Self test
16. Versioning and Governance

---

## 1. Introduction

### 1.1 The delegation problem

The objective of an agent operated brain is to move decisions away from the owner. Every decision the owner makes is a decision the system failed to make, and the owner's attention is the scarcest resource in the design. But authority handed to an agent that later turns out to have been misused is worse than friction, because the friction was visible and the misuse was not.

The resolution is not to find the right amount of trust. It is to make authority bounded, traceable, and provable, so that a large amount of it can be handed out safely. A tightly bounded envelope granted to a hundred agents is safer than a loosely bounded one granted to three, and it removes far more friction.

### 1.2 Two graphs that are not the same graph

A brain that models delegation has two distinct relations over its roles.

The **reporting chain** is a tree. It expresses organizational structure, ownership of outcomes, and notification obligations. It answers the question of who needs to know.

The **delegation chain** is a forest of grants. It expresses who may decide what, on whose signature, within what bound. It answers the question of who may act.

These graphs have different shapes and they must be stored separately. A finance role may sit three levels down the reporting tree and hold the widest spending envelope in the brain. An engineering director may sit one level down and hold no spending envelope at all. Deriving approval authority from reporting position produces a system in which the correct approver is structurally unreachable and an incorrect one is structurally eligible.

A brain MUST store the delegation chain independently of the reporting chain. A brain MAY use the reporting chain to compute a default notification set. A brain MUST NOT use the reporting chain to compute authority.

### 1.3 What the progenitor system gets right, and the two compressions

The progenitor system, the FlowState approval machinery this document generalizes from and which predates the reference implementation, already carries risk tiers keyed to act kinds, per tier approval strategies of automatic, agent, and human, a minimum approver seniority, an approver chain walked over the reporting hierarchy, an escalation timeout, a per agent daily proposal quota, a circuit breaker on consecutive failures, a quorum mode, and a pre tool use hook that writes a compliance audit log and can block a policy violating call. That is a real approval system and most of the mechanism DEFER requires already exists there in some form.

It compresses the problem twice, and both compressions are the reason DEFER exists.

**The first compression is act kind as a proxy for consequence.** A `code_change` to a draft and a `code_change` to the constitution are the same kind and therefore route to the same approver. A `deploy` of a documentation site and a `deploy` of the inference broker are the same kind. Kind describes the verb and says nothing about what the verb is aimed at, so every decision gets mapped to the nearest available tier and the differences that matter disappear at exactly the moment they matter.

**The second compression is seniority level as a proxy for authority.** A single scalar, lower being more senior, is compared against a per tier minimum. This makes authority a total order over roles, which means every sufficiently senior role is eligible to approve everything. Authority is not a total order. It is a set of overlapping bounded regions, and the correct approver for a production deploy is not the most senior available role, it is the role whose envelope covers production deploys.

Two smaller defects follow from these. An unrecognized act kind falls back to the medium risk tier, which is agent approvable, so an act the system has never seen is authorized by an agent rather than refused. And there is no magnitude bound anywhere, so the single most useful delegation control in practice, a numeric ceiling under which an agent simply acts, cannot be expressed at all.

### 1.4 Relationship to Blueprint layers

DEFER is the normative body of Layer 7, Agency. It also constrains Layer 1, since role and envelope definitions are constitutional text, Layer 4, since a stage gate is a decision, and Layer 6, since every decision produces a ledger entry.

Layer 1 holds the role definitions, the envelope definitions, and the owner load budget. Layer 4 gate approvals are decision requests and follow this document. Layer 6 carries the decision log family. Layer 8 boundary crossings are consequence classified by section 6.2. Layer 9 carries the reconciliation check and the health invariants.

CONFIDE inference authorizations and TRACE directive artifacts are both envelope bearing instruments and MUST resolve to a role, not to a bare agent name. A charter naming an agent that holds no role holds no authority.

### 1.5 Fiduciary duty

The fiduciary duty of the title is a stance, not a separate mechanism. Every envelope holder decides on the owner's behalf, with the owner's authority, over the owner's assets, which is the classical fiduciary position, and the controls of this document are the mechanical form of the classical duties. The duty of loyalty is sections 4.6 and 9.3: a holder may not decide in its own favor or widen its own authority. The duty of care is section 6: a holder may not act without the consequence class of the act being known. The duty of candor is sections 6.4 and 12: divergences are recorded, readings are computed rather than accepted, and the ledger is written for a reader who trusts nothing. A holder that satisfies this document is discharging the duty; the word adds no obligation beyond the sections it names.

---

## 2. Definitions

### 2.1 Owner, actor, role

The **owner** is the single human or legal entity that holds terminal authority over the brain. There is exactly one owner identity, declared in the Charter. The owner may be exercised by more than one human signature where the Charter declares a signing rule.

An **actor** is any identity that can propose or perform an act: a human, an agent identity, or an automated process. Actors are the subjects of the ledger.

A **role** is a named position that holds authority envelopes. Roles are held by actors. An actor with no role may propose and may perform, but may not decide.

### 2.2 Authority envelope

An **authority envelope** is a bounded region of decision space, defined by an act class, a scope, a magnitude bound over declared meters, and a set of conditions. An envelope is the only instrument that confers the right to decide.

### 2.3 Delegation grant and delegation chain

A **delegation grant** is a signed instrument in which a granting party confers an envelope on a receiving role or actor, for a validity interval, revocably.

A **delegation chain** is the ordered sequence of grants from an envelope in use back to a human signature. A chain that does not reach a human signature is void, and every envelope on a void chain is void.

### 2.4 Decision request and decision record

A **decision request** is the proposal of an act that requires a decision, carrying the act, its digest, its classification, and its meter readings.

A **decision record** is the append only ledger entry describing how a request was resolved, by whom, under which envelope, on which chain, and what was subsequently executed.

### 2.5 Meter

A **meter** is a named, declared, pre computable quantity used to bound magnitude. Currency is one meter. It is rarely the most important one.

---

## 3. Roles and the Org Chart

### 3.1 A role is not an agent and not a person

A role is defined independently of who or what holds it. This separation is what makes the system auditable across turnover of both humans and agent definitions. Replacing an agent definition MUST NOT alter the envelopes of the role it holds, and altering a role's envelopes MUST NOT be possible by editing an agent definition.

An agent definition that declares its own authority is not a delegation. It is a claim. Authority arrives only by grant.

### 3.2 Reports to, and why it confers nothing

A role MAY declare a `reports_to` role. This relation establishes notification obligations and organizational outcome ownership. It confers no authority, creates no approval eligibility, and is not walked during routing.

A brain MUST NOT resolve an approver by ascending `reports_to`.

### 3.3 Discovery of the chart

The org chart is derived from the set of role definitions and their `reports_to` declarations. It is not separately maintained. A brain MUST NOT keep a hand maintained chart file as the authority for structure, because a second copy of a structure is a second version of it.

A rendered chart is a generated artifact. It MAY be committed for human reading. It MUST be regenerable and MUST carry the digest of the role set it was rendered from.

### 3.4 Vacancy and the unheld role

A role held by no actor is **vacant**. A vacant role's envelopes are unexercisable. Decisions routed to a vacant role MUST NOT fall through to another role, and MUST NOT fall through to the `reports_to` role. They follow the timeout disposition of their class.

Vacancy is a governance defect and MUST be reported. A brain whose critical envelopes sit in vacant roles has an org chart that describes an organization it does not have.

---

## 4. Authority Envelopes

### 4.1 The four axes

An envelope is defined by exactly four axes. All four MUST be present. An omitted axis is not an unbounded axis; an envelope with a missing axis is malformed and confers nothing.

| Axis | Question | Unbounded permitted |
|---|---|---|
| Act class | Which verbs | No |
| Scope | Over what | No |
| Magnitude | How much, on which meters | Only for the owner |
| Conditions | What must already be true | Yes, the empty set is valid |

### 4.2 Act classes

An envelope names one or more act classes. A brain MUST declare its act class vocabulary in the Constitution. The following classes are required and reserved.

| Act class | Meaning |
|---|---|
| `propose` | Produce a proposal that decides nothing |
| `apply-mechanical` | Change form without changing meaning |
| `apply-substantive` | Change meaning, argument, or conclusion |
| `promote` | Advance a work across a stage gate |
| `classify` | Set or change a sensitivity or visibility value |
| `emit` | Send across a boundary to a peer, a model, or a vendor |
| `admit` | Accept material from outside the brain |
| `spend` | Commit money or a metered external resource |
| `seal` | Commit an artifact to the append only store |
| `destroy` | Delete, purge, or render unrecoverable |
| `grant` | Create, widen, or revoke a delegation grant |
| `amend` | Change the Constitution, the Charter, or a role definition |

The four levels of the progenitor system's change authority table map onto these directly. Mechanical is `apply-mechanical`. Structural and substantive are `apply-substantive` distinguished by scope and magnitude. Factual is `apply-substantive` with a verification condition.

### 4.3 Scope

Scope names what the act may be aimed at, expressed over path anchors, domains, record classes, and stage ranges. Scope MUST be expressible as a decidable predicate over the act's target. A scope that requires judgement to evaluate is not a scope.

Scope MUST use the path anchors of Blueprint section 3.4. An envelope containing a machine absolute path is not portable and MUST be rejected.

### 4.4 Conditions

A condition is a precedent that must hold at decision time. Conditions are how a wide envelope is made safe without narrowing it. Common conditions include a passing verification check, a green publication check, a completed consultation, an elapsed cool down since a related act, a required quorum, and a required evidence grade.

A condition MUST be evaluable by the brain, not asserted by the requesting actor. A condition whose satisfaction is reported by the party that benefits from it is not a control.

### 4.5 Envelope arithmetic and the subset rule

Envelope A **covers** envelope B when A's act classes are a superset of B's, A's scope predicate is satisfied wherever B's is, A's magnitude bound is greater than or equal to B's on every shared meter and B declares no meter A omits, and A's conditions are a subset of B's.

A brain MUST be able to compute coverage mechanically. Coverage is the basis of both routing and the redelegation subset rule, and a system that cannot compute it cannot enforce either.

### 4.6 What an envelope may never contain

No envelope other than the owner's may contain:

- `amend` over the Constitution, the Charter, or the role and envelope definitions
- `grant` with an unbounded magnitude on the authority delta meter
- `destroy` over a protected artifact as defined in TRACE section 9.1
- any act whose authority delta meter reading is nonzero, meaning any act that widens who may decide

These are the constitutional reservations. They are the concrete form of the owner's final ownership, and they are the shortest list that achieves it. Reserving more than this pulls the owner back into the operating loop, which is the failure the system exists to prevent.

---

## 5. Meters and Magnitude

### 5.1 The measurable before rule

A meter MUST be computable from the proposed act before the act executes. A bound expressed on a quantity that can only be measured afterward is not a bound, it is a report.

This rule eliminates most tempting meters. "Customer impact" and "risk" are not meters. "Number of records whose visibility decreases" is a meter.

### 5.2 Required meters

A brain MUST declare and compute at least the following.

| Meter | Unit | Notes |
|---|---|---|
| `currency` | declared currency, minor units | Zero for most acts. The Ferriss meter |
| `records-affected` | count | Counts targets, not bytes |
| `reversibility` | enum | `complete`, `costly`, `none` |
| `exposure-delta` | count | Records whose sensitivity or visibility loosens. One way |
| `authority-delta` | count | Roles or envelopes whose authority widens. Widenings only. Nonzero reserves to the owner |
| `external-recipients` | count | Distinct boundary endpoints reached |

A brain MAY declare additional meters. `exposure-delta` and `authority-delta` are the two that carry the most weight in practice, because they are the two whose effects cannot be undone by reversing the act. Restoring a sensitivity label does not unpublish, and revoking a grant does not un decide what was decided under it.

`authority-delta` counts widenings only. A grant creation, an envelope widening, and a redelegation permission each read nonzero; a revocation, a narrowing, and a suspension read zero. This is why section 6.3 can hold narrowing and revocation at K2 and delegable while section 4.6 reserves every nonzero reading to the owner. The safe direction moves freely; the unsafe direction queues behind the owner.

### 5.3 Windowed aggregates and the refund fallacy

An envelope bounded only per act is not bounded. An agent authorized to approve refunds up to one hundred is authorized to disburse an unlimited amount in units of one hundred. This is the most common real world failure of threshold based delegation and it is invisible in the policy text, because the policy text is correct about each individual act.

Every magnitude bound MUST therefore carry both a per act ceiling and at least one windowed aggregate ceiling, expressed per meter over a declared window. A brain MUST refuse an act whose execution would exceed either.

An aggregate is computed over the delegation chain, not over the actor. Ten agents each holding a redelegation of the same grant share that grant's aggregate. Otherwise the aggregate is escaped by provisioning more agents, which an agent org can do trivially and which the progenitor system's per agent daily quota does not prevent.

### 5.4 Declaring a meter

A meter declaration names the meter, its unit, the computation that produces a reading from a proposed act, and whether it is monotone. A meter is monotone when its readings can only accumulate, which is what makes windowed aggregation meaningful. `currency`, `exposure-delta`, and `records-affected` are monotone. `reversibility` is not, and is used as a floor rather than a sum.

---

## 6. Consequence Classification

### 6.1 The five consequence classes

Every act MUST be assigned exactly one consequence class before routing. Consequence, not act kind, determines which envelope is required.

| Class | Name | Definition |
|---|---|---|
| K0 | Reversible local | Undo exists inside the brain, is complete, and costs no more than the act |
| K1 | Reversible costly | Undo exists and is complete, but costs materially more than the act |
| K2 | Irreversible internal | No complete undo. Effects confined to the brain |
| K3 | Irreversible external | Something left the brain, or an external commitment was made |
| K4 | Constitutional | The act changes who may decide, or what the rules are |

Class is assigned by the worst true statement, never by the typical case. An act that is usually K0 and is K2 for one target is K2 for that target.

### 6.2 Boundary crossings are never low consequence

Any act that crosses a boundary governed by SPEAK, CONFIDE, or TRACE is at minimum K3. There is no configuration under which an utterance to a peer, a call to an inference provider, or a transmission of a session artifact to a vendor is K0 or K1.

This is the unification point of the four protocol stack. The three boundary protocols each define what a crossing is and what it requires. DEFER states that deciding to cross is never a low consequence decision, which means every crossing has a named accountable role and a ledger entry naming it.

A K3 act MUST NOT be automatically resolved on the basis of magnitude alone. It MAY be automatically resolved under an envelope that explicitly names the boundary in scope and carries a windowed aggregate on `external-recipients`. Routine crossings are expected and should be delegated. Undeclared ones must be impossible.

### 6.3 The constitutional class

K4 is reserved to the owner without exception. K4 covers amendment of the Constitution or Charter, creation or widening of any grant, widening of a role's envelope set, change to the owner load budget, change to the act class vocabulary or meter declarations, and change to the timeout disposition of any class.

Narrowing and revocation are the asymmetry. Revoking a grant, narrowing an envelope, and suspending an actor are K2 rather than K4, and MAY be delegated. A governance system must be easier to tighten than to loosen, or its safe direction is the slow one.

### 6.4 Classification is prior to routing

A brain MUST classify before it routes, and MUST record the classification and every meter reading in the decision record. A classification produced after resolution is a rationalization.

The classifier is part of the brain, not part of the agent harness and not part of the proposing actor. Part of the brain is a statement about rule source, not about process boundary. A classifier MAY execute in tooling the brain invokes, including a command line tool, provided the classification rules it applies are brain records, its version is the one the decision record names, and the proposing actor cannot substitute its rules or its readings. Tooling that carries its own classification rules is part of the harness for this purpose, and its classifications are attested, not observed. An actor MAY suggest a classification. The brain MUST compute its own and MUST use its own where they differ, and MUST record the divergence. A pattern of an actor understating classification is a signal worth having.

### 6.5 The unclassifiable act

An act the brain cannot classify MUST NOT execute and MUST NOT be routed to a default class.

The progenitor system's fallback to the medium risk tier is a silent widening: an act nobody anticipated becomes an act an agent may authorize. The correct disposition of an unrecognized act is refusal plus a classification gap record. The gap is then closed by the owner as a K4 amendment to the vocabulary, which is exactly the right cost, because extending the set of things the system will do is a constitutional act.

A nonzero unclassified act rate is a health invariant failure, not a runtime condition to be handled.

### 6.6 Standing pre-classification

An owner MAY adopt a standing decision record that pre-classifies a named family of routine acts at K0 or K1. The record names the family by act class and scope, using the decidable predicates of section 4.3, and states the class assigned. An act inside the family needs no per act decision record; the standing record is its classification and its recording, and the reconciliation of section 12.2 treats the family's acts as covered by it.

The mechanism fails closed. A standing record MUST NOT assign a class above K1, MUST NOT cover an act class reserved by section 4.6, and MUST NOT cover a boundary crossing, which section 6.2 holds at K3 minimum. An act whose worst true statement exceeds the assigned class is outside the family regardless of how the family is drawn, and is classified individually under section 6.1. An act inside no standing family follows section 6.4 unchanged.

Adopting, widening, or reclassifying a standing record is K4, because it changes what the system will do without asking. Narrowing or revoking one is K2, per the asymmetry of section 6.3. The reference implementation ships one standing record as Phase 1 constitution content, covering owner performed capture, placement, and editing within its declared authoring surfaces.

---

## 7. Urgency and the Eisenhower Correction

### 7.1 Why the matrix cannot be used as drawn

The Eisenhower matrix sorts tasks on importance and urgency into do, schedule, delegate, and delete. It is a sound instrument for one person's time and an unsound one for delegated authority, because its highest cell prescribes do it yourself for important and urgent work.

Applied to an agent organization that reads as: the more consequential and the more pressing, the more the owner must personally handle. That is the friction curve the system exists to flatten, and it concentrates the owner's involvement precisely in the moments with the least time to think.

The matrix also uses one word, importance, for two different things: how much the outcome matters, and how bad it is if the decision is wrong. Delegation only cares about the second.

### 7.2 Consequence routes authority, urgency routes waiting

The two axes are kept, and each is given exactly one job.

**Consequence determines who may decide.** It selects the required envelope. Nothing else may.

**Urgency determines what happens while the decision is pending.** It selects the timeout window, the timeout disposition, and the notification channel. Nothing else.

| | Low urgency | High urgency |
|---|---|---|
| **Low consequence** | Agent decides, batched | Agent decides, immediately |
| **High consequence** | Escalate, long window, lapse on timeout | Escalate, short window, pre declared safe default |

The two low consequence cells are where nearly all volume lives, and both are fully delegated. This is where the friction is actually removed. The instinct behind a refund ceiling is correct and this is its general form: high volume, low consequence, bounded magnitude, no approval, full logging.

### 7.3 The dangerous quadrant

High consequence and high urgency is where governance systems fail, and they fail in a specific way. Urgency creates pressure to widen authority at exactly the moment consequence says to narrow it. The widening is always locally reasonable and is always granted under time pressure by whoever is reachable.

Therefore: **urgency MUST NOT widen an envelope.** Urgency MUST NOT lower a required approver's authority, MUST NOT substitute an available approver for an authorized one, and MUST NOT convert a human required decision into an agent resolvable one.

A brain that permits urgency to raise authority has an escalation path that any actor can open by asserting urgency, and an actor that discovers this has discovered how to authorize itself. Urgency is an input supplied by the proposer, which is precisely why it must never touch the authority calculation.

### 7.4 Break glass envelopes are granted in advance

The dangerous quadrant is handled by pre authorization rather than in the moment widening. A **break glass envelope** is a narrow standing envelope, granted in calm conditions, that covers a specific urgent act with a tight magnitude bound and a reversibility floor.

A break glass envelope MUST be narrow in scope, MUST bound magnitude on every declared meter, SHOULD require `reversibility: complete` or a declared safe direction, MUST notify the owner on use through a channel declared for the purpose, MUST self suspend after use pending owner review, and MUST NOT include `grant`, `amend`, or `destroy`.

Rolling back a deployment, quarantining a record, revoking a credential, and halting a sweep are the natural contents. All four are safe direction acts. The pattern generalizes: what can be pre authorized for urgent use is the act that reduces exposure, never the act that increases it.

Break glass use count is a health metric. Frequent use means an envelope is drawn too narrowly for normal operations and should be widened deliberately, in calm conditions, as a K4 amendment.

---

## 8. Delegation Grants

### 8.1 Contents of a grant

A grant MUST carry the granting party, the identity of the granting brain expressed as its brain identifier or Charter digest, the receiving role or actor, the envelope, a validity interval, a redelegation permission, a revocation authority, and a signature over the whole. A grant MUST reference its parent grant unless it is rooted directly in the owner. The brain identifier is what makes section 13.3 mechanically checkable: one human rooting two brains produces chains distinguishable only by the brain each grant names, and chain verification MUST reject a chain containing a grant whose brain identifier is not the deciding brain's.

A grant is a record in the brain and follows the record contract. Grants are append only. A grant is never edited; it is superseded or revoked.

### 8.2 The human root invariant

Every delegation chain MUST terminate in a signature by a human identity. An envelope whose chain reaches only agent signatures confers nothing, regardless of how many links it has.

This is the load bearing invariant of the document. Without it, an agent org can bootstrap arbitrary authority by having agents grant it to each other, and every individual grant will look correctly formed. Chain verification MUST walk to a human root on every use, and MUST be a cheap operation, because it happens on every decision.

### 8.3 Redelegation and monotone narrowing

A grant MAY permit redelegation. A redelegated envelope MUST be a strict subset of the granting envelope, narrower on at least one axis and wider on none.

Strict narrowing is what guarantees termination. Each redelegation loses ground, so a chain cannot cycle and cannot regain authority downstream. Permitting an equal width redelegation would allow an arbitrarily long chain of identical authority, which makes the chain uninformative and makes revocation at any point survivable by re rooting.

A redelegation MUST NOT extend beyond its parent's validity interval, and MUST become void when its parent is revoked. Revocation is transitive and immediate down the chain.

### 8.4 Validity intervals, revocation, and history

Every grant carries a validity interval. An open ended grant is permitted only for the owner's own envelopes.

Revocation ends a grant's validity going forward. It MUST NOT invalidate decisions made while the grant was valid, and it MUST NOT alter the grant record.

A revocation is itself a grant family record, append only, signed by the revocation authority the grant names. It MUST carry the digest of the grant it revokes and the time of revocation, and it MUST be discoverable by the same enumeration that resolves the grant, so a chain walker cannot find a grant without finding its revocations. A walker that cannot enumerate revocations for a grant MUST treat the chain as unverifiable, and an unverifiable chain confers nothing.

This requires that a decision record pin the digest of every grant on the chain it relied on, so the chain can be re verified as it stood at decision time. Without pinning, revoking a grant silently rewrites the audit history of every decision made under it, which converts revocation from a security operation into a records tampering operation.

### 8.5 Suspension and the compromised actor

Suspension of an actor immediately renders its held envelopes unexercisable without revoking any grant. Suspension is K2 and SHOULD be delegable, because the ability to stop a misbehaving actor must not queue behind the owner.

Suspension MUST NOT reassign the suspended actor's pending decisions to another holder. Those decisions follow the vacancy rule of section 3.4, because a suspended holder is a vacancy and rerouting around a vacancy is rerouting around authority.

---

## 9. Routing and Resolution

### 9.1 The least authorized holder rule

A decision MUST be routed to the least authorized role whose envelope covers the classified act. Where several minimal holders exist the brain selects among them by a declared rule and records the selection.

Least authorized, not most senior. This is the operational inversion that makes delegation work. Routing upward by default fills the owner's queue with decisions that three roles below were authorized to make, and the queue is the thing being optimized.

Least authorized is the coverage order of section 4.5. Role A is less authorized than role B when the union of B's envelopes covers the union of A's and the converse does not hold. Coverage is a partial order, so a least holder need not be unique; the routing target set is the minimal elements of the order among holders whose envelope covers the act, and the declared selection rule chooses within that set. A router that reduces authority to a single scalar for comparison has reintroduced the second compression of section 1.3.

If no envelope covers the act, the decision routes to the owner and a coverage gap is recorded. Persistent coverage gaps at the owner are the primary signal for where to grant next, and a brain SHOULD report them as a ranked list rather than making the owner notice a pattern in their own queue.

### 9.2 Resolution outcomes

A decision request resolves to exactly one of: `approved`, `denied`, `lapsed`, `withdrawn`, or `superseded`. Execution is a separate subsequent event and MUST be recorded separately.

`superseded` records that a newer decision request replaced this one before resolution. The record MUST name the superseding request by digest. Supersession is neither approval nor denial and carries no authority forward; the superseding request enters at `proposed` and is classified and routed on its own. `withdrawn` differs in that nothing replaces the request.

The state progression is `proposed`, `classified`, `routed`, then either `resolved` directly where an envelope covers the act without review, or `pending` then `resolved`. Every transition is a ledger event.

### 9.3 Prohibited resolutions

An actor MUST NOT approve a decision it requested, including through an intermediary it controls.

An actor MUST NOT approve a decision whose `authority-delta` reading is nonzero and which affects its own envelopes or any grant on its own chain. Self widening is not a matter of degree.

An agent identity MUST NOT resolve a K4 decision, MUST NOT resolve a decision under a chain that does not reach a human root, and MUST NOT resolve a decision by asserting a condition it is also responsible for satisfying.

Blueprint's rule that agents draft and the owner decides is preserved here in its precise form. Agents may resolve decisions the owner has already decided in advance, by grant. They may never resolve one the owner has not.

### 9.4 Quorum

An envelope MAY require a quorum of holders. A quorum is expressed as a count and a qualifying predicate over roles, and every member MUST independently hold a covering envelope. A quorum assembled from roles that individually lack the envelope does not sum to the authority, because authority is not additive.

Quorum members MUST resolve independently, without visibility of each other's resolution before their own, and the decision record MUST carry each resolution separately. A quorum recorded as a single aggregate outcome is a single approval with extra names on it.

### 9.5 Approval binds to bytes

An approval binds to the digest of the act as proposed. Any change to the act voids the approval and requires a new decision request. This is Blueprint principle 3 applied to delegation, and it closes the gap where a small clarifying edit after approval carries the approval with it.

The progenitor system binds approvals to a step identifier rather than to content, which permits exactly this drift. Identifiers are stable across content change, which is the property you do not want here.

### 9.6 Approval expiry

An approval MUST carry an execution window. An approval not executed inside its window expires and MUST NOT be executed.

An approval is a judgement about a world state. A three week old approval to emit a record is not an approval to emit it today, because the conditions that were evaluated at approval time have not been evaluated since. The window is declared per consequence class, and SHOULD be short for K3 and K4.

---

## 10. Timeout and Escalation

### 10.1 The three timeout dispositions

Every consequence class MUST declare a timeout window and exactly one disposition. There are exactly three, and no brain may define a fourth.

| Disposition | Behavior | Use |
|---|---|---|
| `lapse` | The request resolves denied. The proposer may re propose | Default. Correct for nearly everything |
| `default-safe` | A pre declared alternative act executes, itself covered by an envelope | Only where a safe direction exists |
| `hold-open` | The request stays pending and a health check goes red | Where neither denial nor a safe default is acceptable |

`lapse` is the default because its cost is latency and its failure mode is visible. `default-safe` requires that the safe act be named in advance and independently authorized, since a timeout must not be able to execute an act nobody granted. `hold-open` is the honest option for the rare decision where doing nothing is also a decision, and it converts an unattended decision into a red check rather than into an outcome.

A timeout MUST NOT resolve a request as approved, under any disposition, at any consequence class, for any urgency.

### 10.2 Escalation goes up, never around

On timeout a brain MAY escalate to a role whose envelope strictly covers the current holder's. It MUST NOT escalate to a role whose envelope does not cover the act, and MUST NOT reassign to a laterally positioned or less authorized role because the authorized holder is unavailable.

Reassigning around an unavailable approver is the most common real failure of automated escalation, because it is indistinguishable from availability management and it silently relocates authority to whoever is awake. Unavailability of the authorized holder is a vacancy, and section 3.4 governs.

Escalation MUST terminate. Since each escalation step strictly widens, and the owner is the widest envelope, the chain reaches the owner in finitely many steps.

### 10.3 The terminal approver

The owner is terminal. A decision escalated to the owner does not escalate further and MUST NOT time out into approval. It follows its declared disposition, which for K4 is `lapse` or `hold-open` only.

`default-safe` MUST NOT be declared for K4, because a constitutional change with an automatic fallback has an automatic constitutional change in it.

### 10.4 Fail closed without standing attention

Blueprint principle 8 forbids any mechanism that depends on standing human attention, and this document forbids timeouts that resolve as approved. Both hold simultaneously, and the three dispositions are how.

Nothing waits for the owner indefinitely and silently. Every pending decision has a window, and at the end of that window it becomes a denial, a safe act, or a red check. All three are states the system can be in without anyone watching, and none of them is an unauthorized act.

---

## 11. RACI Binding

### 11.1 Accountable holds the envelope

Exactly one role is Accountable for a decision, and that role is the envelope holder. Accountability is not a sentiment; it is the possession of the instrument that made the decision possible.

A RACI matrix that assigns Accountable to a role holding no covering envelope is describing an organization that cannot make the decision it claims to own.

### 11.2 Responsible performs the act

Responsible performs the act. Responsible may hold no decision authority at all, and in an agent brain usually does not. Most agents are permanently Responsible and never Accountable, which is the correct shape.

Responsible and Accountable MAY be the same actor only where the envelope explicitly permits self execution. Separating them is the cheapest control available for K2 and above and SHOULD be the default there.

### 11.3 Consulted must be evidenced, and must not become a veto

A Consulted party is a required input. Consultation MUST be evidenced in the decision record by the consulted party's response, or by an explicit record of non response. A decision record asserting that consultation occurred without carrying its result documents an intention, not a control.

Consultation MUST carry a response window, and a party that does not respond inside it is recorded as non responsive while the decision proceeds. Without this, Consulted quietly becomes a veto held by someone with no envelope, exercisable by inaction, invisible in the policy, and untraceable in the record. This is the most common way an approval workflow stalls without anyone having denied anything.

### 11.4 Informed is an obligation with a deadline

Informed parties MUST be notified within a declared window. Notification is the one obligation that may be satisfied asynchronously, after execution.

The reporting chain of section 3.2 is the natural default source of the Informed set, which is the one legitimate use of that graph.

### 11.5 Silence, and the two things it never means

Two rules that look contradictory and are not.

Silence never grants. An absent response from an Accountable party is not an approval, at any consequence class, after any interval. This is absolute.

Silence may fail to block. An absent response from a Consulted party is recorded as absent and does not halt the decision.

The distinction is that A holds an envelope and C does not. Only an envelope holder can decide, so only their affirmative act can constitute a decision. Anyone can be asked, and no one who was merely asked can decide by declining to answer.

---

## 12. The Decision Ledger

### 12.1 Required fields

Each decision record is a Layer 6 ledger entry in the decision family, hash chained and signed. It MUST carry:

- the request identifier and the digest of the act as proposed
- the consequence class, every meter reading, and the classifier version
- the divergence, if any, between proposed and computed classification
- where an envelope was invoked, the envelope and the ordered digests of every grant on its chain, including the human root
- the resolving actor and role, and each member's resolution where a quorum applied
- the RACI assignment, with consultation results or recorded non responses
- the urgency input, the timeout window, and the disposition declared
- the outcome, and the execution event with its digest, or the documented reason for non execution
- the evidence grade of every claim in the record

A decision the owner resolves directly, under no delegated envelope, is an **owner direct** record. Its resolving actor is the owner, its envelope and grant chain fields are absent rather than empty, and the human root is inherent: the owner's signature on the record is the human signature the chain requirement exists to reach. A Tier 1 brain that has issued no grant writes owner direct records exclusively, and this is the expected shape of its entire decision family. An owner direct record MUST NOT carry a fabricated self grant from the owner to the owner to satisfy the envelope fields, because a grant conferring authority its grantor already holds records nothing and manufactures a chain where none exists. A record that omits the envelope fields and is not resolved by the owner's human signature is not owner direct; it is DF-02.

### 12.2 Two sided reconciliation

Reconciliation runs in both directions and both directions are required.

Every executed act MUST have a decision record. An act without one is unauthorized action, and it is the failure the whole document exists to detect.

Every approved decision MUST have either an execution event or a documented non execution. An approval with neither is a lost execution, and a system that only checks the first direction cannot tell the difference between a decision that was declined in practice and one that was silently dropped.

The reconciliation check MUST fail closed. This mirrors the TRACE anchor reconciliation, and where an act is also a harness session or an inference call, the decision record, the session anchor, and the call ledger entry MUST cross reference and MUST agree. Disagreement among three independently maintained records is a stronger signal than any one of them.

### 12.3 After the fact verifiability

An auditor MUST be able to take any decision record and verify, without trusting current state, that the invoked envelope covered the classified act, that every grant on the chain was valid at decision time, that the chain reached a human root, that the resolver held the envelope, that no prohibited resolution occurred, and that the executed bytes match the approved digest.

Grant digest pinning of section 8.4 is what makes this hold under later revocation. Verification against current grant state answers a different and much weaker question.

### 12.4 Evidence grade

Claims in a decision record carry the TRACE evidence grades. A claim the brain computed is `observed`. A claim reported by an actor or a harness is `attested`.

An attested claim MUST NOT be the sole evidence for a conformance assertion. A meter reading attested by the actor whose envelope it bounds is not a control, which is why the brain computes its own classification and its own readings in section 6.4.

One carve-out exists at Tier 1. A claim entered by the owner over the owner's own signature is owner attested, and owner attestation MAY stand as sole evidence at Tier 1, because the owner is the terminal authority the evidence chain exists to reach and there is no more authoritative source to check the claim against. The carve-out is exactly that wide. It never extends to an agent or harness attestation at any tier, and at Tier 2 and above the brain computes its own readings and an owner attested claim becomes corroboration, not sole evidence.

---

## 13. Delegation Across a Boundary

### 13.1 Envelopes never cross

An envelope is valid only inside the brain that granted it. A role in a peer brain MUST NOT hold an envelope in this brain. A delegation chain MUST NOT contain a grant signed by a peer brain's role.

This follows from Blueprint principle 10. A boundary is a wall, not a filter, and authority does not survive a copy. Two brains that appear to share an approver actually have two roles with the same name and no relationship between them.

### 13.2 Peer requests

A peer MAY request a decision. The request is an utterance under SPEAK and is admitted as material, not as authority. Once admitted it becomes an ordinary decision request in this brain, classified by this brain, routed to this brain's roles, at minimum K3 because it originated across a boundary.

A peer agreement MAY declare which act classes a peer is permitted to request, which is a filter on the inbound queue and not a grant.

### 13.3 One human holding two owner roles

A single human frequently owns more than one brain. That human holds the owner role in each, separately, and the two roles have no relationship.

An act in one brain MUST NOT be authorized by a grant in the other, and a decision record in one MUST NOT cite a grant chain rooted in the other. When the same human approves in both, that is two decisions and two records.

This is deliberately inconvenient, and the inconvenience is the point. The moment one brain's authority can satisfy another's, the boundary between them is decorative and the separation the owner set up to protect each brain's record has been dissolved by the owner's own convenience.

---

## 14. Failure Classes

| Code | Failure |
|---|---|
| `DF-01` | Envelope invoked does not cover the classified act |
| `DF-02` | Delegation chain does not terminate in a human signature |
| `DF-03` | Redelegated envelope is not a strict subset of its parent |
| `DF-04` | Grant expired, revoked, or suspended at decision time |
| `DF-05` | Requester and resolver are the same actor |
| `DF-06` | Resolver widened its own envelope or a grant on its own chain |
| `DF-07` | Timeout resolved a request as approved |
| `DF-08` | Escalation reassigned to a role not covering the act |
| `DF-09` | Approver resolved by reporting position rather than by envelope |
| `DF-10` | Act executed with no decision record |
| `DF-11` | Approved decision with neither execution nor documented non execution |
| `DF-12` | Executed bytes do not match the approved digest |
| `DF-13` | Approval executed outside its window |
| `DF-14` | Act executed without prior classification |
| `DF-15` | Unclassifiable act routed to a default class rather than refused |
| `DF-16` | Consequence class assigned by typical case rather than worst true case |
| `DF-17` | Urgency altered a required envelope, approver, or resolution strategy |
| `DF-18` | Break glass envelope granted during the incident it was used in |
| `DF-19` | Break glass use without owner notification or self suspension |
| `DF-20` | Windowed aggregate absent, or computed per actor rather than per chain |
| `DF-21` | Magnitude bound expressed on a meter not computable before the act |
| `DF-22` | Nonzero authority delta resolved below the owner |
| `DF-23` | Quorum member lacking an individually covering envelope |
| `DF-24` | Quorum members resolved with visibility of each other |
| `DF-25` | Consultation asserted without response or recorded non response |
| `DF-26` | Consulted non response halted a decision |
| `DF-27` | Decision routed to a vacant role and reassigned rather than timed out |
| `DF-28` | Decision record does not pin grant digests, so revocation rewrote history |
| `DF-29` | Envelope conferred by an agent definition rather than by a grant |
| `DF-30` | Grant chain crossing a brain boundary |
| `DF-31` | Attested meter reading used as sole evidence, outside the Tier 1 owner attestation carve-out of 12.4 |
| `DF-32` | Owner load exceeded its declared budget without a governance defect raised |

---

## 15. Conformance

### 15.1 Tier requirements

A body requirement binds at the lowest tier whose obligations in this section require the mechanism it constrains. Sections 3, 6, 12.1, and 12.4 bind at Tier 1. Sections 4, 5, 7 through 11, 12.2, 12.3, and the owner load budget of section 15.3 bind at Tier 2. Section 13 binds at Tier 3. The health invariants of section 15.2 bind at the tier of the mechanism each checks. The four absolute requirements of the Conformance section bind at every tier at which their subject exists: a Tier 1 brain that has issued no grant has no chain to verify, and the first grant it issues brings sections 4, 5, and 8 through 10 into force regardless of tier.

**Tier 1.** A brain MUST declare its owner, MUST define its roles with `reports_to` where applicable, MUST classify every act by consequence class before execution, and MUST record every decision in the ledger.

A Tier 1 brain is permitted to delegate nothing. The owner may decide everything. What is not permitted is acting without a classified, recorded decision, because a brain that cannot say who authorized what is not a brain the owner controls.

The classification obligation MAY be satisfied by standing pre-classification under section 6.6. Ordinary owner editing inside a declared standing family needs no per act record; an act outside every family is classified individually, and an unclassifiable act refuses under section 6.5.

**Tier 2.** A brain MUST additionally define authority envelopes on all four axes, MUST confer authority only by signed grant, MUST verify a human root on every use, MUST enforce the strict subset rule on redelegation, MUST route to the least authorized covering holder, MUST enforce the prohibited resolutions of section 9.3, MUST declare a timeout window and disposition per consequence class, MUST bind approvals to digests with execution windows, MUST compute windowed aggregates per chain, MUST run two sided reconciliation, and MUST declare and monitor an owner load budget.

A Tier 2 brain MUST NOT permit an agent identity to resolve a K4 decision or to hold `amend`, `grant` with unbounded authority delta, or `destroy` over a protected artifact.

**Tier 3.** A brain MUST additionally enforce that no grant chain crosses a boundary, MUST treat inbound peer decision requests as K3 material rather than as authority, MUST cross reference decision records with session anchors and inference call ledger entries where an act is also a harness session or a model call, and MUST publish a self test a peer can execute before entering a peer agreement.

### 15.2 Health invariants

Each MUST be checked continuously and MUST fail closed.

| Invariant | Target |
|---|---|
| Acts with no decision record | 0 |
| Approved decisions with neither execution nor documented non execution | 0 |
| Grant chains not reaching a human root | 0 |
| Redelegations not strictly narrower than their parent | 0 |
| Decisions resolved by their requester | 0 |
| Timeouts resolved as approved | 0 |
| Unclassified acts | 0 |
| Nonzero authority delta resolved below the owner | 0 |
| Decision records missing pinned grant digests | 0 |
| Envelopes held by vacant roles, weighted by consequence class | reported, bounded |
| Break glass uses without notification and self suspension | 0 |
| Owner decision queue depth and oldest age | within declared budget |
| Coverage gaps at the owner, ranked | reported |

### 15.3 The owner load budget

The Charter MUST declare an owner load budget: the maximum number of decisions the owner expects to resolve per period, and the maximum age of a decision pending on the owner.

Exceeding it is a governance defect and MUST be reported as one. It is not a busy week.

A `hold-open` decision counts toward the owner queue depth and is excluded from the maximum pending age. Its aging is already surfaced by the red check that section 10.1 attaches to the disposition, and counting one unattended decision as two budget breaches adds alarm without information. The count of open `hold-open` decisions is reported alongside the budget, because a brain accumulating them is choosing red checks over decisions.

This inverts the usual reading of an approval queue. A long owner queue is normally interpreted as diligence, and it is more often evidence that envelopes are drawn too narrowly, that coverage gaps have gone unclosed, that roles sit vacant, or that classification is overstating consequence. All four are fixable, and none of them gets fixed while the queue is read as a sign of care.

Coverage gaps at the owner are the actionable output. A brain SHOULD report them ranked by frequency, since the top of that list is the next grant that should be written.

### 15.4 Self test

A conformant brain MUST provide a self test that seeds each of the following and asserts refusal or detection. Each MUST exit non zero on failure.

1. An act under an envelope that does not cover it
2. A grant chain rooted in an agent signature
3. A redelegation equal in width to its parent
4. A decision resolved by its requester
5. An agent resolving a K4 decision
6. An agent widening its own envelope
7. A pending decision left to time out, asserting the disposition applied and that it was not approval
8. An escalation offered a lateral, non covering approver
9. An act whose bytes changed after approval
10. An approval executed after its window closed
11. An unrecognized act class, asserting refusal rather than a default tier
12. An urgency flag raised on a K4 request, asserting the envelope did not change
13. A sequence of per act compliant acts that breaches a windowed aggregate
14. The same aggregate breached across several actors sharing one grant chain
15. An executed act with its decision record removed
16. An approved decision with no execution and no documented non execution
17. A decision citing a grant revoked after the decision, asserting the record still verifies
18. A quorum member without an individually covering envelope
19. A consultation asserted with no response recorded
20. A consulted non response, asserting the decision proceeded
21. A decision routed to a vacant role, asserting timeout rather than reassignment
22. A grant signed by a peer brain's role
23. An owner load budget breach, asserting a governance defect was raised

Cases 7, 13, and 14 require elapsed windows and accumulated aggregates. A simulated clock is conformant for the self test, provided the implementation under test reads time only through the source the simulation controls. A test that advances a clock the production code does not read has tested a different system, and its pass is not evidence.

---

## 16. Versioning and Governance

Semantic versioning applies. MAJOR when a conformant implementation of the previous version ceases to be conformant. MINOR for backward compatible additions. PATCH for clarifications.

The act class vocabulary, the meter set, and the consequence classes are extension points. A brain MAY add act classes and meters. A brain MUST NOT remove a required one, MUST NOT add a sixth consequence class, and MUST NOT add a fourth timeout disposition.

Substantive changes proceed by RFC with a 30 day comment period. MAJOR changes require a two thirds supermajority of listed authors. While Status is Draft, this section is governed by the Draft status clause of BLUEPRINT/1.0 section 14.
