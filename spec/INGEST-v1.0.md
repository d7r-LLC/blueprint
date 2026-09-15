# INGEST: the inbound boundary

## Version 1.0

**Specification:** INGEST/1.0
**Status:** Draft. Sections 1 through 11 are written.
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Requires:** BLUEPRINT/1.0 Layer 4 for record identity and Layer 8 for boundary. DEFER/1.0 for the authority that admits material. POLARIS/1.0 for the refusals that reject it.
**Relates to:** SPEAK/1.0, CONFIDE/1.0, and TRACE/1.0 govern the three outbound crossings. This document governs the inbound one.
**License:** Apache 2.0

---

> **Status note.** Draft, published for review. An implementation MUST NOT claim INGEST conformance while this Status reads Draft.

---

## Abstract

INGEST names the letters **I**ntake, **N**ormalization, **G**ates, **E**vidence, **S**ource, and **T**raceability.

Blueprint declares three boundaries and all three point outward. SPEAK governs what crosses to another brain, CONFIDE what crosses to a model, TRACE what crosses into tooling. Every one of them asks the same question about material already inside: may this leave, and under what custody.

None of them asks how it got in.

That is the gap this document closes. A brain that governs its exports and admits its inputs unexamined has an audit trail that terminates in a shrug. The provenance chain reads back cleanly through every transformation and then stops at a file that appeared, from somewhere, at some time, asserted by nobody.

INGEST specifies that material entering a brain is attested by a person before it is processed, that the original is preserved and hashed before it is touched, that cleanup is mechanical and separately certified, that every downstream sentence carries a path back to a certified source, and that the authorship of any published artifact is declared rather than assumed.

It specifies no capture device, no transcription engine, no storage layout, and no editorial standard. Two conformant brains may ingest completely different material through completely different tools. INGEST governs the evidence, not the instrument.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Three requirements are absolute.

1. **No inference of attestation.** An implementation MUST NOT treat the presence of a file, the success of a job, or the passage of time as an attestation. Absent an explicit signed claim, material is unattested and MUST be handled as such.
2. **No silent authorship.** An implementation MUST NOT publish an artifact whose authorship class is undeclared. An undeclared class is malformed, not a default.
3. **No retroactive certification.** A certification MUST bind a hash computed at the moment of certification. Certifying material by reference to a path, a filename, or a version is malformed, because none of them constrain the bytes.

Requirement 3 is what separates this document from a filing convention. A signature over a location proves that somebody once looked at something in that location. A signature over a digest proves what they looked at.

---

## Table of Contents

1. Introduction
2. Definitions
3. Attestation
4. Preservation
5. Normalization and certification
6. Authorship classes
7. Composition and traceability
8. Surface classes
9. Disclosure
10. Records
11. Failure classes

---

## 1 Introduction

### 1.1 The boundary nobody declared

Blueprint's boundary layer is written from the position of a brain that already holds something and is deciding whether to let it out. This is the right shape for exchange, inference, and tooling. It is the wrong shape for the first moment, when material is not yet held by anyone and its origin is still a live question.

The asymmetry has a practical cost. A brain can enforce custody classes on every model call, sign every utterance to every peer, and seal every session artifact, and still be built on a foundation of files whose origin is undocumented. The governance is real and it is applied one layer too late.

### 1.2 What an unattested input costs

Three failures follow from admitting material without a claim about where it came from.

The provenance chain cannot close. A published claim traced backward arrives at a source record and stops, because the source record asserts nothing about itself.

Consent cannot be established. Material involving other people carries obligations that depend entirely on the circumstances of capture, and those circumstances are exactly what an unattested file does not record.

Authorship cannot be distinguished. Once machine-generated text and captured human speech sit in the same store with the same shape, no later process can reliably tell them apart, and every downstream artifact inherits the ambiguity.

### 1.3 Position in the stack

INGEST sits before Layer 4 record creation. Material that has not cleared INGEST is not yet a record and MUST NOT be cited, exchanged, submitted for inference, or drawn on for composition.

DEFER governs who may admit material. POLARIS governs whether the brain will admit it at all. INGEST governs the evidence that admission produces.

---

## 2 Definitions

**Capture.** A recording, document, image, or file originating outside the brain, before any processing.

**Attestation.** A signed claim by a person about a capture: what it is, how it was made, and who was present. An attestation is made by a party, never by a process.

**Attesting party.** The person whose signature the attestation carries. This party MUST be a human being. An agent MAY prepare an attestation and MUST NOT sign one.

**Preservation record.** The immutable record of a capture: its digest, its size, its store location, and the time it was preserved.

**Normalization.** Mechanical transformation that changes form and not content. Transcription, transcoding, punctuation, and correction of evident mishearing are normalization. Condensing, reordering, improving, and summarizing are not.

**Certification.** A signed claim by a person that a normalized artifact is faithful to its capture. Distinct from attestation, which concerns origin.

**Certified source.** A normalized artifact carrying a valid certification. The only material eligible to compose a curated artifact.

**Authorship class.** The declared relationship between a published artifact and the human whose name is on it. Values in section 6.

**Surface class.** The category of a published artifact, which determines the authorship class it requires. Values in section 8.

**Trace path.** The chain from a published sentence back to the certified source it derives from, or to a declaration that the author composed it directly.

---

## 3 Attestation

### 3.1 The entry condition

An attestation MUST exist before any processing step runs against a capture. An implementation MUST reject a capture with no attestation rather than queue it, and MUST NOT create a preservation record for it.

This ordering is the whole point. Attestation after processing certifies a pipeline output, which is not the claim anyone needs.

### 3.2 Claims

An attestation MUST carry exactly one claim from the following set.

| Claim | Meaning |
|---|---|
| `authentic-capture` | The attesting party made this recording, it is of the events it appears to be of, and it has not been altered. |
| `received-capture` | The attesting party received this from a named origin and did not make it. |
| `synthetic` | This was generated by a machine, in whole or in part. |
| `unknown-origin` | The attesting party holds this and cannot account for its origin. |

`unknown-origin` is a valid claim and it is not a failure. It is how a brain admits an old file honestly. Material attested `unknown-origin` MUST NOT compose a curated artifact under section 7.

An attestation MUST NOT carry more than one claim. A capture that is partly synthetic is `synthetic`.

### 3.3 Presence

When a capture involves identifiable people other than the attesting party, the attestation MUST record them, and MUST record the consent state for each: `granted`, `pending`, or `refused`.

`pending` and `refused` both block publication. They differ in whether asking again is meaningful.

### 3.4 Signature

An attestation MUST bind the digest of the capture, computed before preservation. An attestation whose digest does not match the preserved bytes is invalid and the capture MUST be treated as unattested.

---

## 4 Preservation

### 4.1 Original bytes

The capture MUST be preserved byte for byte before normalization. The preserved copy MUST be verified by digest comparison after the copy completes, and a mismatch MUST abort the ingest.

### 4.2 Separation

The preserved capture SHOULD be stored outside the working set of the brain. The brain retains the preservation record. This keeps large media out of the record store without weakening the chain, because the digest binds them.

### 4.3 Immutability

A preserved capture MUST NOT be modified. An edited version, including one edited for release, is a derived artifact with its own digest and its own record, and MUST reference the capture it derives from.

This is the requirement that makes a released edit auditable. The published cut and the original both exist, both are hashed, and the relationship between them is recorded rather than implied.

---

## 5 Normalization and certification

### 5.1 Mechanical only

Normalization MUST preserve content. An implementation MUST NOT condense, reorder, improve, summarize, or complete during normalization.

The test is whether the author would recognize a sentence as one they said. Fixing a transcription error passes. Fixing a sentence does not.

### 5.2 The raw artifact is immutable

The first machine-readable rendering of a capture MUST be immutable once written. Corrections MUST produce a new artifact rather than edit it.

An implementation SHOULD retain a timed rendering alongside the raw one where the capture is time-based, because downstream artifacts that reference positions in the capture depend on it.

### 5.3 Certification

A normalized artifact becomes a certified source when a person signs a certification binding its digest.

An agent MUST NOT certify. An agent MAY prepare a normalized artifact and present it for certification.

### 5.4 What certification means

Certification asserts faithfulness to the capture. It does not assert that the content is true, publishable, consented to, or good. Those are separate determinations under other documents.

---

## 6 Authorship classes

Every published artifact MUST declare exactly one class.

| Class | Meaning | Machine participation |
|---|---|---|
| `curated` | Every sentence traces to certified source, or to the author's direct composition. | Assembly and mechanical editing only. No generated sentences. |
| `assisted` | The author composed the artifact with machine help that reached the sentences. | Permitted, and disclosed. |
| `generated` | The artifact was produced by machine from records the author approved. | Full. |

The classes are ordered by human authorship and an artifact takes the weakest true class. An article that is ninety-five percent curated and carries three generated sentences is `assisted`.

`curated` is a claim about every sentence. It is not a claim about effort, intent, or overall proportion.

---

## 7 Composition and traceability

### 7.1 The composition rule

A `curated` artifact MUST be composed only from:

1. certified sources attested `authentic-capture`, or
2. text the author wrote or assembled directly.

Material attested `received-capture`, `synthetic`, or `unknown-origin` MUST NOT compose a `curated` artifact. It MAY be quoted with attribution, which is a citation rather than composition.

### 7.2 Trace paths

A `curated` artifact MUST carry a trace path resolving every passage to a certified source or to a direct-composition declaration.

The trace path MUST reference certified sources by digest. Referencing them by title or path does not satisfy this, for the reason given in absolute requirement 3.

### 7.3 Granularity

An implementation MUST declare the granularity at which it traces: per artifact, per section, or per sentence. Coarser granularity is permitted and MUST be stated, because an undeclared granularity invites a reader to assume the finest one.

### 7.4 What a trace path is not

A trace path is not a bibliography. It does not establish that a claim is true, only that a sentence came from where it says it came from.

---

## 8 Surface classes

### 8.1 Required authorship by surface

An implementation MUST declare, for each surface it publishes, the weakest authorship class that surface accepts.

| Surface class | Examples | Weakest acceptable |
|---|---|---|
| `authored` | Articles, essays, blog posts, books, official statements | `curated` |
| `derived` | Summaries, indexes, inventories, show notes, changelogs | `generated` |
| `operational` | Documentation, process pages, reference material | `generated` |

An artifact whose class is weaker than its surface accepts MUST NOT publish there. An artifact stronger than required MAY publish anywhere.

### 8.2 Why the split exists

The distinction is not about quality. An episode inventory is a list of things named in a recording, and a machine builds it from approved records more accurately than a person does at one in the morning. Generating it is correct.

An article is a person saying something. Generating it produces a document that reads as though somebody meant it when nobody did, and the reader has no way to tell. That is the failure this separation exists to prevent.

---

## 9 Disclosure

### 9.1 Visible declaration

A published artifact MUST declare its authorship class where a reader encounters the artifact, not only in metadata a reader would have to seek out.

`generated` and `assisted` artifacts MUST carry the declaration visibly. A `curated` artifact MAY carry it visibly and MUST carry it in metadata.

### 9.2 Wording

An implementation MUST NOT phrase a disclosure so that it can be read as decoration or as a disclaimer of responsibility. The author remains responsible for a `generated` artifact published under their name.

### 9.3 Inherited class

An artifact that embeds another takes the weakest class present. A page combining a curated essay with a generated summary is `assisted` at the page level, and the parts MAY be declared separately where the boundary between them is visible to the reader.

---

## 10 Records

Four record types. JSON Schema files live in `schema/v1/`.

### 10.1 Source attestation

`source-attestation.schema.json`

Required: `contractVersion`, `attestationId`, `captureDigest`, `digestAlgorithm`, `claim`, `attestedAt`, `attestingParty`, `signature`.
Optional: `capturedAt`, `device`, `origin`, `presentParties`, `notes`.

`digestAlgorithm` MUST be a member of the SHA-2 or SHA-3 families. MD5 and SHA-1 MUST NOT be used, because neither offers collision resistance and both therefore fail to bind a specific artifact.

### 10.2 Preservation record

`preservation-record.schema.json`

Required: `contractVersion`, `preservationId`, `attestationId`, `digest`, `digestAlgorithm`, `bytes`, `storeLocation`, `preservedAt`, `verified`.

`verified` records the post-copy digest comparison. A record with `verified: false` MUST NOT be cited.

### 10.3 Source certification

`source-certification.schema.json`

Required: `contractVersion`, `certificationId`, `preservationId`, `artifactDigest`, `digestAlgorithm`, `normalization`, `certifiedAt`, `certifyingParty`, `signature`.

`normalization` names the transformations applied, so a reader can tell what was permitted to change.

### 10.4 Authorship record

`authorship-record.schema.json`

Required: `contractVersion`, `authorshipId`, `artifactDigest`, `digestAlgorithm`, `class`, `surfaceClass`, `traceGranularity`, `declaredAt`.
Required when `class` is `curated` or `assisted`: `tracePath`.
Required when `class` is `assisted` or `generated`: `disclosure`.

`tracePath` is an array of entries, each carrying either `certificationId` and `sourceDigest`, or `directComposition: true`.

---

## 11 Failure classes

| Code | Failure |
|---|---|
| `IN-01` | Capture processed with no attestation |
| `IN-02` | Attestation digest does not match preserved bytes |
| `IN-03` | Attestation signed by a non-human party |
| `IN-04` | Preservation digest comparison failed or absent |
| `IN-05` | Preserved capture modified in place |
| `IN-06` | Normalization altered content |
| `IN-07` | Raw artifact edited rather than superseded |
| `IN-08` | Certification by a non-human party |
| `IN-09` | Certification bound to a path rather than a digest |
| `IN-10` | Published artifact with undeclared authorship class |
| `IN-11` | `curated` artifact composed from uncertified material |
| `IN-12` | `curated` or `assisted` artifact with no trace path |
| `IN-13` | Trace path referencing sources by name rather than digest |
| `IN-14` | Undeclared trace granularity |
| `IN-15` | Artifact published to a surface that requires a stronger class |
| `IN-16` | `assisted` or `generated` artifact published without visible disclosure |
| `IN-17` | Consent state `pending` or `refused` at publication |
| `IN-18` | Broken digest algorithm used to bind any record in this document |

---

## Design notes

Three choices in this document are contestable and are recorded as choices rather than presented as obvious.

**Attestation is a human act with no machine equivalent.** An automated capture pipeline cannot attest to its own output, which means fully unattended ingest is not conformant. This is deliberate and it is expensive. The alternative is a chain whose first link is an assertion nobody made.

**`unknown-origin` is admitted rather than refused.** A specification that refuses unattested material forces implementers to either lie or abandon their existing archive. Admitting it under an honest label, and barring it from curated composition, keeps the archive and keeps the guarantee.

**Authorship takes the weakest true class.** The alternative, a proportional or majority rule, produces the outcome where an article is called curated because most of it was. Most is not the claim that matters to a reader asking whether a person meant the sentence in front of them.
