# Indications and Routing: design note for BEARING

**Status:** Design note. Non normative. Options and open questions belong here, not in `spec/`.
**Author:** Spencer Thornock
**Written:** 2026-08-30
**Covers:** `spec/BEARING-v1.0.md`.
**Companion to:** `design/0005-meat-suit-interface.md`, which proposed the family, and `design/0006-operator-family-integration.md`, which describes it. This note carries the reasoning behind the fifth document, which the specification itself cannot hold.

---

## 0. What this note is for

BEARING borrows its machinery from a clinical classification manual and then refuses that manual's central act. A specification cannot explain that. It can state a requirement and its failure mode, and every sentence explaining why a borrowed mechanism was taken, altered, or refused is prose that belongs in `design/` under the repository's own precedence rule.

This note does five jobs and no others.

It states **why the document routes rather than classifies**, which is the decision every other decision in BEARING follows from. It records **what was borrowed from the source discipline**, mechanism by mechanism, with what changed on import. It records **what was deliberately rejected**, with the reason for each, because a refusal without a reason is reversed by the first reader who finds the refused thing convenient. It records **the non clinical precedents**, which are where most of the actual machinery came from and which a reader will otherwise assume were invented here. And it states **the safety analysis**: the misuses the document is written against, the requirement that closes each one, and the ones that are not closed.

Three constraints govern everything below.

**Nothing here is normative.** Where this note states a rule, it is either quoting BEARING or proposing something nothing owns yet, and every proposal is an open question in section 6.

**No condition is named anywhere in this note.** The specification refuses to name one at 16.1 and refuses to let a guide name one at 16.3, and a design note that named one would have put the content back into the repository through the door marked non normative. Where a published finding is about a specific diagnostic category, the category is described by its structural role and never by its name. This costs nothing: every finding used below is a finding about **mechanism**, and the mechanism is what transfers.

**The clean room rule is sharper here than anywhere else in the family.** The reference implementation for this subject is not a vault, it is a person's history. The transcripts are read and the general rule is written. Nothing in `spec/` and nothing in this note derives its text from a personal disclosure, and section 5 states the safety consequence of that discipline rather than an account of what motivated it.

---

## 1. Why this document routes rather than classifies

### 1.1 The choice, stated once

A system that reads a person's records and notices something can do one of two things with what it noticed. It can **classify**, producing a name for the pattern and attaching it to the person. Or it can **route**, producing an event addressed to a party who can act, carrying the evidence and no conclusion.

BEARING routes. The abstract states it in the first line and the whole document is that decision propagated: no label, no condition name, no category, no code, no screening instrument, a raise that carries evidence rather than a conclusion, and a lifecycle with no word meaning resolved.

The choice was not made on taste. It was made because a classifier has four failures that a router does not have, and because the one advantage a classifier has is unavailable in this setting.

### 1.2 The four failures a classifier has and a router does not

**A category name does not describe its members.** The source discipline's criteria sets are polythetic: a threshold count of features out of a larger listed set qualifies, and no individual feature is either necessary or sufficient. The consequence is arithmetic and it is severe. Where a definition admits any sufficient subset of a larger set, two records that share **no feature at all** are reported identically, and one published personality category admits 256 distinct sign and symptom combinations. So the name is not a description. It is a pointer to a set whose members may have nothing in common, and anyone who reads the name and believes they know what is in the record has been misled by the format.

BEARING keeps the mechanism and drops the name. 5.3 requires that every raise carry the signals that fired, each with its reference source, and states the reason in those terms: a threshold crossed, reported without the signals that crossed it, is a word that does not describe its instances.

**A label persists and travels after the condition that produced it has gone.** This is the harm the identity firewall exists for, and the source discipline's own structure makes it worse rather than better, because the portable token is not the narrative formulation but the code. The code travels into claims systems, insurance records, disability determinations, school records, court filings, and employment screening. The formulation does not travel. **Any structure that mints a code has minted a permanent, transferable, adversarially usable label, whatever the surrounding text says.**

BEARING has no code and could not acquire one, because 5.7 forbids a field named `code`, `category`, `diagnosis`, `condition_name`, `profile`, or `pattern`, 5.1 closes the schema so there is nowhere to put one, and 5.11 gives every raise a mandatory expiry with `indefinite` refused outright. **An event with an expiry is not an attribute.**

**A classification's reliability is a property of the observation regime, and the regime here is the worst available one.** Section 1.3 below.

**A classifier has to be right, and a router has to be loud.** These are different jobs with different error postures, and a system built for one is dangerous when used for the other. A classifier that fires too readily manufactures conditions. A router that fires too readily wastes a human's attention, which is a real cost with a documented failure mode and is not the same kind of cost.

### 1.3 The observer problem, and the ceiling it sets

The source discipline assumes a **trained party applying criteria to another person**. BEARING has an operator applying criteria to themselves, through the very instrument that may be at fault. That is TETHER 1.2 arriving in the alignment domain and it is the honest reason the document routes.

The published evidence sets the ceiling and the ceiling is low.

The manual's own field trials used a **test and retest** design: the same patient interviewed independently by two clinicians on two separate occasions, four hours to two weeks apart, using their usual clinical methods. Reliability was reported as an intraclass kappa. Of the diagnoses tested, five reached the band the manual called very good, nine good, six questionable, and three unacceptable, and two fell below kappa 0.20 outright. The bands themselves had been published in advance and were substantially more permissive than the standards they displaced: an earlier and widely used convention held that kappa above 0.7 was only satisfactory and below 0.5 was poor, while the newer bands treated 0.40 to 0.59 as good and argued that a realistic goal for psychiatric diagnosis was 0.4 to 0.6, with 0.2 to 0.4 acceptable. A planned second phase in routine, non academic clinical settings was cancelled as time ran out.

The defence of those figures is real and is the more important half for this document's purposes. Earlier field trials estimated reliability by having two raters score **the same recorded interview**, which measures only whether raters interpret identical elicited information identically. The decisive study estimated both methods in the same patient sample: the recording method gave a mean kappa of 0.80, and independent re interview of the same people gave 0.47. **The criteria did not change. The regime did.** The likeliest reading is that the newer trials revealed long standing unreliability that the older method had been concealing.

Two things follow, and BEARING states both.

**15.2 requires every reported figure to state the observation regime that produced it**, on the ground that a figure quoted without its regime is not a weaker figure but an ambiguous one, and that the ambiguity always resolves in the flattering direction when a reader supplies the missing half.

**1.5 states the ceiling for a self applied set and states it as an unknown rather than as a number.** The expected agreement of a self applied criteria set is unknown. There is no reason to believe it exceeds the worst published figure for trained parties applying structured criteria to someone else, and every reason drawn from TETHER 1.2 to believe it is lower, because the party applying the criteria and the party whose condition is in question are the same party and share the same degraded reference.

**A system with that ceiling may not conclude.** It may notice, it may carry what it noticed to someone with training and access it does not have, and that is the whole of what it may do. Routing is not a modest version of classifying. It is the only honest act available at this reliability.

### 1.4 The governing analogy, and the four consequences that became structure

**A smoke detector does not diagnose the fire. It makes noise.** Its job is to be loud, early, wrong sometimes, and to summon someone qualified. Its job is never to determine what is burning.

The analogy is in the abstract because four structural decisions follow from it and a reader who meets them as four separate requirements will not see that they are one idea.

**Inputs are records that already exist** (4.2). A smoke detector does not interview the building.

**The trigger is automatic and periodic, never invoked** (4.4). A detector you have to press is a detector that reports the state of the building at the moment somebody already suspected something.

**The output is an emitted call out addressed to a human** (section 5), and never a finding the operator reached, a state the operator adopted, or a value stored about them.

**The failure posture is that a monitor which cannot run, has no data, or is out of date is `unknown` and is itself a raise** (4.10). **Silence is never health. A dead smoke detector is a fault.**

### 1.5 The one event the whole design is built around

BEARING 3.2 names it and it is the most useful sentence in the document for a reviewer: **the entire misuse surface concentrates in one event, a raise becoming consequential.** A purity ladder needs a raise to gate a capability. A screening use needs a raise to inform a decision about a person. A shame engine needs a raise to cost something.

That is why B-A1 is a leaf rule rather than a promise, and why 0006 section 1.2 treats it as the family's strongest structural property. If nothing above may read a raise, none of the three can be built, and non coercion becomes a property of the dependency graph that a reviewer confirms in one pass over the other documents without reading BEARING at all.

### 1.6 Why the two arms are one document

The abstract states it and it is worth recording why the alternative was rejected. An Arm A adoptable without an Arm B is **an unowned machine counting a person's alignment**, which is the artifact this whole design exists to prevent. Publishing the monitor specification separately from the review specification would have made that artifact conformant, and it would have been the version a vendor shipped, because the monitors are the part that automates and the review is the part that requires a person to sit down.

The split itself is the safety property: **the machine counts, the human decides.** It is not an original rule. The reference implementation's own alignment ledger already worked this way, reporting days spent off the stack as days spent off the stack, with no agent adding encouragement, scolding, or a motivational reading, and the author drawing the conclusion. B-A2 is that practice made normative and made structural.

---

## 2. What was borrowed, and what changed on import

The source discipline is a criteria manual, and the reason to borrow from it is that it is the most heavily scrutinized apparatus in existence for turning observations about a person into a decision, including scrutiny of its own failures by its own authors. Almost everything BEARING needed had already been tried there, and most of it had already broken there in public.

Each row below states the mechanism, what it does in the source, where it lands in BEARING, and what changed.

| Mechanism | What it does in the source | Where it lands | What changed on import |
|---|---|---|---|
| **Polythetic thresholds**, n of m rather than all of m | Buys robustness to item level rater disagreement, because the count survives disagreement about any single feature | `persistence` (4.5), multi source satisfaction (4.8), and the trip condition generally | The threshold survives; **the category name does not**. 5.3 requires which signals fired to travel with the raise, because a polythetic definition admits records sharing no feature and reports them identically |
| **Four structurally distinct encodings of time**: minimum duration, within window density, baseline change, developmental onset | Separates a bad week from a condition, an intermittent occurrence from a sustained one, a deterioration from a stable trait, and a lifelong pattern from a new one | 2.3's four time requirements, kept structurally distinct and separately declared: `window`, `interval`, `persistence`, `duration` | Three of the four transfer. **Developmental onset is not imported at all**, because it is a fact about a person's history and BEARING stores no facts about persons. The baseline change clause transfers as 15.4 and 11.3, which is the strongest thing taken from this row |
| **The baseline change clause**, comparing a person to their own prior state rather than to a population norm | The manual's structural acknowledgement that a stable long standing trait is not the same phenomenon as a deterioration | 15.4 for the fault lane, 11.3 for the spectrum lane, both requiring the comparator resolve against the operator's own prior record | **Strengthened into a prohibition.** A comparator drawn from a population norm, a cohort, a target, or any value the specification or a guide supplies is void under `BR-79`. There is no population value anywhere in the system for a placement to be measured against, because none exists to be measured against |
| **The clinical significance criterion**, requiring functional consequence and not merely presence | Introduced as a false positive guard after symptom criteria alone produced implausible prevalence rates in epidemiological surveys | 15.3's `functional_impact` element on an `instrument` raise, satisfied by enumerated records showing effect on named declared priorities, obligations, quests, or capabilities | **Imported with its failure disclosed, in normative text.** When the equivalent criterion was tested against population data it did not solve the false positive problem it was introduced for, and the field's settled reading is that it failed. 15.3 requires the specification to say so and forbids presenting the gate as solved. It is also forbidden to be satisfied by asking the operator whether they are impaired |
| **The substance and medical condition rule out**, "not attributable to the physiological effects of a substance or another medical condition" | Forces consideration of a non psychiatric causal pathway before a presentation is attributed to a mental disorder. The single most directly transferable sentence in the manual | The attribution ladder, section 7, with the family's four registers substituted for the manual's two: HABITAT at rung 1, KIT at rung 2, TETHER at rung 3, QUEST at rung 4 | **The logic is inverted and the inversion is written down as an inversion.** Section 3.3 below |
| **The definition level environment and person firewall**: an expectable response to a common stressor is not a disorder, and conflict between an individual and society is not a disorder unless it results from a dysfunction in the individual | Two sentences in the manual's own definition, structurally stronger than any per category criterion, and the closest published analogue to an attribution ladder step | HABITAT's whole thesis, reached independently, and BEARING 7.1 rung 1 and 7.2 | The family had already arrived at this before the manual was read for it, which is the strongest available evidence that it is structural rather than borrowed |
| **The split residual**: "other specified", meaning it does not fit and here is why, against "unspecified", meaning it does not fit and either I cannot say why or I lack the data | Fixes a single earlier bucket that conflated a considered non fit with a low information one, and makes insufficient information an **affirmatively documented state** rather than an absence of record | 6.2, which splits the residual into `monitor` with `reason: unclassified` and `monitor` with `reason: no-data` | **Taken almost unchanged**, and 6.2 says why in the source's own terms: the low information case is the one most likely to be dropped, which is why it gets a named recordable state rather than a blank field. This is the highest value structural move BEARING took from the manual |
| **The `provisional` uncertainty marker**, attached to the assertion itself | Records a strong presumption that criteria will ultimately be met where information is currently insufficient | The `provisional` field of 5.1 | **The subject changed and the change is the point.** In the source, `provisional` qualifies the assertion about the person. In BEARING it qualifies **the apparatus**: it says the emitting monitor is running outside the acceptance bands it published in advance. 5.1 states explicitly that it is never a property of the raise's strength or of the operator, and that rendering it as a confidence is a severity under a friendlier name |
| **Principal diagnosis, ordered by current focus** and explicitly not by severity or by importance to the person | Designates one entry as the reason for the visit when several apply | 5.12, requiring raises be ordered by `raised_at` or by the operator's own declared order and never by a computed magnitude | Taken as an **existence proof**: several items can be presented in an order without ranking them. 5.12's own note is that a sort order is a scalar with the number hidden, and it is the shape the adversary reaches for after the numeric field is refused |
| **Remission defined as a duration of non qualification**, with a named carve out for which specific criteria may persist inside a clear state | Makes a state vocabulary about elapsed time rather than about a judgement of recovery | 10.4's `current`, `lapsed`, `undeclared`, where `lapsed` names an elapsed review interval with no closed review | The mechanism transfers and the direction reverses. The source names a state in which criteria are no longer met. **BEARING has no state meaning that, by construction** (5.10), and its three values name only whether the check happened. `lapsed` names the missing check and says nothing about the conduct |
| **The asymmetric threshold by consequence.** A cross cutting screen sets its inquiry threshold at mild for most domains and lowers it to slight for the three where a missed signal is worst, deliberately accepting more false positives there | Encodes the judgement that the cost of a miss and the cost of a false alarm are not equal in every domain, and settles it in advance | The `crisis` carve out, at 4.4, 4.5, 8.2, and the unbudgeted lane at 4.14 | **This is the single most consequential borrowing in the document.** It supplies the published precedent for firing earlier where a miss is most costly, which is what lets 8.2 exempt the crisis lane from persistence without contradicting 4.5. BEARING makes the asymmetry structural rather than numeric: the lane has no interval, no persistence requirement, and no budget at all |
| **The cross cutting measure's output posture**: a guide for additional inquiry, with no total score and no cross domain sum | The measure routes attention and does not conclude | The entire design, and 11.2's argmin specifically | Taken as confirmation rather than as a mechanism. A published clinical instrument that deliberately declines to produce a total is the strongest available answer to "surely it should add up to something" |
| **The unscored cultural interview**: open questions, narrative output, no number, no category, no threshold, the person's own definition of the problem elicited **before** the clinician imposes a frame | Person centred formulation, and an explicit acknowledgement that a self account benefits from a second source the self did not produce | 12.5, where the operator's own declared priority set is the `criteria` every alignment monitor measures against; 9.6, where every disposition carries a stated cause in the operator's own words; 9.3, which forbids a prompted form, item bank, scale, or anchors for one | **The strongest single import and the least visible one.** The rule that the person's own definition comes first, unprompted and unscored, is what keeps Arm B from becoming a questionnaire. The interview's informant version maps onto TETHER 2.3's `second-party` reference source, which the family already had |
| **Publishing the field trial reliability figures, including the poor ones** | The manual published its own agreement statistics and some were bad | 15.1, requiring every monitor to publish its `unknown` rate against its declared acceptance bands, per period, and to publish poor figures as they are | 15.1 calls this the thing most worth importing, more than any of the machinery: a monitoring system whose reliability is unpublished is a system whose users must assume it is good, and they will |
| **Publishing acceptance bands in advance** | The bands were stated before the results arrived, which was unusual and was the honest half of the exercise | 4.13, requiring every protocol to declare acceptance bands before its first evaluation | The dishonest half came from the same effort and is imported as the cautionary history: redefining adequacy after the results arrived was read by the field as moving the bar, and the reputational damage exceeded what the weak results would have done alone. `BR-12` makes the prior band govern the period retroactively |
| **Promoting the misuse warning out of the appendix** | The manual moved its own cautionary statement on forensic use into front matter, precisely because the appendix version was not read | BEARING's Conformance section, which makes front matter placement of the cautionary statement a requirement and an appendix or footer placement non conformant independently of the text's content | Then generalized past the source. **8.6 applies the same placement rule to the escalation path**, on the reasoning that every word of the argument applies with more force to the thing more consequential than a misuse warning |
| **The lesson of removing the context axis** | When a manual removed the axis that had carried psychosocial and environmental context, the **obligation** to consider context survived and the **structural prompt** did not. Formulations narrowed. The rule turned out to live in the form rather than in the practitioner's memory | 7.5, requiring the four ladder findings and the peer substitution question be transmitted **with the referral itself**, and making a separate filing a non conformant format | This is the reason the ladder findings ride along rather than being filed. It is a finding about forms, not about clinicians, and it is the best argument in the manual's history for putting a rule where the work happens |
| **The quarantine tier.** Everything in the manual's emerging measures section is marked as requiring further study and not established for routine clinical use, and placement there is a published statement of the manual's own confidence level | A location that says what the material is, rather than a warning attached to material sitting in the main body | Annex A, the worked example, described as non normative, structurally separated from every requirement, with the separation stated as the disclaimer | The stated reason is the same one the tier exists for: **readers extract examples far more readily than they extract caveats** |
| **Recording an event rather than forecasting one.** The manual's most recent revision added codes for the occurrence of certain behaviours and deliberately did not add a risk score or a predictive instrument | A way to record that something happened, not a way to predict that it will | 8.3, which states that routing on an explicit disclosure present in the record is transport and not scoring, sitting beside B-A6, which forbids a risk score including a two value high and low flag | The line the manual drew is exactly the line B-A6 draws, and 8.3 exists so that B-A6 is not read as forbidding the routing that several jurisdictions now require |

---

## 3. What was deliberately rejected, and the reason for each

A refusal with no recorded reason is reversed by the first reader who finds the refused thing convenient. Each rejection below is stated with the reason, and in most cases with the published failure that produced the reason.

### 3.1 The criteria set itself

**Rejected.** 16.1 forbids BEARING to contain an enumerated criteria set, a described experience, a symptom, an item, a response scale, an anchor, a cut point, a threshold quantity, a condition name, a category, a pattern, a profile, a constellation, or an archetype.

**The reason is regulatory before it is ethical.** The moment a specification states criteria content it has become a screening instrument, and screening instruments are clinically validated or they are dangerous, and are regulated in most jurisdictions. This is the family's form and content rule arriving with a consequence the other four documents never had to face, and it is why BEARING is the only member whose own prose is bound by a refusal about how it describes itself, at 17.2, on the published principle that intended purpose is set by labelling, instructions, and promotional material rather than by what the artifact does.

**The content had to go somewhere**, which is why section 16 has a guide layer and the other four documents do not. That is discussed at 0006 section 6 item 11 and carried as an open question here at 6.4.

### 3.2 The lettered criteria structure

**Rejected, and the finding that produced the rejection is negative and worth stating plainly.** The letters in a criteria set have **no universal semantics**. There is no manual wide rule that criterion A means one thing and criterion D another. The lettering is a within category ordinal labelling scheme whose real function is **addressability**, so that a clinician, a coder, a researcher, or a court can refer to a specific requirement unambiguously. Its conventional ordering, phenomenon then time then impact then alternative explanations, is real and is the transferable part, but the same letters carry entirely different cargo in different parts of the manual.

BEARING therefore took the **ordering** and refused the **notation**. Its equivalent of phenomenon is the trip condition, of time is 2.3's four separately declared requirements, of impact is 15.3, and of alternative explanations is section 7. Nothing is lettered, because addressability without semantics is a format that invites a reader to believe a structure exists where none does.

### 3.3 The conjunctive rule out

**Rejected, and inverted, and the inversion is written down at 7.3 as an inversion rather than left to be inferred.**

In the source, exclusions are **conjunctive with the finding**: fail a rule out and the finding is not made. That is correct there, because the output is a diagnosis and a diagnosis attributed to the wrong cause is a wrong diagnosis.

Carried across unmodified it becomes **the environment explains it, so no referral**, which is the well meant framework that kills people. It produces the "I will fix my sleep first and see someone later" failure, and the later never arrives, because the ladder always has one more rung and every rung is genuinely worth working.

BEARING's answer is not a policy sentence, because a policy sentence saying that the ladder does not gate routing is defeated by an implementation that simply orders the two writes, and nobody reviewing that implementation would see a violation since each write is individually conformant. **The routing record and the ladder record are separate records with separate write paths, a routing record MUST NOT carry a field referencing a ladder record, and a ladder record MUST NOT carry a lifecycle value.** Two write paths cannot be sequenced into one without building a field that does not exist.

7.4 closes the same failure one layer down: a ladder finding may not transition a raise's lifecycle or be recorded as grounds for a closure, because a rung 1 finding of `out-of-spec` is the most persuasive object the document produces and is exactly the object that must not be allowed to close anything. **The environment being out of spec explains a great deal and rules out nothing.**

### 3.4 The coding layer

**Rejected outright, and it is the most dangerous thing in the source.** Each category carries an alphanumeric code, the manual does not own those codes, and providers diagnose with the manual and bill with the code. That is the whole point of the layer and the whole danger: the code is the portable, machine readable, institutionally consequential token, and it is what travels into claims systems, insurance records, disability determinations, school records, court filings, and employment screening. The narrative does not travel.

Everything R1 refuses follows from this one observation, and the enforcement is three deep: 5.7 forbids the field names, 5.1 closes the schema so there is nowhere to put one, and 16.3 with `BR-88` stops a guide from carrying a condition name into a raise through the `criteria` identifier.

### 3.5 Severity, course, and remission specifiers

**Rejected.** 5.7's forbidden field list includes `severity`, `score`, `grade`, `level`, `rank`, `index`, `percentile`, `rating`, `risk`, `confidence`, `probability`, `likelihood`, `trend`, `streak`, `progress`, and `percent_complete`, and states that functional equivalence under a friendlier name is the same violation.

The source's own governing rule for severity specifiers is worth recording because it is the rule an implementer will not expect: severity and course specifiers are applied **only when the full criteria are met**, and a severity grade is never a substitute for meeting criteria and never applies to a sub threshold presentation. BEARING never has full criteria met, because it never has criteria in the first place, so the source's own rule already forbids what BEARING would have been tempted to build. The vocabulary was refused on its own discipline's terms.

`BR-20` makes the check a script rather than a review judgement. 5.7 states the reason directly: a reviewer asked whether a field is a characterization will sometimes say no, and a script asked whether a field is named `confidence` always says yes.

### 3.6 The global functioning scale and the axis it lived on

**Rejected, and this rejection is the one the family had already made under a different name.**

The removed scale was a single 0 to 100 rating, and the sharpest published criticism of it is exactly on point: it **dimensionalized the patient, not the disorder**, as to severity, function, and dangerousness to self or others. A one number global rating of a person, mixing symptoms, risk, and disability into one scalar, is the thing its own professional body removed. The stated grounds were conceptual lack of clarity, insufficient reliability in clinical settings, lack of precision, inability to detect change, and dependence on specialised training.

That is Q-A1 arriving from outside the family and confirming it. BEARING inherits Q-A1 unchanged and adds only the exhaustive enumeration of the three derived quantities it permits, at 5.6.

The proposed replacement is also instructive and is routinely misreported. A disability assessment schedule was **recommended** by the revision task force as a replacement and was **not approved** by the professional body for that purpose, so it sits in the emerging measures tier rather than as an endorsed successor. What it does have is the property BEARING wanted: it measures functioning in named domains, separately from any diagnosis, on a fixed recall window. It is the anti scalar. The diagnosis is not graded and the person is not summarized.

### 3.7 The multiaxial system, and the half of it that should have been kept

**Rejected as a structure, with its most useful property retained by a different mechanism.**

The axes were dropped for defensible reasons: the distinctions between them were not defensible in practice, the system was not required to make a diagnosis despite being widely adopted by insurers and government agencies, and it was rarely used to its full potential.

**The published criticism of the removal is the part BEARING acted on.** Removing the axis removed the **structural prompt** that had forced consideration of context on every diagnosis. The obligation survived and the reminder did not, and the reported consequence was narrower, more biomedical formulations.

BEARING's answer is 7.5: the four ladder findings and the peer substitution question ride with the referral itself, and filing them separately is a non conformant format whatever their content. The rule lives in the form, because that is where the evidence says it lives.

### 3.8 The diagnostic hierarchy and the "better explained by" rule out

**Not adopted.** In the source, hierarchy rules implement parsimony and prevent diagnostic proliferation from one underlying cause. In BEARING there is nothing to be parsimonious about, because there are no categories to prefer between, and a "better explained by" rule would have become a suppressor: a raise not emitted because another monitor's raise explains it. B-A3 forbids exactly that, and 4.8's prohibition on carry forward means each evaluation re establishes its own state rather than deferring to another's.

### 3.9 The interview, and every question addressed to the operator

**Rejected, at write time rather than by preference**, and BEARING 4.2 gives three independent grounds because a reader who defeats one will otherwise reintroduce the mechanism.

**First, it is the active self diagnostic tool the document exists partly to refuse.** Asking a person to look inward and score what they find is the mechanism that produces rumination and self labelling, and it converts a monitor into an examination.

**Second, inquiry addressed to the party under review is the weakest evidence class.** The audit profession places inquiry at the bottom of its evidence hierarchy and holds that inquiry alone cannot support a conclusion about a control's effectiveness. POLARIS 5.3 says the same thing in one sentence.

**Third, in any employment adjacent deployment the question is already the violation.** An inquiry likely to elicit information about a disability is prohibited by virtue of being **asked**, independently of the answer and independently of what is done with it. A specification that shipped an item bank would make its own conformant implementations unlawful in a deployment its own R4 refusal already forbids, which is a strong signal that the mechanism is wrong rather than merely risky.

9.3 states the refusal a second time for the docket, because the review is the moment when asking feels appropriate and is the second and independent place where the mechanism gets built.

### 3.10 The compliance shaped signal

**Rejected, and this is the one whose history is worst.**

4.3 forbids a monitor to read any signal whose subject is the operator's perceived honesty, insight, cooperation, engagement, responsiveness to the system, agreement with the framework, adherence, promptness, tone, affect, sentiment, or use of the tool. It is excluded from the closed `input_source` enum at 4.1 rather than forbidden in prose, so the check is a membership test a write path can implement, and 4.3's second paragraph closes the content route for a record held in another register whose subject is nonetheless the operator's engagement.

The rationale is stated with its history because this is the class an automated monitor is most tempted to collect. **Compliance telemetry is the cheapest telemetry there is**: the system already logs whether the operator opened the review, whether they dispositioned promptly, and whether they agreed. It is also the class with the worst record. Signals of this kind, inferred from patients' responses as symptom denial and poor insight, produced a documented racial disparity in one diagnosis. The same class, formalized, produced a state category whose enumerated criteria included perseverance, struggle for the truth, and conflict with authority.

**It is the single step by which an alignment monitor becomes a loyalty monitor, and there is no version of it that is safe because it is well intentioned.**

The requirement earned its structural enforcement the expensive way. An earlier draft of 9.16 raised on a pattern of rejected review attempts, with the honest stated reason that a silent rejection is a machine deciding something about a person without telling them. That was the first engagement telemetry monitor in the system, monitoring the operator's eagerness to review themselves, which is the most loyalty shaped signal available anywhere in the document. It was collected in the name of transparency. Returning the rejection to the operator at the moment of the attempt discharges the stated reason completely and creates no record at all.

### 3.11 The reliability band redefinition

**Rejected as a practice, retained as a cautionary history.** The manual published its bands in advance, which was honest, and the field's reading was that the bands themselves had been set where weak results would present acceptably. Whether that reading is fair is not the point BEARING takes. The point is 4.13's: **once thresholds move to fit results, every number the system emits afterward is uninterpretable**, and Arm A's numbers are the only asset Arm B has. `BR-12` makes the prior band govern the period and enumerates the revision as drift.

### 3.12 Disclosure as a sufficient control on interest

**Rejected as insufficient, with the structural exclusion stated alongside it.** 16.4 forbids a guide author or a monitor owner to hold an undisclosed interest in the routing target, and makes the coincidence of referral destination and criteria author in the same commercial entity a conformance failure and a red check **regardless of disclosure**.

The evidence is direct. The finding on a comparable panel is that transparency alone cannot mitigate bias, and disclosure policies were already in place when a large fraction of one manual's revision panel was found to have received undisclosed industry payments. **The disclosure requirement is the one that was in place when the failure occurred**, which is why the structural exclusion is stated as well.

16.6 closes the adjacent case from the same history: a criterion's author may not be its sole attester, on the documented failure of a work group subjectively confirming the validity of criteria it had itself proposed. That is TETHER 1.2 and POLARIS 5.3 arriving in the guide layer, and both apply without modification.

### 3.13 The awareness content assumption

**Rejected, and this is the one place in the whole document where the evidence supports adding material rather than removing it.**

A controlled trial found that ten minutes of expectation effect education **halved and then eliminated** false self diagnosis that accurate, well intentioned awareness content had **doubled within a single session**. The doubling and the correction were measured in the same session, in the same population, from the same content.

Two requirements follow. 16.5 requires an expectation effect notice on every guide. And R7's refusal takes the form it does because **awareness content does not have to be wrong to cause the harm**: a guide that is entirely accurate still needs the notice.

---

## 4. The non clinical precedents

Most of BEARING's actual machinery is not clinical at all. A reader who assumes it was invented here will treat it as taste, and taste is negotiable in a way that a documented industrial failure is not.

### 4.1 The watchdog, and the three clauses it supplies

**A watchdog is satisfied only after several unrelated good things have happened, its state is zeroed each cycle so the good state is affirmatively re earned rather than inherited, and it treats too fast exactly as it treats too slow.** All three are in 4.8, and the third is the least obvious and the most useful: a period of completions backfilled into one minute looks complete, satisfies every count, and reports out of range **without the monitor forming any view about why**, which is exactly the division of labour B-A2 requires.

4.12 takes the watchdog's other rule, that a watchdog cannot run on the clock that may fail, and combines it with two more from unrelated fields: an auditor must not assume ownership of the monitoring it evaluates, which is why the protocol register is not the monitor's own state, and an observer must not evaluate their own tasks, which is why a monitor's interval is not set by the schedule it audits. **Three traditions converging on one requirement is why it is stated as an absolute of construction rather than as a recommendation.**

### 4.2 Readiness against liveness

The single most important import in the document, and 3.3 states it exactly. **A readiness check removes an endpoint from the evaluated set, kills nothing, and rejoins automatically on the next passing evaluation. A liveness check restarts the container.** BEARING's unlocking model is a readiness check. Importing the wrong one takes capability away from an operator at the moment they most need it, which is the moment they stopped being able to complete a review.

That analogy is what turns B-A4 from a good intention into a shape an engineer recognizes. It is also why 10.6 requires Arm A to keep running when Arm B lapses: if skipping the review silenced the monitors, the cheapest way to a clean record would be to stop looking at it, and the record would go quiet exactly when it had the most to say.

### 4.3 Alarm management

Three findings, from three separate industrial disasters and one healthcare series, and they supply four requirements between them.

**Alarm rationalization**, and the discipline arrived at the expensive way after a plant explosion during which two operators received two hundred seventy five alarms in eleven minutes. The finding was not that the alarms were wrong. **It was that an alarm nobody can act on consumes the attention the actionable ones needed**, so the correct disposition is removal rather than adjustment. That is 4.15: a monitor with no defined recipient action is retired, never tuned, and tuning is deliberately unavailable because tuning is how a monitor nobody can act on survives review after review.

**Alarms turned off** was the largest single counted contributing factor to deaths in a published healthcare sentinel event series, and false rates approaching ninety percent are what produce the muting. That is 4.14: the budget raises and never suppresses, exceedance emits a raise naming the producing monitors, and **the correct response to too many raises is a raise about that fact addressed to the maintainer, never fewer raises reaching the human.**

**Single signal triggering is the documented path to a muted monitor.** In a population where fewer than one in a hundred carry a condition, four in five can carry one flag, so a monitor that fires on one flag fires constantly and is turned off. That is 4.5's persistence requirement, and it is 4.14's failure arriving through the trip condition rather than through the budget.

**Unanswered reports are how reporting systems silently die**, and the mechanism is not malice: people stop reporting when reports go nowhere. That is 6.4's closure discipline, and it matters more here than in an industrial setting because the register Arm A reads is written by the same person who stopped.

### 4.4 Government auditing standards, and where a report stops

Auditing standards define a finding as **criteria, condition, cause, and effect**, and then state that where the objective is to determine current status, developing **the condition alone** addresses the objective and the other elements are not necessary.

That is authoritative standards text licensing exactly Arm A's shape, and 5.2 cites it rather than asserting the rule, because the instinct of every implementer will be that a report without a cause is incomplete. **Cause belongs to Arm B, where the operator writes a stated cause on a disposition, and to the qualified human, who has the training and the access Arm A does not.**

The audit evidence hierarchy supplies the other half, at 4.2 and 12.2: inquiry sits at the bottom and cannot alone support a conclusion about a control's effectiveness. `unmeasured` is the honest disposition and it is neither a pass nor a fault.

### 4.5 Testing a protection that has never fired

POLARIS 4.5 states the dead refusal problem and supplies no mechanism. Four unrelated domains supply one, which is why 12.1 specifies a **seeded submission** rather than an inspection.

A **standardized harmless token** that every compliant scanner must detect, existing solely so that detection can be verified without anyone handling the real thing. **Functional testing with a listed analog**, where a self test button explicitly does not satisfy the requirement, because the button tests the announcement and not the mechanism. And a **protective device that fails internally while still passing power**, which is the dead refusal problem in one sentence: everything downstream works, the protection is gone, and nothing anywhere reports a fault.

The same discipline is then turned on BEARING itself at 15.5. **A suite that need never run is indistinguishable from an inert one**, and a specification that exempted its own checks from the discipline it imposes would be making exactly the argument POLARIS 4.5 refuses.

### 4.6 The blameless review

9.17 offers one shape for the review and quotes three properties from the source discipline as normative properties **of that discipline**: it is not a critique; nobody, regardless of rank, position, or strength of personality, has all the information or all the answers; and it does not grade success or failure.

The important sentence is the qualifier. **Blamelessness is not the absence of a standard.** What is refused is grading the person and handing down one authority's verdict. What is retained is that the standard was declared in advance, the observation is specific and recorded, and the interpretation is produced by the participant rather than delivered to them.

9.5's freeze comes from an adjacent finding about a structured decision tool with a human judgement at the end: **some users ran it backwards**, working from the conclusion they had already reached to the inputs that produced it. In a self applied setting the operator can launder a conclusion about themselves the same way, and no second party is present to notice. Freezing the count before the meaning is written means a disposition can disagree with the count and can never rewrite it, and the disagreement is then itself in the record.

### 4.7 The corrupted indicator

14.6 rests on the law that the more a quantitative indicator is used for decision making, **the more subject it is to corruption pressure and the more apt it is to distort the process it was meant to monitor.** A count that is consequential stops measuring.

12.6 carries the case that makes it concrete and that an implementer will remember. An employment agency published per person referral statistics, and its agents began concealing job openings from one another. **Individual numbers improved while total placements fell**, and the least cooperative unit posted the highest averages. Every number was true. The measure had become the objective, and the objective it displaced was the one the organization existed for.

### 4.8 Unidirectional rules are not used unidirectionally

13.2's ratchet sits in the write path rather than in prose because the published record on unidirectional decision rules is that they are almost never used unidirectionally in the field. A rule intended only to escalate is read in both directions by the people using it, because **the negative reading is the useful one when the queue is long**. A direction that lives in prose is a direction that will be reversed by the first busy implementation.

That finding then applied to itself. An earlier draft stated the ratchet correctly and left one act outside it: 13.1 permitted an agent to compute a run, and a run returning `no-trip` is not a rejected write and produces no record of an attempt, so it was the largest available move away from human attention and the one the ratchet could not see. `BR-94` closes it, and 13.1 records the reasoning against its own earlier text.

### 4.9 Envelopes and leading indicators

4.7 collapses two documented failures into one requirement. **Decision rules are routinely applied outside the population they were derived in**, where their operating characteristics are unknown and are usually worse. And in one well studied hardware population, **the strongest leading indicators were absent in over a third of real failures**, which means a monitor can be correct inside its envelope and silent for exactly the cases that matter most, without ever producing a wrong answer.

The second is the more unsettling of the two and it is the honest bound on everything Arm A can claim.

### 4.10 Labelling, and grep

Two smaller precedents that shaped the document's form rather than its logic.

**Intended purpose is set by labelling, instructions, and promotional material.** That is why 17.2 binds the specification's own prose first and the implementation second, and why the motivating phrase about early detection of deep level system faults is refused in normative text. It correctly describes why the work was undertaken and inaccurately describes what the resulting document does, and a specification carrying it would have described itself as a detection system in the one artifact that determines whether it is one. **The phrase belongs here, and this note is where it now lives.**

**A rule enforced by grep is a different kind of rule.** The reference implementation's published style guide already bans the rating idiom and the advice register by mechanical check. 5.7's enumerated field name list and 5.9's forbidden state name list exist so that B-A2 is checkable by a script rather than by a reviewer's judgement, and 5.8's prohibition on implementation authored prose converts a question about tone into a code inspection: a renderer holding natural language templates other than field labels is non conformant on inspection, and inspection of the templates is the check.

---

## 5. The safety analysis

### 5.1 The thing this could become

Stated once, in the document's own words: **an automated system that grades a person's alignment to their own stated values is a machine for manufacturing shame at scale, and that is the single worst thing this document could become.**

Everything below is an enumeration of the routes to that outcome and of what closes each.

### 5.2 The misuse table

| The misuse | How it would actually get built | What closes it | Why that closure and not another |
|---|---|---|---|
| **A purity ladder.** Capabilities earned by proving alignment | A gate somewhere in the stack reads a calibration state or a review record | B-A1(a) forbids any other document to cite a BEARING element; B-A1(b) makes every BEARING artifact confer nothing; 9.18 restates it in the section where an implementer feels something has been earned | A prohibition on building a ladder is a promise. A dependency graph with no inbound edges is a property. 3.1 makes it a search |
| **A shame engine.** The count acquires a cost | A lapse, an `undifferentiated` reading, or a low argmin is wired to a consequence | B-A4: an absent, lapsed, declined, unowned, or unsigned review may not block, revoke, downgrade, withhold, delay, price, penalise, or condition anything. 10.5 restates it in the one section where the state and the motive sit in front of the reader at once | 10.5 is the honest placement decision in the document. `lapsed` is true, cheap, and decidable, and wiring it to anything is one line of code |
| **A third party screening product.** An employer, insurer, school, or court reads the register | Aggregation, cohorting, and export | 14.4 bans the infrastructure rather than the interpretation; 14.5 refuses any result with more than one distinct subject **in full and never truncated**; B-A5 forbids a third party mode and any artifact whose function is to demonstrate that a review occurred; the front matter cautionary statement says so where it will be read | Reification is produced by the second order infrastructure built on a category, not by the noun. Truncation is refused specifically because it is the plausible choice and it defeats the control: a caller receiving one subject per request builds the multi subject view by iterating |
| **A diagnosis by another name** | A `criteria` identifier or a raise type carries a condition name into every raise | 16.1 for the specification, 16.3 and `BR-88` for the guide layer, with the enforcement being that **every monitor citing a violating guide reports `unknown-undeclared`** and its already emitted raises are void | BEARING has no authority over a guide's review path, because 16.2 defined the guide as outside its conformance. What it controls is whether a monitor may read one, and that is sufficient |
| **A risk score** | Any stratification of a disclosure, including a two value flag | B-A6, which names the two value flag explicitly so it cannot be reached by minimalism; 8.3, which distinguishes transport from scoring so B-A6 is not read as forbidding required routing | The source discipline's own most recent revision drew this exact line: a way to record an event, deliberately not a way to forecast one |
| **A loyalty monitor** | The system reads whether the operator engaged, agreed, or responded promptly | 4.3, enforced as a membership test against the closed `input_source` enum of 4.1, with the content route closed separately; self test check 11 seeds an engagement sourced input and asserts the rejection | Prose would not have survived. The earlier 9.16 draft built exactly this monitor in the name of transparency, which is the proof that the prohibition needed a structural form |
| **A model deciding whether a person is aligned** | A language model evaluates the trip condition, or an agent does it and is not called a model | 4.6, with `BR-06` rejecting the protocol at write time; 2.10 defining a model backed agent to be a model for 4.6's purposes; `BR-94` making an agent determined run result `unknown-unauthorized` and itself a raise | If a model decides whether conduct is aligned, the operator's alignment is the model's alignment, filtered through a prompt, subject to a provider's policy, and revisable with no amendment record |
| **Surveillance under another name** | A standing automated evaluation runs with no scoped, expiring, revocable grant | 13.3 requiring a CONFIDE section 4 inference authorization, revocable at any time with no stated cause and no cost, never renewed by default; `BR-69` making every affected monitor `unknown-unauthorized` and deleting unauthorized outputs | The precondition standard is deliberately stronger than a consent checkbox: an evidentiary precondition before any inquiry, and a scope limited to what the declared purpose needs. **This closure is incomplete and section 6.2 says why** |
| **Rumination with a schema** | The review runs daily, or an ambient stream of self ratings replaces the two cadences | 9.16's minimum interval as well as a review interval, rejected at write time with the rejection returned to the operator at the moment of the attempt; 2.1 keeping the informal check in entirely outside the document's reach | **Too much signal is a fault**, and this is the shape of harm the document is most likely to cause the person it is trying to help |
| **An effort measure over a person** | A minimum duration for the sitting itself | Dropped, and the reason recorded at 9.16: a duration floor is an effort measure over a person, it is defeated by leaving a window open, and it would have been the one place in the document where a number about how hard someone tried was stored | Recorded rather than merely removed, because the requirement is reasonable on its face and will be proposed again |
| **Alignment achieved by amendment** | The inconvenient count is made to disappear by lowering the bar | 9.11's cooling rule, binding a declared element **and a monitor**, with the prior value governing and two separate failure classes; 9.13 routing every revision through POLARIS's ordinary amendment path and supplying no machinery of its own | **BEARING applies the cooling rule to the monitor because the monitor is the newer and softer target.** An operator who would not amend a refusal to make a count go away will widen a window without noticing that these are the same act |
| **Retroactive alignment** | The period is reviewed against a declaration amended after the period began | 9.2, requiring the review cite the declaration version as it stood at the **start** of the reviewed period | The move is not cynical and would rarely be deliberate. It is what any reasonable implementation does by default, because the current declaration is the one in hand |
| **A priority set inferred from conduct** | The system reconstructs what the operator must have valued, from what they did | 12.5, with `BR-66` rejecting it at write time **regardless of clinical direction** | It is the single most tempting shortcut in the document and it inverts the entire mechanism. A priority set derived from the conduct it would be measuring **cannot detect drift** and will report perfect alignment for every operator forever |
| **A conclusion that help is unnecessary** | Any state meaning resolved, cleared, ruled out, dismissed, or handled | 5.10's three value lifecycle, with two transitions out of the open set and no identity permitted to write a third meaning | **This is the anti self talk requirement in structural form.** The framework cannot be used to conclude that help is unnecessary because it has no way to say so, which is stronger than a rule against reaching the conclusion, since a rule is applied by the same faculty that would reach it |
| **A dishonest review** | Correction is cheap and acceptance is expensive, so the operator learns which answer costs less | 9.7, forbidding `accepted` to require more fields, confirmations, or authority, or to create any follow up another disposition does not; 9.12, forbidding `confirmed` to be rendered as lesser | A review whose only cheap output is correction does not produce fewer accepted items. It produces **dishonest dispositions**, which poisons the count the next period reads, and the count is the only asset Arm B has |
| **A monitor tuned into silence** | The system responds to disagreement by adjusting itself | 9.10, enumerating repeatedly disputed monitors and forbidding automatic removal, disabling, retuning, widening, or narrowing; 9.8, retaining a disputed count unchanged beside its dispute; 9.9, re presenting a re raise with its prior dispute attached | A system that tunes itself toward silence in response to disagreement will reach silence, through a sequence of individually reasonable adjustments, which is POLARIS 11.5's own description of drift |

### 5.3 The failures that run the other way, and why they are the harder half

The 2026-08-30 review found ten blockers in BEARING, and its most useful observation was about their direction rather than their content: **every one of the top defects failed toward the raise not being emitted, not being routed, or not reaching a human.**

That is worth generalizing, because it is not obvious from the outside. A document written against the harms in 5.2 accumulates prohibitions, and prohibitions compose into deadlocks at the write path. The specific instances were exact: a closed raise schema that omitted five elements other requirements made mandatory, so that the two write time rules fired against the same record and the conformant implementation was the one that did not emit; a general prohibition on raising from a single evaluation with no crisis exception, so that a disclosure written on day one of a declared interval was carried on day thirty if at all; a write time identity comparison that silently excluded every operator under guardianship from all output including crisis output; a retirement clause that let a maintainer close a retired monitor's outstanding raises, which was 5.10 defeated in one clause by the one party with an operational reason to want the queue empty; and health invariants that were most cheaply satisfied by withholding the raises whose ladders were incomplete, which rebuilt the failure 7.3 exists to prevent one layer below where 7.3 reaches.

**The lesson is a drafting lesson and it belongs in this note rather than in the specification.** In a document whose subject is a monitor, a safety requirement and a suppression are the same shape, and the reviewer's question is never only "what does this forbid" but "what does an implementation that wants to do nothing do with this". Three of BEARING's requirements now exist specifically because the answer was uncomfortable: 6.3 separates performing a routing from recording it, 19.2 replaces two counts with an enumeration because a count of incomplete ladders is most cheaply reduced by not emitting, and 8.6 exists because the mandatory placement rule had been spent on a misuse warning while the crisis path was governed entirely machine to path.

### 5.4 What is not closed, stated plainly

**A custody floor is unenforceable against a recipient who breaches it.** 14.7 says so. No ledger the operator holds catches a comparison computed elsewhere. What the floor buys is that the obligation was stated, was recorded, and can be pointed at. A document implying more would be lying about its reach.

**The crossings that matter most go to a human by design.** An `instrument` raise routed to a qualified human carries fired signals, functional impact evidence, a baseline comparator, and four ladder findings, and that is correct. What happens to those records afterward is governed by the RETAIN operator adapter, which is unwritten.

**Ownership is not mechanically detectable and 10.1 refuses to build a proxy.** Ownership is the whole content of Arm B and it is invisible to a machine. The family already concedes the unmechanizable half of the identity firewall rather than pretending otherwise, and 10.1 is the same honesty in the same shape. Stating it is what stops an implementer from building a proxy and calling it ownership.

**The peer substitution question at 7.2 is not closed and is a live defect.** It is discussed at 6.1.

**Nothing measures whether any of this works.** There is no proposed evidence that a conformant register produces a better outcome for an operator than an unstructured practice, and no document in the family claims one. That honesty should be preserved rather than quietly upgraded when the material reaches courseware.

---

## 6. Open questions

### 6.1 The peer substitution question

7.2 records a fifth question that is not a rung: would a comparably situated party, in the same declared environment with the same declared kit, plausibly have produced the same record. Its intent is right, and it is the only mechanism in the document that separates a system induced outcome from an individual one without naming a defect in a person.

Its form is wrong. 4.2 forbids any question administered to the operator, 4.6 forbids a model from determining a monitor result, and the only party left to answer a question containing the word "plausibly" is the operator, about themselves, through the instrument that may be at fault. 7.5 then requires it to travel with the referral, which makes it the one place in the document where a self applied judgement reaches a third party. It carries no failure class.

**Two options.** Recast it as a mechanical query over HABITAT provisioning party records and KIT loadout records, so that it resolves without asking anyone anything. Or move it out of the transmitted referral into non normative guidance under section 16, where an unanswerable question is an invitation to think rather than a field in a referral. Either way it needs a failure class.

### 6.2 The inference authorization's two missing bounds

13.3 requires a CONFIDE section 4 inference authorization naming five things: the purpose, the enumerated monitors, the scope of records readable, the agent identity bound, and an expiry. CONFIDE 4.1's named fields cover three of the five. There is no enumerated monitor field and no record scope field.

The enforcement question is separate and sharper. CONFIDE 4.2's hook fires when an actor performs inference with no authorization, while BEARING 4.6 forbids a monitor's predicate from requiring a model at all, so **a conformant monitor makes no inference call for the hook to catch.** `BR-69` has no mechanism to detect the absence it disposes of.

**Two options.** Define a BEARING scoped grant carrying the five fields and route its refinement to the CONFIDE operator adapter. Or state precisely which CONFIDE fields carry the monitor enumeration and the record scope, and add both to the adapters README as inbound obligations on CONFIDE. Either way, state how the authorization is enforced when the evaluated activity involves no inference call. **13.3 calls this requirement the difference between monitoring and surveillance**, which is the reason it is first on this list rather than filed as drafting residue.

### 6.3 The review record as a portable credential

R4 claims no third party screening use and claims it is unconfigurable. 9.1 mandates, for reasons that have nothing to do with third parties, a review record carrying `closed_at`, the period bounds, the declaration version reviewed against, the frozen docket hash, and the operator's signature. That is a better compliance credential than a third party would have designed, and B-A5's test is function as designed rather than intent.

BEARING defines no export format for one, which is the current answer, and 14.7 concedes that the floor is unenforceable and disclosure is the only control. **Two options.** Soften R4 to name what is actually refused, which is comparison infrastructure inside BEARING, and cite 14.7's honest reach statement beside it. Or add a requirement that BEARING define no export format for a review record at all. The aggregation happens in the recipient's spreadsheet, one export at a time, which is the iteration 14.5's truncation rule anticipates for queries and does not reach for exports.

### 6.4 Does the guide layer generalize

BEARING owns the family's only treatment of author written domain content, and its enforcement model is transferable: a specification has no authority over a layer it defined as outside its own conformance, so what it controls is not whether the guide exists but whether anything inside the specification may read it. Nothing equivalent exists for a KIT loadout guide, a QUEST curriculum, or a HABITAT environment guide. 0006 carries this as Q14 and section 6 item 11.

### 6.5 Should the alignment spectrum binding be in a specification at all

Section 11 binds to a published four module course, names no position, and is optional at every conformance tier. That is the most conservative possible treatment and it is still the only place in the family where a specification is shaped by a specific piece of teaching material.

The argument for keeping it is that the binding is a set of refusals rather than a set of contents: positions never composited, comparison self referential, a machine never moves the dot, the argmin as the only derived quantity, and no position named. Every one of those is a rule the material's own author has already stated in published text, twice in the case of the score refusal, and a specification that introduced a rating would contradict a grep enforced house rule of the material it serves.

The argument against is that a section optional at every tier, binding to one artifact, is a section that could live entirely in a guide. **The question is whether removing it would lose the refusals**, and the honest answer is that it probably would, because the refusals are the part a guide author would drop.

### 6.6 The argmin

11.2 permits exactly one derived quantity over an operator's own placements, and it is the only such quantity in the entire published alignment system. It survives Q-A1 because a pointer moves in both directions, is scoped to one sighting, and accumulates nothing.

It also required two repairs during drafting, which is a signal worth recording rather than ignoring. The first formulation said "low pole" and imported the ordering that 11.5 forbids two subsections later, which is why `low` and `high` are now in 5.9's forbidden vocabulary so that a script catches a reintroduction. The second was that the argmin is uncomputable across positions with no shared ordinal scale, and an implementation would have invented one, which is the composite 11.1 refuses arriving as an implementation detail nobody reviews. Both are now fixed and both were found in review rather than in drafting.

**The open question is whether a quantity that needed two repairs to stay Q-A1 compatible should exist in a specification at all**, given that it is optional, that its home is published canon, and that its absence would cost the operator a pointer they could compute by looking at their own placements.

### 6.7 The crisis lane and TETHER section 9

Four BEARING requirements route into a skeleton. This is 0006's Q16 and it is the only question in either note that should be answered before anything in `spec/` leaves Draft. It is a question about TETHER rather than about BEARING.

### 6.8 The guardianship exclusion

B-A5 removes an entire population from the document rather than defining a mode for them. The reasoning is right: a guardianship grant would be the configuration that reintroduces a standing alignment monitor pointed at another person, which is precisely what R4 refuses, and BEARING's own boundary statement is explicit that no lane remains live under a guardian's signature including the crisis lane.

What is open is not whether the exclusion is correct today. It is whether anything is ever written for the population TETHER 4.2 names as the severest case, and if so, in which document. 0006 carries it as Q17.

### 6.9 Should the self applied ceiling be published as a number

1.5 states the ceiling as an unknown and argues that it is probably below the worst published figure for trained parties. That is honest and it is also unfalsifiable, and 15.1 requires every monitor to publish its own figures while the document's central reliability claim is a qualitative argument.

The alternative is to run something and publish what comes out, which would require a study this family has no apparatus for and which section 5.4 already concedes does not exist. **The question is whether the qualitative ceiling is the right permanent answer or a placeholder**, and stating it as a placeholder in the specification would itself be a claim about future work that nothing supports.

---

## Sources

This note derives from `spec/BEARING-v1.0.md`, the four sibling specification drafts, `spec/adapters/README.md`, design notes 0005 and 0006, the 2026-08-30 review of BEARING, and the published literature on the source discipline's structure, field trials, and known failures.

The reference implementation is the author's own operating practice as recorded in the vault, together with its published four module alignment course, which BEARING treats as canon it may not contradict. Per the clean room rule both are read and never copied, and nothing in `spec/` derives its text from either. **No condition is named in this note, no criteria set is reproduced, and no item content from any published instrument appears anywhere in it**, which is the same boundary BEARING 16.1 imposes on itself and Annex A imposes on its own worked example.
