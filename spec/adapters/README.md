# Operator adapters

**Status:** Draft. Six planned annexes, none written. This file states each adapter's thesis and the one thing that would otherwise be got wrong, so that the set can be reviewed as a set before any of it is drafted.
**Design note:** `design/0005-meat-suit-interface.md`, non normative.

---

## What an adapter is

The six governance documents in this stack are written for a subject that is a folder. TETHER introduces a subject that is a person and an instrument, and HABITAT introduces the environment that instrument runs in. Each governance document has a true and non obvious reading against that subject, and **none of those readings is reachable by substituting nouns.** An adapter is where the reading is written down.

An adapter is a **normative annex**, not a new specification. It binds its base document's machinery to the operator subject and states three things: what carries over unchanged, what changes and why, and the one thing an implementer would otherwise get wrong. It is short, because the base document does the work.

An adapter inherits precedence and never creates it. POLARIS for operators still holds the highest precedence to forbid and none to permit. An instrument condition or an environment mismatch bounds what an operator may be authorized to do. It is never a permission, never a satisfied check, and never an excuse offered after the fact.

Every adapter inherits TETHER's four absolute requirements without restating them, in particular clinical precedence and the identity firewall.

Naming: `spec/adapters/<BASE>-for-operators-v1.0.md`.

---

## The base documents that delegate into this set

**TETHER** and **HABITAT** are the two documents the adapters were originally conceived alongside. **KIT**, **QUEST**, and **BEARING** are the three drafted afterward, and all three delegate into this set rather than duplicating it. Each names an adapter as the owner of a classification, a routing, or a retention rule, and each is written so that it gains no rule of its own when the adapter lands.

The obligations below are **inbound**: they are what KIT, QUEST, and BEARING already require of an adapter, collected here so that the set can be reviewed as a set before any of it is drafted, and so that no adapter author has to read three long specifications to find out what is expected of them. **Nothing here is a new requirement.** Each is a pointer to the normative home in KIT, QUEST, or BEARING.

| Adapter | Inbound obligation | Normative home |
|---|---|---|
| **CONFIDE** | The custody class of an item's transmitting endpoint, and the provider record justifying it. Until this adapter lands, every transmitting endpoint is C4 Open by construction and no stronger class may be claimed | KIT 9.1 |
| **CONFIDE** | The custody floor on a comparison crossing of capability, quest, completion, activity, verification, or item records | QUEST 9 |
| **CONFIDE** | **The custody class of a routing endpoint that is a human recipient**, which the class vocabulary does not currently describe: CONFIDE 2.1 defines C4 Open as a third party operating a model under consumer terms, and CONFIDE 2.4's unknown posture rule is scoped to a provider's posture field. BEARING declares an interim floor in its own terms rather than borrowing C4, because reading a clinician as C4 would put an instrument referral into a matrix cell CONFIDE 5.1 reads prohibit. **Whether a human recipient is inside the provider vocabulary at all, and if so which cell governs an instrument raise crossing to a clinician, is a matrix exception only CONFIDE can grant**, and it is the first thing this adapter has to settle | BEARING 8.5 |
| **TRACE** | **The derived number subject rule as it reaches BEARING's own outputs**: a raise, a ladder finding, a docket disposition, and a calibration state are each derived from a monitor over the operator's records, and none of them may be adopted as an observation into the operator, instrument, fault, inventory, or capability registers. Three of the four are strings rather than numbers, which is why the rule is stated over derived values and not over scalars | BEARING 14.3 |
| **RETAIN** | **Post crossing retention of referral records.** An instrument raise routed to a qualified human crosses by design, carrying fired signals, functional impact evidence, a baseline comparator, and four ladder findings, and what the recipient keeps afterward is enumerated with a declared end of engagement disposition | BEARING 14.7 |
| **POLARIS** | **Declared priorities as criteria.** An operator's declared priorities, together with their statement of what evidence in the record would count as serving each, are the object every alignment monitor measures against. A declared priority with no such statement is not measurable and reports `unknown-undeclared` rather than being inferred from conduct | BEARING 2.5, BEARING section 12 |
| **TRACE** | The artifact class of an item that retains data about the instrument, and the registration of its artifact roots and retention policy | KIT 9.1 |
| **TRACE** | **The derived number subject rule.** A derived number whose subject is the operator's capability, or the operator and kit composite, rather than a measured property of the instrument, MUST NOT be adopted as an observation. This rule is drawn here rather than in either sibling because KIT 9.2's adoption door has no scalar filter, Q-A1's subject is a number over an operator, and K-A3 forbids KIT from citing Q-A1 at all. Drawn once here, both siblings cite one rule and K-A3 is not breached. A vendor readiness score, fitness age, or recovery index is the case | KIT 9.2, Q-A1 |
| **RETAIN** | The parties K-A1 and KIT 3.4 route off the inventory: agents, software, and any identity that can hold a register or consent, recorded as an engagement rather than as a possession | KIT K-A1, KIT 3.4 |
| **RETAIN** | **Post crossing retention.** Records held by another party after a QUEST section 9 crossing, enumerated with a declared end of engagement disposition. This is where the identity firewall becomes enforceable against parties other than the operator, and it is the difference between governing the moment of crossing and governing what happens after it | QUEST 9, QUEST 12.1 Tier 3 |
| **DEFER** | **Cite KIT section 8 for the budget object rather than duplicating it.** The slot, the meter, the bound and its two ceiling halves, and the loadout review interval are already specified there | KIT 8, KIT 13 |
| **DEFER** | The handover grant a party declared as an item is routed to | KIT K-A1 |
| **SPEAK** | Agreements a party routed off the inventory is recorded under | KIT K-A1, KIT 3.4 |
| **SPEAK** | The comparison crossing, and the floor that travels with the crossed records on POLARIS 12.1's model, strengthenable and never weakenable | QUEST 9, BEARING 8.5 |
| **POLARIS** | Capability conditioned refusals, which QUEST 1.4 routes here rather than defining | QUEST 1.4, Q-A3 |

Five of the six carry an inbound obligation from KIT or QUEST, and **four of those five carry a further one from BEARING**, which routes to CONFIDE, TRACE, RETAIN, and POLARIS. **SPEAK carries an inbound obligation from BEARING as well**, at BEARING 8.5, which requires the comparison floor that travels with a crossed record on POLARIS 12.1's model, strengthenable and never weakenable. **All six therefore carry an inbound obligation before they are written.** That is worth stating plainly, because all three siblings are conformant today by carrying the fields and applying the base documents directly, and an adapter author who reads this table will find the obligations already scoped rather than open.

**BEARING's rows are the reason this file exists.** An adapter author who drafted CONFIDE, TRACE, RETAIN, or POLARIS for operators without knowing that BEARING routes to them would have written the adapter to a subject it does not cover, which is the precise failure the inbound table is here to prevent.

---

## The six

### CONFIDE for operators
**Draft first.** Who may process instrument telemetry, under what custody.

The custody ladder transfers almost unchanged. Wearables, health applications, laboratories, patient portals, insurers, and employers are all endpoints operating under contracts, a class describes an endpoint under a contract and never a company, and chains take the weakest class.

**What would otherwise be got wrong:** an undeclared retention posture is C4 open, and most consumer health telemetry is C4 by default. Operators routinely believe their instrument data is held at a custody class it is not. The adapter's most useful output is a table and the discipline to stop there.

This is the adapter that is immediately practical, requires no metaphysics, and nobody has written.

### TRACE for operators
**Draft second.** The residue of health tooling: wearable histories, application state, portal records, imaging, and every derived score.

The six artifact classes map with almost no strain, and the protected artifact rule carries directly.

**What would otherwise be got wrong:** a **derived score is an A2 derived artifact, not an observation.** It is adopted deliberately into the instrument register or it expires. A score computed once from a model nobody can inspect, then re served to the operator as a fact about them, is exactly the accumulation problem TRACE exists to name, and it is the mechanism by which a number becomes a permanent property of a person.

### RETAIN for operators
**The one with teeth. Draft carefully.** What a clinician, coach, employer, or institution keeps about the instrument, and what they keep when the engagement ends.

**What would otherwise be got wrong:** this is where the identity firewall becomes enforceable against parties other than the operator. A retained finding, held by an institution and re served to the operator, is the accumulation attack in the base document, and the operator holds no ledger that can catch it. The base document is already honest that no ledger catches cross domain learning and that disclosure and consent are the only control. The same is true of a diagnosis, which is the most consequential retained record most people will ever be the subject of, and saying so plainly is the adapter's job.

**The risk in this adapter is the reason to write it carefully.** One careless sentence turns it into an argument against clinical record keeping, which would be wrong and would be dangerous. TETHER 4.3, on what the firewall does not forbid, governs every paragraph, and clinical precedence applies with full force.

### DEFER for operators
Who may decide what about the instrument: operator root, clinician envelope, emergency path, guardian.

Carries the shifted consequence ladder from TETHER 3.2, where the classes are redefined for a system with one instance, no restore, and a cumulative history.

**What would otherwise be got wrong:** both halves have to be held at once. Clinical authority is real, bounded, and must not be undercut, and root remains with the operator. A document holding only the first half is a compliance manual. A document holding only the second is reckless. **Guardianship is the one case where root genuinely moves**, and it needs its own section covering who holds it, on what basis, what bounds it, and how it returns, rather than an exception clause.

### POLARIS for operators
The operator's purpose, refusals, and loyalty order regarding their own instrument. Refusals about the instrument are the most testable refusals a person owns, because compliance is observable on a daily interval, which makes this a good teaching entry point into the whole POLARIS model.

**What would otherwise be got wrong:** the loyalty order must be published including where the operator's own instrument sits in it, and an operator whose declared order puts the instrument last has declared something true and useful. A document that quietly forbids that answer has stopped specifying and started prescribing a life.

**One constraint carried from the reference implementation.** The author's alignment work places a **given purpose** above POLARIS, received rather than chosen, and a 2026-08-26 ruling deliberately left it unnamed pending a neutral name. The adapter must not name it either, and must not quietly resolve an open question by needing a word for it.

### SPEAK for operators
**Draft last.** Disclosure between operators, and between an operator and a clinical or institutional party. An instrument record crossing to another party is an utterance under an agreement carrying a custody floor.

Consent is the agreement: directional, scoped, revocable.

**What would otherwise be got wrong:** the base document's rule that the floor travels with the record and may be strengthened but never weakened is the rule most people assume governs their health disclosures, and it frequently does not. Naming the gap is most of the value.

**Sequencing:** SPEAK itself is a skeleton that locks later than the rest of the family, so this adapter cites a moving target until it locks. It is drafted last for that reason and not because it matters least.

---

## Order and rationale

| Order | Adapter | Why here |
|---|---|---|
| 1 | CONFIDE | Highest practical value, cleanest transfer, no prerequisites |
| 2 | TRACE | Same, and it establishes the derived score rule the others rely on |
| 3 | RETAIN | Needs the derived score rule, and gives the identity firewall its reach |
| 4 | DEFER | Needs TETHER's consequence ladder settled first |
| 5 | POLARIS | Needs the others to point at, and touches an open naming question |
| 6 | SPEAK | Blocked on SPEAK locking |
