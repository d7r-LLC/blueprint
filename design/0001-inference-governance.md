# Inference Governance: Design Note

Non normative working note. Records rationale, alternatives, and open decisions for CONFIDE/1.0.
Prepared: 2026-08-25.

---

## 1. The question

Language model inference is necessary to operate a brain at any useful scale. It is also the single highest volume path by which brain content leaves the owner's custody. A brain can have flawless publication gates, signed peer exchange, and hash chained ledgers, and still leak everything, because an agent summarized a folder against a consumer API endpoint on a Tuesday and nobody recorded it.

So the requirement is not "restrict inference." It is: **every crossing is catalogued, bounded by policy the owner signed, enforced mechanically, and answerable after the fact.**

## 2. The central reframe

Inference is a boundary crossing. It belongs in Layer 8, not in an appendix.

Blueprint already had two flows. Output, where knowledge leaves for a peer or the public. Input, where external material arrives. Inference is the third, and it is a round trip: content crosses out and derived content crosses back in one operation.

Treating it as a boundary crossing rather than as an integration detail buys the whole existing vocabulary. There is already a guard concept, a ledger concept, a classification matrix, an agreement concept, a receipt concept, and a hash chain. Inference needs all six, and reusing them means one mental model instead of two.

The four ways inference differs from the other two flows, which is where the new machinery is needed:

| | Peer exchange | Inference |
|---|---|---|
| Counterparty | A brain. Runs its own admission check, signs a receipt, keeps a reconcilable ledger. | Not a brain. Verifies nothing, signs nothing, reconciles nothing. |
| Retention | Governed by a mutual agreement both sides can audit. | Happens on infrastructure outside audit reach. The owner holds evidence of a promise, never proof of deletion. |
| Return content | Authored by a person, attributable. | Derived by a machine, requires provenance rather than attribution. |
| Frequency | Weekly. | Hundreds of times a day. |

That last row governs the whole design. **A control that requires the owner to think before each call will be bypassed inside a week.** So the decision has to sit at the level of the provider and the authorization, which are reviewed rarely, and the per call check has to be mechanical and invisible.

## 3. Why this is not a new layer

The obvious move is Layer 10, Cognition. I decided against it, for one reason: a control that lives in its own layer can be omitted while still claiming conformance to the others. A brain could implement Layers 0 through 9 faithfully, skip Layer 10, and describe itself as governed.

Instead the enforcement is threaded into six existing layers, so that skipping it breaks conformance to layers the brain already claims.

| Layer | What it now carries |
|---|---|
| 0 Charter | Declares whether the brain operates a broker, its default maximum custody class, and where the registry and call ledger live. |
| 3 Records | `derivedVia` provenance on generated content. `custodyFloor` as a record property. |
| 5 Classification | The custody matrix. Consent to process as distinct from consent to record. |
| 7 Agency | An agent charter MUST name its inference authorization. Agents MUST NOT hold provider credentials. |
| 8 Boundary | The third flow, the third guard. |
| 9 Operations | The broker as a required component. Egress invariants. Evidence expiry sweep. |

The catalog format, the authorization format, the call record format, and the failure class registry are third party facing and will version on their own schedule, so those get a separate document: **CONFIDE/1.0**. The name is a bare word matching Blueprint rather than a forced acronym, and it says the right thing: you confide brain content to an outside mind, under terms, with an expectation of discretion. Alternative if it reads too soft: `IGP/1.0`, Inference Governance Protocol.

## 4. The custody ladder

You asked for local terms to classify providers. The classification axis is **custody**, not vendor, and it answers exactly one question: at the moment of inference, who physically holds the bytes, and who is in a position to retain them.

| Class | Term | Hardware | Model operator | Example |
|---|---|---|---|---|
| C0 | **Resident** | Owner owns and physically holds | Owner | Quantized model on your MacBook Pro |
| C1 | **Enclave** | Owner controls, does not physically hold | Owner | Colocated box, owner holds disk keys |
| C2 | **Tenant** | Vendor owns, owner controls the stack | Owner | GPU virtual machine running open weights |
| C3 | **Broker** | Vendor owns | Vendor, under contract | Enterprise or zero retention API tier |
| C4 | **Open** | Vendor owns | Vendor, default terms | Consumer tier, free key, unclear retention |

Short nouns on purpose, so they survive being spoken. "Confidential never leaves resident." "That vector store is a tenant surface, at best."

Four rules make the ladder hold up under contact with reality.

**A provider record describes an endpoint and a contract, never a company.** The same vendor is C3 on one endpoint and C4 on another. The difference between C3 and C4 is documentary, not technical.

**Weakest link.** Where a provider routes, subcontracts, or falls back, the effective class is the numerically highest class in the chain. A routing service is C4 unless the authorization pins a downstream provider and the response is verifiable against the pin.

**Unknown is not a class, it is C4.** An omitted retention field must never widen what a provider may receive. This closes the most common failure, which is a half filled registry entry read charitably.

**The ladder is an incentive gradient.** C0 is permissive at every sensitivity, because C0 produces no egress of record content at all. That is the reward for owning the machine. You said you ideally want dedicated inference infrastructure; the matrix should make that the path of least resistance rather than a virtue you have to remember.

## 5. The matrix

| Record sensitivity | C0 Resident | C1 Enclave | C2 Tenant | C3 Broker | C4 Open |
|---|---|---|---|---|---|
| `none`, public | allow | allow | allow | allow | allow |
| `none`, private or internal | allow | allow | allow | allow with unexpired evidence | prohibit |
| `personal` | allow | allow | allow with unexpired evidence | per record approval | prohibit |
| `third-party` | allow with processing consent | allow with processing consent | consent and evidence | prohibit | prohibit |
| `confidential` | allow | per record approval | prohibit | prohibit | prohibit |

Cells may be lowered freely and raised only by a signed owner decision naming the cell, the provider, the justification, and a review date. `confidential` may never be raised above C1. A lowered cell cannot be raised again by an agent or by configuration inheritance.

## 6. How this is actually enforced

Policy that an agent can ignore is not a control. Three mechanisms, in descending order of how much work they do.

**Credential isolation is the real enforcement.** Provider credentials live only in the broker, never in the brain folder, never readable by an agent process. An agent that decides to ignore the policy has no key with which to act on that decision. This is the single most important requirement in CONFIDE, and everything else is bookkeeping on top of it.

**One chokepoint.** All inference goes through one broker that runs the check, writes the ledger entry, and is the only component that contacts a provider. This mirrors your existing rule that classification is enforced at exactly one boundary. Two enforcement points are equivalent to none, because they diverge.

**Detectability as the backstop.** Network egress from a brain host to an endpoint not in the provider registry is a health invariant. If someone finds a side channel, the invariant goes red rather than the leak going unnoticed.

And the broker fails closed. A broker that cannot read the registry, cannot validate an authorization, cannot determine a record's sensitivity, or cannot reach its own ledger refuses the call. A refusal is always recorded, because an unrecorded refusal is indistinguishable from a call that never happened.

## 7. Four controls that are easy to miss

These are the ones I would expect a careful implementation to get wrong.

**Evidence expires; beliefs do not.** A zero retention commitment is a document with a hash and a review date, not a memory. Every retention claim carries evidence with a mandatory `expiresAt`, and when the newest evidence expires the provider degrades automatically to `probationary` and may then receive only public material. This also satisfies the rule that no control may depend on the owner remembering to revisit it. A provider approved in March on the strength of a contract tier is not still approved in December by default.

**The ledger stores hashes, not prompts.** A ledger holding prompt text becomes the largest single concentration of sensitive content in the brain, is read far more often than the records it describes, and is precisely the surface an auditor gets access to. Recording the SHA-256 of the transmitted bytes plus the input record ids preserves provability, because the record bodies are in the brain and can be rehashed. Transcript retention is an explicit per authorization opt in, written to a separate surface with its own sensitivity, referenced from the ledger by hash only.

**Consent to record is not consent to process.** Layer 5 already requires third party consent before publication. Sending a record about a person to a model is a different act from writing it down, and it needs its own consent state. This is the requirement most likely to be inconvenient, and the one that most directly protects people who are described in a brain but do not own it.

**The agent loop is the real leak path.** If a model can invoke tools that read the brain, the check has to be evaluated against the union of everything read, and re evaluated before every turn. Checking once at the start of a loop that can widen its own scope is how a conformant looking implementation ships a `confidential` record to C4: turn one is clean, and turn six retrieves something the check never saw.

Two smaller ones worth naming. Embeddings are inference calls, inherit the sensitivity of the source, and a third party vector store is itself a provider that must be registered. And prompt caching extends retention, so a provider claiming `inputRetention: none` with caching enabled has an `unknown` posture, not a clean one.

## 8. Custody floors, and why they matter more than anything else here

This is the part that connects CONFIDE back to SPEAK, and it is the control I would fight hardest to keep.

When your brain sends a record to the D7R org brain, every careful control in your brain stops applying. D7R now holds a copy, and D7R decides where it gets processed. One unconstrained peer defeats your entire inference policy.

So a peer agreement declares, per direction, the weakest custody class at which transferred records may be processed, and whether inference use is permitted at all.

```yaml
directions:
  outbound:
    maxCustodyClass: C1
    inferenceUse: permitted
```

The floor is a property of the record, not of the inbox. It survives routing, adoption, editing, and derivation. A listener may strengthen it and may never weaken it, including by the obvious evasion of summarizing the record and treating the summary as unconstrained. Content derived from a floored record inherits the floor.

Processing above a floor is a boundary incident rather than a routine refusal: it lands in both ledgers, and the speaking brain is notified by an `acknowledge` utterance carrying the incident reference. The agreement should state the consequence in advance, and suspension should be available.

This is also the honest limit of the design, and it should be written down as such. A custody floor is enforceable by a conformant peer and unenforceable against a dishonest one. What it buys is not prevention. It is that the constraint was stated, signed, and recorded, so a violation is a breach of a specific term rather than a disagreement about expectations. That is the same guarantee a data processing agreement provides, and it is worth having for the same reason.

## 9. Where it lands in the tiers

Making this a priority means it cannot be optional at the tier where it matters.

**Tier 1 Sovereign.** Any brain that performs any inference maintains a registry and logs every call. Even a hobbyist. A brain that cannot say what it has sent, and where, is not a brain the owner controls.

**Tier 2 Governed.** Single broker, enforced matrix, credentials isolated from agents, every agent charter bound to an authorization, fail closed on expired evidence. You cannot claim Governed without this, which is the mechanism by which it stays a priority rather than becoming a backlog item.

**Tier 3 Federated.** Custody limits declared in every peer agreement, inbound floors enforced, violations reported.

Plus a self test requirement that I think is the highest value line in the document: a Tier 2 brain seeds a deliberate violation of each of the twelve check conditions and asserts the broker refuses with the expected failure class. **A control that has never been observed to refuse has not been demonstrated to work.** Your vault's own history is the argument for this: gates sat at 44 of 44 pending and a request queue sat at 6 in and 0 out, both of which were working exactly as written and doing nothing.

## 10. Open decisions

1. **Spec name.** `CONFIDE/1.0` as a bare word matching Blueprint, or plain `IGP/1.0`.
2. **Five classes or four.** C1 Enclave and C2 Tenant differ only in who owns the metal, and both are cases where the owner supplies the weights. Collapsing them to one class would simplify the matrix at the cost of losing the distinction between a colocated box you control and a cloud virtual machine you rent. I recommend keeping five, because the disk encryption key holder is a real difference.
3. **Whether C4 should exist at all in a registry.** The alternative is to make C4 unregisterable, so a brain simply cannot record a consumer tier provider. That is cleaner and less flexible. I kept C4 registerable so that public material can legitimately use cheap endpoints, and so that the ledger can record that it happened.
4. **Default for an unregistered call during migration.** Today's rule is fail closed immediately. For a brain retrofitting an existing setup, a bounded `observe` mode that logs and permits would ease adoption and would also be the exact hole an attacker wants. I lean toward no observe mode, and instead a short dated matrix override that expires.
5. **Whether the broker is normative or a pattern.** Requiring a broker component is a strong architectural constraint for a specification that otherwise only requires a folder and a text format. The weaker form is to require credential isolation and single point enforcement and let the shape be an implementation choice. I lean toward the weaker normative wording with the broker as the reference pattern.
6. **Processing consent granularity.** Per record, per person, or per purpose. Per person is the most useful and the hardest to represent, because it requires the shared entity layer to carry consent state that records then inherit.

## 11. Suggested next build steps

These extend the milestones in `0000-workflow-and-spec-design.md` and slot in before the first peer exchange, because it would be strange to sign a custody floor you cannot yet enforce.

1. Catalog what you are already using. One provider record per endpoint currently in play across the vault's automation, with honest `unknown` values wherever the posture is not documented. Expect this to be uncomfortable reading, and expect it to be the most valuable artifact in this whole effort.
2. Stand up a C0 Resident provider record for local inference on the M4 Max, with weight hashes. This is the one that makes the matrix generous rather than restrictive.
3. Write the broker as a thin process that holds keys and refuses. Ledger and check first, provider adapters second.
4. Write authorizations for the seven existing agent identities. Scout, Curator, Librarian, Groundskeeper, Skeptic, Editor, Auditor. Deliberately narrow, and expect several to need only C0.
5. Wire the twelve condition self test, seeded to fail, before wiring any real traffic.
6. Only then add the custody floor fields to the D7R agreement and proceed with the first exchange.

---

## Sources

Local files on the author's machine, read 2026-08-25, plus the specifications in this repository.

- `<repo>/blueprint/spec/BLUEPRINT-v1.0.md`, `spec/SPEAK-v1.0.md`, `spec/CONFIDE-v1.0.md`
- `<repo>/blueprint/design/0000-workflow-and-spec-design.md`
- `/Users/sthornock/code/obsidian/brain/AGENTS.md` (sensitivity and visibility vocabularies, the seven agent identities, the publication check, decisions `0005`, `0017`, `0018`, `0019`, `0027`, `0028`, `0037`, `0038`)
- `/Users/sthornock/code/obsidian/automation/flowstate_outbox_contract.py` (`PRIVACY_CLASSES`, `PRIVACY_DENY_KEYS`, the state machine and readback reconciliation reused here)
- `/Users/sthornock/code/obsidian/audit/2026-08-23-distributed/architecture-review.md` (fail closed when the serializer is unreachable; the evidence that unattended gates rot)
- `/Users/sthornock/code/d7r/src/saga-standard/spec/SAGA-v1.0.md` (data classification 13.5, redaction manifests 13.5.4, canonical JSON and signatures 16)
- `/Users/sthornock/code/d7r/src/agent-rights/spec/BILL_OF_RIGHTS-v1.0.md` (Right IX Transparency, which is the reason generated content carries its derivation rather than passing as authored)
