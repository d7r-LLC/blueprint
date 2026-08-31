# HABITAT: the operating environment of an instrument

## Version 1.0

**Specification:** HABITAT/1.0
**Status:** Draft, structural. Sections 1 through 4 are written. Sections 5 through 9 are skeletons with their theses stated.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**License:** Apache 2.0
**Requires:** TETHER/1.0 for operator and instrument vocabulary. DERP/1.0 as the structural counterpart, informative.
**Design note:** `design/0005-meat-suit-interface.md`, non normative.

---

> **Status note.** Structural draft, published for review of its shape. An implementation MUST NOT claim HABITAT conformance while this Status reads Draft.

---

## Abstract

DERP answers what a runtime must provide for an agent to operate. HABITAT answers the same question where the operator is a person and the runtime is the physical and social environment their instrument runs in.

An instrument has a design envelope it did not choose, set by an environment its operator does not live in. The current environment is not a given, it is a **declared configuration**, and it is provisioned largely by parties other than the operator. Most of the distance between how an instrument performs and how it could perform is a property of that configuration rather than of the instrument.

The document's load bearing requirement is one sentence. **A fault is tested against the declared environment before it is attributed to the instrument.** Attributing an environment fault to the instrument licenses a repair aimed at the wrong layer, and a system performing badly outside its stated operating conditions is not a faulty system. This is the same discipline any operations practice applies to a service before it declares a bug, applied to the one system where it is least often applied.

HABITAT specifies that an environment class is declared, that provision is distinguished from availability, that timing is a property of an input rather than a scheduling detail, that the mismatch between design envelope and declared environment is registered and kept current, and that the party who provisions each class is named. It specifies no quantity, no threshold, no target, and no protocol. Two conformant operators may live in radically different environments and HABITAT ranks neither, exactly as DERP ranks no runtime.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Two requirements are absolute.

1. **Clinical precedence.** HABITAT MUST NOT supply grounds to decline, delay, or discontinue care. It inherits TETHER's absolute requirement 1 unchanged.
2. **No target values.** HABITAT MUST NOT state a quantity, threshold, target, or schedule for any input class. A conformance requirement expressed as a value is malformed and MUST be rejected as non conformant text.

Requirement 2 is what keeps this a specification rather than a regimen. The moment a normative document states how much sunlight is correct, it has stopped specifying a form and started prescribing a life, and it has done so with a number it cannot justify for every instrument that will read it.

---

## Table of Contents

1. Introduction
   1.1 The environment is the runtime
   1.2 Mismatch is the default condition
   1.3 Position in the stack
2. Definitions
   2.1 Design envelope and declared environment
   2.2 Input class
   2.3 Provision and availability
   2.4 Provisioning party
3. Provision Is Not Availability
4. Timing Is a Property of an Input
5. Input Classes (skeleton)
6. The Mismatch Register (skeleton)
7. Provisioning Parties (skeleton)
8. Adaptation and the Silent Floor (skeleton)
9. Failure Classes and Conformance (skeleton)

---

## 1. Introduction

### 1.1 The environment is the runtime

The author's own specification alignment work assigns the runtime document to the environment rather than to the body, with the body retained as host. HABITAT fills that slot.

The mapping is exact enough to be useful rather than merely evocative. A runtime provides resources on a schedule, under contention, with quality of service that varies and is rarely measured by the thing consuming it. An environment provides light, temperature, air, water, food, opportunity for load, opportunity for sleep, social contact, and information, on a schedule, under contention, with quality that varies and is rarely measured by the person consuming it. In both cases the consumer's performance is routinely attributed to the consumer.

### 1.2 Mismatch is the default condition

An instrument's design envelope was set by an environment that no longer exists for most operators. This is not a claim that the older environment was better, and HABITAT takes no position on that question, which is contested, romanticized in both directions, and irrelevant to the requirement. The claim is narrower and is not seriously disputed: the envelope was set somewhere other than here, so the delta is nonzero, and an unmeasured nonzero delta is the standard precondition for misattribution.

The requirement that follows is procedural, not substantive. **Register the delta, and consult it before attributing a fault.** HABITAT does not say what the delta should be, or that it should be smaller.

### 1.3 Position in the stack

HABITAT inherits POLARIS's asymmetric precedence through TETHER. A declared environment or a registered mismatch may **narrow** what an operator is authorized to do, and may never widen it, satisfy another document's check, or excuse a failure. "The environment was out of spec" is a bound declared in advance and a cause recorded afterward. It is never an authorization and never an excuse.

---

## 2. Definitions

### 2.1 Design envelope and declared environment

The **design envelope** is the range of environmental conditions under which the instrument performs as its structure anticipates. It is not chosen by the operator and is not fully known.

The **declared environment** is the operator's written statement of the conditions the instrument is actually in, class by class. It is a configuration, it changes, and it is declared rather than assumed.

### 2.2 Input class

A category of thing the environment supplies to the instrument. Section 5 enumerates the classes an implementation declares.

### 2.3 Provision and availability

An input is **available** when the environment permits the operator to obtain it. An input is **provisioned** when the operator actually receives it.

Section 3 is why these are separate words.

### 2.4 Provisioning party

The party that controls whether a class is provisioned. It is frequently not the operator. It is a declared field, not an assumption.

---

## 3. Provision Is Not Availability

**An implementation MUST declare each input class by what the environment provides, and MUST NOT declare a class satisfied on the grounds that the input was available.**

This is the distinction most environment assessments collapse, and collapsing it produces a report that looks conformant while describing an environment that supplies nothing. Sunlight is available above every office building. Sleep opportunity is available to anyone with a bed. Movement is available to anyone with legs. Availability is a property of the world; provision is a property of what reached the instrument, and only the second one has any effect.

**Failure mode: an undeclared class is treated as unprovisioned, never as adequate.** Fail closed. An implementation that reads silence as sufficiency has inverted the requirement, because the classes most likely to go undeclared are precisely the ones nobody noticed were missing, which is section 8.

---

## 4. Timing Is a Property of an Input

**An input declaration without a timing property is malformed.**

The same quantity of the same input, supplied at a different hour, is a different input. The systems it acts on are phase dependent, so quantity alone does not identify what was supplied. An implementation that records amounts without times has recorded something, and it has not recorded the input.

This is where periodicity enters the specification as structure rather than as advice. Note carefully what is and is not required: HABITAT requires that timing be **declared**, and says nothing whatever about what the timing should be. The operator working nights and the operator rising at dawn both conform, and both have declared something true that a quantity alone would have hidden.

**Failure mode:** a declaration missing a timing property is rejected at write time, in the same way TETHER rejects an intervention missing an exit condition.

---

## 5. Input Classes (skeleton)

**Thesis.** A small, enumerated, extensible set of classes, each declared with provision, timing, and provisioning party. The set is chosen to be exhaustive at the level of what an environment supplies, not at the level of what physiology does with it.

Working set, to be settled: light (spectrum, intensity, timing), thermal, respiratory and hydrological, nutritional, mechanical load, sleep opportunity, social band, information load.

To be written: the declaration schema for a class; the extension rule; the treatment of a class an operator declines to declare, which under section 3 is unprovisioned rather than unknown; and the interaction between information load and the rest of the stack, since information crossing into an operator is already governed by the boundary documents and HABITAT should declare the class and delegate rather than restate them.

## 6. The Mismatch Register (skeleton)

**Thesis.** The delta between design envelope and declared environment, written down, kept current, and consulted before a fault is attributed to the instrument. This is the document's reason for existing.

To be written: the register's form; the currency interval; the consultation requirement and its binding to TETHER section 7; and the disposition when the register is stale or absent, which is that the fault is recorded **unattributed** rather than attributed to the instrument. Fail closed, and note that this is the one place where fail closed is genuinely protective of a person rather than merely of a record.

## 7. Provisioning Parties (skeleton)

**Thesis.** An operator who does not control provisioning of a class cannot be held to an envelope they cannot reach, and the party that does control it is identifiable and is a declared field.

To be written: the declaration; the routing to the DEFER adapter when the provisioning party and the deciding party differ; and the case that gives the section its weight, an operator who cannot choose their environment at all. A school, a workplace, a household, and an institution are all provisioning parties, and where an operator is a child the provisioning party is the whole of the environment. Stated generally: where an operator has no authority over a class, a fault in that class is attributable to the provisioning party and not to the instrument. That is a specification requirement about attribution, not a claim about blame, and the text must stay on the correct side of that line.

## 8. Adaptation and the Silent Floor (skeleton)

**Thesis.** A system recalibrates around a persistently absent input and reports the recalibrated state as baseline. A class can be unprovisioned for years and produce no complaint, so no event driven check will ever fire.

To be written: the periodic re declaration requirement and its interval; why it is periodic rather than triggered; and its relationship to TETHER 5.4, which requires the same discipline on the instrument side for the same reason. The two documents converge here, and the convergence is the strongest evidence that the observation is structural rather than rhetorical.

## 9. Failure Classes and Conformance (skeleton)

To be written. Identified so far:

| # | Failure | Disposition |
|---|---|---|
| H1 | Availability declared as provision | Non conformant. Section 3. |
| H2 | Undeclared class read as adequate | The class is unprovisioned. Fail closed. |
| H3 | Input declaration missing a timing property | Rejected at write time. Section 4. |
| H4 | Fault attributed to the instrument with a stale or absent mismatch register | Recorded `unattributed`. Never an instrument fault. |
| H5 | Operator held to a class they do not provision | Attribution routed to the provisioning party. Section 7. |
| H6 | A normative value: a quantity, threshold, target, or schedule in specification text | The text is non conformant. Absolute requirement 2. |

Tiers will mirror TETHER's Attended, Referenced, Governed.
