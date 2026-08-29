# Blueprint: Workflow and Specification Design

Non normative working note. This file records rationale and open options, not requirements.
It is the one file in this repository permitted to cite machine absolute reference paths, because its purpose is to record what was read. No specification text under `spec/` may do so.

Status: design proposal for review. Nothing here is adopted until you accept it as a decision record.
Prepared: 2026-08-25. Grounded in `~/code/obsidian` (57 decision records, `brain/AGENTS.md` at 62,430 bytes, ~6,200 lines of existing bridge machinery), `~/code/epic/saga-standard`, `~/code/epic/derp-spec`, `~/code/epic/agent-rights`, and `audit/2026-08-23-distributed/architecture-review.md`.

---

## 1. What this is and where it sits

You already own three specs that stack cleanly:

```
Agent Bill of Rights (ABR)      policy: what agents deserve
        |
        v
DERP Specification              runtime: what the environment must provide
        |
        v
SAGA Standard                   format: how an agent is represented
```

Blueprint is the fourth member, and it answers a question none of the other three answer: **where does the knowledge live, who owns it, and how does it move between owners.** SAGA moves an agent. Blueprint moves a thought.

```
ABR        what agents deserve
DERP       what the runtime must provide
SAGA       how an agent is represented
Blueprint  how knowledge is held, governed, and exchanged between brains
```

Two documents, not one. Blueprint defines the vessel. A companion protocol defines the wire.

| Spec | Id | Scope |
|---|---|---|
| **Blueprint** | `BLUEPRINT/1.0` | Structure, governance, and configuration of a single brain. Ten layers. |
| **SPEAK** | `SPEAK/1.0` | Signed Provenance Exchange for Attributable Knowledge. Brain to brain transfer. |

`SPEAK` is a naming proposal, chosen to match the house style of playful vocabulary over serious guarantees, and because it fits your own metaphor exactly: a human speaks a word and the word becomes part of another mind. The transfer unit is an **utterance**. The sender **says**, the receiver **hears**, and neither shares a mind. If you want the plain option instead, `BXP/1.0` (Brain Exchange Protocol) carries the same content with no metaphor. Everything below works under either name.

### The one-sentence thesis

A brain is a locally owned, policy-governed, append-only-audited folder of plain text, and knowledge leaves it only as a signed, classified, gate-approved utterance that the receiving brain must independently admit.

---

## 2. Ten insights that shape the design

These came out of reading what you already built. They are the load-bearing observations.

**1. You already have the constitution pattern.** `brain/AGENTS.md` outranks every guide, plugin, and code registry, and says so explicitly: "`vaultlib.CONTROLLED` is **the** registry, `AGENTS.md` is its source of truth, when the two disagree `CONTROLLED` is the bug." A spec cannot invent that. It can require it. Layer 1 of the Blueprint is "there must be exactly one file that wins."

**2. Domains are discovered, not registered.** Decision `0030`: automation globs `*/Domain Manifest.md` for `automation: active`. There is no central list to keep in sync. This is the single most portable idea in your vault and the Blueprint should make it normative, because it is what lets a brain grow without a maintainer.

**3. A domain is already a counterparty.** `brain/d7r/` is your private knowledge *about* D7R. `brain/Epic/` is your private knowledge about Epic. You did not build those as topics. You built them as relationships. So the boundary between brains belongs **inside the domain**, and your instruction to log output in the d7r domain folder is not a convenience, it is the correct architecture. State it as a rule: *the personal brain's name for a counterparty is a domain; the organizational brain's name for a counterparty is a contributor.* The boundary machinery is the same shape, mounted at two different places.

**4. Gates already work and the reason is the hash.** Decision `0005`: compute the SHA-256 *after* writing approval metadata, so editing an approved artifact re-blocks it automatically. Approval cannot be inherited by changed text. That single mechanic is what makes an approval gate real rather than decorative, and it must survive into the export gate.

**5. Location is not permission.** Decision `0018`: "Presence in an `Outputs/` folder is **not** publication. The guard fires on promotion, not on location." The inbound direction needs the exact mirror, and this is the design's symmetry: presence in an inbox is not knowledge. Admission is not adoption.

**6. There is no publisher agent, on purpose.** Decision `0028`. Publication stays human plus script. So the export gate must also stay human plus script, and no agent identity may ever be the thing that authorizes an utterance.

**7. Your outbox is already better than most production systems, and it has no signatures.** `flowstate_outbox_contract.py` is 2,518 lines of SQLite WAL append-only ledger with a monotonic per-operation sequence, trusted DB-side timestamps, per-org fencing tokens, an 11-state machine, and genuine reconciliation where an ack is explicitly not a confirmation and only an authoritative readback promotes to `confirmed`. What it does not have: any cryptography beyond `hashlib`. The only `hmac` use in the entire repository is `hmac.compare_digest` at `flowstate_bridge_contract.py:356`, a constant-time comparison. There is no keypair, no signing function, no verification function. **Signing is genuinely new work, and everything else is reuse.**

**8. Your outbox is metadata-only, and knowledge transfer is content.** `PRIVACY_CLASSES = {"internal-metadata"}` and `PRIVACY_DENY_KEYS` blocks `body`, `content`, `excerpt`, `notebody`, `transcript`. That stance is correct for a project-tracking bridge and fatal for a knowledge bridge. The Blueprint needs content-carrying classes with explicit redaction rules, which is precisely what SAGA 13.5 already models.

**9. Mutual exclusion over an eventually consistent file sync is impossible, and you already proved it.** The distributed review is unambiguous: "Two machines each create `lock.json`; Sync accepts both. That is not a weak lock, it is worse than no lock, because it looks like one and will be trusted." The finding that matters for SPEAK: a non-forced git push is a server-side compare-and-swap, so **Forgejo refs are a linearizable serializer you already own.** Sync carries the watermark, advisory. Refs carry the authority, binding. Never decide on the watermark.

**10. Every mechanism that requires standing human attention will rot.** Also from the review, evidenced: the pickle queue at 6 requests and 0 responses, gates at 44/44 pending. This is the most important non-technical constraint in the whole design. A protocol whose safety depends on you remembering to reconcile is already broken. Every gate needs either a TTL, a fail-closed default, or a CI check that goes red.

---

## 3. The Blueprint: ten layers

Mirrors SAGA's layer structure so the two read as siblings. Each layer is independently conformable. A brain declares which layers it implements, in its Charter.

| # | Layer | Owns | Existing analogue in your vault |
|---|---|---|---|
| 0 | **Charter** | Brain identity, ownership, legal entity, keys, lineage, license | (new) |
| 1 | **Constitution** | The one governing file, precedence, prime directives, path anchors | `brain/AGENTS.md`, decision `0047` |
| 2 | **Topology** | Folder taxonomy, domains, manifests, shared entity layer | decisions `0030`, `0020`, `automation/new_domain.py` |
| 3 | **Records** | Frontmatter contract, controlled vocabularies, ids, filenames, derived state | decisions `0022`, `0023`, `0052` |
| 4 | **Lifecycle** | Sources vs works, stages 0 to 10, gates, change authority, source hierarchy | decisions `0016`, `0003`, `0004`, `0005`, `0039` |
| 5 | **Classification** | Sensitivity, visibility, consent, privacy classes, publication guard | decisions `0017`, `0018`, `0019`, `0038` |
| 6 | **Ledger** | Append-only log families, sequencing, hash chaining, trusted time, decision records | decision `0036`, `automation/newlog.py` |
| 7 | **Agency** | Agent identities, authorities, enforcement hook, authorship policy | decisions `0027`, `0028`, `0029`, `0035`, `0037`, `automation/guard.py` |
| 8 | **Boundary** | Input and output flows, peers, agreements, utterances, receipts, reconciliation | `flowstate_*_contract.py` (outbound, metadata-only) |
| 9 | **Operations** | Automation, host roles, schedulers, verification, conformance self-test, invariants | `automation/`, `scripts/ci.sh`, the distributed review |

Layer 8 is the new work. Layers 0 through 7 are largely a clean-room generalization of what you have, which decision `0050` already requires: "The distributable template is built from scratch as a generic scaffold. This vault may be read as a reference; it is never the source of the template artifact."

### Layer notes worth flagging now

**Layer 0, Charter.** This is where your ownership question becomes machine-readable rather than a memory. A Charter declares `brainId`, the owning legal entity, the signing keys, and a `lineage` block. Your Epic to D7R transfer is a lineage entry:

```yaml
brainId: brain:spencer-thornock
owner: { kind: individual, legalName: "Spencer Thornock" }
lineage:
  - derivesFrom: "FlowState Method"
    originEntity: "d7r LLC"
    originOwner: "Spencer Thornock"
    relationship: derivative-work
    rightsBasis: sole-ownership-of-origin-entity
    transferPlanned: "D7R LLC"
    transferStatus: pending
```

Two reasons this belongs in the spec and not in a lawyer's folder. First, a receiving brain can verify chain of title before admitting knowledge. Second, when the transfer completes, it is one signed Charter revision with an append-only lineage entry, not an archaeology project.

**Layer 3, Records.** Add one property the vault does not yet carry: `authorship`, from your decision `0007` (per-surface authorship policy). Values `human`, `agent-drafted-human-approved`, `agent`. It matters at the boundary, because the receiving brain has a legitimate interest in knowing whether a claim was authored or generated, and ABR Right IX (Transparency) points the same direction.

**Layer 4, Lifecycle.** Add a sixth gate: `gate_export_approval`, on the record or work being sent, bound to the SHA-256 of the exact bytes exported, computed after writing the approval metadata. Same mechanic as `gate_publication_approval`, different destination. Publication is "the world may read this." Export is "brain X may hold a copy of this." Those are different decisions and must be different gates.

**Layer 5, Classification.** Adopt SAGA 13.5's four levels rather than inventing new ones, and map them onto your existing `sensitivity` property:

| SPEAK classification | Meaning | Interaction with your `sensitivity` |
|---|---|---|
| `brain-portable` | Belongs to the speaker. Travels as-is. | any |
| `public` | Non-sensitive, already publishable. | `sensitivity` absent |
| `peer-internal` | Shareable with this peer under agreement. Titles and summaries travel, bodies may be redacted. | `personal` requires deliberate author choice |
| `peer-confidential` | Named peer only, never onward. Stripped from any further utterance. | `confidential` may reach this class only by explicit agreement |

And keep your hard rule intact: `sensitivity: confidential` is never publishable. Under SPEAK it becomes never publishable *and* never exportable except as `peer-confidential` under an agreement that names it. `third-party` with `consent_status` not `granted` blocks export absolutely, same as publication.

**Layer 6, Ledger.** One change to what you have: the existing `operation_events` chain links *state* (`operation_id, sequence, previous_state, next_state`) but not *content*. There is no `previous_record_sha256`. For cross-brain audit the receiving side must be able to prove the sender's log was not rewritten, so boundary ledgers get a content hash chain: every entry carries `prevEntrySha256`, and the head hash is what a peer attests to. Internal ledgers can stay as they are.

**Layer 9, Operations.** Carry the distributed review's conclusions in as normative requirements, because they are physics and not preference: exactly one host owns each mutable state root; authority-bearing state uses a compare-and-swap serializer; advisory state may use eventually consistent sync and may never be decided on; every lease has a TTL and is stealable; identifiers are coordination-free (timestamp plus entropy, never "next free NNN"); a brain that cannot reach its serializer refuses to act rather than falling back to local state.

---

## 4. Conformance tiers

Three tiers, mirroring DERP. Each includes the one below. A brain claims a tier in its Charter, and a peer may refuse to exchange with a brain below a required tier.

**Tier 1: Sovereign.** Layers 0 to 3, plus Layer 6 internal ledgers. A local folder that is owned, structured, and logged. Plain text is the source of truth. No exchange. This is a real and useful destination, and most individuals should stop here for months.

**Tier 2: Governed.** Adds Layers 4, 5, 7, and a publication guard. Gates are hash-bound. Classification exists and is enforced at exactly one boundary by a script that exits non-zero. Agents may draft and may never approve. This tier is what makes a brain safe to publish *from*.

**Tier 3: Federated.** Adds Layer 8 and Layer 9. Signed bidirectional exchange with reconciliation, an admission gate, a peer registry, key rotation and revocation, and a conformance self-test that a peer can run against you. Only a Tier 3 brain may participate in SPEAK.

The tiers are also the curriculum ladder, which is a happy accident worth using: your three courses already share one twelve-theme arc, and D7R-1 Explorer, D7R-2 Operator, D7R-3 Architect map onto Sovereign, Governed, Federated with almost no strain.

---

## 5. SPEAK: the exchange protocol

### 5.1 The five objects

**Brain identity.** A brain is identified by a URN, `brain:<handle>`, reusing the `brain:` namespace your bridge contract already validates (`SOURCE_KEY_RE = ^brain:[A-Za-z0-9][A-Za-z0-9._:/-]*$`). Your brain is `brain:spencer-thornock`. The org brain is `brain:d7r`. Each brain holds an Ed25519 keypair per host. Public keys and `keyId`s are declared in the Charter; private keys live in the OS keychain and never in the vault. Where a brain also has a SAGA identity, the Charter cross-references the wallet address, so a human contributor and an agent contributor are the same kind of citizen. That satisfies your requirement to use agent identity for all creators of knowledge including humans.

**Peer Agreement.** The bilateral contract, and the heart of your requirement that each brain sets its own rules for what transfers. Both sides sign it, both sides keep a copy, and it is content-addressed so every utterance can cite the exact agreement version that authorized it. This is your `AUTHORITY_KEYS` object generalized from one org to a peer relationship.

```yaml
agreementId: agr:spencer-d7r/v1
parties:
  - { brainId: brain:spencer-thornock, role: contributor, keyIds: [k1] }
  - { brainId: brain:d7r, role: organization, keyIds: [k7] }
directions:
  outbound:                       # what I may say to d7r
    scopes: ["d7r/**"]            # only from my d7r domain
    classifications: [brain-portable, public, peer-internal]
    recordTypes: [decision, concept, output, idea, area, project]
    acts: [assert, revise, retract]
    maxSensitivity: personal      # requires deliberate author choice per record
    denyKeys: [credential, secret, token, apikey, password, absolutepath]
  inbound:                        # what d7r may say to me
    scopes: ["**"]
    classifications: [brain-portable, public, peer-internal]
    onwardTransfer: prohibited    # peer-confidential never re-exported
retention: { onRetract: tombstone-and-quarantine, onRevoke: retain-with-frozen-provenance }
requiredTier: 3
revocation: { effectiveOn: signed-notice, keyRevocationList: "System/Identity/krl.json" }
agreementSha256: "<computed>"
signatures:
  - { brainId: brain:spencer-thornock, keyId: k1, alg: ed25519, sig: "..." }
  - { brainId: brain:d7r, keyId: k7, alg: ed25519, sig: "..." }
```

**Utterance.** The transfer unit. One envelope, one or more records, one signature.

```json
{
  "contractVersion": "speak-utterance/v1",
  "utteranceId": "01J9XZ...",
  "idempotencyKey": "utter:v1:<sha256 of canonical payload>",
  "agreementSha256": "<pins the authorizing agreement version>",
  "speaker":  { "brainId": "brain:spencer-thornock", "actorId": "saga:0xabc...", "keyId": "k1" },
  "listener": { "brainId": "brain:d7r" },
  "act": "assert | revise | retract | request | acknowledge",
  "scope": { "originDomain": "d7r", "targetHint": "Areas/Frontier Academy" },
  "classification": "peer-internal",
  "sensitivity": "none",
  "consent": { "required": [], "status": "n/a" },
  "authorship": "agent-drafted-human-approved",
  "records": [
    { "recordId": "rec:...", "type": "decision", "title": "...",
      "path": "records/rec-....md", "bodySha256": "...",
      "supersedes": null, "originRecordId": "..." }
  ],
  "payloadSha256": "...",
  "sourceRevisionSha256": "...",
  "provenance": { "originBrainId": "brain:spencer-thornock", "derivedFrom": [], "redactionManifestSha256": null },
  "gate": { "gate_export_approval": "approved", "approvedArtifactSha256": "...", "approvedAt": "...", "approvedBy": "author" },
  "emittedAt": "2026-08-25T11:00:00Z",
  "prevEntrySha256": "<hash chain link to the previous Out ledger entry>",
  "signature": { "alg": "ed25519", "keyId": "k1", "sig": "..." }
}
```

Signature is computed over RFC 8785 canonical JSON of the envelope with `signature` excluded, exactly as SAGA 16 specifies, so verification code is shared between the two specs. Canonicalization keeps your existing strictness: duplicate object keys rejected, `NaN` and `Infinity` rejected, Unicode normalized.

**Receipt.** The receiving brain's signed answer, and the thing that makes your reconciliation requirement real.

```json
{
  "contractVersion": "speak-receipt/v1",
  "receiptId": "...", "utteranceId": "...", "payloadSha256": "...",
  "listener": { "brainId": "brain:d7r", "keyId": "k7" },
  "verdict": "admitted | quarantined | rejected",
  "failureClass": null,
  "observedAt": "...", "prevEntrySha256": "...",
  "signature": { "alg": "ed25519", "keyId": "k7", "sig": "..." }
}
```

**Bundle.** The normative wire format. Transport agnostic by design, so git, filesystem, USB, or object storage all work. Mirrors the `.saga` ZIP layout deliberately.

```
<name>.brainpack                  ZIP archive
  manifest.json                   bundle header, agreementSha256, utterance index, merkle root
  utterances.jsonl                hash-chained utterance envelopes, one per line
  records/<recordId>.md           payload records, plain markdown with frontmatter
  attachments/                    binary assets, referenced by sha256
  META                            format version, per-file checksum manifest
  SIGNATURE                       detached Ed25519 signature over the SHA-256 of all other files
```

A receiver MUST verify `SIGNATURE` before reading anything else, and MUST verify each utterance signature independently. Bundle-level and utterance-level signatures are both required, because the bundle proves who assembled the shipment and the utterance proves who authored each claim.

### 5.2 The two guards, and the symmetry

This is the conceptual core.

```
                 OUTBOUND                                    INBOUND
        ---------------------------                 ---------------------------
        record in brain                             bundle arrives
              |                                             |
        [ export check ]  <- script, exit non-zero    [ admission check ] <- script
        6 conditions, hash-bound gate                 8 conditions, signature-bound
              |                                             |
        Out ledger entry (append-only, chained)       In ledger entry (append-only, chained)
              |                                             |
        bundle emitted                                staged in Boundary/In/Quarantine/
              |                                             |
        awaits signed receipt                         routing decision by a human
              |                                             |
        reconciled                                    adopted into the brain proper
```

**The export check** extends your existing six-point publication check with export-specific conditions: no `confidential` material in the record or anything it links to; every `third-party` dependency has `consent_status: granted`; every `[!private]` callout resolved; `gate_export_approval: approved` with a hash matching the exact bytes; the agreement permits this classification, scope, record type, and act; no denied key appears anywhere in the payload tree. Exit 0 is the only path to an outbound bundle.

**The admission check** is the mirror, and it is entirely new: bundle `SIGNATURE` verifies; every utterance signature verifies against a `keyId` that is in the Charter and not on the revocation list; `agreementSha256` matches a locally held, locally signed agreement; the utterance's classification, scope, record type, and act are all permitted inbound by that agreement; `payloadSha256` matches the actual record bytes; `prevEntrySha256` continues the sender's chain with no gap; `idempotencyKey` has not been seen (replays collapse silently rather than duplicating); no denied key appears in the payload. Any failure quarantines with a named failure class and emits a signed `rejected` receipt.

**Admission is not adoption.** An admitted bundle lands in `Boundary/In/Quarantine/`, which is inside the brain's folder and outside the brain's knowledge. A human, or a Curator identity drafting for a human, then makes a **routing decision**, which is an ordinary internal record with a provenance pointer back to the utterance. Nothing is auto-filed. This is your decision `0018` logic inverted, and it is the single rule that keeps a peer from writing into your mind.

### 5.3 State machines

Sender, reusing your existing 11-state vocabulary where it fits:

```
drafted -> export_blocked            (check failed, terminal until fixed)
drafted -> approved -> emitted -> delivered -> acknowledged -> reconciled
                                          \-> retryable -> delivered
                                          \-> rejected (terminal, with failure class)
                                          \-> uncertain -> recovered
any     -> superseded                (a revise utterance supersedes by id, never mutates)
```

Receiver:

```
received -> verified -> admitted -> routed -> adopted
        \-> quarantined -> (rejected | admitted after author override, logged)
```

Two rules carried straight over from your outbox, because you already got them right. First, **an ack is not a confirmation**: `reconciled` requires a valid signed receipt whose `payloadSha256` equals the local canonical payload, which is your `record_authoritative_readback` pattern expressed symmetrically. Second, **nothing is ever mutated**: a correction is a `revise` utterance with `supersedes`, and a withdrawal is a `retract` utterance that produces a tombstone. The receiving brain decides what a tombstone means for its own copy, per the agreement's `retention` block, because it owns its copy.

### 5.4 Where the ledgers live

Asymmetric on purpose, because the two brains have asymmetric relationships to each other.

Your brain, boundary mounted **inside the domain**, since the domain is your name for the counterparty:

```
brain/d7r/Boundary/
  Peer.md                          peer record: brainId, keys, tier, agreement pointer
  Agreement/agr-spencer-d7r-v1.yaml
  Out/
    ledger.jsonl                   append-only, hash-chained: one entry per utterance
    bundles/20260825T110000Z-<hex>.brainpack
    receipts/<utteranceId>.json    countersigned receipts received back
  In/
    ledger.jsonl                   append-only, hash-chained: one entry per admission
    Quarantine/<utteranceId>/      admitted, not yet adopted
```

The org brain, boundary mounted **per contributor**, since a contributor is its name for the counterparty:

```
brain/System/Boundary/
  Peers/spencer-thornock.md        contributor record, contribution ledger pointer
  Agreements/agr-spencer-d7r-v1.yaml
  spencer-thornock/
    In/  ledger.jsonl  Quarantine/
    Out/ ledger.jsonl  bundles/  receipts/
```

Ledger entries are minted the way your logs already are, with `automation/newlog.py`'s discipline: never compute a sequence number, use timestamp plus entropy. The distributed review's R3 race, where two hosts both saw max `087` and both wrote `087`, is exactly the failure a coordination-free name prevents.

### 5.5 Transport binding: git as the reference wire

The bundle is normative. Git is the first conformant transport, and the reason is the finding from your own architecture review: a non-forced push is a server-side compare-and-swap, so a Forgejo ref is a linearizable serializer you already run on Tailscale with no new failure domain.

```
Transfer repo (Forgejo), one per peer pair:
  refs/speak/v1/out/<listener-handle>/<utteranceId>    bundle + envelope, created by sender
  refs/speak/v1/ack/<speaker-handle>/<utteranceId>     signed receipt, created by receiver
  refs/speak/v1/head/<speaker-handle>                  sender's chain head, fast-forward only
```

Ref creation fails if the ref exists, which gives idempotent delivery for free. The `head` ref is fast-forward only, which makes the sender's hash chain globally monotone and detects a rewritten ledger at push time rather than at audit time. A brain that cannot reach the transfer remote refuses to emit, and refuses to mark anything delivered, rather than falling back to local state.

What git must **not** carry: the brains themselves. Two brains do not share a repo, do not share a working tree, and do not merge. The transfer repo holds bundles and receipts only, and either side can prune it after reconciliation because both sides keep their own append-only ledger. This is how the spec enforces your boundary requirement structurally rather than by discipline.

Obsidian Sync stays exactly where the architecture review put it: advisory watermark, never authority. No lease, no claim, and no chain head in `brain/`.

### 5.6 The non-goals, stated as normative prohibitions

Your boundary requirements deserve to be MUST NOTs in the document, because they are the parts a well-meaning implementer will get wrong.

- A brain MUST NOT hold a full copy of a peer brain. It holds only records it admitted, plus its own knowledge about that peer.
- An utterance transfers a **copy**. On admission the receiver becomes the owner of its copy, and the two copies legitimately diverge. There is no shared mutable state, no sync, and no mirroring between brains. (Contrast your decision `0010`, where a repo mirror *is* owned upstream and hand-edits register as drift. Brain to brain is deliberately not that.)
- No inbound utterance may set a gate, change a `visibility`, change a `sensitivity`, alter decision text, or write into a note body. This is your `External Connections.md` rule verbatim, and it is the right rule: "No external event can change a gate, decision text, sensitivity, visibility, identity, hierarchy, or note body."
- No agent identity may approve an export. Human plus script, same as publication.
- `peer-confidential` MUST NOT be re-exported onward, in any act, to any third brain.
- A `retract` MUST NOT be implemented as a delete on the receiving side. It produces a tombstone, and the receiver's retention policy governs the rest.

---

## 6. The setup workflow, twelve phases

This is the process an individual or an existing business runs to stand up a Blueprint brain, from an empty folder to a federated one. Each phase has an entry condition, a small number of artifacts, and one gate. It is deliberately twelve phases, because your three courses already share a twelve-theme arc and the mapping is close to free.

| Phase | Name | Produces | Gate to exit | Tier |
|---|---|---|---|---|
| 0 | **Declare** | Charter, keypair, `brainId`, lineage, license, tier claim | Author signs the Charter | 1 |
| 1 | **Constitute** | The one governing file, precedence rules, prime directives, path anchors, decision `0001` | Constitution adopted as a decision record | 1 |
| 2 | **Scaffold** | Topology, first domain manifest, shared entity layer, home dashboard | Scaffold self-test passes | 1 |
| 3 | **Schema** | Controlled vocabularies, templates, id and filename rules, derived-state list | Schema check passes on a seeded note | 1 |
| 4 | **Capture** | Intake flows, source preservation rule, stages 0 to 3, routing vocabulary | First source preserved with `gate_source_preservation` | 1 |
| 5 | **Develop** | Works pipeline, stages 4 to 10, task tree, critical thinking at stage 4 | First work reaches stage 6 with belief gate approved | 2 |
| 6 | **Classify** | Sensitivity, visibility, consent, publication guard script | Publication check exits 0 on one work, non-zero on a seeded violation | 2 |
| 7 | **Ledger** | Log families, minting discipline, decision records, hash chaining on boundary logs | Two concurrent minting attempts collide zero times | 2 |
| 8 | **Agency** | Agent identities and charters, authorities, enforcement hook, authorship policy | Guard blocks a deliberate forbidden write | 2 |
| 9 | **Boundary** | Peer record, agreement, keys, export and admission checks, Out and In ledgers | One round trip completes: emit, admit, receipt, reconcile | 3 |
| 10 | **Operate** | Host roles, schedulers, CI, conformance self-test, invariant health check | Full self-test green on two hosts, single-owner state proven | 3 |
| 11 | **Federate** | Second peer, key rotation drill, revocation drill, cross-brain audit | Rotation and revocation both exercised without data loss | 3 |

### Two entry tracks

**Individual, greenfield.** Runs 0 through 11 in order. Phase 2 creates one domain. Phase 4 is where most of the early value lands, and most people should sit at Tier 1 for a while before touching gates.

**Existing business, brownfield.** Two changes, and they are the ones that go wrong in practice.

First, at Phase 2 all existing material is imported **as sources, never as works**. Your decision `0014` already says migration is copy-only and sources are never deleted or modified, and `0016` says nothing past stage 3 lives in a source folder. A business with ten years of Drive documents has ten years of *sources*, and treating them as finished works is the failure mode that produces an unusable brain. An imported finished work keeps its published structure and is marked as such; everything else enters at stage 0.

Second, Phase 9 arrives earlier and matters more, because a business has contributors from day one. A business brain is an org brain, so it should scaffold `System/Boundary/Peers/` at Phase 2 even though it will not use it until Phase 9, and its Charter should claim Tier 3 as a target from the start.

### The gate that decides whether this works

Phase 6 and Phase 9 are the only two phases where a script must exit non-zero and stop the line. Everything else can be soft. Insight 10 says the rest will rot unless it is checked, so the conformance self-test at Phase 10 is not optional polish: it is the mechanism by which a brain notices it has decayed. It should be the thing a peer can run against you before agreeing to exchange.

---

## 7. First milestone: your brain to the D7R org brain

Concrete, in order, with the risks named.

**M1. Charter your own brain.** `brainId: brain:spencer-thornock`, Ed25519 keypair in the Mac keychain, public key and `keyId` in the Charter, lineage entry recording the Epic to D7R derivation. Nothing else changes. This is a day of work and it is the prerequisite for everything.

**M2. Mount the boundary in your d7r domain.** `brain/d7r/Boundary/` with empty `Out/ledger.jsonl` and `In/ledger.jsonl`, a `Peer.md` for `brain:d7r`, and the export check wired into `scripts/ci.sh` alongside `publication-check.py`. Still no peer, so nothing can be emitted, which is the correct fail-closed state.

**M3. Stand up the D7R org brain.** On the dedicated machine, at `/Users/d7r/code/obsidian`, a Tier 1 brain scaffolded clean-room from the Blueprint template, not copied from yours. Its own Charter, its own keypair, its own constitution, `System/Boundary/Peers/spencer-thornock.md`. Per decision `0050` this must be built from the spec, and building it is also the first real test of whether the spec is complete.

**M4. Sign the agreement.** One `agr:spencer-d7r/v1`, both signatures, both copies. Start deliberately narrow: outbound scope `d7r/**`, classifications `brain-portable` and `peer-internal` only, acts `assert` and `revise` only, `retract` deferred. A narrow first agreement is easier to widen than to unwind.

**M5. One round trip, by hand.** Pick one record. Approve `gate_export_approval`. Run the export check. Emit a bundle. Copy it by hand, not by git. Run the admission check on the org side. Emit a receipt. Reconcile. Read both ledgers and confirm the chains link. Doing this manually once, before any automation, is what surfaces the schema mistakes.

**M6. Bind the git transport.** A transfer repo on Forgejo, `refs/speak/v1/**`, ref-creation-as-CAS, fail closed when unreachable. Only now automate.

**M7. Rotation and revocation drill.** Rotate `k1` with an overlap window and confirm old utterances still verify against the retired key while new ones require the new one. Then revoke and confirm the org brain refuses a bundle signed with the revoked key. Untested key rotation is not key management.

### Risks specific to your setup

The dedicated machine for the D7R brain is the right call, and the architecture review explains why better than I can: role partitioning removes whole classes of race rather than coordinating them. But three of its findings apply directly here.

Do not let the two brains share an Obsidian Sync vault, ever. Sync merges Markdown with diff-match-patch silently, and two brains converging on one file is the R1 race with a legal boundary running through it.

Do not put the chain head, the agreement, or any lease in a Sync'd folder. Refs carry authority. Sync carries the watermark.

Fix `write_vault_note` before the org brain goes live. The fixed `p + ".tmp"` name inside the Sync target (`vaultlib.py:232`) is R2, and an admission pipeline writing into quarantine with no compare-and-swap precondition is the same bug with a peer's data in it.

---

## 8. What I recommend you decide next

Six decisions, in dependency order. Each is small, and each unblocks a lot.

1. **Name.** `SPEAK` with utterance vocabulary, or `BXP` plain. This propagates into every identifier, so it is worth five minutes now.
2. ~~Spec repo layout.~~ **Resolved 2026-08-25.** The repository is `<repo>/blueprint`, sibling to `saga-standard`, `derp-spec`, and `agent-rights` under one source root. The specification name is `Blueprint`, matching the bare-name style of the siblings rather than carrying an organization prefix. Schema identifiers and the published site anchor on `blueprint-spec.dev`, by analogy with `derp-spec.dev`. Change the domain now if it is wrong, because it is embedded in every schema `$id`.
3. **One document or two.** Blueprint plus SPEAK as siblings, which is my recommendation and mirrors SAGA plus DERP, or one combined document.
4. **Signature algorithm.** Ed25519 detached signatures with an in-Charter keyring, which is my recommendation, or SAGA wallet signatures for continuity with the existing stack. Ed25519 is simpler and has no chain dependency. Wallet signing gets you SAGA identity reuse for free. You can also do both, with Ed25519 normative and wallet as an alternative `alg`.
5. **Tier claim for the org brain.** Tier 1 first and grow, or Tier 3 target from day one. Brownfield orgs usually need the latter.
6. **Whether `retract` is in v1.** Retraction has real semantics for the receiver's retention policy and it is the field most likely to be got wrong. Deferring it to v1.1 is defensible.

---

## Sources

All primary sources are local files on the author's machine, read 2026-08-25.

- `~/code/obsidian/brain/AGENTS.md` (canonical vault contract, 62,430 bytes)
- `~/code/obsidian/brain/System/Decisions/` (57 decision records; `0003`, `0004`, `0005`, `0007`, `0010`, `0014`, `0016`, `0017`, `0018`, `0019`, `0020`, `0022`, `0027`, `0028`, `0029`, `0030`, `0036`, `0038`, `0039`, `0047`, `0050`, `0052` cited)
- `~/code/obsidian/brain/System/Automation/External Connections.md`
- `~/code/obsidian/automation/flowstate_bridge_contract.py` (695 lines; envelope contract, 14-step preflight, 21 failure classes)
- `~/code/obsidian/automation/flowstate_outbox_contract.py` (2,518 lines; SQLite WAL append-only outbox, 11-state machine, leases and fencing, readback reconciliation)
- `~/code/obsidian/scripts/publication-check.py`, `scripts/check-gates.py`, `scripts/ci.sh`, `automation/guard.py`, `automation/newlog.py`, `automation/vaultlib.py`
- `~/code/obsidian/audit/2026-08-23-distributed/architecture-review.md` (transports, coordination gap, ranked races R1 to R7, phased plan P0 to P9, invariants)
- `~/code/epic/saga-standard/spec/SAGA-v1.0.md` (envelope 3.1, identity Layer 1, transfer protocol 13, data classification 13.5, redaction manifest 13.5.4, cryptographic verification 16, conformance 17, `.saga` format Appendix C)
- `~/code/epic/derp-spec/spec/DERP-v1.0.md` (three-spec stack 1.1, conformance tiers 4, manifest 10)
- `~/code/epic/agent-rights/spec/BILL_OF_RIGHTS-v1.0.md` (Rights I to X across Identity, Labor, Dignity tiers)
- `~/code/obsidian/brain/d7r/Outputs/Courses/D7R-{1,2,3}` (twelve-theme arc, 35 of 36 modules still outlines)
