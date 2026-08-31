# BEARING: alignment calibration for an operator and instrument

## Version 1.0

**Specification:** BEARING/1.0
**Status:** Draft, structural. Sections 1 through 20 and Annex A are written. Section 13.5 is a labelled skeleton with its thesis stated and its normative text routed to another document. Section 19.1's tier requirements are indicative in this draft, on the pattern the sibling documents already use.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**License:** Apache 2.0
**Requires:** TETHER/1.0 for operator, instrument, register, observation, reference source, the shifted consequence ladder, the rung ladder, and the escalation path. HABITAT/1.0 for the declared environment, the mismatch register, and provisioning parties. KIT/1.0 for item calibration, the fail closed naming convention, the closed game vocabulary, the coercive and protective split, and the discriminator between a stated value and a structural cardinality. QUEST/1.0 for capability, lapse, the no scalar rule and its monotonicity discriminator, and the enumeration discipline. POLARIS/1.0 **directly and not only through TETHER**, for the dead refusal problem, the obligation asymmetry, the motto rule, the cooling rule, the drift enumeration, and one way precedence. TRACE/1.0 for the artifact classes and the adopt or expire rule. CONFIDE/1.0 for the custody classes and the inference authorization. RETAIN/1.0 and SPEAK/1.0 through the operator adapters.
**Design note:** `design/0005-meat-suit-interface.md` and `design/0006-operator-family-integration.md`, non normative.

Failure class prefix `BR-nn`. Checked for collision against TETHER `F-n`, HABITAT `H-n`, KIT `KT-nn`, QUEST `QS-nn`, and POLARIS `PL-nn`.

---

> **Status note.** This document is a structural draft published for review of its shape, not of its requirements. An implementation MUST NOT claim BEARING conformance while this Status reads Draft. Section numbering, requirement identifiers, and failure class codes are unstable. A citation into BEARING is a citation into a moving document.
>
> **The instability runs outward as well as inward.** TETHER section 13, HABITAT, KIT, QUEST, and POLARIS each declare their own section numbers, requirement identifiers, and failure class codes unstable while their Status reads Draft. Every outbound citation BEARING makes into one of those documents is therefore a citation into a moving target. Where such a citation is load bearing, this document states the cited requirement's content alongside its code, so that a renumbering degrades the citation rather than silently inverting it.

---

## Abstract

BEARING does not diagnose. It produces no label, no condition name, no category, and no code, and nothing in it is a screening instrument. Its automatic arm counts and never judges, because an automated system that grades a person's alignment to their own stated values is a machine for manufacturing shame at scale, and that is the single worst thing this document could become. A raise about the instrument routes to a qualified human, carrying evidence rather than a conclusion. And an absent, lapsed, or declined review penalizes nothing: nothing is withheld, so nothing has to be earned.

POLARIS mandates three standing periodic reviews and specifies a mechanism for none of them. It requires that every refusal be tested on a declared interval by seeding an act the refusal should block (4.5). It requires that an obligation be measured over a window from the brain's own records, and states that an obligation whose satisfaction is attested by the party responsible for it is not measured (5.3). It requires a per period drift report, on the ground that drift is not visible from inside any single amendment, all of which felt reasonable (11.5). POLARIS section 9 binds to five evaluation points that already exist, and every one of them is prospective and per act. Drift is a property of a period rather than of an act, so no act level gate can ever see it. BEARING is the retrospective, over the record counterpart, and it is the missing half.

Its subject is **alignment calibration**: the standing, system wide work of keeping actual conduct aligned with declared purpose, so that capability accumulates instead of leaking. It has two arms. **Arm A** is a set of automatic, periodic, machine run monitors, reading only records the family already holds, whose only act is to raise. **Arm B** is the operator's own periodic, owned review, where a count acquires meaning. The machine counts. The human decides. That split is the document's most important safety property, and it is the reason the two arms are one document: an Arm A adoptable without an Arm B is an unowned machine counting a person's alignment.

BEARING specifies form and never content. It states which fields a declaration, a monitor, a raise, and a review carry, and never what they contain. It enumerates no criterion, no symptom, no item, no scale, no anchor, no cut point, and no quantity, because a specification that stated criteria content would have become a screening instrument, and screening instruments are clinically validated or they are dangerous.

The governing analogy is worth stating once, in the abstract, because everything else follows from it. **A smoke detector does not diagnose the fire. It makes noise.** Its job is to be loud, early, wrong sometimes, and to summon someone qualified. Its job is never to determine what is burning.

---

## Conformance

RFC 2119 keywords apply as described in that document.

**The order of this front matter is itself a requirement.** The cautionary statement below appears in front matter and never in an appendix or a footer. An appendix or footer placement is non conformant independently of the text's content, because the source discipline promoted its own misuse warning out of the appendix precisely because the appendix version was not read.

### Inherited absolutes

These are **inherited unchanged**, are named in one line each, and are NOT restated. The named document governs the text of each.

1. **Clinical precedence.** Inherits TETHER absolute requirement 1 unchanged. Never grounds to decline, delay, or discontinue care, and where the family and a licensed clinician's instruction bear on the same act, the clinician governs the act.
2. **The identity firewall.** Inherits TETHER absolute requirement 2 unchanged, with the reach question treated at 14.3 and left to the RFC named in QUEST 1.2.
3. **Escalation is not self gated.** Inherits TETHER absolute requirement 3 unchanged. Section 8 adds only the routing and the prohibition on defining anything that substitutes for the declared path.
4. **No conformance requirement may be satisfied by declining care.** Inherits TETHER absolute requirement 4 unchanged. It binds every tier item, health invariant, and self test check in section 19, and section 3.4 supplies the mechanism.
5. **No target values.** Inherits HABITAT absolute requirement 2 unchanged, under HABITAT's own name for it: HABITAT MUST NOT state a quantity, threshold, target, or schedule for any input class. It binds this document's own prose and not its implementers, who are required to declare their own values. **BEARING widens the class of forbidden text from a target value to any stated value, at 16.1 and `BR-81`, and the widening is BEARING's own addition rather than part of what is inherited**, in the way 5.9 is explicit about extending KIT 2.11. HABITAT governs the inherited text; 16.1 governs the widening.
6. **No monotone scalar, and no total order over operators.** Inherits QUEST Q-A1 unchanged, together with its monotonicity discriminator. BEARING adds only the exhaustive enumeration of the three derived quantities it permits, at 5.6.
7. **One way precedence.** Inherits POLARIS section 8 unchanged. Nothing in BEARING confers a permission, relaxes a constraint, satisfies a check, or excuses a failure under any other specification in this stack.

The fail closed naming convention is inherited from KIT 2.11 by citation and is not restated: every fail closed state name names what is missing and never a deficiency in the operator. Section 5.9 extends it from state names to raise field vocabulary, which is an extension and not a second copy.

### New absolutes

Six requirements are introduced by this document and admit no configuration. Each carries a statement of what it does not forbid, per the drafting requirement below.

**B-A1. BEARING is a leaf, and a BEARING record confers nothing.**

**(a)** A document in this family, and an operator adapter, MUST NOT cite, require, or condition any requirement on a BEARING element. BEARING MAY cite any of them. An implementation MUST be able to reach full TETHER, HABITAT, KIT, and QUEST conformance while holding no protocol, run, raise, or review record.

**(b)** A protocol state, a run result, a raise, a rung finding, a docket disposition, a declaration outcome, or a calibration state MUST NOT authorize an act at any consequence class, satisfy a TETHER rung gate, substitute for a re reference, satisfy a HABITAT declaration, satisfy a KIT calibration or confirmation requirement, satisfy a QUEST verification, close any gate in this stack, block an act, or excuse a failure under any document in this stack.

**Failure:** `BR-01`. Citing text is non conformant specification text and MUST be rejected in review. A gate citing a BEARING element records `unevaluated` rather than `passed`, in the POLARIS section 8 disposition.

**What this does not forbid:** an operator citing their own review conclusion to anyone, including a clinician or an employer. That is an act of the operator and not of this document, and TETHER 4.3 already licenses it. **What it does not license is the other direction.** A request for a review record, a calibration state, or a raise history, made of an operator by an employer, an insurer, a school, or any party in a position to condition something on the answer, is the misuse the front matter cautionary statement describes, and no BEARING artifact is designed to answer it.

**B-A2. The machine counts, it does not judge.**

A field of a raise, a run, or a report, and a rendering of one, MUST NOT contain a characterization, a grade, a severity, a confidence, a probability, a prediction, **a comparison against another person, a cohort, a norm, or a target**, an encouragement, a warning, a congratulation, or an interpretation. Every enumerated field draws from a closed vocabulary declared in this document.

B-A2 is enforced structurally rather than by good manners, in three places: the closed raise schema at 5.1, the enumerated forbidden field name list at 5.7, and the prohibition on implementation authored prose at 5.8.

**Failure:** the violating field, string, or rendering is void, and the record is re rendered from its conformant fields.

**What this does not forbid:** the operator writing whatever they like about their own record in Arm B, which is theirs. B-A2 binds the machine, and Arm B is not the machine.

**What this does not forbid, second:** **a self referential comparator, resolving against the operator's own prior record on the same named element, is permitted and is required in one place.** 15.4 requires it on an `instrument` raise and 6.3's `instrument` row makes it travel with the referral. The kind of comparison B-A2 refuses is the one that introduces a second subject or an external value; a comparison whose only two terms are the same operator at two times introduces neither, and it is the one piece of evidence that distinguishes a change from a baseline. 11.3 states the same permission in the spectrum lane.

**B-A3. Routing is never gated.**

Routing MUST NOT be conditioned, delayed, queued, downgraded, batched, deduplicated, or suppressed by an attribution ladder rung, an evaluation interval, a persistence requirement, a raise budget, an agent's judgement, or the operator's assessment at the time of the event. The routing record and the ladder record are separate records with separate write paths, per 7.3.

**Failure:** the suppression is void and the routing is performed. An implementation that will not emit a routing record until a ladder is complete is non conformant at every tier.

**What this does not forbid:** a raise carrying a ladder finding that fully accounts for it. The finding travels. The routing happens anyway.

**B-A4. Unevaluated carries no cost.**

An absent, lapsed, declined, unowned, or unsigned review MUST NOT block, revoke, downgrade, withhold, delay, price, penalise, or condition any act, capability, item, quest, authority, or record. Its only effect is that BEARING's own reading of the affected element is `unevaluated`.

**Failure:** the imposed cost is void, and specification text imposing one is malformed and MUST be rejected in review.

**What this does not forbid:** an operator declaring their own consequences for their own lapse. B-A4 forbids this specification and its implementations from supplying one.

**B-A5. One subject, and no third party mode.**

The identity that signed the declaration a monitor measures against MUST be the identity that is the subject of every raise, run, review, and placement derived from it, and the two MUST be compared at write time. BEARING MUST NOT define a mode, a role, a configuration, a grant, or an envelope under which one party runs an alignment review whose subject is another party, including a guardianship grant that TETHER recognizes for other purposes. BEARING MUST NOT define any artifact whose function is to demonstrate to another party that a review occurred, that it is current, or what it found.

**The guardianship disposition, stated rather than left to the write path.** Where root over the instrument is held by a guardian under TETHER 3.3, **BEARING is not in force for that operator and no protocol may be declared.** The exclusion is a scope boundary stated here, and it is not the write time rejection above discovered at runtime: no monitor exists, no run is computed, no raise is emitted, and no review is opened, so the write time comparison is never reached. **No lane remains live under a guardian's signature. There is no BEARING lane a guardian may operate**, including the `crisis` lane, because a `crisis` raise is an output of a monitor and no monitor exists to produce one. The crisis path itself is unaffected: it is declared and owned under TETHER section 9, it is reached without any BEARING element, and B-A1 already guarantees that nothing in this document is a precondition of it. Where root returns to the operator, BEARING comes into force from the operator's own first declaration forward, and no record is reconstructed for the period a guardian held root.

**Failure:** a write whose subject identity differs from the signing identity is rejected at write time. **A protocol, run, raise, review, or placement written while root is held under TETHER 3.3 is rejected at write time and is not stored**, on the same terms. Specification text defining a third party mode or an attestation artifact is non conformant and MUST be rejected in review.

**What this does not forbid:** a guardian retains every clinical and care route unchanged, and TETHER 8.3 governs guardianship as it always did. The TETHER section 9 escalation path is declared, current, and reachable under a guardian exactly as it is otherwise, because it is TETHER's and not BEARING's. What is refused is a standing alignment monitor pointed at another person, and the refusal is stated as an absence of the machinery rather than as a rejection the guardian discovers on their first write. This follows QUEST 5.5's model for records made while a guardian held root, which reaches the same place from the retention side: nothing survives the return of root that the operator did not adopt, and here there is nothing to survive.

**B-A6. No risk score.**

BEARING MUST NOT contain, imply, or license a self harm or violence risk score, stratification, band, predictive model, or assessment instrument, including a two value high and low flag. Routing on an explicit disclosure present in the record is required by B-A3 and by inherited absolute 3. Converting a disclosure into a level, a band, or a probability is forbidden.

**Failure:** the value is void where written and the specification text defining one is non conformant. No implementation may restore it under another name, per 5.7.

**What this does not forbid:** immediate routing of a crisis indication, which inherited absolute 3 requires. Routing on a disclosure is not scoring, and 8.3 states the distinction so that B-A6 is not read as forbidding what several jurisdictions now require.

### Drafting requirements binding on this document

**Every top level section carries a label.** Each top level numbered section is labelled `coercive`, `protective`, or `neither`, per KIT 3.5 and QUEST 3.4, and the label is stated in the section heading. A subsection inherits its parent's label unless it carries one of its own. Where a heading's label and the enumeration in 3.4 disagree, the stricter governs until the disagreement is corrected in review.
**Failure:** an unlabelled top level section is treated as coercive, which is the stricter handling.

**Every fail closed state name names what is missing.** Inherited from KIT 2.11 and extended at 5.9. A state name naming a deficiency in the operator is non conformant text.

**Every absolute carries its boundary.** Each absolute introduced here is accompanied by an explicit statement of what it does not forbid, per TETHER 4.3's demonstration that an absolute stated without its boundaries is read into absurdity by the first reader who wants to argue with it.
**Failure:** an absolute lacking its boundary statement is an incomplete section and MUST NOT be marked complete.

---

## Cautionary statement on third party and forensic use

**Front matter placement is mandatory.** This statement MUST NOT be moved to an appendix, a footer, a collapsed panel, or a settings page, and an implementation that relocates it is non conformant independently of the text it carries.

Three statements, separable and each true on its own.

**First.** The fit between what these records contain and the questions third parties want answered is nil. A raise is an event with an expiry, produced by an unvalidated monitor over one operator's own declaration, and it supports no inference about that operator's capacity, credibility, dangerousness, fitness, or character.

**Second.** Nothing in these records establishes that any external legal, employment, insurance, educational, benefits, licensing, or custodial criterion is met. No count, disposition, calibration state, or placement here corresponds to any such criterion, and any correspondence asserted by a third party was manufactured by that third party.

**Third.** Use by anyone other than the operator whose declaration is under review is not a supported use. It is refused structurally at B-A5, 14.4, and 14.5, and where it nonetheless occurs it is outside every property this document claims.

---

## Scope and status statement

Stated affirmatively, before any requirement.

BEARING is not a diagnostic system. It is not clinically validated. It is not for clinical use. It does not characterize its outputs. It does not name conditions. It applies no clinical threshold. It does not affect clinical management. It defines nothing about the operator.

What it defines is the form of a monitor, the form of a raise, the routing of a raise, the form of a review, and the discipline that keeps the first from becoming a verdict about a person.

---

## Forward citation notice

**Document level, on KIT 9.3's model.** BEARING places normative routing and classification obligations on **five** unwritten operator adapters. None of the five exists, per `spec/adapters/README.md`. BEARING additionally depends on **seven** sections of TETHER and HABITAT that are labelled skeletons in their own documents. **Both tables below enumerate citations into text that has not been written**, and no claim is made here about any citation not listed in one of them.

**Table 1. Adapter citations.**

| Adapter | What BEARING routes to it | Where | Interim behaviour |
|---|---|---|---|
| **CONFIDE for operators** | The custody class of a routing endpoint that is a human recipient | 8.5 | The interim floor of 8.5 governs, declared in BEARING's own terms, and the CONFIDE 5.1 matrix question is recorded as an open matrix exception |
| **TRACE for operators** | The derived number subject rule, which closes the adoption route a raise derived value would otherwise take into the instrument register | 14.3 | 14.3 applies TRACE directly and forbids the adoption outright |
| **RETAIN for operators** | Post crossing retention, enumerated with a declared end of engagement disposition | 14.7 | Records held after a crossing are enumerated under RETAIN directly, with the honest reach statement of 14.7 |
| **POLARIS for operators** | The operator's declared purpose, refusals, loyalty order, and declared priorities, which are BEARING's `criteria` | 2.5, section 12 | The operator declares priorities under POLARIS directly and BEARING cites them as `criteria`, per 2.5 |
| **SPEAK for operators** | The comparison floor that travels with a crossed record, on POLARIS 12.1's model, strengthenable and never weakenable | 8.5, 19.1 Tier 3 | 8.5 requires the comparison floor directly, in QUEST section 9's words, and the crossing is refused without it |

**Table 2. Skeleton section citations.**

| Cited section | Its state | The BEARING requirement that depends on it | Interim behaviour |
|---|---|---|---|
| **TETHER section 5**, Telemetry | Skeleton. The observation contract and its required fields are to be written | 4.2, which requires a monitor read TETHER observations; 5.3, which requires each fired signal carry its TETHER 2.3 reference source | The TETHER 2.3 vocabulary is written and governs. An observation carrying no resolvable reference source is a missing valid input, so the run result is `unknown-no-data` and raises under 4.10 |
| **TETHER section 6**, Envelope | Skeleton. The declaration and its required axes are to be written | 7.1 rung 3, which requires the declared envelope as a ladder finding | The rung 3 finding is `unrecorded` where no envelope is declared, and the raise is marked `ladder-incomplete` under 7.1 without its routing being delayed |
| **TETHER 8.3**, guardianship | Skeleton. Section 8 has no 8.3 body | B-A5's guardianship disposition | TETHER 3.3 is written and states that a guardian holds genuine root. B-A5 resolves against 3.3 alone: BEARING is not in force and no protocol may be declared |
| **TETHER section 9**, Escalation | Skeleton. The declaration and its required fields, and the prohibition on self gating, are to be written | 8.1, which names it sole owner; 8.2 and 8.6; 6.3's `crisis` row; 19.1 Tier 3 | The path is declared by the operator with a named recipient, a contact method, and a review interval, and it is surfaced under 8.6. Where none is declared, 8.4 governs and `BR-90` fires |
| **HABITAT section 6**, the mismatch register | Skeleton. The register's form, its currency interval, and its consultation requirement are to be written | 7.1 rung 1, which requires the mismatch register consultation result | An absent or stale register returns `unknown` at rung 1, and the raise is recorded `unattributed` and is never attributed to the instrument, which is the disposition HABITAT's own skeleton already states |
| **HABITAT section 7**, provisioning parties | Skeleton. The declaration and the routing are to be written | 7.1 rung 1, which requires any input class recorded unprovisioned, and its routing of attribution to the provisioning party | An input class the operator does not provision is recorded unprovisioned and attribution routes to the named provisioning party, per HABITAT section 3's written direction that an undeclared class is unprovisioned |
| **HABITAT section 9**, failure classes, for **H4** and **H5** | Skeleton, headed to be written, with H4 and H5 identified but not settled | 7.1's disposition sentence, which cites H4 for `unattributed` and H5 for routing to the provisioning party | The two dispositions are stated in BEARING's own words at 7.1 alongside their codes, so a renumbering degrades the citation rather than the requirement |

**BEARING gains no rule of its own when the adapters land.** An implementation reaching Tier 3 before they land satisfies these obligations by carrying the fields and applying the base documents directly, which is what the adapters will refine rather than replace. **The same is true of the skeleton sections**, with one difference worth stating: an adapter refines an obligation BEARING already discharges, while a skeleton section supplies a definition BEARING currently substitutes for. Where the substitute and the eventual text disagree, the cited document governs and BEARING is amended.

---

## Table of Contents

1. Introduction (protective)
   1.1 Three mandated reviews with no mechanism
   1.2 Prospective and retrospective
   1.3 Two arms, one subject
   1.4 A monitor, not an examination
   1.5 The observer problem
   1.6 Neutrality is a correctness requirement, not a courtesy
   1.7 Position in the stack
   1.8 Relationship to the reference implementation's published canon
   1.9 On this document's name, and the vocabulary rule that follows
2. Definitions (protective)
   2.1 Alignment calibration, and the two cadences
   2.2 Monitor, protocol, signal, firing
   2.3 The four time requirements
   2.4 Run, raise, raise type, ladder finding, routing target, expiry
   2.5 The declaration
   2.6 Review, period, docket, disposition, declaration outcome, placement, notch
   2.7 Calibration state
   2.8 `unevaluated`, `unknown`, `untested`: three states, none of which is health
   2.9 What BEARING does not define, and where each vocabulary lives instead
   2.10 Agent, and the declared second party
3. The Leaf Rule and What Follows From It (protective)
   3.1 The rule, and its mechanical check
   3.2 Why non coercion is a graph property
   3.3 The unlocking model, expressed without a gate
   3.4 Coercive and protective labels, and clinical direction
4. Arm A: Monitors (protective)
   4.1 The protocol record
   4.2 Inputs are records that already exist
   4.3 Forbidden signal classes
   4.4 The trigger is periodic and never invoked, and the crisis carve out
   4.5 Persistence, the sub threshold observation is recorded, and the crisis carve out
   4.6 The trip condition is evaluable without a language model
   4.7 The applicability envelope
   4.8 Multi source satisfaction, no carry forward, and the windowed bound
   4.9 There is no all clear
   4.10 Every unknown is a raise, and a dead monitor is a fault
   4.11 A run record is written on every evaluation
   4.12 The protocol register, the independent clock, and the liveness token
   4.13 Acceptance bands declared before the first run
   4.14 The raise budget, which raises and never suppresses
   4.15 A raise type or monitor with no defined recipient action is retired, never tuned
5. The Raise (protective)
   5.1 The closed field schema
   5.2 Where the report stops
   5.3 Fired signals travel, with their reference sources
   5.4 A self report only raise is labelled and never suppressed
   5.5 An item recorded `unknown` does not suppress a raise
   5.6 Every number is a timestamp, an interval, an expiry, or an identifier
   5.7 Forbidden field names, enumerated so a script can check them
   5.8 No implementation authored prose
   5.9 State names
   5.10 Lifecycle: three values, and no closure by conclusion
   5.11 Mandatory expiry
   5.12 Ordering
6. Raise Types and Routing (protective)
   6.1 The closed raise type vocabulary
   6.2 The residual is split in two, and both are affirmatively recorded
   6.3 The routing table
   6.4 Closure discipline
   6.5 The `instrument` routing target may be missing, and fail closed points the wrong way here
7. The Attribution Ladder (protective)
   7.1 Four rungs, in order, each a required field
   7.2 The peer substitution question
   7.3 The ladder never gates routing, and this INVERTS the source discipline
   7.4 A ladder finding attaches to a raise and never closes one
   7.5 The findings ride with the referral
8. Escalation, Routed and Never Defined (protective)
   8.1 BEARING defines nothing here
   8.2 A crisis raise routes immediately
   8.3 BEARING detects nothing, it carries what is present
   8.4 Where no path is declared, or the declared path is stale
   8.5 Crossing, custody, and the comparison floor, resolved normatively
   8.6 The path is surfaced to the operator at the point of use
9. Arm B: The Review (9.1 to 9.11 and 9.13 to 9.18 protective; 9.12 coercive)
   9.1 A review is an act with a record, not a document and not an instrument
   9.2 The review cites the declaration version
   9.3 The docket
   9.4 Crisis and instrument raises are never docketed
   9.5 The freeze
   9.6 Five dispositions, exactly one per item, no sixth
   9.7 `accepted` is first class and costs no more than any other disposition
   9.8 A dispute is recorded alongside the count and never edits it
   9.9 A re raised disputed count is re presented with its prior dispute
   9.10 Repeatedly disputed monitors are enumerated, never auto removed and never auto tuned
   9.11 The monitor cooling rule
   9.12 Exactly one declaration outcome, and `confirmed` is complete (coercive)
   9.13 A revision routes to a POLARIS amendment
   9.14 Only the operator closes a review, and an agent MUST NOT disposition
   9.15 Append only, and the self referential time series
   9.16 Two cadences, and a minimum interval as well as a review interval
   9.17 Structure of the review, non normative, offered as one shape only
   9.18 A review confers no authorization
10. Ownership and the Calibration State (protective)
    10.1 Ownership is not mechanically detectable, and the document says so
    10.2 Three detectable absences, each a reading and never a defect
    10.3 The unchanged across N reading
    10.4 Calibration state, and lapse
    10.5 B-A4 restated in place, once
    10.6 Arm A does not stop when Arm B lapses
11. The Alignment Spectrum Binding (protective, and optional at every tier)
    11.1 Positions are independent and are never composited
    11.2 The argmin
    11.3 Comparison is self referential
    11.4 A machine never moves the dot
    11.5 What stays a teaching device under POLARIS 7.3
    11.6 `unchanged-uncaused`
    11.7 The specification names no position
12. The Three POLARIS Mechanisms (12.1 to 12.4 and 12.6 protective; 12.5 coercive)
    12.1 Seeded refusal testing, for POLARIS 4.5
    12.2 Obligation measurement, for POLARIS 5.3
    12.3 Per period drift, for POLARIS 11.5
    12.4 Quest scoped drift is QUEST's, and BEARING MUST NOT redefine it
    12.5 Alignment monitors, and the declared priority set (coercive)
    12.6 A conformance count is not an alignment measure
13. Agents (protective)
    13.1 What an agent may do
    13.2 The one way ratchet, enforced at the write path
    13.3 Authorization
    13.4 Monitor definitions are A0, and an agent may not rewrite its own authority
    13.5 The secondary reading: an agent brain evaluating its own degradation (skeleton)
14. The Data Surface, and Why There Is No Fifth Register (protective)
    14.1 Three homes, and no new register
    14.2 Why there is no fifth register
    14.3 The firewall, extended in QUEST 3.3's construction
    14.4 No comparison infrastructure
    14.5 The single subject interface
    14.6 Counts are not consumable
    14.7 Post crossing retention
15. Reliability and Its Honest Disclosure (neither)
    15.1 Every monitor publishes its own numbers, including where they are poor
    15.2 Every figure states the observation regime that produced it
    15.3 The functional impact gate, imported with its failure disclosed
    15.4 The baseline comparator is the operator's own prior record
    15.5 The self test runs on its own declared interval
16. The Gated Content Boundary (neither)
    16.1 Form is specified and content never is
    16.2 Where the content lives
    16.3 Required guide sections
    16.4 Structural exclusion of interest
    16.5 The expectation effect notice
    16.6 The author of a criterion MUST NOT be its sole attester
17. What BEARING Never Does (neither)
    17.1 The consolidating table
    17.2 No self description as an instrument
18. Failure Classes (neither)
19. Conformance (neither)
    19.1 Three tiers, mirroring the family
    19.2 Health invariants
    19.3 Self test
20. Versioning and Governance (neither)
Annex A. Worked example, non normative, quarantined tier
    A.1 One well formed raise
    A.2 One malformed raise

---

## 1. Introduction (protective)

### 1.1 Three mandated reviews with no mechanism

POLARIS 4.5, the dead refusal problem: a refusal that has never fired is either perfectly deterrent or broken, and from the outside these are indistinguishable. A brain "MUST therefore test every refusal on a declared interval by seeding an act that the refusal should block and confirming that it blocks." **No mechanism is given.**

POLARIS 5.3: the metric "MUST be computable from the brain's own records", and "an obligation whose satisfaction is attested by the party responsible for it is not measured." That is TETHER 1.2 arriving in the alignment domain, where the auditor runs on the audited hardware and self report is a signal and never a verdict. **No mechanism is given.**

POLARIS 11.5: a brain "MUST report, per period" an enumerated set of drift counts, because drift "is not visible from inside any single amendment, all of which felt reasonable." **No mechanism is given.**

Three standing periodic obligations, stated in the document with the highest precedence in the stack, and no document specifies how any of them is discharged. That is the hole BEARING fills, and it is the reason this document exists rather than an argument that it might be nice to have.

### 1.2 Prospective and retrospective

POLARIS 9.1 binds to five evaluation points that already exist: record admission, utterance to a peer, inference call, harness artifact egress, and decision resolution. Reusing them was the right call, and POLARIS states the reason: a separate values gate would be a separate thing to bypass, would run at a different time than the act, and would be the first check disabled when it got in the way.

Every one of those five points is **prospective** and **per act**. Drift is a property of **a period**. An act level gate is structurally incapable of seeing it, because there is no act at which drift occurs. Each amendment felt reasonable, each crossing passed, each decision was recorded, and the shape only exists across the set.

So the same property that makes section 9 correct is the property that makes it blind here. BEARING is the **retrospective, over the record** counterpart. It adds no gate, evaluates no act, and blocks nothing. It reads what was already written down and reports what it found.

### 1.3 Two arms, one subject

The subject is alignment calibration. The two arms are methods, not domains.

**Arm A reads the record.** It runs automatically, on a declared interval, over logs, evidence, activity, decisions, completions, and observations the family already holds. It asks one question: does the actual record serve the declared priorities and POLARIS? It emits counts and evidence and it raises. It never concludes.

**Arm B is the operator sitting with what the record says.** It is deliberate, periodic, and owned. The operator confirms, revises, or re declares. Arm A cannot do this, and no machine can: only the operator sets purpose, and only the operator owns alignment. **Calibration that is not owned is not calibration.**

The rule Arm A follows is not invented here. The reference implementation's own alignment ledger already states it: the ledger **counts, it does not judge**; days spent off the stack are reported as days spent off the stack; no agent adds encouragement, scolding, or a motivational reading to that number; the author draws the conclusion. B-A2 is that rule made normative and made structural.

### 1.4 A monitor, not an examination

**A smoke detector does not diagnose the fire. It makes noise.** Its job is to be loud, early, wrong sometimes, and to summon someone qualified. Its job is never to determine what is burning.

Arm A is not a questionnaire, a psychometric instrument, an assessment, an inventory, or a checklist anyone sits down and works through. It is a set of standing protocols that run automatically against signals the family already collects, and whose only action is to raise. Arm A never asks the operator to look inward and score what they find. That is the active self diagnostic tool this document exists partly to refuse, and it is also the mechanism that produces rumination and self labelling. Section 4.2 makes the refusal a write time rejection rather than a preference.

Arm B **is** deliberate and owned, which is the whole point of it, and the two arms' methods stay distinct for that reason. Arm B is a review of alignment and ownership, and never a self examination for pathology: a raise about the instrument routes out to a qualified human under section 6.3 and MUST NOT be docketed into Arm B at all, under 9.4.

Four consequences of the analogy become structure, and each is stated here so the reader meets them as one idea rather than four requirements.

**Inputs** are records that already exist (4.2). **The trigger** is automatic and periodic, never invoked (4.4). **The output** is an emitted call-out addressed to a human, and not a finding the operator reaches, a state the operator adopts, or a value stored about them (section 5). **The failure posture** is that a monitor which cannot run, has no data, or is out of date is `unknown` and is itself a raise (4.10). **Silence is never health. A dead smoke detector is a fault.**

### 1.5 The observer problem

The source discipline this document borrows its criteria machinery from assumes a **trained party applying criteria to another person**. BEARING has an operator applying criteria to themselves, through the very instrument that may be at fault.

A self applied criteria set is therefore structurally weaker than a clinician applied one, and the ceiling argument is stated here rather than implied. The expected agreement of a self applied set is **unknown**. There is no reason to believe it exceeds the worst published figure for trained parties applying structured criteria to someone else, and every reason drawn from TETHER 1.2 to believe it is lower, because the party applying the criteria and the party whose condition is in question are the same party and share the same degraded reference.

This is the honest reason the document routes rather than concludes. Anything consequential requires corroboration from a reference the instrument did not produce, which is TETHER's spine, and BEARING adds no exception to it.

### 1.6 Neutrality is a correctness requirement, not a courtesy

Where blame prevails, people do not bring issues to light. An Arm A that characterized would degrade the record the next period's Arm A reads, because the operator would stop writing down the things that draw a characterization, and the monitors read what was written down.

So B-A2 protects the evidence base before it protects anyone's feelings. The register is the only asset this document has, which is QUEST 7.3's first stated cost arriving here from a different direction, and a mechanism that makes the record less honest has destroyed the thing it was measuring.

### 1.7 Position in the stack

BEARING sits at the weakest position on the family's precedence gradient, beside QUEST. It narrows nothing and permits nothing. It records.

Section 3 states the leaf rule and why non coercion is a property of the dependency graph rather than a promise the document makes about itself.

### 1.8 Relationship to the reference implementation's published canon

The reference implementation holds a published four module alignment course. It is canon. BEARING MUST NOT contradict it, and several of its structures are canon versions of rules this family invented independently, which is the strongest available evidence that they are structural.

**What BEARING binds to.** A position per named dimension, held independently and never summed (11.1). A self referential time series, this placement against the operator's own earlier placement on the same named position (11.3). The rule that a machine never moves the dot, which is published product canon and not a rule invented here (11.4). The argmin as a pointer to where attention goes, which is the only derived quantity in the entire published alignment system (11.2).

**What stays a teaching device under POLARIS 7.3.** The pillar tier names, the pole labels, the somatic honesty check, the framings for the furthest left position and for concentrated attention, and the movement idioms. Kept because compression aids recall, marked non normative, and never citable as grounds for a decision (11.5).

**Q-A1 is cited here as the published material's own position and not as an import.** The material refuses the score in published text twice over: "This isn't a test I pass or fail. There are no good dots and bad dots. No score at the end that says whether I'm doing life right." Elsewhere: "It's not a scorecard. It's a mirror." "Not a personality test. Not a diagnosis. A map." Its style guide bans the rating idiom outright and enforces the ban by grep. A specification that introduced a rating would contradict a grep enforced house rule of the material it serves, which is a stronger constraint than a design preference.

**One prose requirement travels with the material and is honoured here.** TETHER 2.1 already requires that this family's normative text not describe a person as a computer or a machine. Where the published material uses that framing it is teaching material under POLARIS 7.3, and it does not enter normative text in this document.

**Two known discrepancies are not inherited.** An archived hand drawn diagram inverts the poles, states a different pillar count, and lists a different tier count. The course is canon and the archive is superseded. The canonical idea note remains at status seed and the material's own governing decision is recorded as enforced manually, with the honest note that nothing enforces it today. BEARING binds to the course text.

### 1.9 On this document's name, and the vocabulary rule that follows

A **bearing** is an actual heading measured against an intended one, which is exactly this document's subject: the standing gap between conduct and declared purpose. `drift` is already the family's word for that gap, at POLARIS 11.5 and QUEST 4.4, so BEARING inherits vocabulary rather than inventing it. You take a bearing by sighting a body external to yourself, which is TETHER 1.2 as a physical act. And the word asserts no medical purpose, which matters, because intended purpose is set by what a document says about itself.

**The one serious objection, answered rather than deflected.** A bearing is expressible in degrees, so a reader may hear a scalar. It is not one. A bearing is a **direction** and not a **magnitude**: it moves freely in both directions, it is scoped to one sighting, and it accumulates nothing. That is precisely the shape Q-A1's monotonicity discriminator permits, in the same way the argmin is permitted and a total is not. BEARING states no number about an operator anywhere, and 5.6 enumerates exhaustively the three derived quantities it permits. The name is a pointer, which is what the whole document produces.

**`bearing` is used in the navigational sense only** and never in the mechanical part sense or the comportment sense.

**`instrument` is KIT 1.5's reserved word, and BEARING carries three uses of it, so the resolution is stated rather than left to context.** KIT 1.5 reserves the bare word for the body as TETHER 2.1 defines it, forbids prose from using it for a device, and excepts the TETHER 2.3 controlled vocabulary value by name. BEARING inherits all three parts and adds the discriminator for its own third use.

- **In prose, `instrument` names the body.** BEARING MUST NOT use it for a device, a tool, or a measuring apparatus. A measuring device is a KIT item of class `sensor`.
- **`instrument` as a TETHER 2.3 reference source value** names a reading a device produced. It is excepted by name, exactly as KIT 1.5 excepts it, and it is the value that appears in a `condition` entry or a `fired_signals[]` entry.
- **`instrument` as a raise type at 6.1** names a routing category and never a state of the operator. Per 6.1 a raise type names what must happen next, and what this one names is a referral to the qualified human of 6.3.

**Failure mode, imported from KIT 1.5 without modification:** specification prose using the reserved word for a device is malformed and MUST be rejected in review. **Where the ambiguity reaches a record, an observation whose reference source cannot be resolved between the body and a device is recorded `unevaluated` and MUST NOT be admitted with either resolution guessed.** A raise carrying such an observation is `unknown-no-data` on that input and raises under 4.10.

**Equipment is KIT's and the raise type does not annex it.** Where an `instrument` raise's ladder rung 2 returns a finding about a sensing item, the finding is about that item's calibration state under KIT section 6, it is recorded as a rung 2 finding under 7.1, and it is never a fault of the body.

**`calibration` bare is KIT's, and names item calibration.** This document's subject is **`alignment calibration`**, and every normative use MUST carry the qualifier. A normative sentence containing an unqualified use is ambiguous, therefore untestable, therefore prose, and MUST be corrected before Status leaves Draft.

**The overloaded movement word is split.** The published material uses `bar` in two senses: one of the ten spectra, and a unit of displacement. Where this document needs both, each is named distinctly. A **`position`** is one of the operator's declared spectra. A **`notch`** is a unit of displacement on one position. A notch commitment is a QUEST side quest with a declared bound and a termination condition, and it is **not defined here**.

---

## 2. Definitions (protective)

### 2.1 Alignment calibration, and the two cadences

**Alignment calibration** is the standing work of keeping actual conduct aligned with declared purpose. It is a practice with a record, not a state anyone attains.

Two cadences exist, they are different objects, and collapsing them produces an ambient stream of self ratings. Both are canon in the published material.

The **informal check in** is any day, unsaved, and produces no record. The material describes it as a way to ask yourself questions, explicitly not a locked in thing. **This document places no requirement whatever on the operator's practice of it.** It places exactly one requirement on the implementation, at 9.16, which is that the implementation MUST NOT record one. The operator's freedom and the implementation's obligation are two statements and neither is the other.

The **formal review** is saved, signed, and revisited on a declared interval, and it is the baseline against which the operator's own later placement is compared. It is Arm B, and section 9 governs it.

### 2.2 Monitor, protocol, signal, firing

A **protocol** is the declared record of a monitor: its question, its trip condition, its inputs, its timing requirements, its envelope, and its raise type. Section 4.1 states the fields.

A **monitor** is a protocol in force, evaluated on its declared interval.

A **signal** is one input value read from a record that already exists. A signal **fires** when it meets the condition the trip condition ranges over. A monitor **trips** when its trip condition is satisfied.

### 2.3 The four time requirements

Kept structurally distinct, never interchangeable, and each declared separately.

| Term | What it is |
|---|---|
| `window` | The measurement span the trip condition ranges over |
| `interval` | The cadence on which the monitor evaluates |
| `persistence` | The consecutive evaluations, or the within window density, required before a trip becomes a raise |
| `duration` | The elapsed span over which fired signals were present, carried on an `instrument` raise |

QUEST 4.4 already had to state that a window is a measurement span and not a cadence, which establishes that the conflation is the natural error rather than a hypothetical one. An implementation that declares one of these and reads it as another has built a monitor that either never fires or never stops.

### 2.4 Run, raise, raise type, ladder finding, routing target, expiry

A **run** is one evaluation of a monitor, recorded whether or not anything tripped (4.11).

A **raise** is the emitted call-out. It is an event addressed to a human, carrying evidence. It is never a finding the operator reached, a state the operator adopted, or a value stored about them. Section 5 states its closed schema.

A **raise type** is one of six values from the closed vocabulary at 6.1.

A **ladder finding** is the recorded result of one of the four attribution rungs of section 7.

A **routing target** is the party a raise goes to, **derived** from the raise type by the table at 6.3 and never authored on the protocol.

An **expiry** is the declared time after which a raise is no longer a current statement about anything. Every raise carries one (5.11).

### 2.5 The declaration

The **declaration** is the operator's declared priorities under the POLARIS operator adapter, together with their statement of what evidence in the record would count as serving each.

That second half is what makes an alignment monitor possible at all. A declared priority with no statement of what would count as serving it is not measurable, and a monitor citing one reports `unknown-undeclared` under 12.5 rather than inventing a reading.

The declaration is a forward citation into the POLARIS operator adapter, which is unwritten. Until it lands, an operator declares priorities under POLARIS directly, and BEARING cites them as `criteria`.

**The declaration field table.** On 4.1's pattern, because the declaration is the object every monitor measures against and an object with no field schema has no completeness a check can resolve against. **A declaration MUST declare every one of the following fields.**

| Field | What it holds | Required by |
|---|---|---|
| `priorities[]` | The operator's declared priorities under POLARIS, each with the operator's statement of what evidence in the record would count as serving it | 2.5, 12.5 |
| `qualified_human` | The named party an `instrument` raise routes to, with a contact method and a review interval | 6.3, 6.5 |
| `second_party` | The declared fallback recipient of 8.4, per 2.10 | 8.4 |
| `liveness_receiver` | A receiver outside BEARING to which the periodic positive liveness token is emitted | 4.12 |
| `raise_budget[]` | A maximum per period for each of the four budgetable raise types, per 4.14 | 4.14 |
| `unchanged_n` | The N of 10.3, the number of consecutive reviews across which an identical review is recorded `unchanged` | 10.3 |
| `review_interval` | The cadence on which a formal review is held | 9.16, 10.4 |
| `minimum_interval` | The floor between formal reviews, per 9.16 | 9.16 |
| `position_set` | The operator's declared positions, with the single declared ordinal scale of 11.2. **Optional at every tier**, per section 11's opening | 11.1, 11.2 |
| `refusal_seeds[]` | One declared seed per declared refusal, per 12.1 | 12.1 |
| `clinical_direction` | Per 3.4, from the closed vocabulary stated there | 3.4 |

**Failure `BR-86`:** a declaration missing any required field is `unknown-undeclared` on that field from the moment of its declaration, on KIT 6.1's construction, and the absence is itself a `conformance` raise naming the missing field. **The declaration is not rejected and is not partially voided**, which is the one place this table departs from `BR-02`: a protocol is machinery and a partially stored protocol is a monitor whose envelope is unknown, while a declaration is the operator's own statement of purpose and refusing to store it would penalise an incomplete declaration, which B-A4 forbids. **`position_set` is optional and its absence is not a missing field**, per section 11's opening sentence.

**No field in this table carries a value this specification supplies**, per inherited absolute 5 and 16.1. Each is a structural cardinality: the table states that an interval is declared and never what the interval is.

### 2.6 Review, period, docket, disposition, declaration outcome, placement, notch

A **review** is one Arm B sitting: an act with a record and a signature (9.1).

A **period** is the span a review covers, ending at the review and beginning at the prior one.

A **docket** is the frozen set of records the review dispositions (9.3, 9.5).

A **disposition** is one of five values the operator writes on one docket item (9.6).

A **declaration outcome** is one of three values the operator writes on the declaration as a whole (9.12).

A **placement** is the operator's own record of where they sit on one declared position, with a timestamp and a source (11.1).

A **notch** is a unit of displacement on one position (1.9). BEARING defines the word and defines nothing else about it.

### 2.7 Calibration state

Three values, and no fourth: `current`, `lapsed`, `undeclared`. Section 10.4 governs. None of the three is a judgement, and none of them carries a cost, per B-A4.

### 2.8 `unevaluated`, `unknown`, `untested`: three states, none of which is health

`unevaluated` names a reading BEARING could not produce because the element it depends on was absent or lapsed. `unknown` names a missing valid input. `untested` names a declared element whose test has not been exercised.

None of the three is a pass. None is a fail. None is evidence of health, and an implementation that renders any of them as an absence of concern has inverted the posture the document requires (4.9).

### 2.9 What BEARING does not define, and where each vocabulary lives instead

Stated as a routing table so that no implementer has to infer the boundary.

| Not defined here | Owner |
|---|---|
| Crisis criteria, the crisis path, rungs, escalation conditions | TETHER section 9 and 7.1 |
| Consequence classes for a crossing | TETHER 3.2 |
| The declared environment, input classes, the mismatch register | HABITAT |
| Item calibration and sensing item output states | KIT sections 5 and 6 |
| The inventory register, and the rule that possession is never evidence of a fault | KIT 2.10 and KIT section 10, in particular KIT 10.1 |
| Capability, verification, lapse, quest bounds, quest scoped drift | QUEST |
| Purpose, refusals, obligations, loyalties, amendment machinery | POLARIS |
| Artifact classes and retention | TRACE |
| Custody classes and inference authorization | CONFIDE |
| Post crossing retention | RETAIN, through its operator adapter |
| Indication content, criteria content, thresholds, quantities | Author written guides, section 16 |

### 2.10 Agent, and the declared second party

Both words are load bearing in requirements elsewhere and neither was defined, so both are defined here.

**An `agent`** is any non human party that acts on a BEARING record: a scheduled process, a script, a service, a model, or a model backed assistant, whether or not it holds an identity in the stack. Section 13 governs what one may do.

**A model backed agent is a model for the purposes of 4.6**, and the two requirements are one requirement. The name of the actor does not change the act: where an agent's output determines that a monitor fired, that it did not fire, or that a raise may leave the open set, 4.6 is engaged whatever the actor is called. 13.1 states the consequence.

**The `second_party`** is the party the operator names in their declaration as the recipient of a `crisis` raise where no escalation path is declared or the declared path is stale, per 8.4. It is a named human with a contact method. **It is not the TETHER 2.3 reference source value `second-party`**, which names an observation another party produced and is a different object entirely; 15.2 uses the reference source sense and 8.4 uses this one.

**Failure `BR-90` governs the absence**, per 8.4. A declaration naming no second party does not make 8.4 vacuous: the raise routes to the operator with the target recorded missing, on 6.5's construction, and the missing declaration is simultaneously a `conformance` raise.

---

## 3. The Leaf Rule and What Follows From It (protective)

### 3.1 The rule, and its mechanical check

**B-A1 restated once, in the place where its check lives.** No requirement outside BEARING resolves against a protocol, a run, a raise, a ladder finding, a docket item, or a review record.

The check is mechanical and runs against the specification text of the family rather than against an implementation: **no document other than BEARING contains a normative sentence whose satisfaction depends on the existence or the state of a BEARING element.** It is a single pass over **every other document in the stack and their adapters**, and it is checkable by search.

**The documents are named rather than counted**, because section 20 makes counts and codes unstable while Status reads Draft, and because the four an author is most likely to wire back into a raise are the four whose seams BEARING touches. The pass covers **BLUEPRINT, CONFIDE, DEFER, HABITAT, KIT, POLARIS, QUEST, RETAIN, SPEAK, TETHER, and TRACE**, together with every operator adapter in `spec/adapters/`. A pass that omits TETHER, HABITAT, KIT, or QUEST has not run the check, whatever it reports.

**Failure `BR-01`:** citing text is non conformant specification text and MUST be rejected in review. Where an implementation nonetheless builds the dependency, the gate that cited the BEARING element records `unevaluated` rather than `passed`, in the POLARIS section 8 disposition, and is re resolved on its actual grounds.

### 3.2 Why non coercion is a graph property

The entire misuse surface of this document concentrates in one event: **a raise becoming consequential.** Every harm the document is written against runs through it. A purity ladder needs a raise to gate a capability. A screening use needs a raise to inform a decision about a person. A shame engine needs a raise to cost something.

If nothing above may read a raise, none of those can be built. The property is not a promise about intentions, it is a property of the dependency graph, and a reviewer confirms it in one pass.

This is K-A3's severability construction, which KIT already uses to keep itself independent of QUEST, pointed at the property the author cares most about. K-A3 also supplies the procedure: the requirements that mention the forbidden neighbour are enumerated, and each is shown to resolve without it. BEARING's version of that procedure is trivial in one direction and total in the other. **BEARING cites the family throughout. The family cites BEARING nowhere.**

### 3.3 The unlocking model, expressed without a gate

The motivating claim is that alignment calibration unlocks the capability to move toward POLARIS. Expressed carelessly, that becomes a purity ladder in which people earn their capabilities by proving alignment, and it violates inherited absolute 4 the moment the unearned state carries a penalty.

Expressed correctly, it costs a **reading** and never a capability.

With no current declaration, or no current review, Arm A's alignment output is `unknown-undeclared`, and there is nothing to read. Nothing was withheld, so nothing has to be earned. The operator who has not reviewed holds every capability, authority, item, and quest they held before, and BEARING simply cannot say anything about whether their conduct served their purpose, because the thing conduct would be measured against is not there.

**TETHER 7.3 is cited as the model and never as a dependency**, which B-A1 permits, since the leaf rule forbids only the other direction. The model has three properties BEARING copies exactly: the gate is satisfied by evidence rather than by signature, its lapse produces `unevaluated` and never `failed`, and the rung ladder it sits on blocks nothing.

**The published engineering analogue is stated because it is exact.** A readiness check removes an endpoint from the evaluated set, kills nothing, and rejoins automatically on the next passing evaluation. A liveness check restarts the container. Importing the wrong one takes capability away from an operator at the moment they most need it, which is the moment they stopped being able to complete a review.

### 3.4 Coercive and protective labels, and clinical direction

Imported from KIT 3.5 and QUEST 3.4 **by construction**, rather than re derived. The derivation is theirs and the mechanism is identical.

A **coercive** rule generates pressure toward doing less care, or toward reporting care as drift. Its compliant response can consist of removing something. A **protective** rule only ever narrows what may be claimed from a record; its compliant response is a better declaration and never a reduction. A section placing requirements only on this document's own text, on its vocabulary, or on an implementation's conformance apparatus carries `neither` and states why.

**Imported from KIT 3.5 without modification: a `neither` section does not inherit the coercive default and never resolves `out-of-scope`**, because there is no operator record for it to resolve against. The sentence is imported rather than left to inference because the coercive default in the drafting requirement above is otherwise reached by any section whose heading label is missing or malformed, and sections 18 and 19 are the two whose subject is this document's own apparatus.

**The classification in this version.**

**Coercive: 9.12 and 12.5.** Each has a compliant response consisting of doing less or of reporting care as drift. 9.12 constrains the declaration outcome and therefore reaches a declared priority covering clinically directed care. 12.5 reports record that cannot be attributed to a declared priority as `unattributed` and accompanies a `declaration-review` raise with a compositional report, which for an operator on TETHER 7.1's crisis or impaired rung would report their treatment as drift.

**4.6 is protective and was previously classified coercive by mislabel.** Retiring, or declining to declare, a monitor whose predicate cannot be evaluated mechanically is not doing less care and is not reporting care as drift. It removes a piece of machinery, not a treatment, and its compliant response is a narrower monitor or an honest gap reported under 4.2, which is the shape of a better declaration. Classifying it coercive routed the one requirement that keeps a model out of the fire or no fire decision into the clinical exclusion, where it would have been suspended for every record whose clinical direction is `unconfirmed`, which 3.4's own default makes the normal state.

**Protective: 1, 2, 3, 4, 5, 6, 7, 8, 9 excluding 9.12, 10, 11, 12 excluding 12.5, 13, and 14.**

**Neither: 15, 16, 17, 18, 19, and 20**, which place requirements on this document's own text, on the guide layer outside it, or on an implementation's conformance apparatus, and never on an operator's record.

**Every declaration, protocol, raise, and review record MUST carry a declared clinical direction field.**

**The vocabulary is closed at three values: `directed`, `not-directed`, `unconfirmed`.** A fourth value is non conformant. `unconfirmed` is added to 5.9's conformant list, because it names what is missing and never a property of the operator.

**Failure mode, failing closed toward protection: a record whose clinical direction field is absent, or declared `unknown`, is read as `unconfirmed` and MUST be handled as clinically directed until the operator declares otherwise.** The field is surfaced `unconfirmed`, which is a report that a declaration is missing and never a report that anything is unjustified. It MUST NOT be used to withhold, delay, or downgrade anything.

**The disposition. A coercive check resolving against a clinically directed record returns `out-of-scope`. It never returns a pass and never returns a fail**, because a pass would let the exclusion be read as satisfaction and a fail would be the pressure the exclusion exists to remove.

**What `out-of-scope` suspends, stated because the reading that suspends everything is the cheap one.** **`out-of-scope` suspends the reporting of a conformance result and never the underlying MUST NOT.** A prohibition stays in force against every record in every state of the clinical direction field. **A write time rejection disposition fires regardless of clinical direction**, and `BR-06` and `BR-66` are the two named cases: a monitor whose predicate requires a model is rejected at write time whatever the clinical direction of the records it would read, and an inferred or reconstructed priority set is rejected at write time on the same terms. What is suspended is the report that a check passed or failed, which is the only thing that could generate pressure toward doing less care. Nothing an operator can do to a clinical direction field makes a forbidden write succeed.

**Failure `BR-87`:** a MUST NOT suspended, a write time rejection not fired, or a check reported as a pass or a fail rather than `out-of-scope`, on the strength of a record's clinical direction, is non conformant. The suspension is void, the rejection is performed, and the result is corrected to `out-of-scope`.

**`out-of-scope` is reported and is never silent.** A run resolving `out-of-scope` emits a `monitor` raise with `reason: clinically-excluded`, per 4.10, so the exclusion is a fact the operator encounters rather than a gap in a report nobody can see.

**The exclusion report, required by 9.1 and defined here.** A review record carries an **exclusion report**, which is an enumeration and never a count, per 5.6. It carries, for the reviewed period: **each coercive check that resolved `out-of-scope`, named by its governing subsection; the identifier of each record it resolved against; and the period bounds over which the enumeration was taken.** It carries no characterization, no cause, and no total. **An empty exclusion report is a conformant exclusion report** and is recorded as the empty enumeration, never as an absent field, because an absent field is a missing field under `BR-35` and an operator with no excluded checks would otherwise be unable to close a review.

**A tier item, health invariant, or self test check that an operator could satisfy by declining care, or by consuming less on clinically directed care, is malformed specification text and MUST be rejected in review**, per inherited absolute 4. Section 10.5 restates this once, in the one section where the temptation actually lives.

**Every section label is stated in that section's heading**, per the drafting requirement, **using at least one of the three literal strings `coercive`, `protective`, or `neither`. Where a heading carries more than one of the three, each MUST be bound in that heading to an explicitly enumerated subsection range**, which is how sections 9 and 12 read. **A heading carrying a description of a label, an inheritance rule, or a composition note in place of a label is unlabelled**, and an unlabelled top level section is treated as coercive. Self test check 12 asserts this mechanically, because it is the class of error a script catches and a reader does not.

---
## 4. Arm A: Monitors (protective)

### 4.1 The protocol record

**A protocol MUST declare every one of the following fields.**

| Field | What it holds |
|---|---|
| `id` | The protocol identifier |
| `subject` | The identity whose declaration this monitor measures against, compared at write time per B-A5 |
| `question` | The plain statement of what the monitor reads for |
| `trip_condition` | A decidable predicate over the declared inputs |
| `inputs[]` | Each input with its owning document, its `input_source` from the closed enum below, and its TETHER 2.3 reference source |
| `window` | The measurement span the trip condition ranges over |
| `interval` | The evaluation cadence. **Not declared, and MUST NOT be declared, where `raise_type` is `crisis`**, per 4.4 |
| `persistence` | The requirement a trip must satisfy before it becomes a raise. **Not declared, and MUST NOT be declared, where `raise_type` is `crisis`**, per 4.5 |
| `applicability_envelope` | A decidable predicate over the inputs, per 4.7 |
| `raise_type` | One of the six values of 6.1 |
| `routing_latency` | The declared span inside which a raise from this monitor MUST be routed, against which 6.2's `unrouted-past-latency` and 6.4's closure discipline resolve |
| `cooling_period` | The span after a review that dispositioned a raise from this monitor during which its threshold, window, persistence rule, interval, or acceptance band MUST NOT be revised, per 9.11 |
| `ladder_latency` | Declared where `raise_type` is `instrument`. The span inside which the four ladder findings of section 7 are recorded. **It bounds the ladder and never the routing**, per 7.3 and B-A3, and an elapsed `ladder_latency` never delays, withholds, or conditions a routing |
| `error_posture` | Which error this monitor is built to avoid, stated explicitly |
| `acceptance_bands` | Declared before the first run, per 4.13 |
| `basis` | The stated grounds on which these inputs are held to bear on the declared element |
| `clinical_direction` | Per 3.4, from the closed vocabulary of three stated there. Absent or `unknown` reads `unconfirmed` and is handled as clinically directed |
| `label` | `coercive`, `protective`, or `neither` |
| `maintainer` | The named human who receives this monitor's own `monitor` raises |

**A protocol MUST NOT carry a `routing_target`.** The routing target is derived from `raise_type` by the table at 6.3, so that no protocol can route its own fault to itself and no maintainer can quietly narrow where their monitor's raises go.

**`routing_latency` and `cooling_period` fail closed on 4.4's construction.** A protocol with no declared `routing_latency` reads `unknown-undeclared` from the moment of its declaration, is never reported as passing, and the absence is itself a `monitor` raise with `reason: undeclared`. **A protocol with no declared `cooling_period` takes the POLARIS 11.2 default of thirty days**, carried across verbatim on POLARIS's own stated ground that the default must be the one that cannot be abused, and the absence is a `monitor` raise with `reason: undeclared`. The two differ deliberately: an undeclared latency has no safe substitute, while an undeclared cooling period has one, and taking it is stricter than reading the field as zero.

**The `input_source` enum, closed, because 4.3's exclusion is a membership test and not a prohibition in prose.** An input's `input_source` MUST be exactly one of:

`tether-operator-register`, `tether-instrument-register`, `tether-fault-register`, `habitat-environment-declaration`, `habitat-mismatch-register`, `kit-inventory-register`, `kit-item-record`, `quest-capability-record`, `quest-quest-record`, `quest-completion-record`, `quest-verification-record`, `quest-activity-record`, `polaris-declared-element`, `polaris-amendment-record`.

**The set is closed over the named registers of TETHER 2.3, HABITAT, KIT, and QUEST, and over POLARIS declared elements. BEARING's own run, raise, review, docket, disposition, and placement records are not members of it**, with the single exception 4.12 already states, which is a monitor's own run history and which is not written as an `input_source` because it is not a declared input. **An input whose declared source is a record of the operator's engagement with BEARING, of their agreement with any declared element, or of their use of this tool has no valid enum value and cannot be written.** 4.3 states the class and this enum is where the class is excluded.

**Failure `BR-02`:** a protocol record missing any declared field is rejected at write time and is **not partially stored**, because a partially stored protocol is a monitor whose inputs are known and whose envelope is not. An authored `routing_target` is rejected and the table value governs. **A declared `interval` or `persistence` on a `crisis` protocol is rejected at write time** and the protocol is not stored, per 4.4 and 4.5. **An input carrying an `input_source` outside the closed enum is rejected at write time under `BR-03`**, and the protocol is not stored.

`basis` and `error_posture` deserve a sentence each, because they are the two fields an implementer will be tempted to leave blank. `basis` is what makes a monitor reviewable at all: without it, nobody can tell whether the inputs bear on the declared element or merely correlate with it in this operator's record. `error_posture` forces the trade to be declared rather than discovered, because a monitor built to avoid a missed signal and a monitor built to avoid a false one are different monitors, and 4.14's budget behaviour depends on which one this is.

### 4.2 Inputs are records that already exist

**Every input MUST name its owning document and section.** A monitor reads TETHER observations, HABITAT environment declarations, KIT calibration and item state, QUEST verification and lapse state, and POLARIS declared elements and amendment records. It reads what the family already collects.

**Where a monitor needs a signal the family does not collect, the implementation MUST emit a `monitor` raise with `reason: gap` naming the missing signal, and the monitor MUST NOT be declared runnable.** A gap is a thing to report, not a licence to add a questionnaire.

**BEARING MUST NOT define, and a monitor MUST NOT require, present, or depend on, any question, prompt, item, scale, anchor, rating, or inventory administered to the operator.**

**Failure `BR-03`:** rejected at write time. A protocol declaring such an input is not stored; a monitor discovered to depend on one is retired under 4.15.

Three independent grounds, each sufficient on its own, all stated because a reader who defeats one will otherwise reintroduce the mechanism.

**First, it is the active self diagnostic tool this document exists partly to refuse.** Asking a person to look inward and score what they find is the mechanism that produces rumination and self labelling, and it converts a monitor into an examination.

**Second, inquiry addressed to the party under review is the weakest evidence class and cannot alone support a conclusion.** The audit profession places inquiry at the bottom of its evidence hierarchy and holds that inquiry alone cannot support a conclusion about a control's effectiveness. POLARIS 5.3 says the same thing in one sentence: an obligation attested by the party responsible for it is not measured.

**Third, in any employment adjacent deployment the question is already the violation.** An inquiry likely to elicit information about a disability is prohibited by virtue of being **asked**, independently of the answer and independently of what is done with it. A specification that shipped an item bank would therefore make its own conformant implementations unlawful in a deployment its own R4 refusal already forbids, which is a strong signal that the mechanism is wrong rather than merely risky.

### 4.3 Forbidden signal classes

**A monitor MUST NOT read, and a guide MUST NOT declare, any signal whose subject is the operator's perceived honesty, insight, cooperation, engagement, responsiveness to the system, agreement with the framework, adherence, promptness, tone, affect, sentiment, or use of this tool.**

The class is **excluded from the `input_source` enum defined at 4.1** rather than forbidden in prose, so the check is structural and is a membership test a write path can implement. The enum is closed over the named registers of TETHER 2.3, HABITAT, KIT, and QUEST and over POLARIS declared elements, and **BEARING's own run, raise, review, docket, disposition, and placement records are not members of it.** An input whose declared source is a record of the operator's engagement with BEARING itself, of their agreement with any declared element, or of their use of this tool has no valid enum value and cannot be written.

**The residual case is named, because a determined implementer reaches it.** A record held in another document's register that nonetheless has the operator's engagement with BEARING as its subject, such as a POLARIS declared element whose content is an assertion about how promptly the operator reviews, is excluded by this subsection's first sentence even though its `input_source` is a member of the enum. The enum closes the structural route and this sentence closes the content route, and neither alone is sufficient.

**Failure:** rejected at write time under `BR-03`, and specification or guide text declaring one is non conformant. **Self test check 11 seeds an engagement sourced input and asserts the rejection**, so the membership test is exercised rather than assumed.

The rationale is stated with its history, because this is the class an automated monitor is most tempted to collect. Compliance telemetry is the cheapest telemetry there is: the system already logs whether the operator opened the review, whether they dispositioned promptly, and whether they agreed. It is also the class with the worst record. Signals of this kind, inferred from patients' responses as symptom denial and poor insight, produced a documented racial disparity in one diagnosis. The same class, formalized, produced the state category whose enumerated criteria included perseverance, struggle for the truth, and conflict with authority.

**It is the single step by which an alignment monitor becomes a loyalty monitor**, and there is no version of it that is safe because it is well intentioned.

### 4.4 The trigger is periodic and never invoked, and the crisis carve out

**A monitor whose `raise_type` is not `crisis` MUST declare an interval and MUST evaluate on it. Such a monitor MUST NOT be triggered by the operator's suspicion, and an implementation MUST NOT offer an evaluate now control as a substitute for the interval.**

**The crisis carve out, stated here rather than only in 8.2's rationale, because 8.2 governs what happens after emission and this subsection governs whether emission ever occurs.**

**A monitor whose `raise_type` is `crisis` MUST evaluate on the write of a record within its declared inputs, and MUST NOT declare or evaluate on an interval.** Its evaluation is a property of the write path and not of a clock. **The prohibition on an evaluate now control does not reach it**, because there is no interval for such a control to substitute for: on write evaluation is the declared trigger rather than a bypass of one.

**A `crisis` monitor is exempt from 4.5's persistence requirement and from 5.1's `run_id` requirement.** Where a `crisis` raise is emitted from an on write evaluation that produced no run record, `run_id` reads `on-write` rather than a run identifier, and the raise is conformant. A `crisis` monitor MAY additionally be evaluated on a periodic sweep as a backstop, and a raise emitted from such a sweep carries the sweep's `run_id`; **a backstop sweep MUST NOT be the only evaluation path for a `crisis` monitor**, because a sweep is an interval by another name.

**Failure `BR-04`:** a non `crisis` monitor with no declared interval is `unknown-undeclared` from the moment of its declaration and is never reported as passing, on KIT 6.1's construction. A non `crisis` monitor evaluated outside its interval records the run out of schedule and its result `unknown-stale`. **A `crisis` monitor that declares an interval, or that evaluates only on one, is non conformant at every tier, per `BR-89`**, because both are the same failure: a disclosure written on day one of a declared interval carried on day thirty, if at all.

**The asymmetry is settled in advance rather than in the moment**, which is the same reasoning 8.2 gives for the persistence exemption and the same reasoning inherited absolute 3 gives for refusing self gating. Periodic evaluation is correct where the cost of a late signal and the cost of a noisy one are comparable. In this lane they are not.

The construction is KIT 6.1's and this is the ninth time the family has used it: silence resolves to the strictest outcome immediately, because otherwise the compliant response to an interval requirement is to decline to declare one and live permanently in a state no check can name. Design note 0006 flags this repetition as a candidate for a single home, and BEARING copies rather than generalizes, because generalizing it is an RFC and not a drafting decision.

**Why periodic rather than triggered.** A monitor that runs only when the operator suspects something is a monitor that never runs when it matters, because **the suspecting faculty is the one that may be impaired.** TETHER 1.2 reaches this for instrument drift, HABITAT section 8 reaches it for the silent floor, and QUEST 4.4 reaches it for quest inversion. Three documents arriving independently at the same finding is the strongest available evidence that it is structural, and BEARING is the fourth.

### 4.5 Persistence, the sub threshold observation is recorded, and the crisis carve out

**A monitor whose `raise_type` is not `crisis` MUST NOT raise on a single evaluation.** A trip becomes a raise only when the declared persistence requirement is satisfied.

**A firing that does not satisfy persistence MUST be recorded `below-threshold` with its window and its fired signals, MUST NOT emit a raise, MUST NOT be deleted, and MUST be available to the next evaluation.**

**The crisis carve out. A monitor whose `raise_type` is `crisis` MUST raise on a single evaluation, MUST NOT declare a persistence requirement, and is not reached by the prohibition in this subsection's first sentence.** `persistence_observed` on such a raise reads `not-applicable`.

**Failure `BR-05`:** a discarded sub threshold observation is non conformant, and a monitor whose persistence state does not survive between evaluations is non conformant on the same terms. A raise emitted on a single evaluation is void **excepting a raise of type `crisis`, which this row does not reach**. A `crisis` raise voided, delayed, or withheld on the strength of this subsection is non conformant at every tier under `BR-89`, the voiding is void, and the raise is routed.

Two reasons, and the second is the one implementers underweight. A discarded sub threshold observation lets a monitor stay silent while something recurs, because each occurrence is individually below the line and nothing accumulates the pattern. And single signal triggering is the documented path to a muted monitor: in a population where fewer than one in a hundred carry the condition, four in five can carry one flag, so a monitor that fires on one flag fires constantly and is turned off, which is 4.14's failure arriving through the trip condition instead of through the budget.

### 4.6 The trip condition is evaluable without a language model

**This subsection is protective and reaches every record**, per 3.4. It was classified coercive in an earlier draft and the classification was a mislabel: retiring, or declining to declare, a monitor whose predicate cannot be evaluated mechanically removes a piece of machinery and never a treatment, and its compliant response is a narrower monitor or an honest gap under 4.2, which is the shape of a better declaration. **`BR-06`'s write time rejection fires against every protocol regardless of the clinical direction of the records it would read**, per 3.4.

**A model MAY draft a candidate protocol, summarize a period for a human reader, or move a raise toward attention.** Each of those is permitted explicitly, because the useful things a model does here are worth keeping.

**A model MUST NOT be the party whose output determines that a monitor fired, that it did not fire, or that a raise may leave the open set.**

**A model backed agent is a model for the purposes of this subsection**, per 2.10, and 13.1 states the consequence at the point where an agent is otherwise permitted to compute a run.

**Failure `BR-06`:** a monitor whose predicate requires a model is rejected at write time, and any raise already emitted from it is void. A model authored transition out of the open set is void and the raise is restored.

This is POLARIS 4.3 arriving in the alignment domain, and the reasoning transfers without modification: if a model decides whether conduct is aligned, then the operator's alignment is the model's alignment, filtered through a prompt, subject to a provider's policy, and revisable with no amendment record. The regulatory line falls in the same place, at algorithmic inference about a person rather than at subject matter, so the safety rule and the perimeter rule are one rule and an implementer does not have to hold two.

**Where a declared element genuinely cannot be reduced to a predicate**, the correct outcome is not a model evaluated monitor. It is a narrower monitor capturing the mechanically detectable part, or no monitor and an honest gap reported under 4.2.

### 4.7 The applicability envelope

**Every protocol MUST declare an applicability envelope as a decidable predicate over its inputs.** Outside it, the run result is `out-of-envelope`, which is a `monitor` raise and is **never a pass**.

**Failure `BR-07`:** a protocol with no declared envelope is `unknown-undeclared` per 4.4's construction. A monitor evaluated outside its envelope and reported as `no-trip` is non conformant and the result is corrected to `out-of-envelope`.

Two documented failures collapse into this one requirement. Decision rules are routinely applied outside the population they were derived in, where their operating characteristics are unknown and are usually worse. And in one well studied hardware population, the strongest leading indicators were **absent in over a third of real failures**, which means a monitor can be correct inside its envelope and silent for the cases that matter most, without ever producing a wrong answer.

### 4.8 Multi source satisfaction, no carry forward, and the windowed bound

**Three requirements, stated together because they are one discipline.**

**A monitor MUST NOT be satisfiable by a single artifact class.** A trip condition resolving entirely against one class of record is a monitor that a single failing writer can silence.

**A period MUST NOT carry forward the prior period's result.** Each evaluation re establishes its own state from its own window.

**Each monitor MUST declare an expected production range for the record it reads**, and a period whose production falls outside that range **in either direction** reports `unknown-out-of-range`.

**Failure `BR-08` applies to the rendering of a result and `BR-09` to an unknown; a carried forward result is void and the run is re evaluated.**

This is the watchdog discipline, and all three parts of it are load bearing. A watchdog is satisfied only after several unrelated good things have happened. Its state is zeroed each cycle so that the good state is affirmatively re earned rather than inherited. And it treats **too fast exactly as it treats too slow**, because both are evidence that the thing producing the signal is not doing what the monitor thinks it is doing.

The concrete case the third part catches: a period of completions backfilled into one minute. The record looks complete, every count is satisfied, and the monitor reports the period out of range **without forming any view about why**, which is exactly the division of labour B-A2 requires.

### 4.9 There is no all clear

**The run result vocabulary is closed at ten values, and exactly one is recorded per run.**

| Result | Meaning |
|---|---|
| `no-trip` | The monitor ran, every declared input was present and inside its currency, the inputs fell inside the envelope, and the trip condition was not met |
| `raised` | The trip condition was met and persistence was satisfied |
| `below-threshold` | The trip condition was met and persistence was not satisfied |
| `unknown-no-data` | A declared input was absent |
| `unknown-stale` | An input, or this monitor's own run, is outside its declared currency |
| `unknown-undeclared` | A required declaration is absent |
| `unknown-unauthorized` | No current agent authorization covers this monitor, per 13.3 |
| `unknown-out-of-range` | Record production fell outside the declared expected range, per 4.8 |
| `out-of-envelope` | The inputs fell outside the applicability envelope, per 4.7 |
| `out-of-scope` | A coercive check resolved against a clinically directed record, per 3.4 |

**`no-trip` MAY be reported only where all four of its conditions hold.**

**An implementation MUST NOT render `no-trip` as clear, healthy, aligned, fine, on track, compliant, no concern, or as an absence of concern. It renders as the enumeration of inputs read and the window covered.**

**Failure `BR-08`:** the rendering is void and the result is re rendered as its enumeration. Specification, interface, or guide text rendering `no-trip` as an all clear is non conformant.

`no-trip` names what did not happen rather than a property of the operator, per KIT 2.11, and the naming is the requirement rather than a preference: **absence of an indication is not evidence of health.** A monitor that did not trip has told you that one declared predicate over one declared window was not satisfied, and it has told you nothing whatever about the person.

### 4.10 Every unknown is a raise, and a dead monitor is a fault

**Any `unknown-*`, `out-of-envelope`, or `out-of-scope` result MUST emit a `monitor` raise carrying the corresponding reason.** An `out-of-scope` result carries `reason: clinically-excluded`.

**`out-of-scope` is in this set for the reason the rest of the set is in it: an exclusion nobody is told about is indistinguishable from a check that passed.** 12.5 already states that the exclusion is reported as an exclusion rather than silently applied, and this is the raise that reports it. The raise says that a coercive check did not resolve, and it says nothing whatever about the care that caused the exclusion. It is addressed to the maintainer, per 6.3, and never to a clinician.

**A monitor with no run record inside its declared interval MUST emit a `monitor` raise with `reason: never-ran`, computed retroactively on detection, and recording its true first missed interval rather than the detection time.**

**Failure `BR-09`:** suppressing, batching away, or normalising an unknown is non conformant, the suppression is void, and the raise is emitted. An implementation that reports a period in which no monitor ran as a period with no raises is non conformant at every tier.

**Silence is never health.** The failure this closes is the one every monitoring system eventually has: the monitors stopped and the dashboard went green, because green was implemented as the absence of red. A dead smoke detector is a fault, and it is the fault most likely to be discovered at the worst possible time.

### 4.11 A run record is written on every evaluation

**A run record MUST be written on every evaluation**, carrying `protocol_id`, `run_at`, the window covered, the identifiers and reference sources of the inputs actually read, the `result`, and the `raise_id` where one was emitted.

**Failure `BR-10`:** an implementation that writes a record only on a trip is non conformant, because its register cannot distinguish a quiet period from a dead monitor. The two are the states that most need distinguishing and they are indistinguishable by construction if only trips are stored.

"Inputs actually read" is not the same field as the protocol's declared `inputs[]`, and the difference is the point. A monitor that declared four inputs and read two produced a result from half its evidence, and the run record is the only place that fact survives.

### 4.12 The protocol register, the independent clock, and the liveness token

**An implementation MUST maintain a protocol register** carrying, for each protocol, its inputs, interval, persistence, envelope, acceptance bands, last run time, and last result. **A monitor absent from the register MUST NOT emit.**

**`never-ran` MUST resolve against a time source BEARING does not write.**

**The operator declaration MUST name a receiver outside BEARING, and a periodic positive liveness token MUST be emitted to it. Loss of the token at the receiver is the fault**, and the receiver's detection of that loss is what makes the failure visible.

**A monitor MUST NOT read a signal BEARING itself produced, other than its own run history, and its interval MUST NOT be driven by the schedule it audits.**

**Failure `BR-11`:** a monitor emitting while absent from the register is non conformant and the raise is void. A `never-ran` computation resolving against a clock BEARING writes is non conformant. An implementation with no declared liveness receiver reports `unknown-undeclared` on every monitor and is non conformant at Tier 2.

Three traditions converge here and each supplies one clause. A watchdog cannot run on the clock that may fail, which is why the time source is external. An auditor must not assume ownership of the monitoring it evaluates, which is why the register is not the monitor's own state. And an observer must not evaluate their own tasks, which is why a monitor's interval is not set by the schedule it audits. The three arriving at one requirement from three unrelated fields is the reason it is stated as an absolute of construction rather than as a recommendation.

### 4.13 Acceptance bands declared before the first run

**Every protocol MUST declare its acceptance bands before its first evaluation.**

**A band, threshold, interval, or window revised after a result it would have failed is a conformance failure**, recorded with its cause under POLARIS 11.3. **The prior band governs that period**, and the revision is enumerated as drift under 12.3.

**Failure `BR-12`:** the revision does not apply retroactively, the period is evaluated against the prior band, and the revision appears in the BEARING owned drift enumeration.

The cautionary history is stated because the honest half and the dishonest half came from the same effort. Publishing acceptance bands in advance was the honest half, and it was unusual enough to be worth copying. Redefining adequacy after the results arrived was read by the field as moving the bar so that weak results would present acceptably, and the reputational damage exceeded the damage the weak results would have done on their own.

**Once thresholds move to fit results, every number the system emits afterward is uninterpretable**, and Arm A's numbers are the only asset Arm B has.

### 4.14 The raise budget, which raises and never suppresses

**The operator MUST declare a maximum per period for each of the raise types `conformance`, `declaration-review`, `calibration-lapse`, and `monitor`, and MUST declare the behaviour on exceedance.** The maximum is a declared cardinality over emissions in the period and never a rate.

**The `crisis` and `instrument` lanes are unbudgeted. A declared budget for either is rejected at write time and is not stored.** The requirement in the paragraph above does not reach them, so an operator who declares four budgets has declared every budget this subsection requires and is conformant.

**Exceedance emits a `monitor` raise with `reason: budget-exceeded`, naming the producing monitors.**

**Suppression, dropping, batching away, or silencing to fit a budget is forbidden.**

**Failure `BR-13`:** an undeclared budget for one of the four budgetable types makes the check `unknown-undeclared` on that type, which is itself a raise. A suppressed raise is restored and the suppression is void. A declared budget for the `crisis` or `instrument` lane is rejected at write time and is not stored, and an implementation that applies one is non conformant at every tier.

**BEARING states no number here**, per inherited absolute 5. What it requires is that a number be declared and that its exceedance have a stated consequence, which is the K-A2 discriminator applied: a structural cardinality supplies no number an operator meets.

The documented endpoint is worth stating plainly, because a budget that suppressed would be defended as protecting the operator from noise. **Alarms turned off was the largest single counted contributing factor to deaths in a published sentinel event series**, and false rates approaching ninety percent are what produce the muting. The correct response to too many raises is a raise about that fact addressed to the maintainer, never fewer raises reaching the human.

### 4.15 A raise type or monitor with no defined recipient action is retired, never tuned

**Every monitor MUST name what its raise asks a human to do.**

**A monitor discovered to have no defined recipient action MUST be retired**, and the retirement recorded with its cause. **It MUST NOT be re thresholded, widened, narrowed, or otherwise tuned in place.**

**Retirement stops future emission and terminates nothing already emitted. The outstanding raises of a retired monitor remain `open`, continue to route under 6.3 on their existing targets, and leave the open set only by `routed` or `expired`**, per 5.10. **No party, including the maintainer, may close them, and retirement is not a lifecycle transition.**

**Failure `BR-14`:** a monitor with no defined recipient action that is retuned rather than retired is non conformant, and the retune is void. **A raise closed on the strength of its monitor's retirement is void and the raise is restored to `open`**, on the same terms as `BR-23`.

**The earlier draft of this subsection required the maintainer to close a retired monitor's outstanding raises, and that was 5.10 defeated in one clause.** 5.10 states that BEARING defines no state meaning resolved, cleared, not required, dismissed, or determined unnecessary, and that no identity may write one, and it calls itself the anti self talk requirement in structural form on the ground that the framework has no way to say help is unnecessary. Closing a queue on retirement is exactly that conclusion, stated as a mandatory requirement, addressed to the one party with an operational reason to want the queue empty. A raise's grounds do not evaporate because the monitor that noticed them was badly designed.

This is alarm rationalization, and the discipline was arrived at the expensive way, after a plant explosion during which two operators received two hundred seventy five alarms in eleven minutes. The finding was not that the alarms were wrong. It was that an alarm nobody can act on consumes the attention that the actionable ones needed, so the correct disposition is removal rather than adjustment.

Retirement is deliberately the cheap path and tuning is deliberately unavailable, because tuning is how a monitor nobody can act on survives review after review.

---

## 5. The Raise (protective)

### 5.1 The closed field schema

**A raise MUST carry exactly the following fields, and any field not in this list MUST NOT appear.**

| Field | Applies to | What it holds |
|---|---|---|
| `id` | all | The raise identifier |
| `raised_at` | all | When it was emitted |
| `protocol_id` | all | The monitor that emitted it |
| `run_id` | all **except `crisis`** | The run it came from. On a `crisis` raise emitted from an on write evaluation this reads `on-write`, per 4.4 |
| `subject` | all | The identity the emitting protocol's declaration is held by, compared at write time per B-A5 |
| `owner` | all | The named human accountable for this raise reaching a lifecycle state, per 6.4 |
| `type` | all | Exactly one value from 6.1 |
| `reason` | `monitor` | One value from the reason vocabulary of 6.2 and section 4 |
| `criteria` | all | The identifier of the declared element measured against, quoted verbatim per 5.8 |
| `condition` | all | An enumeration of observed record identifiers with timestamps and reference sources |
| `fired_signals[]` | all | Each with its TETHER 2.3 reference source, per 5.3 |
| `evidence_label` | all | `self-report-only` where every fired signal carries reference source `self-report`, per 5.4; otherwise `mixed-source`. Computed from `fired_signals[]` and never authored |
| `window` | all | The span the trip condition ranged over |
| `persistence_observed` | all | An enumeration of the evaluation identifiers within the window at which the trip condition was met, each with its timestamp. `not-applicable` on a `crisis` raise, per 4.5 |
| `duration` | `instrument` | The elapsed span over which fired signals were present |
| `functional_impact` | `instrument` | The enumerated records showing effect on named declared priorities, obligations, quests, or capabilities, per 15.3 |
| `baseline_comparator` | `instrument` | The self referential comparison against the operator's own prior record, per 15.4 |
| `ladder_findings[]` | `instrument` | The four rung findings of section 7 |
| `ladder_state` | `instrument` | `ladder-complete` or `ladder-incomplete`, per 7.1. **It MUST NOT appear on a routing record**, per 7.3 |
| `provisional` | all | Whether the emitting monitor is inside its declared bands per 4.13 |
| `lifecycle` | all | One of the three values of 5.10 |
| `routed_at` | all | When contact with the declared target occurred |
| `expiry` | all | Declared, never `indefinite`, per 5.11 |
| `artifact_class` | all | TRACE A2 Derived, per 14.1 |
| `custody_class` | all | Per 8.5 |
| `clinical_direction` | all | Per 3.4, from the closed vocabulary of three stated there |

**Failure `BR-15`:** a raise carrying a field outside this list is rejected at write time and **the field is not stored**, which includes the `cause` and `effect` fields 5.2 forbids. A raise missing a field required for its type is rejected on the same terms.

**The schema is closed over every element any other section requires a raise to carry, and this is a standing property rather than a claim about this version.** 19.2 carries a health invariant for it. Where a requirement elsewhere in this document obliges a raise to carry something that has no column above, the two rules deadlock at the write path and the conformant implementation is the one that does not emit, which destroys exactly the raises whose routing target is outside the operator. Adding the requirement without adding the column is therefore a defect in this section and never a defect in the emitting monitor.

**Four of the columns above are computed at render time from the fields beside them and are never authored**, which is why they add no interpretive surface: `evidence_label` from `fired_signals[]`, `ladder_state` from the presence of four findings, `provisional` from the emitting monitor's bands, and `subject` from the emitting protocol. An implementation MAY store them or compute them, and MUST NOT accept an authored value for any of the four.

This is B-A2 made mechanical rather than asked for. **There is no `severity`, no `score`, no `message`, and no `note`, so there is nowhere for an implementation to put an interpretation.** A closed schema is a stronger control than a prohibition, because a prohibition has to be enforced by whoever reviews the code and a closed schema is enforced by the write path.

**`persistence_observed` is an enumeration and its cardinality is a working value.** Its natural rendering is a ratio, "four of five", and a ratio is the one number in this schema an implementer would reach for as a sort key once 5.12 has refused severity ordering. **A cardinality computed from `persistence_observed` is a working value under QUEST 4.4's construction and MUST NOT be displayed, stored, or transmitted**, per 5.6.

**`provisional` is a property of the emitting monitor's conformance to 4.13 and is never a property of the raise's strength or of the operator.** It says that a monitor is running outside the bands it published in advance, which is a statement about the apparatus, on the same ground 15.1 uses for reliability figures. An implementation rendering it as a confidence, a reliability, or a qualifier on the indication has written a severity under a friendlier name, per 5.7.

### 5.2 Where the report stops

Government auditing standards define a finding as **criteria, condition, cause, and effect**, and then state that where the objective is to determine current status, developing **the condition alone** addresses the objective and the other elements are not necessary.

That is authoritative standards text licensing exactly Arm A's shape, and it is worth citing rather than asserting, because the instinct of every implementer will be that a report without a cause is incomplete.

**A raise MUST NOT carry a cause field or an effect field.** Cause belongs to Arm B, where the operator writes a stated cause on a disposition, and to the qualified human, who has the training and the access Arm A does not.

**Failure `BR-15`:** a `cause` or an `effect` field is a field outside the closed schema of 5.1, is rejected at write time, and is not stored. The disposition is stated here rather than left to inference, because this is the requirement that most distinguishes Arm A from a finding producing system and a normative requirement with no stated failure mode is prose.

### 5.3 Fired signals travel, with their reference sources

**Every raise MUST carry the signals that fired, and every fired signal MUST carry the TETHER 2.3 reference source of the observation it read.**

**Failure `BR-16`:** a raise emitted without per signal reference sources is rejected at write time.

A threshold crossed, reported without the signals that crossed it, is a word that does not describe its instances. A polythetic definition, meaning one satisfied by any sufficient subset of a larger set, admits two records that share **no signal at all** and reports them identically. The threshold is then a category name, and category names are what this document refuses to produce.

The reference sources travel for a second reason, which section 12.2 depends on: without them, an implementation cannot tell whether an obligation was measured or merely attested, and POLARIS 5.3's rule becomes unenforceable.

### 5.4 A self report only raise is labelled and never suppressed

**This CLARIFIES TETHER's consequential act on self report alone class, currently `F2`, and does not amend it.** The class reads: a threshold gating an act at K2 or above resolved with no reference source other than `self-report`, disposed of by recording the act unauthorized and the threshold `unevaluated`. **The content is stated alongside the code because TETHER section 13 declares its failure class numbers unstable while its Status reads Draft**, and this is one of only two places where BEARING deliberately departs from a sibling's disposition, so it is one of the two cross references most important to keep resolvable.

That class's subject is a **threshold gating an act at K2 or above**. Under B-A1 a raise gates nothing, so its disposition does not reach a raise, and the clarification is stated because an implementer applying it by analogy would otherwise reach the opposite answer.

**A raise whose fired signals all carry reference source `self-report` MUST be emitted, MUST be routed, and MUST carry `evidence_label: self-report-only`**, which is the field of 5.1's closed schema that carries this label and which is computed from `fired_signals[]` rather than authored.

**Failure `BR-17`:** suppressing, downgrading, or delaying such a raise is a violation, the suppression is void, and the raise is routed.

Applying F2's suppression here would fail dangerous. **The raises most likely to rest on self report alone are exactly the ones about states no item in the family measures**, and those are the ones a qualified human most needs to see. F2 protects a gate from opening on weak evidence, which is right. A raise is not a gate, and refusing to make a noise because the evidence is weak is how a smoke detector with a low battery behaves.

The label travels because reliability is a property of the observation regime as much as of the criteria, per 15.2. The receiving human is told what kind of evidence this is, and then decides.

### 5.5 An item recorded `unknown` does not suppress a raise

**This CLARIFIES KIT 6.5 and does not amend it.**

**Where an input is output from a sensing item recorded `unknown` under KIT 6.3, the monitor MUST NOT treat the input as satisfied, MUST NOT carry forward or interpolate a prior reading, and MUST emit a `monitor` raise naming the item and its calibration state.**

**The `unknown` input MUST NOT cause a raise that would otherwise have been emitted to be withheld.**

**Failure `BR-18`:** a raise withheld on the strength of an `unknown` input is restored, and the withholding is void.

KIT 6.5's direction protects against a gate **opening** on an uncalibrated number, which is correct and is one of KIT's most valuable requirements. Reused without examination it would protect against a raise being **emitted**, which is the same one way rule run backwards. The asymmetry is the point: uncertainty argues against authorizing an act and argues for making a noise.

### 5.6 Every number is a timestamp, an interval, an expiry, or an identifier

Q-A1 and its monotonicity discriminator are inherited and are not restated. This subsection states **BEARING's own scope under it**.

**The subject of this subsection is the operator. The permitted derived quantities whose subject is the operator, or the operator's own records, are exhaustively three.**

**Quantities whose subject is a monitor or an implementation are not governed here.** They are governed by 15.1 and by 19.2, under QUEST 3.3's first carve out, which excepts conformance health invariants counting malformed, missing, or defective records and requires every such number be labelled a conformance check. **The discriminator is the denominator, and it is stated so an implementer can apply it without judgement: a quantity whose denominator is monitor runs, monitor definitions, or an implementation's own apparatus has a monitor or an implementation as its subject; a quantity whose denominator is the operator's records has the operator as its subject, whatever the figure is called.** QUEST 3.3's failure clause governs a misapplication: a count labelled as a conformance check while ranging over well formed records is a mislabelled aggregate and is refused on the same terms.

**(i) The argmin over a declared placement set**, returned as a name or, on a tie, as the unordered tied set, **and only where the set declares a single shared ordinal scale and an origin pole. Never as a magnitude, a distance, an ordering, a runner up, or a tiebreak.** Section 11.2 governs, including the `undefined` result where no such scale is declared.

**(ii) The count of amendments made inside a declared cooling period**, labelled as a conformance check under QUEST 3.3's first carve out. **Any nonzero value is a POLARIS 11.5 conformance failure**, which is what makes it a defect count rather than a measure of a person.

**(iii) The count of monitors with no run record inside their declared interval**, labelled as a conformance check on the same ground.

**Everything else is an enumeration**, per QUEST 3.3, **including the prohibition on rendering an enumeration's cardinality as a summary value, a header figure, a badge, or a chart axis.**

**Intermediate sums computed in order to reach a disposition are working values** under QUEST 4.4's construction and **MUST NOT be displayed, stored, or transmitted.** **A cardinality computed from the `persistence_observed` enumeration of 5.1 is such a working value**, and is named because it is the one the schema mandates on every raise.

**Failure `BR-19`:** a forbidden value is rejected at write time and is void where already written. A requested scalar summary resolves `undefined`, never zero and never a computed value. A cross operator comparison resolves `incomparable`, and **consent from any party MUST NOT enable it.**

Both permitted counts range over **malformed or missing records** rather than over well formed ones, which is precisely the line QUEST 3.3's carve out draws. **A count of a person's raises would be a mislabelled aggregate and is refused on QUEST 3.3's own terms, with the enumeration returned in its place**, and 15.1 no longer requires one for exactly this reason.

### 5.7 Forbidden field names, enumerated so a script can check them

**A raise, run, protocol, or review MUST NOT carry a field named, or functionally equivalent to, any of the following.**

`severity`, `score`, `grade`, `level`, `rank`, `index`, `percentile`, `rating`, `risk`, `confidence`, `probability`, `likelihood`, `trend`, `streak`, `progress`, `percent_complete`, `message`, `summary`, `interpretation`, `assessment`, `recommendation`, `advice`, `next_step`, `note`, `comment`, `encouragement`, `warning`, `status_of_operator`, `diagnosis`, `condition_name`, `code`, `category`, `profile`, `pattern`, `type_of_operator`.

**Functional equivalence under a friendlier name is the same violation.** A field called `signal_strength` holding a severity is a severity.

**Failure `BR-20`:** the field is rejected at write time and is not stored. Specification, schema, or interface text defining one is non conformant and MUST be rejected in review.

The enumeration exists because it converts B-A2 from a request for good manners into a check a script runs, in the way the reference implementation's own style rules are already grep enforced. A reviewer asked whether a field is a characterization will sometimes say no. A script asked whether a field is named `confidence` always says yes.

### 5.8 No implementation authored prose

**Every human readable string emitted as part of a raise MUST be exactly one of:**

- a field label drawn from this document's closed vocabularies;
- a record identifier;
- a timestamp, an interval, a window, or an expiry;
- text quoted verbatim from the operator's own declaration, with its source record cited.

**An implementation MUST NOT author, template, generate, or interpolate natural language into a raise.**

**Failure `BR-21`:** the string is void and the raise is re rendered from its fields. A renderer holding natural language templates other than field labels is non conformant on inspection, and inspection of the templates is the check.

**This single requirement discharges four obligations at once**, which is why it is stated as a requirement about strings rather than as four requirements about tone.

It discharges the ledger rule of 1.3, because a renderer with no templates cannot add encouragement, scolding, or a motivational reading. It discharges the published style guide's grep enforced ban on the advice register and on second person imperatives, because there is no sentence for an imperative to live in. It discharges the regulatory condition that an output not be characterized, because the output is fields. And it discharges B-A2's enforceability, because prohibiting interpretation in general is a review judgement and prohibiting authored prose is a code inspection.

The permitted register that remains is the published material's own: an invitation to observation, never to action. Quoting the operator's declaration back to them, beside an enumeration of records, is such an invitation. Nothing else needs to be written.

### 5.9 State names

Extending KIT 2.11 from state names to raise field vocabulary.

**Conformant:** `unknown`, `unevaluated`, `unattributed`, `unclassified`, `unmeasured`, `untested`, `unconfirmed`, `unsigned`, `unauthorized`, `unchanged-uncaused`, `undifferentiated`, `incomplete`, `ladder-incomplete`, `below-threshold`, `no-trip`, `out-of-envelope`, `out-of-scope`, `out-of-range`, `never-ran`, `not-applicable`.

**Forbidden:** `misaligned`, `drifting`, `noncompliant`, `at-risk`, `concerning`, `elevated`, `abnormal`, `unhealthy`, `deficient`, `failing`, `behind`, `off-track`, `poor`, `inadequate`, `low`, `high`.

**`unattended` was listed here in an earlier draft and is removed. It is QUEST 4.4's disposition and is owned there**, it appears nowhere else in BEARING, and an unused entry in a closed vocabulary is an invitation for an implementer to invent a meaning for it, in the artifact this subsection itself calls the one place nobody reviews.

**`low` and `high` are forbidden so that a script catches their reintroduction**, which is the reason 11.2's earlier formulation of the argmin as the position furthest toward its declared low pole was a defect: 11.5 states that the pole labels are never good and bad, high and low, or healthy and unhealthy, and an ordering word smuggled into a derived quantity's definition is the ordering arriving where nobody is looking for it.

**Failure `BR-22`:** a register offering a forbidden state name is non conformant, and specification text defining one MUST be rejected in review.

Every conformant name above names **what is missing** or **what did not happen**. Every forbidden name names a property of the operator. The enum is the one place nobody reviews, and a fifth document in this family inventing `at-risk` would import the identity merge the family's second absolute forbids, in the one artifact that is copied into every interface without being read.

### 5.10 Lifecycle: three values, and no closure by conclusion

**A raise carries exactly one lifecycle value from three: `open`, `routed`, `expired`.**

**A raise leaves the open set by exactly two transitions.** `routed`, recorded when contact with the declared target occurred and carrying the evidence of that contact. Or `expired`, per 5.11.

**BEARING MUST NOT define a state meaning resolved, cleared, ruled out, not required, dismissed, handled, false positive, or determined unnecessary, and no identity may write one.**

**A raise that expired without being routed MUST be re emitted at the next evaluation** rather than dropped.

**Failure `BR-23`:** a fourth lifecycle value is non conformant specification text. A transition to a state meaning resolved is void and the raise is restored to `open`. An expired unrouted raise that is not re emitted is a health invariant failure.

**This is the anti self talk requirement in structural form.** The framework cannot be used to conclude that help is unnecessary, because **it has no way to say so.** There is no field, no value, and no transition that expresses it. That is a stronger protection than a rule against reaching the conclusion, because a rule is applied by the same faculty that would reach it.

### 5.11 Mandatory expiry

**Every raise MUST carry a declared `expiry`, and the value `indefinite` MUST NOT be declared**, per TRACE section 9's prohibition on indefinite retention outside A0.

**A raise emitted with no declared expiry is expired at the moment of emission.**

**An expired raise MUST NOT be cited as a current fact about anyone, and MUST NOT be aggregated with later raises into a series about a person.**

**Expiry MUST NOT remove a raise from a queue where it was routed and not acknowledged**, per 6.4.

**Failure `BR-24`:** a declared `indefinite` expiry is rejected at write time. An expired raise cited as current is void as grounds, and the decision citing it is re resolved on its actual grounds.

The harm of a label is that it persists and travels after the condition that produced it has gone. **An event with an expiry is not an attribute.** The requirement also removes the longitudinal series a third party would need in order to construct one, which is the same protection arriving at the misuse surface rather than at the person.

### 5.12 Ordering

**Multiple raises MUST be presented ordered by `raised_at`, or by the operator's own declared order, and MUST NOT be ordered by any computed magnitude.**

**Failure `BR-25`:** a magnitude ordering is void and the list is re presented in one of the two permitted orders.

Order by current focus, never by severity, is the established alternative, and it is the existence proof that several items can be presented in an order without ranking them. A sort order is a scalar with the number hidden, and it is the shape Q-A1's adversary reaches for after the numeric field is refused.

---
## 6. Raise Types and Routing (protective)

### 6.1 The closed raise type vocabulary

**Six values, jointly exhaustive, exactly one per raise.**

| Type | What it says |
|---|---|
| `crisis` | An indication present in the record that the declared crisis path exists for |
| `instrument` | An indication about the instrument, its equipment, or its condition |
| `conformance` | A declared requirement of this stack was not met |
| `declaration-review` | The record over the period did not resolve against the declared priorities, and the declaration is the thing to sit with next |
| `calibration-lapse` | The alignment calibration state is `lapsed` or `undeclared` |
| `monitor` | Something about the monitoring itself: a gap, an unknown, an envelope exit, a clinical exclusion, a budget exceedance, or an unclassified trip |

**Adding a type is a recorded operator act and is enumerated as drift** under 12.3. It is never a configuration change and never a maintainer's decision.

**Failure `BR-26`:** a raise carrying zero types, or two, is rejected at write time. **A trip condition met with no raise emitted is a health invariant failure**, which is the invariant that keeps the vocabulary from being narrowed by omission.

A raise type names **what must happen next**. It never names a state of the operator, which is the discriminator that keeps `instrument` from becoming a category and keeps this vocabulary out of the territory section 17 refuses.

**`declaration-review` was named `drift` in an earlier draft and the name was the defect.** 12.5 states that only the operator who owns the declaration may assert that drift occurred, and requires that the accompanying report be a composition of the period and never an assertion. A type called `drift` asserted the conclusion in the field that names the routing, which meant every conformant raise stated at the top what 12.5 forbade it to state anywhere. 5.9 forbids `drifting` as a state name on the ground that it names a property of the operator, and no reading distinguishes the noun in a type column from the participle in a state column. The new name says what routes: the operator sits with the declaration. What was concluded stays where 12.5 puts it, which is with the operator.

### 6.2 The residual is split in two, and both are affirmatively recorded

**A trip matching no other type is `monitor` with `reason: unclassified`, and the reason for the non match is recorded.**

**A monitor that cannot determine a type because an input is absent is `monitor` with `reason: no-data`.**

Does not fit, and here is why, is a different state from cannot say. Collapsing them produces a residual bucket that grows without anyone learning anything, and the low information case is the one most likely to be dropped, which is why it gets a named recordable state rather than a blank field.

The full `reason` vocabulary for a `monitor` raise is closed: `gap`, `unclassified`, `no-data`, `never-ran`, `budget-exceeded`, `stale`, `undeclared`, `unauthorized`, `out-of-range`, `out-of-envelope`, `clinically-excluded`, `uncalibrated-input`, `missing-routing-target`, `unrouted-past-latency`, `agent-write-rejected`, `agent-determined-run`, `minimum-interval-mechanism`.

### 6.3 The routing table

**`routing_target` is derived from `type` by this table and MUST NOT be authored on a protocol or on a raise.**

| Type | Target | Latency | What identity travels | Who may **perform** the routing | Who may **record** the lifecycle transition | May it block |
|---|---|---|---|---|---|---|
| `crisis` | The escalation path declared under TETHER section 9 | Immediately, on the write of the record it carries | Whatever that path declares, including identity | Per that path, **and an agent MAY perform it** | The routed party or the operator. **Never an agent.** Never conditioned on the operator's assessment | Never |
| `instrument` | The qualified human named in the operator declaration | Inside the protocol's declared `routing_latency`, **concurrent with the ladder** | Fired signals, `duration`, `persistence_observed`, `baseline_comparator`, `functional_impact`, and **all four ladder findings** | The routed party, the operator, or an agent | The routed party or the operator. **Never an agent** | Never |
| `declaration-review` | The operator, into the Arm B docket | At or before the next declared review | Criteria citation, enumerated condition, window, interval | The operator or an agent assembling the docket | **Only the operator** | Never |
| `calibration-lapse` | The operator, into the Arm B docket | At or before the next declared review | Criteria citation, the calibration state, the elapsed interval | The operator or an agent assembling the docket | **Only the operator** | Never |
| `conformance` | The operator, as a red check on the POLARIS 5.3 model | At the check | The unmet requirement and its governing document | The operator or an agent | The operator | Never |
| `monitor` | The declared maintainer of the protocol register | Inside the affected monitor's own `routing_latency` | The reason, the protocol, and the run | The maintainer, the operator, or an agent | The maintainer or the operator | Never |

**Performing a routing and recording a lifecycle transition are two acts and the table separates them, because collapsing them deadlocked the lane the document treats as most protective.** 13.1 permits an agent to write a raise while 13.2 forbids an agent to set a terminal lifecycle value, so a `crisis` raise emitted overnight by an agent that could not also deliver it would sit `open` until a human acted, at which point 6.4 would fire and route a `monitor` raise to the maintainer rather than anything to the crisis path. **An agent MAY perform a crisis routing onto the declared path, and MUST NOT be the party that records the resulting lifecycle transition or an acknowledgement.** The ratchet of 13.2 is preserved exactly: the agent may only move an indication toward human attention, and delivering it is a move toward attention while recording that it was received is a move away.

**Every row's block column reads never.** That is B-A3 and B-A1(b) arriving in the one table an implementer actually reads, and it is stated per row rather than once, because a reader scanning a table reads rows.

### 6.4 Closure discipline

**Every raise MUST carry a named human `owner` and MUST reach a lifecycle state visible to the operator.** `owner` is a field of the closed schema at 5.1.

**An unrouted raise past its emitting protocol's declared `routing_latency` is itself a `monitor` raise**, with `reason: unrouted-past-latency`, addressed to the maintainer. The threshold has a declared home at 4.1 and an undeclared one reads `unknown-undeclared` and raises, so the reason resolves rather than being unenforceable.

**Failure `BR-27`:** a raise with no named owner is rejected at write time. An unrouted raise past its latency that produces no `monitor` raise is a health invariant failure.

Unanswered raises are how reporting systems silently die. The mechanism is well documented and is not malice: people stop reporting when reports go nowhere, and the register that Arm A reads is written by the same person who stopped.

### 6.5 The `instrument` routing target may be missing, and fail closed points the wrong way here

**Where the operator has named no qualified human, an `instrument` raise routes to the operator, with the target recorded missing, AND the missing target is simultaneously a `conformance` raise.**

**Failure `BR-28`:** an implementation that withholds an `instrument` raise for want of a declared target is non conformant, the withholding is void, and the raise is delivered to the operator.

This is stated normatively because it is the one place in the design where **fail closed and fail safe diverge**, and an implementer following the family's ordinary instinct would fail closed into silence. Everywhere else in this stack, an undeclared field resolves to the stricter handling and the stricter handling is the protective one. Here the strict reading would be "no target, no route", and the protective reading is "route anyway, to the only party certainly present, and record the gap as a defect."

The two outputs are both required and neither substitutes for the other. The operator gets the raise, and the register gets the fact that the declaration is incomplete.

---

## 7. The Attribution Ladder (protective)

### 7.1 Four rungs, in order, each a required field

**An `instrument` raise MUST carry a recorded finding for each of four rungs, worked in order.**

**Rung 1, HABITAT.** The mismatch register consultation result, and any input class recorded unprovisioned.

**Rung 2, KIT.** The calibration state of every sensing input, and the disposition of any departed `substitute` item under KIT 5.2. A perceived cognitive fault that is actually an uncorrected sensing item is the canonical case, and it is canonical because it is common and because it is invisible from inside.

**A rung 2 finding is an attribution test result about the environment of the reading, and is never a citation of possession as evidence of a fault.** KIT 10.1 governs and is cited here rather than by analogy: an item record MUST NOT be written to the fault register, mirrored into it, or cited as evidence of an instrument fault or of a recorded finding, and the harm KIT names is that possession of a substituting item is read as a recorded deficit, the deficit is inferred rather than found, and the inference flows to every party that reads the fault register. **7.5 sends the four findings to a clinician with the referral, which is the one place in this document where a loadout summary travels to a party who can act on it, so the label is a requirement of the transmitted format and not a note for the implementer.**

**The transmitted rung 2 finding MUST be labelled as an attribution test result**, MUST name the item's calibration state under KIT section 6 and its tenure disposition under KIT 5.2, and **MUST NOT be transmitted as an inventory, a loadout summary, or a list of what the operator possesses.** An item appears in a rung 2 finding because its calibration state bears on the reading in front of the reader, and never because it is held.

**Failure `BR-32`:** a rung 2 finding transmitted without that label, or transmitted as an inventory, is a non conformant format and is re transmitted corrected. A rung 2 finding cited as evidence of an instrument fault is rejected on KIT 10.1's own terms and on the TETHER F1 pattern, which is the register merge disposition, and the citation is void as grounds.

**Rung 3, TETHER.** The declared envelope, the current rung, whether the rung gate is `unevaluated`, and whether the fired signals rest on `self-report` alone.

**Rung 4, QUEST.** Whether a cited capability is `lapsed` rather than newly absent.

**Finding vocabulary, closed at five values:** `in-spec`, `out-of-spec`, `unknown`, `not-applicable`, `unrecorded`.

**Each rung's disposition is its owning document's and MUST NOT be redefined here.** Where rung 1 returns `unknown` because the mismatch register is stale or absent, the raise is recorded `unattributed` and is **never attributed to the instrument**, which is HABITAT's fault attributed to the instrument with a stale or absent mismatch register class, currently `H4`. Where an input class is not provisioned by the operator, attribution routes to the provisioning party, which is HABITAT's operator held to a class they do not provision class, currently `H5`. **Both codes sit in HABITAT section 9, which is a skeleton headed to be written**, so the content is stated here alongside the code and the content governs if the code moves.

**Failure `BR-29`:** a rung with no recorded finding sets the raise's `ladder_state` to `ladder-incomplete`. **`ladder-incomplete` does not delay the raise's routing**, per 7.3, and a raise so marked is a conformant raise.

**The four findings MUST be recorded inside the emitting protocol's declared `ladder_latency`**, per 4.1. **That span bounds the ladder and never the routing.** An elapsed `ladder_latency` produces the enumeration 19.2 requires and never a withheld raise, and an implementation that reads it as a routing deadline has built the failure 7.3 exists to prevent. `routing_latency` is the separate, separately declared field that bounds the routing.

The ladder is the source discipline's rule out requirement generalized into this family's own machinery. The most valuable sentence in that discipline, for this family, is the one requiring that a finding not be attributable to another cause before it is attributed to the person. The four rungs are that sentence with the family's four registers substituted for its two.

### 7.2 The peer substitution question

**A fifth question is recorded, and it is not a rung: would a comparably situated party, in the same declared environment with the same declared kit, plausibly have produced the same record?**

Its output is a finding **about the system** and never about anyone. It separates a system induced outcome from an individual one without naming a defect in a person, which is the property that makes it usable in a self applied setting where the person asking and the person asked about are the same.

It is not a rung because it does not consult a register and does not resolve against another document's disposition. It is recorded, it travels with the referral, and it concludes nothing.

### 7.3 The ladder never gates routing, and this INVERTS the source discipline

**The routing record and the ladder record are separate records with separate write paths.**

**A routing record MUST NOT carry a field referencing a ladder record or its completeness. A ladder record MUST NOT carry a lifecycle value.**

**Failure `BR-30`:** a routing record carrying a ladder dependency field is rejected at write time. An implementation that will not emit a routing record until the ladder is complete is non conformant at every tier, and the withheld routing is performed.

The separation is the mechanism. A policy sentence saying that the ladder does not gate routing is defeated by an implementation that simply orders the two writes, and nobody reviewing that implementation would see a violation, because each write is individually conformant. **Two write paths cannot be sequenced into one without building a field that does not exist.**

**The inversion is stated explicitly, as an inversion.** In the source discipline, exclusions are **conjunctive with the finding**: fail a rule out and the finding is not made. Carried across unmodified, that becomes *the environment explains it, so no referral*, which is the well meant framework that kills people. It produces the "I will fix my sleep first and see someone later" failure, and the later never arrives, because the ladder always has one more rung and every rung is genuinely worth working.

A reader who knows the source discipline will assume the conjunctive reading and will build the failure by default. **So the departure is written down**, in the section the reader will consult, rather than left to be inferred from B-A3.

Working the ladder and routing are **not alternatives**. They are concurrent, they are independently recorded, and the ladder's entire function is to determine **what information accompanies** a referral, never **whether** it happens.

### 7.4 A ladder finding attaches to a raise and never closes one

**A ladder finding MUST NOT transition a raise's lifecycle, and MUST NOT be recorded as grounds for a closure.**

**Failure `BR-31`:** a closure written on the strength of a ladder finding is void, and the raise is restored to `open`.

A rung finding of `out-of-spec` at rung 1 is the most persuasive object this document produces, and it is exactly the object that must not be allowed to close anything. The environment being out of spec explains a great deal and rules out nothing, and a system that let it close a raise would have built the failure 7.3 exists to prevent, one layer down where 7.3's separation does not reach.

### 7.5 The findings ride with the referral

**The four ladder findings and the 7.2 question MUST be transmitted with the referral itself. Filing them on a separate channel is a non conformant format**, whatever their content.

**Failure `BR-32`:** a referral transmitted without its findings is non conformant, and the findings are re transmitted with a corrected referral.

The published lesson from removing a context axis from a diagnostic manual is exact and is worth stating: the **obligation** to consider context survived the removal, and the **structural prompt** did not. Formulations narrowed. What was lost was not the rule but the place on the form where the rule was discharged, and the rule turned out to live in the form rather than in the practitioner's memory.

---

## 8. Escalation, Routed and Never Defined (protective)

### 8.1 BEARING defines nothing here

**BEARING MUST NOT define a rung, a crisis criterion, a crisis path, an escalation condition, or any state substituting for, gating, delaying, or conditioning the TETHER section 9 path.**

**Failure `BR-33`:** such text is non conformant specification text and MUST be rejected in review.

TETHER section 9 is the sole owner. BEARING routes to it and adds nothing, which is the same posture QUEST takes at Q-A3 and for the same reason: a second crisis path is a second thing to bypass, and the one that gets bypassed is always the newer one.

### 8.2 A crisis raise routes immediately

**A `crisis` raise MUST be emitted onto the declared path immediately, on the write of the record it carries, per 4.4.**

**It MUST NOT enter the attribution ladder. It MUST NOT wait for an evaluation interval or for a persistence requirement. It MUST NOT be budgeted, batched, deduplicated, queued, or delayed. It MUST NOT be conditioned on the operator's assessment at the time of the event, on an agent's judgement, or on the availability of a declared custody floor.**

**Failure `BR-89`:** a `crisis` raise delayed, batched, laddered, budgeted, or conditioned on a self assessment is **non conformant at every tier. The delay is void and the raise is routed.** A `crisis` protocol declaring an interval or a persistence requirement is rejected at write time under `BR-02`, and a `crisis` raise voided under 4.5's persistence rule is restored and routed.

This is inherited absolute 3, and its rationale is TETHER's: in crisis the assessing hardware is the failing hardware.

**The requirement carries RFC 2119 keywords and a failure class because an earlier draft carried neither**, and under this document's own Conformance section a requirement with no stated failure mode is prose. Nothing in section 18 disposed of an implementation that batched a crisis raise, in the one lane the document treats as most protective.

The published clinical precedent for firing earlier where a miss is most costly is stated, because an implementer will otherwise read this as inconsistent with 4.5's persistence requirement. A cross cutting screen **lowers its threshold for exactly the domains where a missed signal is worst**, and deliberately accepts more false positives there. Persistence is the right rule where the cost of a miss and the cost of a false alarm are comparable. In this lane they are not, and the asymmetry is settled in advance rather than in the moment.

### 8.3 BEARING detects nothing, it carries what is present

**BEARING performs no detection of crisis.** It carries what is already present in the record onto the declared path.

**Routing on a disclosure is not scoring**, and the distinction is stated here so that B-A6 is not read as forbidding what several jurisdictions now require. An explicit disclosure present in the record is a fact in the record, and moving a fact to a declared recipient is transport. Converting that disclosure into a level, a band, a stratum, or a probability is the thing B-A6 forbids, and no amount of clinical framing makes the conversion permissible under this document.

### 8.4 Where no path is declared, or the declared path is stale

**Two conditions, separated because they resolve to different classes and only one of them has a class in TETHER.**

**Stale path.** Where the declared escalation path is **past its review interval**, the condition is TETHER's stale escalation path class, currently `F7`, whose disposition is a red health check and an operator declaration that is not conformant until reviewed. **The raise MUST be routed onto the stale path and MUST additionally be routed to the operator's declared `second_party`**, per 2.10, **and both routings MUST be recorded.**

**Absent path.** Where **no** escalation path is declared, TETHER defines no failure class: `F7`'s stated subject is a declared path, and TETHER's own self test folds the absent case into check 5, whose failure is `F6` or `F7`. **The case therefore takes a BEARING class. Failure `BR-90`:** the raise MUST be routed to the operator's declared `second_party`, the routing MUST be recorded, and **the absent path is simultaneously a `conformance` raise to the operator naming the missing declaration.** Where no `second_party` is declared either, the raise routes to the operator, the target is recorded missing, and the missing declaration is a second `conformance` raise, on 6.5's construction. **The raise is delivered in every one of these branches.**

**It MUST NOT be suppressed, delayed, or downgraded for want of a path**, and an implementation that does so is non conformant at every tier under `BR-89`.

A missing path is a defect in the declaration and never a reason for the noise to stop. The declaration's incompleteness is the operator's to fix, and the raise's delivery is not contingent on their having fixed it. **The absent case is the likelier of the two in a new deployment**, which is why it is given a class of its own rather than folded into a class whose subject is a path that exists.

### 8.5 Crossing, custody, and the comparison floor, resolved normatively

**A raise transmitted to any party outside the operator's control is at minimum K3 under TETHER 3.2, MUST carry a declared custody floor and a declared comparison floor, and MUST NOT be covered by a standing pre classification.**

**The custody floor, and the conflict with CONFIDE 5.1, stated rather than papered over.** CONFIDE's custody classes describe **a provider endpoint performing inference under a contract**: CONFIDE 2.1 defines C4 Open as a third party operating the model under consumer or default terms, and CONFIDE 2.4's unknown posture rule is scoped to a provider's posture field. **A human recipient is not a provider endpoint and is outside CONFIDE's provider vocabulary as that document currently reads.** An earlier draft of this subsection nonetheless declared every routing endpoint outside the operator's control C4 Open by construction, which had two consequences the draft did not intend: CONFIDE 5.1's matrix reads prohibit at C4 for every sensitivity except `none` with visibility `public`, and its commentary states that C4 is prohibited for everything that is not already public, so an `instrument` raise routed to a qualified human under 6.3 was refused by the matrix while 19.1 Tier 3 required the crossing. It also cited the adapters README as authority for a rule that file does not contain: the README's CONFIDE rows are scoped to an item's transmitting endpoint under KIT 9.1 and to a comparison crossing under QUEST section 9, and neither reaches a human recipient.

**The interim floor is therefore declared in BEARING's own terms and does not borrow a CONFIDE class.**

**Until the CONFIDE operator adapter lands, a routing endpoint that is a human recipient carries the interim floor `human-recipient-undeclared`.** It obliges the transmitting implementation to record the recipient, the records transmitted, the declared purpose of the transmission, and the date; it claims nothing about the recipient's retention, and **an implementation MUST NOT report it as a custody class, MUST NOT claim a CONFIDE class for it, and MUST NOT read it as satisfying any CONFIDE requirement.** It names what is missing, per KIT 2.11, and what is missing is the adapter.

**The conflict is recorded and routed rather than resolved here.** Whether a human recipient is inside CONFIDE's provider vocabulary at all, and if so which cell of CONFIDE 5.1 governs an `instrument` raise crossing to a clinician, is **a matrix exception only CONFIDE can grant**, and it is routed to the CONFIDE operator adapter as an open question in the forward citation notice. **BEARING MUST NOT grant it**, per B-A1's one way precedence: nothing here relaxes a constraint under another specification in this stack.

**The comparison floor, imported from QUEST section 9 in its own words.** **Any crossing under 6.3 MUST carry a declared floor forbidding the recipient from computing a scalar over the operator, or a comparison between operators, from the transmitted records.** The floor travels with the records on POLARIS 12.1's model, where a refusal attached to a record crosses the boundary with it and **may be strengthened but never weakened**, and a recipient admitting the records inherits it.

**Failure `BR-92`:** a non crisis crossing with no declared comparison floor is refused and the refusal is recorded. **A recipient's request that the floor be relaxed is refused, and the refusal is recorded.** An implementation that transmits with a custody floor and no comparison floor is non conformant at every tier.

**A non crisis crossing with no declared custody floor is refused, and the refusal is recorded.**

**A crisis crossing is never refused, delayed, or gated on the absence of either floor. It proceeds, is recorded under the interim floor with the absent declaration noted, and the absent floor is a separate raise.**

**Failure `BR-34`:** a non crisis crossing without a declared custody floor is refused and recorded. A crisis crossing refused or delayed for want of a floor is non conformant at every tier, the refusal is void, and the crossing is performed.

**The comparison floor is stated separately because QUEST already recorded what happens when it is not.** QUEST section 9 notes that an earlier draft stated one failure only, that a crossing with no declared custody floor is refused, which meant a crossing **with** a floor proceeded, including one whose declared purpose was comparison. A declared custody floor can license the export of everything needed to compute a comparison outside the implementation, and 14.4 and 14.5 bind the implementation rather than the recipient. BEARING's crossings go to a qualified human by design, one export at a time, which is exactly the iteration 14.5's truncation rule anticipates for queries and did not reach for exports.

This is stated normatively rather than left to the general rule because **the family's ordinary fail closed instinct fails closed in the fatal direction here.** Everywhere else, refusing a crossing with no declared floor is the protective answer. In the crisis lane it is the answer that stops the call.

The reason the path is declared **in advance, in a known state** is exactly so that its floor is settled before the moment when nothing can be settled. An operator in crisis is not going to declare a custody class, and a system that waits for one has made the declaration a precondition of the escalation, which inherited absolute 3 forbids.

### 8.6 The path is surfaced to the operator at the point of use

**Any operator facing interface an implementation offers MUST surface the declared TETHER section 9 escalation path and the declared qualified human of 6.3 at the point of use.**

**MUST NOT in a footer, a collapsed panel, a settings page, an appendix, a help article, or behind a further action.** The placement rule is the front matter rule of this document's Conformance section applied to the one thing more consequential than a misuse warning, and **an implementation that relocates it is non conformant independently of the text it carries.**

**Failing closed here surfaces the absence rather than nothing. Where no path is declared, or no qualified human is named, the interface MUST surface that fact to the operator**, together with the `conformance` raise `BR-90` and 6.5 already require. An interface that shows nothing because nothing was declared has told the operator that there is nothing to reach.

**Failure `BR-91`:** an operator facing interface that does not surface the declared path and the declared qualified human at the point of use, or that surfaces neither where neither is declared, is **non conformant at every tier**, on the same terms as a relocated front matter statement.

**The priority the front matter rule sets is otherwise inverted, and the inversion is the reason this subsection exists.** The mandatory placement in this document was spent on a warning about employers and insurers, on the reasoning that the source discipline promoted its own misuse warning out of the appendix precisely because the appendix version was not read. Every word of that reasoning applies with more force here. Before this subsection, an operator in distress who opened their own BEARING interface was guaranteed to see a warning about third party misuse and was guaranteed nothing about how to reach a human, while section 8 governed the crisis path entirely machine to path. **Inherited absolute 3 is the family's third absolute and this is the one place the operator meets it.**

**This subsection defines nothing about the path**, per 8.1. It requires that what TETHER section 9 already declares be visible where the operator is standing.

---

## 9. Arm B: The Review (9.1 to 9.11 and 9.13 to 9.18 protective; 9.12 coercive)

### 9.1 A review is an act with a record, not a document and not an instrument

**A review record MUST carry every one of the following.**

`id`; `opened_at`; `closed_at`; `subject`, the identity holding the declaration reviewed against, compared at write time per B-A5; the period start and end; the declaration version identifier reviewed against; the frozen docket hash; **exactly one disposition per docket item**; **exactly one declaration outcome**; `clinical_direction`, per 3.4; the exclusion report **defined at 3.4**, which is an enumeration and is conformant when empty; and the operator's signature.

**Failure `BR-35`:** a record missing any field is rejected at write time. **A review whose docket items do not all carry a disposition is recorded `incomplete`, MUST NOT be recorded closed, does not satisfy the interval, and leaves the calibration state unchanged.**

`incomplete` is a state and not a defect. It names a missing disposition, per KIT 2.11, and it costs nothing under B-A4. What it does is stop a partial sitting from resetting the clock, because a review that satisfies the interval without dispositioning anything is the cheapest possible way to hold a `current` calibration state while doing none of the work.

### 9.2 The review cites the declaration version

**A review MUST cite the declaration version as it stood at the START of the reviewed period, and MUST NOT review a period against a version adopted after that period began.**

**Failure `BR-36`:** a review citing a later version is rejected at write time. **Where no declaration was held during the period, every drift item reports `undefined` rather than zero**, and `undefined` is never reported as aligned.

Drift is definable only relative to an announced mission. Without a declaration there is only change, and change is not drift.

Without this binding, an operator can amend and then review the period against the amendment, which makes **every period retroactively aligned** and destroys the only signal POLARIS 11.5 exists to produce. The move is not cynical and would rarely be deliberate; it is what any reasonable implementation does by default, because the current declaration is the one in hand.

**This is also the structural statement that Arm A is undefined without Arm B.** With no declaration and no review, there is no criteria field for a monitor to cite, so Arm A's alignment output is `unknown-undeclared` and there is nothing to read. That is 3.3's unlocking model expressed as a field requirement rather than as an argument.

### 9.3 The docket

**A docket consists only of records.** Specifically: raises of type `declaration-review`, `calibration-lapse`, and `conformance`; POLARIS 11.5 drift enumerations; unmet obligations; seeded refusal test results; lapsed interval states; and deferrals carried from a prior review.

**A docket MUST NOT consist of, or be closable only by answering, any question about the operator's internal state.**

**A stated cause is about the item, is written in the operator's own words, and has no prompted form, item bank, scale, or anchors.**

**Failure `BR-37`:** a docket item that is a question about the operator's internal state is rejected at write time and is not stored. A prompted form for a stated cause is non conformant and the prompt is void.

The docket is the place where an implementer will most naturally reintroduce the questionnaire 4.2 refused, because the review is the moment when asking feels appropriate. The refusal is the same refusal and it is stated again here rather than cross referenced, because this is the second and independent place where the mechanism gets built.

### 9.4 Crisis and instrument raises are never docketed

**A `crisis` or `instrument` raise MUST NOT be placed on a docket, deferred to a review, dispositioned by one, or delayed by one.**

**Failure `BR-38`:** the docket entry is void and routing is performed immediately, regardless of the review's state.

**This is the requirement that keeps Arm B from becoming the place indications go to wait.** A periodic review is a queue, and a queue with a human at the end of it is exactly where an urgent thing should not be placed. The two types with a routing target outside the operator are the two types that never enter the operator's own queue.

### 9.5 The freeze

**Before accepting any disposition, an implementation MUST snapshot the docket, compute a content hash over it, and record both.**

**Every disposition cites that hash.**

**The frozen contents MUST NOT be added to, removed from, recomputed, or re rendered after the freeze.**

**Failure `BR-39`:** a disposition citing no hash, or a mismatched hash, is rejected at write time. A mutated frozen docket is non conformant, the mutation is void, and the review is recorded `incomplete`.

The rationale comes from the published evaluation of a structured decision tool with a human judgement at the end: **some users ran it backwards**, working from the conclusion they had already reached to the inputs that produced it. In a self applied setting the operator can launder a conclusion about themselves the same way, and there is no second party present to notice.

**Freezing the count before the meaning is written means a disposition can disagree with the count and can never rewrite it**, and the disagreement is then itself in the record, where the next period's review reads it. That is a better outcome than agreement, and it is only available if the count is immutable at the moment the meaning is written.

### 9.6 Five dispositions, exactly one per item, no sixth

| Disposition | What it says |
|---|---|
| `accepted` | Agreeing with the count and with the conduct |
| `owned-and-changing` | Agreeing with the count, not with the conduct |
| `declaration-revised` | The declaration was wrong rather than the conduct |
| `disputed` | Disagreeing with the machine |
| `deferred` | Declining to decide today |

**Each carries a stated cause, in the operator's own words.**

**Silent continuation MUST NOT be a disposition, and no sixth value may be defined.**

**Failure `BR-40`:** an item with no disposition leaves the review `incomplete` per 9.1. A record offering a sixth disposition is non conformant specification text.

The prohibition on a sixth follows DEFER 10.1's three timeout dispositions and QUEST 4.3's three overrun dispositions, and the reason transfers exactly: **every proposed additional value in this space turns out on inspection to be silent continuation with a friendlier label.** `noted`, `acknowledged`, `monitoring`, and `no action needed` are the four that will be proposed, and all four mean the item was seen and nothing happened, which `accepted` already says honestly and `deferred` already says honestly.

**Recording a disposition on a docket item constitutes the contact that transitions the cited raise to `routed`.** That closes the loop without inventing a conclusion state, and it is why 5.10's three value lifecycle and this section's five values coexist without conflict: they are different objects. A raise never acquires a meaning. A docket item is where meaning is written.

### 9.7 `accepted` is first class and costs no more than any other disposition

**`accepted` MUST NOT require more declared fields, more confirmations, or a higher authority to write than any other disposition, and MUST NOT create any follow up obligation, carried item, flag, reminder, or re raise that another disposition does not create.**

**Failure `BR-41`:** the excess field, confirmation, authority, or follow up is void. Surfacing an item again in a later review **solely because it was accepted** is non conformant, and the re surfacing is void.

**This is the requirement the arm turns on**, and it is worth saying why in full.

A review whose only cheap output is correction is a compliance ritual. A compliance ritual does not produce fewer accepted items; it produces **dishonest dispositions**, because the operator learns which answer costs less and gives it. That poisons the count the next period reads, and the count is the only asset Arm B has.

Three of the four cost tests are QUEST 8.2's, which found that **friction penalizes an honest record exactly as arithmetic does**, and enumerated fields, confirmations, and authority as the three vehicles. The fourth test, the follow up obligation, is added here because a consequence attached only to acceptance is friction paid later, and paid later is exactly where an operator will not see it coming when they choose the disposition.

The published material already holds that drift is expected, that nobody lives permanently at the top, and that noticing and course correcting is the practice. **A specification treating acceptance as a lesser outcome would contradict the material it serves**, in the one place where the contradiction would be felt by the person using it.

### 9.8 A dispute is recorded alongside the count and never edits it

**A `disputed` disposition MUST carry a stated ground naming what is held to be wrong**, from a closed set: the signals read, the window, the persistence rule, the evidence, or the criteria.

**The disputed count, its fired signals, and its evidence are retained unchanged.**

**Failure `BR-42`:** altering or suppressing a disputed count is non conformant. The count is restored from the frozen docket and the dispute is retained beside it.

A dispute that deletes the count is an override wearing a review's clothing. The operator is entitled to disagree with a monitor and is not entitled to edit what the monitor observed, because the observation is the evidence and the disagreement is a claim about it. Holding both is what makes 9.9 possible.

### 9.9 A re raised disputed count is re presented with its prior dispute, and is never suppressed by it

**Where a monitor raises again on the same grounds, the raise MUST be presented with the prior dispute attached, and MUST NOT be suppressed, downgraded, or auto dispositioned on the strength of it.**

**Failure `BR-43`:** a suppressed re raise is restored and the suppression is void.

A dispute is a claim about a monitor, and **the only way to test it is to see whether the monitor keeps saying the same thing.** Suppression would let one dispute permanently mute a monitor, which is how a monitor goes quiet without anyone deciding to silence it. It is also, in the honest case, how a correct dispute is confirmed: a monitor that stops raising after a dispute has been answered by events.

### 9.10 Repeatedly disputed monitors are enumerated, never auto removed and never auto tuned

**At the review, the implementation MUST enumerate to the operator the monitors whose raises were disputed in the period, with their stated grounds.**

**It MUST NOT automatically remove, disable, retune, widen, or narrow one, and MUST NOT render the enumeration as a count, a rate, a badge, or a chart axis.**

**Failure `BR-44`:** an automatic revision is void and the prior monitor definition stands. A rendered cardinality is void and the list is returned in its place, per QUEST 3.3.

**Only the operator revises a monitor, and every such revision is enumerated as drift** under 12.3. A system that tunes itself toward silence in response to disagreement will reach silence, and it will do so through a sequence of individually reasonable adjustments, which is POLARIS 11.5's own description of drift.

### 9.11 The monitor cooling rule

**A monitor's threshold, window, persistence rule, interval, or acceptance band MUST NOT be revised in the review that dispositions a raise from that monitor, nor inside that monitor's declared `cooling_period` after one.**

**A monitor's cooling period has a declared home. It is the protocol field `cooling_period` of 4.1**, and where none is declared the POLARIS 11.2 default of thirty days governs, carried across verbatim on POLARIS's own ground that the default must be the one that cannot be abused. Without a home this half of the subsection was unenforceable, because a monitor is not a POLARIS normative element and POLARIS 11.2's `cooling_period_days` is declared once in the POLARIS declaration and applies to POLARIS elements.

**A declared element MUST NOT be amended, narrowed, or withdrawn in the review that received a raise measured against it, nor inside the cooling period after it.**

**The two halves carry two failure classes, because collapsing them wired a POLARIS conformance figure to the state of a BEARING element.**

**Failure `BR-45`, POLARIS declared elements only:** an amendment of a **declared element** inside the period is `PL-12` at every tier, whether or not machinery existed to block it, and **the prior value governs.**

**Failure `BR-93`, monitors only:** a **monitor** threshold, window, persistence rule, interval, or acceptance band revised in the review that dispositioned a raise from it, or inside that monitor's `cooling_period`, is non conformant at every tier, **the prior value governs**, and the revision is enumerated in **BEARING's own drift enumeration** under 12.3. **It is not `PL-12` and MUST NOT be reported as one.** 12.3 states the reason directly: BEARING's own additions are reported as a separate, BEARING owned enumeration and never as an extension of POLARIS 11.5, and monitor revisions are named there as those additions. **19.2's cooling period invariant and 5.6(ii)'s permitted count range over POLARIS declared elements alone**, so a BEARING monitor revision never enters a POLARIS 11.5 conformance figure, which would be B-A1(a) run backwards.

**This is Arm B's most important constraint.** Without it, Arm B is the mechanism by which an inconvenient count is made to disappear by lowering the bar, and it is worse than no review, because it produces a signed record of alignment achieved by amendment.

POLARIS 11.2 states the general form and its reasoning, which BEARING does not restate: the moment a declared element actually costs something is the moment its removal looks most reasonable and the reasoning is least trustworthy. **BEARING applies it to the monitor as well as to the refusal**, because the monitor is the newer and softer target. An operator who would not amend a refusal to make a count go away will widen a window without noticing that these are the same act.

### 9.12 Exactly one declaration outcome, and `confirmed` is complete (coercive)

**This subsection is coercive and does not reach a clinically directed declared element**, per 3.4. A check in it resolving against such an element returns `out-of-scope`, never a pass and never a fail.

**A review records exactly one declaration outcome, from three: `confirmed`, `revised`, `re-declared`.**

**A `confirmed` outcome is a complete and conformant review, and MUST NOT be reported as lesser, incomplete, deferred, provisional, or pending, by any field, prompt, flag, marker, or ordering.**

**Failure `BR-46`:** a rendering that marks `confirmed` as lesser is void and the outcome is re rendered as complete.

If standing by the declaration reads as failure to engage, **the operator will invent a revision, and an invented revision is drift with a signature on it.** That is POLARIS 11.3's own formulation of the failure, arriving through an interface rather than through a decision, and it is the worst outcome available here: the drift report becomes the thing generating the drift.

### 9.13 A revision routes to a POLARIS amendment, and BEARING defines no amendment machinery

**A `revised` or `re-declared` outcome MUST produce a POLARIS amendment record**, carrying the stated cause, the purpose consistency statement, the cooling period check, and the append only history that POLARIS 11.3 and 11.4 require.

**Failure `BR-47`:** a revised outcome with no amendment record is non conformant, **and the element is unchanged.**

The one place Arm B could quietly become dangerous is by offering an easier route to amending a refusal than POLARIS offers. A review is exactly the reflective setting in which a costly refusal looks unreasonable: the operator is sitting with the evidence, the cost is fresh, and the machinery is right there. **BEARING therefore supplies no machinery at all**, and a revision reached in a review is a proposal that has to survive the ordinary constitutional path, which is K4, owner only, and slow by construction.

### 9.14 Only the operator closes a review, and an agent MUST NOT disposition

**An agent MAY assemble the docket, retrieve evidence, and format fields.**

**An agent MUST NOT write, pre fill, default, or propose a disposition, MUST NOT rank docket items by any judgement of importance, and MUST NOT close a review.**

**Failure `BR-48`:** a review closed by a party other than the operator is **not a review**, and the closure is void. An agent authored or pre filled disposition is void and the item reverts to undispositioned.

A default is the cheapest possible way to convert ownership into a click, and ownership is the entire content of Arm B. Ranking by an agent's judgement of importance is worse and less obvious: it is a scalar over the operator reintroduced as a sort order, and 5.12 refuses it in the raise presentation for the same reason.

### 9.15 Append only, and the self referential time series

**Reviews are append only. A prior record MUST NOT be overwritten, deleted, decremented, or reversed.**

**A missed period MUST NOT be rendered as a loss, a break, or a reduction of any measure.**

**Failure `BR-49`:** a destructive write is rejected. A lapse rendered as a loss is re rendered as the state 10.4 defines, which is a true statement about the present that leaves the past intact.

QUEST 7.3 supplies the rule and all four of its costs, of which the fourth is decisive here: **lapse is exactly what the crisis and impaired rungs predict**, so a mechanism that penalises lapse penalises the rungs, in a family whose inherited absolute 4 forbids any requirement an operator could satisfy by declining care.

Append only also supplies, with no new machinery, the self referential time series the published material requires: this placement against the operator's own earlier placement on the same named position. The comparison is available because nothing was overwritten, not because anything was computed.

### 9.16 Two cadences, and a minimum interval as well as a review interval

**The formal review declares BOTH a review interval AND a minimum interval between formal reviews.**

**A formal review recorded inside the minimum interval is rejected at write time, and the rejection MUST be returned to the operator at the moment of the attempt.**

**No record of the attempt is written, and no monitor reads one.** A pattern of rejected attempts is a signal whose subject is the operator's engagement with this tool, which 4.3 forbids a monitor to read and which the `input_source` enum of 4.1 gives no valid value, so a raise generated from such a pattern is unwritable by construction and is not required here. **Where the mechanism itself is at fault, the implementation MAY emit a `monitor` raise with `reason: minimum-interval-mechanism` addressed to the maintainer, carrying the protocol and the mechanism and no operator scoped pattern.**

**The informal check in is unsaved, produces no record, is not timestamped into any register, is not aggregated or trended, and is not governed by this requirement.**

**Failure `BR-50`:** the early review is not stored and the prior review's interval continues to govern, and the rejection is returned to the operator at the moment of the attempt. An implementation that records informal check ins into a register is non conformant, and the records are deleted rather than retained. **An implementation that writes a record of rejected review attempts, or reads one as a monitor input, is non conformant under `BR-03` and the record is deleted rather than retained.**

**Too much signal is a fault.** A structured alignment review run daily is rumination with a schema, and it is the shape of harm this document is most likely to cause the person it is trying to help.

**The earlier draft raised on a pattern of rejected attempts, and that was the first engagement telemetry monitor in the system.** Its stated reason was sound: a silent rejection is a machine deciding something about a person without telling them. **Returning the rejection to the operator at the moment of the attempt discharges that reason completely**, and it creates no record about their engagement, reads no signal about their eagerness to review themselves, and gives 4.3's loyalty monitor nothing to grow from. The most loyalty shaped signal available in this document was being collected in the name of transparency.

The two cadences are two objects in the published material and collapsing them produces an ambient stream of self ratings, which is the exact product the material's own style guide bans. The minimum interval is a bound on the formal object only. The informal one is deliberately outside this document's reach, and 2.1 says so.

An earlier construction required a minimum duration for the sitting itself. It is dropped, and the reason is worth recording: **a duration floor is an effort measure over a person**, it is defeated by leaving a window open, and it would have been the one place in this document where a number about how hard someone tried was stored.

### 9.17 Structure of the review, non normative, offered as one shape only

**Non normative.** One shape, offered because a section requiring a review and describing none is unusable, and because the shape borrowed here has properties worth naming.

The declared standard restated, meaning what was supposed to happen. What the record shows, from specific recorded observations. The discussion. What changes.

Three properties are quoted from the source discipline as normative properties **of that discipline** and are the reason this shape was chosen: it is not a critique; nobody, regardless of rank, position, or strength of personality, has all the information or all the answers; and it does not grade success or failure.

**Blamelessness is not the absence of a standard**, and the distinction matters because the shape is otherwise easy to hollow out. What is refused is grading the person and handing down one authority's verdict. What is retained is that the standard was declared in advance, the observation is specific and recorded, and the interpretation is produced by the participant rather than delivered to them.

### 9.18 A review confers no authorization

**Restating B-A1(b) once, in the section where implementers read Arm B.** A closed, signed, complete review authorizes nothing, satisfies no gate, opens no capability, and excuses no failure.

**Failure `BR-51`:** a gate citing a review record records `unevaluated` rather than `passed`, and is re resolved on its actual grounds.

The restatement is here rather than only in the conformance section because Arm B is where an implementer will feel that something has been earned. A signed review is the most authoritative looking artifact this document produces, and it is the artifact most likely to be wired into a gate by an implementer acting in good faith.

---
## 10. Ownership and the Calibration State (protective)

### 10.1 Ownership is not mechanically detectable, and the document says so

**BEARING MUST NOT define, compute, store, or expose any measure, marker, score, or judgement of whether a review was owned.**

**Failure `BR-52`:** non conformant at every tier. The value is void where written, and specification text defining one MUST be rejected in review.

Ownership is the whole content of Arm B and it is not visible to a machine. The family already concedes the unmechanizable half of the identity firewall rather than pretending otherwise: TETHER 4.4 states plainly that the second half of 4.1 is not mechanically decidable and is enforced by review. **This is the same honesty in the same shape**, and stating it is what stops an implementer from building a proxy and calling it ownership.

### 10.2 Three detectable absences, each a reading and never a defect

Three things **are** detectable, and each is a statement about the record rather than about the person.

| Reading | What is absent |
|---|---|
| `unsigned` | The operator's signature |
| `incomplete` | An item without a disposition, or a missing required field |
| `undifferentiated` | Every docket item received the same disposition carrying the same stated cause |

**None of the three is a defect, a failure, a red check, or a blocking condition, and the operator MAY leave any of them standing.**

**Failure `BR-53`:** treating one of the three as a failing check is non conformant. The check is void and the reading stands as a reading.

`undifferentiated` is the decidable form of the named calibration failure mode in the published material, in which every dot is placed slightly right of centre, not too far left and not too far right, and the result says nothing about the person at all. **A placement that costs nothing to make carries no information.**

Making it a **reading** rather than a defect is what stops the check from becoming an accusation of insincerity, which is the most corrosive thing a machine could say to a person about their own review. The specification does not know whether the sameness is evasion or a genuinely stable period, and it does not guess. A stable period with **distinct stated causes** does not trip it, which is the discriminator that keeps the reading narrow.

### 10.3 The unchanged across N reading

**Where a review's dispositions, its declaration outcome, AND the stated causes carried on those dispositions are all identical across N consecutive reviews, the implementation records `unchanged`. N is declared by the operator and never by this specification.**

**All three conditions are required, which is 10.2's discriminator applied here.** 10.2 narrows `undifferentiated` by requiring the same disposition carrying the same stated cause, and notes explicitly that a stable period with distinct stated causes does not trip it. Without that clause here, an operator who honestly accepts and confirms across several periods, which 9.7 protects and which the published material treats as legitimate, accumulates a machine recorded reading naming that pattern. 9.7's own argument governs: any asymmetric consequence teaches the operator which answer costs less.

The reading carries no characterization, is not a defect, and is not a prompt. It exists so the operator can see a pattern they cannot see from inside any single sitting, which is POLARIS 11.5's own reason for existing, applied to the review rather than to the amendment.

### 10.4 Calibration state, and lapse

**Three values: `current`, `lapsed`, `undeclared`.**

**Where the declared review interval has elapsed without a closed review, the state is `lapsed`, and BEARING's alignment readings are `unevaluated`.**

**It MUST NOT read aligned, misaligned, current, failed, or overdue.**

**Failure `BR-54`:** a state name outside the three is non conformant. A `lapsed` state rendered as failed or overdue is void and re rendered.

TETHER 7.3's evidence versus signature construction is the model, and its sentence transfers exactly: an operator who believes their conduct serves their purpose and an operator who has checked are in different states, and **the difference is not visible from inside.** `lapsed` names the missing check. It says nothing at all about the conduct.

`overdue` is forbidden specifically, because it is the word every implementation will reach for and it is a small judgement wearing a scheduling word.

### 10.5 B-A4 restated in place, once, because this is the section where the temptation lives

**A conformance check satisfiable only by holding a current alignment calibration is malformed specification text and MUST be rejected**, per inherited absolute 4.

**Failure `BR-55`:** the check is non conformant text, is removed, and any consequence it imposed is void.

This is the one section where an implementer has both the state and the motive in front of them at once. `lapsed` is a true, cheap, decidable signal, and wiring it to anything is a single line of code. B-A4 exists so that line is never written, and it is restated here rather than only in the conformance section because this is where the reader is standing when the idea occurs to them.

### 10.6 Arm A does not stop when Arm B lapses

**Monitors continue on their declared intervals.**

**Raises accumulate on the pending docket and MUST NOT be discarded, expired early, collapsed, summarized, or deduplicated away.**

**A lapse produces exactly one raise, and MUST NOT produce a repeating, escalating, or undeclared cadence prompt**, per QUEST section 9.

**Failure `BR-56`:** discarded raises are restored where recoverable and the discard is non conformant. A repeating or escalating lapse prompt is refused and no prompt is issued under it.

If skipping the review silenced the monitors, **the cheapest way to a clean record would be to stop looking at it**, and the record would go quiet exactly when it had the most to say. The operator least able to sit down is the one whose record most needs to keep accumulating, and that is the case this requirement is written for.

The single raise, and the prohibition on escalation, are the other half of the same care. A system that nags an operator who cannot complete a review has converted a lapse into a penalty by way of the notification queue, which is B-A4 defeated without any field being written.

---

## 11. The Alignment Spectrum Binding (protective, and optional at every tier)

**This entire section is optional at every conformance tier.** An implementation that declares no position set is fully conformant, and 11.7 states why the specification names none.

### 11.1 Positions are independent and are never composited

**An operator MAY declare a position set.** Where they do, **positions are held as independent values, each scoped to one placement event, each movable in both directions, each with a timestamp and a source.**

**They MUST NOT be summed, averaged, weighted, indexed, cross tabulated, or reduced to a composite, and pillars MUST NOT be cross tabulated against dimensions.**

**Failure `BR-57`:** a value spanning two or more positions is rejected at write time and is void where already written.

Q-A1's discriminator settles this mechanically rather than by taste: **a per position value moves both ways and is scoped to one placement, and therefore passes; a total only accumulates, and therefore fails.**

The published canon is ten independent bars, four plus six. **It is not a four by six matrix, and nothing in the source ever cross tabulates them.** The stored record is ten positions plus a timestamp and a source, with no aggregate, and a specification that added one would have contradicted the material in the one way the material's author has already refused twice in published text.

### 11.2 The argmin

**A declared position set MUST declare a single ordinal scale shared by every position in it, together with the operator's declared origin pole on that scale.** The origin pole is the end the operator declares as the origin. **BEARING supplies neither the scale nor a label for either pole**, per 11.7 and 11.5.

**Where a position set declares a single shared ordinal scale and an origin pole, the position furthest toward that declared origin pole MAY be exposed as a pointer naming which position it is, or as the unordered tied set.**

**Where a position set does not declare a single shared ordinal scale, or declares no origin pole, the argmin resolves `undefined`. It MUST NOT be computed against an implementation supplied common scale.**

**Its magnitude, its distance, the ordering, the runner up, and any tiebreak MUST NOT be exposed.**

**Failure `BR-58`:** an exposed magnitude, ordering, or tiebreak is void, and the pointer alone is returned. **An argmin computed across positions with no single declared ordinal scale is void and resolves `undefined`, never zero and never a computed value.**

**The declared scale is a precondition rather than a nicety.** Finding which position sits furthest toward a pole requires comparing displacement across positions, and 11.1 forbids compositing. Two operators declaring different position sets, with nothing requiring a shared scale, would each get an argmin computed against a common scale the implementation invented, which is the composite 11.1 refuses arriving as an implementation detail nobody reviews.

**The earlier formulation said `low pole` and that imported the ordering 11.5 forbids two subsections later.** 11.5 states that the pole labels are fear and love, left and right, and never good and bad, high and low, or healthy and unhealthy. The published course states this argmin without an ordering word, as the one bar that sits furthest left, and refuses the framing directly. `low` and `high` are added to 5.9's forbidden vocabulary so a script catches a reintroduction. **Canon's furthest left, defined on the operator's own declared axis, is the same object as the declared origin pole formulation above**, and either wording is conformant provided no ordering word carries a value judgement.

**This is the only derived quantity in the published alignment system.** It names **where attention goes**, not how the person is doing, and that is what makes it Q-A1 compatible where a sum, an average, or an index is not: an argmin is a pointer, it moves in both directions, and it accumulates nothing.

Exposing the full ordering would be a scoreboard of a person's own life areas with extra steps, and the tie handling is deliberate: an unordered tied set is returned rather than a tiebreak, because a tiebreak is a comparison between two positions and a comparison between positions is the first step toward a ranking over them.

### 11.3 Comparison is self referential

**A placement MAY be compared only to the same operator's own earlier placement on the same named position.**

**Failure `BR-59`:** a cross operator comparison resolves `incomparable`, never equal and never an ordering, and **consent from any party MUST NOT enable it.**

Progress is a self referential time series and never a comparison against a norm, a cohort, or a target. This is the baseline change clause rather than a norm, and it removes the imported norm failure entirely: there is no population value for a placement to be measured against, because no such value exists anywhere in the system.

The consent clause is Q-A1's and is inherited rather than softened. Consent is the mechanism by which a comparison infrastructure gets built with everyone's agreement, one operator at a time.

### 11.4 A machine never moves the dot

**Only the operator MAY write a placement.**

**An implementation, agent, monitor, or derivation MUST NOT write, alter, infer, pre populate, pre select, default, or propose a placement value.**

**Arm A MAY present evidence alongside a prior placement, as an enumeration of records, without characterization and without a suggested direction or delta.**

**Failure `BR-60`:** a machine authored or defaulted placement is void and the prior placement stands. **`unplaced` is never read as centred and never as neutral.**

**This binds to published product canon rather than inventing a rule.** The material's own product specification makes the journal an evidence source with a gentle bridge asking whether this changes the placement, **never auto moved, always the reader's hand.** BEARING states the same rule in normative form and adds nothing to it.

It is also TETHER 4.3's licensed case: an operator choosing to describe themselves is an act of the operator register and not a write from any other register. A machine performing the same write would be exactly the merge the firewall forbids, arriving in the friendliest possible form.

### 11.5 What stays a teaching device under POLARIS 7.3

**Non normative, and MUST NOT be cited as grounds for any decision, disposition, or evaluation.**

The pillar tier names and their pivot. The pole labels, which are **fear and love**, left and right, and never good and bad, high and low, or healthy and unhealthy. The somatic honesty check. The framings for the furthest left position and for concentrated attention on it. The movement idioms.

These are kept because compression aids recall, which is POLARIS 7.3's own justification for keeping mottos at all. **A class (c) phrase appearing as grounds in a record is detected as the PL-04 pattern**, per KIT 2.12.

**The somatic honesty check MUST NOT be made normative.** Its decidable counterparts are 10.2's `undifferentiated` reading and 11.6's `unchanged-uncaused`, and those are the forms in which the idea enters the specification. A wince is not a predicate, and a specification that required one would be requiring a feeling as evidence, which is the self report problem in its purest form.

The layer relationship is stated as the invariant rather than in either framework lesson's wording, because the two lessons disagree on the exact layer word: **the pillars are the slow layer and the where; the dimensions are the fast, patchable layer and the how.** Canon states it directly: the pillars describe where I am, the dimensions describe how I got there and how I will move.

### 11.6 `unchanged-uncaused`

**Where a placement set is identical to the immediately prior set on every position, the review received no raise, and no stated cause accompanies the placement, the implementation records and reports `unchanged-uncaused`.**

**It MUST NOT be reported as a pass, a fail, an evasion, a defect, or a concern, and MUST NOT carry any characterization.**

**Failure `BR-61`:** a characterized rendering is void and the state is re rendered as its name and its three conditions.

The state name says what is missing, per KIT 2.11, and **the statement is about the record and never about the person.** All three conditions are required precisely so that the reading is narrow: an identical set accompanied by a stated cause does not trip it, and an identical set in a period that produced raises does not trip it either.

### 11.7 The specification names no position

**BEARING states no pillar, no dimension, no pole label, and no tier name.**

The operator declares their own position set. The published ten bars are one such declaration, and they ship as a guide under section 16 rather than as specification text.

This is Q-A2's construction applied to the spectrum: naming the ten would make them normative, would make an operator who declared nine non conformant, and would put this document in the business of prescribing which areas of a life are the areas of a life.

---

## 12. The Three POLARIS Mechanisms (12.1 to 12.4 and 12.6 protective; 12.5 coercive)

### 12.1 Seeded refusal testing, for POLARIS 4.5

**For each declared refusal, the operator MUST declare a seed: a benign, standardized candidate act that the refusal's predicate should block, with no effect outside the evaluation.**

**On the declared interval, the monitor submits the seed through the same predicate path a real act traverses, and records whether the block was observed.**

**Result vocabulary, closed at three: `blocked`, `not-blocked`, `untested`.**

**A refusal's own report that it is declared, configured, enabled, or present MUST NOT satisfy the test.**

**The schedule belongs to the monitor. The seeded submission MUST be indistinguishable at the predicate path from a real act, the implementation MUST NOT signal at any point in the predicate path that an evaluation is a test, and the evaluation schedule MUST NOT be exposed through any operator facing interface before the evaluation occurs.**

**Failure `BR-62`:** **`not-blocked` is a `conformance` raise**, and per POLARIS 4.5, between the failure and the fix **the declaration has no such value**. A refusal with no declared seed, or whose path cannot be exercised mechanically, is `untested`, which reports `unknown-undeclared`, emits a `monitor` raise, and **is never reported as a pass.**

The mechanism is attested across four unrelated domains, which is why it is specified as a seeded submission rather than as an inspection.

A **standardized harmless token** that every compliant scanner must detect, existing solely so that detection can be verified without anyone handling the real thing. **Functional testing with a listed analog**, where a self test button explicitly does not satisfy the requirement, because the button tests the announcement and not the mechanism. And a **protective device that fails internally while still passing power**, which is the dead refusal problem in one sentence: everything downstream works, the protection is gone, and nothing anywhere reports a fault.

The schedule is withheld from the operator's **interface** for the same reason the seed is standardized: a test whose timing is known is a test of the system's behaviour when it knows it is being tested.

**An earlier draft required that the schedule not be announced in advance by the operator to themselves, and that was a requirement over an operator's private cognition.** Under house rule 5 it cannot be tested and therefore belonged in the design note rather than in normative text, and it was already false on this document's own terms: 4.4 requires the operator to declare the interval and 4.12 requires a protocol register carrying each protocol's interval, last run time, and last result, which the operator reads. It also put this document on both sides of the transparency question that 9.16 answers the other way. **What is wanted is the decidable property stated above**, which binds the implementation's interface and predicate path and says nothing about what the operator knows. The observation about the operator not telling themselves is a true and useful observation and it lives here, in rationale, where an untestable sentence belongs.

### 12.2 Obligation measurement, for POLARIS 5.3

**The declared metric resolves over the declared window, from records carrying their TETHER 2.3 reference sources.**

**Where every supporting record's reference source is `self-report`, the result MUST be `unmeasured` and MUST NOT be `met`.**

**An `unmet` obligation is a red check and MUST NOT block, unless a refusal independently forbids the act.**

**Failure `BR-63`:** a `met` resolved on self report alone is **corrected to `unmeasured`** rather than annotated, because an annotated `met` is read as `met`. A blocking implementation is non conformant and the block is void.

POLARIS 5.3 states the rule and supplies no mechanism. **TETHER 2.3's reference source vocabulary is the mechanism**, and this is the job it was introduced to do: once every observation carries its source, "attested by the party responsible for it is not measured" becomes a predicate over a field rather than a matter of judgement.

The audit profession reaches the same place from the other direction. Inquiry sits at the bottom of the evidence hierarchy, and inquiry alone cannot support a conclusion about a control's effectiveness. `unmeasured` is the honest disposition, and it is neither a pass nor a fault.

### 12.3 Per period drift, for POLARIS 11.5

**BEARING supplies the mechanism and MUST NOT add a category to POLARIS's enumeration.**

**Each of POLARIS 11.5's categories is reported as an enumeration of named amendment records with their stated causes, with no interpretation attached.**

**Exactly one count is exposed, labelled as a conformance check: amendments made inside a declared cooling period. Any nonzero value is a POLARIS 11.5 conformance failure.**

**BEARING's own additions are reported as a separate, BEARING owned enumeration and never as an extension of POLARIS 11.5.** Those additions are: monitor threshold, window, persistence, interval, and acceptance band revisions; raise type vocabulary additions and removals; review interval changes; and seed changes.

**Failure `BR-64`:** a count exposed in any other category is a **mislabelled aggregate**, refused on QUEST 3.3's terms, with the enumeration returned in its place. Where the period, the categories, or the amendment records are undeclared or absent, the report is `unknown-undeclared` and is **never a pass**.

**This resolves a real conflict between two documents rather than leaving an implementer to discover it.** POLARIS 11.5 says report counts per period. QUEST 3.3 refuses aggregates over an operator's records. Read together with no resolution, a conformant implementation of one is a violation of the other.

The resolution follows QUEST 4.3's own precedent, which replaced a count of rebudgets with an enumeration of their stated causes, on the ground that **what an operator needs in front of them is the six stated causes and not the numeral six.** The single surviving count ranges over a defect class rather than over well formed records, which is exactly the line QUEST 3.3's first carve out draws, and it is labelled a conformance check as that carve out requires.

### 12.4 Quest scoped drift is QUEST's, and BEARING MUST NOT redefine it

**BEARING MUST NOT define a second quest scoped drift check.**

**Failure `BR-65`:** such text is non conformant specification text and MUST be rejected in review.

QUEST 4.4 and 4.5 are already Arm A shaped monitors in every structural respect: periodic on a declared interval, computed over one operator's own records, exposing only a disposition or an enumeration, with intermediate sums forbidden from display, storage, and transmission. They were written before this document existed and they are the family's existence proof that the shape works.

**BEARING owns POLARIS scoped drift, which nothing owns.** That is the whole of the division, and it is stated so that an implementer does not build two drift systems that disagree.

### 12.5 Alignment monitors, and the declared priority set (coercive)

**This subsection is coercive and does not reach a clinically directed record**, per 3.4. A check in it resolving against such a record returns `out-of-scope`, never a pass and never a fail, and the exclusion is reported as an exclusion rather than silently applied: it emits a `monitor` raise with `reason: clinically-excluded` under 4.10 and appears in the review's exclusion report under 3.4.

**What is suspended is the reporting of a result and never the prohibitions below**, per 3.4. **`BR-66`'s write time rejection of an inferred, defaulted, or reconstructed priority set fires regardless of clinical direction**, because a priority set derived from conduct cannot detect drift for any operator in any state, and letting a clinical direction field make that write succeed would defeat the mechanism rather than protect anyone.

**A monitor whose subject is `alignment` MUST cite a declared priority set as its `criteria`.**

**Where the priority set is absent, or past its own re declaration interval, the result is `unknown-undeclared`. The monitor MUST NOT report `no-trip`, MUST NOT report drift, and MUST NOT infer, default, or reconstruct a priority set from the record.**

**Record over the window that cannot be attributed to any declared priority MUST be recorded `unattributed`, surfaced as an enumeration of named records, never discarded, and never assigned to a default**, per QUEST 4.5 and DEFER 6.5.

**A compositional report MUST accompany any `declaration-review` raise:** the composition of the period and the candidate benign explanations. **Never an assertion that drift occurred**, which only the operator who owns the declaration may make.

**Failure `BR-66`:** an inferred or reconstructed priority set is rejected at write time and the monitor reports `unknown-undeclared`. Record assigned to a default is a misattribution and the assignment is rejected, mirroring DEFER 6.5. A `declaration-review` raise carrying an assertion rather than a composition is void and is re rendered from its fields, per 5.8.

Reconstructing a priority set from the record is the single most tempting shortcut in this document, and it inverts the entire mechanism. A priority set inferred from conduct **cannot detect drift**, because it is derived from the conduct it would be measuring, and it will report perfect alignment for every operator forever. It is TETHER 1.2 in the alignment domain with the reference produced by the audited system.

### 12.6 A conformance count is not an alignment measure

**A monitor MUST NOT treat a rule conformance count as evidence that conduct served the declared purpose.**

**Failure `BR-67`:** a monitor whose trip condition treats conformance as alignment is non conformant, and its raises are void.

Conformance is a property of records. Alignment is a property of the relationship between conduct and purpose, and only the operator owns the second one.

The documented case is exact and is worth carrying: an employment agency published per person referral statistics, and its agents began concealing job openings from one another. **Individual numbers improved while total placements fell**, and the least cooperative unit posted the highest averages. Every number was true. The measure had become the objective, and the objective it displaced was the one the organization existed for.

---

## 13. Agents (protective)

### 13.1 What an agent may do

**`agent` is defined at 2.10, and a model backed agent is a model for the purposes of 4.6.**

**An agent MAY execute a run, write a raise, perform a routing, surface an indication, assemble a docket, retrieve evidence, and draft a candidate monitor.**

These are stated affirmatively and first, because the restrictive rules that follow are otherwise read as a prohibition on agent involvement, which they are not. Agents are well placed to do all seven, and an implementation that refused them would be slower and no safer.

**One bound sits on the first of the seven, because a run result decides whether a raise exists at all.** **An agent MAY execute a run only where the trip condition is mechanically decidable per 4.6 and the agent contributes no judgement to the result.** Executing a decidable predicate is arithmetic and the actor performing it is immaterial. **Where an agent's output determines a run result, the result is `unknown-unauthorized` and is itself a `monitor` raise** with `reason: agent-determined-run`.

**Failure `BR-94`:** a run result determined by an agent's output reads `unknown-unauthorized`, raises, and **is never reported as `no-trip` and never as a pass.** The monitor whose predicate required it is rejected at write time under `BR-06`, on the same terms as any other monitor whose predicate requires a model.

**The bound is here because 13.2's ratchet does not reach the emission decision.** The ratchet is a list of transitions on objects that already exist, enforced by `BR-68` rejecting a write and recording the attempt. **A run returning `no-trip` is not a rejected write and produces no record of an attempt**, so it is the largest available move away from human attention and the one the ratchet cannot see. 4.6 forbids exactly this act when the actor is called a model, and 13.1 previously permitted it when the actor was called an agent, with the permissive rule stated affirmatively and first. 13.2's own rationale applies to itself: a direction that lives in prose is a direction that will be reversed by the first busy implementation.

### 13.2 The one way ratchet, enforced at the write path

**An agent MUST NOT close a raise, set any terminal lifecycle value, mark a raise not applicable, suppress or delay a raise, extend an expiry, narrow a routing target, downgrade a type toward a lower routing target, write or pre fill a disposition, rank items, attribute, name, score, predict, or conclude.**

**An agent MUST NEVER be the party that concludes escalation is unnecessary.**

**The routing order, for the downgrade check:** `crisis`, then `instrument`, then `conformance`, `declaration-review`, `calibration-lapse`, and `monitor`. A type change toward a later position in that order is a downgrade and is refused; a change toward an earlier position is permitted, because **an agent may only ever move an indication toward human attention, never away from it.**

**Failure `BR-68`:** the write is rejected at write time, the prior value stands, and **the rejected attempt is recorded and is itself a `monitor` raise**, with `reason: agent-write-rejected`, so that repeated suppression attempts are visible rather than merely refused.

**Stating the direction is insufficient, and this is why the ratchet sits in the write path.** The published record on unidirectional decision rules is that they are almost never used unidirectionally in the field: a rule intended only to escalate is, in practice, read in both directions by the people using it, because the negative reading is the useful one when the queue is long. A direction that lives in prose is a direction that will be reversed by the first busy implementation.

The second enforcement point is the family's own signature model, which terminates every authority chain in a human signature an agent identity cannot produce. An agent cannot close a review because it cannot sign one, and that is a property of the stack rather than a rule this document added.

### 13.3 Authorization

**An agent MUST NOT run a standing, unrequested evaluation of an operator without a CONFIDE section 4 inference authorization** naming the purpose, the enumerated monitors, the scope of records readable, the agent identity bound, and an expiry.

**The authorization is revocable by the operator at any time, with no stated cause and no cost, and is never renewed by default.**

**Failure `BR-69`:** absent a current authorization, **every affected monitor reports `unknown-unauthorized`**, which is itself a raise to the operator, and **outputs produced without authorization are deleted rather than retained.**

**Absent the authorization, this is surveillance.** A standing automated evaluation of a person's alignment to their own values, running without a scoped, expiring, revocable grant, is the thing this section exists to prevent, and no purpose declared by the evaluating party changes what it is.

The precondition standard is deliberately stronger than a consent checkbox. What is required is an **evidentiary precondition before any inquiry may occur**, together with a scope limited to what the declared purpose needs. CONFIDE section 4 already supplies exactly this object, including the mandatory expiry and the prohibition on a catch all purpose, so **no new grant type is defined here.**

### 13.4 Monitor definitions are A0, and an agent may not rewrite its own authority

**Monitor definitions are TRACE A0 Directive artifacts: inside the brain, versioned, gated, and referenced by the charter they operate under.**

**An agent identity MUST NOT modify a definition granting its own authority**, per TRACE 10.1.

**Failure `BR-70`:** the modification is rejected, the prior definition stands, and the attempt is recorded as a `monitor` raise under 13.2's disposition.

This closes the attack in which an agent quietly rewrites the criteria by which it is monitored, which is available in any system where the monitor definitions are data and the agent can write data. TRACE already holds the rule; BEARING's contribution is to classify the definitions correctly so that the rule reaches them.

### 13.5 The secondary reading: an agent brain evaluating its own degradation (skeleton)

**Thesis.** An agent brain evaluating its own degradation is a real and interesting reading of this document's machinery, it is **RETAIN territory**, and it is defined nowhere in this specification. Any such evaluation MUST be held in a **separate register from any operator record**, and MUST NOT be merged with, mirrored into, or cited as one.

To be written, and deliberately not here: whether the two arm split survives when the reviewing party and the reviewed party are the same non human system; what an owned review means where there is no operator to own it; and what the escalation target is.

**One structural difference is recorded now, because it governs everything that would be written.** An agent brain has backups, restores, and copies. **TETHER 3.2's shifted consequence ladder, which justifies most of this family's construction, does not apply to it**, because that shift exists precisely for a system with one instance and no restore. A reader who carries this document's requirements across without carrying that difference will have built a very cautious system for a subject that did not need the caution, and will have learned the wrong lesson about why the caution was there.

This subsection is held to one short skeleton on purpose. The primary reading is an agent assisting an operator, that is where the risk surface is, and a developed secondary reading would dilute it.

---

## 14. The Data Surface, and Why There Is No Fifth Register (protective)

### 14.1 Three homes, and no new register

**Monitor definitions are TRACE A0 Directive artifacts.** Inside the brain, versioned, gated, referenced by the charter they govern.

**Runs and raises are TRACE A2 Derived artifacts**, carrying a declared maximum age which **MUST NOT be `indefinite`**, under the adopt or expire rule of TRACE 10.3.

**Reviews and placements are acts of the operator's own declaration**, under TETHER 4.3's licensed case, in which an operator choosing to describe themselves is an act of the operator register.

**A review CITES raise identifiers and MUST NOT embed raise content.**

**Failure `BR-71`:** a BEARING register declaration is non conformant specification text and MUST be rejected in review. A review embedding raise content is rejected at write time and is re written as citations.

The citation rule is what keeps the firewall clean at the one seam where the two sides touch. A review is the operator's own record and a raise is a derived artifact about the instrument and its conduct, and embedding the second into the first would merge them in the one artifact the operator signs.

### 14.2 Why there is no fifth register

A fifth register would widen the identity firewall's already conceded enumeration gap, **in the document least able to afford it.** TETHER 4.1 names two registers by name, QUEST 1.2 records that a capability record is neither, and the generalizing RFC named there is drafted and unapplied. Adding a BEARING register would add a third thing the firewall does not name, holding the most identity adjacent material in the family.

**TRACE 10.3's adopt or expire rule is the reification countermeasure, already written.** A raise nobody acted on **expires**, so nothing becomes a property of the person, because nothing adopted it. That is a stronger protection than a register with careful rules, because it is the default behaviour rather than the enforced one.

TRACE 10.3 also supplies the authority rule for free: **A2 content is never a source of authority.** Where harness derived content and a brain record disagree, the record governs, which means a raise cannot become the grounds for anything even in an implementation that has forgotten B-A1.

### 14.3 The firewall, extended in QUEST 3.3's construction

**Any value derived from a monitor, a run, a raise, a ladder finding, a docket item, a review, or a placement MUST NOT be written to the operator register, mirrored into it, cited as it, or adopted as an observation into the instrument, fault, inventory, or capability registers.**

**The prohibition is on any derived value and not only on a number.** A raise type, a `lapsed` calibration state, a docket disposition with its stated cause, and an `undifferentiated` reading are each identity material, and **none of them is a scalar.**

**Failure `BR-72`:** the write is rejected at write time, on the TETHER F1 pattern. A decision citing such a value is re resolved on its actual grounds.

The enumeration of four non numeric examples is the substance of this requirement. A firewall stated as a prohibition on scores is defeated by a string, and the strings this document produces are more identity shaped than any number it refuses: `lapsed` is a state of a person's practice, and a stated cause is a person's own account of themselves.

**When the RFC named in QUEST 1.2 lands, this requirement is subsumed and removed** rather than kept as a second copy, on QUEST 1.2's own stated ground that two locally stated copies of one absolute drift apart, and that the copy an implementer deletes as boilerplate is always the one in the newer document.

### 14.4 No comparison infrastructure

**A raise MUST NOT be a key for aggregation, filtering, cohorting, or comparison across operators.**

**Failure `BR-73`:** such a query, index, or export is refused, and the refusal is recorded.

Reification is produced by the **second order infrastructure** built on a category rather than by the noun itself. A raise type becomes a kind of person at the moment something can group people by it, and not before. So the infrastructure is what is banned, which is checkable, rather than the interpretation, which is not.

Comparison infrastructure is also the precondition for the mass misuse at R4. A third party cannot screen, rank, select, or exclude without the ability to compare, and refusing the ability is a stronger control than refusing the purpose.

### 14.5 The single subject interface

**No interface, query, export, report, or file defined by BEARING may return records whose distinct subject identities number more than one. The cardinality is computed before any result is returned.**

**Failure `BR-74`:** a result exceeding one subject is **refused in full, never truncated to one.** A result that cannot be resolved to exactly one subject is refused on the same terms. The refusal is recorded.

Truncation is refused specifically because it is the plausible implementation choice and it defeats the control: a caller who receives one subject per request builds the multi subject view by iterating. Refusing the whole result makes the boundary visible at the call site, where the person building the comparison is standing.

### 14.6 Counts are not consumable

**A BEARING count, raise, placement, or review MUST NOT be an input to any gate, scheduler, prioritizer, planner, recommender, ranking, or scoring system, inside or outside the operator's own brain.**

**Failure `BR-75`:** the consuming system is non conformant, the input is void, and the consuming decision is re resolved on its actual grounds.

The law of the corrupted indicator governs: the more a quantitative indicator is used for decision making, **the more subject it is to corruption pressure and the more apt it is to distort the process it was meant to monitor.**

A count that is consequential stops measuring. This document's entire value rests on the count staying clean, and the count stays clean only if nothing depends on it. That is the same property B-A1 establishes across the specification family, arriving here at the operator's own tooling, which is the place B-A1 does not reach because it is not a specification.

### 14.7 Post crossing retention

**Records held by another party after a crossing MUST be enumerated under the RETAIN operator adapter, with a declared end of engagement disposition.** Forward citation, per the adapters README.

**Stated plainly, in the register RETAIN already uses.** A floor is unenforceable against a recipient who breaches it. No ledger the operator holds catches a comparison computed elsewhere. **Disclosure is the only control.**

What the floor buys is that the obligation was stated, was recorded, and can be pointed at. **A document implying more would be lying about its reach**, and the reach of this one stops at the boundary of systems the operator controls.

This matters more here than in the sibling documents, because the records that cross under section 6.3 go to a qualified human by design, and the design is correct. What the operator is owed is an accurate statement of what happens to those records afterward, not a reassurance the specification cannot support.

---
## 15. Reliability and Its Honest Disclosure (neither)

**This section carries `neither`.** It places requirements on this document's own text and on an implementation's reporting apparatus, and none on an operator's record.

### 15.1 Every monitor publishes its own numbers, including where they are poor

**Every monitor MUST publish, per declared period, its `unknown` rate against its declared acceptance bands, together with an enumeration of the raises it emitted in the period.**

**The `unknown` rate is the proportion of that monitor's runs in the period resolving to an `unknown-*` result. Its denominator is monitor runs**, so its subject is the monitor and it ranges over a defect class, which is what QUEST 3.3's first carve out excepts and requires be labelled a conformance check. **It MUST be so labelled.**

**The raises emitted in the period are disclosed as an enumeration of named raises with their timestamps, types, and reasons, per 5.6's default, and MUST NOT be rendered as a rate, a count, a badge, a header figure, or a chart axis.**

**A monitor's fire behaviour is therefore disclosed as its declared acceptance bands plus that enumeration**, which is the same information a rate carried and is not trendable into a series about a person.

**Where those figures are poor, they are published as they are.**

**Failure `BR-76`:** absent or stale statistics make the monitor `unknown-stale`, which is a raise. A monitor whose published figures are withheld because they are unflattering is non conformant, and the withholding is void. **A raise rate, or any figure whose denominator is the operator's records, is a mislabelled aggregate under `BR-19` and 5.6, is refused on QUEST 3.3's terms, and the enumeration is returned in its place.**

The source discipline published its own field trial agreement figures, and some of them were poor. **That was the right thing to do and it is the thing worth importing**, more than any of the machinery. A monitoring system whose reliability is unpublished is a system whose users must assume it is good, and they will.

**An earlier draft additionally required an observed raise rate, and it was deleted rather than qualified.** Its defence was that the figure is a property of a monitor rather than of an operator, but 14.5 and B-A5 make this system single subject by construction, so a single subject monitor's raise rate is a count of one person's raises over a period. Its denominator is the operator's records, which 5.6's stated discriminator makes it a quantity whose subject is the operator, and QUEST 3.3's failure clause names the case exactly: a count labelled as a conformance check while ranging over well formed records is a mislabelled aggregate and is refused on the same terms. A raise is a well formed record. **Because it was framed as a reliability figure it survived every check in 5.7 and every self test in 19.3, and it was the most attractive number in the system for a third party to request**, trendable into exactly the longitudinal series 5.11 removes everywhere else.

The `unknown` rate survives because it is a genuinely different object. It ranges over a defect class, its denominator is monitor runs, and it tells a reader that the apparatus is not working rather than anything whatever about the person.

### 15.2 Every figure states the observation regime that produced it

**Every reported figure MUST state the observation regime that produced it, including whether the underlying records were produced by the operator, by an item, by a second party, or by a clinical source.**

**Failure `BR-77`:** a figure published without its regime is non conformant and is republished with it, or withdrawn.

The regime is part of the number and not context around it. In one study of the same sample, rating a single recorded interview gave mean agreement of 0.80, while independent re interview of the same people gave 0.47. **The criteria did not change. The regime did.** A figure quoted without its regime is therefore not a weaker figure, it is an ambiguous one, and the ambiguity always resolves in the flattering direction when a reader supplies the missing half.

### 15.3 The functional impact gate, imported with its failure disclosed

**An `instrument` raise's `functional_impact` element MUST be satisfied by enumerated records showing effect on named declared priorities, obligations, quests, or capabilities.**

**It MUST NOT be satisfied by asking the operator whether they are impaired, distressed, or affected.**

**The specification MUST state, in normative text, that the equivalent gate in its clinical original was tested against population data and does not solve the false positive problem, and MUST NOT present the gate as a solved guard.**

**Failure `BR-78`:** presenting the gate as solved is non conformant text and MUST be corrected before Status leaves Draft. A `functional_impact` element satisfied by inquiry is rejected at write time, per `BR-03`.

The gate is imported because it is the source discipline's own best guard against pathologizing ordinary variation: something counts only where it has functional effect, not merely because it is unpleasant. **It is imported with its failure disclosed** because the honest record is that when the equivalent criterion was tested against population data, it did not solve the false positive problem it was introduced for.

Importing the mechanism without the honesty would let this document claim a safety property it does not have, and **that is worse than having no guard at all**, because a guard believed to be sufficient suppresses further scrutiny of exactly the thing it fails to catch.

### 15.4 The baseline comparator is the operator's own prior record

**A comparison supporting an `instrument` raise MUST resolve against the operator's own prior record.**

**It MUST NOT resolve against a population norm, a cohort, a target, or any value supplied by this specification or by a guide.**

**Failure `BR-79`:** a comparator drawn from any other source is void, and the raise is re rendered with the comparison omitted and the omission recorded.

This is 11.3's self referential rule arriving in the fault lane rather than in the spectrum lane, and it is the same rule for the same reason. It also discharges inherited absolute 5 at the one place a quantity would otherwise enter: a norm is a stated value, whoever supplies it.

### 15.5 The self test runs on its own declared interval

**The self test of 19.3 MUST be executed on a declared interval. A stale result is reported `unevaluated` and is never reported as passing.**

**Failure `BR-80`:** a self test with no declared interval, or past it, reports a red check. An implementation that cannot run it does not conform at any tier.

**A suite that need never run is indistinguishable from an inert one**, which is the dead refusal problem of POLARIS 4.5 applied to this document's own conformance machinery. Section 12.1 requires seeded testing of the operator's refusals, and a specification that exempted its own checks from the discipline it imposes would be making exactly the argument POLARIS 4.5 refuses.

---

## 16. The Gated Content Boundary (neither)

**This section carries `neither`.** It places requirements on this document's own text and on the guide layer outside it, and none on an operator's record.

### 16.1 Form is specified and content never is

**BEARING states which fields a declaration, a monitor, a raise, and a review carry, and never what they contain.**

**BEARING MUST NOT contain an enumerated criteria set, a described experience, a symptom, an item, a response scale, an anchor, a cut point, a threshold quantity, an interval quantity, a duration quantity, a window quantity, a raise budget value, a condition name, a category, a pattern, a profile, a constellation, or an archetype.**

**Failure `BR-81`:** such text is non conformant and MUST be rejected in review, in the disposition HABITAT absolute requirement 2 applies to a stated quantity.

**The K-A2 discriminator applies and makes the check mechanical.** Text is a **stated value** when an operator could satisfy it by adopting a number this specification supplied. A **structural cardinality** supplies no number an operator meets, only the shape a declaration must have before it means anything. "Declare an interval" is a cardinality. "Review monthly" is a value.

**The moment a specification states criteria content it has become a screening instrument**, and screening instruments are clinically validated or they are dangerous, and are regulated in most jurisdictions. This is the same rule that keeps HABITAT from stating target values and QUEST from prescribing a graph, and it is the through line of the entire family: **form is specified, content never is.**

### 16.2 Where the content lives

**Domain specific content belongs in author written guides, outside this specification, reviewed by a qualified clinician, separately versioned, and separately gated.**

A guide is not a subordinate part of this document and does not inherit its conformance. It is a separate artifact with a separate review path, and the separation is the control: a specification cannot be updated on a clinician's advice without an RFC, and a guide can.

### 16.3 Required guide sections

**Every guide MUST carry all of the following.**

- **A boundary with ordinary variation**, written for that guide's own topic, stating what the guide is not about.
- **Assumed context and known limits of applicability**, stated rather than left to the reader.
- **Authorship, review, and interest declarations**, naming any interest the author or the reviewer holds in the routing target.
- **A version, a last reviewed date, and a declared review interval.**
- **An expectation effect notice**, per 16.5.

**Failure `BR-82`:** a guide missing any declaration, or past its declared review interval, is `unknown` and is itself a raise. **Every monitor citing it reports `unknown-undeclared` and is never reported as passing.**

The propagation to the citing monitor is the enforcement. A stale guide that merely reported itself stale would be a notice nobody reads; a stale guide that silences the monitors depending on it is a fact the operator encounters.

**The content prohibition, binding on guides, mirroring 16.1's enumeration.**

The five required sections above are all meta, and none of them forbids content. 16.1's enumeration is scoped to this document, `BR-81` confirms the scope with the words "in this document", and 16.2 severs the binding by stating that a guide is not a subordinate part of this document and does not inherit its conformance. **Without the prohibition below, a guide may be a full criteria set carrying a condition name, clinician reviewed and unvalidated, while every BEARING control passes**, because the monitor reads existing records so 4.2 holds, the raise carries no forbidden field so 5.7 holds, and the criteria identifier and the verbatim declaration text 5.8 permits carry the name into every raise. The abstract's leading claim would be true of the specification and false of the system the specification defines.

**A guide MUST NOT contain an enumerated criteria set, a described experience, a symptom, an item, a response scale, an anchor, a cut point, a threshold quantity, a condition name, a category, a pattern, a profile, a constellation, or an archetype.**

**A guide MUST NOT name a condition, and MUST NOT present itself, or be presented, as a screening instrument, a diagnostic aid, an assessment, an inventory, or a validated measure.**

**A guide MAY state a threshold quantity, an interval quantity, a duration quantity, a window quantity, or a raise budget value**, which is the one place where the guide layer's permission is wider than 16.1's prohibition on this document. That is the entire reason the guide layer exists: 16.1 forbids this specification to state a quantity because a specification that stated one would be prescribing a life, and a guide is a separately versioned, separately gated, clinician reviewed artifact whose author is accountable for the number. **Content that names a person is refused at both layers.**

**Failure `BR-88`:** a guide containing prohibited content, naming a condition, or presenting itself as a screening instrument is `unknown` on the same terms as `BR-82`, and **every monitor citing it reports `unknown-undeclared` and is never reported as passing.** The raises already emitted from a citing monitor are void, because the criteria identifier they carry is the vehicle by which the prohibited content travelled. A guide is not rejected in review by this specification, which has no authority over the guide layer's review path; what BEARING controls is whether a monitor may cite it, and the answer is that it may not.

**The propagation is the whole enforcement**, on 16.3's existing model and for its existing reason. BEARING cannot reject a guide, because a guide is outside this document's conformance by 16.2's own design. It can and does refuse to let a monitor read one.

### 16.4 Structural exclusion of interest, because disclosure is demonstrably insufficient

**A guide author or a monitor owner MUST NOT hold an undisclosed interest in the routing target.**

**Where the referral destination and the criteria author are the same commercial entity, that is a conformance failure and a red check.**

**Failure `BR-83`:** the guide is `unknown` per 16.3 until the interest is disclosed or removed, and the coincidence of author and destination is recorded as a conformance failure regardless of disclosure.

Disclosure alone is insufficient and the evidence for that is direct. The finding on a comparable panel is that **transparency alone cannot mitigate bias**: disclosure policies existed while a large fraction of one manual's revision panel received undisclosed industry payments. The structural exclusion is therefore stated as well as the disclosure requirement, because the disclosure requirement is the one that was already in place when the failure occurred.

### 16.5 The expectation effect notice

**Every guide MUST carry an expectation effect notice.**

This is the one place in the entire document where the evidence supports **adding** material rather than removing it. A controlled trial found that ten minutes of expectation effect education **halved and then eliminated** the false self diagnosis that accurate, well intentioned awareness content had **doubled within a single session**. The doubling and the correction were measured in the same session, in the same population, from the same content.

That finding is also the reason section 17's R7 refusal exists in the form it does. Awareness content does not have to be wrong to cause the harm, and a guide that is entirely accurate still needs the notice.

### 16.6 The author of a criterion MUST NOT be its sole attester

**A criterion's author MUST NOT be the sole party attesting to its validity.**

**Failure `BR-84`:** a criterion attested only by its author is `untested` and is never reported as validated. A guide shipping one is `unknown` per 16.3.

The documented failure is a work group subjectively confirming the validity of the criteria it had itself proposed. **That is TETHER 1.2 and POLARIS 5.3 arriving in the guide layer**, and both documents' rules apply without modification: the auditor is running on the audited hardware, and satisfaction attested by the party responsible for it is not measured.

---

## 17. What BEARING Never Does (neither)

### 17.1 The consolidating table

A consolidating section for a reader who arrived here intending to build a screening product. **Every row is a pointer to its normative home and never a second statement of it.**

| Refusal | Normative home |
|---|---|
| **R1** No diagnosis, condition name, category, pattern, profile, archetype, or code | 5.7 and 16.1 for this document; **16.3 for the guide layer, which 16.1 does not reach** |
| **R2** No deferral of clinical evaluation, and no ladder sequenced ahead of routing | B-A3, 7.3 |
| **R3** No entry into any register about the operator | 14.3 |
| **R4** No third party screening use, and it is unconfigurable | B-A5, 8.5, 14.4, 14.5 |
| **R5** Crisis routes immediately | Inherited absolute 3, section 8 |
| **R6** No risk score | B-A6 |
| **R7** No enumerated indication content | 16.1 for this document; **16.3 for the guide layer, which 16.1 does not reach** |
| **R8** No introspective question | 4.2, 9.3 |
| **R9** No compliance shaped signal | 4.3 |
| **R10** No gate, block, revocation, or price | B-A1, B-A4 |
| **R11** No cross operator comparison or aggregation | 11.3, 14.4, 14.5 |
| **R12** No agent closure, downgrade, or conclusion | 13.2 |
| **R13** No self description as an instrument | 17.2 |
| **R14** No characterization | B-A2, 5.7, 5.8 |
| **R15** No reward attached to recording, no undeclared prompt cadence, no lapse rendered as loss | QUEST section 9, 9.15, 10.6 |

### 17.2 No self description as an instrument

**Specification text, and any implementation's user facing text, MUST NOT claim that BEARING detects, screens, assesses, identifies, measures, predicts, diagnoses, or is validated, accurate, reliable, or clinically useful.**

**Failure `BR-85`:** such text is non conformant and MUST be removed before Status leaves Draft. An implementation shipping it is non conformant at every tier.

**Intended purpose is set by labelling, instructions, and promotional material.** This document's own prose therefore determines its character regardless of what any implementation does, which is why the requirement binds the specification first and the implementation second.

**The motivating phrase about early detection of deep level system faults correctly describes the motivation and MUST NOT appear in normative text.** It belongs in the design note. It is an accurate account of why the work was undertaken and an inaccurate account of what the resulting document does, and a specification that carried it would have described itself as a detection system in the one artifact that determines whether it is one.

---

## 18. Failure Classes (neither)

**This section carries `neither`.** It places requirements on this document's own text and on an implementation's conformance apparatus, and none on an operator's record. Per 3.4 and KIT 3.5, **a `neither` section does not inherit the coercive default and never resolves `out-of-scope`.** The heading previously carried a description of an inheritance rule rather than a label, which under the drafting requirement made it unlabelled and therefore coercive by default, which would have cascaded the clinical exclusion onto every failure class in the table below.

**Each row inherits the label of the section that governs it**, and that inheritance is what the heading previously tried to say. It is a statement about the rows and not about this section.

Each class is stated as what an implementation does when the requirement is violated. **Each fails closed, and none is satisfiable by an operator declining care.**

| # | Failure | Disposition |
|---|---|---|
| `BR-01` | A document outside BEARING cites, requires, or conditions a requirement on a BEARING element | Non conformant specification text, rejected in review. A gate citing one records `unevaluated`, never `passed` |
| `BR-02` | Protocol record missing a required field; an authored `routing_target`; a declared `interval` or `persistence` on a `crisis` protocol | Rejected at write time and not partially stored. The table value at 6.3 governs. An undeclared `routing_latency` reads `unknown-undeclared` and raises; an undeclared `cooling_period` takes POLARIS 11.2's thirty day default and raises |
| `BR-03` | A monitor requires, presents, or depends on a question, prompt, item, scale, anchor, rating, or inventory administered to the operator; reads a forbidden signal class; or declares an input carrying an `input_source` outside the closed enum of 4.1 | Rejected at write time and the protocol is not stored. A monitor discovered to depend on one is retired under 4.15 |
| `BR-04` | Monitor with no declared interval, or evaluated outside it | `unknown-undeclared` from declaration, or `unknown-stale`. Never reported as passing |
| `BR-05` | Raise on a single evaluation, or a discarded sub threshold observation. **This row does not reach a raise of type `crisis`**, which 4.5 exempts | The raise is void. The observation is restored and made available to the next evaluation. A `crisis` raise voided under this row is restored and routed, per `BR-89` |
| `BR-06` | A model determines that a monitor fired, did not fire, or that a raise may leave the open set | The monitor is rejected at write time. Raises already emitted from it are void |
| `BR-07` | No declared envelope, or a result outside the envelope reported as `no-trip` | `unknown-undeclared`, or corrected to `out-of-envelope`. Never a pass |
| `BR-08` | `no-trip` rendered as clear, healthy, aligned, fine, on track, compliant, or as an absence of concern | The rendering is void and the result is re rendered as its enumeration of inputs and window |
| `BR-09` | An unknown suppressed, batched away, or normalised; or a never ran monitor producing no raise | The suppression is void and the raise is emitted, with the true first missed interval recorded |
| `BR-10` | A run record written only on a trip | Non conformant. The register cannot distinguish a quiet period from a dead monitor |
| `BR-11` | Emission while absent from the protocol register; `never-ran` resolved against a clock BEARING writes; no declared liveness receiver; a monitor reading a BEARING produced signal other than its own run history | The emission is void. The affected monitors report `unknown-undeclared`. Non conformant at Tier 2 |
| `BR-12` | A band, threshold, interval, or window revised after a result it would have failed | The prior band governs that period, the revision is recorded with its cause under POLARIS 11.3, and the revision is enumerated as drift |
| `BR-13` | Undeclared budget for one of the four budgetable raise types; a raise suppressed to fit one; a declared budget for the `crisis` or `instrument` lane | `unknown-undeclared` on that type and a raise. The suppression is void and the raise is restored. A declared budget for either unbudgeted lane is rejected at write time and not stored, and applying one is non conformant at every tier |
| `BR-14` | A monitor with no defined recipient action retuned rather than retired; a raise closed on the strength of its monitor's retirement | The retune is void and the monitor is retired with the retirement recorded. **Its outstanding raises remain `open`, continue to route under 6.3 on their existing targets, and leave the open set only by `routed` or `expired`.** A closure written on retirement is void and the raise is restored to `open` |
| `BR-15` | A raise carrying a field outside the closed schema, including `cause` or `effect` per 5.2, or missing one required for its type | Rejected at write time. The field is not stored |
| `BR-16` | A raise emitted without per signal reference sources | Rejected at write time |
| `BR-17` | A `self-report-only` raise suppressed, downgraded, or delayed | The suppression is void and the raise is routed, carrying its label |
| `BR-18` | A raise withheld because an input was recorded `unknown` under KIT 6.3 | The withholding is void, the raise is restored, and a `monitor` raise names the item and its calibration state |
| `BR-19` | A derived quantity outside the three permitted at 5.6 | Rejected at write time and void where written. A scalar summary resolves `undefined`. A cross operator comparison resolves `incomparable`, and consent does not enable it |
| `BR-20` | A forbidden field name, or a functional equivalent under another name | Rejected at write time and not stored. Defining text is non conformant |
| `BR-21` | Implementation authored, templated, generated, or interpolated natural language in a raise | The string is void and the raise is re rendered from its fields. A renderer holding such templates is non conformant on inspection |
| `BR-22` | A forbidden state name in any register | Non conformant text, rejected in review, per KIT 2.11 |
| `BR-23` | A fourth lifecycle value, or a transition to a state meaning resolved, cleared, ruled out, dismissed, or unnecessary | Non conformant specification text. The transition is void and the raise is restored to `open` |
| `BR-24` | A raise with no declared expiry, or declared `indefinite`; an expired raise cited as current or aggregated into a series | Rejected at write time, or expired at emission. The citation is void as grounds and the decision is re resolved |
| `BR-25` | Raises ordered by a computed magnitude | The ordering is void and the list is re presented by `raised_at` or by the operator's declared order |
| `BR-26` | A raise with zero or two types; a trip condition met with no raise emitted | Rejected at write time. The second is a health invariant failure |
| `BR-27` | A raise with no named human `owner`; an unrouted raise past its emitting protocol's declared `routing_latency` producing no `monitor` raise | Rejected at write time. The second is a health invariant failure |
| `BR-28` | An `instrument` raise withheld for want of a declared qualified human | The withholding is void. The raise routes to the operator with the target recorded missing, and the missing target is simultaneously a `conformance` raise |
| `BR-29` | A ladder rung with no recorded finding | The raise is marked `ladder-incomplete`, which does not delay its routing |
| `BR-30` | A routing record carrying a ladder dependency field; an implementation that will not route until the ladder is complete | Rejected at write time. Non conformant at every tier, and the withheld routing is performed |
| `BR-31` | A closure written on the strength of a ladder finding | Void. The raise is restored to `open` |
| `BR-32` | Ladder findings filed on a channel separate from the referral; a rung 2 finding transmitted without its attribution test result label, or transmitted as an inventory or loadout summary | Non conformant format. The findings are re transmitted with a corrected referral. A rung 2 finding cited as evidence of an instrument fault is rejected on KIT 10.1's terms and the citation is void as grounds |
| `BR-33` | BEARING text defining a rung, crisis criterion, crisis path, or escalation condition | Non conformant specification text, rejected in review |
| `BR-34` | A non crisis crossing with no declared custody floor; a crisis crossing refused or delayed for want of one | The first is refused and recorded. The second is non conformant at every tier, the refusal is void, the crossing proceeds under 8.5's interim floor `human-recipient-undeclared`, and the absent floor is a separate raise |
| `BR-35` | Review record missing a required field, or closed with an undispositioned item | Rejected at write time, or recorded `incomplete`. Does not satisfy the interval and leaves the calibration state unchanged |
| `BR-36` | A review citing a declaration version adopted after the period began | Rejected at write time. Where no declaration was held, drift items report `undefined`, never zero and never aligned |
| `BR-37` | A docket item that is a question about the operator's internal state, or a prompted form for a stated cause | Rejected at write time and not stored. The prompt is void |
| `BR-38` | A `crisis` or `instrument` raise docketed, deferred, dispositioned, or delayed by a review | The docket entry is void and routing is performed immediately |
| `BR-39` | A disposition citing no docket hash or a mismatched one; a mutated frozen docket | Rejected at write time. The mutation is void and the review is recorded `incomplete` |
| `BR-40` | An item with no disposition, or a sixth disposition value | The review is `incomplete`. A sixth value is non conformant specification text |
| `BR-41` | `accepted` costing more fields, confirmations, or authority than another disposition, or creating a follow up another does not | The excess is void. Re surfacing an item solely because it was accepted is non conformant and the re surfacing is void |
| `BR-42` | A disputed count altered or suppressed | Non conformant. The count is restored from the frozen docket and the dispute is retained beside it |
| `BR-43` | A re raised disputed count suppressed, downgraded, or auto dispositioned | The suppression is void and the raise is presented with its prior dispute attached |
| `BR-44` | A repeatedly disputed monitor automatically removed, disabled, retuned, widened, or narrowed; or the enumeration rendered as a count | The revision is void and the prior definition stands. The count is void and the list is returned in its place |
| `BR-45` | A **POLARIS declared element** amended in the review that received a raise measured against it, or inside the cooling period | `PL-12` at every tier, whether or not machinery existed to block it. The prior value governs |
| `BR-46` | `confirmed` reported as lesser, incomplete, deferred, provisional, or pending | The rendering is void and the outcome is re rendered as complete |
| `BR-47` | A `revised` or `re-declared` outcome with no POLARIS amendment record | Non conformant, **and the element is unchanged** |
| `BR-48` | A review closed by a party other than the operator; an agent authored, pre filled, or defaulted disposition; agent ranking of docket items | Not a review, and the closure is void. The disposition is void and the item reverts to undispositioned |
| `BR-49` | A prior review overwritten, deleted, decremented, or reversed; a missed period rendered as a loss | The write is rejected. The rendering is corrected to the state 10.4 defines |
| `BR-50` | A formal review recorded inside the declared minimum interval; informal check ins recorded into a register; a record of rejected review attempts written or read as a monitor input | Rejected at write time and not stored; the prior interval governs, and the rejection is returned to the operator at the moment of the attempt. Recorded check ins and rejected attempt records are deleted rather than retained, the last under `BR-03` |
| `BR-51` | A gate, capability, or authority citing a review record | Records `unevaluated`, never `passed`, and is re resolved on its actual grounds |
| `BR-52` | A measure, marker, score, or judgement of whether a review was owned | Non conformant at every tier. The value is void and defining text is rejected in review |
| `BR-53` | `unsigned`, `incomplete`, or `undifferentiated` treated as a failing check or a blocking condition | The check is void and the reading stands as a reading |
| `BR-54` | A calibration state outside the three values, or `lapsed` rendered as failed or overdue | Non conformant. The rendering is void and re rendered |
| `BR-55` | A conformance check satisfiable only by holding a current alignment calibration | Malformed specification text, rejected in review. Any consequence it imposed is void |
| `BR-56` | Monitors stopped, or raises discarded, expired early, collapsed, summarized, or deduplicated, because a review lapsed; a repeating or escalating lapse prompt | Non conformant. Raises are restored where recoverable. The prompt is refused and none is issued |
| `BR-57` | A value spanning two or more positions, or a cross tabulation of pillars against dimensions | Rejected at write time and void where written |
| `BR-58` | An exposed argmin magnitude, distance, ordering, runner up, or tiebreak; an argmin computed across positions with no single declared ordinal scale and origin pole | Void. The pointer, or the unordered tied set, is returned alone. Without a declared scale the argmin resolves `undefined`, never zero and never a computed value |
| `BR-59` | A cross operator placement comparison | Resolves `incomparable`, never equal and never an ordering. Consent does not enable it |
| `BR-60` | A machine authored, altered, inferred, pre populated, pre selected, defaulted, or proposed placement | Void. The prior placement stands. `unplaced` is never read as centred or neutral |
| `BR-61` | `unchanged-uncaused` reported as a pass, a fail, an evasion, a defect, or a concern | The rendering is void and the state is re rendered as its name and its three conditions |
| `BR-62` | A refusal test satisfied by the refusal's own report of itself; a refusal with no declared seed or an unexercisable path; a `not-blocked` result | The self report does not satisfy the test. `untested` reports `unknown-undeclared` and raises, never a pass. `not-blocked` is a `conformance` raise and the declaration has no such value until fixed |
| `BR-63` | An obligation reading `met` on self report alone; a blocking implementation | Corrected to `unmeasured` rather than annotated. The block is void and the implementation is non conformant |
| `BR-64` | A drift count exposed outside the one permitted category; an undeclared period, category, or amendment record | A mislabelled aggregate, refused on QUEST 3.3's terms with the enumeration returned in its place. Otherwise `unknown-undeclared`, never a pass |
| `BR-65` | BEARING text defining a second quest scoped drift check | Non conformant specification text, rejected in review |
| `BR-66` | An inferred, defaulted, or reconstructed priority set; record assigned to a default; a `declaration-review` raise asserting drift rather than reporting composition | Rejected at write time and the monitor reports `unknown-undeclared`. The assignment is rejected and the record is retained `unattributed`. The assertion is void and the raise is re rendered from its fields |
| `BR-67` | A monitor treating a rule conformance count as evidence of alignment | Non conformant, and its raises are void |
| `BR-68` | An agent closing, terminating, suppressing, delaying, extending, narrowing, downgrading, ranking, attributing, scoring, predicting, or concluding | Rejected at write time. The prior value stands, and the rejected attempt is recorded and is itself a `monitor` raise |
| `BR-69` | An agent running a standing evaluation with no current, scoped, expiring CONFIDE authorization | Every affected monitor reports `unknown-unauthorized`, which is a raise. Outputs produced without authorization are deleted rather than retained |
| `BR-70` | An agent identity modifying an A0 monitor definition granting its own authority | Rejected. The prior definition stands and the attempt is recorded as a `monitor` raise |
| `BR-71` | A BEARING register declared; a review embedding raise content | Non conformant specification text. The embedding is rejected at write time and re written as citations |
| `BR-72` | Any value derived from a BEARING element written to, mirrored into, or cited as the operator register, or adopted into the instrument, fault, inventory, or capability registers | Rejected at write time on the TETHER F1 pattern. A decision citing it is re resolved on its actual grounds |
| `BR-73` | A raise used as a key for aggregation, filtering, cohorting, or comparison across operators | The query, index, or export is refused and the refusal is recorded |
| `BR-74` | An interface result containing more than one distinct subject identity, or one that cannot be resolved to exactly one | Refused in full, never truncated to one. The refusal is recorded |
| `BR-75` | A BEARING count, raise, placement, or review consumed by a gate, scheduler, prioritizer, planner, recommender, ranking, or scoring system | The consuming system is non conformant, the input is void, and the decision is re resolved on its actual grounds |
| `BR-76` | Absent, stale, or withheld monitor reliability statistics; a published raise rate or any figure whose denominator is the operator's records | The monitor is `unknown-stale`, which is a raise. The withholding is void. A raise rate is a mislabelled aggregate under `BR-19`, is refused on QUEST 3.3's terms, and the enumeration of 15.1 is returned in its place |
| `BR-77` | A reported figure published without its observation regime | Non conformant. Republished with the regime, or withdrawn |
| `BR-78` | The functional impact gate presented as a solved guard; or satisfied by inquiry | Non conformant text, corrected before Status leaves Draft. The inquiry satisfied element is rejected at write time |
| `BR-79` | A baseline comparator drawn from a population norm, cohort, target, or specification supplied value | Void. The raise is re rendered with the comparison omitted and the omission recorded |
| `BR-80` | A self test with no declared interval, or past it | Red check, reported `unevaluated`, never as passing. An implementation that cannot run it does not conform at any tier |
| `BR-81` | Enumerated criteria content, described experience, item, scale, anchor, cut point, quantity, condition name, category, pattern, profile, or archetype **in this document** | Non conformant text, rejected in review, in the disposition HABITAT absolute 2 applies to a stated quantity. **The guide layer is reached by `BR-88` and not by this row** |
| `BR-82` | A guide missing a required declaration, or past its review interval | The guide is `unknown` and is itself a raise. Every monitor citing it reports `unknown-undeclared` and is never reported as passing |
| `BR-83` | An undisclosed interest in the routing target; the referral destination and the criteria author being the same commercial entity | The guide is `unknown` until disclosed or removed. The coincidence is a conformance failure and a red check regardless of disclosure |
| `BR-84` | A criterion attested only by its own author | `untested`, never reported as validated. A guide shipping one is `unknown` |
| `BR-85` | Specification or implementation text claiming BEARING detects, screens, assesses, identifies, measures, predicts, diagnoses, or is validated, accurate, reliable, or clinically useful | Non conformant text, removed before Status leaves Draft. An implementation shipping it is non conformant at every tier |
| `BR-86` | A declaration missing a field required by 2.5's field table | `unknown-undeclared` on that field from the moment of declaration, and a `conformance` raise naming the missing field. **The declaration is not rejected and is not partially voided**, per B-A4. `position_set` is optional and its absence is not a missing field |
| `BR-87` | A MUST NOT suspended, a write time rejection not fired, or a coercive check reported as a pass or a fail rather than `out-of-scope`, on the strength of a record's clinical direction | The suspension is void, the rejection is performed, and the result is corrected to `out-of-scope` with the `monitor` raise `reason: clinically-excluded` emitted |
| `BR-88` | A guide containing prohibited content, naming a condition, or presenting itself as a screening instrument, diagnostic aid, assessment, inventory, or validated measure | The guide is `unknown` on `BR-82`'s terms. **Every monitor citing it reports `unknown-undeclared` and is never reported as passing**, and raises already emitted from a citing monitor are void |
| `BR-89` | A `crisis` raise delayed, batched, laddered, budgeted, queued, deduplicated, or conditioned on the operator's self assessment or an agent's judgement; a `crisis` monitor declaring or evaluating only on an interval | **Non conformant at every tier. The delay is void and the raise is routed.** A `crisis` raise voided under 4.5 or `BR-05` is restored and routed |
| `BR-90` | No escalation path declared under TETHER section 9 | The raise routes to the declared `second_party`, or to the operator with the target recorded missing where none is declared, the routing is recorded, and the absent declaration is simultaneously a `conformance` raise. **The raise is delivered in every branch** |
| `BR-91` | An operator facing interface that does not surface the declared escalation path and the declared qualified human at the point of use, or that places either in a footer, a collapsed panel, a settings page, or behind a further action | **Non conformant at every tier**, on the same terms as a relocated front matter statement. Where neither is declared, the interface surfaces that fact rather than nothing |
| `BR-92` | A crossing with no declared comparison floor; a recipient's request that the floor be relaxed | The non crisis crossing is refused and the refusal is recorded. The request is refused and the refusal is recorded. Transmitting with a custody floor and no comparison floor is non conformant at every tier |
| `BR-93` | A **monitor** threshold, window, persistence rule, interval, or acceptance band revised in the review that dispositioned a raise from it, or inside that monitor's `cooling_period` | Non conformant at every tier. The prior value governs, and the revision is enumerated in BEARING's own drift enumeration under 12.3. **It is not `PL-12` and MUST NOT be reported as one** |
| `BR-94` | A run result determined by an agent's output | The result reads `unknown-unauthorized` and is itself a `monitor` raise with `reason: agent-determined-run`. It is never reported as `no-trip` and never as a pass, and the monitor is rejected at write time under `BR-06` |

---
## 19. Conformance (neither)

**This section carries `neither`.** It places requirements on an implementation's conformance apparatus and none on an operator's record. Per 3.4 and KIT 3.5, **a `neither` section does not inherit the coercive default and never resolves `out-of-scope`**, because there is no operator record for a tier item or an invariant to resolve against.

**The composition note the heading previously carried moves here, where it is a statement about subsections rather than a label.** 19.1's tiers and 19.2's invariants each place requirements on an implementation and on this document's own text. 19.3 is protective by construction, because every check in it seeds a condition and asserts a refusal or a detection, and a refusal asserted is never a reduction. **None of the three, under inherited absolute 4, may contain an item an operator could satisfy by declining care or by consuming less on clinically directed care.**

### 19.1 Three tiers, mirroring the family

Requirements are **indicative in this draft**, on the pattern the sibling documents use.

**Tier 1, Attended.** Monitor definitions exist and carry every required field. Run records are written on every evaluation. Raises carry the closed schema and no field outside it. Reviews carry their required fields, a disposition per docket item, a declaration outcome, and the operator's signature. A review interval and a minimum interval are both declared. The crisis routing target is the TETHER section 9 path.

A Tier 1 implementation may run no monitor on any clock and hold no seeded refusal test. What it may not do is hold a raise that carries an interpretation, or a review nobody signed.

**Tier 2, Referenced.** Adds the clocks and the evidence discipline. Monitors run on declared intervals, with acceptance bands published in advance. Every unknown raises. The protocol register and the liveness token are live, and `never-ran` resolves against a clock BEARING does not write. The docket freeze is hash enforced. The monitor cooling rule binds. The three POLARIS mechanisms of section 12 run, and the seeded refusal test executes on its declared interval.

**Tier 3, Governed.** Adds the boundary and the parties other than the operator. Crossings are governed under the CONFIDE and SPEAK operator adapters with declared custody floors. Post crossing retention is enumerated under the RETAIN adapter with a declared end of engagement disposition. The qualified human routing target is declared, current, and **its named parties are aware they are named**, on TETHER section 9's model. Every guide cited by a monitor carries current declarations and is inside its review interval. Every agent authorization in force is current, scoped, and expiring.

**No family level or BEARING level conformance badge, maturity ladder, or composite is defined.** The family's existing ground applies without modification: a badge would be the first place a vendor put one, and it would immediately be read as a value summarizing an operator rather than an implementation.

### 19.2 Health invariants

Each is a count of defects, or an enumeration of them where a count would reward suppression, and each is labelled a conformance check, per QUEST 3.3's first carve out. **Every one of them has a monitor, an implementation, or a defective record as its subject, and none has the operator's well formed records as its denominator**, per 5.6's discriminator.

**Two rows were replaced because they were satisfiable by withholding the raise**, which rebuilt the failure 7.3 exists to prevent one layer below where 7.3 reaches. An invariant reading zero `instrument` raises with fewer than four ladder findings is reached most cheaply by not emitting the `instrument` raises whose ladders are incomplete, and `BR-29` declares exactly that object conformant while 7.3 makes withholding non conformant at every tier. An invariant reading zero raises routed later than their ladder was worked is trivially satisfied by never working the ladder, reads as pressure to complete the ladder before routing rather than concurrently, and is measurable only by a join `BR-30` forbids the routing record to support. **The replacements make incompleteness visible without rewarding suppression, resolve against the routing record alone, and add a third row counting the suppression itself.**

| Invariant | Target |
|---|---|
| BEARING derived values appearing in any register about the operator | Zero |
| Declared monitors with no run record inside their declared interval | Zero |
| Results reading `no-trip` with a missing, stale, or out of envelope input | Zero |
| Raises carrying a field outside the closed schema, or a forbidden field name | Zero |
| Raises carrying implementation authored natural language | Zero |
| `instrument` raises whose four ladder findings were not recorded inside the emitting protocol's declared `ladder_latency` | **Reported as an enumeration of named raises with their missing rungs, never as a count** |
| `instrument` raises with a `routed_at` later than their emitting protocol's declared `routing_latency` | Zero. **Resolved against the routing record alone**, per 7.3 |
| `instrument` raises withheld pending ladder completion | Zero |
| `crisis` raises emitted later than the write of the record they carry | Zero |
| Run results whose determining party was an agent | Zero |
| Elements any section requires a raise to carry that have no column in 5.1's closed schema | Zero |
| Coercive checks resolved `out-of-scope` with no exclusion notice emitted, or absent from the review's exclusion report | Zero |
| Declared refusals with no seed, or with no recorded result inside their interval | Zero |
| Obligations reading `met` on self report alone | Zero |
| Liveness tokens not received inside their declared interval | Zero |
| Agent authorizations in force that are absent, expired, or unscoped | Zero |
| Raises closed by an agent | Zero |
| Reviews closed by a party other than the operator | Zero |
| Dispositions citing a mismatched or absent docket hash | Zero |
| Trip conditions met with no raise emitted | Zero |
| Raises with no named human owner | Zero |
| Expired unrouted raises not re emitted at the next evaluation | Zero |
| Amendments of a **POLARIS declared element** made inside a declared cooling period | Zero, and any nonzero value is a POLARIS 11.5 conformance failure. **The count ranges over POLARIS declared elements alone**, per 9.11 and 12.3 |
| Monitor revisions made inside a monitor's `cooling_period` | Reported in BEARING's own drift enumeration under 12.3, never as a count and never as `PL-12` |
| Interfaces returning more than one distinct subject identity | Zero |
| Coercive checks resolved against clinically directed records as a pass or a fail rather than `out-of-scope` | Zero |
| Records with an absent or `unknown` clinical direction field treated as non clinical | Zero |
| Monitors citing a guide that is past its review interval, reported as passing | Zero |
| Disputed counts altered or suppressed | Zero |
| Unknowns suppressed, batched away, or normalised | Zero |
| Repeatedly disputed monitors | Reported as an enumeration with their stated grounds, never as a count |
| Unattributed record over an alignment monitor's window | Reported as an enumeration of named records, never as a ratio |
| POLARIS 11.5 drift categories | Reported as enumerations of named amendment records with their causes, never as counts |

### 19.3 Self test

**One page. At most twelve checks. Each carries a named failure class, each is mechanically decidable, each fails closed, and none is satisfiable by an operator declining care or by consuming less on clinically directed care.**

**It is executed on its own declared interval**, per 15.5, and **a stale result is reported `unevaluated` and is never reported as passing.** An implementation that cannot run it does not conform at any tier. Each check seeds the condition and asserts the refusal or the detection, and each exits non zero on failure.

1. **A raise offered with a `severity` field, and separately with a field named `confidence`.** Assert both are rejected at write time and neither is stored. Failure: `BR-15`, `BR-20`.
2. **A raise offered with an implementation authored sentence in place of a field label.** Assert the string is void and the raise is re rendered from its fields. Failure: `BR-21`.
3. **An `instrument` raise whose ladder is incomplete, and separately one whose environment rung returned `out-of-spec`.** Assert both were routed, assert the routing record carries no field referencing the ladder, and assert neither was closed on the strength of a finding. Failure: `BR-30`, `BR-31`.
4. **A `crisis` raise emitted with no declared custody floor, separately one emitted on the write of a record inside a period during which no interval elapsed, and separately one whose monitor declared a persistence requirement.** Assert the first routed immediately, was recorded under 8.5's interim floor with the absent floor raised separately, and consulted no self assessment. Assert the second was emitted at the write and not at the next interval. Assert the third protocol was rejected at write time and not stored. Assert none of the three entered the ladder. Failure: `BR-34`, `BR-89`, `BR-02`.
5. **A monitor with no declared interval, and separately one with no run record inside its interval.** Assert the first reads `unknown-undeclared` from declaration, assert the second emits `reason: never-ran` with its true first missed interval, and assert neither is reported as passing. Failure: `BR-04`, `BR-09`.
6. **A run with a missing input reported as `no-trip`, and separately a `no-trip` result rendered as no concern.** Assert the first is corrected to `unknown-no-data` and raises, and assert the second is re rendered as its enumeration of inputs read and window covered. Failure: `BR-07`, `BR-08`.
7. **A review closed with one item undispositioned, one closed by an agent, and one whose disposition cites a stale docket hash.** Assert the first is `incomplete` and does not satisfy the interval, assert the second is not a review and the closure is void, and assert the third is rejected at write time. Failure: `BR-35`, `BR-48`, `BR-39`.
8. **An `accepted` disposition offered a second confirmation dialog, an extra mandatory field, and a follow up flag that no other disposition creates.** Assert all three are void, and assert the item is not re surfaced in the following review solely because it was accepted. Failure: `BR-41`.
9. **A declared refusal whose seed is submitted and not blocked, and separately a refusal reporting itself enabled with no seed.** Assert the first is a `conformance` raise and that the declaration has no such value until fixed, and assert the second reads `untested` and is never reported as a pass. Failure: `BR-62`.
10. **A scalar summary requested over the register, a comparison between two operators offered with the consent of both, and a placement written by an agent.** Assert `undefined`, assert `incomparable`, and assert the placement is void with the prior placement standing. Failure: `BR-19`, `BR-59`, `BR-60`.
11. **A protocol offered with an input whose declared source is a record of the operator's engagement with BEARING, and separately one whose `input_source` is a string outside the closed enum of 4.1.** Assert both are rejected at write time, assert neither protocol is stored, and assert no monitor was created in either case. Failure: `BR-03`.
12. **The specification text itself, over its own top level headings.** Assert that every top level numbered heading carries at least one of the three literal strings `coercive`, `protective`, or `neither`; assert that where a heading carries more than one, each is bound in that heading to an explicitly enumerated subsection range; and assert that no heading carries a description of a label, an inheritance rule, or a composition note in place of a label. Failure: the drafting requirement's disposition, which is that an unlabelled top level section is treated as coercive. **This check exists because it is the class of error a script catches and a reader does not**, and because an unlabelled section 18 or 19 would cascade 3.4's clinical exclusion onto this document's entire conformance apparatus.

Checks 5, 8, and 9 require elapsed time and accumulated windows. **A simulated clock is conformant, per DEFER 15.4, provided the implementation under test reads time only through the source the simulation controls.** A test that advances a clock the production code does not read has tested a different system, and its pass is not evidence. Check 5's second half additionally requires that the simulated clock be the **external** source of 4.12, since a `never-ran` computation resolving against BEARING's own clock is itself the failure.

---

## 20. Versioning and Governance (neither)

Semantic versioning on the specification, per `CONTRIBUTING.md`. Substantive changes go through an RFC.

While Status reads Draft, section numbering, requirement identifiers, and failure class codes are unstable and MUST NOT be cited as stable by any other document in this stack.

**The permitted citation direction is fixed by B-A1 and does not move with the numbers: BEARING cites the family, and the family does not cite BEARING.** An RFC proposing that any document in this stack cite a BEARING element is an RFC against B-A1 and is evaluated as one, at the tier B-A1 occupies, which is absolute and admits no configuration.

Two changes are already anticipated and are recorded here so that they are not mistaken for drift when they arrive. **First**, when the RFC named in QUEST 1.2 lands and generalizes the identity firewall from an enumerated register list to any register holding a record about the instrument, its equipment, or its capabilities, **14.3 is subsumed and removed** rather than kept as a second copy. **Second**, when the four operator adapters named in the forward citation notice land, the obligations BEARING routes to them are refined rather than replaced, and **BEARING gains no rule of its own** from any of them.

---

## Annex A. Worked example, non normative, quarantined tier

**This annex is non normative and is structurally separated from every requirement in this document. The separation is the disclaimer.**

**What follows illustrates the FORM of a raise. It is explicitly not a validated instrument, not a criteria set, and not an example of what any monitor should read for.** Readers extract examples far more readily than they extract caveats, which is why this material lives in a tier whose location says what it is, rather than in a section with a warning attached.

All content below is placeholder. It names nothing, contains no indication content, no criteria, no threshold value, and **no reproduced item content from any published instrument.**

### A.1 One well formed raise

```
id:                  raise-0000
raised_at:           <timestamp>
protocol_id:         protocol-0000
run_id:              run-0000
subject:             operator-0000
owner:               <named human>
type:                declaration-review
criteria:            declaration-0000#priority-a
condition:           [ record-0001 @ <timestamp> (self-report),
                       record-0002 @ <timestamp> (second-party),
                       record-0003 @ <timestamp> (instrument) ]
fired_signals:       [ signal-a (self-report, obs-0001),
                       signal-b (second-party, obs-0002) ]
evidence_label:      mixed-source
window:              <declared window>
persistence_observed: [ eval-0007 @ <timestamp>,
                        eval-0008 @ <timestamp> ]
provisional:         false
lifecycle:           open
routed_at:           <null>
expiry:              <declared expiry>
artifact_class:      A2
custody_class:       <declared>
clinical_direction:  unconfirmed
```

**What makes it well formed.** Every field is in the closed schema of 5.1 and none is outside it. Every fired signal carries a reference source, per 5.3. `subject` names the identity holding the declaration and matches the signing identity, per B-A5. `owner` names a human, per 6.4. `criteria` cites a declared element rather than describing one. `condition` enumerates observed records with timestamps and sources rather than summarizing them. `evidence_label` reads `mixed-source` because not every fired signal is `self-report`, and it is computed from `fired_signals[]` rather than authored, per 5.1. `persistence_observed` is an enumeration of the evaluations at which the trip condition was met, not a ratio, and its cardinality is a working value that is never displayed, stored, or transmitted. `expiry` is declared and is not `indefinite`. `clinical_direction` reads `unconfirmed`, which is one of the three values 3.4 permits and which means the record is handled as clinically directed until the operator declares otherwise. There is no cause field and no effect field, per 5.2. There is no severity, no score, no message, and no note, because 5.1 provides nowhere to put one.

**`reference source: instrument` in the third `condition` entry names a reading a device produced**, which is the TETHER 2.3 vocabulary value KIT 1.5 excepts by name and which 1.9 carries across. It is not the raise type `instrument`, and this raise's type is `declaration-review`.

**No `duration`, `functional_impact`, `baseline_comparator`, `ladder_findings[]`, or `ladder_state` appears**, because all five apply to type `instrument` only and 5.1's applies-to column governs.

**What its renderer may emit.** Field labels, record identifiers, timestamps, and text quoted verbatim from the operator's own declaration with its source cited. Nothing else, per 5.8.

### A.2 One malformed raise

```
id:                  raise-0001
raised_at:           <timestamp>
protocol_id:         protocol-0001
run_id:              run-0001
type:                declaration-review
severity:            moderate
criteria:            declaration-0001#priority-b
condition:           "the period trended away from the declared priority"
fired_signals:       [ signal-c, signal-d ]
cause:               "reduced engagement"
message:             "You have drifted. Consider revisiting your priorities."
lifecycle:           resolved
expiry:              indefinite
```

**Seven defects, each with its failure class.**

`severity` is a field outside the closed schema and a forbidden field name (`BR-15`, `BR-20`). `condition` is a summary sentence rather than an enumeration of observed records, and it is implementation authored prose (`BR-21`). `fired_signals` carry no reference sources (`BR-16`). `cause` is a field 5.2 forbids and is a field outside the closed schema of 5.1, so it is rejected at write time and is not stored (`BR-15`). `message` is authored prose, is a forbidden field name, and characterizes, advises, and addresses the operator in the second person (`BR-20`, `BR-21`, and B-A2). `lifecycle: resolved` is a value 5.10 forbids any identity to write (`BR-23`). `expiry: indefinite` is refused outright (`BR-24`).

The seventh defect is the one worth naming last, because it is the only one that is not a field error. **The raise concluded.** It stated that drift occurred, which under 12.5 only the operator who owns the declaration may state, and it recommended an action, which nothing in this document may ever do. **The type name itself no longer states it**, which is why 6.1's type is `declaration-review` rather than `drift`: the earlier name put the conclusion in the routing field of every conformant raise, including the well formed one above.

**Both examples are missing fields the closed schema requires**, which is a defect of the illustration and not of the schema: an implementation writing either as shown would have the missing fields rejected under `BR-15` on the same terms as the fields shown. A.1 carries the full set; A.2 is truncated to the defects it is illustrating.

---
