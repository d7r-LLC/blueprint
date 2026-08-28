# SPEAK: Signed Provenance Exchange for Attributable Knowledge

## Version 1.0

**Specification:** SPEAK/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 3 or Tier 3 candidate (section 1.4), CONFIDE/1.0 section 11 (custody floor profile)

---

> **Status note.** SPEAK locks at a later version than the rest of the BLUEPRINT/1.0 family. The other six specifications lock at d7r-cto release; SPEAK does not, because sections 2 through 15 are unwritten and locking a skeleton would freeze the wrong text. Until those sections are written, every SPEAK row in a conformance requirement register is volatile: the current count reflects only this document's introduction and will grow substantially at writing time. An implementation MUST NOT claim SPEAK conformance, and MUST NOT treat a register row citing an unwritten section as stable, while this document's Status is Draft. A cross-spec citation into SPEAK is a citation into a moving document and is pinned only at SPEAK's own lock.

---

## Abstract

A human speaks a word and the word becomes part of another mind. Neither mind is merged, neither mind is copied, and the listener decides what to do with what it heard.

SPEAK defines that operation between two brains. The transfer unit is an **utterance**: a signed, classified, provenance bearing envelope carrying one or more records, authorized by a bilateral peer agreement and answered by a signed receipt. Every utterance is recorded in the speaker's append only outbound ledger and, on admission, in the listener's append only inbound ledger, and the two ledgers reconcile.

Every agreement declares a custody floor: the weakest inference custody class at which the transferred records may later be processed. The floor travels with the record, may be strengthened by the listener, and may never be weakened. Without it, exporting a record surrenders all control over where it is subsequently sent, and every control in the speaker's own brain is defeated by one unconstrained peer.

SPEAK is not a synchronization protocol. Two brains never share a repository, a working tree, or a mutable state root. An utterance transfers a copy. On admission the listener becomes the owner of its copy, and the two copies legitimately diverge.

Admission is not adoption. A verified utterance enters a quarantine surface inside the listener's folder and outside the listener's knowledge. Only a routing decision, made by the listener's owner, moves it into the brain proper.

---

## Conformance

RFC 2119 keywords apply as described in that document.

---

## Table of Contents

1. Introduction
   1.1 Scope and non goals
   1.2 The two guards
   1.3 The ownership chain
   1.4 Tier 3 candidacy
   1.5 Quarantine is one state
   1.6 Normative paths
2. Identity
   2.1 Brain identifiers
   2.2 Keys, keyring, and rotation
   2.3 Revocation
   2.4 Relationship to SAGA identity
3. Peer Agreements
   3.1 Structure
   3.2 Directional scopes
   3.3 Classifications
   3.4 Custody limits and inference use
   3.5 Retention and revocation
   3.6 Signing and content addressing
4. Classification
   4.1 The four classes
   4.2 Mapping to brain sensitivity
   4.3 Redaction manifests
   4.4 Onward transfer prohibition
   4.5 Custody floors (CONFIDE/1.0 section 11)
5. The Utterance
   5.1 Envelope
   5.2 Speech acts
   5.3 Records and payload hashing
   5.4 Provenance
   5.5 Export gate binding
   5.6 Canonicalization and signature
6. The Receipt
7. The Bundle
   7.1 Container layout
   7.2 Checksum manifest
   7.3 Detached signature
   7.4 Verification order
8. The Export Check
9. The Admission Check
10. State Machines
    10.1 Speaker
    10.2 Listener
    10.3 An acknowledgement is not a confirmation
    10.4 Supersession and retraction
11. Ledgers
    11.1 Boundary mounting
    11.2 Entry format and hash chaining
    11.3 Reconciliation
    11.4 Audit
12. Transport Bindings
    12.1 Requirements on a transport
    12.2 Binding: filesystem
    12.3 Binding: git reference compare and swap
    12.4 Prohibited transports
13. Failure Classes
14. Conformance and Self Test
15. Versioning and Governance
    Appendix A: Agreement schema
    Appendix B: Utterance schema
    Appendix C: Receipt schema
    Appendix D: Canonical JSON test vectors
    Appendix E: Bundle format

---

## 1. Introduction

### 1.1 Scope and non goals

SPEAK defines the transfer of knowledge between two Blueprint brains at Tier 3, including a Tier 3 candidate performing the exchange that confers the tier (section 1.4).

The following are explicit non goals, stated as normative prohibitions because they are the requirements an implementer is most likely to violate with good intentions.

- A brain MUST NOT acquire a peer brain's records through any path other than per utterance admission. It holds only records it has admitted, plus its own knowledge about that peer. The prohibition on holding a full copy of a peer brain is not a size test and has no threshold; it is enforced structurally by this clause together with the shared state prohibition below, because no bulk path exists when every record enters one authorized utterance at a time.
- Two brains MUST NOT share a repository, a working tree, or any mutable state root. There is no shared mutable state and no mirroring.
- An inbound utterance MUST NOT set a gate, alter a classification, alter a sensitivity, alter decision text, alter identity, alter hierarchy, or write into a record body in the listener's brain.
- An agent identity MUST NOT authorize an export.
- A record classified `peer-confidential` MUST NOT be transferred onward to a third brain under any speech act.
- A listener MUST NOT process an admitted record at a custody class weaker than the floor declared in the authorizing agreement, MUST NOT weaken that floor, and MUST NOT evade it by deriving new content from the record and treating the derivative as unconstrained. See CONFIDE/1.0 section 11. For mechanical checking, derivation is bounded operationally: content produced by an inference call whose context contained the record inherits the floor, and the CONFIDE/1.0 call ledger is the witness. Derivation outside a witnessed inference call remains prohibited, and is enforced by the owner's duty rather than by a check.
- A `retract` MUST NOT be implemented as a deletion by the listener. It produces a tombstone, and the agreement's retention policy governs the remainder.

### 1.2 The two guards

Every brain has exactly two enforced crossings.

```
        OUTBOUND                              INBOUND
   record in brain                       bundle arrives
        |                                     |
  [ export check ]                     [ admission check ]
  hash bound gate                      signature bound
        |                                     |
  Out ledger entry                      In ledger entry
        |                                     |
  bundle emitted                       staged in quarantine
        |                                     |
  awaits signed receipt                routing decision by owner
        |                                     |
  reconciled                           adopted
```

The outbound guard answers "may this leave." The inbound guard answers "did this arrive intact and permitted." Neither answers "should this become knowledge." That question is answered only by the receiving owner, in a routing decision that is an ordinary record in the receiving brain.

### 1.3 The ownership chain

The governing model for this specification, in the author's words:

> "My brain is my owned knowledge. I use the d7r tools to create signed artifacts that are included in the sibling repo, who then owns that knowledge, and on and on."

Four principles follow, and every section of this document is subordinate to them.

- **Emission is signing.** Knowledge leaves a brain only as a signed artifact. An unsigned transfer is not speech under this specification; it is leakage.
- **Admission transfers ownership of the copy.** On admission the admitting brain owns its admitted copy. It may hold it, route it, revise its own copy, and pass signed artifacts onward under its own agreements, subject only to the classification and custody floor that traveled with the record.
- **Provenance chains hop by hop.** Each transfer cites its authorizing agreement and its origin. A record two hops from its origin carries a chain of signed hops, not a claim of direct acquaintance.
- **Siblings never nest.** Brains are sibling repositories. No brain lives inside another brain's records, working tree, or state root, and no fixture, template, or agent brain is exempt.

One boundary clause follows from the ownership chain and is stated now because RETAIN/1.0 depends on it. The agreement's retention block governs only the boundary disposition of admitted copies, that is, the tombstone and freeze semantics on `retract` and on revocation. All other retention inside a brain is governed by RETAIN/1.0, because the admitting brain owns its copy. An agreement MUST NOT impose retention obligations on anything beyond the copies it authorized, and where an agreement clause and RETAIN/1.0 both speak to a store that is not an admitted copy, RETAIN/1.0 governs.

### 1.4 Tier 3 candidacy

BLUEPRINT/1.0 Phase 9 exits by performing one complete SPEAK round trip, and Tier 3 requires SPEAK conformance. Read literally, a brain would need Tier 3 to speak and would need to speak to reach Tier 3. The resolution is a candidate state.

A brain at BLUEPRINT/1.0 Tier 2 that has scaffolded its boundary and holds a signed peer agreement is a **Tier 3 candidate**. A Tier 3 candidate MAY perform its first exchange, and every requirement of this specification binds it during that exchange exactly as it binds a Tier 3 brain. Completing Phase 9's exit gate, one round trip of emit, admit, receipt, and reconcile, confers Tier 3. A candidate that fails the round trip remains a candidate; nothing downgrades, because nothing was yet conferred.

Wherever this document or its header says Tier 3, read Tier 3 or a Tier 3 candidate performing the exchange that would confer it.

### 1.5 Quarantine is one state

The word quarantine names exactly one thing in this specification: the staging surface, inside the listener's folder and outside the listener's knowledge, where a verified and admitted utterance waits for the owner's routing decision. Nothing else is called quarantine.

An utterance that fails any admission check is not quarantined. It is **impounded**: held in a distinct surface for audit together with its named failure class, answered by a signed `rejected` receipt, and never eligible for routing. Impoundment exists so that a failed verification leaves evidence rather than vanishing, and an impound surface MUST NOT be the quarantine surface, because a routing decision made over an impounded utterance would adopt unverified content. Where section 10's listener state machine provides an owner override out of impoundment, the override is a logged admission act by the owner, and the utterance then enters quarantine like any other admitted utterance.

A receipt verdict therefore has two values, `admitted` and `rejected`. A verdict `quarantined` is not defined, because every admitted utterance is quarantined by definition and the verdict would carry no information.

### 1.6 Normative paths

Two paths are fixed now, ahead of sections 2 and 11, so that implementations and the companion specifications may cite them stably.

- The key revocation list is `System/Identity/krl.json`, relative to the brain root. Every signature verification MUST consult it, and a key's presence on it MUST fail verification closed, regardless of what section 2.3 adds when written.
- The boundary mounts inside the brain that owns it. Where the brain names the counterparty with a domain, the mount is `<domain>/Boundary/`. For every other peer the default mount is `Boundary/<peer-handle>/` at the brain root, one directory per peer, holding that peer's record, agreement, and Out and In ledgers. An implementation MAY mount elsewhere only where its Charter declares the mount, because a boundary a peer cannot locate is a boundary a peer cannot audit.

---

## 2 through 15

*(to be written, with two exceptions. Section 12.4 below is written early because its failure mode is the first one implementers meet in practice, and section 1.6 fixes two paths that sections 2.3 and 11.1 incorporate when written. See `design/0000-workflow-and-spec-design.md` section 5 for the object definitions, the two guard condition sets, the state machines, ledger layout, and the git reference transport binding, and section 7 for the first implementation milestones.)*

The following bindings are fixed in advance so that writing time does not reopen them.

- Section 4 MUST define all four classifications, including `brain-portable`, and MUST state the sensitivity mapping so that the classification ladder is monotone: each step from `public` toward `peer-confidential` admits more sensitive material under stricter carriage, and no mapping row inverts that order.
- Section 6 and section 10.3 MUST distinguish the Receipt from the `acknowledge` act. The Receipt is the transport level answer to one utterance, emitted by the admission machinery, and carries a verdict. The `acknowledge` act is an utterance in its own right, carrying substantive content such as a custody floor incident reference under CONFIDE/1.0 section 11.3, and it passes the export check like any other utterance.
- Appendix C and the receipt schema MUST carry the two value verdict vocabulary of section 1.5.
- Appendix E MUST designate a single integrity authority for the bundle: the detached signature over the per file checksum manifest is the authority, any merkle root is an index for partial verification and MUST NOT be treated as an alternate authority, and the signed byte stream is defined exactly, never as an unordered concatenation.
- Section 14 MUST define the attestation behind `requiredTier`. A tier claim is a property of a signed instantiation, attested by its signed conformance register; a peer MAY require the register digest in the agreement and MAY run the self test against the counterparty before signing. Self assertion without an attestation artifact does not satisfy `requiredTier`.

### 12.4 Prohibited transports

A transport carries immutable bundles between two brains that share nothing. Anything that makes the two brains writers of one surface is not a transport, whatever it is called. The first real world failure mode here is not an attacker; it is a convenience feature.

- A live file synchronization service (Obsidian Sync, iCloud Drive, Dropbox, Google Drive, OneDrive, Syncthing, or any service that continuously replicates file state between machines) MUST NOT be used as a transport, and a synchronized folder MUST NOT contain any boundary surface: no bundle in flight, no ledger, no agreement, no chain head, no quarantine. Such a service is a shared mutable state root entered by accident: it merges concurrent edits silently, delivers partial states with no transactional boundary, offers no compare and swap, and turns the prohibition of section 1.1 into a default configuration.
- A shared repository or shared working tree that both brains write MUST NOT be used as a transport. This does not prohibit the git reference binding of section 12.3, where a transfer repository carries only bundles and receipts under create only references and either side may prune it after reconciliation. The distinction is that neither brain's state root lives there and no reference is ever rewritten.
- A collaboratively editable surface (a shared live document, a shared database, a shared vault) MUST NOT be used as a transport, because an utterance is a signed immutable artifact and a surface any party can mutate after signing cannot carry one.
- A transport MUST deliver the bundle bytes themselves. A mutable reference, such as a link to a live document, is not a bundle, and an admission check run against bytes that can change after verification has verified nothing.

Discovery of a prohibited channel between two brains is a boundary incident. Each brain MUST refuse to emit over the channel, MUST NOT admit from it, and MUST record the incident in its boundary ledger. Fail closed: knowledge that cannot travel over a conformant transport does not travel.
