# CONFIDE: Controlled Inference and Disclosure Governance

## Version 1.0

**Specification:** CONFIDE/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 1
**See also:** TRACE/1.0

---

## Abstract

Inference is a boundary crossing. When a brain sends a record to a language model, the record leaves the owner's custody, is processed by machinery the owner may not control, may be retained for a period the owner did not choose, and returns as derived content whose origin must be recorded. That is the same shape as knowledge leaving for a peer brain, and it MUST be governed with the same seriousness.

CONFIDE defines how a brain catalogs inference providers, classifies them by custody, authorizes agents to use them, enforces limits at a single chokepoint, and records every call in an append only ledger. It defines five custody classes, a normative matrix binding record sensitivity to permitted custody, an inference broker as the sole holder of provider credentials, and a custody floor that travels with a record across brain boundaries so that the brain which authored a record retains control over where that record may later be processed.

The artifacts that agent tooling leaves behind when it performs inference on brain content, including session transcripts, derived memory, and file snapshots, are governed by a companion specification, TRACE/1.0. CONFIDE governs the crossing. TRACE governs the residue. A brain that conforms to only one of them can route every call to a resident provider and still ship the full text of every session to a vendor cloud.

CONFIDE is not a prohibition on third party inference. Inference is necessary. CONFIDE exists so that using it is a recorded, bounded, reviewable decision rather than an unexamined default.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Every normative requirement in this document has a defined failure mode. The default is to refuse the call and record a refusal.

---

## Table of Contents

1. Introduction
   1.1 Why inference is a boundary crossing
   1.2 The threat this addresses
   1.3 Relationship to Blueprint layers
2. Custody Classes
   2.1 The five classes
   2.2 Determining a provider's class
   2.3 Weakest link and provider chains
   2.4 Unknown is not a class
3. The Provider Registry
   3.1 Provider records
   3.2 Retention posture
   3.3 Evidence and expiry
   3.4 Model declarations and version pinning
   3.5 Status lifecycle
4. Inference Authorizations
   4.1 Structure
   4.2 Binding to an actor
   4.3 Purposes
   4.4 Redaction profiles
   4.5 Expiry and revocation
5. The Custody Matrix
   5.1 Normative defaults
   5.2 Raising a limit
   5.3 Consent to process is not consent to record
6. The Inference Broker
   6.1 Single chokepoint
   6.2 Credential isolation
   6.3 Refusal behavior
7. The Inference Check
   7.1 Conditions
   7.2 Failure classes
8. The Call Ledger
   8.1 Entry format
   8.2 Hashes, not prompts
   8.3 Optional prompt retention
   8.4 Hash chaining and audit
9. Output Handling
   9.1 Derived content provenance
   9.2 Stage ceiling on generated content
   9.3 Gates and generated content
10. Special Cases
    10.1 Embeddings and vector stores
    10.2 Prompt caching
    10.3 Tool use and agent loops
    10.4 Training and fine tuning on brain data
11. Custody Floors Across Brains
    11.1 Declaration in a peer agreement
    11.2 Travel and stickiness
    11.3 Violation as a boundary incident
12. Conformance
    12.1 Tier requirements
    12.2 Health invariants
    12.3 Self test
13. Versioning and Governance
    Appendix A: Provider schema
    Appendix B: Authorization schema
    Appendix C: Call record schema
    Appendix D: Custody classification worked examples
    Appendix E: Failure class registry

---

## 1. Introduction

### 1.1 Why inference is a boundary crossing

Blueprint Layer 8 defines two flows: output, where knowledge leaves for a peer or the public, and input, where external material arrives. Inference is a third flow with a distinct shape. It is a round trip. Data crosses out, and derived data crosses back, in a single operation that the owner initiated.

It differs from the other two flows in four ways that matter.

1. The counterparty is not a brain. It performs no admission check, keeps no reconcilable ledger, and signs no receipt.
2. Retention happens on infrastructure outside the owner's audit reach. The owner cannot verify deletion; the owner can only hold evidence of a commitment.
3. The returned content is derived work with no author. It requires provenance to a machine rather than attribution to a person.
4. The crossing is high frequency. A peer exchange might happen weekly. Inference happens hundreds of times a day, which means the control MUST be automatic or it will not exist.

That fourth point governs the design. A control that requires the owner to think before each call will be bypassed within a week. CONFIDE therefore places the decision at the level of the provider and the authorization, which are reviewed rarely, and makes the per call check mechanical.

### 1.2 The threat this addresses

The threat is not a malicious provider. It is the ordinary accumulation of unrecorded disclosure.

An agent is written to summarize notes. It works. It is pointed at a wider scope. Someone adds a folder. A record marked confidential enters that folder. Six months later nobody can answer the question "has this ever been sent to a third party, and if so, under what retention terms." That question MUST be answerable from the ledger, exactly, for every record, without recourse to memory.

A second threat is silent posture change. A provider is approved on the strength of a zero retention commitment. The commitment is tied to an endpoint, a contract tier, or a model version. Any of those can change without notice. A brain that recorded the commitment as a belief rather than as evidence with an expiry will not notice.

### 1.3 Relationship to Blueprint layers

CONFIDE is deliberately not a new Blueprint layer. Its enforcement is threaded into existing layers, because a control that lives in its own layer can be omitted while claiming conformance to the others.

| Blueprint layer | What CONFIDE adds |
|---|---|
| 0 Charter | The brain declares its default maximum custody class and whether it operates a broker. |
| 3 Records | `derivedVia` provenance on generated content; `authorship` extended. |
| 5 Classification | The custody matrix. Consent to process as distinct from consent to record. |
| 7 Agency | An agent charter MUST name its inference authorization. Agents MUST NOT hold provider credentials. |
| 8 Boundary | Inference is the third flow, with the third guard. |
| 9 Operations | The broker as a required component. Egress invariants. Evidence expiry sweep. |

---

## 2. Custody Classes

### 2.1 The five classes

A custody class answers one question: at the moment of inference, who has physical and administrative custody of the bytes, and who is in a position to retain them.

Classes are ordered from highest custody to lowest. Lower numbers are stronger.

**C0 Resident.** Inference executes on hardware the brain owner owns and physically possesses. Model weights are stored locally. The operation requires no network egress of record content whatsoever. Example: a quantized model running on the owner's laptop or a machine in the owner's home or office.

**C1 Enclave.** Hardware the owner controls administratively but does not physically possess. The owner controls the operating system, holds the disk encryption keys, and installed the model weights. Record content leaves the owner's premises but does not leave the owner's administrative control. Example: a dedicated colocated server, or a bare metal rental with owner managed full disk encryption.

**C2 Tenant.** Rented compute on shared infrastructure where the owner controls the software stack and supplies the model weights, but the infrastructure operator has technical access to memory, storage, or both. No model vendor is involved. Example: a GPU virtual machine on a general cloud provider running an open weights model.

**C3 Broker.** A third party operates both the model and the infrastructure, under a contract that includes enforceable retention terms, a prohibition on training, and a data processing agreement. The owner has contractual recourse and documentary evidence, and no technical control. Example: an enterprise or zero retention API tier from a model vendor.

**C4 Open.** A third party operates the model under consumer or default terms. Retention is long, unknown, or unbounded. Training on inputs is permitted, or is not clearly prohibited. Human review may occur. There is no data processing agreement specific to the owner. Example: a free or consumer tier chat interface or API key.

The distinction between C3 and C4 is documentary, not technical. The same vendor can be C3 on one endpoint and C4 on another. A provider record therefore describes an endpoint and a contract, never a company.

### 2.2 Determining a provider's class

A provider record MUST state its custody class, and the class MUST be justified by evidence recorded in the same record. An implementation MUST NOT infer a class from a vendor name.

### 2.3 Weakest link and provider chains

Where a provider routes to, subcontracts to, or falls back to another provider, the effective custody class of the composite is the weakest, that is the numerically highest, class of any component in the chain.

A provider that does not enumerate its subprocessors MUST be recorded with `subprocessors: unknown`, and its effective custody class MUST be C4 regardless of other claims.

A routing service that selects among providers at request time MUST be recorded as C4 unless the authorization pins a specific downstream provider and the response is verifiable against that pin.

### 2.4 Unknown is not a class

Where a required posture field is unknown, the provider MUST be treated as C4 for the purpose of the custody matrix. An implementation MUST NOT treat an unknown retention posture as favorable, and MUST NOT allow an omitted field to widen what a provider may receive.

---

## 3. The Provider Registry

### 3.1 Provider records

A brain that performs inference MUST maintain a provider registry. Each authorized provider MUST have a record, and every inference call MUST cite a `providerId` present in that registry.

Provider records live on a system surface of the brain and are ordinary Blueprint records, subject to the same schema, gate, and ledger requirements as any other. A provider record is authorized by the owner, not by an agent.

The normative shape is defined in `schema/v1/inference-provider.schema.json`.

### 3.2 Retention posture

A provider record MUST state, for both inputs and outputs: retention duration, whether the content may be used for training, whether human review may occur, whether prompt caching is enabled, the enumerated subprocessors, the jurisdictions in which content is processed or stored, and whether the owner holds an enforceable deletion right.

Each field MUST be one of a declared value or the literal `unknown`. There is no default.

### 3.3 Evidence and expiry

Every retention claim MUST be supported by at least one evidence entry recording the kind of evidence, a locator, the SHA-256 of the retrieved artifact, when it was retrieved, and when it expires.

Evidence MUST expire. An implementation MUST NOT accept an evidence entry with no `expiresAt`.

When the newest supporting evidence for a provider expires, the provider's status MUST degrade automatically to `probationary`. A `probationary` provider MAY receive records whose sensitivity is `none` and whose visibility is `public`, and MUST NOT receive anything else.

This requirement exists because a retention commitment is a document, not a memory, and because no control in a brain may depend on the owner remembering to revisit it.

### 3.4 Model declarations and version pinning

A provider record MUST enumerate the models it is authorized to serve, each with an identifier and a version. For C0, C1, and C2 providers, where the owner supplies the weights, the record MUST include the SHA-256 of the weights and the quantization, because the model is part of the owner's own supply chain.

An inference call MUST pin a declared model and version. If a response indicates that a different model or version served the request, the call MUST be recorded with verdict `failed` and failure class `model-substitution`, and its output MUST NOT be admitted into the brain.

### 3.5 Status lifecycle

```
draft -> authorized -> probationary -> authorized
                    -> suspended    -> authorized
                    -> prohibited   (terminal)
```

Only the owner may move a provider to `authorized`. Degradation to `probationary` is automatic on evidence expiry. `prohibited` is terminal and MUST cause every authorization referencing the provider to fail closed.

---

## 4. Inference Authorizations

### 4.1 Structure

An inference authorization is the owner's signed grant permitting a named actor to send a bounded class of records to a bounded set of providers for a bounded set of purposes. It is to inference what a peer agreement is to exchange, with the difference that it is unilateral, because the counterparty is not a brain and cannot countersign.

The normative shape is defined in `schema/v1/inference-authorization.schema.json`.

### 4.2 Binding to an actor

Every authorization MUST name exactly one actor, identified as a Blueprint Layer 7 actor identity. An actor with no authorization MUST NOT be able to perform inference. A Blueprint agent charter MUST name the authorization the agent operates under, and the enforcement hook MUST refuse to run an agent whose named authorization is missing, expired, or revoked.

### 4.3 Purposes

An authorization MUST enumerate permitted purposes. A purpose is a coarse category of operation, such as summarize, classify, extract, draft, translate, embed, or critique. The purpose is recorded on every call and is what makes the ledger answerable to questions of the form "what was this record ever used for."

An implementation MUST refuse a call whose purpose is not enumerated. An implementation MUST NOT provide a catch all purpose.

### 4.4 Redaction profiles

An authorization MAY require a named redaction profile to be applied before egress. Where a profile is required, the resulting redaction manifest MUST be hashed and the hash recorded on the call, so that an auditor can later establish what was removed without the ledger holding the removed content.

### 4.5 Expiry and revocation

Every authorization MUST have an `expiresAt`. An implementation MUST NOT accept an authorization without one. Revocation is immediate on the owner's signed notice, and in flight calls under a revoked authorization MUST be recorded with verdict `refused`.

---

## 5. The Custody Matrix

### 5.1 Normative defaults

The following matrix binds the sensitivity of a record to the custody classes it may cross into. These are the normative defaults for a conformant brain.

| Record sensitivity | C0 Resident | C1 Enclave | C2 Tenant | C3 Broker | C4 Open |
|---|---|---|---|---|---|
| `none`, visibility `public` | allow | allow | allow | allow | allow |
| `none`, visibility private or internal | allow | allow | allow | allow with unexpired evidence | prohibit |
| `personal` | allow | allow | allow with unexpired evidence | per record owner approval | prohibit |
| `third-party` | allow with processing consent | allow with processing consent | processing consent and unexpired evidence | prohibit | prohibit |
| `confidential` | allow | per record owner approval | prohibit | prohibit | prohibit |

Two properties of this matrix are intentional.

First, C4 is prohibited for everything that is not already public. A brain that wishes to use a consumer tier service may do so only with material it would publish anyway.

Second, C0 is permissive at every sensitivity, because a C0 provider produces no egress of record content. The matrix therefore creates a gradient in favor of owned inference infrastructure. That is deliberate: the strongest control available to a brain owner is to own the machine that performs the inference.

### 5.2 Raising a limit

A brain MAY raise a cell of the matrix, and MUST do so only by an explicit owner decision record that names the cell, the provider, the justification, and a review date. A brain MUST NOT raise a cell to permit `confidential` at C2, C3, or C4.

A brain MAY lower any cell freely. A lowered cell MUST NOT be raised again by an agent, by configuration inheritance, or by any means other than a new owner decision.

### 5.3 Consent to process is not consent to record

Where a record's sensitivity is `third-party`, Blueprint Layer 5 already requires consent before publication. CONFIDE adds a distinct requirement: consent to be recorded in a brain is not consent to be transmitted to an inference provider.

A `third-party` record MUST carry a separate processing consent state before it may cross into any custody class. Where processing consent is absent, unknown, pending, or withdrawn, the call MUST be refused with failure class `processing-consent-absent`.

This is the requirement most likely to be inconvenient in practice, and it is the requirement that most directly protects people who are described in a brain but do not own it.

---

## 6. The Inference Broker

### 6.1 Single chokepoint

A Tier 2 or Tier 3 brain MUST route all inference through a single broker component. The broker performs the inference check, writes the call ledger entry, and is the only component that contacts a provider endpoint.

This mirrors the Blueprint requirement that classification be enforced at exactly one boundary. Two enforcement points are equivalent to none, because they will diverge.

### 6.2 Credential isolation

Provider credentials MUST be held only by the broker, MUST NOT be stored in the brain folder, and MUST NOT be readable by any agent process. An agent obtains inference by asking the broker, never by holding a key.

This is what converts CONFIDE from a request into an enforcement. An agent that decides to ignore the policy has no credential with which to act on that decision.

### 6.3 Refusal behavior

The broker MUST fail closed. A broker that cannot read the provider registry, cannot validate an authorization, cannot determine a record's sensitivity, or cannot reach its own ledger MUST refuse the call rather than proceed.

A refusal MUST be recorded. An unrecorded refusal is indistinguishable from a call that never happened, which defeats audit.

---

## 7. The Inference Check

### 7.1 Conditions

The broker MUST refuse the call unless every one of the following holds.

1. An authorization exists that names this actor, is signed by the owner, and has not expired or been revoked.
2. Every requested `providerId` is present in the registry with status `authorized`, or with status `probationary` where the payload qualifies under 3.3.
3. The newest supporting evidence for the provider has not expired.
4. The provider's effective custody class, computed per 2.3, is at least as strong as the authorization's `maxCustodyClass`.
5. Every input record's sensitivity is permitted at that custody class by the matrix in 5.1, as amended by any owner decision under 5.2.
6. Every input record falls within a scope enumerated by the authorization.
7. Every `third-party` input record has processing consent granted.
8. No denied key appears anywhere in the assembled payload.
9. Where the authorization requires a redaction profile, the profile has been applied and its manifest hashed.
10. The call does not exceed the authorization's rate or payload size limits.
11. The requested model and version are enumerated in the provider record.
12. Any input record admitted from a peer brain carries a custody floor no weaker than the provider's effective class, per section 11.

### 7.2 Failure classes

Failure classes are stable identifiers recorded on refusals so that patterns are countable. The registry is normative and appears in Appendix E. The initial set:

`authorization-absent`, `authorization-expired`, `authorization-revoked`, `actor-unauthorized`, `provider-unregistered`, `provider-suspended`, `provider-prohibited`, `evidence-expired`, `custody-class-exceeded`, `sensitivity-exceeds-custody`, `scope-not-permitted`, `processing-consent-absent`, `denied-key-present`, `redaction-not-applied`, `rate-limit-exceeded`, `payload-too-large`, `model-undeclared`, `model-substitution`, `custody-floor-violation`, `ledger-unavailable`, `registry-unreadable`, `purpose-not-permitted`.

---

## 8. The Call Ledger

### 8.1 Entry format

Every call attempt, whether completed, refused, or failed, MUST produce exactly one append only ledger entry. The normative shape is defined in `schema/v1/inference-call.schema.json`.

### 8.2 Hashes, not prompts

The ledger MUST record the SHA-256 of the exact bytes transmitted, the byte count, and the identifiers and body hashes of the input records. The ledger MUST NOT record the prompt text or the response text.

This is a deliberate and load bearing restriction. A ledger that stores prompts becomes the largest single concentration of sensitive content in the brain, is read far more often than the records it describes, and is exactly the surface an auditor is granted access to. Recording hashes preserves the ability to prove what was sent, because the record bodies are themselves in the brain and can be rehashed, while removing the incentive to protect the audit log more carefully than the brain.

### 8.3 Optional prompt retention

An owner MAY enable prompt and response retention for a specific authorization. Where enabled, retained transcripts MUST be written to a separate surface, MUST carry their own sensitivity and visibility, MUST NOT be written into the ledger, and MUST be referenced from the ledger entry by hash only.

### 8.4 Hash chaining and audit

Call ledger entries MUST be hash chained by `prevEntrySha256` and MUST be signed. The chain head is what an auditor attests to.

The ledger MUST be able to answer, for any record in the brain, the complete list of calls in which that record was an input, with provider, custody class, model, purpose, actor, and timestamp for each. An implementation that cannot answer this query is not conformant.

---

## 9. Output Handling

### 9.1 Derived content provenance

Any content admitted into the brain that was produced by an inference call MUST carry `authorship: agent` and a `derivedVia` block naming the `callId`, `providerId`, `modelId`, and `custodyClass`.

Content derived from other derived content MUST carry the full chain, or a pointer to the earliest call in the chain. An implementation MUST NOT silently drop derivation provenance during editing.

### 9.2 Stage ceiling on generated content

Generated content MUST enter the brain at the earliest lifecycle stage. Model output is a source, not a work. An implementation MUST NOT admit generated content at a stage that implies review the owner has not performed.

### 9.3 Gates and generated content

Generated content MUST NOT satisfy a gate, and an inference call MUST NOT set, clear, or alter a gate. This follows directly from the Blueprint requirement that agents draft and the owner decides, and it closes the path by which a brain could launder a model's assertion into an approved position.

---

## 10. Special Cases

### 10.1 Embeddings and vector stores

Computing an embedding is an inference call and MUST be recorded as one, with purpose `embed`. An embedding inherits the sensitivity of its source record.

The store that holds embeddings is itself subject to the custody matrix, evaluated against the highest sensitivity it contains. A vector store hosted by a third party is at best a C3 surface and MUST be recorded as a provider.

This case is called out because it is routinely overlooked. An embedding is treated as a derived number and therefore as harmless, while in practice a corpus of embeddings plus a model is a meaningful reconstruction surface.

### 10.2 Prompt caching

Where a provider offers prompt caching, a provider record MUST state whether caching is enabled. Caching extends retention. A provider claiming `inputRetention: none` while caching is enabled MUST NOT be recorded as `none`, and an implementation that finds this combination MUST treat the retention posture as `unknown`.

### 10.3 Tool use and agent loops

Where an inference call grants the model the ability to invoke tools that read the brain, every resulting read is an input to that call and MUST be recorded as such. The check in section 7 MUST be evaluated against the union of all records read during the loop, and MUST be re evaluated before each subsequent turn.

An implementation MUST NOT evaluate the check once at the start of a loop that can widen its own scope. This is the most likely route by which a conformant looking implementation leaks a `confidential` record: the first turn is clean, and turn six retrieves something the check never saw.

### 10.4 Training and fine tuning on brain data

Using brain content to train, fine tune, or otherwise adapt a model is a distinct operation from inference and MUST have its own owner decision record. It MUST NOT be authorized by an inference authorization.

Where training occurs at custody class C2 or weaker, the resulting weights MUST be recorded as containing content at the highest sensitivity present in the training set, and MUST be governed accordingly. A model fine tuned on confidential records is a confidential artifact.

---

## 11. Custody Floors Across Brains

### 11.1 Declaration in a peer agreement

A SPEAK peer agreement MUST declare, per direction, the weakest custody class at which transferred records may be processed, and whether inference use is permitted at all.

```yaml
directions:
  outbound:
    maxCustodyClass: C1
    inferenceUse: permitted
```

This is the requirement that makes brain to brain exchange trustworthy. Without it, exporting a record to a peer means surrendering all control over where that record is subsequently processed, and every careful control in the speaker's own brain is defeated by one unconstrained peer.

### 11.2 Travel and stickiness

An admitted record MUST carry the custody floor declared by the agreement under which it arrived. The floor is a property of the record, not of the inbox, and MUST survive routing, adoption, editing, and derivation.

A receiving brain MAY strengthen a floor. A receiving brain MUST NOT weaken one, and MUST NOT weaken one by any indirect means, including by summarizing the record and treating the summary as unconstrained. Content derived from a floored record inherits the floor.

### 11.3 Violation as a boundary incident

Processing a record above its custody floor is a boundary incident, not a routine refusal. It MUST be recorded in both the call ledger and the boundary ledger, and the speaking brain MUST be notified by an `acknowledge` utterance carrying the incident reference.

A brain that detects a floor violation by a peer MAY suspend the agreement. The agreement SHOULD state the consequence in advance.

---

## 12. Conformance

### 12.1 Tier requirements

**Tier 1 Sovereign.** A brain that performs any inference MUST maintain a provider registry and MUST record every call in an append only ledger. It SHOULD apply the custody matrix.

Cataloging is required even at the lowest tier. A brain that cannot say what it has sent, and where, is not a brain the owner controls.

**Tier 2 Governed.** MUST route all inference through a single broker. MUST enforce the custody matrix. MUST isolate provider credentials from agents. MUST bind every agent charter to an authorization. MUST fail closed on expired evidence.

**Tier 3 Federated.** MUST declare custody limits in every peer agreement, MUST enforce inbound custody floors, and MUST report floor violations to the speaker.

### 12.2 Health invariants

A conformant brain MUST continuously check, and MUST report as unhealthy, each of the following.

- Network egress from a brain host to an endpoint not present in the provider registry.
- Any provider whose newest evidence expires within 30 days.
- Any authorization expiring within 30 days.
- Any provider credential readable from a path inside the brain folder.
- Any record carrying `derivedVia` with no corresponding call ledger entry.
- Any call ledger entry whose chain link does not verify.
- Any agent charter naming an absent, expired, or revoked authorization.

### 12.3 Self test

A Tier 2 brain MUST publish a self test that seeds a deliberate violation of each condition in section 7.1 and asserts that the broker refuses with the expected failure class. A control that has never been observed to refuse has not been demonstrated to work.

---

## 13. Versioning and Governance

As BLUEPRINT/1.0 section 14. Any change to the custody class definitions, or to the matrix in 5.1, is at minimum MINOR, and any change that widens a matrix cell is MAJOR.
