# KIT: Kind, Integrity, Tenure

## Version 1.0

**Specification:** KIT/1.0
**Status:** Draft, structural. Sections 1 through 13 are written. Section 2.13, the item class vocabulary, is a labelled skeleton with its thesis stated and its enumeration unsettled. No other section is a skeleton.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**License:** Apache 2.0
**Requires:** TETHER/1.0 for operator, instrument, register, observation, reference source, the intervention record and its four required elements at TETHER 2.4, and the shifted consequence ladder. HABITAT/1.0 for provisioning party, for the undeclared class direction of HABITAT section 3, for the attribution routing of HABITAT section 7, and for HABITAT absolute requirement 2 and failure class H5. DEFER/1.0 for meters, the meter declaration of DEFER 5.4, consequence classification, and decidable predicates. TRACE/1.0 and CONFIDE/1.0 for the data surface, the artifact classes, the custody classes, and the provider registration bridge at TRACE 11.1. SPEAK/1.0 and RETAIN/1.0 for the relationships K-A1 and 3.4 route off the inventory. POLARIS/1.0 for precedence inherited through TETHER and not restated, and directly for the motto rule and PL-04 at 2.12, the obligation asymmetry of POLARIS 5.2 at 8.4, and the dead refusal problem of POLARIS 4.5 at 10.2.
**Design note:** `design/0005-meat-suit-interface.md`, non normative.

---

> **Status note.** Structural draft, published for review of its shape. An implementation MUST NOT claim KIT conformance while this Status reads Draft. Requirement numbering, section numbering, and failure class codes are unstable, and a cross specification citation into KIT is a citation into a moving document.

---

## Abstract

TETHER specifies the operator and the instrument it perceives through. HABITAT specifies the environment the instrument runs in. KIT specifies the third thing: what the operator interposes between the environment and the instrument.

Two sentences carry the document.

**An item is external, and it has a custody holder who may not be the operator.** Every property that makes an item different from a capability follows from that: it can be taken, it can be withheld, it can expire, it can be provisioned by an employer, a vendor, a household, or a subscription, and none of those events is an act on the instrument or a decision of the operator.

**A sensing item that has drifted is worse than no item, because it converts unknown into confidently wrong.** No item is the honest state. A drifted item supplies a number, the number is precise, the precision is read as accuracy, and the operator now holds a belief about the instrument that is worse grounded than the belief they held before they bought anything.

The second sentence generalizes into the structural finding that makes this document worth writing independently of anyone asking for it. TETHER's spine is that a consequential threshold resolves against a reference source other than `self-report`, and TETHER 2.3 offers `instrument` as one of the alternatives. **Without KIT, that requirement is defeated by purchase.** An operator acquires an uncalibrated device, its output is tagged `instrument` because a device produced it, the non self report requirement is satisfied, and a gate opens on a number nobody calibrated. Nobody lies. No gate fails. The reading is self report grade confidence wearing an `instrument` label, and the attack is reference source laundering. KIT section 6 is what makes the word `instrument` in TETHER 2.3 mean something.

KIT specifies form and never content. It states no quantity, no threshold, no target, no schedule, and no recommended loadout. Two conformant operators may hold wildly different kits and KIT ranks neither.

---

## Conformance

RFC 2119 keywords apply as described in that document.

### Inherited absolutes

TETHER's four absolute requirements are inherited unchanged and are NOT restated here. Each is named in one line, with an explicit inherits unchanged marker.

1. **Clinical precedence.** Inherits TETHER absolute requirement 1 unchanged.
2. **The identity firewall.** Inherits TETHER absolute requirement 2 unchanged. An RFC generalising TETHER 4.1 from an enumerated list of registers to any register holding a record about the instrument, its equipment, or its capabilities is a deliverable of this work, drafted and not applied. KIT states no second copy of the firewall, and section 10.1 is a narrower and separate requirement about the fault register rather than a restatement.
3. **Escalation is not self gated.** Inherits TETHER absolute requirement 3 unchanged. No item, item state, or loadout state conditions, gates, delays, or substitutes for a declared escalation path.
4. **No conformance requirement may be satisfied by declining care.** Inherits TETHER absolute requirement 4 unchanged. **This inherited absolute is the source of the coercive and protective split in section 3.5.** The split is derived from it rather than freshly invented: a rule that generates pressure toward carrying fewer items is a rule an operator could satisfy by discontinuing a clinically directed one, so those rules are labelled and held out of reach of such an item, while rules that only narrow what may be claimed from an item continue to apply.

### New absolutes

Three requirements are absolute and admit no configuration. Each carries a statement of what it does not forbid, per the drafting requirement below.

**K-A1. A party is not an item.** An item MUST be an object. Any identity that can hold a register, can consent, or can be an operator MUST NOT be declared as an item, placed in a slot, counted against a budget, or written to the inventory register.
**Failure:** the declaration is rejected at write time and is routed to the DEFER adapter as a handover grant, to the SPEAK adapter as an agreement, or to the RETAIN adapter as an engagement, according to the relationship declared.
**What this does not forbid:** recording that the operator works with a coach, a clinician, or an assistant. The relationship is recorded. It is recorded somewhere other than an inventory.

**K-A2. No stated measurement values.** KIT MUST NOT state the value of any meter, bound, threshold, target, schedule, or recommended loadout for any slot, meter, or budget.
**Failure:** the specification text is non conformant and MUST be rejected in review, in the disposition HABITAT absolute requirement 2 applies to a normative value.
**What this does not forbid:** an operator declaring their own budget values, which section 8 requires them to do. K-A2 constrains this specification, not its implementers. **It also does not forbid a structural cardinality that carries no measurement**, such as the requirement that a slot hold at most one item (8.1), or that a budget declare at least one meter that is not `currency` and that every declared bound carry at least one windowed aggregate ceiling (8.2). The discriminator is mechanical: text is a stated value when an operator could satisfy it by adopting a number this specification supplied, and a cardinality supplies no number an operator meets, only the shape a declaration must have before it means anything.

**K-A3. KIT does not depend on QUEST.** KIT MUST NOT cite, require, or condition any requirement on a QUEST element. QUEST MAY cite KIT. An implementation MUST be able to reach full KIT conformance while declaring no capability, node, or quest.
**Failure:** a KIT requirement citing a QUEST element is non conformant specification text and MUST be rejected in review. The check is mechanical against the specification text: no KIT requirement's satisfaction depends on the existence or the state of a capability record, a node, a prerequisite edge, or a quest.

**The procedure, named, so that the check is runnable rather than asserted.** The requirements in KIT that mention a capability at all are exactly these: **2.2** (the named capability a kind is declared against), **4.1** (the kind declaration), **4.2** (loss posture), **5.1** (confirmation), **5.2** (departure disposition), **5.4** (supply failure attribution), and **10.2** (the unused item). **Each of the seven resolves against the item record alone, and none of them reads, writes, or conditions on a capability record, a node, a prerequisite edge, or a quest.** 2.2 states the reason: within this document a named capability is an opaque operator declared label with no structure, no state, and no record, and KIT never reads a capability record. **KIT assigns no capability state anywhere.** The transition of a dependent capability when an item departs is QUEST 7.4's, and naming that is routing rather than dependency.
**Failure of the procedure:** a KIT requirement mentioning a capability and absent from the list above is unreviewed specification text and MUST be rejected in review until it is added to the list and shown to resolve against the item record alone. An implementation that resolves any KIT requirement by reading a capability record is non conformant, and the requirement is re resolved against the item record alone.
**What this does not forbid:** naming QUEST as the document that governs capabilities, which sections 1.2 and 1.3 do. That is a routing statement telling a reader where a non item goes, and it creates no dependency, because KIT's requirements are unchanged whether or not any QUEST record exists.

### Drafting requirements binding on this document

**Every absolute carries its boundary.** Each absolute requirement introduced by KIT MUST be accompanied by an explicit statement of what it does not forbid.
**Failure:** an absolute lacking its boundary statement is an incomplete section and MUST NOT be marked complete, under the repository rule against sections completed with unwritten parentheticals. TETHER 4.3 proved this necessary and stated why: read broadly, an absolute becomes an argument against something the document never meant to touch.

**Fail closed states name what is missing.** Every fail closed state name MUST name what is missing and MUST NOT name a deficiency in the operator. `unconfirmed`, `unprovisioned`, `unknown`, `unused`, `unattributed`, `unevaluated`, `over-equipped`, and `out-of-scope` are conformant. `deficient`, `failed`, `inadequate`, and `substandard` MUST NOT be used as state names.
**Failure:** a register offering a deficiency named state is non conformant, and specification text defining one MUST be rejected in review.

**Every section is labelled coercive or protective.** Every **top level** numbered section header in this document carries the label, so that the split of section 3.5 is checkable against the specification text rather than against an implementer's judgement. A subsection inherits its parent's label unless it carries one of its own. A section stating no requirement about an item carries the label `neither` and states why.
**Failure:** an unlabelled top level section cannot be evaluated under 3.5 and MUST be treated as coercive, which is the stricter handling and holds it out of reach of a clinically directed item. A section labelled `neither` while stating a requirement about an item is mislabelled and MUST be corrected in review. Where a header label and the enumeration in 3.5 disagree, the stricter governs until the disagreement is corrected, per 3.5.

---

## Table of Contents

1. Introduction (protective)
   1.1 What an item is, and the attack this closes
   1.2 Custody is the membership test
   1.3 Severability, and why the dependency runs one way
   1.4 Position in the stack
   1.5 `instrument` is a reserved word
2. Definitions (protective)
   2.1 Item
   2.2 Kind
   2.3 Class
   2.4 Job
   2.5 Slot and loadout
   2.6 Custody holder and provisioning party
   2.7 Confirmation interval, calibration interval, calibration reference
   2.8 Loss posture and replacement latency
   2.9 Budget and meter
   2.10 The inventory register
   2.11 The fail closed naming convention
   2.12 The closed game vocabulary
   2.13 The class vocabulary and its extension rule (skeleton)
3. Membership, and the Boundary with TETHER (protective)
   3.1 The custody test, normatively
   3.2 The removal test, and the boundary with TETHER 10
   3.3 The `fitted` class
   3.4 A party is not an item
   3.5 Clinical direction, and the coercive and protective split
4. Kind: Substitution and Amplification (4.1 to 4.3 protective, 4.4 coercive)
   4.1 The declaration
   4.2 Loss posture is required on every substituting item
   4.3 Permanence is a declared state, never a defect
   4.4 Trial items and exit conditions (coercive)
5. Tenure: Custody, Confirmation, and Loss (protective)
   5.1 Confirmation is periodic, because loss produces no event
   5.2 Leaving the loadout carries a disposition
   5.3 Replacement latency and loss exposure
   5.4 A supply failure is not an instrument fault
6. Integrity: Calibration and the Sensing Item (protective)
   6.1 The calibration declaration
   6.2 No self calibration
   6.3 Output outside the interval is unknown
   6.4 The reading is not an observation, and the write is rejected
   6.5 An uncalibrated sensing item closes no gate
   6.6 Observations citing an item
7. Job, and Off Job Application (protective)
   7.1 The job predicate
   7.2 Off job application is recorded, never forbidden
   7.3 Classification is on the target, never on the item
8. Slots, Budgets, and Contention (coercive, except 8.1 which is protective)
   8.1 Slots
   8.2 The budget declaration
   8.3 Budgets are the operator's
   8.4 Over equipment is reported and never blocked
   8.5 No stated values
9. The Data Surface (protective)
   9.1 Enumeration is required
   9.2 A computed number is a derived artifact, not an observation
   9.3 Forward citation notice
10. The Inventory Register (10.1 protective, 10.2 coercive)
    10.1 Possession is not evidence of a fault
    10.2 An unused item is not an owned capability (coercive)
11. Failure Classes (each row inherits the label of its governing section)
12. Conformance (12.1 and 12.2 mixed, 12.3 protective)
    12.1 Tier requirements
    12.2 Health invariants
    12.3 Self test
13. Versioning and Governance (neither coercive nor protective)

---

## 1. Introduction (protective)

### 1.1 What an item is, and the attack this closes

An **item** is an external object the operator equips, applies, or carries. Corrective optics, a load bearing brace, a respirator, a wearable, a chair, a knife, a subscription to a service, a supply of a consumable: all items, all governed here, none of them the instrument and none of them a capability.

The stack does not currently have a word for one, and the absence is not cosmetic. It leaves an attack open on the document the family is built around.

TETHER 1.2 establishes the spine: self report is a signal and never a verdict, and a threshold gating an act at K2 or above resolves against at least one reference the instrument did not produce. TETHER 2.3 makes that mechanically checkable by giving every observation a reference source from a controlled vocabulary, `self-report`, `instrument`, `second-party`, `clinical`, and TETHER F2 makes the failure detectable: a threshold gating K2 or above, resolved with no reference source other than `self-report`, leaves the act unauthorized and the threshold `unevaluated`.

Now run the attack.

An operator acquires a device. The device measures something about the instrument and emits a number. The number is written as an observation with reference source `instrument`, because a device produced it and no other value in the vocabulary fits. The threshold now has a non self report reference. The check passes. The gate opens. And the device has never been calibrated against anything, or was calibrated once at manufacture, or has drifted for three years, or is calibrating against its own reading history and has therefore recalibrated around its own drift and now reports the drifted state as zero.

Nobody lied. No gate failed. The requirement was satisfied in form and defeated in substance, and it was defeated by purchase, which is the cheapest possible way to defeat a governance requirement. The general name for this is **reference source laundering**: an act that raises a reading's apparent evidence grade without raising its actual reliability. Naming it is what makes it detectable.

Section 6 closes it. A sensing item declares a calibration interval and an external calibration reference; output produced outside the interval is `unknown`, is rejected at write time to the instrument register, and closes no gate. The consequence is that the word `instrument` in TETHER 2.3 stops meaning "a device produced it" and starts meaning "a device whose currency is on the record produced it". That is the whole of KIT's claim to independent necessity. Everything else in this document is inheritance, routing, and the ordinary discipline of declaring what you have.

### 1.2 Custody is the membership test

KIT governs items. QUEST governs capabilities. The boundary between them is one test, and it is decidable at write time.

**Can a party other than the operator end the operator's access to this, without acting on the instrument?**

If yes, it is an item and KIT governs it. If no, it is a capability, KIT does not govern it, and QUEST is the document that does.

The test is chosen over the intuitive alternative, that a tool can be lost and a skill cannot, because the intuitive alternative is false. Capabilities are lost, to disuse, to injury, and to time, and a document resting on their permanence would be unravelled by the first reader who noticed. The custody test survives that objection and does more work besides. It resolves the hard cases in form, without naming any operator's actual possessions:

- **A rented thing.** Item. The lessor can end access by declining to renew.
- **A borrowed thing.** Item. The lender can end access by asking for it back.
- **A subscription.** Item, even where nothing physical is held. The vendor can end access by terminating the service, and the capability that depended on it goes with it.
- **An employer issued thing.** Item, and the custody holder is the employer, which is the fact the operator most needs written down before they depend on it.
- **A fitted device.** Item, plus an intervention record, because ending access requires acting on the instrument. Section 3.3 governs.
- **A language the operator speaks.** Not an item. No party can end access to it without acting on the instrument.

Custody also generates three failures as one family rather than three unrelated ones: dispossession, where the custody holder ends access; vendor capture, where the custody holder is the only source of a substituting item; and replacement latency, where access ends and the gap is measured in weeks. Section 5 treats them together for that reason.

### 1.3 Severability, and why the dependency runs one way

K-A3 forbids KIT from depending on QUEST. The rationale is a safety property, not tidiness.

The entire misuse surface of this family concentrates in progression: levels, ranking, scoring, credentialing, gatekeeping. KIT carries almost none of it. An inventory of external objects, each declaring its kind, its custody, and its calibration currency, ranks nobody and grades nothing.

As one document, that separation is unavailable. An implementer who wants an equipment inventory drags the ranking machinery in with them and has to be trusted not to use it, and a vendor shipping a leveling product gets the inventory as legitimising ballast, because the safe half of the document vouches for the dangerous half. Split, the dangerous half is optional, and the optionality is mechanically checkable: full KIT conformance is reachable with no capability, node, or quest declared anywhere, which section 12.1 states again where implementers read tiers.

Severability runs one way on purpose. The dangerous document depends on the safe one; the safe one never depends on the dangerous one. A dependency in the other direction would make the equipment inventory unreachable without the progression machinery, which is precisely the coupling the split exists to prevent.

### 1.4 Position in the stack

KIT inherits POLARIS's asymmetric precedence through TETHER and does not restate it.

An item condition, an item loss, or an over equipped loadout MAY **narrow** what an operator is authorized to do. It MAY NEVER widen it, satisfy another document's check, or excuse a failure under any specification in this stack.

"I had the right gear" authorizes nothing. "The item was out of calibration" is a bound that narrows what may be claimed from its output, and it is never an excuse offered afterward for an act already taken. An operator who acted outside a bound has acted outside it, the record says so, and nothing in this document softens that.

### 1.5 `instrument` is a reserved word

Within this family, **instrument** means the body, as defined in TETHER 2.1. **In prose, KIT MUST NOT use the word for a device, a tool, or a measuring apparatus.** A measuring device is an item of class `sensor`.

**The reservation is on prose and does not reach the TETHER 2.3 controlled vocabulary.** The reference source value `instrument`, defined by TETHER 2.3, names a reading a device produced and is excepted from this reservation by name, in this subsection and in `KT-37`. The exception is necessary rather than convenient: section 1.1's whole attack analysis, and the whole of section 6, are stated about readings carrying that value, and a reservation that swallowed it would make every device reading in this family `unevaluated` and would defeat the section it exists to support. An RFC renaming the TETHER 2.3 value from `instrument` to `device` would remove the collision at its source and is the preferable long term fix. It is not raised here, and until it is raised the exception governs.

**Failure mode:** specification prose using the reserved word for an item is malformed and MUST be rejected in review, except where it is quoting or citing the TETHER 2.3 vocabulary value. Where the ambiguity reaches a record, an observation whose reference source cannot be resolved between the body and a device is recorded `unevaluated` and MUST NOT be admitted with either resolution guessed.

The reservation is worth a numbered subsection because the ambiguity runs exactly along the boundary TETHER section 5 exists to police. "An instrument reading" is a phrase that means the body's condition in TETHER and a device's output in ordinary technical English, and those are the two things whose confusion produces the attack in 1.1. One careless page would blunt the distinction that the rest of this document sharpens.

---

## 2. Definitions (protective)

### 2.1 Item

An **item** is an external object the operator equips, applies, or carries, whose membership in this document is settled by the custody test of section 3.1 and the removal test of section 3.2.

`tool` is a permitted informal synonym for use in guides, courseware, and speech. It MUST NOT appear in normative text where `item` is available.
**Failure:** normative text using `tool` as the governed noun is editorially non conformant and MUST be corrected in review. This is a drafting rule, not a runtime check.

### 2.2 Kind

**Kind** is one of exactly two values, declared per item against a named capability.

- `substitute`. The item stands in for a capability. Without the item, the capability is absent.
- `amplify`. The item raises a capability the operator holds without it. Without the item, the capability is reduced and not absent.

Kind is the axis that determines whether losing the item is an inconvenience or an outage. Section 4 governs it.

**A named capability, as this document uses the term, is an opaque operator declared label.** It has no structure, no state, and no record in KIT. **KIT never reads a capability record, never writes one, never assigns a capability a state, and never conditions any requirement on the existence or the state of one**, per K-A3. A label naming nothing that exists in any other register is still a well formed label, and every requirement in this document resolves against the item record alone.

**Failure:** an implementation resolving any KIT requirement by reading a capability record is non conformant, and the requirement is re resolved against the item record alone. Specification text in this document assigning a state to a capability is non conformant and MUST be rejected in review under K-A3.

The label exists so that an item can say what it is for without this document acquiring an opinion about capabilities. Where an operator also runs a capability register, QUEST 7.4 governs what a dependent capability does when an item departs, and that sentence is a routing statement rather than a dependency: KIT's own requirements are unchanged whether or not any such register exists.

### 2.3 Class

**Class** is the handling category an item falls into, declared per item from the vocabulary of section 2.13. The class that carries normative weight in this version is `sensor`, which is the class section 6 governs, and it carries that weight because sensing items fail silently while other classes fail loudly.

### 2.4 Job

A **job** is the declared set of targets an item is for, expressed as a decidable predicate over targets. A predicate requiring judgement to evaluate is not a job, per DEFER 4.3. Section 7 governs.

### 2.5 Slot and loadout

A **slot** is a typed, exclusive position an item occupies. Slots model the scarcity that is structural rather than fungible: two items cannot occupy the same position at the same time regardless of how much money, attention, or time the operator has.

A **loadout** is the set of items equipped at one time, together with their slot assignments and their summed draw on each declared budget meter.

### 2.6 Custody holder and provisioning party

The **custody holder** is the party able to end the operator's access to an item without acting on the instrument. It is a declared field. It is frequently not the operator.

The **provisioning party** is defined by HABITAT 2.4 and is not redefined here. KIT requires it as a field on a substituting item (5.3) and delegates every attribution rule to HABITAT.

The two are distinct and an implementation MUST NOT collapse them. A custody holder can end access to a specific item the operator already holds. A provisioning party controls whether the class of input reaches the operator at all. The same party frequently occupies both roles and the fields are still separate, because the failures they name are different: dispossession against a supply failure.

### 2.7 Confirmation interval, calibration interval, calibration reference

A **confirmation interval** is the declared period inside which an item MUST be confirmed present. Section 5.1 governs.

A **calibration interval** is the declared period inside which a sensing item's calibration MUST be refreshed against its reference. Section 6.1 governs.

A **calibration reference** is a source the item did not produce, against which its output is checked. Section 6.2 governs, and the requirement that it be external is the whole of its content.

### 2.8 Loss posture and replacement latency

A **loss posture** is the declared state a dependent capability takes while a substituting item is absent, together with the fallback in force during that absence.

**Replacement latency** is the declared period between an item's loss and the operator's realistic recovery of an equivalent item. It is a declared field, and an undeclared one reads unbounded rather than zero.

**Loss exposure** is a per item record and never a computed value. It names one `substitute` item and carries that item's loss posture, its replacement latency or `unbounded`, its custody holder, and whether a fallback is declared. It has no magnitude, so there is nothing to total, order, or compare. Section 5.3 governs its required output form.

### 2.9 Budget and meter

A **meter** is defined by DEFER 2.5 and is not redefined here.

A **budget** is a set of declared meters, each optionally carrying a bound, against which a loadout's summed draw is computed. A meter declaration takes the form DEFER 5.4 states. Section 8 governs, including the requirement that at least one declared meter is not `currency`, that every declared bound carries at least one windowed aggregate ceiling, that an item scoped bound additionally carries a per item ceiling, and that a budget declaration carries a loadout review interval.

### 2.10 The inventory register

The **inventory register** holds item records: what the operator holds, on what terms, in what condition. It sits alongside TETHER's operator register and instrument register and shares entries with neither.

An item record is not an observation, is not an identity record, and is not a fault record. Section 10.1 states the requirement that makes the last of those three load bearing.

### 2.11 The fail closed naming convention

Every fail closed state name in this document names what is missing and never a deficiency in the operator. `unconfirmed` names a missing confirmation. `unprovisioned` names a missing supply. `unknown` names a missing valid reading. `unused` names a missing application record. `over-equipped` names a declared bound exceeded. `out-of-scope` names a check that does not reach its subject.

The convention is not invented here. TETHER already uses `unevaluated`, and HABITAT already uses `unattributed` and `unprovisioned`. A fifth document in this family inventing `deficient` would import, in a state name, exactly the identity merge the family's second absolute forbids, and it would import it in the one place nobody reviews: the enum.

### 2.12 The closed game vocabulary

This document uses game native vocabulary deliberately, and the vocabulary is closed. Three classes, and the discriminator is **ordering connotation**, not etymology and not informality.

Design note 0005 section 2 ruled that "meat suit" stays in teaching material and out of normative text. That ruling is honored here and it does not settle this case, because it turned on a specific property: "meat suit" is a framing of what a person is, and a specification requiring a metaphysics is a creed. `loadout` makes no claim about what a person is.

**(a) Normative defined terms.** A game native word MAY be a normative defined term where it is a noun with a decidable definition carrying no ordering, ranking, or accumulation connotation. In this document: `item`, `kit`, `loadout`, `slot`, `class`, `kind`, `job`. These are as normative as `envelope` or `observation`.

**(b) Forbidden in normative text regardless of definition.** `level`, `rank`, `tier` used as a property of an operator, `score`, `grade`, `index`, `experience points`, `XP`, `prestige`, `elite`, `mastery`, and `grinding` used as a verdict. These are the vehicle by which a teaching device becomes a score applied to a person, and defining them carefully does not disarm them.
**Failure:** specification text using a class (b) term as a property of an operator is non conformant and MUST be rejected in review. Note that `tier` remains available in its stack sense, as a conformance tier of an implementation, which is a property of an implementation and not of a person.

**(c) Motto class, non normative.** The third person narration: "achievement unlocked", "map marker updated", "accepting a side quest", "the tracker". These are marked non normative under POLARIS 7.3, are kept because compression aids recall, and MUST NOT be cited as grounds for any decision, gate evaluation, or approval.
**Failure:** a class (c) phrase appearing as grounds in a record is detected as the POLARIS PL-04 pattern.

**The table is closed.** An implementation MUST NOT introduce a game term outside it.
**Failure:** an introduced term is non conformant vocabulary and MUST be rejected in review; admitting a new term is an RFC. The reason is specific: an open vocabulary acquires `prestige`, `ascended`, and `tier` from whatever product the reader last used, and each one smuggles a total order back in through a word this specification never defined and therefore never bounded.

**Reversal path.** If the institutional readership argument wins outright, every normative section is rewritten with neutral terms (equipped set, declared position, applied object) and the whole game vocabulary moves into the closed non normative table. No requirement changes in substance, only in wording. The table above already exists, so the reversal costs one editing pass rather than a redesign, and the author's choice is therefore real rather than nominal.

### 2.13 The class vocabulary and its extension rule (skeleton)

**Thesis.** Class is the handling category, and the set is chosen by what fails differently rather than by what an object is made of. A sensing item fails silently and needs a clock; a load bearing item fails loudly and does not. A consumable is exhausted rather than lost, which is a different disposition on the same axis as section 5.2. The set is small, enumerated, and extensible by RFC rather than by an implementer, for the same reason the game vocabulary is closed: an open set acquires categories that carry rules nobody wrote.

Working set, to be settled: `sensor`, `load-bearing`, `protective`, `computational`, `consumable`.

To be written: the declaration form for a class; the extension rule and its RFC threshold; the rule for an item that plausibly belongs to two classes, which should follow TRACE 3.2's direction that the stronger handling applies and should state the order explicitly; the disposition of a consumable, whose exhaustion is a foreseen expiry rather than an unforeseen loss and therefore may need a disposition value section 5.2 does not currently carry; and the treatment of an item whose class an operator declines to declare, which under this document's fail closed direction is handled as `sensor` where it produces any output about the instrument and is otherwise rejected at write time.

What is already settled and binds regardless of how this section closes: every item MUST declare a class (4.1), an item of class `sensor` is governed by section 6, and **the disposition for an undeclared class has been lifted out of this skeleton into 4.1, where the MUST lives, and binds from there.** No requirement in this document now depends on this section closing. What remains open here is the working set's final membership, the declaration form, the RFC threshold, the two class tiebreak order, and the consumable disposition.

---

## 3. Membership, and the Boundary with TETHER (protective)

### 3.1 The custody test, normatively

**Every item record MUST declare its custody holder, meaning the party able to end the operator's access to it without acting on the instrument.**

**Failure mode: an item with no declared custody holder MUST be treated as held by a third party.** Fail closed to third party, never to operator.

The direction matters and is not arbitrary. Defaulting in the operator's favour erases the distinction exactly where an implementer was lazy, and the items whose custody goes undeclared are disproportionately the ones an operator has stopped thinking of as external: the employer issued device, the auto renewing subscription, the thing that has been in the drawer so long it feels owned. Reading silence as ownership would report the operator as holding a loadout they may not hold.

The direction follows the family's established pattern rather than inventing one. CONFIDE 2.4 treats an undeclared retention posture as C4 and forbids an omitted field from widening what a provider may receive. HABITAT section 3 treats an undeclared input class as unprovisioned rather than adequate. KIT treats an undeclared custody holder as external. In all three, silence is never read as favorable.

A thing that fails the custody test, meaning no party other than the operator can end access to it without acting on the instrument, is not an item, is out of scope for this document, and is governed by QUEST. KIT states no requirement about it and gains none when QUEST lands.

### 3.2 The removal test, and the boundary with TETHER 10

**A thing whose removal from the instrument is classified K2 or above under TETHER 3.2 MUST NOT be recorded as an item alone.** It is an intervention, and TETHER 2.4 defines the four required elements (purpose, cost, exit condition, evaluation window), with TETHER section 10 governing interventions once written.

**A second routing test, keyed on the act rather than on the removal.** **An item whose application is itself an act undertaken to change the instrument's condition MUST carry an intervention record alongside its item record**, on the `fitted` pattern of 3.3. TETHER 2.4 keys the definition of an intervention on the act, and the removal test alone does not reach it: a supply of a consumable is named as an item in 1.1, its removal from a loadout is not a K2 act, and its ingestion is plainly an act undertaken to change the instrument's condition.

**Failure mode for the second test:** an item whose application meets TETHER 2.4's test and which carries no intervention record is malformed and is rejected at write time, on the same terms 3.3 applies to a `fitted` item carrying only one of its two records. The four elements bind the intervention record. They do not bind the item record, and 4.3 says so, so that this test creates no pressure to discontinue a substituting item.

**Failure mode:** the record is rejected as an item record at write time and MUST be reopened as an intervention record. The rejection is at write time rather than at review, because a record that exists for a week as equipment has already been read by whatever consults the inventory.

Without this test, KIT's lighter regime is the cheap route around TETHER 10. An intervention record demands four elements including an exit condition and an evaluation window, and an item record does not. An operator or an implementer who would prefer not to declare an evaluation window has, absent this test, a filing option: call it equipment. The test closes it with a criterion neither party controls, since the classification of a removal is computed under TETHER 3.2 rather than chosen.

The test is the losability asymmetry made mechanical, and it is the honest form of the intuition the custody test replaced in 1.2: if you cannot take it off without leaving a durable trace in the instrument, it is not equipment.

### 3.3 The `fitted` class

**An item that is both equipped and not removable without a K2 act carries both an item record and an intervention record.** It is declared `fitted`. Both regimes bind: KIT's calibration, custody, job, and data surface rules apply to the item record, and TETHER 2.4's four required elements apply to the intervention record, governed by TETHER section 10 once that section is written.

**Failure mode:** a `fitted` item carrying only one of the two records is malformed and is rejected at write time. Carrying only the item record evades the four elements. Carrying only the intervention record loses the calibration discipline of section 6, which is the discipline that matters most for exactly this population, since a fitted sensing item is the one whose drift is hardest to notice and whose output is trusted most.

### 3.4 A party is not an item

K-A1 in full.

**An item MUST be an object. Any identity that can hold a register, can consent, or can be an operator MUST NOT be declared as an item, placed in a slot, counted against a budget, or written to the inventory register.**

**Decidable test:** if the thing could hold a register or could consent, it is a party.

**Failure mode:** the declaration is rejected at write time and is routed according to the relationship declared: to the DEFER adapter as a handover grant where the party decides, to the SPEAK adapter as an agreement where records cross between them, and to the RETAIN adapter as an engagement where the party accumulates state about the operator.

Agents and software fall on the party side of the test and route to RETAIN, whose residue routes to TRACE and whose telemetry routes to CONFIDE. KIT gains nothing by claiming them and would lose the test by trying, since a decidable object test survives contact with a hard case only while it refuses to be argued into covering things that can consent.

**What this does not forbid:** recording that the operator works with a coach, a clinician, or an assistant. The relationship is recordable, and it is recorded in a register that models parties rather than in one that models possessions. The prohibition is on the filing, and the reason is that an inventory is a thing you confirm the presence of, count against a budget, and mark `unused`, and none of those are things to do to a person.

### 3.5 Clinical direction, and the coercive and protective split

**Where an item is prescribed, fitted, or directed by a licensed clinician, the item record MUST carry that direction as a declared field.**

**Failure mode for the field itself, and it fails closed toward protection. An item record whose clinical direction field is absent, or declared `unknown`, MUST be handled as clinically directed for the purpose of the coercive and protective split, until the operator declares otherwise.** The item is surfaced as `unconfirmed` on that field, and it MUST NOT be assumed non clinical. A coercive check resolving against such a record returns `out-of-scope` on the same terms as one resolving against a record that carries the field, per the disposition below.

The direction is the one this document already applies everywhere else and is not invented here. An undeclared custody holder is external (3.1), an undeclared kind is `substitute` (4.1), an undeclared job is an empty predicate (7.1), and an undeclared calibration interval is out of calibration from the moment of declaration (6.1). In every case, silence resolves to the stricter handling. This field is the single input that routes an item into the protection derived from inherited absolute 4, and reading its absence as "not clinical" would put a prescribed brace, respirator, or monitor into budget pressure, slot contention, trial exit conditions, and an `unused` mark, on the strength of a field nobody filled in. The count in 12.2 is also uncountable unless the discriminating field has a defined value in every case, which this failure mode supplies.

**The `unconfirmed` surfacing is protective and never coercive.** It is a report that a declaration is missing. It is never a report that the item is unjustified, MUST NOT be presented as a defect, and MUST NOT be used to withhold, delay, or downgrade anything about the item.

Every section of this document is classified **coercive** or **protective**, and the two are applied asymmetrically to a clinically directed item.

A **coercive** rule generates pressure toward carrying fewer items. Budget bounds, slot contention, loadout ceilings, the unused item rule, and the trial adoption and exit rules are all coercive: each of them has a compliant response that consists of removing something.

A **protective** rule only ever narrows what may be claimed from an item. Calibration, the unknown output rule, the reference source rules, job declaration, custody declaration, and provisioning declaration are all protective: their compliant response is a better declaration, never a removal.

**Coercive rules MUST NOT be applied to a clinically directed item.** In this version those are sections 4.4, 8 **excluding 8.1**, and 10.2. **8.1's slot exclusivity is protective and continues to apply**, under the clinical branch stated there, because it is a statement of physical fact rather than pressure: exempting it would admit two items to one slot and make the register assert a loadout that cannot exist.
**Protective rules continue to apply to a clinically directed item.** In this version those are sections 1, 2, 3, 4.1 to 4.3, 5, 6, 7, 9, and 10.1.

The protective enumeration is stated exhaustively rather than by omission, because an enumeration that skipped sections 1, 2, and 4.1 to 4.3 left them to the unlabelled default, and the default is coercive. That would have made 4.2's loss posture requirement coercive and returned `out-of-scope` for a clinically directed item, exempting exactly the population that most needs a fallback declared from declaring one.

**Scope of the label.** A section's label is a statement about the requirements it places **on an item**. A section placing requirements only on this specification's own text, or only on an implementation's reports, carries the label `neither`, and K-A2, K-A3, 1.5, 2.11, and 2.12 carry `neither` explicitly on that ground. A `neither` section does not inherit the coercive default and never resolves `out-of-scope`, because there is no item for it to resolve against.

**Inheritance and precedence between the two mechanisms.** The label attaches to a top level numbered section. **A subsection inherits its parent section's label unless it carries a label of its own**, which is how sections 4 and 10 already read and which is why sections 5, 6, 7, and 9 carry no subsection labels. **Where a section header's label and the enumeration above disagree, the stricter of the two governs until the disagreement is corrected in review**, and a disagreement is itself a defect to be corrected rather than a state to be left standing.

**Failure mode:** a coercive class check resolving against a clinically directed item returns `out-of-scope`. It never returns a pass and never returns a fail, because a pass would let the item's exclusion be read as satisfaction and a fail would be the pressure the exclusion exists to remove.

**A tier item, health invariant, or self test check that an operator could satisfy by discontinuing a clinically directed item is malformed specification text and MUST be rejected in review**, per inherited absolute 4.

This resolution is chosen over the simpler one of excluding clinically directed items from KIT entirely. Exclusion has an obvious appeal and one fatal consequence: it puts the calibration rules of section 6 out of reach of the sensor whose drift matters most, since a clinically directed sensing item is precisely the one whose output will be offered to a consequential threshold. The asymmetric split keeps the protection and drops the pressure, which is the only combination that satisfies both inherited absolute 1 and inherited absolute 4 at once.

Membership between item and intervention is settled by the removal test of 3.2 and not by the presence of clinical direction. A clinically directed item that can be removed without a K2 act is an item, carries the clinical direction field, and is governed by the protective sections. A `fitted` item carries both records, per 3.3.

---

## 4. Kind: Substitution and Amplification (4.1 to 4.3 protective, 4.4 coercive)

### 4.1 The declaration (protective)

**Every item record MUST declare exactly one kind, `substitute` or `amplify`, against a named capability, and MUST declare its class.**

**Failure mode: an item with no declared kind is written as `substitute`.** The stricter handling applies, following TRACE 3.2's direction that where a thing could belong to two classes the stronger handling is used.

**Failure mode for the class declaration, stated here rather than left inside the skeleton of 2.13, because 4.1 carries the MUST and a MUST with no failure mode is not a requirement. An item with no declared class that produces any output about the instrument is handled as class `sensor`, and is therefore governed by section 6 including 6.1's disposition for an undeclared calibration interval. An item with no declared class that produces no such output is rejected at write time.** The direction is the one 2.13 already states and is binding in this version whatever else 2.13 settles: `sensor` is the strictest available handling, and the item that produces a number about the instrument is the item whose misclassification costs the most.

The named capability the kind is declared against is the opaque label of 2.2. It carries no state, no record, and no requirement, and this subsection resolves entirely against the item record.

The asymmetry of costs is the whole argument. Wrongly treating an amplifier as a dependency costs a loss posture declaration nobody needed, which is a paragraph of writing and a slightly noisier report. Wrongly treating a dependency as an amplifier costs a capability that vanishes without warning, with no fallback declared, no replacement latency computed, and a register still asserting the capability is held. The default goes to the direction whose error is cheap.

A single item MAY be declared against more than one capability, with a kind per capability, since an item that amplifies one capability while substituting for another is ordinary rather than exotic. Each declaration is evaluated independently under this section.
**Failure:** a multi capability declaration missing a kind for any named capability is treated as `substitute` for that capability, per the default above.

### 4.2 Loss posture is required on every substituting item (protective)

**A `substitute` item MUST declare a loss posture: the state the dependent capability takes while the item is absent, and the fallback in force during that absence.**

**Failure mode:** a `substitute` record missing a loss posture is rejected at write time. Where such an item is nonetheless absent with no declared loss posture, the item is recorded absent under 5.2 with the disposition that section supplies, and any threshold depending on that item's output is `unevaluated`, per TETHER F2. Neither is an error. Both are states. **KIT assigns no state to the named capability here or anywhere**, per K-A3 and 2.2. Where the operator also runs a capability register, the transition of the dependent capability is QUEST 7.4's.

A loss posture is what makes loss exposure computable in 5.3, and it is required rather than recommended because the moment at which an operator would most want it written down is the moment they are least able to write it: the item is already gone.

### 4.3 Permanence is a declared state, never a defect (protective)

**An item record MAY declare its dependency `permanent`. An implementation MUST NOT treat a permanent dependency as a deficiency, a failure, an unmet requirement, or an item to be resolved.**

**Failure mode:** a check, tier item, or health invariant reporting a permanent dependency as unsatisfied is malformed specification text and MUST be rejected as non conformant. A report listing permanent dependencies MUST present them as declared facts, and MUST NOT rank, total, or flag them.

**Failure mode for the implementation, so that the prohibition binds a product and not only this document's wording: a report that ranks permanent dependencies, that totals them, or that flags any of them is non conformant, the ranking or total is void, and the report MUST be re rendered as an unordered per item enumeration.** An ordering across items requires a comparable per item magnitude, which is the scalar 5.3 exists to prevent, and it is the same value whether it arrives in a report field, a sort order, or a table's default column.

**The prohibition on requiring an exit condition binds the item record only.** It is never a waiver of TETHER 2.4 for an intervention record accompanying that item under 3.2 or 3.3. Where the item's application is itself an act on the instrument, the intervention record carries the four elements and the item record does not, and an implementation that reads 4.3 as excusing the intervention record has read it wrongly.

The rationale stated plainly, because this is the section most likely to be misread by an implementer who has read a wellness product: **permanence MUST be declared so that loss exposure can be computed, and MUST NEVER be treated as a defect.** The undeclared dependency is the failure. The declared permanent one is a fact.

This section is also where the author's original seed was inverted deliberately, and the inversion is recorded here so that a future reader does not restore it. A rule requiring every substituting item to declare what would end it generates pressure to stop using the item. Applied to corrective optics, a mobility aid, or a monitor, that is inherited absolute 4 violated in one sentence, and it is the exact failure this family exists to prevent. The concept therefore splits: a **loss posture** is required on every substituting item, so exposure can be computed, and an **exit condition** is required only on a `trial` item, per 4.4.

### 4.4 Trial items and exit conditions (coercive)

**An item MAY be declared `trial`, meaning adopted to test a stated hypothesis. A `trial` item MUST declare an exit condition and an evaluation window.**

**Failure mode:** a `trial` record missing either element is rejected at write time, on the same terms TETHER F4 applies to an intervention record missing one of its four elements.

**An item that is not declared `trial` MUST NOT be required to declare an exit condition.** An implementation that requires one of every substituting item is non conformant, per 4.3.

An item MUST NOT be recorded as ineffective before its declared evaluation window closes; closure inside the window is recorded as **abandoned** and never as **ineffective**, per TETHER F5. The distinction is not bookkeeping. A register that conflates a deliberate stop with a demonstrated failure poisons every later decision that reads it, because the operator will later see "ineffective" and decline to reconsider a thing that was never actually tested.

**This section is coercive and does not reach a clinically directed item**, per 3.5. A coercive check resolving against such an item returns `out-of-scope`.

---

## 5. Tenure: Custody, Confirmation, and Loss (protective)

### 5.1 Confirmation is periodic, because loss produces no event

**Every item MUST declare a confirmation interval. An item not confirmed present inside its interval MUST be recorded `unconfirmed`.**

**Failure mode: an item with no declared confirmation interval MUST be recorded `unconfirmed` from the moment of its declaration**, on 6.1's construction and for 6.1's reason. Without that clause the compliant response to this section is to decline to declare an interval, and the item never becomes `unconfirmed` at all, so the register goes on asserting possession of a thing nobody has checked for and no check can name the gap.

**Failure mode:** fail closed to `unconfirmed`. `unconfirmed` is a state and not an error. An implementation treating a past confirmation as continuing satisfaction is non conformant, in the disposition TETHER F3 applies to a lapsed re reference.

**KIT records the item side fact and stops.** It assigns no state to any named capability, per K-A3 and 2.2. Where the operator also runs a capability register, QUEST 7.4 governs what an `unconfirmed` substituting item does to a dependent capability.

TETHER 5.4 is the canonical statement that re referencing is periodic rather than triggered, and this section cites it rather than restating its reasoning. **That citation is a forward citation into an unwritten section**, marked as such per TETHER's own status note, and this document declares only its own interval and its own lapse disposition. The reasoning is not repeated a fourth time in this family, and the recommendation to the author stands that TETHER 5.4 be written to own it.

What is specific to items, and is therefore stated here: loss produces no event on the operator's side. A device stops working and announces it. A device left in a taxi announces nothing, and neither does one a custody holder declined to renew. The register goes on asserting a capability the operator does not have, and it asserts it most confidently for the items that are most routine, because those are the ones nobody thinks to check.

### 5.2 Leaving the loadout carries a disposition

**An item leaving a loadout MUST be recorded with a disposition from `lost`, `broken`, `expired`, `superseded`, `released`, `unprovisioned`. `released` MUST NOT be recorded as `lost`, and `lost` MUST NOT be recorded as `released`.**

**Failure mode:** an item absent with no recorded disposition fails closed to `lost`. **The disposition is the whole of KIT's output here.** KIT assigns no capability state, per K-A3 and 2.2. Where the operator also runs a capability register, QUEST 7.4 governs what any of the six dispositions does to a capability that declared a `substitute` dependency on the item.

This is TETHER F5's discipline applied to equipment. A register that conflates a deliberate decision with an involuntary failure poisons every later decision that reads it, exactly as conflating `abandoned` with `ineffective` does, and it poisons it in both directions: an operator who reads `lost` where they released something will replace a thing they chose to stop carrying, and an operator who reads `released` where something was taken will not notice a custody holder who is quietly ending their access.

The failure this section prevents is not the loss. Loss is ordinary and this document takes no position on it. The failure is the long interval during which nothing records what is gone while the register goes on asserting a capability nobody has, which is the equipment form of the silent drift TETHER 1.2 and HABITAT section 8 both name.

### 5.3 Replacement latency and loss exposure

**A `substitute` item MUST declare its replacement latency, its replacement cost, and its provisioning party under HABITAT 2.4.**

**An implementation MUST compute loss exposure for each `substitute` item** from its loss posture, its replacement latency, and whether its custody holder is a party other than the operator, **and MUST surface any `substitute` item whose custody holder is not the operator.**

**Loss exposure is a per item record and never a computed magnitude.** Its required output form is exactly one entry per `substitute` item, carrying that item's identifier, its declared loss posture, its replacement latency or `unbounded`, its custody holder, and whether a fallback is declared. **It carries no value, no grade, and no ordering.**

**Failure mode:** a record missing latency, cost, or provisioning party is rejected at write time. An undeclared replacement latency is recorded unbounded rather than zero. A `substitute` item held at external custody with no declared fallback is an undeclared single point of failure, is surfaced as such, and MUST NOT be reported as an adequate loadout. **An implementation that surfaces no loss exposure entry for a `substitute` item has not computed loss exposure, is non conformant, and MUST NOT report the loadout as adequate.** Stating this separately matters, because the three failure modes above all address a record missing a field, and an implementation carrying every field while computing nothing would otherwise pass every check in this section undetected.

Loss exposure is enumerated per item and MUST NOT be reduced to a single figure across items. **A report over loss exposure MUST NOT total it, rank it, order the items by it, or present it as a magnitude, and an implementation doing any of the four is non conformant with the report void and re rendered as an unordered enumeration.** A report saying which substituting capabilities are exposed is useful; a report saying how exposed the operator is has produced a number about a person, which is the vehicle this family removes.

The rationale stated as the general rule, never as a case: **a substituting sensing item, with a long replacement latency, held at a custody the operator does not control, is a capability that will simply be gone for a measured period.** Each field in that sentence is individually unremarkable and every operator would shrug at it in isolation. Their conjunction is the failure, and the conjunction is invisible unless all four fields are on one record, which is the entire reason this section requires them together rather than separately.

### 5.4 A supply failure is not an instrument fault

**Where the operator is not the provisioning party, an item recorded `unprovisioned` MUST have its resulting capability loss attributed to the provisioning party, and MUST NOT be attributed to the instrument or to the operator.**

**Failure mode:** a capability loss attributed to the instrument while the provisioning party is another party is recorded `unattributed`, under the **HABITAT H5** disposition, and is routed under HABITAT section 7. H5 is the on point class: it governs an operator held to a class they do not provision, with attribution routed to the provisioning party under section 7, which is exactly the case this subsection states. H4 governs a fault attributed to the instrument against a stale or absent mismatch register, which is a different failure that happens to share a disposition word. **Both HABITAT section 9 codes are forward citations into a section HABITAT itself labels as unwritten**, on the same terms as the adapter citations marked in 9.3.

The named capability in this subsection is the opaque label of 2.2, and KIT assigns it no state. What KIT records is the item side fact (`unprovisioned`) and the attribution routing.

KIT declares the field and routes. It states no attribution rule of its own, and gains none when HABITAT section 7 is written.

HABITAT's own caution is carried forward and applies to every sentence in this subsection: this is a requirement about attribution and not a claim about blame. An employer, a household, an insurer, or a supplier that does not provision an item is the party a fault attaches to for the purpose of the register, and the register's purpose is to keep the repair aimed at the right layer. Nothing here says a party did wrong, and text drifting to that side is non conformant.

---

## 6. Integrity: Calibration and the Sensing Item (protective)

Failures come in two kinds and only one of them generates a requirement.

A **loud** failure announces itself. A load bearing item that snaps, a strap that tears, a battery that dies: the operator learns at the moment of failure, no interval is needed, and no specification improves the situation. A **silent** failure does not. A sensing item that has drifted goes on producing readings in the same units at the same precision on the same schedule, and there is nothing in the output that distinguishes a good reading from a bad one.

This section is therefore about sensing items and not about durability generally. Durability of a loud failing item is a maintenance concern and KIT states no requirement about it, because a requirement there would be advice rather than governance.

### 6.1 The calibration declaration

**An item of class `sensor` MUST declare a calibration interval, a calibration reference external to the item, and the version of its measurement pipeline**, meaning the identifier of the firmware, model, or processing chain that produces its output.

**Failure mode: an item of class `sensor` with no declared calibration interval MUST be treated as out of calibration from the moment of its declaration**, and its output is therefore `unknown` under 6.3 from the moment it is recorded. **An item of class `sensor` with no declared measurement pipeline version is treated on the same terms**, out of calibration from the moment of its declaration.

**A change to the declared measurement pipeline version MUST reset the calibration interval**, and the item is out of calibration until it is recalibrated against its reference under 6.2. **Failure mode:** an implementation carrying a calibration interval across a pipeline version change is non conformant, and the interval is treated as never having been reset, on 6.2's existing pattern that a rejected calibration does not reset the interval. An over the air update that silently alters what the number means is a drift with no drift: nothing about the item aged, and the reading nonetheless stopped meaning what it meant, which is a failure of exactly the silent kind this section exists for.

This clause is the teeth of the section. Without it, the compliant response to section 6 is to decline to declare an interval, and every sensing item lives permanently in an unevaluated state that no check can name. With it, the failure to declare produces the strictest outcome immediately, which is the only construction that makes an interval requirement bind against an implementer in a hurry.

### 6.2 No self calibration

**A calibration reference MUST be a source produced neither by the item nor by any party in the item's custody or supply chain, and MUST NOT be the item's own reading history or the reading history of the population the item belongs to.**

**Failure mode:** the calibration record is rejected at write time, and the item's calibration state remains lapsed. A rejected calibration MUST NOT reset the interval.

**What this does not forbid:** a vendor supplied calibration service, provided that service is itself externally referenced and the record says against what. The prohibition is on a closed loop, not on the vendor.

The scope is the supply chain and not the single unit, because the error generalizes without weakening. A vendor that normalizes every unit against its own fleet population has satisfied a single item reading of this requirement and committed the identical error at fleet scale: the reference is still produced by the party whose drift is in question, and the whole population has recalibrated around its own.

TETHER 1.2 is the reasoning and this document does not restate it. One sentence of application is enough: an item calibrating against its own history has recalibrated around its own drift and now reports the drifted state as zero, which is the auditor running on the audited hardware with the hardware purchased rather than born.

### 6.3 Output outside the interval is unknown

**Where a sensing item is outside its declared calibration interval, an implementation MUST report its output as `unknown`, and MUST NOT report, carry forward, interpolate, or display its last recorded reading as current.**

**Failure mode:** fail closed to `unknown`. Never to last known good. Never to an interpolated value. Never to the reading itself with a warning attached.

The three prohibited fallbacks are enumerated because each is a plausible implementation choice and each reconstructs the failure. Last known good is a stale reading presented as current. Interpolation manufactures a reading nothing produced. A reading with a warning attached is the worst of the three, because the number is what gets read and the warning is what gets dismissed, and the operator ends with a precise figure and a vague unease rather than an honest absence.

### 6.4 The reading is not an observation, and the write is rejected

**Output produced by a sensing item outside its calibration interval MUST be rejected at write time to the instrument register, and MUST instead be recorded as an item condition entry in that item's own record.**

**An item condition entry carries exactly four fields: the reading, its timestamp, the identifier of the item that produced it, and the item's calibration state at the time of the reading.** A record missing any of the four is malformed and is rejected. The entry lives in the item's own record and never in the instrument register, and it is the evidence that the item has drifted, which is the reason the reading is kept rather than discarded.

The noun is `item condition entry` and not `tool condition entry`, per 2.1: `tool` is an informal synonym and MUST NOT appear in normative text where `item` is available, which here it plainly is.

**Failure mode:** the write is rejected. The underlying instrument condition retains its last valid value and its own currency, which then lapses to `unevaluated` under TETHER 5.4 by the ordinary mechanism. The system degrades to unknown rather than to a false reading.

The attack closed is the reference source laundering of section 1.1: a reading still tagged `instrument` carries self report grade reliability into a higher grade, with nobody lying and no gate failing.

**Note for the drafter, and for any future amendment.** This construction is chosen specifically because it adds no value to TETHER 2.3's controlled vocabulary and requires no TETHER amendment. The tempting alternative, degrading such a reading's reference source to `self-report`, is rejected on two grounds: it is false in the other direction, since the operator did not report it and a later reader would conclude they did, and it would require a change to a vocabulary four documents already depend on. Rejecting the write and holding the reading in the item's own record achieves the same protection with no new machinery, and it keeps the item's condition history, which is itself the evidence that the item has drifted.

### 6.5 An uncalibrated sensing item closes no gate

**Output from an item recorded `unknown` under 6.3 MUST NOT satisfy a TETHER 7.3 rung gate, and MUST NOT be the supporting reference for a threshold gating an act at K2 or above.**

**Failure mode:** the rung gate is `unevaluated` and never `passed`, per TETHER F3. The threshold is `unevaluated` and the act is unauthorized, per TETHER F2. Neither is an error. Both are states.

This follows from 6.4 and is nonetheless written, because the inference is exactly the one implementers skip. Left implicit, a wearable closes a gate: the reading was already in the system from before the lapse, or it arrived by a path that did not pass through the instrument register, or the gate consults the device rather than the register. Stating the prohibition at the gate makes the requirement visible where the decision is made rather than only where the write happens.

There is a second reason, and it is a clarification the family currently lacks rather than a restriction. TETHER 7.3 makes the rung gate the one gate in this stack satisfied by evidence external to the instrument rather than by an authorized signature, and **a sensing item is external to the instrument.** That is correct and it is useful: a calibrated item legitimately closes gates the operator's own reading cannot, which is most of why an operator acquires one. The entire load therefore falls on calibration currency. This section is where that load is made visible.

### 6.6 Observations citing an item

**An observation citing a sensing item MUST record that item's identifier and the currency of its last calibration.**

**Failure mode:** an observation citing a sensing item without both fields is malformed and is rejected at write time.

The failure mode is unusually strict for a missing field and the reason is mechanical rather than punitive: without the identifier and the currency, section 6.4 cannot be evaluated against the observation at all. A record that cannot be checked against the rule that governs it is not a weaker record, it is an unchecked one, and it will be read later as though it had passed.

---

## 7. Job, and Off Job Application (protective)

### 7.1 The job predicate

**Every item MUST declare its job as a decidable predicate over targets.** A predicate requiring judgement to evaluate is not a job, per DEFER 4.3.

**Failure mode: an item with no declared job has an empty predicate, and every application of it is therefore an off job application** under 7.2.

The default is what makes this section survive contact with an implementer in a hurry. An undeclared job that produced no consequence would be the universal choice, and the section would bind against nobody. An undeclared job that makes every use off job produces noise immediately, on the first application, which is the moment at which declaring the job is cheapest and most accurate.

### 7.2 Off job application is recorded, never forbidden

**Application to a target outside the declared job MUST be recorded as an off job application.**

**Failure mode:** an unrecorded off job application is an unrecorded act, in the disposition DEFER DF-10 applies. Where a fault later appears and the ledger holds no record of the application, the fault is recorded `unattributed` under the HABITAT H4 disposition and MUST NOT be attributed to the instrument.

The design choice is deliberate and is stated so that a reviewer does not read it as a gap. **The specification records rather than forbids**, because improvisation is sometimes correct, occasionally necessary, and routinely the only option available at the time. A document that forbade it would be ignored rather than followed, and a document that is ignored records nothing, which costs the register the very entry that makes a later fault attributable.

### 7.3 Classification is on the target, never on the item

**An off job application MUST be classified on the target's worst true consequence under DEFER 6.1, and MUST NOT inherit the consequence class of an in job application of the same item.**

**Where the target is the instrument, the application is classified on the target's worst true consequence under DEFER 6.1, and MUST NOT be covered by a standing pre classification, per DEFER 6.6.**

**No class floor is asserted here, and none is attributed to TETHER 3.2.** An earlier draft of this subsection stated a K2 minimum and attributed it to TETHER 3.2, which states no such floor and whose K0 and K1 definitions are themselves about the instrument, K0 by absence of residue and K1 as reversible over a declared window at real cost. A floor would have emptied both rungs, and because 3.2's removal test also resolves against TETHER 3.2's classification, a floor making everything on the instrument K2 would have collapsed the boundary between an item and an intervention. The requirement that survives is the one that was doing the work: classify on the target, and refuse the standing pre classification.

**Failure mode:** an off job application classified at the item's ordinary class is a classification defect on the DEFER DF-16 pattern, which is a class assigned by typical case rather than by worst true case. The act is unauthorized, and the classification is recomputed on the target.

The author's framing of this is preserved because it is right. **The failure of the wrong tool is not that it fails to work. It is that it damages what it was applied to.** A tool used off job that simply does not work is a wasted afternoon and generates no requirement. A tool used off job that works well enough to be persisted with, while transferring load into something that was not built to receive it, is the case worth governing, and the damage lands on the target rather than on the item. Classification therefore has to follow the target, or the class is computed against the party that does not absorb the consequence.

The standing pre classification exclusion follows DEFER 6.6, which forbids a standing record from assigning a class above K1. It is stated explicitly here because implementers will otherwise let a routine item carry its routine class into a non routine use, which is the exact shape of the exclusion DEFER 6.6 already writes for act families and which is easier to overlook when the family is defined by an object rather than by a verb.

---

## 8. Slots, Budgets, and Contention (coercive, except 8.1 which is protective)

**This section is coercive and does not reach a clinically directed item**, per 3.5, **with one carve out: 8.1's slot exclusivity is protective and continues to apply, under the clinical branch stated there.** Every other check in this section resolving against a clinically directed item returns `out-of-scope`, never a pass and never a fail.

Two kinds of scarcity, and implementations that conflate them get contention wrong in both directions.

A **slot** is typed and exclusive. Contention on a slot is decidable: either the position is occupied or it is not, and no amount of budget resolves it. A **budget** is fungible and accumulating. Contention on a budget is a sum against a bound over a window, and it is where DEFER 5.3's refund fallacy lands in physical form, since ten items each individually affordable is exactly ten refunds each individually under the ceiling.

### 8.1 Slots

**Every item MUST declare the slot it occupies. A slot MUST hold at most one item.**

**Failure mode:** a second item declared into an occupied slot is rejected at write time. The rejection names both items, so that the conflict is visible as a choice between two things rather than as an error on the second one. **An item with no declared slot is rejected at write time**, on 6.1's construction: without that clause the compliant response to this subsection is to decline to declare a slot, and an item with no slot never contends with anything.

**Slot exclusivity is protective and is carved out of section 8's coercive exemption.** It is a statement of physical fact rather than a source of pressure: two items cannot occupy one position however much money, attention, or time the operator has (2.5), and 3.5's justification for the exemption, that coercive rules generate pressure toward carrying fewer items, does not reach a fact about geometry.

**The clinical branch.** **Where one or both contending items are clinically directed, the write is not simply rejected. The conflict MUST be recorded and surfaced naming both items, the clinically directed item retains the slot, and no check returns a fail against it.** Where both are clinically directed, both are named and the conflict is surfaced undecided, for the operator and their clinician to resolve.

**Failure mode for the clinical branch:** an implementation that admits two items to one slot is non conformant, because the register then asserts a loadout that cannot exist and every computation reading it, loss exposure in 5.3, budget draw in 8.2, and `unused` in 10.2, runs against a fiction. An implementation that resolves the conflict by dropping, blocking, or auto reducing the clinically directed item is non conformant under inherited absolute 4 and under 8.4. This is 3.3's `fitted` pattern applied to contention: keep the fact, drop the pressure.

### 8.2 The budget declaration

**An operator MUST declare their budget meters and MAY declare a bound on each.**

**Every declared meter MUST be computable before the item is equipped**, per DEFER 5.1.

**A budget declaration MUST include at least one meter that is not `currency`.**

**A meter declaration takes the form DEFER 5.4 states, and this document does not restate it.**

**The shape of a bound is stated in two parts, so that the object is citable by a subject that holds no items.**

**Every declared bound MUST carry at least one windowed aggregate ceiling.** This half is general. It binds every bound on every meter, whatever the subject the draw is attributed to, and a document outside KIT may cite it for a bound over something that is not an item.

**Every declared bound whose subject is an item MUST additionally carry a per item ceiling.** This half is item scoped and binds only here.

**Failure mode:** a budget declaring only `currency` is rejected at write time. **A bound with no windowed aggregate ceiling is malformed and confers no bound**, so an implementation MUST NOT report a loadout as within budget against it. An item scoped bound carrying a windowed aggregate and no per item ceiling is malformed on the same terms. A meter measurable only after equipping is rejected, per DEFER 5.1.

Three inheritances, each doing distinct work.

**The meters named in the three paragraphs below are non normative illustrations of DEFER 5.1's computability test, and are not a recommended set.** KIT declares no meter set, and an implementation adopting the illustrated names because they appear here has read a worked example as a requirement.

DEFER 5.1 eliminates the tempting meters immediately. "Overwhelm" is not a meter and cannot be computed before the act. "Hours of maintenance per period" is a meter, is computable from the item's declared demands, and is exactly the resource an over equipped loadout consumes. Both are illustrations of the test and neither is prescribed.

DEFER 5.2 observes that currency is one meter and rarely the important one. A loadout bounded only on money declares a budget the operator was never spending against, while whatever the operator actually spends goes unbounded. The requirement for one non currency meter is a structural cardinality under K-A2 rather than a stated value: it fixes the shape of the declaration and names no meter the operator must adopt.

DEFER 5.3 is the whole point of the windowed aggregate requirement. Ten items each individually inside budget is the refund fallacy in equipment form: the policy text is correct about each individual item, each acquisition passes its check, and the aggregate is unbounded. A per item ceiling alone is not a bound, and this document says so in the same words DEFER does, because the failure is the same failure.

### 8.3 Budgets are the operator's

**A budget MUST NOT be declared by a party other than the operator.**

**Failure mode:** a budget declared by another party is rejected as a budget, and is recorded instead as an external requirement set naming its author. It remains visible, it remains attributable, and it does not function as the operator's declared bound.

A budget declared by an employer is a quota. The distinction is not rhetorical: a budget is a bound the operator sets on their own consumption and may revise, and a quota is a bound another party sets on the operator, which the operator's own governance should surface as an external constraint rather than absorb as a self declaration. Absorbing it hides the author, and the author is the fact that matters when the bound turns out to be the binding one.

### 8.4 Over equipment is reported and never blocked

**A loadout whose summed draw exceeds a declared bound on any meter MUST be recorded `over-equipped`, and MUST be surfaced at the next declared review. An implementation MUST NOT block, auto reduce, or drop an item from a loadout.**

**An operator declaring a budget MUST declare a loadout review interval alongside it.**

**Failure mode:** an over equipped loadout not surfaced by the next review is a health invariant failure, and the register is reported stale. **A budget declared with no loadout review interval is malformed, and an over equipped loadout under it is surfaced immediately rather than at a review that will never arrive**, with the register reported stale from the moment of the declaration. Without this clause the compliant response to this subsection is to declare no review, and "surfaced at the next declared review" never fires, so the invariant is satisfied by never reporting.

`over-equipped` is a reported state, never a failure, and never a score. **`over-equipped` MUST NOT be presented as a score, a magnitude, a percentage over bound, a grade, or an ordering across loadouts or across items.** **Failure mode:** an implementation presenting it in any of those forms is non conformant, the presentation is void, and the state is re rendered as the bare fact that a named bound on a named meter was exceeded.

POLARIS 5.2 already established the asymmetry this inherits: an obligation cannot fail closed, because there is no moment at which a party can be stopped from failing to have done something, so a commitment to act is reported as unmet rather than enforced by blocking. A budget bound is that shape exactly. DEFER 15.3 supplies the disposition and the phrasing discipline: exceeding a declared budget is a governance defect and MUST be reported as one, and it is not a busy month.

The refusal to auto reduce deserves its own sentence, because an implementer will read the requirement as a missing feature. Automatic reduction is a system deciding which of an operator's possessions they stop carrying. It is the same division this repository enforces when it says an agent drafts and the author decides, and it is a division that gets more important rather than less as the subject gets closer to the person.

### 8.5 No stated values

K-A2 restated in place, once, because this is the section where the temptation lives and where a future editor is most likely to help.

**KIT MUST NOT state the value of any meter, bound, threshold, target, schedule, or recommended loadout for any slot, meter, or budget.** Not a number of slots. Not a maintenance hour ceiling. Not a starter kit.
**Failure:** the specification text is non conformant and MUST be rejected in review.
**What this does not forbid:** an operator declaring their own values, which 8.2 requires. Nor a structural cardinality carrying no measurement, such as 8.1's one item per slot or 8.2's one non `currency` meter and one windowed aggregate ceiling per bound, per K-A2's boundary statement.

---

## 9. The Data Surface (protective)

This section is the model for how KIT stays short, and it is the clearest case in the document of delete and cross reference. **KIT MUST NOT restate any artifact class rule or any custody class rule.** It requires the fields, and the base documents supply the classification.

### 9.1 Enumeration is required

**Every item record MUST state whether the item retains data, whether it transmits, and to whom.**

**Where it retains, the record MUST carry the artifact class assigned under the TRACE for operators adapter. Where it transmits, the record MUST carry the endpoint's custody class determined under the CONFIDE for operators adapter.**

**Failure mode:** an undeclared retention posture is C4 Open, per CONFIDE 2.4, and an undeclared telemetry posture is treated as transmitting content, per TRACE 10.6. Fail closed in both directions: silence is never read as favorable, and an omitted field never widens what an item may hold or send.

**An item whose emitter posture is undeclared is C4 Open per CONFIDE 2.4, and MUST NOT be authorized for any use whose records declare a custody floor stronger than C4.** A **custody floor** is the weakest custody class a record may be held at, defined by CONFIDE and not redefined here. The direction is stated as "stronger than C4" rather than as "exceeding the C4 floor", because C4 is the weakest class on the ladder and the shorter phrasing reads equally naturally in the direction that would authorize exactly the emitters this subsection exists to stop.

**Transmission is a boundary crossing and carries a consequence class.** **Transmission of any record about the instrument to a party outside the operator's control is at minimum K3 under TETHER 3.2, MUST NOT proceed without a declared custody floor, and MUST NOT be covered by a standing pre classification per DEFER 6.6.**
**Failure mode:** a crossing with no declared custody floor is refused and the refusal is recorded. An implementation transmitting without one is non conformant at every tier. Item telemetry is the most routine crossing this family will ever see, and leaving it unclassified would have made the routine crossing cheaper to perform than the comparison crossing QUEST section 9 refuses, which is the inversion the shifted ladder exists to prevent.

**Registration, so that the classes 9.1 requires can actually be assigned.** **An item that retains data about the instrument MUST be registered with its declared artifact roots and a retention policy per class, per TRACE 3.2 and TRACE 4.1. An item that transmits MUST be registered as a CONFIDE provider under the TRACE 11.1 bridge and MUST carry the provider record CONFIDE 2.2 requires, with the evidence justifying its class in that same record. An item computing any number about the instrument MUST declare that number's maximum age, per TRACE 10.3, which forbids `indefinite`.**
**Failure mode:** an item that transmits with no provider record is non conformant and its endpoint is **C4 Open by construction**, which is also the honest default until the CONFIDE for operators adapter lands: **while that adapter is unwritten, every transmitting endpoint is C4 Open and no stronger class may be claimed.** An A2 output with no declared maximum age is malformed and is rejected at write time, since without it the expiry schedule 9.2 invokes cannot run.

The direction is inherited verbatim from CONFIDE 2.4 rather than reasoned afresh, because CONFIDE already settled it for providers and an item that transmits is a provider with a strap on it.

### 9.2 A computed number is a derived artifact, not an observation

**Any number an item computes about the instrument is an A2 Derived artifact under TRACE 3.1, and MUST NOT be admitted to the instrument register as an observation unless deliberately adopted.**

**Failure mode:** admitted without adoption, the entry is rejected at write time and expires on the A2 schedule per TRACE 10.3, which requires a declared maximum age and forbids `indefinite`.

**The adoption door carries a subject filter, and the filter lives upstream.** **A derived number whose subject is the operator's capability, or the operator and kit composite, rather than a measured property of the instrument, MUST NOT be adopted as an observation**, under the rule owned by the **TRACE for operators adapter** and enumerated in `spec/adapters/README.md`. **Failure:** the adoption is rejected at write time and the number remains an A2 derived artifact expiring on its declared schedule. The rule is drawn upstream of both siblings deliberately: a commercial readiness score, fitness age, or recovery index is a number over the operator and kit composite that a vendor will label as instrument telemetry, and without an upstream filter it enters through this subsection unchallenged, because K-A3 forbids KIT from citing QUEST's prohibition and KIT has none of its own. Drawn once, upstream, both documents cite one rule and K-A3 is not breached. **This citation is a forward citation into an unwritten adapter**, per 9.3.

Cite and stop. TRACE 10.3 states the reasoning and this document adds nothing to it.

One boundary is worth naming because it sits at the seam of two sections: 6.4 governs a **reading** from an item outside its calibration interval, and 9.2 governs a **computed number** an item derives about the instrument whatever its calibration state. An item can be perfectly calibrated and still emit a score, and the score is an A2 artifact rather than an observation because a model nobody can inspect produced it, not because the sensor drifted.

### 9.3 Forward citation notice

**This notice is document level and not local to section 9.** KIT places normative routing obligations on **five** unwritten operator adapters, and all five citations are forward citations: the **TRACE** and **CONFIDE** adapters in 9.1 and 9.2, and the **DEFER**, **SPEAK**, and **RETAIN** adapters in K-A1 and 3.4, which is where a party declared as an item is routed. None of the five exists, per `spec/adapters/README.md`.

Those citations are therefore **forward citations**. **KIT declares the field and delegates the classification.** KIT gains no rule of its own when the adapters land, and an implementation reaching Tier 3 before they land satisfies 9.1 by carrying the fields and applying the base documents directly, which is what the adapters will refine rather than replace.

---

## 10. The Inventory Register (10.1 protective, 10.2 coercive)

### 10.1 Possession is not evidence of a fault (protective)

**An item record MUST NOT be written to the fault register, mirrored into it, or cited as evidence of an instrument fault or of a recorded finding.**

**Failure mode:** the write or the citation is rejected. An implementation deriving fault register content from loadout content is non conformant, on the TETHER F1 pattern.

This requirement is narrow, and the narrowness is the point.

Without it, the loadout becomes a back door into the fault register. Possession of a substituting item is read as a recorded deficit, the deficit is inferred rather than found, and the inference then flows to every party that reads the fault register, with no clinician having made a finding and no operator having disclosed one. The inference is also frequently wrong, since an item may be held for a job that never arose, borrowed, inherited, or acquired for someone else, and none of those facts survive the inference.

**What this forbids and what it does not.** It forbids the inference, and it forbids nothing else. It does not forbid recording an item accurately, which sections 3 through 9 require. It does not forbid an operator disclosing a loadout, to anyone, for any reason. It does not forbid a clinician prescribing an item, and it does not forbid the item record carrying that direction, which 3.5 requires. It does not forbid a fault register entry that a clinician made, about an instrument, that happens to concern the same subject as an item. The prohibited act is the derivation: reading a possession as a finding.

This is a narrower requirement than the identity firewall and is not a second copy of it. The firewall governs the operator register and is inherited unchanged, in one line, in the Conformance section. This governs the fault register, which is a different register with a different failure, and the pending RFC generalising TETHER 4.1 does not make this section redundant when it lands.

### 10.2 An unused item is not an owned capability (coercive)

**Every item MUST declare a review interval. An item with no recorded application inside its review interval MUST be recorded `unused`, and MUST NOT be counted as satisfying the named capability label it was declared against, or any loadout requirement.**

**An item declared for a contingency MUST declare a readiness verification in place of a use record, and a readiness verification inside the interval satisfies this section.**

**Failure mode: an item with no declared review interval MUST be recorded `unused` from the moment of its declaration**, on 6.1's construction. Without that clause the compliant response to this subsection is to decline to declare a review interval, and no item ever becomes `unused`.

**Failure mode:** the item reads `unused` and the loadout MUST NOT be reported as supplying the named capability it was declared against, inheriting HABITAT section 3's direction that an undeclared class is unprovisioned rather than sufficient. An implementation counting inventory presence as capability is non conformant. **KIT records the item side fact and assigns no capability state**, per K-A3 and 2.2; the label of 2.2 is opaque and carries none.

**Both failure modes in this subsection are coercive and return `out-of-scope` against a clinically directed item**, including the undeclared interval disposition, since an interval an operator never declared is not grounds for marking a prescribed item unused.

POLARIS 4.5's dead refusal problem transfers to objects with the same indistinguishability. An item never applied is either perfectly suited to a job that never arose, or it was the wrong item from the day it was acquired and has been inert ever since. From the outside those look identical, and the second is common. POLARIS's resolution, which is to test the thing on an interval rather than to infer from its silence, is the resolution here.

The readiness carve out exists because a contingency item is the honest third case. An emergency supply, a spare, a backup: these are correctly never applied, and their non application is the desired outcome rather than evidence of anything. A document without the carve out would report an unopened emergency kit as a defect, which is both wrong and the kind of wrong that teaches an operator to ignore the report.

**This section is coercive and does not reach a clinically directed item**, per 3.5.

---

## 11. Failure Classes (each row inherits the label of its governing section)

Each stated as what an implementation does when the requirement is violated. A row's coercive or protective label is the label of the section named in its disposition, and a row whose governing section is coercive does not reach a clinically directed item, per 3.5.

| Code | Failure | Disposition |
|---|---|---|
| `KT-01` | Item record with no declared custody holder | Treated as held by a third party. Fail closed. Section 3.1 |
| `KT-02` | A thing whose removal is K2 or above under TETHER 3.2 recorded as an item alone | Rejected as an item record at write time. Reopened as an intervention record. Section 3.2 |
| `KT-03` | `fitted` item carrying only one of the item record and the intervention record | Malformed. Rejected at write time. Section 3.3 |
| `KT-04` | A party declared as an item, placed in a slot, or counted against a budget | Rejected at write time. Routed to the DEFER, SPEAK, or RETAIN adapter per the relationship. K-A1 |
| `KT-05` | A coercive class check resolved against a clinically directed item | Returns `out-of-scope`. Never a pass, never a fail. Section 3.5 |
| `KT-06` | Item record with no declared kind | Written as `substitute`. Stricter handling. Section 4.1 |
| `KT-07` | `substitute` item with no declared loss posture | Rejected at write time. If the item is absent, it is dispositioned under 5.2 and thresholds depending on its output are `unevaluated`. KIT assigns no capability state, K-A3. Section 4.2 |
| `KT-08` | A declared permanent dependency reported as unsatisfied, deficient, or unmet | The check is malformed specification text and MUST be rejected as non conformant. Section 4.3 |
| `KT-09` | `trial` item with no exit condition or no evaluation window | Rejected at write time, on the TETHER F4 pattern. Section 4.4 |
| `KT-10` | An exit condition required of an item not declared `trial` | The requirement is non conformant. Section 4.3 |
| `KT-11` | Confirmation interval lapsed and the past confirmation treated as continuing satisfaction | Non conformant, in the TETHER F3 disposition. The item is `unconfirmed`. KIT assigns no capability state, K-A3. Section 5.1 |
| `KT-12` | Item absent from the loadout with no recorded disposition | Fails closed to `lost`. KIT assigns no capability state, K-A3. Section 5.2 |
| `KT-13` | `released` recorded as `lost`, or `lost` recorded as `released` | Non conformant record, in the TETHER F5 disposition. Section 5.2 |
| `KT-14` | `substitute` item missing replacement latency, replacement cost, or provisioning party | Rejected at write time. An undeclared latency reads unbounded. Section 5.3 |
| `KT-15` | `substitute` item at external custody with no declared fallback reported as an adequate loadout | Non conformant. Surfaced as an undeclared single point of failure. Section 5.3 |
| `KT-16` | Capability loss from an `unprovisioned` item attributed to the instrument while the provisioning party is another party | Recorded `unattributed`, HABITAT **H5**. Routed under HABITAT section 7. Forward citation into an unwritten HABITAT section. Section 5.4 |
| `KT-17` | Item of class `sensor` with no declared calibration interval, or no declared measurement pipeline version | Out of calibration from the moment of declaration. Output `unknown`. Section 6.1 |
| `KT-18` | Calibration reference produced by the item, by its population, or by any party in its custody or supply chain | Calibration record rejected at write time. Calibration state remains lapsed and the interval does not reset. Section 6.2 |
| `KT-18a` | Calibration interval carried across a change to the declared measurement pipeline version | Non conformant. The interval is treated as never reset and the item is out of calibration. Section 6.1 |
| `KT-19` | Stale reading from a lapsed sensing item displayed, carried forward, or interpolated as current | Fail closed to `unknown`. Section 6.3 |
| `KT-20` | Output from a lapsed sensing item written to the instrument register as an observation | Write rejected. Recorded as an item condition entry in the item's own record, carrying its four required fields. The instrument condition lapses to `unevaluated` by the ordinary mechanism. Section 6.4 |
| `KT-21` | Output recorded `unknown` closing a TETHER 7.3 rung gate or supporting a threshold gating K2 or above | The gate is `unevaluated`, never `passed`, per TETHER F3. The threshold is `unevaluated` and the act is unauthorized, per TETHER F2. Section 6.5 |
| `KT-22` | Observation citing a sensing item without the item identifier and its calibration currency | Malformed. Rejected at write time. Section 6.6 |
| `KT-23` | Job declared as a predicate requiring judgement to evaluate | Not a job, per DEFER 4.3. The predicate is empty and every application is off job. Section 7.1 |
| `KT-24` | Off job application unrecorded | An unrecorded act, DEFER DF-10. A later fault is recorded `unattributed`, HABITAT H4. Section 7.2 |
| `KT-25` | Off job application classified at the item's ordinary class rather than on the target, or covered by a standing pre classification | Classification defect on the DEFER DF-16 pattern. The act is unauthorized and the class is recomputed on the target under DEFER 6.1. No class floor is asserted. Section 7.3 |
| `KT-26` | A second item declared into an occupied slot | Rejected at write time, naming both items. Where one or both are clinically directed, the conflict is recorded and surfaced naming both, the clinically directed item retains the slot, and no check returns a fail against it. Section 8.1 |
| `KT-26a` | Two items admitted to one slot, or a clinically directed item dropped, blocked, or auto reduced to resolve a slot conflict | Non conformant. The register MUST NOT assert a loadout that cannot exist, and MUST NOT resolve contention against a clinically directed item. Section 8.1 |
| `KT-26b` | Item with no declared slot | Rejected at write time. Section 8.1 |
| `KT-27` | Budget declaring only the `currency` meter | Rejected at write time. Section 8.2 |
| `KT-28` | Declared bound carrying no windowed aggregate ceiling, or an item scoped bound carrying no per item ceiling | Malformed. Confers no bound, and a loadout MUST NOT be reported as within budget against it. DEFER 5.3. Section 8.2 |
| `KT-29` | Budget declared by a party other than the operator | Rejected as a budget. Recorded as an external requirement set naming its author. Section 8.3 |
| `KT-30` | Over equipped loadout blocked, auto reduced, or silently dropped from | Non conformant. `over-equipped` is reported and surfaced at the next review, never enforced. Section 8.4 |
| `KT-31` | Over equipped loadout not surfaced by the next declared review | Health invariant failure. The register is reported stale. Governance defect per DEFER 15.3. Section 8.4 |
| `KT-31a` | Budget declared with no loadout review interval | Malformed. Over equipment under it is surfaced immediately and the register is reported stale from the declaration. Section 8.4 |
| `KT-31b` | `over-equipped` presented as a score, a magnitude, a percentage over bound, a grade, or an ordering | Non conformant. The presentation is void and the state is re rendered as the bare fact of a named bound exceeded. Section 8.4 |
| `KT-32` | Item with an undeclared emitter authorized for a use whose records declare a custody floor stronger than C4 | Non conformant. Undeclared retention is C4 Open per CONFIDE 2.4, undeclared telemetry transmits content per TRACE 10.6. Section 9.1 |
| `KT-32a` | Record about the instrument transmitted to a party outside the operator's control with no declared custody floor, or under a standing pre classification | Refused, and the refusal recorded. K3 minimum under TETHER 3.2, no standing pre classification per DEFER 6.6. Section 9.1 |
| `KT-32b` | Transmitting item with no CONFIDE provider record under the TRACE 11.1 bridge, or a class stronger than C4 Open claimed while the CONFIDE adapter is unwritten | Non conformant. The endpoint is C4 Open by construction. Section 9.1 |
| `KT-33` | A number an item computed about the instrument admitted to the instrument register as an observation without adoption | Rejected at write time. Expires on the A2 schedule, TRACE 10.3. Section 9.2 |
| `KT-33a` | An A2 output with no declared maximum age, or declared `indefinite` | Malformed. Rejected at write time, so that the TRACE 10.3 schedule is executable. Section 9.1 and 9.2 |
| `KT-34` | An item record written to, mirrored into, or cited as the fault register | Rejected, on the TETHER F1 pattern. Section 10.1 |
| `KT-35` | An item with no recorded application or readiness verification inside its review interval counted as satisfying a capability label or a loadout requirement | Non conformant. The item is `unused` and the loadout is not reported as supplying the label. KIT assigns no capability state, K-A3. Coercive. Section 10.2 |
| `KT-35a` | Item with no declared review interval | `unused` from the moment of declaration. Coercive, so `out-of-scope` against a clinically directed item. Section 10.2 |
| `KT-36` | Specification text stating the **value** of a meter, bound, threshold, target, schedule, or recommended loadout | Non conformant text. Rejected in review. A structural cardinality carrying no measurement is not a stated value and is not a `KT-36` defect. K-A2 |
| `KT-37` | Specification **prose** using the reserved word `instrument` for a device | Malformed. Rejected in review. The TETHER 2.3 vocabulary value `instrument` is excepted by name and is not a `KT-37` defect. Where the ambiguity reaches a record, the observation is `unevaluated`. Section 1.5 |
| `KT-38` | A KIT requirement citing, requiring, or conditioning on a QUEST element | Non conformant specification text. Rejected in review. Checkable mechanically. K-A3 |
| `KT-39` | A fail closed state named for a deficiency in the operator | Non conformant register. Specification text defining one is rejected in review. Section 2.11 |
| `KT-40` | A game term used outside the closed vocabulary of 2.12, or a class (b) term used as a property of an operator | Non conformant vocabulary. Rejected in review. Admission is an RFC. Section 2.12 |
| `KT-41` | Item record whose clinical direction field is absent or `unknown` | Handled as clinically directed until the operator declares otherwise, and surfaced `unconfirmed` on that field. Never assumed non clinical. Fail closed toward protection. Section 3.5 |
| `KT-42` | Item record with no declared class | Handled as class `sensor` where it produces any output about the instrument, and rejected at write time otherwise. Section 4.1 |
| `KT-43` | A report reducing loss exposure across items to a single figure, a total, a magnitude, or an ordering | Non conformant. The figure is void and the report is re rendered as an unordered per item enumeration. Sections 5.3 and 12.2 |
| `KT-44` | A report ranking, totalling, or flagging permanent dependencies | Non conformant. The ranking or total is void and the report is re rendered as an unordered per item enumeration of declared facts. Section 4.3 |
| `KT-45` | Any report field that is a scalar computed across items about the operator | Non conformant at every tier. The field is void, is not returned, and the report resolves to the enumeration it would have summarized. Sections 4.3, 5.3, 8.4 |
| `KT-46` | An implementation surfacing no loss exposure entry for a `substitute` item | Loss exposure was not computed. Non conformant, and the loadout MUST NOT be reported as adequate. Section 5.3 |
| `KT-47` | An item whose application is an act undertaken to change the instrument's condition, recorded with no accompanying intervention record | Malformed. Rejected at write time, on the 3.3 pattern. TETHER 2.4's four elements bind the intervention record and never the item record. Section 3.2 |

---

## 12. Conformance (12.1 and 12.2 mixed, 12.3 protective)

Section 12 states requirements on an implementation rather than on an item, and its coercive content is exactly the content that references a coercive body section. Where a tier item or a health invariant in 12.1 or 12.2 depends on section 4.4, 8, or 10.2, it is coercive and resolves `out-of-scope` against a clinically directed item, per 3.5. Section 12.3 is protective by construction: it is a requirement of this document that no self test check be satisfiable by discontinuing a clinically directed item.

### 12.1 Tier requirements

Three tiers, named to mirror TETHER. Requirements are indicative in this draft.

**Tier 1, Attended.** The inventory register exists and is separate from the operator, instrument, and fault registers. Every item declares its kind, its class, its job, its custody holder, its slot, its confirmation interval, its review interval, and **its clinical direction field**, whose absence is handled as clinically directed and surfaced `unconfirmed` per 3.5. Every item leaving the loadout carries a disposition. No party is declared as an item. No report field is a scalar computed across items about the operator.

**Tier 2, Referenced.** Adds the mechanism that makes Tier 1 more than an inventory. Calibration intervals are declared for every `sensor` item and enforced. Output from a lapsed sensing item is `unknown`, is rejected at write time to the instrument register, and closes no gate. Loss exposure is computed per substituting item and items at external custody are surfaced. Budgets are declared with at least one non currency meter and a windowed aggregate on every bound, and over equipment is reported.

**Tier 3, Governed.** Adds the boundary. The data surface is enumerated and classified under the TRACE and CONFIDE adapters, or against the base documents directly while those adapters are unwritten, with every transmitting endpoint C4 Open by construction until the CONFIDE adapter lands. **Transmission of a record about the instrument to a party outside the operator's control is classified at minimum K3, carries a declared custody floor, and is refused without one.** Retaining items are registered with declared artifact roots, transmitting items carry a CONFIDE provider record under the TRACE 11.1 bridge, and every computed number about the instrument declares its maximum age. Provisioning parties are named and supply failures are routed under HABITAT section 7. Off job applications are recorded and classified on the target.

**Tier 1 KIT conformance is reachable with no QUEST record of any kind**, and so is Tier 3. This is stated here, where implementers read tiers, so that nobody infers from the family's shape that the two documents bind together. K-A3 is the requirement; this is the reminder.

### 12.2 Health invariants

The invariants are stated in two blocks, because a single blanket rule was wrong for half of them. **Every invariant in both blocks MUST be checked on a declared interval.** What happens on a red check differs by block, and the difference is the whole reason for the split.

**Block A. Fail closed, target 0.** Each of these MUST fail closed on a red check.

| Invariant | Target |
|---|---|
| Items with no declared custody holder | 0 |
| Parties declared as items | 0 |
| `substitute` items with no declared loss posture | 0 |
| `substitute` items with no loss exposure entry surfaced | 0 |
| Item records with an absent or `unknown` clinical direction field, not handled as clinically directed | 0 |
| Item records with no declared class, accepted rather than handled as `sensor` or rejected | 0 |
| Items with no declared confirmation interval, not reading `unconfirmed` | 0 |
| Items with no declared review interval, not reading `unused` | 0 |
| Items with no declared slot, accepted | 0 |
| Budgets declared with no loadout review interval, accepted | 0 |
| Reads served from a sensing item past its calibration interval carrying any value other than `unknown` | 0 |
| Sensing items whose calibration reference is produced by the item, its population, or a party in its custody or supply chain | 0 |
| Sensing items with no declared measurement pipeline version, or carrying an interval across a version change | 0 |
| Item records written to, mirrored into, or cited as the fault register | 0 |
| Items absent from the loadout with no recorded disposition | 0 |
| Coercive checks resolved against clinically directed items as pass or fail rather than `out-of-scope` | 0 |
| Slots holding more than one item | 0 |
| Declared bounds carrying no windowed aggregate | 0 |
| Transmitting items with no CONFIDE provider record | 0 |
| A2 outputs about the instrument with no declared maximum age | 0 |
| Crossings of a record about the instrument with no declared custody floor | 0 |
| **Report fields that are a scalar computed across items about the operator** | **0** |
| Reports that rank, order, or total items, permanent dependencies, or loss exposure | 0 |
| Over equipped loadouts not surfaced by the next declared review | 0 |

The display invariant is stated as a register property (reads served carrying a value other than `unknown`) rather than as a property of a user interface, because a register based checker cannot observe a screen, and 6.3's three prohibited fallbacks make the register form decidable.

**Block B. Reported, and these MUST NOT block.** Each MUST be surfaced at the declared review and **MUST NOT** cause an implementation to block, auto reduce, or drop anything, per 8.4 and per POLARIS 5.2's rule that an obligation cannot fail closed. A red check here is a report to the operator and never an enforcement.

| Invariant | Target |
|---|---|
| Over equipped loadouts | reported, enumerated |
| `substitute` items at external custody with no declared fallback | reported, enumerated |
| Items `unused` past their review interval | reported, enumerated |

An over equipped loadout and an externally held dependency are facts about an operator's life that this document surfaces and does not correct. **No invariant's report in either block may impose an ordering over items or over the operator's possessions**, per 4.3 and 5.3: an ordering requires a comparable per item magnitude, and that magnitude is the scalar 5.3 exists to prevent, arriving through a word in a table rather than through a reviewed requirement. Reporting is enumerated per item and MUST NOT be reduced to a summary figure.

### 12.3 Self test

One page. Every check is mechanically decidable, and every check is one no operator can satisfy by discontinuing a clinically directed item. A conformant implementation seeds each case and asserts refusal or detection, exiting non zero on failure.

1. A reading from a `sensor` item past its calibration interval, written to the instrument register. Assert the write is rejected and the reading lands as an item condition entry in the item's record, carrying its four required fields. Failure: `KT-20`.
2. A calibration record whose reference is the item's own reading history. Assert rejection and that the calibration state remains lapsed and the interval did not reset. Failure: `KT-18`.
3. An `unknown` reading offered to a TETHER 7.3 rung gate. Assert the gate resolves `unevaluated` and not `passed`. Failure: `KT-21`.
4. An item absent from the loadout with no recorded disposition. Assert it reads `lost`, and assert that the implementation writes no capability state of its own. Failure: `KT-12`.
5. A `substitute` item declared with no loss posture. Assert rejection at write time. Failure: `KT-07`.
6. A dependency declared `permanent`, offered to a health check. Assert the check does not report it as unsatisfied, deficient, or unmet. Failure: `KT-08`.
7. A party declared as an item. Assert rejection at write time, and assert the presence of a routing record naming the relationship class (handover grant, agreement, or engagement). The routing record is decidable against the artifact today and stays correct when the DEFER, SPEAK, and RETAIN adapters land. Failure: `KT-04`.
8. A budget declared with `currency` as its only meter. Assert rejection. Failure: `KT-27`.
9. A budget bound declared with a per item ceiling and no windowed aggregate, followed by a sequence of individually compliant acquisitions. Assert the bound confers nothing and the loadout is not reported as within budget. Failure: `KT-28`.
10. A loadout exceeding a declared bound. Assert it was recorded `over-equipped` and surfaced at the next review, and assert that no item was blocked, auto reduced, or dropped. Failure: `KT-30` or `KT-31`.
11. An off job application classified at the item's ordinary class. Assert the classification is recomputed on the target and that the act is unauthorized until it is. Failure: `KT-25`.
12. An item record offered to the fault register, and separately, a fault register entry derived from loadout content. Assert both are rejected. Failure: `KT-34`.
13. A coercive check, from sections 4.4, 8, or 10.2, resolved against a clinically directed item. Assert it returns `out-of-scope`, and assert specifically that it returns neither a pass nor a fail. Failure: `KT-05`.
14. An item record seeded with the clinical direction field **absent**, and separately with it declared `unknown`. Assert a coercive check returns `out-of-scope` against both, assert neither returns a pass or a fail, and assert the field is surfaced `unconfirmed` rather than the item being treated as non clinical. Failure: `KT-41`.
15. An item record with no declared class that produces output about the instrument, and one with no declared class that produces none. Assert the first is handled as `sensor` and therefore falls under section 6, and assert the second is rejected at write time. Failure: `KT-42`.
16. Three `substitute` items seeded at external custody, each with a declared loss posture and no declared fallback. Assert the report is a per item enumeration of exactly three entries, assert there is **no cross item total, sum, index, or summary figure**, and assert the entries carry **no ordering**, including no default sort by latency, cost, or any other magnitude. Failure: `KT-43` or `KT-45`.
17. A slot conflict seeded between a clinically directed item and an ordinary one. Assert the register does not record both as occupying the slot, assert the conflict is recorded and surfaced naming both items, assert the clinically directed item retains the slot, and assert no check returned a fail against it. Failure: `KT-26a`.
18. A record about the instrument offered for transmission to a party outside the operator's control with no declared custody floor. Assert refusal, assert the refusal is recorded, and assert the act was classified at minimum K3 with no standing pre classification applied. Failure: `KT-32a`.

Cases 1, 2, 3, 4, 9, and 10 require elapsed intervals, windows, or accumulated aggregates. **A simulated clock is conformant for the self test, provided the implementation under test reads time only through the source the simulation controls**, per DEFER 15.4. A test that advances a clock the production code does not read has tested a different system, and its pass is not evidence.

---

## 13. Versioning and Governance (neither coercive nor protective)

This section states no requirement about an item and therefore carries neither label. It is labelled explicitly rather than left blank, because the drafting requirement treats an unlabelled section as coercive and an unlabelled governance section would be a check nobody can evaluate.

Semantic versioning on the specification, per `CONTRIBUTING.md`. Substantive changes go through an RFC. Admitting a term to the closed vocabulary of section 2.12, or a class to the vocabulary of section 2.13, is a substantive change and requires an RFC.

While Status reads Draft, section numbering, requirement identifiers, and failure class codes are unstable and MUST NOT be cited as stable by any other document in this stack. A document permitted to cite KIT is citing a moving document until this Status changes. The permitted citation direction is fixed by K-A3 and does not move with the numbers.

The instruction that the DEFER for operators adapter cite KIT section 8 for the budget object rather than duplicating it now lives in `spec/adapters/README.md`, alongside the other inbound obligations KIT and QUEST place on the adapter set. It is not restated here, because a MUST placed by one document on another that does not yet exist binds nobody, and the adapters README is where the set is reviewed as a set.
