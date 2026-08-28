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

Six companion specifications complete the protocol set. POLARIS/1.0 governs purpose and refusals, DEFER/1.0 delegated authority, SPEAK/1.0 exchange between brains, CONFIDE/1.0 language model inference over brain content, TRACE/1.0 the artifacts that agent tooling leaves behind, and RETAIN/1.0 the state an engaged agent accumulates. All six are normative for the tiers that require them (section 12).

---

## Conformance

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL in this document are to be interpreted as described in RFC 2119.

Every normative requirement in this specification has a defined failure mode. Where a requirement can be violated, this document states what a conformant implementation does in response. The default response is to fail closed: refuse the operation rather than proceed with reduced guarantees.

While Status is Draft, some layer sections defer their bodies and say so in place. A deferred layer introduces no requirement of its own; its requirements bind through the explicit citations of section 12, each of which names a companion clause carrying its own defined failure modes. The promise above therefore holds for every requirement this document actually states, and the set of deferred bodies is visible in the text rather than implied.

---

## Table of Contents

1. Introduction
   1.1 The sibling specification stack
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
   2.7 The POLARIS declaration (normative body: POLARIS/1.0 sections 3, 4, and 6)
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
   4.8 Source surfaces and preservation
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
    13.1 The fifteen phases
    13.2 Individual track
    13.3 Organization track
14. Versioning and Governance
15. Registry
16. Reference Implementation
    16.1 A template is not a brain
    16.2 Enforcement roadmap
    16.3 Fixture peers are sibling repositories
    Appendix A: Schema directory
    Appendix B: Profile: individual
    Appendix C: Profile: organization
    Appendix D: Conformance test suite

---

## 1. Introduction

### 1.1 The sibling specification stack

Blueprint is the fourth member of a stack of four sibling specifications: ABR states what agents deserve, DERP what the runtime must provide, SAGA how an agent is represented, and the Blueprint how knowledge is held, governed, and exchanged. A Blueprint brain that hosts agent activity SHOULD run on a DERP conformant runtime and SHOULD identify its actors using SAGA identity.

The sibling stack and the protocol set of section 1.1.1 are distinct groupings, and this document names both to keep them distinct. The sibling stack relates this document to the specifications beside it. The protocol set is this document plus its six normative companions.

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

Each companion is a name first and an expansion second. The expansions are pinned here, once, and this table is the only place in this repository where they are canonical. Where any other text, including a non normative note under `design/`, expands one of these names differently, that text is stale and this table governs.

| Name | Expands to |
|---|---|
| POLARIS | Purpose, Obligations, Loyalties, Alignment, Refusals, Identity, Standards |
| DEFER | Delegated Envelopes, Fiduciary duty, Escalation, and Records |
| SPEAK | Signed Provenance Exchange for Attributable Knowledge |
| CONFIDE | Controlled Inference and Disclosure Governance |
| TRACE | Tooling Residue, Artifact Custody, and Evidence |
| RETAIN | Retention, Engagement, Thresholds, Admission, Identity, and Non-nesting |

The expansions are non normative. Each specification is identified by its name and version, never by its expansion, so no conformance result turns on the words in this table and no requirement may be derived from them. They are kept because a name whose expansion is remembered differently by every reader has stopped being one name.

### 1.1.2 Precedence

Precedence in this stack is asymmetric, and the asymmetry is normative.

POLARIS/1.0 holds the highest precedence for **forbidding** an act and no precedence for **permitting** one. A POLARIS refusal blocks an act every other document allows. No POLARIS element may permit an act any other document forbids, relax a requirement, satisfy a check, confer authority, or excuse a failure. See POLARIS/1.0 section 8.

Below POLARIS, the order is the Constitution, then this document, then the boundary and authority companions, then profiles, then implementation. Where two documents at the same level conflict, the more restrictive requirement applies.

Precedence within this stack does not cross a brain boundary. An agent brain evaluates its own POLARIS and the refusal floor inherited from the principal for the life of the engagement, and the more restrictive result governs. A principal holds no precedence over an agent brain's own declaration and cannot amend it. See RETAIN/1.0 section 4.3.

The combined effect is a ratchet. Constraints accumulate cheaply and are removed only by amendment with a stated cause and a recorded history. A governance system should be easy to tighten and slow to loosen.

### 1.2 Design principles

Sixteen principles govern the design. Their normative status is interpretive: where a requirement of this specification or a companion admits two readings, the reading consistent with these principles governs. A principle does not by itself create a conformance requirement; requirements live in the layer bodies, in section 12, and in the companions. Where a principle is load bearing before its owning layer body is written, the owning section restates it as a requirement with a failure mode: principles 3 and 8 are restated in section 6.

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

| Term | Definition |
|---|---|
| brain | A locally owned, policy governed, append only audited collection of plain text records constituted by a signed Charter (section 2) |
| owner | The single individual or organization the Charter declares; holder of the signing keys and of the final refusal |
| actor | Any identity that performs acts in a brain: the owner, another human, or an agent identity |
| tier | One of three cumulative conformance levels a brain claims in its Charter (section 12) |
| domain | A topology subtree holding the brain's knowledge about one counterparty, commitment, or standing area, declared by a domain manifest (4.2) |
| record | A plain text file governed by the frontmatter contract of Layer 3; the unit of knowledge |
| source | Preserved evidence: raw captured bytes held unmodified under a provenance record (4.8, 5.6) |
| work | The brain's own developing product, advanced through stages toward publication or export |
| stage | A named position in a work's lifecycle from capture to published; the reference stage set runs 0 through 10 |
| mid stage | The band in which a work's substance is complete and its belief gate is evaluated, before presentation and publication stages; stage 6 in the reference stage set |
| gate | A recorded approval bound to the SHA-256 of the approved bytes, void when the bytes change (section 6) |
| belief gate | The Layer 4 gate at which the owner records that a work's claims are claims the owner actually holds; approved at mid stage |
| preservation | The recorded property that a source's bytes match its provenance record's digest; structural at Tier 1 (4.8) |
| promotion blocker | A recorded condition that prevents promotion of a store or record while it is present (RETAIN/1.0 section 3.4) |
| consequence class | DEFER/1.0 section 6.1's classification of an act by the worst true statement about its reversibility, K0 through K4; K3 is irreversible external (something left the brain), K4 constitutional |
| ledger | The append only log families of Layer 6 |
| boundary | An enforced surface where content leaves or enters the brain: to a peer (SPEAK/1.0), to a model (CONFIDE/1.0), or into tooling (TRACE/1.0) |
| peer | Another brain, under a signed agreement |
| utterance | The signed transfer unit of SPEAK/1.0 |
| admission | The verified entry of an inbound artifact into quarantine: inside the brain's folder, outside the brain's knowledge (SPEAK/1.0 section 1.2) |
| adoption | The routing decision by which the owner moves admitted material into the brain proper; admission is not adoption |
| harness | An agent tool that can reach brain content (TRACE/1.0 section 2.1) |
| instantiation | A brain founded from a template by an owner's signature; conformance attaches to instantiations, never to templates (16.1) |

---

## 2. Layer 0: Charter

Layer 0 answers who this brain is, who owns it, and under what claim. It is the root of every verification chain: signatures verify against Charter keys, tier claims are read from the Charter, and a peer that cannot verify a Charter refuses exchange. Layer 0 binds at every tier (12.1).

### 2.1 Brain identity

A brain MUST be identified by a stable identifier declared in its Charter, of the form `brain:<handle>` (SPEAK/1.0 section 2). The identifier MUST NOT encode a filesystem location, a host name, or the owner's legal name, because each of those changes for reasons that have nothing to do with identity.

Exactly one Charter exists per brain, at a location the Constitution anchors (3.4). Two records claiming to be the Charter is a fail closed condition: every operation that requires Charter verification MUST refuse until the owner resolves which one governs. A folder with no resolvable Charter is not a brain and claims nothing.

### 2.2 Ownership and legal entity

The Charter MUST declare exactly one owner: an individual or an organization, with its legal name. One brain, one owner (RETAIN/1.0 section 4.1). Joint ownership is not representable, because a brain that two parties can sign for has no single refusal, and the refusal is the boundary.

An organization owner SHOULD declare its jurisdiction. An owner that also holds a SAGA identity SHOULD cross reference it, so that a human contributor and an agent contributor are the same kind of citizen at the boundary.

### 2.3 Keys and keyring

The Charter MUST declare the brain's public signing keys: for each key an identifier, algorithm, public key material, status (`active`, `retired`, or `revoked`), and creation date. The Charter MUST declare the location of the key revocation list. Private key material MUST NOT be stored within the brain's records or its version history; it lives in operating system key custody outside the tree. A private key found inside the tree is a credential artifact and the check goes red (TRACE/1.0 section 10.5).

A signature that verifies only against a key absent from the Charter, or present with status `revoked`, MUST be treated as no signature. A `retired` key verifies signatures made before its retirement and MUST NOT make new ones. Verification that cannot determine a key's status fails closed.

The owner holds the private keys. A brain whose signing key is held by another party is a domain of that party and MUST NOT be described as a brain (RETAIN/1.0, Conformance clause).

### 2.4 Lineage and chain of title

The Charter MAY carry lineage entries recording what this brain derives from: the origin work, the origin entity and owner, the relationship (`derivative-work`, `assignment`, `license`, or `successor`), and the rights basis. The lineage list is append only. A completed ownership transfer is one signed Charter revision appending a lineage entry, never a rewrite of prior entries, so that chain of title is an audit rather than an archaeology project.

A receiving brain MAY verify chain of title before admitting knowledge, and MAY refuse admission from a brain whose lineage it cannot verify.

### 2.5 Tier claim and layer declaration

The Charter MUST declare the tier the brain claims and the set of layers it implements (section 12). The claim is a floor for verification, not a boast: every check the claimed tier requires MUST pass, and a brain whose checks fail its own claim MUST surface that state rather than continue asserting the claim. A peer MAY refuse exchange with a brain below a required tier, which is what makes the claim load bearing.

A template, and any unsigned clone of one, claims no tier (16.1).

### 2.6 Inference posture declaration

The Charter MUST declare the brain's inference posture: whether an inference broker is operated, the default maximum custody class, and the anchored locations of the provider registry and the call ledger, per CONFIDE/1.0. A brain that performs no inference declares exactly that, and the declaration is what makes the absence checkable. Inference performed under no declared posture is an uncatalogued crossing: the check goes red and the operation MUST be refused where the brain's tooling mediates it.

The Charter likewise declares the tooling surfaces TRACE/1.0 requires: the harness registry, the artifact ledger and store, and the declared scratch surfaces, using the path anchors of 3.4 (see 4.6 and 4.7).

### 2.7 The POLARIS declaration

Layer 0 carries the brain's POLARIS declaration: exactly one purpose statement, at least one refusal with a decidable predicate, a total loyalty order, and the normative status of every declared element, per POLARIS/1.0 sections 3, 4, and 6. The normative body for element kinds, evaluation, amendment, and precedence effect is POLARIS/1.0 in its entirety; this document adds only the placement. The declaration is part of Layer 0 and is adopted at Phase 0, so that a brain has a reason before it has a structure, and every later layer is built under a declaration that can already refuse.

The one way precedence rule of POLARIS/1.0 section 8 governs the declaration's effect on every other layer, as stated in 1.1.2.

---

## 3. Layer 1: Constitution

Layer 1 answers which text governs. It binds at every tier (12.1).

### 3.1 The single governing file

A brain MUST have exactly one governing file, named in the Charter, and every other instruction surface in the brain MUST be subordinate to it: guides, agent instructions, plugin configuration, and generated registries. The Constitution states its own supremacy in its own text, so that a reader holding any one file learns which file wins.

Zero governing files is a brain with no law. Two is worse: each is a fork of authority, and every actor picks the one that permits more. Where two instruction surfaces disagree, the Constitution governs and the disagreement is a defect in the other surface. An operation that cannot determine which text governs MUST refuse.

### 3.2 Precedence and the registry rule

The Constitution MUST state the precedence order of 1.1.2 as it applies inside this brain, from the POLARIS declaration's power to forbid, through the Constitution itself, to profiles and implementation detail.

The registry rule: where the Constitution declares a vocabulary, index, or registry that is generated or mirrored elsewhere, the declaration is the source of truth and the generated copy is subordinate. When the two disagree, the generated copy is the bug. A check that discovers such a disagreement MUST report it and MUST NOT amend the declaration to match the copy, because a subordinate artifact that can amend its source has inverted the precedence this section exists to fix.

### 3.3 Prime directives

The Constitution SHOULD open with a small set of prime directives: the standing rules an operator or agent holds even when no check is running, restating the discipline of this specification in the brain's own voice. Directives do not replace checks. The Constitution MUST NOT present an advisory directive as enforced, because a rule believed enforced and actually advisory is where governance fails first; a directive whose enforcement exists names the check that enforces it.

### 3.4 Path anchors and portability

The Constitution MUST declare a set of named path anchors, and every path cited by a governed record or declaration MUST be expressed relative to an anchor. The anchor set MUST be sufficient to name locations outside the brain's own tree, because harness artifact roots live outside it and TRACE/1.0 section 4.2 declares roots using these anchors: at minimum the brain root, and anchors for the machine surfaces the brain's tooling touches, such as the repository root, the user home, application support, and temporary directories.

Anchors are what make a brain portable: a brain moved to a new machine or path re binds its anchors in one place and every governed reference survives. A machine absolute path in a record is a latent breakage: the schema check MUST report it, a capture surface MAY tolerate it, and it MUST NOT survive promotion.

### 3.5 Amendment

The Constitution MUST declare its own amendment procedure. Amendment is a constitutional act, K4 (DEFER/1.0 section 6.3): owner resolved, recorded as a decision record carrying the SHA-256 of the adopted bytes (8.6). An amendment that is not recorded has not happened: when the Constitution's bytes do not match the last adopted digest, verification fails and the brain treats the on disk text as unadopted until the owner resolves it. Superseded text is superseded by record, never silently overwritten.

---

## 4. Layer 2: Topology

Layer 2 answers where things live and what kind of surface each place is. The owner defines the taxonomy; this layer constrains only its edges. Layer 2 binds at every tier (12.1).

### 4.1 Taxonomy requirements

A conformant topology MUST distinguish four kinds of surface: knowledge surfaces (domains and the shared entity layer), source surfaces (4.8), system surfaces (4.5), and excluded surfaces (4.6, 4.7). Every path in the brain MUST be attributable to exactly one kind. A path attributable to none is an unclassified surface, and the enumeration sweep reports it (TRACE/1.0 section 5.1).

Within those edges the taxonomy is the owner's. This specification never names the owner's folders, only the properties the folders must declare.

### 4.2 Domains and domain manifests

A domain is the unit of knowledge topology: a subtree holding the brain's knowledge about one counterparty, one commitment, or one standing area. A domain is a relationship, not a topic, and the distinction matters at Layer 8: the personal brain's name for a counterparty is a domain, which is why a boundary can later be mounted inside one (10.2).

Every domain MUST carry a domain manifest: a record declaring the domain's name, its type, and its automation posture. A subtree without a manifest is not a domain, whatever its name suggests, and automation MUST NOT treat it as one.

### 4.3 Discovery over registration

Domains MUST be discoverable by enumeration of their manifests, and automation MUST discover domains by that enumeration rather than by a hand maintained central list. A central list maintained by hand is guaranteed to disagree with the tree eventually, and when it does, the brain's automation operates on the list's fiction. Where a generated index of domains exists for convenience, the manifests govern and the index is subordinate (3.2).

### 4.4 The shared entity layer

The topology MUST provide a shared entity layer: surfaces for people, organizations, concepts, and vocabulary that appear in more than one domain, so that a fact about an entity is written once and referenced everywhere it applies. A fact written twice will eventually be corrected once, and the uncorrected copy becomes the one an automation reads.

### 4.5 System surfaces

The topology MUST reserve system surfaces, distinct from knowledge surfaces, for the machinery this specification requires: identity, governance data, ledgers, conformance records, templates, and schema documentation. System surfaces hold records about the brain rather than knowledge in it. Knowledge queries and gates MUST NOT count system surfaces as knowledge, and a check that finds knowledge records living in a system surface reports it.

### 4.6 Harness artifact roots

Every artifact root of every harness operated against the brain MUST be declared, whether the root lies inside the brain's tree or outside it, per TRACE/1.0 section 4.2, using the path anchors of 3.4. A root inside the brain MUST additionally be declared as an excluded surface under 4.7. An undeclared root is the enumeration sweep's first finding, and the sweep failing to run on its declared interval is itself a red check.

### 4.7 Scratch surfaces and declared exceptions

A scratch surface is a path inside the brain that a harness writes and the brain does not govern as knowledge. Every scratch surface MUST be declared. A declared scratch surface MUST be excluded from knowledge: no gate may count it, no promotion may source from it without an explicit adoption decision, and version control SHOULD exclude it, with declared directive artifacts as the tracked exception (TRACE/1.0 section 10.1). Quarantine surfaces (Layer 8) are excluded the same way: inside the folder, outside the knowledge.

The declared exception list is a governed record. An exclusion that exists only in tool configuration, with no declaration, is an undeclared surface and the sweep reports it.

### 4.8 Source surfaces and preservation

The topology MUST distinguish source surfaces from work surfaces. A source is preserved evidence: the raw bytes as captured, never edited. A work is the brain's own developing product. The two MUST NOT share a surface, because an edit that is routine in a work destroys a source.

Preservation is a structural property, and it is the only gate like mechanic that binds at Tier 1. A preserved source consists of the raw artifact, unmodified, plus a provenance record binding the artifact's SHA-256, byte count, and capture date (5.6). A conformant brain verifies preservation by check: recorded digest equals present bytes. A source that fails the check is unpreserved, the check MUST report it, and promotion of anything derived from it MUST be refused while the check is red. Approval routing, belief evaluation, and stage machinery are Layer 4 mechanics and bind at Tier 2 (section 6); the preservation property binds at Tier 1 because without it nothing later is evidence.

---

## 5. Layer 3: Records

Layer 3 answers what a record must say about itself. It binds at every tier (12.1).

### 5.1 The frontmatter contract

Every record MUST carry structured frontmatter declaring, at minimum, its type and its identifier. Every type the brain uses MUST have a declared contract listing its required and optional properties and their value spaces; the contract is what the schema check enforces. A record that violates its type's contract fails the check. A type with no contract is itself the violation.

Fail closed applies at promotion, not placement (principle 2): a malformed note may sit in a capture surface, and it MUST NOT promote, satisfy a gate, or feed automation until it validates.

### 5.2 Controlled vocabularies

Every property whose values are drawn from a fixed set MUST have that set declared in exactly one vocabulary registry. One registry, because two registries disagree, and the property whose legal values depend on which file you opened has no legal values. A value outside the declared set fails the schema check. Extending a vocabulary is an ordinary recorded change; using an undeclared value is not an extension.

### 5.3 Identifiers and filenames

Record identifiers MUST be coordination free: mintable on any host without consulting any other host, timestamp plus entropy or equivalent, never the next free number (8.3). Identity lives in the record, not in its path: a move MUST NOT change an identifier, and references SHOULD cite identifiers rather than paths so that reorganization is not breakage. Filenames SHOULD derive from identifiers or titles by a declared rule, so that a filename collision is a minting error surfaced by check rather than a silent overwrite.

### 5.4 Derived state

State that can be computed from records MUST be declared as derived, and derived state MUST NOT be hand edited. When derived state and its sources disagree, the sources govern and the derived copy is regenerated; this is the registry rule of 3.2 applied to data. A decision or gate MUST cite records, not derived state, because a cache is not evidence.

### 5.5 Authorship

Every record MUST declare its authorship: `human`, `agent-drafted-human-approved`, or `agent`. The declaration matters at every boundary: a receiving brain, a model context, and a reader each have a legitimate interest in whether a claim was authored or generated.

A record with no authorship declaration MUST NOT promote past capture. Where an undeclared record must nevertheless be read, its authorship MUST be read as `agent`, never as `human`, because misattributing generated text to a human is the worse failure and the default must point away from it.

### 5.6 Derivation provenance and custody floors

A record derived from a source MUST name the source it derives from. The provenance record of a preserved source (4.8) is the anchor of every such chain: it binds the source identifier, the SHA-256 of the raw bytes, the byte count, the capture date, and the anchored location of the preserved artifact, and it is written once, at capture.

A record that carries a custody floor, whether admitted from a peer (SPEAK/1.0), processed under CONFIDE/1.0, or inherited through an artifact (TRACE/1.0 section 7.2), keeps that floor in its frontmatter, and every derivative record inherits the strongest floor among its inputs (CONFIDE/1.0 section 11). At Tier 1 the floor properties MUST be preserved and carried where present; enforcement at each crossing binds with the layer that owns the crossing.

---

## 6. Layer 4: Lifecycle

Layer 4 binds at Tier 2 (12.2). Body deferred; its requirements bind via the section 12 citations until this section is written. Layer 4 owns sources versus works, stages, approval gates, change authority, and the source hierarchy. Two rules are stated now because other sections depend on them and no other body carries them. First, approval binds to bytes: a gate approval records the SHA-256 of the approved artifact, computed after the approval metadata is written, and is void the moment the bytes change, the gate reverting to unapproved without human action (fail closed, principle 3). Second, no gate may depend on standing human attention: every gate MUST carry a TTL, a fail closed default, or a check that goes red when the gate is stale, because an unwatched approval queue rots into a pile of pending items nobody reads (principle 8). The preservation property exercised at Phase 4 is not a Layer 4 gate; it is the Layer 2 and Layer 3 structural property of 4.8 and 5.6 and binds at Tier 1.

---

## 7. Layer 5: Classification

Layer 5 binds at Tier 2 (12.2). Body deferred; its requirements bind via the section 12 citations until this section is written. Layer 5 owns sensitivity, visibility, consent to record, consent to process, the publication guard, and the export gate; the custody matrix is defined by CONFIDE/1.0 section 5 and inheritance by artifacts by TRACE/1.0 section 7. One rule is stated now: classification is enforced at exactly one boundary, by a check that terminates with a non zero status when a violation is present (12.2), and presence in any folder is never permission to publish (principle 2).

---

## 8. Layer 6: Ledger

Layer 6 answers what happened, in a form that cannot be quietly rewritten. Its internal families bind at Tier 1, its tooling families at Tier 2, and its boundary families at Tier 3 (8.1, 12.1).

### 8.1 Log families

A ledger is a set of append only log families. A log family is a sequence of entries sharing one schema, one surface, and one custody rule. Two groups are defined.

**Internal families** record what happened inside the brain:

| Family | Records | Defined by |
|---|---|---|
| Operations log | General events: checks run, sweeps, imports, amendments applied | This section |
| Decision family | One record per resolved decision, including genesis and adoptions | DEFER/1.0 section 12, and 8.6 |
| Inference call family | One entry per inference call attempt, completed or refused | CONFIDE/1.0 section 8 |
| Tooling families | Session anchors and the artifact ledger | TRACE/1.0 sections 6 and 8, and 8.7 |

**Boundary families** record what crossed: the outbound and inbound ledgers of Layer 8, one pair per peer, per SPEAK/1.0 section 11.

Tier scoping is explicit, because section 12.1 binds "the internal log families" at Tier 1. At Tier 1 the operations log and the decision family MUST exist and be operated, and the inference call family MUST exist whenever the brain performs any inference (CONFIDE/1.0 section 12.1). The tooling families bind at Tier 2 with TRACE/1.0 section 13.1; at Tier 1 their surfaces SHOULD exist empty, so that Tier 2 is an upgrade rather than a restructure. Boundary families bind at Tier 3.

### 8.2 Append only semantics

An entry, once written, MUST NOT be modified or deleted. A correction is a new entry that supersedes by identifier; a withdrawal is a new entry that tombstones. A family in which an entry has changed in place has stopped being a ledger: verification MUST treat the family as failed and MUST report it, and evidence drawn from a failed family is no evidence. In practice entries are new files or appended lines, and a version control diff showing modification of an existing entry is a red check.

### 8.3 Coordination free identifiers

Ledger entries MUST be minted coordination free: timestamp plus entropy or equivalent, mintable on any host with no knowledge of any other host. An implementation MUST NOT compute the next free sequence number, because two hosts computing it concurrently both get the same answer and one of them silently loses. The Phase 7 exit gate is the demonstration of this property under deliberate concurrency (13.1).

### 8.4 Hash chaining

An entry MAY carry the digest of the previous entry in its family. A family so chained is tamper evident end to end: rewriting any entry breaks every link after it.

Chaining is REQUIRED for every boundary family and for any family whose chain head a peer attests to, because a peer's attestation is only as good as the chain beneath it (SPEAK/1.0 section 11). For internal families chaining is RECOMMENDED and is not required at Tier 1: within one brain, the append only rule, version control history, and DEFER/1.0's two sided reconciliation provide the tamper evidence, and a Tier 1 brain has no peer to prove a chain to. A family that declares chaining MUST verify it, and a broken link fails the family (8.2).

### 8.5 Trusted time

Every entry MUST carry a UTC timestamp from a declared time source. At Tier 1 the local clock is an acceptable declared source, and monotonicity within each family MUST be checked: an entry timestamped before its predecessor is a red check, because it is either a clock fault or a rewrite, and both demand the owner's attention. No external time attestation is required below Tier 3. At Tier 3 the boundary families gain cross attestation structurally: a signed receipt is a peer's statement of when it observed an utterance, and reconciliation of the two ledgers is the time audit.

### 8.6 Decision records

The decision family is the brain's memory of who decided what. Every decision record MUST carry the consequence classification, the resolving actor, the resolution, and the digest of what was approved, per DEFER/1.0 section 12. Recording binds at Tier 1: DEFER/1.0 section 15.1 requires a classified, recorded decision from the first act, and the decision family is where those records live.

Two entries carry names. The genesis record is the family's first entry: the owner signed record of the brain's creation, classified K3 or above (RETAIN/1.0 section 10.2). Adoption records bind the Constitution and every other governing text to the SHA-256 of the adopted bytes, so that adopted is a checkable property of bytes rather than a memory (3.5).

### 8.7 Session anchors and the artifact ledger

The tooling families are defined by TRACE/1.0: session anchors by section 6, the artifact ledger by section 8. They are internal families and are held to the same append only and minting rules as every other family in this layer. Anchoring and sealing bind at Tier 2 (TRACE/1.0 section 13.1). At Tier 1 the surfaces SHOULD exist empty, and a Tier 1 brain that voluntarily anchors sessions records them in these families rather than inventing a parallel structure.

### 8.8 Protected artifacts and deletion as an entry

Deletion of a protected artifact is itself a ledger event: recorded, attributed, and refused to agent identities, per TRACE/1.0 sections 9.3 and 13.1, binding at Tier 2. The Layer 6 rule beneath it binds at every tier: no ledger entry is ever deleted (8.2), and an artifact that is absent with no deletion entry is detected by sweep as a vanished artifact, which is a red check.

---

## 9. Layer 7: Agency

Layer 7 binds at Tier 2 (12.2). Normative body: DEFER/1.0, with RETAIN/1.0 section 2 governing agent state thresholds and RETAIN/1.0 section 4.6 the separation of knowing and acting, per the subsection citations in the table of contents. Body deferred; its requirements bind via the section 12 citations until this section is written. The layer's two fixed points are already normative elsewhere and are only pointed to here: agents draft and the owner decides (principle 9), and no agent identity approves a gate (12.2).

---

## 10. Layer 8: Boundary

Layer 8 binds at Tier 3 (12.3). Normative bodies: SPEAK/1.0 for what crosses to another brain, CONFIDE/1.0 for what crosses to a model, TRACE/1.0 for what crosses into tooling, and RETAIN/1.0 sections 6 and 8 for the engagement of agent brains. Body deferred; its requirements bind via the section 12 citations until this section is written. The governing model is stated now because sections 12 and 16 depend on it: knowledge leaves a brain as a signed artifact and enters another by admission; the admitting brain owns its admitted copy and may pass signed artifacts onward under the same rule; brains relate as siblings under asymmetric agreements, never by nesting (RETAIN/1.0 section 3). Publishing a repository is not a crossing in this sense (12.1, 16.3).

---

## 11. Layer 9: Operations

Layer 9 binds at Tier 3 (12.3). Body deferred; its requirements bind via the section 12 citations until this section is written. Layer 9 owns host roles, serializers and advisory state, leases, continuous verification, the inference broker as a component, egress invariants, enumeration and retention sweeps, and the conformance self test a peer can execute. One rule is stated now because every tier's checks already rely on it: exactly one host owns each mutable state root, and authority bearing state is decided on a serializer, never on an eventually consistent sync, because a lock that sync can duplicate is worse than no lock.

---

## 12. Conformance Tiers

Each tier includes every requirement of the tier below it. A brain declares its tier in its Charter. A peer MAY refuse to exchange with a brain below a required tier.

### 12.1 Tier 1: Sovereign

A Sovereign brain MUST implement Layers 0, 1, 2, and 3, and MUST implement the internal log families of Layer 6 (8.1).

A Sovereign brain is owned, structured, and logged. It MUST NOT exchange knowledge with another brain: no utterance emitted, no record admitted. Exchange requires Layer 8 and binds at Tier 3, and an exchange performed by a brain claiming Tier 1 is an ungoverned crossing that voids the claim until the owner records the crossing and corrects the claim. Publishing a brain repository, or offering one as a template, is not knowledge exchange in the sense of SPEAK/1.0: nothing is admitted, no receiving brain signs, and no peer relationship is created. Exchange is admission: a signed artifact crossing under an agreement, admitted by a receiving brain that then owns its admitted copy (sections 10 and 16.3).

A Sovereign brain that performs any language model inference over its own content MUST additionally satisfy CONFIDE/1.0 section 12.1 for Tier 1: it MUST maintain an inference provider registry and MUST record every call in an append only ledger. Cataloging is required at the lowest tier, because a brain that cannot say what it has sent, and where, is not a brain the owner controls.

A Sovereign brain that is operated on by any agent harness MUST additionally satisfy TRACE/1.0 section 13.1 for Tier 1: it MUST register every harness with declared artifact roots, MUST enumerate undeclared roots, and MUST declare every scratch surface that a harness writes inside the brain folder.

A Sovereign brain MUST satisfy POLARIS/1.0 section 15.1 for Tier 1. It MUST declare exactly one purpose statement, at least one refusal carrying a decidable predicate, a total loyalty order, and the normative status of every declared element. Purpose is required at the lowest tier because a brain with no declared reason for existing has nothing against which to test its own amendments.

A Sovereign brain MUST satisfy DEFER/1.0 section 15.1 for Tier 1. It MUST declare its owner, define its roles, classify every act by consequence class before execution, and record every decision in the ledger. A Tier 1 brain is permitted to delegate nothing and may have the owner decide everything. What is not permitted is acting without a classified, recorded decision.

A Sovereign brain MUST NOT contain another brain within its records, and MUST NOT delegate the creation of a brain. These two prohibitions bind at every tier: they are absolute requirements of RETAIN/1.0's Conformance clause, stated in RETAIN/1.0 sections 3 and 10.1, and they admit no tier scoping. RETAIN/1.0's tiered conformance begins at Tier 2 (RETAIN/1.0 section 13.1), so a Tier 1 brain has no other RETAIN obligations: agent state thresholds presuppose the enforced classification of Tier 2.

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

### 13.1 The fifteen phases

Fifteen phases: twelve numbered 0 through 11, plus three inserted phases. Phases 8a and 8b extend Phase 8 with the DEFER/1.0 and RETAIN/1.0 mechanics, and 9a extends Phase 9 with agent brain engagement. The letter suffixes keep the original numbering stable in citations and curricula.

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

Phase and tier interact by one rule: a phase's exit gate exercises the mechanics of the layers its tier includes, and nothing above them. Two apparent contradictions are resolved explicitly.

**The Phase 4 preservation gate at Tier 1.** Approval gates are Layer 4 mechanics and bind at Tier 2. The preservation gate is not one of them. It is the Layer 2 and Layer 3 structural property of sections 4.8 and 5.6: raw bytes held unmodified under a provenance record, verified by a check that recorded digest equals present bytes. A Tier 1 brain enforces preservation by that check, and the check failing blocks promotion of anything derived from the source. No approval routing, belief evaluation, or stage machinery is required at Tier 1.

**Phase 7 at Tier 2 while Layer 6 binds at Tier 1.** The internal log families, append only semantics, coordination free minting, and decision records of sections 8.1, 8.2, 8.3, and 8.6 bind from Phase 0 at Tier 1: DEFER/1.0 requires a recorded decision from the first act, and section 12.1 requires the internal families. Phase 7 does not introduce the ledger. It proves the ledger under deliberate concurrency and hardens it, adding hash chaining on every family a peer will later attest to (8.4).

**The Phase 2 scaffold self test.** The exit gate's self test MUST assert, at minimum: every domain manifest is discoverable by the declared enumeration (4.3); every scratch surface is declared and excluded (4.7); no credential artifact is present in the working set or its history (TRACE/1.0 section 10.5); quarantine and scratch surfaces are excluded from knowledge; exactly one mutable state root exists; declaration time POLARIS rejections fire on seeded fixtures (POLARIS/1.0 section 15.1); and a harness record exists for the executing host wherever a harness operates (TRACE/1.0 section 4.1). The reference implementation carries the executable form of this test as data (section 16), and that form is the reference definition until this list is expanded at lock.

### 13.2 Individual track

*(to be written.)*

### 13.3 Organization track

An organization establishing a brain over existing material MUST import that material as sources. Imported material MUST NOT be admitted at a stage that implies review the organization has not performed.

*(to be expanded.)*

---

## 14. Versioning and Governance

Semantic versioning applies to the specification. MAJOR when a conformant implementation of the previous version ceases to be conformant. MINOR for backward compatible additions. PATCH for clarifications that do not alter conformance.

Substantive changes proceed by RFC with a 30 day comment period. MAJOR changes require a two thirds supermajority of listed authors.

**Draft status.** While Status is Draft, the 30 day comment period and the supermajority requirement above are suspended. The amendment channel while Status is Draft is the defect docket to RFCs loop operated through the reference implementation (section 16): a defect found in implementation is filed against the specification, routed as an RFC, and resolved by author ruling, with the resolving change recorded in the specification's history. Semantic versioning applies to Draft changes unchanged.

**Lock.** BLUEPRINT/1.0, POLARIS/1.0, DEFER/1.0, CONFIDE/1.0, TRACE/1.0, and RETAIN/1.0 lock together at the release of the d7r conformance tooling (section 16). SPEAK/1.0 is deferred and locks separately at a later version. At the lock commit, every cross specification citation in this document is converted to a digest pinned citation naming the cited specification's content digest at lock. Until lock, citations are by name, version, and section number, and a citation made stale by a companion's renumbering is a defect to file, not a silent breakage to tolerate.

---

## 15. Registry

Deferred; nothing is registered while Status is Draft. When written, this section will hold the identifier registry of the protocol set: the specification names and versions of 1.1.1, the schema identifier namespace of Appendix A, the requirement identifier prefixes minted into the specifications (BP, PL, DF, CF, TR, RT, SP), the stable failure class identifiers that conformance fixtures key against, and the reserved values of the controlled vocabularies this document defines. It will register identifiers, never brains: a brain is constituted by its signed Charter, and no central registration is required for a brain to exist or to claim a tier.

---

## 16. Reference Implementation

Two artifacts constitute the reference implementation. The **Governed Brain Starter** is a public template repository: a complete brain tree with a charter template, constitution, POLARIS element registry, topology, schemas, record templates, seeded fixtures, and a conformance register, published for instantiation. **d7r-cto** is the conformance tooling and register: the command line tool that executes the checks this specification family requires, the register that maps every requirement to its route and status, and the defect docket that is the Draft amendment channel (section 14).

### 16.1 A template is not a brain

Conformance is a property of a signed instantiation, never of a repository. The public repository is a reference template. It claims no tier, and no conformance language in it attaches to a clone. An unsigned clone claims nothing: its charter carries an unsigned sentinel, its checks fail closed on that sentinel, and every check that requires a signature is red until an owner signs. A brain comes into existence when an owner signs its Charter (Phase 0), and every conformance claim dates from that signature. A clone, mirror, or template instantiation that has not been signed is a folder holding a template, whatever its history says.

### 16.2 Enforcement roadmap

The signed reference instantiation claims Tier 1, enforced by the repository's checks as data and the d7r command line tool. The agent tiers follow on a planned roadmap: Tier 2 adds the d7r agent as the enforcement layer (broker, session anchoring, sealing, runtime gates), and Tier 3 adds a peer. Each is designed as an additive upgrade to the same tree, never a restructure, and no tier is claimed before its enforcement exists.

### 16.3 Fixture peers are sibling repositories

A fixture brain used to exercise SPEAK/1.0 MUST be a sibling repository. It MUST NOT live inside the reference brain's records, per the absolute non nesting requirement of RETAIN/1.0 (Conformance clause; section 3): a brain contained within another brain is not a fixture of exchange, it is a violation of the thing being tested. The federation model the fixtures exercise is the specification's own: a brain uses its tools to create signed artifacts; a sibling brain admits them and owns its admitted copies; and it may pass signed artifacts onward under the same rule. Sibling repositories under agreements, never nesting. Publication of the template repository itself is not exchange (12.1).

---

## Appendix A: Schema directory

Normative machine readable schemas live at `schema/v1/`, one JSON Schema per contract, each identified by a stable `$id` under `https://blueprint-spec.dev/schema/v1/`. The directory defines eighteen schemas:

| Schema | Contract | Defined by |
|---|---|---|
| `brain-charter` | The Layer 0 Charter: identity, owner, keys, lineage, tier and layer claim, inference and tooling declarations | This document, section 2 |
| `polaris-declaration` | The Layer 0 POLARIS declaration and its element kinds | POLARIS/1.0 |
| `role` | A named position that holds authority envelopes | DEFER/1.0 section 3 |
| `authority-envelope` | A bounded region of decision space on four axes | DEFER/1.0 section 4 |
| `delegation-grant` | A signed instrument conferring an envelope, chain terminating in a human signature | DEFER/1.0 section 8 |
| `decision-request` | The proposal of an act requiring a decision, classified before routing | DEFER/1.0 section 6 |
| `decision-record` | The Layer 6 entry for a resolved decision | DEFER/1.0 section 12 |
| `inference-provider` | One inference endpoint under one set of terms | CONFIDE/1.0 section 3 |
| `inference-authorization` | An owner grant binding actor, providers, and purposes | CONFIDE/1.0 section 4 |
| `inference-call` | One call ledger entry, hashes never prompt text | CONFIDE/1.0 section 8 |
| `harness` | One agent harness per host, with declared artifact roots | TRACE/1.0 section 4 |
| `session-anchor` | The brain owned ledger entry for one harness session | TRACE/1.0 section 6 |
| `artifact-seal` | One artifact ledger entry per sealed artifact, refusal, or deletion | TRACE/1.0 section 8 |
| `agent-brain` | The threshold classification of an agent state store | RETAIN/1.0 section 2 |
| `mandate` | The engagement instrument between principal and agent brain | RETAIN/1.0 section 6 |
| `peer-agreement` | The bilateral exchange contract | SPEAK/1.0 section 3 (body pending; see section 14 on SPEAK deferral) |
| `utterance` | The signed transfer unit | SPEAK/1.0 section 5 (body pending) |
| `receipt` | The listener's signed answer | SPEAK/1.0 section 6 (body pending) |

Two record schemas are specified here and are not yet authored in `schema/v1/`. The Phase 3 schema check requires both; authoring them is reference implementation work fed back into this directory.

**`record`**, the Layer 3 frontmatter contract for an ordinary record (5.1): required `type` (from the vocabulary registry) and `id` (coordination free, 5.3); required `created` (UTC) and `authorship` (5.5) for promotion past capture; optional `sensitivity`, `visibility`, custody floor properties (5.6), and gate properties, each validated against its controlled vocabulary where present. A domain manifest (4.2) is a record of type `domain-manifest` carrying an `automation` property, validated under this schema plus its vocabulary entries; it needs no separate schema.

**`source-provenance`**, the preservation record of 4.8 and 5.6: required source identifier, `sha256` of the raw bytes, byte count, capture date, capture method, and the anchored path of the preserved artifact; optional consent fields for third party material.

---

## Appendix B: Profile: individual

Non normative. A starting configuration for one person, maintained at `profiles/individual.md` in this repository. A profile is a configuration, not a requirement: every element is intended to be changed by the owner.

---

## Appendix C: Profile: organization

Non normative. A starting configuration for a company, team, or other legal entity, maintained at `profiles/organization.md` in this repository.

---

## Appendix D: Conformance test suite

Deferred. The conformance test suite ships as data in the reference implementation (section 16): assertions and seeded violation fixtures keyed to stable failure class identifiers, executed by the conformance tooling. This appendix will normatively enumerate the assertion set at lock.
