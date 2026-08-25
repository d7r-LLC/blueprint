# Blueprint: A Specification for Owned, Governed Knowledge

## Version 1.0

**Specification:** BLUEPRINT/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0

---

## Abstract

A brain is a locally owned, policy governed, append only audited collection of plain text files that serves as the source of truth for an individual's or an organization's knowledge. This specification defines the structure of a brain in ten independently conformable layers, three conformance tiers, and the process by which a brain is established and operated.

The Blueprint is a specification of structure and governance, not an implementation. It requires only a storage device, a directory, and a plain text format. It is deliberately editor agnostic.

The Blueprint is customizable by design. An owner MUST be able to define their own taxonomy, their own workflow, and their own vocabulary. What the Blueprint fixes is not the shape of the knowledge but the discipline at its edges: what is recorded, what is approved, what is logged, and what is permitted to leave.

Exchange between brains is defined in a companion specification, SPEAK/1.0. Governance of language model inference over brain content is defined in a companion specification, CONFIDE/1.0. Governance of the artifacts that agent tooling leaves behind is defined in a companion specification, TRACE/1.0. All three are normative for the tiers that require them.

---

## Conformance

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL in this document are to be interpreted as described in RFC 2119.

Every normative requirement in this specification has a defined failure mode. Where a requirement can be violated, this document states what a conformant implementation does in response. The default response is to fail closed: refuse the operation rather than proceed with reduced guarantees.

---

## Table of Contents

0. Layer 0: Charter and Purpose (normative body: POLARIS/1.0)
   0.1 Owner declaration and tier claim
   0.2 Purpose, refusals, and the loyalty order (POLARIS/1.0 sections 3, 4, 6)
   0.3 The one way precedence rule (POLARIS/1.0 section 8)
1. Introduction
   1.1 The four specification stack
   1.1.1 The Blueprint protocol set
   1.1.2 Precedence
   1.2 Design principles
   1.3 Terminology
2. Layer 0: Charter
   2.1 Brain identity
   2.2 Ownership and legal entity
   2.3 Keys and keyring
   2.4 Lineage and chain of title
   2.5 Tier claim and layer declaration
   2.6 Inference posture declaration
3. Layer 1: Constitution
   3.1 The single governing file
   3.2 Precedence and the registry rule
   3.3 Prime directives
   3.4 Path anchors and portability
   3.5 Amendment
4. Layer 2: Topology
   4.1 Taxonomy requirements
   4.2 Domains and domain manifests
   4.3 Discovery over registration
   4.4 The shared entity layer
   4.5 System surfaces
   4.6 Harness artifact roots
   4.7 Scratch surfaces and declared exceptions
5. Layer 3: Records
   5.1 The frontmatter contract
   5.2 Controlled vocabularies
   5.3 Identifiers and filenames
   5.4 Derived state
   5.5 Authorship
   5.6 Derivation provenance and custody floors
6. Layer 4: Lifecycle
   6.1 Sources and works
   6.2 Stages
   6.3 Gates and hash binding
   6.4 Change authority
   6.5 Source hierarchy and conflict resolution
7. Layer 5: Classification
   7.1 Sensitivity
   7.2 Visibility
   7.3 Consent to record
   7.4 Consent to process
   7.5 The publication guard
   7.6 The export gate
   7.7 The custody matrix (CONFIDE/1.0 section 5)
   7.8 Inheritance by artifacts (TRACE/1.0 section 7)
8. Layer 6: Ledger
   8.1 Log families
   8.2 Append only semantics
   8.3 Coordination free identifiers
   8.4 Hash chaining
   8.5 Trusted time
   8.6 Decision records
   8.7 Session anchors and the artifact ledger (TRACE/1.0 sections 6 and 8)
   8.8 Protected artifacts and deletion as an entry
9. Layer 7: Agency (normative body: DEFER/1.0)
   9.1 Actor identity
   9.2 Agent identities and charters
   9.3 Authorities
   9.4 The enforcement hook
   9.5 Agents draft, the owner decides
   9.6 Inference authorization binding
   9.7 Credential isolation
   9.8 Directive artifacts as the source of agent behavior (TRACE/1.0 section 10.1)
   9.9 Roles, envelopes, and delegation grants (DEFER/1.0 sections 3, 4, 8)
   9.10 Consequence classification and routing (DEFER/1.0 sections 6, 9)
   9.11 Timeout dispositions and the prohibition on approval by timeout (DEFER/1.0 section 10)
   9.12 Agent state thresholds: residue, domain, brain (RETAIN/1.0 section 2)
   9.13 A brain is where an agent knows, a role is where an agent may act (RETAIN/1.0 section 4.6)
10. Layer 8: Boundary
    10.1 The three flows: input, output, inference
    10.2 Boundary mounting
    10.3 Relationship to SPEAK/1.0
    10.4 Relationship to CONFIDE/1.0
    10.5 Relationship to RETAIN/1.0
    10.6 Mandates and the dual registration of an agent brain (RETAIN/1.0 sections 6 and 8)
    10.7 Projections in place of read permissions (RETAIN/1.0 section 8.3)
11. Layer 9: Operations
    11.1 Host roles and single owner state
    11.2 Serializers and advisory state
    11.3 Leases
    11.4 Verification and continuous checks
    11.5 The inference broker as a required component
    11.6 Egress invariants
    11.7 Artifact enumeration and retention sweeps
    11.8 The conformance self test
12. Conformance Tiers
    12.1 Tier 1: Sovereign
    12.2 Tier 2: Governed
    12.3 Tier 3: Federated
13. Establishment Workflow
    13.1 The twelve phases
    13.2 Individual track
    13.3 Organization track
14. Versioning and Governance
15. Registry
16. Reference Implementation
    Appendix A: Charter schema
    Appendix B: Profile: individual
    Appendix C: Profile: organization
    Appendix D: Conformance test suite

---

## 1. Introduction

### 1.1 The four specification stack

*(to be written: ABR states what agents deserve, DERP what the runtime must provide, SAGA how an agent is represented, and the Blueprint how knowledge is held and exchanged. A Blueprint brain that hosts agent activity SHOULD run on a DERP conformant runtime and SHOULD identify its actors using SAGA identity.)*

### 1.1.1 The Blueprint protocol set

Blueprint is one specification with six normative companions, each governing a distinct question.

| Document | Question | Blueprint layer |
|---|---|---|
| POLARIS/1.0 | What is this brain for, and what will it never do | Layer 0, root of precedence |
| DEFER/1.0 | Who may decide, bounded by what | Layer 7 |
| SPEAK/1.0 | What crosses to another brain | Layer 8 |
| CONFIDE/1.0 | What crosses to a model | Layer 8 |
| TRACE/1.0 | What crosses into the tooling | Layer 8 |
| RETAIN/1.0 | Whose brain does an agent have | Layers 7 and 8 |

One brain, three boundaries, one authority model, one reason.

RETAIN is the only companion that spans two layers, because the question it answers is not a boundary question or an authority question but the point at which the two meet. An agent that accumulates state is either part of this brain or a party to it, and which one it is determines both what may cross to it and what it may decide.

### 1.1.2 Precedence

Precedence in this stack is asymmetric, and the asymmetry is normative.

POLARIS/1.0 holds the highest precedence for **forbidding** an act and no precedence for **permitting** one. A POLARIS refusal blocks an act every other document allows. No POLARIS element may permit an act any other document forbids, relax a requirement, satisfy a check, confer authority, or excuse a failure. See POLARIS/1.0 section 8.

Below POLARIS, the order is the Constitution, then this document, then the boundary and authority companions, then profiles, then implementation. Where two documents at the same level conflict, the more restrictive requirement applies.

Precedence within this stack does not cross a brain boundary. An agent brain evaluates its own POLARIS and the refusal floor inherited from the principal for the life of the engagement, and the more restrictive result governs. A principal holds no precedence over an agent brain's own declaration and cannot amend it. See RETAIN/1.0 section 4.3.

The combined effect is a ratchet. Constraints accumulate cheaply and are removed only by amendment with a stated cause and a recorded history. A governance system should be easy to tighten and slow to loosen.

### 1.2 Design principles

*(to be written. The candidate set, from the design notes:)*

1. Plain text on a device the owner controls is the source of truth.
2. Location is not permission. A guard fires on promotion, never on placement.
3. Approval binds to bytes. An approval is void the moment the approved text changes.
4. Append only, never mutate. Corrections supersede, they do not overwrite.
5. Discovery over registration. Structure declares itself; no central list is maintained by hand.
6. Coordination free names. Never compute the next free number.
7. Fail closed. A brain that cannot verify refuses to act.
8. No mechanism may depend on standing human attention. Every gate has a TTL, a fail closed default, or a check that goes red.
9. Agents draft, the owner decides.
10. A boundary is a wall, not a filter. Knowledge crosses as a copy, and the copies diverge.
11. No inference without a declared custody boundary. Sending a record to a language model is a boundary crossing, and an uncatalogued crossing is a leak that has not been noticed yet.
12. What a tool leaves behind is part of the record. Session logs, derived memory, file snapshots, and scratch directories are either governed evidence or an ungoverned copy of the brain, and they do not become the former by being ignored.
13. Authority is a bounded envelope, not a rank. Seniority is a single number over a many dimensional space, so ranking roles makes every sufficiently senior role eligible to decide everything. The correct approver for an act is the one whose envelope covers it, which is usually the least authorized holder rather than the most senior one.
14. Urgency never widens authority. Urgency decides what happens while a decision waits. It never decides who may make it. A brain in which asserting urgency raises the ceiling has an escalation path any actor can open by asserting urgency.
15. A value that cannot produce a refusal is decoration. Purpose narrows what a brain will do and never widens it, and the highest layer in any stack is the most dangerous place to put a permission.
16. A brain the parent can sign for is a folder with aspirations. Containment and boundary are mutually exclusive, so a brain cannot be nested inside another brain. Whoever holds the signing key owns the refusal, and the refusal a principal cannot overrule is the only evidence that an agent's brain is real. What looks like a hierarchy of brains is a set of peers under asymmetric agreements plus an authority graph.

### 1.3 Terminology

*(to be written: brain, owner, actor, domain, record, source, work, stage, gate, ledger, boundary, peer, utterance, admission, adoption.)*

---

## 2 through 11

*(Layer sections to be written. See `design/0000-workflow-and-spec-design.md` section 3 for the layer table, the per layer notes, and the grounding in the reference implementation.)*

---

## 12. Conformance Tiers

Each tier includes every requirement of the tier below it. A brain declares its tier in its Charter. A peer MAY refuse to exchange with a brain below a required tier.

### 12.1 Tier 1: Sovereign

A Sovereign brain MUST implement Layers 0, 1, 2, and 3, and MUST implement the internal log families of Layer 6.

A Sovereign brain is owned, structured, and logged, and does not exchange knowledge with other brains.

A Sovereign brain that performs any language model inference over its own content MUST additionally satisfy CONFIDE/1.0 section 12.1 for Tier 1: it MUST maintain an inference provider registry and MUST record every call in an append only ledger. Cataloging is required at the lowest tier, because a brain that cannot say what it has sent, and where, is not a brain the owner controls.

A Sovereign brain that is operated on by any agent harness MUST additionally satisfy TRACE/1.0 section 13.1 for Tier 1: it MUST register every harness with declared artifact roots, MUST enumerate undeclared roots, and MUST declare every scratch surface that a harness writes inside the brain folder.

A Sovereign brain MUST satisfy POLARIS/1.0 section 15.1 for Tier 1. It MUST declare exactly one purpose statement, at least one refusal carrying a decidable predicate, a total loyalty order, and the normative status of every declared element. Purpose is required at the lowest tier because a brain with no declared reason for existing has nothing against which to test its own amendments.

A Sovereign brain MUST satisfy DEFER/1.0 section 15.1 for Tier 1. It MUST declare its owner, define its roles, classify every act by consequence class before execution, and record every decision in the ledger. A Tier 1 brain is permitted to delegate nothing and may have the owner decide everything. What is not permitted is acting without a classified, recorded decision.

A Sovereign brain MUST NOT contain another brain within its records, and MUST NOT delegate the creation of a brain. These two prohibitions bind at every tier, per RETAIN/1.0 section 13.1. A Tier 1 brain has no other RETAIN obligations, because agent state thresholds presuppose the enforced classification of Tier 2.

### 12.2 Tier 2: Governed

A Governed brain MUST additionally implement Layers 4, 5, and 7.

A Governed brain MUST enforce classification at exactly one boundary, by a check that terminates with a non zero status when a violation is present. A Governed brain MUST NOT permit an agent identity to approve a gate.

A Governed brain MUST satisfy CONFIDE/1.0 section 12.1 for Tier 2. It MUST route all inference through a single broker, MUST enforce the custody matrix, MUST hold provider credentials outside the reach of any agent process, MUST bind every agent charter to an inference authorization, and MUST fail closed when provider evidence has expired.

A Governed brain MUST satisfy TRACE/1.0 section 13.1 for Tier 2. It MUST anchor every harness session to its ledger, MUST seal evidence grade artifacts into an append only store under a declared policy, MUST hold directive artifacts inside the brain under version control and reference them by digest from the charters they implement, MUST record every deletion of a protected artifact, and MUST NOT permit an agent identity to delete one.

A Governed brain MUST satisfy DEFER/1.0 section 15.1 for Tier 2. It MUST define authority envelopes on all four axes, confer authority only by signed grant, verify a human root on every use, enforce strict narrowing on redelegation, route to the least authorized covering holder, bind approvals to digests with execution windows, compute windowed magnitude aggregates per delegation chain rather than per actor, declare a timeout window and disposition per consequence class, run two sided reconciliation between acts and decision records, and declare and monitor an owner load budget.

A Governed brain MUST NOT resolve a constitutional decision below the owner, MUST NOT permit an actor to approve a decision it requested, and MUST NOT permit a timeout to resolve a decision as approved.

A Governed brain MUST satisfy RETAIN/1.0 section 13.1 for Tier 2. It MUST classify every persistent agent state store as residue, domain, or brain, and MUST apply the key holding test, so that a store whose signing key it holds is classified as its own domain regardless of how the store is described. It MUST hold agent domain charters as directive artifacts rather than as values documents, and MUST NOT permit an agent domain to carry its own POLARIS declaration. It MUST record every shared agent state store with its participants as a promotion blocker. It MUST classify the creation or promotion of a brain at K3 or above and MUST declare that brain's disposition on the retirement of its owner at the moment of creation. A brain that engages no agent brains, only domains, has no further RETAIN obligations, and this is the expected posture for most brains.

A Governed brain MUST satisfy POLARIS/1.0 section 15.1 for Tier 2. It MUST evaluate refusals at every boundary crossing and record the evaluations in every decision record, MUST enforce the one way precedence rule mechanically, MUST test every refusal on its declared interval, and MUST enforce cooling periods on amendment. A refusal predicate MUST NOT require language model inference to evaluate, because a value enforced by a model is a value the model owns.

### 12.3 Tier 3: Federated

A Federated brain MUST additionally implement Layers 8 and 9, and MUST conform to SPEAK/1.0 and to CONFIDE/1.0 section 12.1 for Tier 3.

A Federated brain MUST declare custody limits in every peer agreement, MUST enforce the custody floor carried by every record it admits from a peer, and MUST report a floor violation to the speaking brain.

A Federated brain MUST enforce artifact custody floors, including in backups and vendor support bundles, and MUST register any harness that transmits session, derived, or copy artifacts to a third party as an inference provider.

A Federated brain MUST satisfy DEFER/1.0 section 15.1 for Tier 3. No delegation grant chain may cross a brain boundary. A role in a peer brain MUST NOT hold an envelope in this brain, and an inbound peer decision request is admitted as material at minimum consequence class K3, never as authority.

A Federated brain MUST satisfy POLARIS/1.0 section 15.1 for Tier 3. It MUST publish its refusals and loyalty order, attach refusal floors to emitted records, enforce inherited floors on admitted records, and include an alignment declaration in every peer agreement. A refusal that does not travel with the record it protects is laundered by the first boundary crossing.

A Federated brain that engages any agent brain MUST satisfy RETAIN/1.0 section 13.1 for Tier 3. It MUST hold a mandate declaring placement, roles, projection, copy expiry, and inherited refusal floor, and that mandate MUST NOT contain an authority envelope. It MUST register every agent brain both as an inference provider and as a peer, and MUST reconcile the two so that they do not disagree on any limit. It MUST record a loyalty order evaluation and a disclosure of other engagements before admission, with a decision recorded wherever a conflict is declared. It MUST expose records as a digest bound projection rather than as a read permission over free form notes. It MUST evaluate its own refusals against admitted material, since a refusal that can be performed by an engaged agent and admitted afterward is optional. It MUST declare which cross domain control applies, and MUST NOT describe cross domain learning as prevented or detected.

A Federated brain MUST publish a conformance self test that a peer can execute against it prior to entering a peer agreement.

---

## 13. Establishment Workflow

### 13.1 The fourteen phases

| Phase | Name | Exit gate | Tier |
|---|---|---|---|
| 0 | Declare | Owner signs the Charter, and the purpose statement, first refusal, and loyalty order are adopted | 1 |
| 1 | Constitute | Constitution adopted as a decision record | 1 |
| 2 | Scaffold | Scaffold self test passes | 1 |
| 3 | Schema | Schema check passes on a seeded record | 1 |
| 4 | Capture | First source preserved under a preservation gate | 1 |
| 5 | Develop | First work reaches mid stage with its belief gate approved | 2 |
| 6 | Classify | Publication check exits 0 on a clean work and non zero on a seeded violation | 2 |
| 7 | Ledger | Two concurrent minting attempts collide zero times | 2 |
| 8 | Agency | The enforcement hook blocks a deliberate forbidden write, and every declared refusal blocks a seeded violating act | 2 |
| 8a | Delegate | One envelope granted, one decision routed and resolved below the owner, one seeded self approval refused, one timeout observed resolving as anything but approval | 2 |
| 8b | Situate | Every persistent agent state store classified as residue, domain, or brain with its key holder identified, every shared agent store recorded as a promotion blocker, one seeded agent initiated brain creation refused, and one seeded POLARIS declaration inside an agent domain refused | 2 |
| 9 | Boundary | One full round trip: emit, admit, receipt, reconcile | 3 |
| 9a | Engage | One agent brain admitted under a mandate with both registrations reconciled, its loyalty order evaluated on the record, one projection regenerated with the prior approval shown dismissed, and one copy past expiry detected | 3 |
| 10 | Operate | Self test green on two hosts, single owner state proven | 3 |
| 11 | Federate | Key rotation and revocation exercised without data loss | 3 |

### 13.2 Individual track

*(to be written.)*

### 13.3 Organization track

An organization establishing a brain over existing material MUST import that material as sources. Imported material MUST NOT be admitted at a stage that implies review the organization has not performed.

*(to be expanded.)*

---

## 14. Versioning and Governance

Semantic versioning applies to the specification. MAJOR when a conformant implementation of the previous version ceases to be conformant. MINOR for backward compatible additions. PATCH for clarifications that do not alter conformance.

Substantive changes proceed by RFC with a 30 day comment period. MAJOR changes require a two thirds supermajority of listed authors.

---

## 15. Registry

*(to be written.)*

## 16. Reference Implementation

*(to be written.)*
