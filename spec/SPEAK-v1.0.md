# SPEAK: Signed Provenance Exchange for Attributable Knowledge

## Version 1.0

**Specification:** SPEAK/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 3, CONFIDE/1.0

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

SPEAK defines the transfer of knowledge between two Blueprint brains at Tier 3.

The following are explicit non goals, stated as normative prohibitions because they are the requirements an implementer is most likely to violate with good intentions.

- A brain MUST NOT hold a full copy of a peer brain. It holds only records it has admitted, plus its own knowledge about that peer.
- Two brains MUST NOT share a repository, a working tree, or any mutable state root. There is no shared mutable state and no mirroring.
- An inbound utterance MUST NOT set a gate, alter a classification, alter a sensitivity, alter decision text, alter identity, alter hierarchy, or write into a record body in the listener's brain.
- An agent identity MUST NOT authorize an export.
- A record classified `peer-confidential` MUST NOT be transferred onward to a third brain under any speech act.
- A listener MUST NOT process an admitted record at a custody class weaker than the floor declared in the authorizing agreement, MUST NOT weaken that floor, and MUST NOT evade it by deriving new content from the record and treating the derivative as unconstrained. See CONFIDE/1.0 section 11.
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

---

## 2 through 15

*(to be written. See `design/0000-workflow-and-spec-design.md` section 5 for the object definitions, the two guard condition sets, the state machines, ledger layout, and the git reference transport binding, and section 7 for the first implementation milestones.)*
