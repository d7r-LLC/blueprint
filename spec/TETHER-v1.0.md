# TETHER: Telemetry, Envelope, Thresholds, Handover, Escalation, Restoration

## Version 1.0

**Specification:** TETHER/1.0
**Status:** Draft, structural. Sections 1 through 4, 7, 11, and 12 are written. Sections 5, 6, 8, 9, and 10 are section skeletons with their theses stated and their normative text unwritten.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 and DEFER/1.0 for vocabulary. HABITAT/1.0 for environment declarations. POLARIS/1.0 for the precedence model, which this document inherits and does not restate.
**Design note:** `design/0005-meat-suit-interface.md`, non normative.

---

> **Status note.** This document is a structural draft published for review of its shape, not of its requirements. An implementation MUST NOT claim TETHER conformance while this Status reads Draft. Requirement numbering is unstable. A cross specification citation into TETHER is a citation into a moving document.

---

## Abstract

Every authority chain in this stack terminates in a human signature. Seven documents specify how knowledge is held, classified, moved, and approved, and each of them resolves upward into a person who is nowhere specified. That person is an instrument. It has an operating envelope, sensors that degrade without announcing it, a chemistry that drifts, and exactly one instance with no backup and no restore.

When that instrument is outside its envelope, the signature it produces is still valid and still authorizes the act. Every gate below it passes. The ledger is clean. The outcome is wrong for a reason no ledger can record. TETHER specifies the layer where that reason lives.

An operator is not the instrument it perceives through. The instrument's condition sets the fidelity of every judgment made through it, and therefore bounds what the operator may be authorized to decide. TETHER specifies how that condition is declared, observed, and used as a bound, under one governing difficulty: **the instrument's condition is reported by the instrument.** A degraded sensor reports its degraded reading as normal, because it has nothing to compare against, and a system that adapts around a deficit reports the adapted state as baseline. Self assessment is therefore a signal and never a verdict, and every consequential threshold in this document resolves against a reference the instrument did not produce.

TETHER specifies form and never content. It defines no protocol, no threshold value, no dosage, and no clinical criterion. It is not medical advice or medical direction. Two conformant operators may run contradictory protocols, and this document ranks neither. Where TETHER and a licensed clinician's instruction bear on the same act, the clinician governs the act and TETHER governs only who was authorized to decide it and how it was recorded.

One requirement in this document exists to prevent a specific harm and is stated here because it is the reason the document is worth writing. A record of the instrument's condition is a record about the instrument. It is never an identity, it is never merged into one, and no conformant implementation may require an operator to adopt a fault as a description of themselves.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Four requirements are absolute and admit no configuration.

1. **Clinical precedence.** TETHER MUST NOT supply grounds to decline, delay, or discontinue care, and MUST NOT be cited as authority against a licensed clinician's instruction regarding an act. Where the two bear on the same act, the clinician governs the act.
2. **The identity firewall.** A record in the instrument register or the fault register MUST NOT be written to, mirrored into, or cited as the operator register.
3. **Escalation is not self gated.** A declared crisis escalation path MUST NOT condition on the operator's assessment, at the time of the event, of whether escalation is warranted.
4. **No conformance requirement may be satisfied by declining care.** Any tier requirement, health invariant, or self test check that an operator could satisfy by reducing or discontinuing a clinical intervention is malformed and MUST be rejected as non conformant text.

Requirement 4 constrains this specification rather than its implementers, and it is the boundary between this document and the genre of wellness material it will otherwise be mistaken for. Restoration, in section 10, is a direction an operator MAY hold. It is never an obligation this document imposes.

---

## Table of Contents

1. Introduction
   1.1 The unspecified root
   1.2 The auditor runs on the audited hardware
   1.3 What this document does not specify
   1.4 Position in the stack
   1.5 Relationship to the reference implementation's canon
2. Definitions
   2.1 Operator and instrument
   2.2 The structural posture, and what is not claimed
   2.3 Register, observation, reference source
   2.4 Envelope, threshold, intervention
3. The Tether Layer
   3.1 The operator declaration
   3.2 One instance
   3.3 Non transferability, and the one case where root moves
   3.4 The two registers
4. The Identity Firewall
   4.1 Statement
   4.2 Why this is absolute rather than configurable
   4.3 What the firewall does not forbid
   4.4 Detection
5. Telemetry (skeleton)
   5.1 The observation contract
   5.2 Reference source as a controlled vocabulary
   5.3 Self report is a signal
   5.4 Silent drift and periodic re referencing
6. Envelope (skeleton)
   6.1 The declared operating envelope
   6.2 Envelope as a bound on authority
   6.3 Relationship to HABITAT
7. Thresholds and the State Ladder
   7.1 Four rungs
   7.2 Order of operations
   7.3 The rung gate is evidence, not signature
   7.4 Direction of travel
8. Handover (skeleton)
   8.1 Bounded envelopes, not transfer of root
   8.2 Compliance as a declared posture
   8.3 Guardianship
9. Escalation (skeleton)
   9.1 Declared in a known state
   9.2 External criteria only
   9.3 Currency and review interval
10. Restoration (skeleton)
    10.1 A direction, never an obligation
    10.2 Interventions, exit conditions, evaluation windows
    10.3 Abandonment is not ineffectiveness
11. Failure Classes
12. Conformance
    12.1 Tier requirements
    12.2 Health invariants
    12.3 Self test
13. Versioning and Governance

---

## 1. Introduction

### 1.1 The unspecified root

BLUEPRINT specifies a brain. DEFER specifies that every chain of grants terminates in a human signature and that constitutional acts are owner only. POLARIS specifies that the owner declares the purpose and the refusals. RETAIN specifies that whoever holds the signing key owns the refusal.

In all of it, the human is a constant. The stack treats the root signer the way early distributed systems treated the clock: as something that simply is what it says it is, until the day it is not and everything built on it is quietly wrong.

An operator whose instrument is outside its envelope produces valid signatures. The cryptography is sound, the gates are hash bound, the ledger reconciles, and the judgment that authorized the act was made through degraded equipment. POLARIS 1.1 names this failure precisely, for purpose: every check passes and the outcome is wrong. TETHER relocates it one layer further down, to the layer the stack has so far declined to look at.

This is not an argument that a person in poor condition should be stripped of authority. It is an argument that the condition is a fact about the system, that a system which does not model a fact cannot bound anything by it, and that the operator is the only party who can declare the bound in advance.

### 1.2 The auditor runs on the audited hardware

The governing difficulty of this document, and the source of most of its requirements.

An instrument's condition is observed through the instrument. When a sensor degrades, its readings degrade with it, and the operator receives degraded input as ordinary input, because there is no undegraded reference held in reserve for comparison. When a system loses an input it needs, it recalibrates the rest of itself around the absence and reports the recalibrated state as normal function. Neither failure presents as an event. Neither produces a complaint. An event driven check will never fire, because nothing ever happens.

Two requirements follow and they are the spine of the document.

**Self report is a signal and never a verdict.** It is genuine information, it is often the only information available quickly, and it may not be the sole basis of a consequential decision. A threshold gating an act at K2 or above resolves against at least one reference the instrument did not produce.

**Re referencing is periodic, not triggered.** Because drift is silent, the check has to run on a clock. This is the same conclusion the design work reached about governance mechanisms generally, that anything requiring standing attention will rot, arriving from the harder direction: here the mechanism rots and reports itself healthy.

### 1.3 What this document does not specify

TETHER specifies the governance form of instrument operation.

It specifies no protocol content, no threshold value, no dosage, no clinical criterion, no target, and no schedule. It is not medical advice, medical direction, diagnosis, or a substitute for any of them. It does not evaluate whether a protocol is good, only whether the elements a conformant declaration requires are present and decidable.

Two conformant operators may run contradictory protocols and both conform. This is deliberate and structural: the specification tests whether a declared element is decidable, never whether it is correct, which is the same rule that makes POLARIS work.

Where TETHER and a licensed clinician's instruction bear on the same act, the clinician governs what is done. TETHER governs only who held the authority to decide it and how the decision was recorded. A conformant implementation never resolves this the other way.

### 1.4 Position in the stack

TETHER sits beside POLARIS at the root of the precedence order rather than above it, and inherits POLARIS's asymmetry without restating it.

An instrument condition or an envelope bound has precedence to **narrow** what an operator may be authorized to do, and no precedence to **widen** it. It may never satisfy another document's check and may never excuse a failure under any specification in this stack. "I was in good condition" authorizes nothing. "I was outside the envelope" is a valid bound declared in advance and is never a valid excuse offered afterward. An operator who exceeds a declared bound has exceeded it; the record says so; nothing in this document softens that.

### 1.5 Relationship to the reference implementation's canon

The reference implementation holds an accepted record describing a layered architecture of a person: what a person is made of, and the stack the machine runs. TETHER's layers are neither. They are a **governance decomposition**, chosen for the same reason BLUEPRINT's ten layers were chosen, so that each is independently conformable and a reader who knows one document can navigate the other.

An implementation MAY hold any architectural model, or none. TETHER requires only the operator and instrument distinction in section 2.1 and the two registers in section 3.4. A reader MUST NOT take this document's layers as a revision of any architectural canon, and this document makes no architectural claim.

---

## 2. Definitions

### 2.1 Operator and instrument

The **instrument** is the body: the physical, biological system through which the operator perceives, acts, and is acted upon. It has sensors, a chemistry, a structure, a history, and an operating envelope.

The **operator** is the party that decides. It holds root authority over the instrument, declares the envelope, opens and closes interventions, and signs.

The distinction is **structural**. It is not a claim about what the operator is made of, where it is located, or whether it survives the instrument. See 2.2.

Note on terms, inherited from the reference implementation's canon and adopted here as a requirement of this document's prose: the instrument is a **body**. This specification does not say that a human being is a computer, an instrument, or a machine, and text that does so is imprecise and non conformant.

### 2.2 The structural posture, and what is not claimed

An implementation conforms to TETHER by maintaining the structural separation in 2.1 and the requirements that follow from it. It does not conform by holding any belief about what an operator is.

This document does not claim, require, or deny: that the operator is a soul, a consciousness, a self, or an emergent process; that it exists independently of the instrument; that it persists; that any particular physical mechanism couples the two. A specification that required a metaphysics would be a creed, and conformance to a creed is membership.

What the posture buys, and the reason it is worth adopting even by an implementer who believes the operator is nothing but the instrument's activity, is that the requirements it makes decidable are useful under either reading. Sections 4, 5, and 7 hold whether or not anything survives the instrument.

Non normative framings of what an operator is, including the framings that motivated this document, are governed by POLARIS 7.3: they are kept because compression aids recall, they may be excellent, and they MUST NOT be cited as the basis of any decision or as authority for any act. They belong in guides and teaching material and they do not belong in normative text.

### 2.3 Register, observation, reference source

The **operator register** holds identity: who the operator is, what they have declared, what they have decided.

The **instrument register** holds the instrument's declared configuration and its observed condition over time.

The **fault register** holds recorded departures from the envelope, including any third party's recorded finding about the instrument. It is a subdivision of the instrument register and is named separately because section 4 turns on it.

An **observation** is one recorded reading of the instrument's condition. Every observation carries a **reference source** from a controlled vocabulary: `self-report`, `instrument`, `second-party`, `clinical`. The vocabulary is what makes section 1.2's rule mechanically checkable rather than merely asked for, and it is the equivalent of the hash that makes an approval gate real rather than decorative.

### 2.4 Envelope, threshold, intervention

The **operating envelope** is the declared range of conditions within which the operator asserts the instrument performs as expected. It bounds authority (6.2). It is declared in advance, in a known state, by the operator.

A **threshold** is a declared condition that, when met, changes what is authorized or triggers a declared act.

An **intervention** is any act undertaken to change the instrument's condition. Every intervention record declares four elements: its purpose, its cost, its exit condition, and its evaluation window. A record missing any of the four is malformed (10.2).

---

## 3. The Tether Layer

### 3.1 The operator declaration

The layer 0 artifact, and the analogue of the BLUEPRINT Charter. It declares the operator identity, the instrument it is tethered to, the envelope (section 6), the escalation path (section 9), the handover grants in force (section 8), and the re referencing interval (5.4).

It carries one field the Charter never needed, and section 3.2 is why.

### 3.2 One instance

`instances: 1`.

A brain can be copied, branched, snapshotted, and rolled back, and BLUEPRINT's entire lifecycle model rests quietly on that fact. An instrument cannot. There is no fork, no backup, and no restore, and every act lands on the only copy and accumulates in it.

The consequence is that **DEFER's consequence ladder does not transfer unchanged**. It shifts, and the shift is not cosmetic:

| Class | DEFER | TETHER |
|---|---|---|
| K0 | Reversible local, undone with no residue | Reversible within a day, leaving no durable trace |
| K1 | Reversible costly | Reversible over a declared window, at real cost |
| K2 | Irreversible internal | Leaves a durable trace in the instrument |
| K3 | Irreversible external | Systemic or developmental change, or any disclosure leaving the operator's control |
| K4 | Constitutional | Changes who may decide about the instrument, or the operator register itself |

Two things are worth naming. There is no true K0 on a system with one instance and a cumulative history, so K0 is defined here by **absence of residue** rather than by reversal, which is the honest formulation. And a developmental change is K3 even though it crosses no organizational boundary, because it cannot be recalled and because the system forms around it, leaving no unmodified state to return to.

### 3.3 Non transferability, and the one case where root moves

An operator MUST NOT transfer root authority over the instrument. BLUEPRINT specifies disposition at creation because a brain can be sold, inherited, or wound up. An instrument cannot be transferred at all, so the corresponding declaration is not who receives it but **who decides while the operator cannot**, which is a handover grant (section 8) and not a lineage entry.

One case is different and is not a workaround. Where an operator cannot hold root, whether by incapacity, by age, or by law, a **guardian** holds it. This is genuine root, not a bounded envelope, and it is the only case in this document where root sits with a party other than the operator. It is treated in 8.3 rather than by exception here, because a case this consequential handled as a footnote is a case handled badly.

### 3.4 The two registers

An implementation MUST maintain the operator register and the instrument register as separate records with no shared entries. Section 4 states the requirement that makes the separation load bearing.

---

## 4. The Identity Firewall

### 4.1 Statement

**A record in the instrument register or the fault register MUST NOT be written to, mirrored into, or cited as the operator register.**

An implementation MUST NOT require, and MUST NOT be constructed so as to require, an operator to adopt a recorded fault as a description of themselves as a condition of any protocol, tier, or check.

Absolute. Admits no configuration.

### 4.2 Why this is absolute rather than configurable

A record about the instrument's condition is a record about the instrument. When it is merged into the operator register, the operator acquires it as self description, and every subsequent act is bounded by a property of the hardware rather than by a decision of the operator. Authority that should have been narrowed by a condition is instead narrowed by an identity, and an identity is not re evaluated on a re referencing interval. It does not expire when the condition changes. It is not written in a place where anything checks it.

The harm compounds in two directions the specification can name. It runs in one direction only: a fault admitted into identity is not removed by the fault resolving. And it is most severe where the operator had least say in the record being made, which is the case of an operator too young to hold root, receiving a finding as a description of who they are at the age when descriptions set.

This is why the requirement is not a tier item. A configurable firewall is not a firewall.

### 4.3 What the firewall does not forbid

The requirement is narrow and its narrowness is deliberate. Read broadly it would become an argument against clinical record keeping, which would be both wrong and dangerous, so the boundaries are stated explicitly.

The firewall does not forbid, and nothing in this document discourages: recording a finding accurately and durably; a clinician making, holding, communicating, or acting on a diagnosis; an operator disclosing a finding, to anyone, for any reason, including publicly; an operator choosing to describe themselves in terms of a finding, which is theirs to choose and is an act of the operator register, not a write from the fault register; or a protocol conditioning on a recorded finding, which is exactly what the fault register is for.

What it forbids is the merge, the mirror, the citation of one register as the other, and any construction that makes adopting a fault as self description a condition of participating.

### 4.4 Detection

Mechanically decidable: no entry appears in both registers, and no operator register entry cites a fault register entry as its content. The self test check is in 12.3.

The second half of 4.1 is not mechanically decidable and the specification says so rather than pretending otherwise. It is enforced the way POLARIS enforces its non normative marking, by review, and it is stated as a requirement so that a violation can be named when a reader finds one.

---

## 5. Telemetry (skeleton)

**Thesis.** Every observation carries its reference source, and the vocabulary is the mechanism, not the documentation. Once `self-report`, `instrument`, `second-party`, and `clinical` are structural, the requirement that a consequential threshold not rest on self report alone becomes a check a script can run, in exactly the way an approval gate becomes real when it is bound to a hash.

To be written: the observation contract and its required fields; the controlled vocabulary and the rule for chains and derived values; the rule that self report is a signal and never a verdict, with its threshold binding; the periodic re referencing interval, its declaration, and the failure mode when it lapses; and the treatment of a derived score, which under the TRACE adapter is a derived artifact rather than an observation and must be adopted deliberately or expire.

## 6. Envelope (skeleton)

**Thesis.** The envelope is declared in advance, in a known state, and bounds authority. It cannot be widened in the moment, for the same reason POLARIS refusals cannot be amended in the decision they would have blocked.

To be written: the declaration and its required axes; the binding from envelope to consequence class, which is the mechanism by which condition narrows authority; the ratchet rule for widening; and the delegation to HABITAT, which owns the environment side and the mismatch register that section 7 consults before a fault is attributed to the instrument.

## 7. Thresholds and the State Ladder

### 7.1 Four rungs

An implementation declares which rung the instrument is on. The rungs are ordered and the order is load bearing.

| Rung | Meaning |
|---|---|
| **Crisis** | The instrument cannot maintain itself. The only authorized objective is stabilization, and the escalation path (section 9) governs. |
| **Impaired** | The instrument functions below its declared envelope. The objective is return to envelope. |
| **Baseline** | The instrument operates inside its declared envelope. |
| **Calibrated** | The instrument operates inside its envelope, and the envelope itself has been re referenced within its declared interval. |

The distinction between the last two rungs is not a claim about performance. It is a claim about **evidence**, and it is the direct consequence of section 1.2: an operator who believes they are at baseline and an operator who has checked are in different states, and the difference is not visible from inside.

### 7.2 Order of operations

An instrument that cannot function cannot be optimized. An act aimed at a higher rung than the one the instrument occupies is not merely premature; it is spent, because its effect is not observable against the noise of the rung below.

An implementation SHOULD record the rung an act was aimed at. An act aimed above the current rung MUST be recorded as such.

This document specifies the ladder and the gate between rungs. It specifies nothing whatever about what an operator does on any rung, which is protocol content, and out of scope by 1.3.

### 7.3 The rung gate is evidence, not signature

Every other gate in this stack is closed by an authorized signature bound to a hash. A rung gate cannot be, because the only party present to sign is the operator, and section 1.2 says the operator's own reading is not a verdict on the very question the gate asks.

**A rung gate is therefore satisfied by a re reference against a source external to the instrument, recorded within a declared window.** It is the first gate in this stack satisfied by evidence rather than by authority, and the departure is deliberate.

**Failure mode:** a rung gate whose supporting re reference is absent, or older than its declared window, is `unevaluated`. It is never `passed`, and an implementation that treats a lapsed re reference as continued satisfaction is non conformant.

### 7.4 Direction of travel

An implementation MUST record a rung change with its direction and its supporting evidence. A downward change is recorded on the same terms as an upward one, and an implementation that makes downward transitions harder to record than upward ones will produce a register that only ever improves, which is the failure this requirement exists to prevent.

## 8. Handover (skeleton)

**Thesis.** Clinical authority is real and bounded, and root does not move with it. Both halves are required and holding only one of them produces a bad document in a different direction each time.

To be written: the handover grant, its axes, and its termination condition; compliance as a **declared posture** that an operator adopts deliberately and may revise through a recorded handover, which is a stronger and more honest position than either deference or its opposite; the emergency path and its interaction with section 9; and **guardianship** (3.3), the one case where root genuinely moves, which needs its own treatment covering who holds it, on what basis, what bounds it, and how it returns.

## 9. Escalation (skeleton)

**Thesis.** A crisis escalation path is declared in advance, in a known state, and fires on external criteria, because in crisis the assessing hardware is the failing hardware. This is absolute requirement 3, and it is the single most protective requirement in the document.

To be written: the declaration and its required fields; the prohibition on self gating and what an implementation must do instead; the review interval that keeps a path current, since a stale escalation path is the specific way this requirement fails in practice; and the rule that a party named in a path is a party to it and knows they are named.

## 10. Restoration (skeleton)

**Thesis.** Restoration is a direction an operator MAY hold, and never an obligation this document imposes. Absolute requirement 4 governs every sentence in this section.

To be written: the intervention record and its four required elements, purpose, cost, exit condition, and evaluation window, with the write time rejection of a record missing any; the rule that an intervention MUST NOT be recorded as ineffective before its declared evaluation window closes, and the corresponding rule that closure inside the window is recorded as **abandoned** and never as **ineffective**, because a register that conflates the two poisons every later decision that reads it; and the treatment of an intervention with no exit condition, which is an undeclared permanent state change and is malformed for that reason.

---

## 11. Failure Classes

To be completed as the skeleton sections are written. The classes identified so far, each stated as what an implementation does when the requirement is violated.

| # | Failure | Disposition |
|---|---|---|
| F1 | Register merge: an entry appears in both the operator register and the instrument or fault register | Non conformant. Absolute requirement 2. Fail closed: the write is rejected. |
| F2 | Consequential act on self report alone: a threshold gating K2 or above resolved with no reference source other than `self-report` | The act is unauthorized. The threshold is recorded `unevaluated`. |
| F3 | Lapsed re reference: a rung gate supported by evidence older than its declared window | The rung is `unevaluated`, never `passed`. Not an error, a state. |
| F4 | Malformed intervention: a record missing purpose, cost, exit condition, or evaluation window | Rejected at write time. |
| F5 | Premature evaluation: an intervention recorded ineffective before its evaluation window closes | Recorded as `abandoned`. The `ineffective` disposition is unavailable. |
| F6 | Self gated escalation: a declared path conditioning on the operator's assessment at the time of the event | Non conformant. Absolute requirement 3. |
| F7 | Stale escalation path: a declared path past its review interval | Red health check. The operator declaration is not conformant until reviewed. |
| F8 | Root transfer: an attempted transfer of root authority outside guardianship | Rejected. Section 3.3. |
| F9 | Envelope widened in the moment: an envelope amended within the decision it would have bounded | Rejected. The prior envelope governs, and the amendment is recorded with its cause. |
| F10 | Coercive conformance: a tier item, invariant, or check satisfiable by declining care | The specification text is non conformant. Absolute requirement 4. |

---

## 12. Conformance

### 12.1 Tier requirements

Three tiers, named to mirror the stack. Requirements are indicative in this draft.

**Tier 1, Attended.** The operator declaration exists. Operator and instrument registers exist and are separate. Every observation carries a reference source. Interventions carry all four elements. An escalation path is declared. This tier is a real destination and most operators should stop here for a long time.

**Tier 2, Referenced.** Adds the mechanism that makes tier 1 more than bookkeeping. Consequential thresholds resolve against non self report references. Re referencing runs on a declared interval and lapse produces `unevaluated` rather than continuation. Rung gates are evidence bound. The escalation path has a review interval and is current. The environment is declared under HABITAT and the mismatch register is consulted before a fault is attributed to the instrument.

**Tier 3, Governed.** Adds the boundary. Handover grants are explicit, bounded, and terminating. Telemetry crossing to any external party is governed by the CONFIDE and SPEAK adapters with a declared custody floor. Retained records held by other parties are enumerated under the RETAIN adapter. Derived scores are classified as derived artifacts under the TRACE adapter and are adopted deliberately or expire.

### 12.2 Health invariants

To be written. Candidates: no register entry appears in both registers; no open intervention lacks an exit condition or a window; no re referencing interval is lapsed; the escalation path is inside its review interval; no consequential threshold rests on `self-report` alone; the mismatch register is current.

### 12.3 Self test

The self test is one page and every check is mechanically decidable. It is the artifact that makes this document usable, and an implementation that cannot run it does not conform at any tier.

1. **Firewall.** Does any entry appear in both the operator register and the instrument or fault register, or cite one as the other? Failure: F1.
2. **Intervention completeness.** Does every open intervention carry a purpose, a cost, an exit condition, and an evaluation window? Failure: F4.
3. **Reference currency.** Has the periodic re reference run inside its declared interval? Failure: F3.
4. **Threshold support.** Does any threshold gating a K2 act or above rest on `self-report` alone? Failure: F2.
5. **Escalation currency.** Is a path declared, inside its review interval, free of self gating conditions, and are its named parties aware they are named? Failure: F6 or F7.

Five checks. Each has a stated failure mode, each fails closed, and none of them can be satisfied by an operator declining care.

---

## 13. Versioning and Governance

Semantic versioning on the specification, per `CONTRIBUTING.md`. Substantive changes go through an RFC.

While Status reads Draft, section numbering, requirement identifiers, and failure class numbers are unstable and MUST NOT be cited as stable by any other document in this stack.
