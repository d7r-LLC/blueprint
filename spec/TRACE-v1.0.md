# TRACE: Tooling Residue, Artifact Custody, and Evidence

## Version 1.0

**Specification:** TRACE/1.0
**Status:** Draft
**Published:** (unpublished)
**Authors:** Spencer Thornock
**Repository:** `<repo>/blueprint`
**Schema:** `schema/v1/`
**License:** Apache 2.0
**Requires:** BLUEPRINT/1.0 Tier 1, CONFIDE/1.0

---

## Abstract

Every agent harness leaves a trail. Session transcripts, prompt histories, file snapshots, derived memory, temporary working directories, credential caches, telemetry, and crash logs accumulate in locations the harness chose, under a schema the harness controls, at a scale the owner did not plan for.

This residue is not incidental. It is a complete record of what an agent read, what it was asked, what it produced, and on whose authority, which makes it the most detailed audit evidence a brain has. It is also a full text copy of brain content sitting outside the record contract, outside classification, outside the ledger, and outside every gate the brain enforces. It is simultaneously the best evidence and the worst leak.

TRACE governs it. TRACE defines what an agent harness is, classifies harness artifacts into six classes with distinct handling rules, requires that every harness be registered with declared artifact roots, binds every harness session to the brain ledger through a session anchor, requires that evidence grade artifacts be sealed into a brain controlled append only store rather than trusted in place, and makes the deletion of a protected artifact a recorded act rather than a housekeeping decision.

TRACE is the third boundary. BLUEPRINT governs one brain. SPEAK governs knowledge crossing to another brain. CONFIDE governs content crossing to a model. TRACE governs content crossing into the tooling, which is the crossing that happens on every single operation and is the one nobody declared.

---

## Conformance

RFC 2119 keywords apply as described in that document.

Two requirements are absolute and admit no configuration. A harness artifact root that is not registered MUST NOT be treated as absent, and MUST be reported. A protected artifact MUST NOT be deleted without a ledger entry.

---

## Table of Contents

1. Introduction
   1.1 The third boundary
   1.2 The threat this addresses
   1.3 Relationship to Blueprint layers
   1.4 Why the harness cannot be trusted to log itself
2. Definitions
   2.1 Agent harness
   2.2 Harness artifact and artifact root
   2.3 Harness session
   2.4 Observed and attested evidence
   2.5 Sealing
3. Artifact Classes
   3.1 The six classes
   3.2 Classifying an artifact
   3.3 Mixed roots and the strongest member rule
4. The Harness Registry
   4.1 Harness records
   4.2 Declared artifact roots
   4.3 Vendor egress declaration
   4.4 Status lifecycle
5. Discovery and Enumeration
   5.1 The unregistered root invariant
   5.2 Scratch surfaces inside the brain
   5.3 Growth and scale reporting
6. Session Anchors
   6.1 Opening an anchor
   6.2 Sealing an anchor
   6.3 Joining to the call ledger
   6.4 Sessions the brain did not observe
7. Classification of Artifacts
   7.1 Sensitivity inheritance
   7.2 Custody floor union
   7.3 Classification of an unsealed session
8. Sealing and the Artifact Store
   8.1 Why in place retention is not evidence
   8.2 The copy and seal operation
   8.3 The artifact ledger
   8.4 Selective sealing and cost
9. Protected Artifacts
   9.1 Which classes are protected
   9.2 Retention periods
   9.3 Deletion as a recorded act
   9.4 Purge and legal hold
10. Class Specific Rules
    10.1 A0 Directive artifacts are authority
    10.2 A1 Session artifacts are evidence
    10.3 A2 Derived artifacts must be adopted or expired
    10.4 A3 Copy artifacts inherit and expire
    10.5 A4 Credential artifacts are excluded by construction
    10.6 A5 Telemetry artifacts are egress
11. Harness Egress
    11.1 A syncing harness is a provider
    11.2 Backup and snapshot inclusion
    11.3 Artifacts crossing to a peer brain
12. Failure Classes
13. Conformance
    13.1 Tier requirements
    13.2 Health invariants
    13.3 Self test
14. Versioning and Governance

---

## 1. Introduction

### 1.1 The third boundary

Blueprint defines a brain as a folder whose every meaningful state change is recorded. That definition holds only for changes the brain can see. An agent harness operates on the brain from outside it, and records its own version of events in its own storage, on its own terms.

The result is a parallel history that is more detailed than the brain's own. The brain's ledger records that a record moved from `draft` to `review`. The harness transcript records the reasoning, the discarded alternatives, the files consulted and rejected, the exact prompt, and the model that answered. If the two histories disagree, the harness trail is usually the one that reflects what happened.

A brain that governs its own ledger with hash chains and signatures, while leaving that richer parallel history in an untracked directory with default permissions, has not achieved auditability. It has moved the audit surface somewhere it is not looking.

### 1.2 The threat this addresses

Six distinct exposures, each of which has a different remedy, which is the reason the artifact classes in section 3 exist.

**Content escape.** A session transcript contains the full text of every record read. Records that the publication guard would never release, and that CONFIDE would restrict to a resident provider, appear verbatim in a file with no classification and no gate.

**Evidence loss.** Harness storage is mutable, compacted, rotated, and version dependent. A transcript the owner may need is deleted by a tool upgrade, and nothing records that it existed.

**Authority drift.** Agent definitions, skills, rules, and permission grants determine what agents may do. When they live only in harness storage, the brain's Layer 7 charters describe an authority model that no longer matches the one in force.

**Shadow memory.** A harness that maintains its own persistent memory is a second brain with no charter, no classification, no ledger, and no owner review, whose contents influence every future session.

**Credential proximity.** Authentication material sits beside content, and the two are captured together by any backup, sync, support bundle, or archive that treats the directory as one unit.

**Correlation and egress.** Telemetry, crash reports, and installation identifiers leave the machine on a schedule the owner did not set, and can carry file paths, project names, and prompt fragments with them.

### 1.3 Relationship to Blueprint layers

TRACE requirements attach to five existing layers. It is not a new layer, for the same reason CONFIDE is not: a control in its own layer can be omitted while conformance to the others is still claimed.

| Layer | What it carries |
|---|---|
| 2 Topology | Registered artifact roots. Declared scratch surfaces inside the brain and their exclusion from every scan. |
| 5 Classification | Sensitivity inheritance from records read to artifacts produced. |
| 6 Ledger | Session anchors. The artifact ledger. Deletion of a protected artifact as an entry. |
| 7 Agency | A0 directive artifacts as the authoritative source of agent behavior, versioned and gated. |
| 9 Operations | Sealing jobs, enumeration sweeps, retention sweeps, invariants, self test. |

### 1.4 Why the harness cannot be trusted to log itself

A harness is third party software. It is not adversarial, but it is not accountable to the brain either. It changes its storage format between versions, rotates and compacts on its own schedule, writes asynchronously, and has no obligation to record a failure in a way the brain can read.

Therefore the brain MUST NOT treat harness produced records as authoritative evidence. It MUST distinguish what it observed itself from what the harness asserts, per section 2.4, and it MUST create its own anchor for every session rather than deriving the session list from harness storage. The harness trail is corroborating detail attached to a brain owned skeleton, never the skeleton itself.

---

## 2. Definitions

### 2.1 Agent harness

An **agent harness** is any program, other than the brain's own automation, that mediates between an actor and an inference provider and is capable of reading or writing brain content. This includes command line coding agents, desktop assistant applications, editor extensions, orchestration frameworks, notebook environments, and any custom program built on a provider SDK.

A harness is distinguished from a provider. A provider performs inference and is governed by CONFIDE. A harness decides what to send, executes the resulting actions, and leaves artifacts behind. A single vendor commonly supplies both, and they MUST be registered separately, because their custody properties are unrelated.

A program that reads brain content but performs no inference is not a harness. A program that performs inference but cannot reach brain content is not a harness. Both are out of scope here.

### 2.2 Harness artifact and artifact root

A **harness artifact** is any file, directory, database, log, cache, or index created or maintained by a harness as a consequence of operating on or near brain content, and which is not itself a brain record conforming to the Layer 3 record contract.

An **artifact root** is a filesystem location under which a harness places artifacts. A harness typically has several: one in the user home directory, one inside each working directory it is invoked in, one in an operating system application support path, and one in a temporary directory.

Artifacts are defined by origin, not by location. A file the harness wrote into the brain folder is still a harness artifact, and a brain record the harness copied into its own cache is still a copy of a record.

### 2.3 Harness session

A **harness session** is one bounded interaction between an actor and a harness, as delimited by the harness itself. A session is the unit that TRACE anchors, because it is the smallest unit that a harness reliably identifies, and because sensitivity accrues across a whole session rather than per call.

A session MAY contain zero or many inference calls, and a call ledger entry MUST NOT be interpreted as a session.

### 2.4 Observed and attested evidence

Every claim recorded about a session carries an **evidence grade**.

- `observed`. Produced by a mechanism the brain controls: a hook the brain installed, a filesystem watcher, a broker call record, a git commit, a ledger entry.
- `attested`. Produced by the harness and read by the brain: a transcript file, a session index, a harness log.

A record whose grade is `attested` MUST NOT be relied upon as sole evidence for a governance conclusion, and any report presenting attested claims MUST show the grade. The distinction is what keeps the audit trail honest: it is the difference between knowing something happened and having been told it happened by the party that did it.

### 2.5 Sealing

**Sealing** is the operation of copying an artifact from a location the harness controls into a brain controlled append only store, computing its digest, and recording that digest in the artifact ledger. A sealed artifact is evidence. An unsealed artifact is a lead.

---

## 3. Artifact Classes

### 3.1 The six classes

Six classes, distinguished by the handling each requires. Classification is by function, not by filename.

| Class | Term | What it is | Governing rule |
|---|---|---|---|
| **A0** | **Directive** | Material that determines agent behavior: agent and subagent definitions, skills, rules, system prompt fragments, tool and connector configuration, permission grants, model selection defaults | Authority. MUST live inside the brain, be versioned, be gated, and be referenced by the Layer 7 charter it governs |
| **A1** | **Session** | Transcripts, prompt and command histories, tool invocation logs, plan and task files, dictation and transcription histories | Evidence. Protected. MUST be anchored and sealed |
| **A2** | **Derived** | Harness maintained memory, learned preferences, extracted facts, embeddings and semantic indexes, goal and progress state | Shadow brain. MUST be adopted into the brain as records or expired on a schedule |
| **A3** | **Copy** | File history snapshots, attachments, pasted content, generated images, screenshots, temporary working directories, worktrees, scratch clones | Derivative. Inherits classification and custody floor. MUST NOT outlive its retention period |
| **A4** | **Credential** | Authentication tokens, refresh tokens, OAuth caches, API keys, session cookies, shell environment snapshots | Excluded by construction. MUST NOT be sealed, copied, backed up with content, or referenced in any artifact the brain retains |
| **A5** | **Telemetry** | Usage counters, performance and debug logs, crash reports, installation and machine identifiers, analytics queues | Egress. MUST be declared under section 11 or disabled |

The class names are short nouns so they can be used in speech. Directive, Session, Derived, Copy, Credential, Telemetry. The parallel to the CONFIDE custody classes is intentional, and the two are orthogonal: an artifact has a class, and the session that produced it has a custody floor.

### 3.2 Classifying an artifact

Every artifact under a registered root MUST be assigned a class. Classification MAY be by pattern rule declared in the harness record, and every root MUST have a default class for unmatched paths.

The default class for unmatched paths MUST NOT be A5. An unrecognized file in a harness root is far more likely to be a session, a copy, or derived state than telemetry, and misclassifying it as telemetry is the one error that both drops it from protection and permits it to leave.

Where a path could belong to two classes, the stronger handling applies, in the order A4, A0, A1, A2, A3, A5.

### 3.3 Mixed roots and the strongest member rule

Harness roots are mixed by default. A single home directory root routinely contains all six classes at once.

Therefore a root MUST NOT be handled as a unit. Any operation applied to a whole root, including backup, sync, archive, transfer, support bundle generation, or deletion, MUST either apply the rules of every class present or be refused. In practice this means credential exclusion must be applied before any bulk operation touches a harness root, and a bulk operation that cannot exclude by path MUST NOT run.

---

## 4. The Harness Registry

### 4.1 Harness records

A brain MUST maintain a registry of harnesses at the path declared in its charter. Each record conforms to `schema/v1/harness.schema.json` and declares identity, vendor, version range, artifact roots with class rules, vendor egress posture, retention policy per class, and status.

A harness MUST be registered before it is used against brain content. An unregistered harness has no declared roots, so nothing it leaves behind can be enumerated, and nothing that cannot be enumerated can be protected.

Records are per harness and per host. The same tool on two machines is two records, because its roots, its version, and its egress settings differ per machine, and a single record would describe neither accurately.

### 4.2 Declared artifact roots

Each root declares its path, whether it is inside the brain folder, its default class, its class pattern rules, its expected growth, and whether it is sealed.

Roots MUST be declared using the path anchors required by BLUEPRINT Layer 1. A root inside the brain MUST additionally be declared in Layer 2 as an excluded surface, per section 5.2.

### 4.3 Vendor egress declaration

Each harness record MUST declare, for each of the six classes, whether the harness transmits artifacts of that class to its vendor or to any third party, and MUST state `unknown` where this is not documented. As in CONFIDE, `unknown` is not neutral: a class marked `unknown` MUST be treated as transmitted.

Where a harness transmits any artifact of class A1, A2, or A3, the harness MUST additionally be registered as a CONFIDE provider under section 11.1, because it is then an inference custody path and not merely a tool.

### 4.4 Status lifecycle

`draft`, `authorized`, `probationary`, `suspended`, `prohibited`, with the same meanings and transitions as CONFIDE section 3.5.

A harness MUST degrade to `probationary` when its observed version falls outside its declared version range. A version change is the event most likely to move, rename, or reformat an artifact root, and a registry describing the previous version's layout is worse than no registry, because it reports healthy while enumerating nothing.

---

## 5. Discovery and Enumeration

### 5.1 The unregistered root invariant

A brain MUST periodically scan for artifact roots that are not present in the registry, and MUST report each one as a health failure. The scan MUST cover, at minimum, the user home directory to a declared depth, the operating system application support and log paths, the temporary directory, and every working directory the brain is checked out in.

This is the counterpart to the CONFIDE egress invariant, and it exists for the same reason: a control that depends on the owner remembering to declare a new tool will be defeated by the first tool the owner installs and forgets. Detection is what makes the registry self correcting rather than aspirational.

### 5.2 Scratch surfaces inside the brain

Harnesses write inside the working directory. A brain MUST declare every such location as a **scratch surface** in Layer 2, and the following MUST hold for each.

- Its contents MUST NOT be counted as brain state, MUST NOT satisfy any Layer 4 gate, and MUST NOT be treated as a record by any check.
- It MUST be excluded from the publication guard's inputs, and MUST also be excluded from the guard's notion of coverage, so that an empty scan of a scratch surface never contributes to a passing result.
- It MUST be excluded from the version control working set unless its class is A0.
- It MUST be listed in the charter, so that its presence is a declared fact rather than a discovered one.

A scratch surface is the one place where a file inside the brain folder is not brain content. That exception MUST be explicit and enumerated, because an unenumerated exception is indistinguishable from a gap.

### 5.3 Growth and scale reporting

Each root MUST report its size and item count on every sweep, and a root exceeding its declared expected growth MUST be reported.

Scale is a governance property, not an operational nuisance. A root holding tens of gigabytes and thousands of session files cannot be reviewed by a person, cannot be searched quickly during an incident, and cannot be honestly described as under control. Growth reporting exists so that the moment a root passes the point of reviewability is a recorded event.

---

## 6. Session Anchors

### 6.1 Opening an anchor

A brain SHOULD open a **session anchor** when a harness session begins against brain content, and MUST have an anchor for every session by the time that session's artifacts are sealed. An anchor conforms to `schema/v1/session-anchor.schema.json`.

An anchor at open declares the harness, the host, the actor identity, the inference authorization in force, the working scope, and the anchor's own identifier. It is written to the brain ledger and is the join key for everything the session produces.

The anchor is created by the brain, not by the harness. A brain that enumerates its sessions by reading harness storage has delegated the completeness of its audit trail to the tool being audited.

### 6.2 Sealing an anchor

At session close, the anchor is sealed with the record set read and written, the call identifiers observed by the broker, the artifacts produced with their classes and digests, the computed sensitivity and custody floor per section 7, and the evidence grade of each claim.

A sealed anchor is append only and hash chained into the ledger as any other Layer 6 entry.

An anchor that is never sealed MUST be reported as `abandoned` after a declared interval and MUST be retained. Abandoned anchors are the normal result of crashes and forced quits, and they are also exactly what a session someone wanted unrecorded looks like, so they MUST NOT be silently discarded.

### 6.3 Joining to the call ledger

The relationship between the two ledgers is containment. A session anchor is the outer container. CONFIDE call records are the inner events. Every call record produced during a session MUST carry its anchor identifier, and every anchor MUST list the calls attributed to it.

Two reconciliation failures MUST be reported.

- A call record naming an anchor that does not exist. This is a call outside any recorded session.
- An anchor listing a call identifier absent from the call ledger. This is an assertion of a call that the broker never saw.

The second failure is the more informative one, because the anchor's call list is partly attested and the call ledger is observed. A disagreement between them means either the harness reached a provider without the broker, which is a CONFIDE credential isolation failure, or the harness misreported, which downgrades the trust in every other attested claim it makes.

### 6.4 Sessions the brain did not observe

Sealing MAY discover artifacts belonging to a session with no anchor. The brain MUST then create a **reconstructed anchor**, marked wholly `attested`, recording what can be recovered and stating plainly what cannot.

A reconstructed anchor MUST be reported. It MUST NOT be presented as equivalent to an observed one, and it MUST NOT be used to satisfy the invariant in section 13.2 requiring that every session be anchored. Retroactively constructing the record of an unobserved session is a mitigation. Treating it as compliance would make the invariant meaningless, since any gap could be papered over after the fact.

---

## 7. Classification of Artifacts

### 7.1 Sensitivity inheritance

An artifact's sensitivity is the **maximum** sensitivity of any record read or written during the session that produced it.

There is no partial credit and no averaging. A session that read forty public records and one `confidential` record produces a `confidential` transcript, because the transcript contains that record's text. Any scheme that dilutes sensitivity across a session's inputs will misclassify precisely the sessions that matter.

Where the record set is unknown, because the session was unobserved or the anchor is reconstructed, the artifact MUST be classified at the highest sensitivity present anywhere in the scope the session had access to. Access is the bound when readership is unknown.

### 7.2 Custody floor union

An artifact carries the strongest custody floor of any record in its session, per CONFIDE section 11.

This has a consequence worth stating explicitly. Where a session reads a record admitted from a peer brain under a floor of C1, the resulting transcript is itself C1 material. It MUST NOT then be sent to a C4 provider for summarization, MUST NOT be pasted into an unregistered tool for debugging, and MUST NOT be attached to a vendor support ticket. Support bundles are the most common way this floor is broken, and they are broken with good intentions every time.

### 7.3 Classification of an unsealed session

An artifact that has not yet been sealed carries the classification implied by its session's scope, from the moment the session opens. Classification attaches on creation, not on sealing. Otherwise every artifact would have a window of unclassified existence, and that window is where the exposure actually lives.

---

## 8. Sealing and the Artifact Store

### 8.1 Why in place retention is not evidence

A file in a directory the producing tool controls can be rewritten, compacted, rotated, truncated, or deleted by that tool at any time, including as a side effect of an upgrade the owner did not initiate. It has no digest, no chain, and no signature. It is not evidence. It is a copy of something that was true when it was written.

Referencing such a file from the ledger does not fix this. It produces a ledger that points at mutable state, which is worse than a ledger with a gap, because it reports integrity it does not have.

### 8.2 The copy and seal operation

Sealing an artifact:

1. Copies the bytes to the artifact store, which MUST be append only and MUST NOT be writable by any harness.
2. Computes the SHA-256 of the copied bytes.
3. Assigns class and sensitivity per sections 3 and 7.
4. Writes an artifact ledger entry with the digest, class, sensitivity, custody floor, source path, anchor identifier, retention expiry, and evidence grade.
5. Chains and signs that entry as any Layer 6 entry.

Sealing MUST refuse, and MUST record the refusal, where the artifact's class is A4, where its sensitivity cannot be determined, or where the artifact store is unreachable. The last case fails closed in the direction of not deleting the source: an unsealed original is a risk, and an unsealed and deleted original is a lost record.

Sealing MUST NOT move or delete the source in the same operation. Deletion of a source is a separate act, subject to section 9.3, and is permitted only after the seal is verified.

### 8.3 The artifact ledger

The artifact ledger is a Layer 6 append only log recording one entry per sealed artifact, per refusal, and per deletion. It records digests, classes, paths, and sizes, and it MUST NOT contain artifact content.

This mirrors the CONFIDE rule that the call ledger stores hashes and not prompts, for the same reason: a ledger that inlines transcript content becomes the single largest concentration of sensitive material in the brain, and it is read far more often, and by more parties, than the records it describes.

### 8.4 Selective sealing and cost

Sealing everything is not always affordable. Session artifacts at scale reach tens of gigabytes, and a brain MAY declare a sealing policy that seals selectively.

A sealing policy MUST be declared in the harness record, MUST be expressed as which sessions are sealed rather than which parts of a session are sealed, and MUST seal at minimum every session whose sensitivity is `confidential` or `third-party`, every session that wrote to a boundary surface, and every session whose anchor reports a refusal or a violation.

Partial sealing within a session is prohibited. A transcript with sections removed is not a smaller piece of evidence, it is an unfalsifiable one, since nothing in it shows what was dropped. Either a session is sealed whole or it is recorded as unsealed, and the unsealed decision is itself a ledger entry stating why.

---

## 9. Protected Artifacts

### 9.1 Which classes are protected

Classes A0, A1, and A3 are **protected artifacts**. A2 is protected once adopted, per section 10.3. A4 is never protected, because it is never retained. A5 is not protected, and is governed as egress.

A protected artifact is part of the audit trail. It is not working data, it is not cache, and it is not the harness's property, notwithstanding that the harness wrote it and stores it.

### 9.2 Retention periods

Each harness record declares a retention period per class, and each period MUST have a stated basis: the owner decision, obligation, or agreement that sets it.

Retention has a floor and a ceiling, and both matter. Too short destroys evidence. Too long accumulates a liability, since an artifact retained past its purpose is a breach surface with no remaining benefit. A retention period of `indefinite` MUST NOT be declared for any class other than A0.

An artifact whose retention has expired MUST be reported for purge and MUST NOT be purged automatically without the review required by section 9.4.

### 9.3 Deletion as a recorded act

Deleting a protected artifact MUST produce an artifact ledger entry naming the artifact digest, the class, the reason, the actor, and the authorizing decision.

An agent identity MUST NOT delete a protected artifact. This follows directly from the existing rule that agents draft and the owner decides, and it closes the obvious hole: an agent that can erase the record of what it did is unauditable regardless of how well every other control is implemented.

A harness deleting its own artifacts is not an exception to this rule, but neither is it something the brain can prevent. Where the brain observes that a previously enumerated protected artifact has disappeared without a corresponding entry, it MUST record a `protected-artifact-vanished` event with the digest if known. This is the reason sealing exists: after a seal, the harness deleting its copy is bookkeeping, and before a seal, it is evidence loss.

### 9.4 Purge and legal hold

A purge MUST be a scheduled, reviewed operation that produces a manifest of what will be deleted, requires owner approval bound to the bytes of that manifest, and writes one ledger entry per deleted artifact.

A **hold** MAY be placed on any artifact, session, scope, or time range. A held artifact MUST NOT be purged, and MUST NOT have its retention shortened, while the hold stands. A hold MUST record who placed it and why, and MUST NOT expire automatically.

Where a hold and a retention expiry conflict, the hold wins. Where a hold and a peer agreement's deletion obligation conflict, the conflict MUST be reported to the owner as a decision and MUST NOT be resolved by either default, because the correct answer depends on the obligation and cannot be encoded in advance.

---

## 10. Class Specific Rules

### 10.1 A0 Directive artifacts are authority

Agent definitions, skills, rules, and permission grants determine what agents do. They are therefore governance material, and the strictest of the class rules applies to them.

- A0 artifacts MUST be stored inside the brain, MUST be under version control, and MUST pass the same gates as any other governing record.
- Every Layer 7 agent charter MUST reference the A0 artifacts that implement it, by path and digest.
- An A0 artifact present in a harness root but not inside the brain MUST be reported as `ungoverned-directive`, and the harness MUST be treated as `probationary` until it is either brought inside or removed.
- A machine specific permission grant MAY be excluded from version control, and MUST then be enumerated and digested by the sweep, since a local grant that widens an agent's authority is exactly the kind of change that should not be invisible.
- An agent identity MUST NOT modify an A0 artifact that grants its own authority.

The distinction between A0 and everything else is the distinction between the instructions and the transcript. Both need governance, and they need opposite kinds: directives must be few, reviewed, versioned, and current, while sessions must be many, unreviewed, sealed, and historical. Storing them in the same tree, as every harness does, is what makes them easy to confuse.

### 10.2 A1 Session artifacts are evidence

Anchored per section 6, sealed per section 8, protected per section 9. Two additional rules.

- A1 artifacts MUST NOT be used as a source for any brain record without passing through the normal input flow. A transcript is not a record, and content lifted from one MUST enter at the earliest stage with `authorship: agent` and its derivation recorded.
- Prompt histories are A1. A cross session prompt history is a single file containing every instruction the owner ever gave, across every project, at the union of all their sensitivities, and it MUST be classified at that union rather than at the sensitivity of the current working scope.

### 10.3 A2 Derived artifacts must be adopted or expired

Harness maintained memory is the most dangerous class, because it is the only one that influences future behavior without being read by anyone. It is a second brain with no charter, and it grows by accretion.

- A2 artifacts MUST have a declared maximum age, and MUST NOT be declared `indefinite`.
- Each A2 artifact MUST be either **adopted** or **expired**. Adoption means its content enters the brain as records, through the input flow, with agent authorship and derivation recorded, at which point it is governed and protected. Expiry means it is deleted at its maximum age.
- A2 content MUST NOT be a source of authority. Where harness memory and a brain record disagree, the record governs. Where harness memory asserts a policy that no A0 artifact states, that policy is not in force.
- Semantic indexes and embedding stores are A2 and are also CONFIDE inference outputs. Their sensitivity inherits from the indexed corpus, and a third party index is a provider.

The adopt or expire rule exists because the alternative is a permanent, unreviewed, unclassified store of extracted facts about the owner's work, which is the exact thing the brain was built to be, except with none of the properties that made the brain trustworthy.

### 10.4 A3 Copy artifacts inherit and expire

- A3 artifacts inherit the classification and custody floor of their source, and inheritance MUST be recorded at creation.
- A copy MUST NOT outlive its declared retention, and MUST NOT be retained after its source record is deleted unless a hold applies.
- Temporary working directories, worktrees, and scratch clones are A3 and MUST be declared as scratch surfaces per section 5.2.
- A copy of a record MUST NOT satisfy a gate, and MUST NOT be counted as the record's presence anywhere. Approval binds to bytes at a declared path, and a copy at a different path is a different artifact even when its digest matches.

### 10.5 A4 Credential artifacts are excluded by construction

- A4 artifacts MUST NOT be sealed, MUST NOT be copied into the artifact store, MUST NOT be included in any backup or archive that includes content, and MUST NOT be referenced by digest in any ledger.
- A brain MUST verify, as an invariant, that no A4 artifact is present in the artifact store, in version control, or in any brain folder.
- A shell environment snapshot MUST be treated as A4 whenever it can contain exported secrets, which is the normal case. It MUST NOT be reclassified as A1 for the convenience of sealing a session whole. Where a session cannot be sealed without including a snapshot, the snapshot is excluded and the exclusion recorded, which is the sole permitted exception to section 8.4.
- Provider credentials remain subject to CONFIDE credential isolation, which is stricter. A harness holding provider credentials directly, rather than obtaining access through the broker, is a CONFIDE section 6.2 violation, and the presence of an A4 artifact containing a provider key is how that violation is usually detected.

### 10.6 A5 Telemetry artifacts are egress

- Every harness record MUST state whether telemetry is transmitted, to whom, and whether it can contain paths, project names, record titles, or prompt fragments.
- Telemetry MUST NOT be assumed to be content free. Paths and project names are content. A crash report commonly contains a fragment of what was being processed at the moment of the crash.
- Where a harness cannot disable telemetry and cannot document its contents, its telemetry posture is `unknown`, it is treated as transmitting content, and the harness MUST NOT be authorized for sessions above `none` sensitivity.
- Installation and machine identifiers are persistent correlation handles across projects and vendors. They MUST be enumerated so that the correlation surface is a known fact.

---

## 11. Harness Egress

### 11.1 A syncing harness is a provider

A harness that transmits A1, A2, or A3 artifacts to its vendor or to any third party is performing the same act as an inference call: brain content crosses to a party outside the owner's custody. It MUST be registered as a CONFIDE provider, assigned a custody class by the same rules, and constrained by the same matrix.

This closes the largest gap in CONFIDE taken alone. A brain can route every inference call through a resident provider at C0 and still ship the complete text of every session to a vendor cloud, because the harness synced its history. The inference was governed and the record still left.

### 11.2 Backup and snapshot inclusion

Backup and snapshot systems copy artifact roots as units, which triggers the mixed root rule in section 3.3.

- A backup that includes an artifact root MUST exclude A4 by path before it runs, and MUST be refused where it cannot.
- Backup destinations MUST be evaluated against the custody floor of the artifacts included. An artifact carrying a C1 floor MUST NOT be backed up to a destination that does not meet C1.
- Where a backup system cannot express path exclusions, harness roots MUST be excluded from it entirely.

### 11.3 Artifacts crossing to a peer brain

Harness artifacts MUST NOT be transferred to a peer brain under any SPEAK speech act, with one exception: a sealed artifact MAY be transferred as evidence in an incident, under an agreement that names artifact transfer explicitly, at a classification no weaker than the artifact's own.

A support bundle sent to a vendor is a transfer to a party with no agreement at all, and section 7.2 governs it.

---

## 12. Failure Classes

A brain MUST report each of the following by name.

`harness-unregistered`, `artifact-root-undeclared`, `artifact-class-unassigned`, `session-unanchored`, `anchor-abandoned`, `anchor-reconstructed`, `call-without-anchor`, `anchor-claims-unknown-call`, `seal-refused`, `seal-store-unreachable`, `artifact-unsealed-past-policy`, `protected-artifact-vanished`, `protected-artifact-deleted-without-entry`, `agent-attempted-artifact-deletion`, `retention-expired-unpurged`, `retention-indefinite-prohibited`, `hold-violated`, `credential-artifact-in-store`, `credential-artifact-in-version-control`, `ungoverned-directive`, `directive-digest-mismatch`, `agent-modified-own-directive`, `derived-artifact-past-max-age`, `derived-artifact-asserted-authority`, `copy-outlived-source`, `copy-satisfied-gate`, `telemetry-posture-unknown`, `harness-egress-unregistered`, `backup-included-credential`, `backup-below-custody-floor`, `scratch-surface-in-working-set`, `scratch-surface-counted-as-state`, `harness-version-out-of-range`, `root-exceeded-expected-growth`.

---

## 13. Conformance

### 13.1 Tier requirements

**Tier 1 Sovereign.** MUST maintain a harness registry with declared artifact roots for every harness used against brain content. MUST run the enumeration sweep of section 5.1. MUST declare every scratch surface inside the brain. MUST classify every artifact root. MUST verify that no A4 artifact is under version control.

Registration and enumeration are required at the lowest tier for the same reason cataloging is required in CONFIDE. A brain that cannot list what its tools have left behind cannot describe its own audit surface.

**Tier 2 Governed.** MUST anchor every session. MUST seal per a declared policy. MUST hold A0 artifacts inside the brain under version control, referenced by digest from the charters they implement. MUST enforce retention with recorded deletion. MUST prevent agent identities from deleting protected artifacts. MUST adopt or expire every A2 artifact. MUST reconcile anchors against the call ledger.

**Tier 3 Federated.** MUST enforce artifact custody floors including in backups and support bundles. MUST register any syncing harness as a CONFIDE provider. MUST NOT transfer artifacts to a peer except under section 11.3.

### 13.2 Health invariants

- Any artifact root not present in the registry.
- Any harness whose observed version falls outside its declared range.
- Any harness session with no anchor, where a reconstructed anchor does not satisfy this check.
- Any anchor unsealed past its abandonment interval.
- Any call ledger entry with no anchor, or any anchor claiming a call absent from the call ledger.
- Any A4 artifact in the artifact store, in version control, or in a brain folder.
- Any A0 artifact in a harness root but not inside the brain, or whose digest does not match the charter that references it.
- Any A2 artifact past its declared maximum age, or with no declared maximum age.
- Any protected artifact past retention with no purge decision, or missing with no deletion entry.
- Any scratch surface present in the version control working set or counted by any gate.
- Any root exceeding its declared expected growth.
- Any harness with telemetry posture `unknown` authorized above `none` sensitivity.

### 13.3 Self test

A Tier 2 brain MUST publish a self test that, at minimum:

1. Creates an artifact root outside the registry and asserts the sweep reports `artifact-root-undeclared`.
2. Places a synthetic credential file in the artifact store and asserts `credential-artifact-in-store`.
3. Writes a synthetic A0 artifact into a harness root and asserts `ungoverned-directive`.
4. Alters a digest referenced by a charter and asserts `directive-digest-mismatch`.
5. Attempts deletion of a protected artifact as an agent identity and asserts refusal.
6. Places a file in a scratch surface that would satisfy a gate and asserts the gate does not pass.
7. Emits a call record naming a nonexistent anchor and asserts `call-without-anchor`.
8. Seals a session containing a `confidential` record and asserts the resulting artifact is classified `confidential` and carries the strongest floor in that session.

A control that has never been observed to refuse has not been demonstrated to work. This applies with particular force here, because every one of these controls governs a path that currently works by default and silently.

---

## 14. Versioning and Governance

As BLUEPRINT/1.0 section 14. Any change to the artifact class definitions in section 3.1, to the protected class list in section 9.1, or to the credential exclusion rules in section 10.5, is at minimum MINOR. Any change that removes a class from protection, permits indefinite retention of a class other than A0, or weakens credential exclusion, is MAJOR.
