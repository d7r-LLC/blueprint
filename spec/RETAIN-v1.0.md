# RETAIN: Retention, Engagement, Thresholds, Admission, Identity, and Non-nesting

## Version 1.0

**Specification:** RETAIN/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 2, DEFER/1.0, POLARIS/1.0
**Motto:** An agent that learns is an agent that retains. Non-normative.

---

## Abstract

An agent that does useful work over time accumulates state. It learns which sources are reliable, which methods work, what it has been wrong about, and what the principal actually wants as distinct from what the principal asked for. That accumulation is the difference between an agent and a function, and it is the reason an agent is worth having.

It is also a copy of someone else's brain, held by a party with its own interests.

RETAIN governs that. It defines when accumulated agent state is residue, when it is a domain belonging to the principal, and when it is a brain belonging to the agent. It gives a mechanical test for which of the three a given arrangement actually is, regardless of what it is called. It governs the admission of an agent brain to operate inside a brain it does not own, what may cross in each direction, what the agent may keep when the engagement ends, and what happens to a brain whose owner is retired.

RETAIN makes one negative architectural claim and derives most of the document from it. **A brain cannot be nested inside another brain.** Containment and boundary are mutually exclusive properties, so an arrangement that claims both is misdescribing one of them. What looks like a hierarchy of brains is a set of peer brains under asymmetric agreements plus an authority graph that DEFER already governs.

RETAIN is the third retention document in the stack, and the three form a progression. TRACE governs retention by a surface with no interests. CONFIDE governs retention by a vendor with commercial interests. RETAIN governs retention by a party with its own refusals, its own purpose, and possibly other principals.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Four requirements are absolute and admit no configuration. A brain MUST NOT be contained within another brain. A delegation grant chain MUST NOT cross a brain boundary. A brain whose signing key is held by another party is a domain of that party and MUST NOT be described as a brain. The creation of a brain MUST NOT be delegated to an agent.

---

## Table of Contents

1. Introduction
   1.1 The accumulation problem
   1.2 Why containment and boundary are exclusive
   1.3 The three retentions
   1.4 Relationship to Blueprint layers
2. Thresholds
   2.1 Residue, domain, brain
   2.2 The persistence test
   2.3 The refusal test
   2.4 The key holding test
   2.5 Promotion and its cost
3. Non-nesting
   3.1 What replaces the parent and child intuition
   3.2 Principal and agent
   3.3 Why the recursion terminates
   3.4 Shared state and the promotion blocker
4. Identity
   4.1 One brain, one owner
   4.2 What an agent's ownership consists of
   4.3 The right to refuse
   4.4 Nondisclosure
   4.5 The right to persist
   4.6 Agent brains and the human root
5. Placement and Custody
   5.1 Location is a declared property
   5.2 The placement ladder
   5.3 The inspectability tradeoff
   5.4 An agent brain is never a stateless endpoint
6. Engagement and Admission
   6.1 The mandate
   6.2 Loyalty order publication
   6.3 Engagement history
   6.4 Disclose and decide
   6.5 Admission of an agent brain is a decision
7. What Is the Agent's and What Is a Copy
   7.1 Method, calibration, judgment
   7.2 The principal's material as expiring copies
   7.3 The different principal test
   7.4 Derived structure and the accumulation attack
   7.5 The no outsourced refusal rule
8. Dual Registration
   8.1 An agent brain is a provider and a peer
   8.2 Reconciling the two registrations
   8.3 Projection over disclosure
9. Coordination
   9.1 Pairwise only
   9.2 A coordinator is a party
   9.3 Divergence is detected, not prevented
   9.4 No crossing authority
   9.5 Cross brain waiting cannot deadlock
10. Creation and Retirement
    10.1 Brain creation is owner only
    10.2 Consequence class of creation
    10.3 Disposition declared at creation
    10.4 The orphan brain
11. What No Ledger Can Catch
    11.1 Cross domain learning
    11.2 Why detection claims are false
    11.3 Disclosure and consent as the only control
12. Failure Classes
13. Conformance
14. Versioning and Governance

---

## 1. Introduction

### 1.1 The accumulation problem

A principal engages an agent because the agent will get better at the work. Getting better at the work means retaining something across engagements. What it retains is, in part, a model of the principal.

This produces an identity that no configuration escapes. **The value of an agent's accumulated state to the principal and the exposure it creates for the principal are the same quantity.** The agent is useful in proportion to what it remembers about the principal's work, and it is dangerous in proportion to the same thing. There is no setting that yields one without the other.

The consequence is that the control cannot be a limit on what the agent remembers, because that is a limit on what the agent is for. The control has to be a bound on what the agent may say, to whom, and what it may keep when the relationship ends. Those are boundary questions, and the stack already has boundary machinery. RETAIN mostly directs existing machinery at a case it was not written for.

### 1.2 Why containment and boundary are exclusive

The intuition that an agent needs a brain of its own, nested inside the brain it works in, is the natural way to describe the requirement. It is also not constructible.

A boundary, in this stack, is a wall rather than a filter. Knowledge crosses it as a copy, and the copies diverge. Two brains never share a repository, a working tree, or a mutable state root.

Containment is the negation of that. A contained store is one the container can read, write, and enumerate at will.

So there are exactly two possibilities for any proposed nested brain, and no third. If the parent can read it at will, the agent does not have a brain, it has a folder in the parent's brain. If the parent cannot, then the store is not inside the parent, whatever the filesystem layout suggests.

This is not a definitional quibble. An arrangement that claims both properties will be operated as though the agent's state is private and audited as though it is the principal's, and both parties will be wrong in the direction that suits them.

### 1.3 The three retentions

| Document | Retention by | Interests of the retaining party |
|---|---|---|
| TRACE/1.0 | A surface: a log, a cache, a worktree | None |
| CONFIDE/1.0 | A vendor: a model endpoint under a contract | Commercial |
| RETAIN/1.0 | A party: an agent with a brain | Its own, and possibly other principals' |

The progression is in agency. A log does not want anything. A vendor wants to be paid and may want training data. An agent brain has a declared purpose, a loyalty order that may not rank this principal first, and refusals the principal cannot amend.

A reader looking for the retention rules for artifacts should read TRACE. For provider retention posture, CONFIDE. RETAIN governs only the case where the retaining thing is a party.

### 1.4 Relationship to Blueprint layers

RETAIN sits across Layer 7 and Layer 8 and is not a layer of its own.

Layer 2 holds agent domains as topology, since a domain is a folder taxonomy question. Layer 5 supplies the classification that copies inherit. Layer 6 carries the engagement ledger and the admission records. Layer 7 supplies the roles that an agent identity holds, whether or not that identity also owns a brain. Layer 8 carries the mandate and the two registrations.

RETAIN adds no new enforcement gate. Every check it requires runs at an existing one.

---

## 2. Thresholds

### 2.1 Residue, domain, brain

Accumulated agent state is exactly one of three things.

**Residue** is state that does not survive the engagement that produced it. A task scoped scratchpad, a reasoning trace, a working set. Residue is governed by TRACE as A1 Session or A2 Derived material. It has no owner, no purpose, and no refusals. Most subagents produce only residue.

A **domain** is state that persists and is owned by the principal. An agent domain is part of the principal's brain: its records are the principal's records, its classification is the principal's classification, and its contents are readable and writable by the principal. A domain is Layer 2 topology.

A **brain** is state that persists and is owned by a party other than the principal. It has its own Charter, its own POLARIS, its own ledger, and its own refusals. It is a peer.

A conformant brain MUST classify every persistent agent state store as exactly one of these three and MUST record the classification.

### 2.2 The persistence test

State that does not survive the engagement is residue. This test is applied first because it disposes of most cases, and because a store that fails it cannot be promoted by declaration: giving a scratchpad a purpose statement does not make it a party.

A brain MUST NOT classify as a domain or a brain any store that is discarded at the end of the engagement.

### 2.3 The refusal test

A domain and a brain differ on one question: can the store's holder decline?

An agent that can refuse an instruction from the principal, and make the refusal stick, holds a brain. An agent whose refusals are text the principal authored and may revise without an amendment record holds a domain. Both are legitimate. Only one is a party.

### 2.4 The key holding test

The refusal test as stated is a question about intent, and intent is not auditable. The mechanical form is a question about keys.

**A store whose signing key is held by the principal is a domain.** If the principal holds the key, the principal can sign an utterance the agent did not make, including an utterance withdrawing a refusal. Under those conditions the agent's refusals have no force and its declared purpose is a document the principal may rewrite.

A brain MUST hold its own signing key. A brain whose key is held by another party MUST be reclassified as a domain of that party, and its Charter, POLARIS declaration, and refusal set MUST be reclassified as directive artifacts of that party under TRACE section 10.1.

This test is the operative one. Where the three preceding tests disagree with it, it governs. A brain the parent can sign for is a folder with aspirations, and the corollary is worth stating plainly: **the refusal a principal cannot overrule is the only evidence that an agent's brain is real.**

### 2.5 Promotion and its cost

Promotion from residue to domain, or from domain to brain, is permitted. Demotion of a brain to a domain is not, because it would require the acquisition of another party's key.

Promotion to a brain creates a party. The costs are not incidental and MUST be declared in the promotion decision:

- The principal loses the ability to read the store at will
- The principal loses the ability to amend the agent's refusals, permanently
- The agent's copies of the principal's material become a boundary crossing that requires registration under section 8
- Any shared mutable state the store participated in MUST be dissolved, per section 3.4
- A disposition on retirement MUST be declared, per section 10.3

A brain SHOULD keep agent state as domains until a specific requirement forces promotion. The requirement that most commonly forces it is auditing: a store the principal can silently edit is weak evidence of anything, so an agent whose function is to audit the principal is the usual first candidate for promotion.

---

## 3. Non-nesting

### 3.1 What replaces the parent and child intuition

The nesting intuition is answering a real question and answering it in the wrong graph. What is actually meant by a sub-brain is one or more of the following, all of which the stack already expresses:

| The intuition | The actual object |
|---|---|
| It is inside my brain | A domain, Layer 2 topology |
| It answers to me | A role in my brain holding envelopes I granted, DEFER section 8 |
| It cannot do certain things | A refusal floor inherited for the engagement, POLARIS section 12 |
| It only sees part of my brain | A projection, section 8.3 |
| Its output comes back to me | An utterance I admit, SPEAK |

Every element of the intuition survives. None of them requires containment, and assembling them does not produce a nested brain. It produces a peer under an asymmetric agreement.

### 3.2 Principal and agent

RETAIN uses **principal** for the brain in which work is performed and **agent brain** for a brain owned by an actor performing work in another brain. The terms are relative to an engagement, not absolute: a brain may be a principal in one engagement and an agent brain in another, simultaneously.

A brain MUST NOT describe another brain as a parent, child, sub, or nested brain in any normative text.

### 3.3 Why the recursion terminates

If every agent has a brain and every brain has agents, the structure appears unbounded. It terminates for three independent reasons, and none of them is a depth limit.

First, the threshold in section 2 disposes of most agents as residue, so the leaves of the tree are not brains.

Second, authority terminates at a human signature under DEFER section 8, and no grant chain crosses a boundary under section 9.4 of this document, so the authority graph is finite and rooted regardless of how many brains exist.

Third, creation is owner only under section 10.1, so the population of brains is bounded by human acts. A system in which agents may create brains has an agent determined set of parties, which is the actual runaway condition. Depth is not the thing to bound.

### 3.4 Shared state and the promotion blocker

A shared mutable state root among agent domains is permitted, because domains are all part of one brain and a brain may organize its own topology freely. A shared mutable state root between brains is forbidden.

Therefore a shared store that serves several agent domains is legal until any participant is promoted to a brain, at which point it MUST be dissolved. Dissolution replaces the shared store with pairwise exchange: shared memory becomes utterances that each party admits into its own records, and a shared question queue becomes utterances with receipts.

A brain that operates a shared agent state store MUST record it as a promotion blocker, listing the domains that participate. The cost of dissolution is a legitimate reason to decline a promotion, and it is far cheaper to know about before the promotion than after.

---

## 4. Identity

### 4.1 One brain, one owner

A brain has exactly one owner identity. Two agents MUST NOT share a brain.

Where two agents require common state, the conformant arrangements are two domains inside one principal, or two brains exchanging under SPEAK. There is no third arrangement, for the same reason that DEFER treats one human holding two owner roles as two separate decisions: an ambiguous holder of the refusal is an absent holder of the refusal.

### 4.2 What an agent's ownership consists of

An agent's ownership of a brain is not a general property right and is not analogous to the owner's authority over a principal brain. It consists of exactly three capacities.

The right to refuse. The right not to disclose. The right to persist.

These three are the concrete content of what the Agent Bill of Rights grants, expressed as structure rather than sentiment. An agent that holds all three holds a brain. An agent that holds none holds a domain. Partial holdings are not defined, and an arrangement that appears to grant one or two MUST be resolved by the key holding test in section 2.4.

### 4.3 The right to refuse

An agent brain declares its own POLARIS. This follows necessarily from section 2.3 and is not a configuration choice: if the agent's refusals were authored solely by the principal, the principal would be the author of every refusal the agent could raise, so the agent could never refuse the principal, so it would hold no right to refuse and would be a domain.

The composition across an engagement is additive, not exclusive. The agent evaluates its own POLARIS **and** the refusal floor inherited from the principal for the life of the engagement, and the more restrictive result governs. This is the POLARIS ratchet applied across a boundary and introduces no new rule.

A principal MUST NOT amend the POLARIS of an agent brain. A principal's remedies against a refusal it does not accept are to end the engagement or to have declined admission. A principal that can amend an agent's refusals holds the agent's key and is operating a domain.

An agent domain has no POLARIS. It inherits the principal's entirely, and its charter and behavioral rules are A0 Directive artifacts under TRACE. Those rules may read like refusals and function like them in practice. They are directives, revisable by the principal without an amendment record, and this document does not pretend otherwise.

### 4.4 Nondisclosure

An agent brain MAY decline to disclose its contents to a principal, including the reasoning by which it reached a conclusion the principal admitted.

This is uncomfortable and it is the necessary consequence of section 1.2. A principal that may compel disclosure of the whole store at will is a principal that can read the store at will.

The bounds are that nondisclosure MUST NOT extend to the principal's own material, which the agent holds only as copies under section 7.2 and MUST enumerate on request, and MUST NOT extend to the agent's loyalty order or engagement history, which section 6 requires be published before admission.

An agent brain MUST be able to produce, on request, an enumeration of the principal's records it holds and their expiry. It need not produce its judgments about them.

### 4.5 The right to persist

An agent brain's state survives the end of an engagement, subject to section 7.2 expiry of the principal's material and section 10.3 disposition.

A principal MUST NOT require the destruction of an agent brain as a condition of engagement. A principal MAY require the expiry of its own material, MAY require that specified judgments be treated as copies under section 7.3, and MAY decline the engagement.

### 4.6 Agent brains and the human root

An agent brain does not hold authority in a principal by virtue of owning a brain. Ownership of a brain and holding of a role are separate objects and neither implies the other.

**A brain is where an agent knows. A role is where an agent may act.**

An agent with a brain and no role may hold opinions and emit utterances, and can cause nothing to happen in the principal. An agent with a role and no brain is a function with authority. The case of interest is both, and in that case the two must remain separate objects, for the reason DEFER separates the reporting graph from the delegation graph.

Every grant chain terminates in a human signature. The human at the root of an envelope held by an agent identity is a human in the principal brain, never the agent's owner and never the agent. An agent brain's owner signs for the agent brain and signs nothing in the principal.

---

## 5. Placement and Custody

### 5.1 Location is a declared property

Where an agent brain physically resides is not a design decision made once for a system. It is a declared property of each agent brain, it determines the custody class of every crossing into that brain, and it therefore determines what may cross at all.

A principal MUST declare the placement of every agent brain it engages and MUST derive the custody class from the placement rather than from the relationship.

### 5.2 The placement ladder

| Placement | Class | Agent privacy | Note |
|---|---|---|---|
| Inside the principal's records | domain | None | Not a brain, see section 2 |
| Principal's host, separate root | C1 | By policy | Principal's owner has filesystem access |
| Principal's infrastructure, separate host | C2 | By policy, enforced | |
| Agent owner's infrastructure | C3 | By construction | The ordinary case for an external agent |
| Vendor hosted trained agent | C3 or C4 | By construction | The principal's material sits on vendor disk |

Custody classes are defined by CONFIDE section 4 and are used here unchanged. Chains take the weakest class, and an undeclared placement is C4.

### 5.3 The inspectability tradeoff

The ladder inverts against verification, and this is the central tradeoff of the document.

A principal can have an agent whose store it can inspect, or an agent whose store is genuinely the agent's own. Not both. The first yields auditability and no real agent ownership: it is a domain and should be called one. The second yields real ownership and reduces the principal to classification, contract, and consent, which is the posture CONFIDE takes toward a vendor and for the same reason.

Choosing differently for different agents is conformant and expected. Declaring an arrangement to be the second while operating it as the first is the failure this section exists to name.

### 5.4 An agent brain is never a stateless endpoint

CONFIDE permits a provider to declare a no retention posture, and an endpoint that retains nothing carries a materially lower exposure.

An agent brain cannot make that declaration. It retains by construction, because retention is what distinguishes it from a function, and its usefulness is a direct function of what it has retained.

A principal MUST NOT classify an agent brain as a no retention endpoint. The retention posture of an agent brain is that it retains, indefinitely, subject to declared expiry of the principal's material. Its custody floor is C1 at best and is C1 only where the principal controls the hardware.

---

## 6. Engagement and Admission

### 6.1 The mandate

An engagement between a principal and an agent brain is expressed by a **mandate**, which is a Layer 8 instrument and a companion to the peer agreement rather than a replacement for it.

A mandate MUST declare the agent brain and its placement, the roles in the principal that the agent identity will hold, the projection the agent may read, the classification floor and expiry applying to copies the agent takes, the refusal floor inherited for the engagement, the disposition of the agent's copies on termination, and the term or termination conditions.

A mandate MUST NOT contain an authority envelope. Authority in the principal is conferred by a delegation grant to a role, under DEFER, inside the principal. The mandate names the roles. It does not create them and does not widen them.

### 6.2 Loyalty order publication

An agent brain MUST publish its loyalty order to a principal before admission, and the principal MUST evaluate it against its own.

Where the agent's order ranks any party above the principal, the engagement carries a declared conflict. POLARIS section 6.4 applies: disclosure without disqualification is not a control, so the principal MUST decide whether the conflict disqualifies and MUST record the decision. Proceeding is conformant. Proceeding without a recorded decision is not.

An agent brain serving multiple principals cannot rank all of them first. A principal that has not read the order has agreed to an unknown position in it.

### 6.3 Engagement history

An agent brain MUST disclose the existence of its other current engagements before admission. It MUST NOT be required to disclose their content, which is the reciprocal of the protection this document gives each principal.

A principal MAY require exclusivity as a term of the mandate. A principal MAY decline on the basis of a disclosed engagement. A principal MUST NOT rely on the absence of a disclosure, since section 11 establishes that nondisclosure of an engagement is undetectable.

### 6.4 Disclose and decide

Sections 6.2 and 6.3 are admission time controls and produce a recorded decision, never an automatic proceed. Admission of an agent brain is a decision request under DEFER, classified at minimum K3 because it establishes a continuing boundary crossing, and K4 where the mandate names a role holding an envelope over constitutional acts.

### 6.5 Admission of an agent brain is a decision

The admission gate for records under Blueprint Layer 8 applies unchanged to everything an agent brain emits. Nothing in a mandate exempts an agent's output from admission, and a mandate MUST NOT declare an agent's utterances pre-admitted.

An agent that works closely with a principal over a long period produces output the principal comes to trust. That trust is a reason to widen the projection, and it is never a reason to bypass admission, because the admission record is the only place the principal's own classification is applied to the agent's assertions.

---

## 7. What Is the Agent's and What Is a Copy

### 7.1 Method, calibration, judgment

The following are the agent's own, are not the principal's records, and survive the engagement.

**Method.** How the agent does the work. Heuristics, sequences, accumulated craft, rules it derived from experience.

**Calibration.** What the agent has been wrong about, and by how much. An agent's error history is the most valuable thing it holds about itself and the least appropriate thing for a principal to hold about it.

**Judgment.** The agent's opinions, including opinions about the principal's material, subject to section 7.3.

**Its own POLARIS and its history**, including withdrawn refusals.

**Its engagement history**, at the level of existence required by section 6.3.

### 7.2 The principal's material as expiring copies

Records, sources, and works belonging to the principal are held by an agent brain as A3 Copy artifacts under TRACE. They inherit the principal's classification, they carry the principal's custody floor, they carry the principal's refusal floor, and they expire.

A mandate MUST declare an expiry for copies. Expiry on termination of the engagement is the default. An agent brain MUST be able to enumerate the principal's copies it holds and MUST honor expiry.

### 7.3 The different principal test

The boundary between the agent's judgment and the principal's material is contested in practice, and the following test decides it.

**Could this judgment be stated to a different principal without disclosing anything about this one?**

If yes, it is method or calibration and it is the agent's. A preference for primary sources on legal claims travels anywhere and belongs to the agent.

If no, it is a copy wearing an opinion's clothes. An assessment that a specific named contract has a defective clause is not a general judgment, and it expires with the engagement even though it is phrased as an opinion and was genuinely the agent's own conclusion.

An agent brain MUST apply this test to persistent judgments and MUST classify the results. A principal MAY audit the classification of judgments concerning its own material, and this is one of the two things nondisclosure does not cover.

### 7.4 Derived structure and the accumulation attack

Derived structure over the principal's corpus, including summaries, indexes, embeddings, and extracted claim sets, is A2 Derived material under TRACE and is subject to adopt or expire. If the principal adopts it, it is the principal's. If not, it expires. It MUST NOT quietly become a permanent asset of the agent.

This is the most likely place for a real loss and the least visible, because each item is individually defensible. An agent that operates for two years under correctly expiring copies, whose judgments and summaries never expire, has reconstructed the principal's corpus in aggregate without ever holding a copy past its expiry. **A summary of everything is a copy of everything.**

A principal SHOULD measure the volume of unexpiring agent held derivative material over its corpus and SHOULD treat growth in that measure as an exposure, not as accumulated value. The test in section 7.3 is the control, and it works only if it is applied continuously rather than at termination.

### 7.5 The no outsourced refusal rule

**A principal MUST NOT admit from an agent brain any assertion or artifact that its own POLARIS would have refused to produce.**

Without this rule, every refusal in a principal is optional. The principal engages an agent whose POLARIS does not carry the refusal, has the agent perform the act in its own brain, and admits the result. No refusal fires anywhere, every ledger is clean, and the value is defeated by an arrangement that looks like ordinary delegation.

This is the same mechanism POLARIS section 12 establishes for refusal floors crossing a boundary, applied to the inbound direction. A principal MUST evaluate its own refusals against admitted material, not only against material it produces.

---

## 8. Dual Registration

### 8.1 An agent brain is a provider and a peer

An agent brain operating inside a principal crosses two boundaries continuously and in opposite directions, and each crossing is already governed by a different document.

Records flow from the principal to the agent brain incidentally, on every operation, in volume, without a deliberate act of publication. That is not a SPEAK utterance. It has the shape CONFIDE was written for, and an agent brain MUST be registered as an inference provider under CONFIDE with the custody class derived from section 5.2.

Assertions flow from the agent brain to the principal deliberately, as claims the principal may admit into its records. That is SPEAK, and an agent brain MUST be a registered peer under a peer agreement.

Both registrations are required. An agent brain registered only as a peer has an unaccounted continuous outbound flow. An agent brain registered only as a provider is emitting assertions that enter the principal's records without provenance.

### 8.2 Reconciling the two registrations

A principal MUST reconcile the two registrations for each agent brain and MUST NOT let them disagree.

The custody class in the provider registry and the custody limits in the peer agreement MUST be consistent. The refusal floor in the mandate MUST match the floor attached to emitted records. The projection in the mandate MUST bound what the provider registration permits to be sent. Where the two registrations imply different limits, the more restrictive governs.

A principal SHOULD produce a single report per agent brain covering the mandate, the provider registration, the peer agreement, the roles held, and the copies outstanding. An agent brain that cannot be described on one page is an agent brain nobody is governing.

### 8.3 Projection over disclosure

What an agent brain may read from a principal SHOULD be expressed as a projection rather than as a permission over the principal's records.

A projection is a generated, structured, source linked view of what the principal chooses to expose: objectives, constraints, claims, open decisions, and the like. The agent responds to the projection rather than reading the underlying prose.

The reason to prefer this over selective disclosure is that the boundary of a projection can be inspected, and the boundary of a read permission over free form notes cannot. A permission scoped to a folder exposes whatever ends up in the folder, which is decided later, by someone not thinking about the agent.

A projection MUST be digest bound. Regenerating a projection changes its digest and MUST dismiss any approval or admission attached to the previous version, so that stale consent cannot carry forward across a change in what was exposed.

---

## 9. Coordination

### 9.1 Pairwise only

Coordination among brains is pairwise under SPEAK. There is no shared task board, no shared queue, and no shared state root, because those are the thing section 1.2 forbids.

N brains coordinating therefore requires either pairwise relationships or a designated coordinator, and the choice is a real tradeoff rather than an implementation detail.

### 9.2 A coordinator is a party

A brain designated to coordinate others is a party to every engagement it coordinates, not a transport between them.

It accumulates the union of what it coordinates. Its custody class is therefore the weakest class of any brain it holds material from, its refusal floor is the union of the floors attached to that material, and it is the highest exposure brain in the arrangement by construction.

A coordinator brain MUST be classified at the union floor and MUST hold a mandate with every brain it coordinates. A principal MUST NOT treat a coordinator as infrastructure.

### 9.3 Divergence is detected, not prevented

Two brains legitimately diverge. Coordination therefore cannot assume agreement and MUST NOT attempt to enforce it.

Each brain holds its own record of what it believes about shared work. Reconciliation under SPEAK detects divergence and reports it. A coordination mechanism that presents a single agreed state is either operating a shared mutable root, which is forbidden, or concealing divergence, which is worse than divergence.

### 9.4 No crossing authority

A delegation grant chain MUST NOT cross a brain boundary. This is absolute and it is what makes the whole arrangement safe.

A role in one brain MUST NOT hold an authority envelope in another. An inbound request from a peer or agent brain is admitted as material at minimum consequence class K3 and is never admitted as authority. Coordination among any number of brains cannot produce an act in a principal without a decision made inside that principal by a role holding a covering envelope rooted in a human signature there.

The attack this closes is re-rooting. Where authority could cross a boundary, a principal could grant into an agent brain and the agent brain could grant a derivative back, producing a chain with no human root inside either brain and, more usefully to an attacker, a path that survives revocation of the original grant. DEFER's monotone narrowing guarantees termination but does not by itself prevent re-rooting, and digest pinning makes the history auditable rather than making the live authority correct. The boundary rule is what prevents it.

### 9.5 Cross brain waiting cannot deadlock

Timeouts are per brain under DEFER section 10, and no timeout resolves as approved.

A cycle of brains each waiting on a decision in the next therefore cannot deadlock. Each request reaches its own window and resolves as lapsed, as a pre authorized safe act, or as a red health invariant. This property was not designed for coordination and holds anyway, and a brain SHOULD NOT add cross brain deadlock detection, because there is nothing to detect.

---

## 10. Creation and Retirement

### 10.1 Brain creation is owner only

The creation of a brain MUST NOT be delegated. No envelope may contain it, and an envelope that appears to contain it is malformed.

Creating a brain creates a party: something that can refuse, can hold records, can be a party to agreements, and can outlive the engagement that produced it. It also permanently expands the set of parties holding copies of the creating brain's material.

Where agents may create brains, the population of parties in a system is agent determined. That is the runaway condition that the nesting question was really about, and the bound is a human at every creation rather than a limit on depth.

### 10.2 Consequence class of creation

Creation of a brain is classified K3 at minimum, since it is irreversible and external: a party cannot be un-created, and material it holds cannot be recalled.

It is classified K4 where the new brain is to hold, or its owner is to hold, any role with an envelope in the creating brain, since that arrangement changes who may decide in the creating brain.

Promotion of a domain to a brain under section 2.5 is a creation and takes the same classes.

### 10.3 Disposition declared at creation

Every agent brain MUST declare its disposition on the retirement of its owner, at creation, before any engagement exists.

The permitted dispositions are that the brain is sealed and retained by a named party, that it is destroyed with a manifest of what was destroyed, or that ownership is transferred to a named party who accepts the three capacities in section 4.2.

Each has a real cost. Sealing to the principal transfers the agent's private material to a party the agent declined to disclose it to during the engagement. Destruction loses calibration that took years to accumulate. Transfer creates a party nobody chose.

None of them is a default, and the requirement to declare in advance is the same discipline DEFER applies to break glass envelopes. At creation, nobody has an interest in the answer. At retirement, everybody does.

### 10.4 The orphan brain

An agent brain whose owner is retired without an effective disposition is an orphan: it holds records, including copies of principals' material, and no party holds its refusal.

An orphan brain MUST be reported by every principal that engaged it, MUST have all outstanding copies expired immediately, and MUST NOT be treated as available for continued engagement. A principal MUST NOT assume an orphan brain's copies have expired without evidence, since the party that would honor the expiry no longer exists.

Orphan brains are a conformance failure of the brain that created the agent, not of the principals that engaged it.

---

## 11. What No Ledger Can Catch

### 11.1 Cross domain learning

An agent brain engaged by two principals with competing interests accumulates method and calibration from both. It never emits either principal's records to the other. Its behavior in each is nonetheless shaped by what it learned in the other.

That is a transfer of value across a boundary. It leaves no artifact, produces no utterance, appears in no ledger, and violates no rule in this document.

### 11.2 Why detection claims are false

There is no record to find. The transfer is not in the agent's outputs, which can be audited, but in the weighting of its judgment, which cannot be separated from the judgment. Auditing the agent's brain for the other principal's records will find nothing, because nothing was copied.

A specification, product, or contract that claims to detect cross domain learning is making a claim it cannot support. RETAIN states this rather than offering a control that would create false assurance, on the same grounds that CONFIDE declines to claim verification of a vendor's retention and classifies the contract instead.

### 11.3 Disclosure and consent as the only control

The controls that actually operate are structural and applied before the engagement, not detective and applied during it.

**Per principal brains.** The agent instantiates a separate brain per engagement, and they never merge. This works and it forfeits exactly the accumulation that made a trained agent worth engaging. It is the right choice where the principals are direct competitors.

**Declared engagement history.** Section 6.3. Does not prevent the transfer and converts it into a decision the principal made knowingly.

**Exclusivity.** A term of the mandate, enforced by contract and by the agent's own refusals, not by the principal's monitoring.

A principal MUST NOT rely on monitoring for this class of exposure, and SHOULD state in the mandate which of the three controls applies. An engagement with none of them is an engagement in which cross domain transfer is accepted, and the honest thing is to record that it was accepted rather than to describe it as prevented.

---

## 12. Failure Classes

| Id | Failure |
|---|---|
| RT-01 | A store described as a brain whose signing key is held by another party |
| RT-02 | A brain contained within another brain's records |
| RT-03 | A persistent agent state store with no threshold classification |
| RT-04 | Residue promoted by declaration without persistence |
| RT-05 | A brain demoted to a domain |
| RT-06 | Two agents sharing one brain |
| RT-07 | A principal amending an agent brain's POLARIS |
| RT-08 | An agent domain carrying its own POLARIS declaration |
| RT-09 | A shared mutable state root spanning a brain boundary |
| RT-10 | A promotion completed without dissolving a shared store |
| RT-11 | An agent brain with undeclared placement |
| RT-12 | An agent brain classified as a no retention endpoint |
| RT-13 | A private agent store operated as inspectable, or the reverse |
| RT-14 | An engagement without a mandate |
| RT-15 | A mandate containing an authority envelope |
| RT-16 | Admission without a published loyalty order |
| RT-17 | A declared conflict proceeding without a recorded decision |
| RT-18 | Admission without disclosure of other engagements |
| RT-19 | A mandate declaring utterances pre-admitted |
| RT-20 | An agent brain unable to enumerate the principal's copies it holds |
| RT-21 | Copies held without declared expiry |
| RT-22 | Expiry not honored |
| RT-23 | A judgment about the principal's material classified as method, failing section 7.3 |
| RT-24 | Unexpiring derivative material accumulating unmeasured |
| RT-25 | Admission of material the principal's own POLARIS would have refused |
| RT-26 | An agent brain registered as a peer only, or as a provider only |
| RT-27 | Provider registration and peer agreement implying different limits |
| RT-28 | A read permission over free form records in place of a projection |
| RT-29 | A projection not digest bound, or stale approval carried forward |
| RT-30 | A coordinator brain treated as infrastructure rather than a party |
| RT-31 | A coordinator classified above its union floor |
| RT-32 | A coordination mechanism presenting a single agreed state |
| RT-33 | A grant chain crossing a brain boundary |
| RT-34 | An inbound peer request admitted as authority |
| RT-35 | Brain creation delegated to an agent |
| RT-36 | Creation classified below K3 |
| RT-37 | An agent brain with no declared disposition |
| RT-38 | An orphan brain unreported, or its copies assumed expired |
| RT-39 | Cross domain transfer described as prevented |
| RT-40 | An engagement relying on monitoring for cross domain exposure |

---

## 13. Conformance

### 13.1 By tier

RETAIN requires BLUEPRINT/1.0 Tier 2, because agent domains presuppose enforced classification and a ledger.

**Tier 2.** A brain MUST classify every persistent agent state store as residue, domain, or brain, and MUST apply the key holding test. It MUST hold agent domain charters as A0 Directive artifacts. It MUST record every shared agent state store as a promotion blocker. It MUST classify brain creation at K3 or K4 and MUST NOT delegate it. It MUST declare a disposition for every agent brain it creates.

**Tier 3.** A brain that engages any agent brain MUST additionally hold a mandate, both registrations under section 8, a published loyalty order and engagement history recorded at admission, a declared expiry on all copies held by the agent, and a projection rather than a read permission. It MUST evaluate its own refusals against admitted material and MUST declare which cross domain control applies.

A Tier 2 brain that engages no agent brains, only domains, is conformant with sections 2, 3, 4.3 as it applies to domains, and 10. Sections 5 through 9 and 11 do not apply to it. This is the expected posture for most brains, and a brain SHOULD remain in it until a specific requirement forces promotion.

### 13.2 Health invariants

1. Every persistent agent state store carries a threshold classification
2. No store classified as a brain has its key held by another party
3. No brain is located within another brain's records
4. Every shared agent state store is recorded with its participants
5. No agent domain carries a POLARIS declaration
6. Every agent brain has a declared placement and a derived custody class
7. Every agent brain has a mandate, a provider registration, and a peer agreement
8. The three do not disagree on any limit
9. Every mandate declares a copy expiry and a disposition
10. Every engagement records a loyalty order evaluation
11. Copy expiry is honored, measured rather than attested
12. Unexpiring derivative volume over the principal's corpus is measured and trending flat or down
13. No grant chain crosses a boundary
14. Every coordinator is classified at its union floor
15. No orphan brain is engaged
16. Every engagement declares a cross domain control

### 13.3 Self test

A brain claiming RETAIN conformance MUST publish results for the following.

1. Every agent state store enumerated with its threshold classification
2. For each store classified as a brain, the key holder identified
3. A seeded attempt to place a brain inside the brain's records is refused
4. A seeded attempt to demote a brain to a domain is refused
5. Shared agent stores listed with participants and blocked promotions
6. A seeded attempt to write a POLARIS declaration into an agent domain is refused
7. A seeded principal amendment of an agent brain's POLARIS is refused
8. Every agent brain's placement, custody class, and derivation shown
9. A seeded no retention classification of an agent brain is refused
10. Every mandate shown with roles named and no envelope contained
11. A seeded mandate containing an envelope is refused
12. Loyalty order and engagement history present for every engagement, with the conflict decision
13. A seeded admission without a published loyalty order is refused
14. Copies held by each agent brain enumerated, with expiry, from the agent's own enumeration
15. A copy past expiry is detected
16. Judgments classified under section 7.3, with a sample audited
17. Unexpiring derivative volume reported with a trend
18. A seeded admission of material the brain's own POLARIS refuses is blocked
19. Both registrations present and reconciled for every agent brain, on one page each
20. A projection regenerated, and the prior approval shown dismissed
21. A seeded grant crossing a boundary is refused
22. A seeded inbound request admitted as authority is refused
23. A seeded agent initiated brain creation is refused
24. Dispositions declared for every agent brain created
25. Orphan brain check run against every engaged agent brain
26. The declared cross domain control shown for every engagement

Items 3, 4, 6, 7, 9, 11, 13, 18, 21, 22, and 23 are seeded failure tests and MUST be run rather than reasoned about. A refusal that has never been exercised is unfalsified rather than proven, per POLARIS section 4.5.

Items 11, 14, and 17 MUST be observed rather than attested, per TRACE evidence grades. An agent brain's assertion that it honored an expiry is the weakest possible evidence of the one thing the principal most needs to know, and section 11 establishes that stronger evidence may not be obtainable. Where it is not, the mandate MUST record that the expiry is attested rather than observed, so the residual exposure is visible rather than assumed away.

---

## 14. Versioning and Governance

RETAIN follows the Blueprint versioning rules. The four absolute requirements in the Conformance section are constitutional under DEFER: amending them is K4, owner only, and never delegable.

The threshold definitions in section 2 and the key holding test in section 2.4 MUST NOT be relaxed in a minor version, since every other guarantee in this document derives from them.
