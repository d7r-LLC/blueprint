# Meat Suit Interface: design note for the eighth document

**Status:** Design note. Non normative. Options and open questions belong here, not in `spec/`.
**Author:** Spencer Thornock
**Written:** 2026-08-30
**Proposes:** `spec/TETHER-v1.0.md`, plus schema, profile, skills, and operator guides.

---

## 1. The argument for admitting this to the stack

The stack currently has a hole at its root, and the hole is load bearing.

RETAIN says every chain of grants terminates in a human signature. DEFER says K4 constitutional acts are owner only. POLARIS says the owner declares the purpose and the refusals. BLUEPRINT says the owner holds the signing key. Seven documents, and every one of them resolves upward into a human being who is never specified.

That human is an instrument. It has an operating envelope, sensors that degrade, a chemistry that drifts, and exactly one instance with no backup. When it is outside its envelope, the signature it produces is still cryptographically valid and still authorizes the act. Every gate below it passes. The ledger is clean. This is precisely the failure POLARIS 1.1 names for purpose ("every check passes and the outcome is wrong"), relocated one layer further down, to the only layer the stack has so far treated as a constant.

The one sentence thesis, in the form the other documents use:

> An operator is not the instrument it perceives through, the instrument's condition determines the fidelity of every judgment made through it, and no authority the operator delegates may exceed the instrument's declared operating envelope.

Two consequences follow, and they are why this is a specification and not an essay.

**First, the root signer is governable.** Not the body's biology, which is not ours to legislate, but the *form* in which its condition is declared, measured, recorded, and used to bound authority. That is exactly the kind of thing this stack specifies: it does not specify what you believe, it specifies that a belief must be decidable before it may be cited.

**Second, this is where the whole stack becomes teachable.** The design note 0000 already found that D7R-1 Explorer, D7R-2 Operator, D7R-3 Architect map onto Sovereign, Governed, Federated with almost no strain. The name of the middle tier is *Operator*. The curriculum has been calling the learner an operator for months without ever specifying what they are operating. This document answers that, and it does so at the level a beginner can actually enter, because everybody already owns the instrument.

### Where it sits

POLARIS holds the highest precedence to forbid and none to permit. This document sits **beside** POLARIS at the root, not above it, and inherits the same asymmetry. An instrument condition may narrow what an operator is authorized to do. It may never widen it, never satisfy another document's check, and never excuse a failure. "I was in a good state" authorizes nothing. "I was outside the envelope" is a valid bound and never a valid excuse after the fact.

The precedence sentence to add to the README:

> TETHER specifies the operator at the root of every authority chain: what is operator and what is instrument, how the instrument's condition is observed without trusting it to observe itself, and how authority is bounded by an envelope that the operator declares in advance and cannot widen in the moment.

### This is a family, not a document

Author direction, 2026-08-30, in two parts, and both change the shape of the proposal.

**First, the six governance documents each need an operator adapter.** POLARIS, DEFER, SPEAK, CONFIDE, TRACE, and RETAIN are all written for a subject that is a folder. Every one of them has a true and non obvious reading when the subject is an instrument and a life, and none of those readings is derivable by a reader substituting nouns. The adapters are section 9.

**Second, there must be a DERP analogue for the environment.** This one is already ruled. The author's spec alignment map (`<vault>` `d7r/Areas/Specifications/2026-08-26 - Human System as a Computer Spec Alignment.md`, ruling 1, 2026-08-26) states that **DERP maps to the environment and not to the body**, with the body and hardware row keeping the host and Layer 9. So the runtime document has a place waiting for it in the author's own alignment work, and this note is not inventing the slot, only filling it. It is proposed here as **HABITAT**, section 8.

The result, as of the 2026-08-30 drafting round, is **five normative documents and six adapters**. The count was two when this note was first written, and KIT, QUEST, and BEARING were drafted afterward against the same author direction. All three cite this note as their design note.

| Document | Subject | Digital counterpart |
|---|---|---|
| **TETHER** | the interface between an operator and the instrument it perceives through | BLUEPRINT |
| **HABITAT** | the environment the instrument runs in, and what it must provide | DERP |
| **KIT** | what the operator interposes between the environment and the instrument: kind, integrity, tenure | (no single counterpart) |
| **QUEST** | the form of an operator's capabilities and objectives | (no single counterpart) |
| **BEARING** | alignment calibration: the standing gap between recorded conduct and declared purpose, monitored automatically and reviewed by the operator | POLARIS sections 4.5, 5.3, and 11.5, which mandate three periodic reviews and specify a mechanism for none of them |
| six adapters | operator readings of the six governance documents | POLARIS, DEFER, SPEAK, CONFIDE, TRACE, RETAIN |

KIT and QUEST are siblings with a one way dependency: QUEST may cite KIT, KIT may never cite QUEST, and full KIT conformance is reachable with no capability, node, or quest declared anywhere. Both place normative routing obligations on five of the six adapters, enumerated in `spec/adapters/README.md`.

**BEARING is a leaf and the direction is absolute rather than conventional.** BEARING may cite every document in the family and no document in the family, and no adapter, may cite BEARING. Its B-A1 makes non coercion a property of the dependency graph rather than a promise, and its own routing obligations reach the sixth adapter, so all six now carry an inbound obligation before any of them is written.

TETHER is the brain. HABITAT is the runtime. The adapters are the governance, re read.

---

## 2. Naming

The suite names each document with an acronym that spells its function. Candidates, with the recommendation first.

**TETHER (recommended).** Telemetry, Envelope, Thresholds, Handover, Escalation, Restoration. The six things the document actually governs, in the order it governs them. The word is the reference implementation's own vocabulary for the operator to instrument relationship, and it carries the right physical connotation: a tether is a real connection, it has a length, and it constrains both ends. It also avoids claiming a metaphysics. A tether is observable from the instrument side whatever you believe is on the other end of it, which is the posture section 4 argues the document must take.

**VESSEL.** Vitals, Envelope, Sensors, State, Escalation, Limits. Fits, but "vessel" names the instrument rather than the relationship, and the relationship is the subject.

**SOMA.** Sensors, Operating envelope, Modulation, Authority. Short and clean, but the word carries a Huxley association that reads as sedation, which inverts the document's entire argument.

**CHASSIS.** The reference implementation uses the word. It names a part, not a relationship, and it has no acronym expansion worth having.

Recommendation: **TETHER**, with "the meat suit interface" as the plain language name used in guides and courseware, the same way "a brain" is the plain language name for what BLUEPRINT specifies. Keep "meat suit" in the teaching material and out of the normative text. The phrase does real work in a podcast and would cost the specification its readership in any clinical or institutional setting.

---

## 3. Ten insights that shape the design

Same form as design note 0000. These are the load bearing observations, and each one produces a requirement.

**1. One instance, no fork, no restore.** A brain can be copied, branched, and rolled back. The instrument cannot. Every act on it is at minimum K2 irreversible internal, and any act with a systemic or developmental effect is K3 or K4 even though it crosses no organizational boundary. **The consequence ladder does not transfer unchanged from DEFER; it shifts up by one class.** This is the single largest structural difference and the document should say so early.

**2. The auditor runs on the audited hardware.** Self assessment of instrument condition is produced by the instrument being assessed. Degraded sensors report their degraded readings as normal, because they have nothing to compare against. The reference implementation states this exactly: the operator drove for years unable to read road signs and experienced it as ordinary vision, and discovered the deficit only against an external reference. **Self report is a signal and never a verdict.** Every consequential threshold needs at least one reference external to the instrument.

**3. Adaptation conceals degradation, so drift is silent.** The system recalibrates around a deficit and reports the new state as baseline. Absence of a complaint is therefore not evidence of function, and no event driven check will fire, because nothing ever presents as an event. **Re referencing must be periodic and scheduled, not triggered.** This is the same finding as design note 0000 insight 10, that every mechanism requiring standing attention will rot, arriving from the opposite direction: here the mechanism rots *and reports itself healthy*.

**4. Latency exceeds the window operators will wait.** An intervention may take months to express an effect. The reference implementation's freight train image is the plain statement of it. Operators abandon inside the window and record the abandonment as failure, which poisons the register for every future decision. **The evaluation window is declared before the intervention starts, and abandonment inside it is recorded as abandonment, never as evidence of ineffect.**

**5. Environment mismatch is the default condition.** The hardware's design envelope was set by an environment the operator no longer inhabits. A fault is therefore tested against the envelope before it is attributed to the instrument. Stated generally, this is the strongest single idea the reference implementation contributes: a system performing badly outside its declared operating conditions is not a faulty system, and calling it one licenses the wrong repair.

**6. A fault report is never an identity.** The operator is not the instrument, so a record about the instrument's condition is a record about the instrument. When a fault register is merged into an identity register the operator acquires the fault as self description, and every subsequent act is bounded by a property of the hardware rather than a decision of the operator. **This is the document's load bearing refusal**, and it needs to be absolute and non configurable, in the way POLARIS makes three of its requirements absolute.

**7. Expertise is authority over the protocol, never over the purpose.** A clinician holds real, delegated, bounded authority and the document must not undercut it. What the clinician does not hold is the operator's root. Compliance is a posture the operator adopts deliberately and may revise through a declared handover. The reference implementation holds both halves at once, which is the correct position and the hard one to write: follow the protocol, take it seriously, do the blood draws, and remain aware that the expert is inside the same system you are.

**8. An intervention with no exit condition is an undeclared permanent state change.** Anything applied to the instrument is declared with what it is for, what it costs, and what would end it. Absent an exit condition, an intervention selected for a bounded purpose silently becomes a permanent property of the system, and the developmental case is the severe one, because the system forms around the intervention and there is no unmodified state to return to.

**9. Order of operations is load bearing and cheap to get wrong.** An instrument that cannot function cannot be optimized, and optimization applied at the wrong rung is wasted. Ladder: stabilize, function, baseline, calibrate. The document specifies the ladder and the gate between each rung, and specifies nothing about what an operator does on any rung.

**10. There is no universal protocol, and the document must be built so that there cannot be.** Two conformant operators may run contradictory protocols. **TETHER governs the form of a protocol and never its content.** This is not modesty. It is the same rule that makes POLARIS work: the specification tests whether a declared element is decidable, and never whether it is correct.

---

## 4. The posture problem, and how to write it

The document has to say what an operator is without ruling on what an operator *is*, and this is the one place where a careless sentence costs the whole thing its credibility.

The reference implementation's framing is explicitly metaphysical: a consciousness tethered through quantum connection, receiving a three dimensional linear time signal through a biological filter, where the fidelity of the hardware sets the fidelity of the experience. That belief is real, it is the author's, and it is publishable as a belief. It cannot be a normative requirement, because a specification that requires you to hold a metaphysics is a creed and conformance to it is membership.

The resolution is the enforceability test POLARIS already established. Take the operator instrument distinction as a **structural posture** rather than a claim about substance, and require only what the posture makes decidable:

- **What is normative.** There exist two registers, an operator register and an instrument register, and no record may be written to both. The instrument's condition bounds authority. Instrument records never enter the identity register. Self report is not a verdict on the instrument. These are all testable, and all of them hold whether the operator believes they are an eternal soul or an emergent process.
- **What is non normative and marked as such.** What the operator *is*. POLARIS 7.3 already built the mechanism for exactly this: a motto is kept because compression aids recall and is forbidden as grounds for any decision. The tethered self, the meat suit, the ghost on a rock hurtling through space: these are excellent, they belong in the guides and the courseware, and they may never be cited as authority for an act.

So the document reads as: whatever you are, you are not the thing you are looking through, and the following consequences are testable. An operator who holds the full metaphysics and an operator who holds none can both conform, which is the property that makes it a specification.

### The safety posture, stated normatively

This is health adjacent and it must be handled in the normative text, not in a footer, and not as a disclaimer that reads as liability management.

TETHER specifies the governance form of instrument operation. It specifies no protocol content, no threshold value, no dosage, no clinical criterion, and it is not medical advice, medical direction, or a substitute for either. Where TETHER and a licensed clinician's instruction bear on the same act, **the clinician governs what is done and TETHER governs only who was authorized to decide it and how it was recorded.** A conformant implementation that ever resolves the other way is non conformant, and this should be one of the absolute requirements alongside the identity firewall.

Two further absolutes, both from insight 2 and both genuinely protective:

- A crisis escalation path MUST NOT be gated on the operator's own assessment of whether escalation is warranted, because in crisis the assessing hardware is the failing hardware. The path is declared in advance, in a known state, and it fires on external criteria.
- The document MUST NOT define a conformance requirement that an operator could satisfy by declining care. Any tier requirement that could read as pressure to reduce or discontinue a clinical intervention is malformed. Restoration is a direction the operator may hold, never an obligation the specification imposes.

That last one is the difference between this document and the genre of wellness content it will otherwise be mistaken for. Worth stating in the abstract.

### Binding constraints inherited from the reference implementation's canon

The reference implementation has already ruled on this vocabulary, once, in an accepted record. These are not suggestions and a draft that violates one is wrong rather than merely different.

1. **Body, never being.** The claim is that a human *body* is a computer. "A human being is a computer" is imprecise and may not be used without qualification. TETHER inherits this: the instrument is the body, and the operator is not a layer of it.
2. **Consciousness is never a layer of the machine.** It is tethered to the stack and sits outside it. Any layer table that lists the operator as the top layer has reproduced the error the canon exists to prevent.
3. **The hedge is load bearing and survives.** The coupling is described as being by "some mechanism such as" quantum entanglement. Entanglement does not transmit information, so a flat assertion of the mechanism is disqualifying in a technical document. In the specification this resolves the way section 4 already argues: the mechanism is not claimed at all, because the specification requires only the structural posture.
4. **Evidence tiering.** Where a physiological structure is named, use the precise term (intrinsic cardiac nervous system, enteric nervous system, vagal tone) and never the popular one. Speculative couplings never appear in a normative table. Better still, describe the function and skip the name, which escapes the choice between jargon and hype.
5. **Two axes, not one ladder.** The canon holds two mappings at once: what a person is made of (consciousness, mind, body) and the machine's own stack (software, firmware, hardware), joined by body equals hardware and mind equals firmware plus software. TETHER's layers are a third thing, a governance decomposition, and the document must say so rather than let a reader take them for a fourth revision of the canon.
6. **The one accepted record is the layer architecture decision, and only that one.** The record that would make a particular published post authoritative is still `proposed` and has been cited downstream as though it were accepted. TETHER must cite only what is accepted, and the design work should not repeat the error.

Two further consequences follow for scope, and both are constraints on *this* project rather than on the specification text.

**The domain that owns the source material is parked.** The reference implementation's Ouchie domain sits at rank 9 on the author's priority stack, parked with a review date of 2026-11-01, and the stack directs agents to say so rather than comply silently. Capture continues during the park; building courseware does not. This design note and the specification drafts are capture and specification work in the d7r repository, which is a different objective. **The guides and the courseware in section 7 are Ouchie work and are parked**, and nothing here should be read as authorizing them to start.

**The richest source transcript is unrouted and consent blocked.** The material that gives this document its vocabulary carries `consent_status: pending` for a named third party and has no routing decision. Under the clean room rule nothing from it reaches specification text anyway, but it also means the *concepts* are not yet canon, and the specification must be written so that it does not depend on their becoming canon.

---

## 5. Layer map

Ten layers, mirroring BLUEPRINT so the two read as siblings and a reader who knows one can navigate the other.

| # | Layer | Owns | BLUEPRINT analogue |
|---|---|---|---|
| 0 | **Tether** | Operator identity, the operator and instrument split, non transferability, the single instance rule | Charter |
| 1 | **Constitution** | The one governing protocol, precedence, the identity firewall, the clinical precedence rule | Constitution |
| 2 | **Topology** | Subsystems and their dependency order: metabolic, circadian, sensory, autonomic, neurochemical, musculoskeletal, cognitive | Topology |
| 3 | **Records** | The observation contract: instrument register, fault register, units, reference source, confidence | Records |
| 4 | **Lifecycle** | The state ladder (crisis, impaired, baseline, calibrated), the gate between rungs, change authority over the instrument | Lifecycle |
| 5 | **Classification** | Health data sensitivity, consent, disclosure, and the identity firewall as an enforced boundary | Classification |
| 6 | **Ledger** | The append only operating log: inputs, interventions, observations, latency windows, abandonment records | Ledger |
| 7 | **Agency** | Who may decide what: operator root, clinician envelope, emergency path, delegate. The shifted consequence ladder | Agency |
| 8 | **Boundary** | What crosses in (light, food, chemical, load, information) and out (disclosure, publication, telemetry export) | Boundary |
| 9 | **Operations** | The daily protocol, the periodic re reference, the self test, verification against external reference | Operations |

Layer 3 and Layer 9 are where the real new work is. Layers 0, 1, 5, and 7 are the governance stack applied to a new subject and should be short, because they inherit.

### Layer notes worth flagging now

**Layer 0, Tether.** The operator declaration is the analogue of the Charter and carries the one field the Charter never needed: `instances: 1`. It also carries the non transferability rule. A brain can be sold, inherited, or wound up, and BLUEPRINT specifies disposition at creation. An instrument cannot be transferred at all, so the disposition field is not "who receives it" but "who decides while the operator cannot," which is a handover grant and not a lineage entry. That is a genuinely different object and it needs its own schema.

**Layer 3, Records.** Every observation carries its **reference source**, and the controlled vocabulary is the point: `self-report`, `instrument`, `second-party`, `clinical`. Insight 2 becomes a schema constraint rather than a good intention, because a threshold that gates a consequential act can then be checked mechanically for whether anything but `self-report` supports it. This is the equivalent of design note 0000's insight 4, that the gate is real because of the hash: here the gate is real because of the reference source.

**Layer 4, Lifecycle.** Four rungs, one direction of travel at a time, and a declared gate between each. The gate is not an approval in the BLUEPRINT sense, because there is nobody to approve it but the operator and insight 2 says the operator's own reading is not a verdict. So the rung gate is satisfied by a **re reference against an external source within a declared window**, which makes it the first gate in the stack that is satisfied by evidence rather than by signature.

**Layer 6, Ledger.** One field the BLUEPRINT ledger does not need: `evaluationWindowEnds`. An intervention record is not evaluable before it, and an entry closing an intervention before that timestamp is recorded as `abandoned` and never as `ineffective`. Insight 4 becomes a mechanical property of the log.

**Layer 7, Agency.** The consequence ladder shifted by insight 1, and it is worth writing out because the shift is the interesting part:

| Class | DEFER meaning | TETHER meaning |
|---|---|---|
| K0 | Reversible local | Reversible within a day, no residue (a meal, a walk) |
| K1 | Reversible costly | Reversible over a declared window (a sleep debt, a training block) |
| K2 | Irreversible internal | Leaves a durable trace in the instrument (an injury, a sustained deficit) |
| K3 | Irreversible external | Systemic or developmental change, or any disclosure that leaves the operator's control |
| K4 | Constitutional | Changes who may decide about the instrument, or the identity register itself |

Note that the two lowest classes compress and the top classes broaden. There is no true K0 on an instrument with one instance and a cumulative history, so K0 is defined by *residue* rather than by reversal, which is the honest version.

**Layer 9, Operations.** The self test is the deliverable that makes the document usable, and it is one page: has every open intervention got an exit condition and a window, has the periodic re reference happened inside its interval, does any consequential threshold rest on `self-report` alone, is the escalation path current and declared in a known state, and does any record appear in both registers. Five checks, each mechanically decidable, each with a stated failure mode.

---

## 6. Refusals, drafted

POLARIS 4.1 makes refusals the load bearing layer, and these are the candidates. Each is stated so that violation is detectable.

- **R1. The identity firewall.** A record in the instrument or fault register MUST NOT be written to, mirrored into, or cited as the operator register. Absolute, non configurable.
- **R2. Root is not delegable.** An operator MUST NOT transfer root authority over the instrument. Bounded envelopes and handover grants only, each with a stated scope and a termination condition.
- **R3. No evaluation inside the window.** An intervention MUST NOT be recorded as ineffective before its declared evaluation window closes.
- **R4. No consequential act on self report alone.** A threshold gating a K2 act or above MUST NOT be satisfied by an observation whose only reference source is `self-report`.
- **R5. No intervention without an exit condition.** An intervention record without a declared exit condition MUST be rejected at write time.
- **R6. Escalation is not self gated.** A crisis escalation path MUST NOT condition on the operator's in the moment assessment.
- **R7. Clinical precedence.** Where TETHER and a licensed clinician's instruction bear on the same act, the clinician governs the act. TETHER never supplies grounds to decline, delay, or discontinue care.

R1, R6, and R7 are the candidates for the absolute, admits no configuration tier, matching POLARIS's three.

---

## 7. Deliverable map

The request is a spec, a set of skills, and user guides. They are three different artifacts with three different homes and three different authorship rules, and conflating them is how this becomes unusable.

| Artifact | Home | Normative | Authorship |
|---|---|---|---|
| `spec/TETHER-v1.0.md` | this repo | yes | clean room, general rules only |
| `spec/HABITAT-v1.0.md` | this repo | yes | clean room, general rules only |
| `spec/KIT-v1.0.md` | this repo | yes | clean room, general rules only |
| `spec/QUEST-v1.0.md` | this repo | yes | clean room, general rules only |
| `spec/BEARING-v1.0.md` | this repo | yes | clean room, general rules only, **and content gated**: BEARING states no criterion, no indication, and no quantity anywhere, per its 16.1 |
| `spec/adapters/README.md`, the set reviewed as a set | this repo | no | states each adapter's thesis and its inbound obligations from KIT, QUEST, and BEARING |
| `spec/adapters/<BASE>-for-operators-v1.0.md`, six of them | this repo | yes | short; the base document does the work |
| `schema/v1/operator-declaration.schema.json` and siblings, including item, loadout, capability, protocol, raise, run, and review schemas | this repo | yes | derived from the specs, and none written |
| `profiles/operator.md` | this repo | no | a starting configuration |
| `design/0006-operator-family-integration.md` | this repo | no | the family map, the through lines, the combined self test, and the open questions carried forward from section 10 |
| `design/0007-indications-and-routing.md` | this repo | no | why BEARING routes rather than classifies, what was borrowed from and rejected in the source discipline, the non clinical precedents, and the safety analysis |
| **Author written guides under BEARING section 16** | outside this repo, separately versioned and separately gated | no | **the fourth artifact class this table previously did not have.** A guide holds the domain specific content BEARING refuses to state, is reviewed by a qualified clinician, and does not inherit BEARING's conformance. BEARING 16.3 binds its required sections and its content prohibition, and `BR-88` refuses any monitor citing a violating guide |
| Operator guides, the True Self series | the vault, `Ouchie/Outputs/` | no | author written, Stage 4 required, **and parked** |
| Skills | the vault skill repository | no | routed per `brain-writing-skills` |

KIT, QUEST, and BEARING were drafted after this note and cite it as their design note. Design note 0006 is the integration note for the family as a whole and is where anything about how the five documents fit together now belongs, and design note 0007 carries the reasoning BEARING's own text cannot hold.

**The unmarked seam this table used to carry is now half resolved.** Both siblings hold that courseware presenting an operator's own records back to them is an **implementation** bound by the specification, while the operator guides row is non normative author written work. BEARING 16.2 and 16.3 supply the missing half for its own subject: a guide is a separate artifact with a separate review path, it does not inherit the specification's conformance, and what the specification controls is not whether the guide may exist but whether a monitor may cite it. That is a general answer and nothing in TETHER, HABITAT, KIT, or QUEST has adopted it. The seam is carried as an open question in 0006 section 7.2.

Two constraints that apply across all of them.

**Clean room, restated for this document specifically.** `AGENTS.md` rule 3 forbids producing specification text by copying and scrubbing a private vault. Here the private material is not a vault, it is the author's medical and personal history, which makes the rule sharper rather than looser. The transcripts are the reference implementation. The specification reads them and writes the general rule. **No specification section may contain a personal disclosure, a diagnosis, a medication, or a dated event from the author's life.** Those belong in the guides, which are author written, gated, and where the disclosure is the point.

**The guides are where the metaphysics lives, and they are a work, not a document.** The True Self operator guide is `work_type: course` or `book` under the vault's Lifecycle rules, which means Stage 4 critical thinking is mandatory before any prose and `gate_belief_clarification` must close. That is not bureaucracy here; the guide's whole subject is a belief the author holds about consciousness and a history involving his own psychiatric care, which is exactly the material the belief register and the sensitivity rules exist for. Do not start drafting the guide from this design note.

### Skill candidates

Named as behaviors, not topics, per the vault's skill rules. Each is a candidate and none is approved.

1. **operator-declaration.** Walk an operator through writing the layer 0 declaration and the initial envelope. One question at a time, proposals only.
2. **instrument-register.** Set up and maintain the layer 3 register: what is measured, with what reference source, at what interval.
3. **intervention-record.** Open an intervention with its purpose, cost, exit condition, and evaluation window. Refuse to write one that lacks any of the four.
4. **re-reference.** Run the layer 9 periodic re reference and report drift against external sources, never against the previous self report.
5. **tether-selftest.** The five check conformance self test, reporting pass or fail per check with the failure mode named.
6. **escalation-path.** Draft and keep current the layer 7 escalation declaration, in a known state, reviewed on an interval.

Skill 3 and skill 5 are the two that carry the specification's actual value, because they are the two that refuse.

---

## 8. HABITAT: the environment document

DERP answers what the runtime must provide. Its operator counterpart answers the same question about the environment an instrument runs in, and the author's own alignment map already assigns DERP to the environment rather than to the body, so this document occupies a slot that has been reserved since 2026-08-26.

**Proposed name: HABITAT.** The word is the ecological term for the environment an organism is adapted to, which is exactly the subject, and the technical literature's phrase for the central problem here is already *habitat mismatch*. It reads as a plain word in the way BLUEPRINT does and needs no acronym expansion, though one is available: Homeostasis, Affordances, Biome, Inputs, Thresholds, Adaptation, Timing.

### The thesis

> An instrument has a design envelope set by an environment its operator does not live in. The current environment is a declared configuration, not a given. A fault is tested against the declared environment before it is attributed to the instrument.

The last sentence is the whole document. It is insight 5 promoted to a normative requirement, and it is the single most consequential idea the reference implementation contributes, because attributing an environment fault to the instrument licenses a repair aimed at the wrong layer. A system performing badly outside its stated operating conditions is not a faulty system.

### What HABITAT specifies

**1. Input classes.** The environment is decomposed into classes an implementation declares and provisions: light (spectrum, intensity, timing), thermal, respiratory and hydrological, nutritional, mechanical load, sleep opportunity, social band, and information load. Each is declared with what the environment actually provides, not what it permits.

**2. Provision is not availability, and this is the load bearing distinction.** An environment that permits an input does not provide it. Sunlight exists above every office. A class is provisioned only when the operator actually receives it, and an implementation that counts availability as provision will report a conformant environment while supplying nothing. **Failure mode: an undeclared class is treated as unprovisioned, never as adequate.**

**3. Timing is a property of an input, not a scheduling convenience.** The same quantity of the same input at a different hour is a different input, because the systems it acts on are phase dependent. An input declaration without a timing property is malformed. This is where the circadian material enters as structure rather than as advice, and note that the document specifies that timing must be declared and never what the timing should be.

**4. The mismatch register.** The delta between the design envelope and the declared environment is written down and kept current. It is the first thing consulted when a fault appears. **Failure mode: a fault attributed to the instrument while the mismatch register is stale or absent is recorded as unattributed, not as an instrument fault.**

**5. Environment is provisioned by parties who are not the operator, and often for operators who cannot choose.** A workplace, a school, a household, and an institution all provision environment. An operator who does not control provisioning cannot be held to an envelope they cannot reach, and the party that does control it is identifiable. This is a DEFER adapter question and HABITAT's job is only to make the provisioning party a declared field rather than an assumption. It is also the general form of the strongest argument in the source material, that a system failing in conditions it was never built for is a conditions problem, and it matters most in exactly the case where the operator is a child.

**6. Adaptation and the silent floor.** Insight 3 lives here as well as in TETHER. A system recalibrates around a persistently absent input and reports the new state as baseline, so a class can be unprovisioned for years without producing a complaint. HABITAT therefore requires **periodic re declaration** of the environment on an interval, not on an event, because the event never comes.

### What HABITAT does not specify

No quantity, no threshold, no target, no protocol. It specifies that a class is declared, that provision is distinguished from availability, that timing is a property, that the mismatch is registered, and that the provisioning party is named. Two conformant operators may live in wildly different environments. One of them may be an ultra endurance athlete and the other bedbound, and HABITAT ranks neither, exactly as DERP ranks no runtime.

---

## 9. The six adapters

Each governance document is written for a subject that is a folder. Each has a true and non obvious reading when the subject is an instrument, and none of those readings is reachable by substituting nouns. An adapter is a normative annex: it binds its base document's machinery to the operator subject, states what carries over unchanged, states what changes, and states the one thing that would otherwise be got wrong.

Proposed home: `spec/adapters/<BASE>-for-operators-v1.0.md`. Each is short, because the base document does the work.

| Adapter | The reading | The thing that would otherwise be got wrong |
|---|---|---|
| **POLARIS for operators** | The operator's purpose, refusals, and loyalty order regarding their own instrument. Refusals about the body are the most testable refusals a person owns, because compliance is observable on a daily interval. | The loyalty order must be published including where the operator's own instrument sits in it. An operator whose declared order puts the instrument last has declared something true and useful, and a document that quietly forbids that answer is prescribing a life. Also: the author's alignment map places a **given purpose** above POLARIS, received rather than chosen, and ruling 8 left it deliberately unnamed. The adapter must not name it either. |
| **DEFER for operators** | Who may decide what about the instrument: operator root, clinician envelope, emergency path, caregiver or guardian. Carries the shifted consequence ladder in section 5. | Clinical authority is real, bounded, and must not be undercut, while root remains with the operator. Both halves at once. A guardian relationship is a genuine root holder for an operator who cannot hold their own, and that is the one case where root moves. It needs its own treatment rather than a footnote. |
| **CONFIDE for operators** | Who may process instrument telemetry, under what custody. The custody ladder transfers almost unchanged: wearables, health apps, labs, portals, insurers, and employers are all endpoints under contracts, and chains take the weakest class. | This is the adapter that is immediately, practically useful and it is the one nobody has written. An undeclared retention posture is C4 open, and most consumer health telemetry is C4 by default. The adapter says so in a table and stops. |
| **TRACE for operators** | The residue of the tooling: wearable histories, app state, portal records, imaging, and every derived score. The six artifact classes map with almost no strain. | A **derived score is an A2 derived artifact and not an observation**, so it is adopted deliberately or it expires. A risk score re served back to the operator as a fact about them is the exact accumulation problem TRACE exists for, and it is how a number computed once becomes a permanent property of a person. |
| **RETAIN for operators** | What a clinician, coach, employer, or institution keeps about the instrument, and what they keep when the engagement ends. | **This is where the identity firewall gets its teeth.** A retained label, held by an institution and re served to the operator, is the accumulation attack in the base document, and the operator has no ledger that can catch it. The base document is already honest that no ledger can catch cross domain learning and that disclosure and consent are the only control. The adapter says the same about a diagnosis, which is the most consequential retained record most people will ever be the subject of. |
| **SPEAK for operators** | Disclosure between operators, and between an operator and a clinical party. An instrument record crossing to another party is an utterance under an agreement with a custody floor. | Consent is the agreement, and it is directional, revocable, and scoped. The base document's rule that the floor travels with the record and may be strengthened but never weakened is exactly the rule people assume governs their health disclosures and it usually does not. Note that SPEAK itself is a skeleton and locks later, so this adapter is drafted last and cites a moving target until then. |

Three notes on the set.

**The adapters inherit precedence, they do not create it.** POLARIS for operators still has the highest precedence to forbid and none to permit. An instrument condition or an environment mismatch is a bound on what an operator may be authorized to do and never a permission, never a satisfied check, and never an excuse after the fact.

**Two adapters carry most of the practical value and should be drafted first: CONFIDE and TRACE.** They are the ones where the base machinery transfers nearly intact, where the answer is genuinely useful to a person on the day they read it, and where nothing in the answer requires anybody to adopt a metaphysics.

**RETAIN's adapter is the one with teeth and the one to write carefully.** It is the natural home of the identity firewall, and it is also the place where a careless sentence turns a governance document into an argument against clinical record keeping. Refusal R7, clinical precedence, applies with full force inside it.

---

## 10. Open questions for the author

The six questions below were written when the proposal was one document. Five documents later, three of them have been answered by what got drafted and three have not. Each carries its status as of 2026-08-30. **Design note 0006 section 7 is the live list**: it carries these six forward with the same numbering and adds the questions that only appeared once the family existed.

1. **Name.** TETHER, or something else. Section 2 recommends TETHER and the recommendation is not strongly held. **Status: settled in practice.** Five documents cite TETHER and the acronym has held up in use. 0006 recommends closing it.
2. **Eighth document or separate repository?** It is admitted here on the argument in section 1, that it specifies the root of every authority chain in the stack. The counterargument is real: a reader arriving for knowledge governance does not expect a document about sleep, and the stack's credibility is a shared resource. A separate repository under the same brand, cross referenced from the README, is the conservative option. **Status: open, and larger than when it was written.** The proposal is now five documents and six annexes rather than one document, so the cost side of the trade has grown while the argument for the root attachment has held. 0006 section 2.2 restates the argument and 0006 section 7.1 keeps the question open.
3. **Does the consequence ladder shift, or does it get its own letters?** Section 5 shifts K0 to K4 in meaning while keeping the names. The alternative is a distinct ladder (B0 to B4) that never gets confused with DEFER's at a glance. Shifting is more elegant and more dangerous. **Status: open, with evidence for the danger half.** A KIT draft asserted a K2 floor and attributed it to TETHER 3.2, which states no such floor, and the error survived to review; the floor would have emptied TETHER's own K0 and K1 rungs. A distinct ladder would have prevented exactly that confusion. 0006 recommends re opening rather than treating this as settled.
4. **How far does layer 8 go?** Inputs crossing into the instrument is a large surface (light, food, chemistry, load, information) and the information half overlaps everything the rest of the stack already governs. Proposal: layer 8 specifies the *declaration* of an input class and its custody, and delegates information inputs to the existing documents rather than restating them. **Status: partially answered by the family's shape.** KIT took the objects, HABITAT took the inputs, and information load is declared as a class and delegated. What remains open is the overlap between HABITAT's information load class and KIT's data surface, since a device that transmits is both an input channel and an emitter.
5. **Is `instances: 1` really invariant?** It is today. The document should not be built so that it breaks if that ever changes, but neither should it hedge in a way that costs it insight 1, which is its sharpest structural observation. **Status: unchanged and untested by anything drafted since.**
6. **Does the reference implementation's belief go in the spec at all?** Section 4 says no, and puts it in the guides under POLARIS's motto rule. Confirm, because the alternative (a normative but explicitly non binding appendix, the way POLARIS carries the Four Agreements worked example) is defensible and would keep the origin visible. **Status: answered no, consistently, five times.** TETHER 2.2, KIT 2.12's treatment of the game vocabulary, QUEST 1.5, BEARING 11.5 and 11.7, and section 2 of this note all resolve the same way, and all three siblings put their motto class terms in a closed table under POLARIS 7.3 rather than in normative text. BEARING is the strongest case, because its subject is the published alignment material itself and it still names no pillar, no dimension, no pole label, and no tier name. 0006 recommends closing it.

## Sources

The reference implementation for this document is the author's own operating practice as recorded in the vault's transcript entries and the podcast pipeline. Per the clean room rule, those are read and never copied. Nothing in `spec/` derives its text from them.
