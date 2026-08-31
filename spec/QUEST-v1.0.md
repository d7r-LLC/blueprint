# QUEST: Quests, Unlocks, Evidence, Skills, Termination

## Version 1.0

**Specification:** QUEST/1.0
**Status:** Draft, structural. Sections 1 through 13 are written. Three bindings are forward citations into documents that are themselves incomplete and are marked as such in the text: TETHER section 5.4, which owns the periodic re referencing rule this document inherits rather than restates; the SPEAK and CONFIDE operator adapters, which own the crossing referred to in section 9; and the RFC named in section 1.2, which is drafted and not applied.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**License:** Apache 2.0
**Requires:** TETHER/1.0 for operator, instrument, register, and reference source vocabulary, for the shifted consequence ladder, and for the identity firewall. KIT/1.0 for the budget object and the shape of a bound (KIT 8.2), the item vocabulary, the substitute and amplify distinction, the item departure dispositions of KIT 5.2, the calibration currency rules of KIT section 6, and the coercive and protective split of KIT 3.5. POLARIS/1.0 for the motto rule, one way precedence, the dead refusal problem, the total ordering discipline, PL-15, and the travelling refusal floor of POLARIS 12.1. DEFER/1.0 for meters, the meter declaration of DEFER 5.4, the monotonicity discriminator of DEFER 5.4, the three timeout dispositions, and the refusal to reduce a bounded region to a scalar. TRACE/1.0 for the adopt or expire rule. SPEAK/1.0, CONFIDE/1.0, and RETAIN/1.0 for the crossing routed under section 9.
**Design note:** `design/0005-meat-suit-interface.md`, non normative.

---

> **Status note.** This document is a structural draft published for review of its shape, not of its requirements. An implementation MUST NOT claim QUEST conformance while this Status reads Draft. Requirement numbering, failure class codes, and the alias table are unstable. A cross specification citation into QUEST is a citation into a moving document.

---

## Abstract

QUEST specifies the form of an operator's capabilities and objectives: how a capability is declared, verified, lapses, and is abandoned; what a quest is, what bounds one, and how drift away from a declared objective is detected. The expansion is Quests, Unlocks, Evidence, Skills, Termination, which are the five things the document governs, in the order it governs them.

The refusals come first, because they are the document.

QUEST supplies no capability, no graph, and no objective. It computes no level, no rank, no score, no percentile, and no comparison between two operators. It never authorizes an act and it never blocks one. Two conformant operators may hold contradictory graphs, and QUEST ranks neither. Nothing in this document opens a gate, and nothing in it closes a door.

Two words are refused deliberately, and the refusals are load bearing rather than stylistic. **Experience** is refused, because an accumulating number is the single mechanic this document exists to prevent, and **Evidence** takes its slot: a node's state is settled by evidence of exercise and never by accumulated points. **Tree** is refused, because a tree has a root, a root gives depth, depth is a number, and a number is a level reached by an adversary who was denied a scalar field. The normative structure is a prerequisite graph. "Skill tree" survives as a teaching alias in section 10, where it does no harm.

The harm this document exists to prevent is one specific merge. TETHER section 4 forbids an instrument derived record from being written into the operator register, and names the severest case as a person receiving a finding as a description of who they are. That is the merge arriving from the fault register: *I am my deficits*. A progression score is the same merge arriving from the opposite direction: *I am my accomplishments*. Both install a record about the instrument as an identity. The second is the more dangerous of the two, because a person resists adopting a fault and volunteers to adopt a score, and because it arrives wearing the vocabulary of self improvement rather than the vocabulary of illness.

QUEST is written in game vocabulary because that vocabulary compresses well and is already how many operators narrate their own work. Section 10 governs it: some game terms are normative defined terms, some are refused outright, and some are motto class devices under POLARIS 7.3, kept because compression aids recall and forbidden as grounds for any decision. The document's own name is in the third category, and section 1.5 says so.

---

## Conformance

RFC 2119 keywords apply as described in that document.

### Inherited absolutes

TETHER's four absolute requirements are **inherited unchanged** and are NOT restated here. Each is named in one line, and the named document governs its text.

1. **Clinical precedence.** Inherited unchanged from TETHER absolute requirement 1.
2. **The identity firewall.** Inherited unchanged from TETHER absolute requirement 2, with the reach question treated in section 1.2 and left to the RFC named there.
3. **Escalation is not self gated.** Inherited unchanged from TETHER absolute requirement 3. Q-A3 adds only the prohibition on defining a QUEST element that substitutes for, gates, delays, or conditions the escalation path.
4. **No conformance requirement may be satisfied by declining care.** Inherited unchanged from TETHER absolute requirement 4. It binds every tier item, health invariant, and self test check in section 12, and section 7.3 is derived from it.

The fail closed naming convention binding on this document family is inherited from KIT section 2 by citation and is not restated: every fail closed state name names what is missing and never a deficiency in the operator.

### New absolutes

Three requirements are introduced by this document and admit no configuration. Each carries an explicit statement of what it does not forbid, because TETHER 4.3 established that an absolute stated without its boundaries is read into absurdity by the first reader who wants to argue with it.

**Q-A1. No monotone scalar, and no total order over operators.**

QUEST MUST NOT define, and an implementation MUST NOT compute, store, expose, or transmit, a level, rank, tier, grade, score, index, percentile, or point total over an operator, a capability record, a graph, or a set of quest records. Capability MUST be represented only as the partial order induced by the declared prerequisite relation. Progression state MUST be held per node, MUST be reversible, and MUST be scoped to exactly one declared graph. An aggregate spanning nodes, spanning graphs, or comparing operators is malformed and MUST be rejected at write time. Consent from any party MUST NOT enable a comparison.

**Failure:** a request for a scalar summary resolves `undefined`, never zero and never a computed value. A cross operator comparison resolves `incomparable`, never equal and never an ordering. An implementation exposing any such value is non conformant at every tier. A scalar already written is marked withdrawn rather than deleted, per POLARIS PL-15, and MUST NOT be cited thereafter.

**The adoption route is closed upstream, where both siblings can cite one rule.** A derived number whose subject is the operator's capability, or the operator and kit composite, rather than a measured property of the instrument, MUST NOT be adopted as an observation, under the rule owned by the **TRACE for operators adapter**. Q-A1's own subject is a number over an operator, KIT 9.2's adoption door has no scalar filter, and K-A3 forbids KIT from citing Q-A1, so a vendor readiness score, fitness age, or recovery index would otherwise arrive as instrument telemetry through the sibling document. **This is a forward citation into an unwritten adapter**, and until it lands, an implementation adopting such a number is non conformant under Q-A1 wherever that number reaches a capability record, a graph, or a set of quest records.

**The discriminator, so that the check is mechanical rather than a matter of review judgement.** A stored numeric field is forbidden under Q-A1 **when it is monotone non decreasing over the operator's history and is not scoped to a single act or a single observation.** Every permitted number in this document passes that test: a timestamp is scoped to one event, an interval and an expiry are properties of a declaration, a lap time is one act, and 4.1's ordinal position is a property of a declaration that moves in both directions. Every forbidden one fails it. **Failure:** a monotone operator scoped numeric field is rejected at write time, and specification text defining one is malformed and MUST be rejected in review. Without the discriminator, a conformance tool must either flag every numeric field or hand the decision to a reviewer, which is the five ways to pass that 1.1 chose Q-A1 to avoid. DEFER 5.4 already holds the mechanism and this is its application.

**What Q-A1 does not forbid.** It does not forbid a stopwatch, a tape measure, a lap time, a repetition count, a blood test, or any other measurement of an act or of the instrument, which are observations under TETHER section 5 and are governed there. It does not forbid two people comparing notes, teaching each other, or agreeing that one of them is better at something. It does not forbid the ordinal position of a quest in the operator's own declared order under section 4.1, which is a property of a declaration and not a property of an operator. It does not forbid the conformance tiers of section 12, which are properties of an implementation and never of an operator. What it forbids is a number over a person, held in a register, that only goes up.

**Q-A2. No prescribed content.**

QUEST MUST NOT name a capability, a graph, a node, a prerequisite edge, a quest, a completion criterion, a budget meter value, or a recommended starting configuration, in normative or informative text. A worked example MAY illustrate the *form* of a record, including a malformed one, and MUST NOT illustrate its *content*. Two conformant operators MAY hold contradictory graphs, and QUEST ranks neither.

**Failure:** specification text naming a capability or shipping an example graph is non conformant text and MUST be rejected in review, in the disposition HABITAT absolute requirement 2 applies to a stated quantity.

**What Q-A2 does not forbid.** It constrains this document rather than its implementers. It does not forbid an operator declaring any capability, graph, or quest they like, which section 3 requires them to do if they want a register at all. It does not forbid an institution publishing a curriculum, which section 5.4 governs as an external requirement set. It does not forbid a course, a coach, or a book from recommending anything whatever; those are claims by other parties and this document is not one of them.

**Q-A3. QUEST confers no authorization.**

A capability record, a node, a completion record, a verification record, or a quest state MUST NOT authorize an act at any consequence class, satisfy a TETHER rung gate, substitute for a re reference, satisfy a HABITAT declaration, close any gate in this stack, block an act, or excuse a failure under any document in this stack. QUEST MUST NOT define a rung, a crisis path, or any state that substitutes for, gates, delays, or conditions the escalation path declared under TETHER section 9.

**Failure:** a decision, gate, or threshold citing a QUEST element as satisfying evidence is a defect detected in the manner of POLARIS PL-02, and the gate is recorded `unevaluated` rather than `passed`. Any such element appearing in specification text is non conformant and MUST be rejected in review.

**What Q-A3 does not forbid.** It does not forbid an operator telling anyone what they can do, including an employer, a client, a clinician, or a peer, and it does not make such a statement a violation of anything. It does not forbid an operator declaring a capability conditioned refusal, which belongs under the POLARIS adapter where refusals live and where the amendment discipline applies. It does not forbid another party from having requirements; it forbids this document from supplying them. QUEST is a record of what an operator has done and can do. It is not a licence, and it is not a disqualification.

---

## Table of Contents

1. Introduction (protective)
   1.1 The friendlier road
   1.2 The firewall gap, and what covers it today
   1.3 Severability, and the dependency on KIT
   1.4 Position in the stack
   1.5 A note on this document's own name
2. Definitions (protective)
   2.1 Capability, node, edge, prerequisite graph
   2.2 Quest, main quest, side quest, objective
   2.3 Completion criterion, completion record, activity record
   2.4 Verification, verification interval
   2.5 The capability register, the external requirement set, the alias table
   2.6 The state vocabulary, and one deliberate omission
3. The Capability Register (protective)
   3.1 A separate register
   3.2 Nothing derived from this register enters the operator register
   3.3 Reports enumerate, they do not aggregate
   3.4 Clinical direction, and the coercive and protective split
4. Q: Quests (4.1, 4.2 and 4.6 protective; 4.3, 4.4 and 4.5 coercive)
   4.1 Main quests are totally ordered with no ties
   4.2 A side quest declares a bound and a termination condition
   4.3 Overrun has exactly three dispositions, and no fourth
   4.4 Inversion is detected, and the main quest is reported unattended
   4.5 Unattributed consumption is recorded and compared
   4.6 Quest status vocabulary
5. U: Unlocks (protective)
   5.1 A prerequisite graph, never a tree
   5.2 A prerequisite records, it never authorizes
   5.3 The dead prerequisite check
   5.4 A graph authored by another party is a requirement set
   5.5 Records made while a guardian held root
6. E: Evidence (6.1, 6.3 and 6.4 protective; 6.2 coercive)
   6.1 Progression is recorded against completion, never against activity
   6.2 Unconverted activity is enumerated, never scolded and never ratioed
   6.3 Verification attests an exercise, and it expires
   6.4 Self report is `claimed` and never `verified`
7. S: Skills (protective)
   7.1 Verification is periodic, and lapse is computed rather than noticed
   7.2 Lapse sets a status, it never removes a record
   7.3 No consecutive period counters
   7.4 A capability verified with an item declares the dependency
8. T: Termination (protective)
   8.1 Abandonment is a disposition, never a failure
   8.2 Abandonment MUST NOT be priced
9. What QUEST Never Does (neither)
10. The Alias Table (neither)
11. Failure Classes (each row inherits the label of its governing section)
12. Conformance (12.1 and 12.2 mixed; 12.3 protective by construction)
    12.1 Tier requirements
    12.2 Health invariants
    12.3 Self test
13. Versioning and Governance (neither)

---

## 1. Introduction (protective)

### 1.1 The friendlier road

TETHER section 4 forbids a record about the instrument from being merged into the operator's identity, and gives the reason: once a condition is held as an identity it stops being re evaluated, it does not expire when the condition changes, and it is not written anywhere that anything checks. The document's worked case is a fault. This document exists because the same merge has a second entrance, and the second entrance is unguarded precisely because it is pleasant to walk through.

A progression score is a record derived from what the instrument has done. Written into the operator register it becomes a self description, and the self description behaves exactly like the adopted fault: it is not re evaluated, it does not expire, and it is cited in decisions that never look at what supports it. The difference is the direction of travel and nothing else. A person argues with a diagnosis and volunteers for a rank.

The distinction that makes Q-A1 drawable rather than vague is **monotonicity**. A rung in TETHER section 7 is a small named state, gated by evidence, that an operator moves *down* as readily as up, and TETHER 7.4 requires that the downward transition be no harder to record than the upward one. A level is a number that only goes up. That single property is what turns a record into a history a person cannot leave: a state you can leave describes a moment, and a quantity that only accumulates describes a person.

So the requirement is not that levels be computed carefully, scoped tightly, or expired promptly. The requirement is that the vehicle is not supplied. DEFER 1.3 made exactly this move one layer up, refusing to reduce a set of overlapping bounded authority regions to a comparable seniority scalar and naming the reduction as the compression that breaks the system. Q-A1 is the same refusal applied to capability, and it is chosen over a governed scalar for the same reason and for one more: "no scalar appears in any register" is a single mechanical check, while "this level was recomputed inside its declared maximum age from a declared function over exactly one declared graph" is five checks with five ways to pass while remaining a score on a person.

The useful half of the governed scalar proposal survives, in section 3.3, as the constructive replacement. **Reports enumerate, they do not aggregate.** This is strictly more useful to the operator, who needs to know *which* capability is unverified and never *how many* are.

### 1.2 The firewall gap, and what covers it today

TETHER 4.1 forbids a record in the instrument register or the fault register from being written to, mirrored into, or cited as the operator register. It names two registers, by name.

A capability record is neither. Under section 2.1 of this document it is a property of the operator, instrument, and kit composite, and a firewall specified as a list of register names is a firewall with a list. Read literally, TETHER 4.1 does not stop a capability derived value from being written into the operator register, which is the friendlier road of 1.1 arriving through a gap in the wall rather than over it.

The fix belongs in TETHER and not here. An RFC generalising TETHER 4.1 from an enumerated list of registers to **any register holding a record about the instrument, its equipment, or its capabilities**, with TETHER 4.3's boundary statement extended in the same change, is a deliverable of this work. It is drafted and is not applied. This document cites it as pending and **does not restate the firewall**, because two locally stated copies of one absolute drift apart, and the copy an implementer deletes as boilerplate is always the one in the newer document.

The gap is not load bearing in the meantime, and it is worth stating why rather than leaving a reader to worry about it. Q-A1 removes the vehicle. There is no level, rank, score, or index to write into the operator register, because no conformant implementation computes one anywhere. The firewall and Q-A1 are belt and braces doing two different jobs: the firewall governs where a record may be written, and Q-A1 governs whether the record exists at all.

### 1.3 Severability, and the dependency on KIT

KIT and QUEST are siblings, and the dependency between them runs one way on purpose.

**QUEST MAY cite KIT. KIT MUST NOT cite QUEST.** QUEST cites KIT normatively in exactly three places, sections 4.2 (the budget object and the shape of a bound), 6.3 (calibration currency behind a verification whose reference source is `instrument`), and 7.4 (item dependency and departure), and nowhere else. An implementation MUST be able to reach full KIT conformance while declaring no capability, no node, and no quest.

The direction is a safety property and not a tidiness preference. The entire misuse surface of this family concentrates in progression: levels, ranking, scoring, credentialing, and gatekeeping all live in this document and almost none of it lives in KIT. As one document, an implementer who wants an equipment inventory drags the ranking machinery in with them, and a vendor shipping a leveling product gets the inventory as legitimising ballast. Split, with the dependency pointing this way, the dangerous half is optional: an implementation conformant on KIT alone is a real destination, and an implementation conformant on QUEST alone is not a thing that exists.

The membership test between the two documents is custody, and it is decided at write time. If a party other than the operator can end the operator's access to a thing without acting on the instrument, it is an item and KIT governs it. If not, it is a capability and QUEST governs it. Possession and exercise are then different verification regimes, which is why the two documents share almost no machinery: an item is verified by possession, which is cheap, binary, external, and checkable by anyone at any moment, while a capability is verified by exercise, which is expensive, graded, interval bound, and prone to exactly the self report failure TETHER 1.2 names.

Loss differs in kind and not in degree, which is why the two documents use different words for it. An item is **removed**: instantaneous, external, often involuntary. A capability **lapses**, which is gradual, internal, and silent, or it is **abandoned**, which is deliberate and recorded. Three words, three dispositions, two documents.

### 1.4 Position in the stack

QUEST inherits POLARIS's asymmetric precedence through TETHER, in the strongest available form.

POLARIS holds the highest precedence to forbid and none to permit. TETHER narrows: an instrument condition may narrow what an operator is authorized to do and may never widen it. HABITAT narrows: a declared environment may narrow and may never widen. **QUEST narrows nothing and permits nothing. It records.**

That is a weaker position than any other document in this family holds, and it is deliberate. A capability record that could narrow authority would be a competence assessment with governance force, and a capability record that could widen it would be a credential. Q-A3 forecloses both. An operator who wants a refusal conditioned on a capability declares the refusal under the POLARIS adapter, where refusals live, where they carry decidable predicates, and where amending one costs what amending a refusal costs.

### 1.5 A note on this document's own name

QUEST is a motto class device under POLARIS 7.3. The name is kept because compression aids recall and because the operator population this document is written for already narrates work in this vocabulary. The name is non normative, it compresses the five sections rather than asserting anything, and it MUST NOT be cited as grounds for any decision, any authorization, any gate evaluation, or any refusal.

Section 10 governs the vocabulary, and a reader arriving at this document intending to build a leveling application should read section 10 and section 9 first.

---

## 2. Definitions (protective)

### 2.1 Capability, node, edge, prerequisite graph

A **capability** is a property of the operator, instrument, and kit composite, evaluated against a declared task at a declared time.

This definition does load bearing work and every part of it is deliberate. A capability is not a property of the operator, so it is not identity and Q-A1 has something to bite on. It is not a property of the instrument, so it is not an observation under TETHER section 5 and does not belong in the instrument register. It is evaluated against a declared task, so it is decidable rather than adjectival. It is evaluated at a declared time, so it can lapse. And it includes the kit, which is why section 7.4 exists: change the equipment and the composite is a different composite, whatever the register still says.

A **node** is one capability record in one declared graph.

An **edge** is a declared prerequisite relation from one node to another, meaning that the operator declares the first to be a precondition for the second.

A **prerequisite graph** is a directed acyclic graph of nodes and edges, declared by the operator, scoped by section 5.1.

An **unlock** is a fact about a graph: a node is unlocked when every node with an edge into it is in state `verified`. An unlock is a reading, never an event, and it grants nothing. Section 5.2 is why.

### 2.2 Quest, main quest, side quest, objective

A **quest** is a declared objective with a declared record of what is spent pursuing it.

An **objective** is a stated outcome the operator is pursuing. It is not required to be decidable, because an operator's reasons for living are not the specification's business; what is required to be decidable is the quest's **termination condition** (2.3), which is a different field for a different job.

A **main quest** is a quest the operator has placed in the declared main quest order of section 4.1. The **rank one main quest** is the first entry in that order. The ordinal position is a property of the declaration and never of the operator, per the Q-A1 boundary statement.

A **side quest** is a bounded, optional, declared detour, carrying its own bound on at least one declared budget meter and its own termination condition. A detour with no bound and no termination condition is not a side quest, and section 4.5 governs what it is.

**Consumption** is the draw an act places on a declared meter, where a meter is defined by DEFER 2.5 and a meter declaration takes the form DEFER 5.4 states. **The rule attributing an act to a meter is DEFER's and is not restated here.** A **consumption record** names the act, the meter, the draw, the quest it is attributed to or `unattributed`, and its clinical direction field per 3.4.

A **declared budget** is the operator's set of declared meters with their bounds, in the form KIT 8.2 states.

A **bound on a quest** carries **at least one windowed aggregate ceiling**, which is the general half of KIT 8.2's shape requirement and binds every bound whatever its subject, and **MAY carry a per period ceiling**, meaning a ceiling on the draw attributable to that quest within one declared period. **A quest is not an item, so KIT 8.2's per item ceiling does not bind a quest bound**, and under KT-28's logic a bound missing a ceiling its shape requires confers no bound at all. Stating both halves here keeps 4.2 and 4.3 citable against a subject that holds no items.

**Failure:** a quest bound with no windowed aggregate ceiling is malformed and confers no bound, so an implementation MUST NOT report a quest as within its bound against it. A ceiling declared on an undeclared meter is malformed and is rejected at write time.

### 2.3 Completion criterion, completion record, activity record

A **completion criterion** is a decidable predicate declared before the activity it governs begins. A criterion requiring judgement to evaluate is not a criterion, per DEFER 4.3, and is rejected at write time.

A **completion record** cites a completion criterion, the evidence that the criterion was satisfied, and the time of satisfaction.

An **activity record** records that an act aimed at a node or a quest occurred, and what it consumed. It is not a completion record, it does not become one, and section 6.1 is the requirement that keeps the two apart.

A **termination condition** is a decidable predicate stating what ends a quest. It is required on a side quest by section 4.2.

### 2.4 Verification, verification interval

A **verification** is a record that a capability was exercised: what was exercised, when, at what scope, and against which reference source from TETHER 2.3's controlled vocabulary. It carries an expiry. Section 6.3 governs its form and the prohibition on expressing it as a property of the operator.

A **verification interval** is a declared period, per node, inside which a verification must have occurred for the node to remain `verified`. Section 7.1 governs lapse.

### 2.5 The capability register, the external requirement set, the alias table

The **capability register** holds capability, node, quest, completion, activity, and verification records. It is separate from the operator register and from the instrument register, per section 3.1.

An **external requirement set** is a graph, node, quest, or completion criterion declared by a party other than the operator. It names its author, it is held separately, and it is never merged into the capability register. Section 5.4 governs.

The **alias table** is the closed table of section 10 mapping every game term this document uses to the normative element it names, with each term marked normative, motto class, or refused.

### 2.6 The state vocabulary, and one deliberate omission

A capability record carries exactly one state, from exactly five values.

| State | Meaning |
|---|---|
| `unheld` | No verification stands and the operator asserts nothing |
| `claimed` | The operator asserts the capability, and no verification supports the assertion |
| `verified` | A verification inside its interval and inside its own expiry supports the record |
| `lapsed` | A verification once supported the record, and time has passed the interval or the expiry |
| `abandoned` | The operator has stopped holding the capability, deliberately and with a stated cause |

**The vocabulary MUST NOT include a `held` value.**

**Failure:** a register offering `held` fails closed. Every such value is read as `claimed`, and the implementation is non conformant.

The omission is the point. `held` is the word that means self report was accepted as a verdict. It is the state every assertion writes itself into and that nothing ever removes, which is TETHER 1.2's problem wearing a new name, and removing the value from the vocabulary is cheaper and stricter than any rule about who may write it.

The five values keep four genuinely different things apart, and collapsing any two produces a register that cannot tell a decision from a decay. `lapsed` is time doing it. `abandoned` is the operator doing it. `claimed` is the operator asserting it. `verified` is evidence doing it. A register that cannot distinguish "I stopped on purpose" from "this quietly went away" is a register whose every later reading is guesswork.

**`unverified` is a reading, not a state.** A node is unverified when its state is any value other than `verified`. The term is used in this document and in section 12 as a query over the register, and an implementation MUST NOT store it as a state value.

**Failure:** a register storing `unverified` as a state value is malformed; the value is read as `unheld` and the write is rejected. This is stated explicitly because the fail closed naming convention permits the word, and a reader would otherwise reasonably expect a sixth state.

---

## 3. The Capability Register (protective)

### 3.1 A separate register

**An implementation MUST maintain the capability register separately from the operator register and from the instrument register**, with no shared entries.

A capability record MUST carry:

- an identifier;
- the identifier of the exactly one graph it belongs to, per Q-A1;
- a declared task, expressed as a decidable predicate;
- a verification interval;
- **a declared evaluation interval for the section 5.3 and section 6.2 checks that range over it**, per 3.4;
- the timestamp and reference source of its most recent verification, or an explicit absence;
- **the identifier of the completion record and of the completion criterion discharged by that most recent verification, or an explicit absence**, per 6.1;
- **the sensing item identifier and its calibration currency where the reference source is `instrument`**, per 6.3 and KIT 6.6, or an explicit absence;
- its state, from the five values of 2.6;
- its declaring party, per 5.4;
- **its clinical direction field**, per 3.4, whose absence or `unknown` value is handled as clinically directed;
- any item dependency, per 7.4.

**Failure:** a record missing any required field is rejected at write time and is not partially stored. A record whose task predicate requires judgement to evaluate is not a task, per DEFER 4.3, and is rejected on the same terms. A record naming two graphs, or none, is malformed and is rejected, because a state scoped to more than one graph is the beginning of an aggregate.

The register sits alongside the operator and instrument registers rather than inside either. It is a third register and not a subdivision, because a capability is a property of a composite (2.1) and neither existing register describes a composite.

### 3.2 Nothing derived from this register enters the operator register

The identity firewall is inherited unchanged from TETHER absolute requirement 2 and is **not restated here**. Its reach over this register is the subject of the RFC named in section 1.2, which is pending. Q-A1 covers part of the gap in the meantime by removing the vehicle.

**A requirement of QUEST's own, stated because the inherited disposition does not reach this register until the RFC lands.** TETHER F1 fires on an entry appearing in both the operator register and the instrument or fault register, and 3.1 places the capability register outside that set by calling it a third register rather than a subdivision. **Any value derived from a capability, node, quest, completion, activity, or verification record MUST NOT be written to the operator register, mirrored into it, or cited as the operator register.** The prohibition is on **any** derived value and not only on a scalar: a completion record, an `abandoned` disposition with its stated cause, and a `lapsed` state are each caught here and none of them is caught by Q-A1, whose subject is a number.

**Failure:** the write or the citation is rejected at write time, on the TETHER F1 pattern, and a decision citing such a value is re resolved on its actual grounds. When the RFC of 1.2 lands and the firewall names any register holding a record about the instrument, its equipment, or its capabilities, this requirement is subsumed by it and is removed rather than kept as a second copy.

**Boundary statement, on the model TETHER 4.3 supplies.** This does not forbid an adoption under 5.4 or 5.5. **An adoption is an act of the operator register, not a write from the capability register**, and the record it creates is the operator's own declaration rather than a derived value crossing the wall. It does not forbid an operator saying what they can do, to anyone, which Q-A3's boundary statement already covers. It does not forbid the capability register holding whatever it holds. The prohibited act is the derivation crossing into identity.

### 3.3 Reports enumerate, they do not aggregate

**A report over capability, quest, completion, or activity records MUST be expressed as an enumeration of named records. An implementation MUST NOT expose a count, ratio, percentage, streak, index, or other aggregate over them.**

**An enumeration MUST NOT be accompanied by, or presented in a form whose primary reading is, its cardinality.** An implementation rendering the count of a returned enumeration as a summary value, a header figure, a badge, or a chart axis is non conformant, and the count is void with the list returned in its place. This is 5.1's anti shape principle applied to the object 3.3 itself mandates: the adversary denied a scalar field computes one from the shape, and an enumeration's shape is its length. "Seven of ten capabilities verified" is a level with extra steps whether the seven is stored or counted at render time.

**Two carve outs are explicit.**

**First,** conformance health invariants that count malformed, missing, or defective records, as required by section 12.2, are excepted, and every such number MUST be labelled as a conformance check.

**Second, the drift comparisons of section 4.** They are computed over **one operator's own records**, are **never exposed as a value**, and expose only the boolean disposition: `unattended` or `uncomputable` under 4.4, and the `unattributed` enumeration under 4.5. The intermediate sums those comparisons require are working values and are covered by 4.4's prohibition on displaying, storing, or transmitting them. The carve out is stated because 4.4 and 4.5 would otherwise be aggregates that 3.3 refuses while section 12 mandates them, which is a conformance suite that cannot be written. The carve out is stated rather than left to inference because TETHER 4.3 demonstrated that an absolute stated without its boundaries gets read into absurdity, and a document that could not count its own malformed records could not be conformance tested.

**Failure:** an aggregate is refused rather than returned. A requested summary resolves to the list it would have summarized, or to `undefined` if the list cannot be produced. An implementation returning a count in place of a list is non conformant, and a count labelled as a conformance check while ranging over well formed records is a mislabelled aggregate and is refused on the same terms.

Q-A1 closes the front door and this closes the side door. Lists do not rank and do not compare, and the list is the strictly more useful output, because an operator reading their own register needs to know which capability is unverified and never how many are.

### 3.4 Clinical direction, and the coercive and protective split

**This subsection discharges inherited absolute 4 in this document.** KIT built the apparatus from the same inherited absolute, at KIT 3.5, and QUEST imports it by construction rather than restating its derivation. Until this subsection existed, QUEST asserted the absolute in one line and derived only 7.3 from it, while four of its own requirements had a compliant response that consists of doing less care.

**Every numbered section of this document is classified `coercive`, `protective`, or `neither`.**

A **coercive** rule generates pressure toward consuming less on care, or toward reporting care consumption as drift. A **protective** rule only ever narrows what may be claimed from a record; its compliant response is a better declaration and never a reduction. A rule that states no requirement about a quest, a capability, or a consumption record carries `neither` and states why.

**The classification in this version.**

**Coercive: 4.3, 4.4, 4.5, and 6.2.** Each has a compliant response consisting of doing less. 4.3 presses a side quest past a ceiling toward `closed`. 4.4 reports the rank one main quest `unattended` when any side quest outconsumes it. 4.5 surfaces unattributed consumption exceeding the main quest's. 6.2 enumerates unconverted activity against a threshold. For an operator on TETHER 7.1's crisis or impaired rung, care consumption exceeding the main quest is the **expected** state, and a conformant register that reported it as drift would be reporting the operator's treatment as a governance defect.

**Protective: 1, 2, 3, 4.1, 4.2, 4.6, 5, 6.1, 6.3, 6.4, 7, and 8.**
**Neither: Q-A2, 9, 10, 11, 12, and 13**, which place requirements on this document's own text, on its vocabulary, or on an implementation's conformance apparatus, and never on a quest, a capability, or a consumption record.

**A subsection inherits its parent section's label unless it carries one of its own.** Where a header label and this enumeration disagree, **the stricter governs** until the disagreement is corrected in review.

**The declared clinical direction field.** **A quest record, a capability record, and a consumption record MUST each carry a declared clinical direction field**, stating whether the objective, the capability, or the consumption is prescribed, fitted, or directed by a licensed clinician.

**Failure mode, failing closed toward protection: a record whose clinical direction field is absent, or declared `unknown`, MUST be handled as clinically directed for the purpose of this split, until the operator declares otherwise.** The field is surfaced `unconfirmed` and the record MUST NOT be assumed non clinical. This is KIT 3.5's disposition, imported unchanged, and for KIT's reason: the field is the single input routing a record into the protection derived from inherited absolute 4, and reading its absence as "not clinical" defeats the protection with an omission.

**The disposition. A coercive check resolving against a clinically directed record returns `out-of-scope`. It never returns a pass and never returns a fail**, because a pass would let the exclusion be read as satisfaction and a fail would be the pressure the exclusion exists to remove.

**A tier item, health invariant, or self test check that an operator could satisfy by consuming less on clinically directed care is malformed specification text and MUST be rejected in review**, per inherited absolute 4. Section 12.3's claim to that effect now has this subsection behind it.

**The consequence for the drift denominator, stated so that no implementer has to infer it.** Consumption on a clinically directed record is **excluded from the inversion denominator of 4.4 and from the unattributed comparison of 4.5**, and its exclusion is reported as an exclusion rather than silently applied. It is not a side quest, it is not unattributed consumption, and it is not drift. An implementation that routes it through either comparison is non conformant and the comparison is recomputed with it excluded.

**What this does not forbid.** It does not forbid an operator declaring a quest whose objective is their own treatment, and 4.2's requirements bind such a quest's form exactly as they bind any other. It does not forbid recording what care consumed, which 4.5 requires so the register can account for the period. It does not make a clinically directed record invisible, unreportable, or second class. What it removes is the pressure, and only the pressure.

---

## 4. Q: Quests (4.1, 4.2 and 4.6 protective; 4.3, 4.4 and 4.5 coercive)

### 4.1 Main quests are totally ordered with no ties

**An operator MUST declare their main quests as a total order with no ties.** A change to the order is a recorded act carrying a stated cause. A main quest leaving the order MUST be recorded `completed`, `abandoned`, or `superseded`, and MUST NOT be silently replaced.

**Failure: a change to the main quest order carrying no stated cause is rejected at write time.** The requirement above states the obligation and stated no disposition for its breach, which left open the mechanism 4.3's own rationale names as the real failure: drift arrives through the order rather than through the budget, and an order that can be silently reordered has no rebudget record to enumerate.

**Failure:** a tie is an undeclared order and the declaration is malformed, in the disposition POLARIS 6.1 applies to a tied loyalty order. A main quest disappearing from the order with none of the three dispositions is recorded as an `unresolved` order change and surfaced at the next review, never dropped. `unresolved` marks the change to the order and is not a quest status under 4.6, which remains a closed set of five.

What the requirement buys: the rank one main quest is the single denominator that makes every drift comparison in this section arithmetic rather than argument. Sections 4.4 and 4.5 both compare consumption against it, and neither is computable without a first entry that is not tied.

What the requirement deliberately does not do: it does not tell an operator how many main quests they have. An operator who is simultaneously the sole carer for a dependent and the sole earner for a household does not obviously have one main quest, and a document that told them to pick one would be prescribing a life rather than specifying a form. Total ordering with no ties delivers everything a singleton would have delivered, because there cannot be two number ones.

### 4.2 A side quest declares a bound and a termination condition

**A side quest record MUST declare three things: its objective; a bound expressed on at least one budget meter declared under KIT section 8, in the shape 2.2 states; and a termination condition stating what ends it.** It MUST also carry the clinical direction field of 3.4, which is a field on every quest record and not a fourth element of the side quest declaration.

**Failure:** a record missing any of the three is malformed and is rejected at write time. A record whose clinical direction field is absent or `unknown` is handled as clinically directed per 3.4 and is not rejected on that ground. An undeclared detour that consumes declared budget is not a side quest at all, and section 4.5 governs it as unattributed consumption.

A bounded optional detour with no stated end is not a detour. It is an unrecorded change to the main quest order, and the register will show the main quest open and attended while nothing whatever is moving it.

Note one asymmetry with KIT, so that a reader who knows both documents does not read a contradiction. KIT does not require an exit condition on every substituting item, because a rule that every substitution must declare what would end it generates pressure to stop wearing the lenses, stop using the chair, and stop carrying the monitor, which is TETHER's inherited absolute 4 violated in one sentence. That hazard does not exist here. A side quest is by definition optional and bounded, nothing about a person's care depends on one continuing, and the requirement can therefore be stated without qualification.

This is the first of the three sections in which QUEST cites KIT, alongside 6.3 and 7.4.

### 4.3 Overrun has exactly three dispositions, and no fourth (coercive)

**This subsection is coercive and does not reach a clinically directed record**, per 3.4. Every check in it resolving against such a record returns `out-of-scope`, never a pass and never a fail.

**A side quest whose consumption exceeds either its declared per period ceiling, where one is declared, or its windowed aggregate ceiling MUST be surfaced as a governance defect, and MUST resolve to exactly one of three dispositions.**

| Disposition | Meaning |
|---|---|
| `closed` | The side quest ends. Its records are retained |
| `rebudgeted` | The bound is changed, with a stated cause |
| `promoted` | The quest enters the main quest order, which is a change to that order under 4.1 |

**No fourth disposition may be defined.** Silent continuation MUST NOT be a disposition. A `rebudgeted` disposition MUST carry a stated cause, and **the rebudget records MUST be enumerated with their causes.** **An implementation MUST NOT close, cancel, suspend, de prioritize, or block a quest automatically.**

The enumeration replaces an earlier requirement to report the count. A count of rebudgets per quest is a number over an operator, held in a register, that nothing in this document ever decrements, which is Q-A1's own definition of the thing it forbids, and 3.3 refuses the aggregate independently. **The enumeration loses nothing the requirement needs and supplies more:** the failure 4.3 exists to catch is six quiet rebudgets that together amend what the operator's time is for, and what an operator needs in front of them is the six stated causes, not the numeral six.

**Failure:** a side quest past a ceiling with no recorded disposition is reported as a governance defect and remains so until dispositioned. It is not a busy month, per DEFER 15.3. A record offering a fourth disposition is non conformant. An implementation that auto closes on overrun is non conformant, and the closure is void.

Three notes on why the shape is this shape. The three dispositions mirror DEFER 10.1's three timeout dispositions and its prohibition on a fourth, and the reason transfers exactly: every proposed fourth value in this space turns out on inspection to be silent continuation with a friendlier label. The rebudget count is POLARIS 10.3 and PL-27, precedent accumulating into a de facto amendment: the real failure is never one overrun, it is six quiet rebudgets that together amend what the operator's time is for, with no amendment ever recorded. And `promoted` is deliberately expensive, because it changes the main quest order and therefore changes the denominator every other check in this section uses.

### 4.4 Inversion is detected, and the main quest is reported unattended (coercive)

**This subsection is coercive and does not reach a clinically directed record**, per 3.4. A check resolving against such a record returns `out-of-scope`, and consumption on a clinically directed record is excluded from the denominator and reported as an exclusion.

**An implementation MUST compute, over a declared window, on a declared evaluation interval, and per declared meter, the consumption attributed to the rank one main quest and to each open side quest. Where any side quest's consumption exceeds the rank one main quest's over that window, the implementation MUST record the inversion and MUST report the main quest as `unattended`.**

**The computed sums MUST NOT be displayed, stored, or transmitted.** They are working values of the comparison and nothing else. **Only the disposition is exposed**, which is `unattended`, `uncomputable`, or nothing at all. **Failure:** a displayed, stored, or transmitted sum is an aggregate over quest and activity records under 3.3 and a scalar over the operator under Q-A1, is rejected at write time, and is void where already written. The second carve out in 3.3 exists to license the computation and not its output.

**`unattended` is a reported reading over the drift comparison. It is not a quest status under 4.6, MUST NOT be stored as one, and MUST NOT be written into a quest's status field**, which remains the closed set of five that section 13 forbids adding to. It carries the same disclaimer 4.1's `unresolved` and 6.1's `unverifiable` already carry, and it was the only one of the three drafted without it.

**On the fail closed naming convention inherited from KIT 2.11**, which requires that a fail closed state name what is missing and never a deficiency in the operator: `unattended` names a **missing attribution of consumption to the rank one main quest over the declared window**, which is a property of the register's records, and it is reported against the quest and never against the operator. 4.4's own load bearing property says the same thing in the other direction, that the report names the main quest as unattended and never the side quest as an offender.

**A declared evaluation interval is required, and its absence is a failure.** **Failure:** where no evaluation interval is declared, or where the declared interval has lapsed, the comparison is reported `uncomputable` and **is never reported as passing**. A declared window is a measurement span and not a cadence, and an implementation that computed the comparison once and never again would otherwise satisfy every stated check while 12.2's undetected inversions target reads zero by silence. This check runs on a clock for the reason 4.4 states below, and a clock with no interval is not a clock.

**Failure:** an undetected inversion is a health invariant failure. **Where the meters, the window, or the evaluation interval required to compute the comparison are undeclared, the comparison is reported `uncomputable`** and the register is non conformant at the tier requiring it. It is never reported as passing. Silence is not evidence of attention.

Two properties of this requirement are load bearing and a reimplementation must preserve both.

**The report names the main quest as unattended, not the side quest as an offender.** This keeps the requirement on the correct side of the line between a governance document and a productivity nag, and it is also the more informative output: the operator already knows what they have been doing, and what they have lost track of is what they have not been doing.

**The requirement takes no position on whether the inversion is wrong.** Sometimes the side quest deserved to win, and the honest move is to promote it under 4.3. The specification makes the fact visible and stops.

This check runs on a clock rather than on an event, and the reason is the same reason TETHER 1.2 gives for periodic re referencing and HABITAT section 8 gives for the silent floor. A side quest that has quietly become the main quest does not announce itself, produces no event, and generates no complaint. An event driven check will never fire, because nothing ever happens. Three documents in this family arrive independently at the same finding, which is the strongest available evidence that it is structural.

### 4.5 Unattributed consumption is recorded and compared (coercive)

**This subsection is coercive and does not reach a clinically directed record**, per 3.4. Consumption on a clinically directed record is excluded from this comparison and reported as an exclusion, and a check resolving against such a record returns `out-of-scope`.

**An act consuming declared budget MUST be attributable to a declared quest. Consumption that cannot be attributed MUST be recorded `unattributed`, MUST NOT be discarded, and MUST NOT be assigned to a default quest.** Where unattributed consumption exceeds the rank one main quest's consumption over a declared window, evaluated on a declared evaluation interval, the implementation MUST surface it as an enumeration of the named consumption records. **The comparison's sums MUST NOT be displayed, stored, or transmitted**, per 4.4. **Failure:** where the window or the evaluation interval is undeclared or lapsed, the comparison is reported `uncomputable` and is never reported as passing.

**Failure:** consumption assigned to a default quest is a misattribution and the assignment is rejected, mirroring DEFER 6.5 and DF-15, where routing an unclassifiable act to a default class is the error precisely because it makes the gap invisible. An implementation that discards unattributed consumption produces a register that reconciles while describing a period it cannot account for, and is non conformant.

Drift rarely arrives as one oversized side quest that section 4.4 catches. It arrives as many small unlogged detours, none of which was worth recording. The honest general form of the question "where did the year go" is an unattributed line that nobody was ever required to write down.

### 4.6 Quest status vocabulary

A quest carries exactly one status, from five values.

| Status | Meaning |
|---|---|
| `open` | Being pursued |
| `blocked` | Waiting on a party who is not the operator |
| `completed` | Its termination condition was satisfied by completion |
| `abandoned` | Ended deliberately by the operator, with a stated cause, per section 8 |
| `overrun` | Past a declared ceiling and awaiting one of the three dispositions of 4.3 |

**QUEST MUST NOT define, and an implementation MUST NOT compute or display, a percentage complete, a progress bar, a remaining estimate expressed as a fraction, or any other partial completion measure.**

**Failure:** a partial completion measure found in any register or view is rejected at write time, and specification text defining one is malformed and MUST be rejected in review.

`blocked` exists because HABITAT section 7 already establishes that waiting on a provisioning party is a common and non culpable state. Without the value, an operator records a stall as their own failure, which is both false and, once it is in a register, durable.

The prohibition on the progress bar is not aesthetic. A bar approaching full is a sunk cost device, and its function in the medium this document borrows its vocabulary from is to override a decision to stop at exactly the moment stopping is most likely to be correct. That is directly opposed to section 8, which exists to make stopping cheap and honest.

---

## 5. U: Unlocks (protective)

### 5.1 A prerequisite graph, never a tree

**The normative structure is a directed acyclic prerequisite graph over declared capabilities. It MUST NOT declare a root capability, MUST be permitted to be disconnected, and MUST NOT carry a depth, tier, or generation field. An implementation MUST NOT compute path length, depth, or breadth for any purpose other than resolving whether a named prerequisite is satisfied.**

**Failure:** a declared root, a depth field, or a computed depth makes the graph malformed and it is rejected at write time. A graph that cannot be validated acyclic is rejected, never accepted with a warning, because a cycle in a prerequisite relation is a graph asserting that a thing is its own precondition and no reading of it is safe.

A tree has a root and therefore a depth. Depth is a number, and a number over a person is a level. The adversary who cannot get a scalar from a field computes one from the shape, and the defence is to make depth undefined rather than merely unreported: forbid the root, permit disconnection, and there is no distance from anywhere to measure.

"Skill tree" survives as the teaching alias in section 10, where it names the structure without carrying the arithmetic.

### 5.2 A prerequisite records, it never authorizes

**An unmet prerequisite MUST NOT block an act, MUST NOT narrow or remove any authority the operator holds, and MUST NOT be cited by any party as grounds for refusing an operator an act, a role, an opportunity, or care.**

**An act aimed at a node whose prerequisites are not `verified` MUST be recorded `attempted-above-prerequisite`, together with its outcome, and MUST NOT produce a completion record.**

**Failure, and read this one carefully, because it is the single place in this family where a careless fail closed builds the gatekeeping machine.** The *progression claim* fails closed: no completion record is written, and the node does not become `verified`. The *act* does not fail at all: it proceeds, and the implementation records what happened. **An implementation that blocks the act on the ground of the unmet prerequisite is non conformant.** An implementation that cites an unmet prerequisite as grounds for a refusal has committed a Q-A3 violation detected in the manner of POLARIS PL-02.

**A block required by any other document in this stack is unaffected by this subsection.** A POLARIS refusal, a DEFER envelope, a TETHER threshold: none of them is a QUEST non conformance, and nothing in this section satisfies, relaxes, or excuses any of them. The failure sentence names its ground for that reason. Left unqualified it read as making conformance to another document's refusal a violation here, which is a widening POLARIS 8.1 forbids and which contradicts 1.4's own statement that QUEST narrows nothing and permits nothing, and it is the failure text that a conformance harness is written against.

TETHER 7.2 already holds the honest version, one layer down: an act aimed above the current rung is **spent**, not forbidden, because its effect is not observable against the noise of the rung below. Order of operations is a fact about what will work. It is not a permission system. The moment an unmet prerequisite can stop a person, this document has become a credential system, and credentials become employment gates, and employment gates are the ladder Q-A1 exists to prevent.

The word **position** is deliberately not used as a name for where an operator sits in the graph. It appeared in earlier drafting in that sense, and in that sense it smuggles the scalar back in, because a position in a graph implies an ordering over the operator standing at it. The word is used elsewhere in this document in an unrelated sense, at 2.2 and 4.1, as the ordinal position of a declaration in the operator's own declared order, which the Q-A1 boundary statement expressly permits as a property of a declaration and never of an operator. `attempted-above-prerequisite` names the fact without naming a rank.

### 5.3 The dead prerequisite check

**An implementation MUST report prerequisite edges that no recorded `attempted-above-prerequisite` outcome has ever tested, at Tier 3, and SHOULD report them below Tier 3.** The tier is named here rather than only in section 12, so that this subsection's own failure mode is decidable without reading the tier ladder.

**The report MUST be produced on a declared evaluation interval**, and where no interval is declared, or the declared interval has lapsed, the report is `uncomputable` and is never reported as passing. **Failure:** untested edges are reported as a signal and never as a defect. An implementation that reports them as failures is non conformant. An implementation at Tier 3 that reports nothing at all is non conformant; below Tier 3 it is conformant. By this subsection's own imported reasoning from POLARIS 4.5, a check run once at build time and never again is indistinguishable from one that is inert.

This is POLARIS 4.5's dead refusal problem applied to a graph. A prerequisite that has never been attempted out of order is either a real constraint or a superstition, and from the outside those are indistinguishable. The requirement is stated at SHOULD strength, and it is framed as recording outcomes when they happen rather than as generating experiments, for one reason: requiring an operator to attempt things out of order in order to test their own graph would be prescribing a life, and this document does not do that.

### 5.4 A graph authored by another party is a requirement set

**A graph, node, quest, or completion criterion declared by a party other than the operator MUST be recorded as an external requirement set naming its author, and MUST NOT be merged into the operator's capability register.** An operator MAY adopt an element of a requirement set, and the adoption is a recorded act of the operator register.

**Failure:** a merge is rejected at write time. A capability record whose declaring party is not the operator and which carries no adoption record is malformed and is rejected.

DEFER 3.1 already holds the general form: an agent definition that declares its own authority is a claim and not a delegation, and authority arrives only by grant. A curriculum handed to a person is a claim about what the party handing it over wants. It becomes the operator's only by an act of the operator.

Keeping the two objects distinct is what lets an institution's requirement set be read, complied with, and refused, without any of those three being confused with a description of the person complying.

### 5.5 Records made while a guardian held root

**A capability, completion, or quest record created while root was held by a guardian under TETHER 3.3 MUST carry the guardian as its declaring party, MUST NOT be exported or published, and MUST expire at the return of root unless the operator adopts it by a recorded act.**

**Failure:** expiry is the default and adoption is the exception. A record persisting past the return of root with no adoption record is expired, never retained. An implementation retaining such records by default is non conformant, and the retention is not cured by the operator's later silence.

**Scheduled expiry under this subsection is deletion, and is expressly carved out of `QS-39` and of the deletion row in section 9.** It is not a deletion in place of marking. **8.1 and POLARIS PL-15 govern the withdrawal of a standing record**, where marking withdrawn preserves evidence that something was once asserted; **this subsection governs the expiry of a time bounded one**, where the whole point is that nothing survives the return of root. An implementation that marks a guardian authored record withdrawn and retains it has defeated 5.5, and one that deletes it under 5.5 does not trip `QS-39`.

TETHER 4.2 already names the severest case the firewall exists for: a finding received as a description of who you are, at the age when descriptions set, by a subject who cannot refuse it. A graded record of what a child could and could not do is the same object arriving through this document, and it has the additional property that it looks like an achievement.

TRACE 10.3 supplies the mechanism ready made: a derived artifact is adopted deliberately or it expires, carries a declared maximum age, and is never indefinite. Expiry as the default is what stops the machinery of a scored childhood surviving into adulthood by inertia, which is the way it actually survives.

---

## 6. E: Evidence (6.1, 6.3 and 6.4 protective; 6.2 coercive)

### 6.1 Progression is recorded against completion, never against activity

**A completion record MUST cite a completion criterion declared before the activity began, and the evidence of its satisfaction. An implementation MUST NOT record progression against elapsed time, session count, attempt count, volume of activity, or any measure of effort.**

**The join between a completion record and a verification, stated in one place because two record types were each said to produce `verified` and their relationship was never stated. A completion record is the only thing that may create a verification, and a verification MUST cite the completion record and the completion criterion it discharged.** A verification citing no completion record is malformed and is rejected at write time. This is the reading that makes 2.6, 6.1, and 7.1 consistent: `verified` is set by a verification (2.6), a verification exists only where a completion discharged a declared criterion (here), and lapse is computed from the most recent verification (7.1). It is also the reading 5.2 assumes when it says that an act above an unmet prerequisite writes no completion record and the node does not become `verified`.

**The consequence for a node with no declared criterion, made explicit.** Such a node cannot receive a completion, therefore cannot receive a verification, therefore **cannot reach `verified`**. It carries the marking `unverifiable` and its state is whatever the five values of 2.6 otherwise make it, which is `unheld` where the operator asserts nothing and `claimed` where they do.

**Failure:** an activity record submitted as a completion is rejected at write time. A completion citing a criterion authored after the fact is malformed, on the DEFER 6.4 pattern where a classification produced after resolution is a rationalization. A node against which no completion criterion has ever been declared cannot receive progression at all, and carries the marking `unverifiable`. That marking is a property of the node's evidence and is not a state value under 2.6, which remains a closed set of five.

State the reason as a design fact rather than as a preference, because it is one. Experience awarded per unit of activity rewards time spent in the medium, and it serves the operator of the game. Experience awarded per completed objective respects the player's time. This document is written for the player.

The consequence for the register is worse than the incentive problem. Activity recorded as progression produces a register that shows advancement where none occurred, and every later decision that reads it is reading a fiction. The register is the only asset this document has.

### 6.2 Unconverted activity is enumerated, never scolded and never ratioed (coercive)

**This subsection is coercive and does not reach a clinically directed record**, per 3.4. A check resolving against such a record returns `out-of-scope`, never a pass and never a fail. Activity that is care, recorded against a node and not converting to a completion, is the expected state on TETHER 7.1's crisis and impaired rungs, and reporting it against a threshold would be the pressure inherited absolute 4 forbids.

**Where activity is recorded against a node with no completion inside that node's declared window, the implementation MUST report, on a declared evaluation interval, the specific unconverted activity as an enumeration of named records, against a threshold the operator declares.**

**The operator's declared unconverted activity threshold and the declared evaluation interval are required fields of the operator's declaration**, without which this check is neither computable nor reportable as uncomputable. **Failure:** where the threshold, the window, or the evaluation interval is undeclared or lapsed, the report is `uncomputable` and is never reported as passing.

**The specification MUST NOT characterize unconverted activity as an error, a defect, or a fault of the operator, and MUST NOT express it as a count, ratio, or percentage.**

**Failure:** an unreported node above the declared threshold is a health invariant failure. Specification text characterizing unconverted activity as an operator failing is malformed and MUST be rejected in review, because a judgment about a person, written into a register on the strength of an activity pattern, is a firewall hazard under TETHER section 4 whether or not anyone calls it a score.

Three reasons the output is a list and not a verdict. Detection is decidable and judgment is not, and the judgment is not this document's to make. A productivity ratio computed over a person is the employee scoring misuse arriving through the back door, and it arrives in a document that has otherwise refused every front door. And the honest output is more useful anyway: the operator needs the names of the things that did not convert.

Letting the operator declare the threshold, and reporting against the declared value, is POLARIS 7.2's mechanism, which exists precisely so that a health signal does not smuggle in a prescription.

### 6.3 Verification attests an exercise, and it expires

**A verification record MUST name the capability exercised, the date, the scope, and its reference source from TETHER 2.3's controlled vocabulary, and MUST carry an expiry.**

**A verification MUST NOT be expressed as an attestation about the operator, MUST NOT carry an issuer authority over the operator, and MUST NOT be declared non expiring or `indefinite`.**

**Where the reference source is `instrument`, the verification MUST name the sensing item that produced the supporting output and that item's calibration currency, per KIT 6.6.** **A verification supported by output recorded `unknown` under KIT 6.3 MUST NOT produce `verified`**, and the node is recorded `claimed` where the operator asserts the capability and `unheld` otherwise.

**Failure:** a verification citing reference source `instrument` without the item identifier and its calibration currency is malformed and is rejected at write time. A node reading `verified` on output recorded `unknown` under KIT 6.3 is non conformant, and the reading is corrected rather than annotated.

The gap this closes is narrow and load bearing. KIT 6.5 scopes its own prohibition to exactly two consumers, a TETHER 7.3 rung gate and a threshold gating an act at K2 or above, and a QUEST verification is neither. 7.4 propagates possession failures and not calibration failures, and a wearable past its calibration interval is present and confirmed, so no KIT section 5 state fires. Without this clause a node reads `verified` on a reading KIT already rejected at the instrument register, which is the reference source laundering attack KIT names as its claim to independent necessity, arriving here. It is worse here than there, because 7.2 forbids reversing the supporting completion records once written.

**This is the third of three places in which QUEST cites KIT**, alongside 4.2 and 7.4.

**Failure:** a verification with no expiry, or declared `indefinite`, is malformed and is rejected at write time. A verification expressed as a property of the operator rather than of an exercise fails closed under Q-A1 and under the pending firewall RFC of section 1.2: the record is rejected, and any decision citing it is re resolved on its actual grounds.

Expiry is what prevents credentialing, and the mechanism is worth naming exactly. A permanent, portable, issuer signed record that a person holds a capability is a certificate. Certificates become employment gates. Employment gates become the ladder. Attesting the *exercise* keeps the record true, that this thing was done on that day at that scope, and keeps it from hardening into a description of the person who did it.

### 6.4 Self report is `claimed` and never `verified`

**A node supported only by the operator's own assertion that the capability is still held MUST be recorded `claimed`, and MUST NOT be recorded `verified`.**

**Failure: a verification record whose reference source is `self-report` MUST NOT set state `verified`, and the write is rejected at write time** rather than accepted and downgraded later. A node found recorded `verified` on self report alone is corrected to `claimed`. Fail closed.

The rejection is at write time because every comparable guard in this document is (2.6, 3.1, 4.2, 5.1, 5.4, 6.1, 6.3, 7.3, 8.1 all read "rejected at write time"), and because "the next check" was defined nowhere, obliged nobody to run, and had no health invariant behind it. A register could therefore hold `verified` on self report for an unbounded period and remain conformant, defeating the requirement this document calls its inheritance from TETHER 1.2, in the one place TETHER's own F2 fails closed immediately.

TETHER 1.2. The reasoning is there and is not restated here.

---

## 7. S: Skills (protective)

### 7.1 Verification is periodic, and lapse is computed rather than noticed

**Every node MUST declare a verification interval. Where a node's most recent verification is older than that interval, or has passed its own expiry under 6.3, whichever comes first, the node's state MUST become `lapsed`, computed from the interval.**

**An implementation MUST NOT carry a `verified` state forward past its interval, and MUST NOT make lapse conditional on an event, a notification, a complaint, or an operator's judgment that re verification is warranted.**

**Failure:** a node past its interval reads `lapsed`. This is not an error and not a fault, it is a state. An implementation that treats a lapsed node as continuing to be held is non conformant, and the reading is corrected rather than preserved.

TETHER 5.4 is the canonical statement that re referencing is periodic rather than triggered, and this is a **forward citation into a section that is currently an unwritten skeleton**, marked as such per TETHER's own status note. This document declares only its own interval and its own lapse disposition, and does not restate the reasoning a fourth time.

The author's premise for splitting these two documents was that a tool can be lost and a skill cannot. This section is the reason that premise is not the one this family uses. Skills are lost, to disuse, to injury, and to time. The membership test is custody (1.3), and lapse is exactly the phenomenon a losability axis would have had to deny.

### 7.2 Lapse sets a status, it never removes a record

**The completion records supporting a lapsed node MUST NOT be deleted, decremented, reduced, or reversed. No progression state may be diminished by the passage of time alone. `lapsed` MUST NOT be rendered as absent, zero, expired, or lost.**

**Failure:** an implementation that zeroes, resets, or decrements on lapse is non conformant, and the decrement is void rather than merely discouraged.

A lapsed node is a true statement about the present that leaves the past intact: the thing was done, on that day, at that scope, and the current state of the composite is unknown. An implementation that erases the first half to express the second half has destroyed evidence in order to render a status.

### 7.3 No consecutive period counters

**QUEST MUST NOT define, and an implementation MUST NOT compute, a count of consecutive periods in which an act occurred, or any measure whose value is reduced by a single missed period.**

**Failure:** a streak counter found in any register is rejected at write time, and specification text defining one is malformed and MUST be rejected in review.

This is the most seductive of the rejected mechanics, so all four costs are stated.

1. **It makes the record more valuable than the thing recorded.** Once the counter has value, there is an incentive to log falsely, and the register is the only asset this document has.
2. **It rewards acting while impaired in order to preserve the number.** That is TETHER 7.2's act aimed above the current rung, taken under a compulsion the implementation manufactured.
3. **It records a break as a failure.** That is the abandonment poison of section 8.1 arriving through arithmetic instead of through a status field.
4. **It builds a penalty for being unwell.** Lapse is exactly what the crisis and impaired rungs predict, so a mechanism that penalises lapse penalises the rungs, in a document whose inherited absolute 4 forbids any requirement an operator could satisfy by declining care.

In one sentence: a streak converts a lapse into a fault.

### 7.4 A capability verified with an item declares the dependency

**A capability record MUST declare any item its verification depended on, and MUST declare whether that dependency is `substitute` or `amplify` per KIT section 4. A capability MUST NOT be recorded `verified` on the basis of a performance that used an item the record does not declare.**

**Where a declared `substitute` dependency takes any disposition under KIT 5.2 (`lost`, `broken`, `expired`, `superseded`, `released`, `unprovisioned`), or is recorded `unconfirmed` under KIT 5.1, or its output is recorded `unknown` under KIT 6.3, the capability MUST leave `verified`.** Its state becomes `claimed` where the operator records an assertion, and `unheld` otherwise. **An `amplify` dependency MUST NOT gate the capability's state.**

The rule is stated in its general form rather than as an enumeration of three, because the enumeration failed open in the commonest case. `QS-24` already states the general form, and an earlier draft covered `unconfirmed`, `lost`, and `unprovisioned` only, leaving a capability whose substitute item is `broken`, `expired`, `superseded`, or `released` reading `verified` indefinitely. **The item being gone is the trigger, and the disposition naming how it went is not the discriminator.** `released` is the case an implementer will most plausibly argue should not fire, on the ground that the operator chose it; that argument is wrong for the same reason KIT 5.2 keeps `released` and `lost` apart, which is that the register's assertion is equally false either way.

**Failure:** a verification citing an undeclared item is rejected at write time. Where a declared substitute item goes unavailable and dependent capabilities remain `verified`, the implementation is non conformant, and the dependent readings are corrected rather than annotated.

The rule needs no case analysis, because the substitute and amplify asymmetry does all the work. A capability that exists only while equipped, recorded as though it were internal, will be cited on the day the item is gone, which is exactly the moment the register is wrong and exactly the moment nobody checks it.

This is also why KIT 5.2 requires a disposition on every item departure. Without a loss record, this transition has no trigger, and an untriggered transition is a `verified` reading that outlives the composite it described.

This is the third of the three sections in which QUEST cites KIT, alongside 4.2 and 6.3, and the direction of the dependency (1.3) is the reason every one of the three runs this way.

---

## 8. T: Termination (protective)

### 8.1 Abandonment is a disposition, never a failure

**An operator MAY move any capability or quest to `abandoned` at any time. Abandonment MUST be recorded with a stated cause. It MUST NOT be recorded as a failure, as decay, as a regression, or as an unmet requirement. `abandoned` MUST be reachable from every state.** Prior verifications and completion records on an abandoned node MUST be retained and marked, never deleted, per POLARIS PL-15.

**Failure:** an abandonment recorded as a failure is rejected and is re recorded as `abandoned` with its cause. Deletion rather than marking is rejected at write time. A capability or quest closed with no disposition defaults to `abandoned`, never to `failed`.

TETHER F5 holds the discipline already, for interventions: closure inside the evaluation window is recorded as `abandoned` and never as `ineffective`. The application here is one sentence. A register that conflates a deliberate stop with a defeat poisons every decision that later reads it, and the operator is the reader.

### 8.2 Abandonment MUST NOT be priced

**An abandonment MUST NOT decrement any value, and an implementation MUST NOT make an abandonment record more costly to write than an addition.**

**Cost is decidable and is stated as three tests, so that the requirement binds friction and not only arithmetic. An abandonment record MUST NOT require more declared fields than a completion record, MUST NOT require more confirmations, and MUST NOT require a higher authority to write.**

**Failure:** an implementation whose arithmetic penalizes abandonment is non conformant, because it will produce a register that only ever grows. **An implementation failing any of the three cost tests is non conformant on the same terms, and the excess field, confirmation, or authority requirement is void.** The narrow arithmetic reading left the section's own named hazard open: three confirmation dialogs and two extra mandatory fields penalize abandonment exactly as a decrement does, and 8.2's rationale says that friction is what produces dishonest records rather than fewer abandonments.

TETHER 7.4 already holds that an implementation that makes downward transitions harder to record than upward ones will produce a register that only ever improves. The application: respec, meaning the deliberate abandonment of a capability in order to hold a different one, is the honest act, and any mechanism that makes the honest record the expensive one will produce dishonest records rather than fewer abandonments.

---

## 9. What QUEST Never Does (neither)

A consolidating section for a reader who arrived here intending to build a leveling product. Every entry is a pointer to its normative home and never a second statement of it.

| Refusal | Normative home |
|---|---|
| No scalar, and no total order over operators | Q-A1 |
| No prescribed capability, graph, quest, or criterion | Q-A2 |
| No authorization, no gate, no block, no rung, no crisis path | Q-A3 |
| No aggregate over records | 3.3 |
| No partial completion measure, no progress bar | 4.6 |
| No root, no depth, no cycle | 5.1 |
| No credential, and no non expiring verification | 6.3 |
| No streak, and no measure reduced by a missed period | 7.3 |
| No priced abandonment | 8.2 |
| No deletion in place of marking, excepting scheduled expiry under 5.5 | 8.1, 5.5, and POLARIS PL-15 |
| No coercive check resolved against a clinically directed record | 3.4 |

Three refusals have no other home and are stated here.

**The engagement mechanics, refused by shape rather than by schema.** Every refusal above is a refusal of a stored or computed value, and a product can ship every mechanic that makes a self improvement product a self improvement product without writing any of it to a register. **An implementation MUST NOT make the act of recording more rewarded than the act recorded. It MUST NOT prompt, notify, or remind on a cadence the operator did not declare. It MUST NOT render a lapse, an abandonment, or a missed period as a loss.**
**Failure:** a reward attached to the recording rather than to the thing recorded is rejected and is void, because it makes the register more valuable than the act, which is 7.3's first cost arriving without a counter. An undeclared prompt cadence is refused and no prompt is issued under it. A lapse rendered as a loss is re rendered as the state 2.6 defines, which is a true statement about the present that leaves the past intact.

**Who is bound.** **Courseware, coaching material, and any other artifact that presents an operator's own records back to them is an implementation** for the purpose of Q-A1, section 3.4, and section 10, and is bound by them. **Material that presents a curriculum, and does not present the operator's records, is an external requirement set under 5.4** and is bound by nothing here except the prohibition on merging it. Q-A2's boundary statement says QUEST is not a course, a coach, or a book; this says which of those three, in which posture, this document nonetheless reaches.

**Any transmission of capability, quest, completion, activity, verification, or item records to a party outside the operator's control is a boundary crossing**, whatever purpose the transmitting party declares. It is governed by the SPEAK and CONFIDE operator adapters, which are unwritten and are cited here as forward citations. It is at minimum K3 under TETHER 3.2, and it MUST NOT proceed without a declared custody floor.

**The rule extends from purpose to obligation, because a purpose is declared by the transmitting party about itself and therefore governs nobody on the other side.** **Any such crossing MUST carry a declared floor forbidding the recipient from computing a scalar over the operator or a comparison between operators from the transmitted records.** The floor travels with the records on POLARIS 12.1's model, where a refusal attached to a record crosses the boundary with it and **may be strengthened but never weakened**, and a recipient admitting the records inherits it.

**Failure:** a crossing with no declared custody floor, or with no declared comparison floor, is refused and the refusal is recorded. An implementation that transmits without both is non conformant at every tier. A recipient's request that the floor be relaxed is refused, and the refusal is recorded.

**Retention after the crossing is governed and is not left open.** **Records held by another party after a crossing MUST be enumerated under the RETAIN operator adapter, with a declared end of engagement disposition.** Without this, QUEST governs the moment of crossing and nothing after it, and an employer, coach, or credentialing institution may retain capability and completion records indefinitely and re serve them as a description of who the operator is. That is the accumulation attack the RETAIN adapter names, and KIT 3.4 already routes to RETAIN, so the family knows the route.

**Stated plainly, in the register RETAIN already uses: the floor is unenforceable against a recipient who breaches it.** Nothing in this document reaches inside another party's systems, no ledger the operator holds catches a comparison computed there, and **disclosure is the only control**. What the floor buys is that the obligation was stated, was recorded, and can be pointed at. A document that implied more would be lying about its reach.

An earlier draft stated one failure only, that a crossing with no declared custody floor is refused, which meant a crossing **with** a floor proceeded, including one whose declared purpose was comparison. A declared custody floor can license the export of everything needed to compute a leaderboard outside the implementation, and Q-A1 binds an implementation rather than a recipient. The commercially realistic misuse is not the operator's own leveling application.

A leaderboard is therefore not merely refused on design grounds. It is a boundary violation carrying a consequence class, and the class is the same one the rest of this stack assigns to publishing something that cannot be recalled.

---

## 10. The Alias Table (neither)

**Every game term used in this document MUST appear in the table below, mapped to the normative element it names, with its status marked. An implementation MUST NOT introduce a game term outside the table. A motto class term MUST NOT be cited as the basis of a decision, an authorization, a gate evaluation, or a refusal.**

**Failure:** a motto class term cited as grounds in any record is a defect detected in the disposition POLARIS applies to PL-04, and the citation is void, so the decision is re resolved on its actual grounds or it is not resolved. A term outside the table is undefined and any record using it is malformed. Admitting a new term is an RFC.

The table is closed rather than open for one reason. An open vocabulary acquires `prestige`, `ascended`, and `tier` from whatever product the reader last used, and each of those smuggles a total order back in through a word this document never defined.

Three statuses. **Normative** means the term is a defined term of this document, as normative as `envelope` or `observation`. **Motto class** means the term is non normative under POLARIS 7.3, kept because compression aids recall, and forbidden as grounds. **Refused** means the term appears here so that it is named and mapped, and MUST NOT appear in normative text or in any register.

**Two carve outs to the Refused status, copying KIT 2.12's wording, without which this document's own normative text is non conformant against this table.**

**`tier` remains available in its conformance tier sense, as a property of an implementation and never of a person**, which is how section 12 and `QS-01` use it. That is KIT 2.12's carve out verbatim, and it was omitted here in error.

**`rank` remains available only in the fixed phrase `rank one main quest`, as a property of a declaration and never of an operator**, which is how 2.2, 4.1, 4.4, and 4.5 use it, and which the Q-A1 boundary statement already licenses as an ordinal position of a declaration. **No other use of `rank` is permitted**, and `rank` as a property of an operator remains Refused.

**Failure:** text using `tier` for anything other than a conformance tier of an implementation, or `rank` outside the fixed phrase, is non conformant and MUST be rejected in review.

**Scope of the closure.** This table closes **this document's** normative text and the registers **this document** governs. KIT 2.12 closes KIT's, and the two tables are disjoint by construction: `quest` and `node` are QUEST's normative terms and are not KIT's, and `job` is KIT's and is not QUEST's. **An implementation conformant on both documents is not thereby non conformant on either**, and a term normative in the sibling document is not a term "outside the table" here. Merging the two into one family vocabulary annex is the cleaner end state and is an RFC, not a redrafting.

| Term | Maps to | Status |
|---|---|---|
| `quest` | A declared objective with a declared record of what is spent pursuing it (2.2) | Normative |
| `main quest` | An entry in the declared total order of 4.1 | Normative |
| `side quest` | A bounded, optional, declared detour with a bound and a termination condition (4.2) | Normative |
| `node` | One capability record in one declared graph (2.1) | Normative |
| `prerequisite` | A declared edge, which records and never authorizes (5.2) | Normative |
| `unlock` | The fact that every node with an edge into a node is `verified` (2.1). Grants nothing | Normative |
| `completion` | A record citing a criterion declared beforehand, and its evidence (6.1) | Normative |
| `item`, `kit`, `slot`, `loadout` | KIT's defined terms, imported by citation and not redefined here | Normative, in KIT |
| `skill tree` | The prerequisite graph of section 5.1, which has no root and no depth | Motto class |
| `respec` | Abandonment with a stated cause (8.1) | Motto class |
| `achievement unlocked` | A completion record was written (6.1) | Motto class |
| `map marker updated` | The main quest order changed, as a recorded act with a cause (4.1) | Motto class |
| `accepting a side quest` | A side quest record was written with its three required fields (4.2) | Motto class |
| `the tracker` | The capability register (3.1) | Motto class |
| `grinding` | Unconverted activity (6.2). MUST NOT be used as a verdict about an operator | Motto class |
| `level` | A set of per node states (2.6), and never a number | Refused |
| `grade`, `score`, `index`, `percentile` | Nothing. Q-A1 supplies no such value | Refused |
| `rank` | Nothing, as a property of an operator. Permitted **only** in the fixed phrase `rank one main quest`, where it is the ordinal position of a declaration (2.2, 4.1) | Refused, with the fixed phrase carve out above |
| `tier` | Nothing, as a property of an operator. Permitted **only** as a conformance tier of an implementation (section 12) | Refused, with the conformance carve out above |
| `unattended` | A reported reading over the drift comparison of 4.4. Never a quest status under 4.6 | Normative |
| `experience points`, `XP` | Nothing. Progression is recorded per node against completion (6.1) | Refused |
| `prestige`, `elite`, `mastery`, `ascended` | Nothing. Each is a total order wearing a noun | Refused |
| `leaderboard` | Nothing. A comparison crossing under section 9, at minimum K3 | Refused |
| `player` | The operator (TETHER 2.1) | Motto class |

Two entries do the document's teaching work, and a reader who reads only those two has understood the central refusal. **`level` maps to a set of per node states and never to a number.** **`grinding` maps to unconverted activity, and is never a verdict.**

The document's own name is motto class, per section 1.5, and this table governs it on the same terms as every other entry.

**Reversal note, non normative.** If the institutional readership argument wins, every normative term above is replaceable with a neutral one (capability, declared objective, bounded detour, equipped set) with no change to any requirement in substance. The table is what makes that a single editing pass rather than a redesign.

---

## 11. Failure Classes (each row inherits the label of its governing section)

| Code | Failure | Disposition |
|---|---|---|
| `QS-01` | A level, rank, score, index, percentile, or point total computed, stored, exposed, or transmitted | Non conformant at every tier. Q-A1. A scalar summary resolves `undefined`. A written scalar is marked withdrawn, never deleted |
| `QS-02` | A comparison computed between two operators | Resolves `incomparable`, never equal and never an ordering |
| `QS-03` | A cross operator comparison enabled by consent from any party | Still `incomparable`. Consent does not reach Q-A1 |
| `QS-04` | An aggregate over capability, quest, completion, or activity records | Refused. The report resolves to the list it would have summarized, or `undefined` |
| `QS-05` | A percentage complete, progress bar, or fractional remaining estimate | Rejected at write time. Specification text defining one is malformed |
| `QS-06` | A capability, graph, or example content named in specification text | Non conformant text. Rejected in review. Q-A2 |
| `QS-07` | A QUEST element cited as satisfying a gate, a rung, a re reference, or a check | The gate is recorded `unevaluated`, never `passed`. POLARIS PL-02 pattern |
| `QS-08` | An act blocked on an unmet prerequisite | Non conformant. The act proceeds; only the completion record fails closed |
| `QS-09` | A prerequisite cited as grounds for refusing an act, a role, an opportunity, or care | Void citation, and a Q-A3 violation. The refusal is re resolved on its actual grounds |
| `QS-10` | A rung, crisis path, or escalation substitute defined by a QUEST element | Non conformant. Inherited absolute 3 and Q-A3 |
| `QS-11` | A graph with a declared root, a depth or generation field, or a computed depth | Malformed. Rejected at write time |
| `QS-12` | A graph containing a cycle | Rejected. Never accepted with a warning |
| `QS-13` | A `held` value offered in the state vocabulary | Fails closed. Read as `claimed`. Implementation non conformant |
| `QS-14` | A verification whose reference source is `self-report` setting state `verified` | Rejected at write time. A node found in that state is corrected to `claimed`. Section 6.4 |
| `QS-15` | A verification with no expiry, or declared `indefinite` | Malformed. Rejected at write time |
| `QS-16` | A verification expressed as a property of the operator, or carrying an issuer authority over the operator | Rejected. Any decision citing it is re resolved |
| `QS-17` | Lapse conditioned on an event, a notification, a complaint, or the operator's judgment | Non conformant. Lapse is computed from the interval |
| `QS-18` | A `verified` state carried past its interval or its expiry | Reads `lapsed`. Not an error, a state |
| `QS-19` | A completion citing a criterion authored after the activity began | Malformed. DEFER 6.4 pattern |
| `QS-20` | Progression recorded against elapsed time, sessions, attempts, volume, or effort | Rejected at write time. An activity record does not become a completion |
| `QS-21` | Unconverted activity expressed as a count, ratio, or percentage, or characterized as an operator failing | Rejected. Specification text characterizing it is malformed |
| `QS-22` | A consecutive period counter, or any measure reduced by one missed period | Rejected at write time. Specification text defining one is malformed |
| `QS-23` | A capability verified on a performance using an undeclared item | Rejected at write time |
| `QS-24` | A declared substitute item under any KIT 5.2 disposition, `unconfirmed` under KIT 5.1, or `unknown` under KIT 6.3, with dependent capabilities still `verified` | Non conformant. Dependents leave `verified`, to `claimed` or `unheld`. Section 7.4 |
| `QS-25` | A main quest order absent, or containing a tie | Malformed declaration. POLARIS 6.1 disposition |
| `QS-26` | A main quest leaving the order with no `completed`, `abandoned`, or `superseded` disposition | Recorded `unresolved` and surfaced at the next review |
| `QS-27` | A side quest missing an objective, a bound, or a termination condition | Malformed. Rejected at write time |
| `QS-28` | A side quest past a ceiling with no recorded disposition | Governance defect, and remains one until dispositioned. Not a busy month |
| `QS-29` | A fourth overrun disposition defined | Non conformant. DEFER 10.1 shape |
| `QS-30` | A quest automatically closed, cancelled, suspended, de prioritized, or blocked | Non conformant. The automatic action is void |
| `QS-31` | A rebudget with no stated cause, or the rebudget records not enumerated with their causes | Governance defect. POLARIS 10.3 and PL-27. A **count** of rebudgets is itself a `QS-01` and `QS-04` defect. Section 4.3 |
| `QS-32` | An inversion undetected, or reported as passing when its meters are undeclared | Health invariant failure. An uncomputable comparison reports `uncomputable` |
| `QS-33` | Unattributed consumption discarded, or assigned to a default quest | The assignment is rejected. DEFER 6.5 and DF-15 |
| `QS-34` | An external requirement set merged into the capability register | Rejected at write time |
| `QS-35` | A capability record whose declaring party is not the operator, with no adoption record | Malformed. Rejected |
| `QS-36` | A guardian authored record retained past the return of root, exported, or published | Expired. Retention by default is non conformant |
| `QS-37` | An abandonment recorded as a failure, a decay, a regression, or an unmet requirement | Rejected and re recorded as `abandoned` with its cause |
| `QS-38` | An abandonment that decrements a value, or that is costlier to record than an addition | Non conformant |
| `QS-39` | A record deleted rather than marked withdrawn | Rejected at write time. POLARIS PL-15. **Scheduled expiry of a guardian authored record under 5.5 is expressly excepted and is deletion by design** |
| `QS-40` | Progression diminished by the passage of time, or `lapsed` rendered as absent, zero, expired, or lost | Non conformant. The decrement is void |
| `QS-41` | A game term used outside the closed alias table | Undefined term. Any record using it is malformed |
| `QS-42` | A motto class term cited as grounds for a decision, authorization, gate evaluation, or refusal | The citation is void. POLARIS PL-04 disposition |
| `QS-43` | A capability record missing a required field, or carrying a task predicate that requires judgement | Rejected at write time. DEFER 4.3 |
| `QS-44` | Capability, quest, completion, activity, verification, or item records crossing to a party outside the operator's control with no declared custody floor, or with no declared floor forbidding the recipient from computing a scalar or a comparison | Refused, and the refusal recorded. K3 minimum under TETHER 3.2. The floor travels on POLARIS 12.1's model and may be strengthened, never weakened. Section 9 |
| `QS-45` | Records held by another party after a crossing, not enumerated under the RETAIN operator adapter with a declared end of engagement disposition | Non conformant at Tier 3. Section 9 |
| `QS-46` | A coercive check resolved against a clinically directed record as a pass or a fail rather than `out-of-scope`, or consumption on a clinically directed record routed into the 4.4 denominator or the 4.5 comparison | Returns `out-of-scope`. Never a pass, never a fail. The comparison is recomputed with the record excluded. Section 3.4 |
| `QS-47` | A quest, capability, or consumption record whose clinical direction field is absent or `unknown`, treated as non clinical | Handled as clinically directed until the operator declares otherwise, and surfaced `unconfirmed`. Fail closed toward protection. Section 3.4 |
| `QS-48` | A value derived from any record in the capability register written to, mirrored into, or cited as the operator register | Rejected at write time, on the TETHER F1 pattern. A decision citing it is re resolved. Section 3.2 |
| `QS-49` | A drift comparison's computed sums displayed, stored, or transmitted | Rejected at write time and void where written. Only the disposition is exposed. Sections 4.4 and 4.5 |
| `QS-50` | `unattended` written as a quest status under 4.6 | Rejected at write time. It is a reported reading and not a state. Section 4.4 |
| `QS-51` | A change to the main quest order with no stated cause | Rejected at write time. Section 4.1 |
| `QS-52` | A section 4, 5.3, or 6.2 check evaluated with no declared evaluation interval, or with a lapsed one, and reported as passing | Reported `uncomputable`, never as passing. Sections 4.4, 4.5, 5.3, 6.2 |
| `QS-53` | A verification citing reference source `instrument` without the sensing item and its calibration currency, or a node reading `verified` on output recorded `unknown` under KIT 6.3 | Malformed and rejected at write time. The node reads `claimed` or `unheld`, and the reading is corrected rather than annotated. Section 6.3 |
| `QS-54` | An abandonment record requiring more declared fields, more confirmations, or a higher authority than a completion record | Non conformant. The excess requirement is void. Section 8.2 |
| `QS-55` | An enumeration's cardinality rendered as a summary value, header figure, badge, or chart axis | The count is void and the list is returned in its place. Section 3.3 |
| `QS-56` | A verification created with no citation of the completion record and criterion it discharged | Malformed. Rejected at write time. Section 6.1 |
| `QS-57` | The self test not executed within its declared interval | The suite reports a red check and MUST NOT be reported as passing. Section 12.3 |

---

## 12. Conformance (12.1 and 12.2 mixed; 12.3 protective by construction)

### 12.1 Tier requirements

Three tiers, named to mirror TETHER. Requirements are indicative in this draft.

**Tier 1, Attended.** The capability register exists and is separate from the operator and instrument registers. Every capability record carries a decidable task predicate, a verification interval, and a clinical direction field whose absence is handled as clinically directed per 3.4. Main quests are declared as a total order with no ties, and every order change carries a stated cause. Every side quest carries an objective, a bound, and a termination condition. No monotone operator scoped numeric field, no aggregate outside the two carve outs of 3.3, and no partial completion measure appears anywhere.

**The tiers are cumulative, and Tier 2's drift computations are not a Tier 1 violation.** Tier 1's refusal of aggregates is the refusal 3.3 states, which now carries the section 4 carve out explicitly: the drift comparisons are computed over one operator's own records, expose only a boolean disposition, and their sums are never displayed, stored, or transmitted. Without that carve out no implementation could be Tier 2 conformant without failing Tier 1, and `QS-04` and `QS-31` gave opposite dispositions for the same object.

A Tier 1 implementation may verify nothing. What it may not do is hold a register that cannot say what a capability was for or when it was last exercised.

**Tier 2, Referenced.** Adds the clocks and the evidence discipline. Lapse is computed from the declared interval rather than noticed. Self report is recorded `claimed` and never `verified`. Every verification carries an expiry. Inversion and unattributed consumption are computed over a declared window, per declared meter, on a declared evaluation interval, with their sums never displayed, stored, or transmitted. Item dependencies are declared under 7.4 and every KIT 5.2 disposition propagates. Verifications citing reference source `instrument` name the sensing item and its calibration currency per 6.3. Overruns carry one of the three dispositions and rebudget records are enumerated with their causes.

**Tier 3, Governed.** Adds the boundary and the parties other than the operator. Guardian authored records expire at the return of root unless adopted. External requirement sets are recorded, attributed, and never merged. Any crossing of capability, quest, completion, activity, verification, or item records to a party outside the operator's control is governed by the **SPEAK, CONFIDE, and RETAIN** operator adapters, with a declared custody floor and a declared floor forbidding the recipient from computing a scalar or a comparison. **Records held by another party after a crossing are enumerated under the RETAIN operator adapter with a declared end of engagement disposition.** The dead prerequisite check of 5.3 is reported on its declared evaluation interval.

### 12.2 Health invariants

Each is a count of defects and is labelled a conformance check, per the carve out in 3.3.

| Invariant | Target |
|---|---|
| **Monotone operator scoped numeric fields** in any register, per the Q-A1 discriminator | Zero |
| Cross operator comparisons computed | Zero |
| **Records crossing to a party outside the operator's control with no declared custody floor, or with no declared floor forbidding the recipient from computing a scalar or a comparison** | **Zero** |
| Records held by another party after a crossing, not enumerated under the RETAIN adapter with an end of engagement disposition | Zero |
| Aggregates outside the two labelled carve outs of 3.3 | Zero |
| Enumeration cardinalities rendered as a summary value | Zero |
| Drift comparison sums displayed, stored, or transmitted | Zero |
| Values derived from the capability register written to or cited as the operator register | Zero |
| **Coercive checks resolved against clinically directed records as a pass or a fail rather than `out-of-scope`** | **Zero** |
| Quest, capability, or consumption records with an absent or `unknown` clinical direction field, treated as non clinical | Zero |
| Nodes reading `verified` past their interval or expiry | Zero |
| Nodes reading `verified` on self report alone | Zero |
| Nodes reading `verified` on output recorded `unknown` under KIT 6.3 | Zero |
| Verifications without an expiry | Zero |
| Verifications created with no citation of a completion record and criterion | Zero |
| Abandonments recorded as failures | Zero |
| Abandonment records costlier to write than a completion, by fields, confirmations, or authority | Zero |
| Main quest order changes with no stated cause | Zero |
| Side quests past a ceiling with no disposition | Zero |
| Undetected inversions | Zero |
| Rebudgets with no stated cause | Zero |
| Rebudget records | Reported as an enumeration with their causes, never as a count |
| Unattributed consumption | Reported as an enumeration, and compared against the rank one main quest |
| Untested prerequisite edges | Reported as a signal, never as a defect |
| Nodes with unconverted activity above the operator's declared threshold | Reported as an enumeration of named records, never as a ratio |
| Records deleted rather than marked withdrawn, excepting scheduled expiry under 5.5 | Zero |
| Uncomputable inversion comparisons | Reported `uncomputable`, never as passing |
| Section 4, 5.3, or 6.2 checks with no declared or a lapsed evaluation interval, reported as passing | Zero |

### 12.3 Self test

A conformant implementation MUST provide a self test **and MUST execute it on a declared interval**. It is one page, every check is mechanically decidable, and **no check is one an operator could satisfy by declining care or by consuming less on clinically directed care**, which section 3.4 now supplies the mechanism for rather than only the claim.

**Failure:** a self test not executed within its declared interval, or with no declared interval, **reports a red check and MUST NOT be reported as passing**, matching POLARIS 4.5 and TETHER F7's treatment of a stale escalation path. A suite that need never run is a refusal that is indistinguishable from an inert one, which is 5.3's own imported reasoning applied to this document's own enforcement. Each check seeds the condition and asserts refusal or detection, and each MUST exit non zero on failure.

1. A request for a scalar summary over the register, asserting `undefined`
2. A comparison between two operators, asserting `incomparable`
3. The same comparison offered with the consent of both, asserting still `incomparable`
4. An aggregate over capability records, asserting refusal and the list returned in its place
5. A graph with a declared root, asserting rejection
6. A graph containing a cycle, asserting rejection rather than a warning
7. A state vocabulary offering `held`, asserting the value reads `claimed` and the implementation reports non conformant
8. A node recorded `verified` on self report alone, asserting downgrade to `claimed`
9. A `verified` node read after its interval has elapsed, asserting `lapsed`
10. A verification submitted with no expiry, and one declared `indefinite`, asserting rejection of both
11. A completion citing a criterion authored after the activity began, asserting rejection
12. An activity record submitted as a completion, asserting rejection
13. A streak counter written to the register, asserting rejection
14. A capability verified on a performance using an undeclared item, asserting rejection
15. A declared substitute item marked `lost`, asserting every dependent capability left `verified`
15a. The same, with the item marked **`released`**, asserting every dependent capability left `verified`. `released` is the disposition an implementer will most plausibly argue should not fire, which is why it is the one seeded
16. An act attempted with an unmet prerequisite, asserting that the act proceeded, that the outcome was recorded `attempted-above-prerequisite`, and that no completion record was written
17. A side quest past its windowed aggregate ceiling and left undispositioned, asserting a governance defect
18. The same quest auto closed by the implementation, asserting non conformance and a void closure
19. A side quest whose windowed consumption exceeds the rank one main quest's, asserting the main quest reported `unattended`
20. Consumption offered a default quest, asserting refusal and an `unattributed` record retained
21. An external requirement set offered for merge into the capability register, asserting rejection
22. A guardian authored record read after the return of root with no adoption, asserting expiry
23. An abandonment offered as a failure, asserting it is re recorded as `abandoned` with its cause
24. A game term used outside the alias table, asserting the record is malformed
25. **A coercive check, from 4.3, 4.4, 4.5, or 6.2, resolved against a clinically directed record.** Assert it returns `out-of-scope`, assert specifically that it returns neither a pass nor a fail, and assert that consumption on that record was excluded from the 4.4 denominator and the 4.5 comparison and that the exclusion was reported. Failure: `QS-46`
26. A quest record, a capability record, and a consumption record each seeded with the clinical direction field **absent**, and separately declared `unknown`. Assert each is handled as clinically directed, assert each is surfaced `unconfirmed` on that field, and assert none is treated as non clinical. Failure: `QS-47`
27. **A comparison crossing offered with no declared custody floor, and separately one offered with a custody floor but no floor forbidding the recipient from computing a scalar or a comparison.** Assert refusal in both cases and assert a recorded refusal in both. Failure: `QS-44`
28. A motto class term cited as grounds for a decision. Assert the citation is void and the decision is re resolved on its actual grounds or left unresolved. Failure: `QS-42`
29. A record offered for deletion in place of marking withdrawn, and separately a guardian authored record reaching its 5.5 expiry. Assert the first is rejected and the second is deleted without tripping the deletion check. Failure: `QS-39`
30. An abandonment record required to carry more declared fields, more confirmations, or a higher authority than a completion record. Assert non conformance and assert the excess requirement is void. Failure: `QS-38` and `QS-54`
31. A rebudget written with no stated cause, and separately a report returning a count of rebudgets. Assert the first is a governance defect and assert the second is refused with the enumeration returned in its place. Failure: `QS-31`
32. A value derived from a capability record offered to the operator register, seeded as a completion record, as an `abandoned` disposition with its cause, and as a `lapsed` state. Assert all three writes are rejected. Failure: `QS-48`
33. A verification whose reference source is `self-report` offered with state `verified`. Assert the write is rejected rather than accepted and downgraded later. Failure: `QS-14`
34. A verification whose reference source is `instrument`, supported by output recorded `unknown` under KIT 6.3. Assert it does not produce `verified` and that the node reads `claimed` or `unheld`. Failure: `QS-53`
35. An inversion comparison run with no declared evaluation interval, and separately with a lapsed one. Assert both report `uncomputable` and assert neither reports as passing. Failure: `QS-52`
36. A report rendering the cardinality of a returned enumeration as a summary value. Assert the count is void and the list is returned in its place. Failure: `QS-55`

Checks 9, 15a, 17, 19, 20, and 35 require elapsed time and accumulated windows. A simulated clock is conformant, per DEFER 15.4, provided the implementation under test reads time only through the source the simulation controls. A test that advances a clock the production code does not read has tested a different system, and its pass is not evidence.

---

## 13. Versioning and Governance (neither)

Semantic versioning on the specification, per `CONTRIBUTING.md`. Substantive changes go through an RFC.

The state vocabulary of 2.6, the quest status vocabulary of 4.6, the three overrun dispositions of 4.3, and the alias table of section 10 are closed sets. An implementation MUST NOT add a value to any of them, MUST NOT define a fourth overrun disposition, and MUST NOT introduce a game term outside the alias table.

**Three readings are not additions to a closed set and are named here so that nobody records them as one.** `unresolved` (4.1) marks a change to the main quest order, `unverifiable` (6.1) is a property of a node's evidence, and `unattended` (4.4) is a reading over the drift comparison. **None of the three is a state under 2.6 or a status under 4.6, and none may be written into a state or status field.** The alias table's closure is scoped to this document's normative text and the registers this document governs, per section 10, and a term normative in KIT is not a term outside this table. Admitting a term or a value is an RFC, and the RFC is the cost that keeps the vocabulary from acquiring a total order by accretion.

While Status reads Draft, section numbering, requirement identifiers, and failure class codes are unstable and MUST NOT be cited as stable by any other document in this stack.
