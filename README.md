# Blueprint

**An open specification for owned, governed, exchangeable knowledge.**

A brain is a locally owned, policy governed, append only audited folder of plain text. Blueprint specifies the structure and governance of one brain. POLARIS specifies what the brain is for and what it refuses to do. DEFER specifies who may decide, bounded by what. SPEAK specifies how knowledge moves between brains without merging them. CONFIDE specifies how brain content may be processed by a language model without leaving the owner's control. TRACE specifies how the artifacts that agent tooling leaves behind become governed evidence instead of an ungoverned copy of the brain. RETAIN specifies whose brain an agent has, and what an agent that learns is allowed to keep.

**Status:** Draft. Nothing in this repository is adopted until it lands as a decision record.

## The stack

Blueprint is the fourth member of a four specification stack.

| Spec | Repository | Site | Answers |
|---|---|---|---|
| Agent Bill of Rights | `<repo>/agent-rights` | agent-rights.org | What agents deserve |
| DERP | `<repo>/derp-spec` | derp-spec.dev | What the runtime must provide |
| SAGA | `<repo>/saga-standard` | saga-standard.dev | How an agent is represented |
| **Blueprint** | `<repo>/blueprint` | blueprint-spec.dev | How knowledge is held, governed, and exchanged |

SAGA moves an agent. Blueprint moves a thought.

## Seven documents

- `spec/BLUEPRINT-v1.0.md` defines a single brain, in ten layers.
- `spec/POLARIS-v1.0.md` defines purpose and alignment: what the brain exists for, and the refusals, obligations, loyalties, and standards that narrow every act.
- `spec/DEFER-v1.0.md` defines delegated authority: consequence classes, authority envelopes, signed grants, routing, escalation, and decision records.
- `spec/SPEAK-v1.0.md` defines brain to brain exchange: signed, classified, reconciled, auditable.
- `spec/CONFIDE-v1.0.md` defines inference governance: which providers may see which records, under what evidence, logged to a hash chained ledger.
- `spec/TRACE-v1.0.md` defines tooling residue: harness registration, artifact classes, session anchors, sealing, and retention of protected artifacts.
- `spec/RETAIN-v1.0.md` defines agent brains: when accumulated agent state is residue, when it is a domain you own, and when it is a brain someone else owns, plus admission, mandates, coordination, and what an agent keeps when the engagement ends.

One brain, three boundaries, one authority model, one reason. Knowledge crosses to another brain under SPEAK, to a model under CONFIDE, and into the tooling under TRACE. The third is the crossing that happens on every operation and is the one nobody declared. Every crossing is an act, DEFER says who may authorize it, and POLARIS says whether the brain will do it at all.

Precedence is asymmetric and the asymmetry is the point. POLARIS holds the highest precedence to **forbid** an act and no precedence to **permit** one. Purpose may narrow what a brain will do. It may never widen it, satisfy another document's check, or excuse a failure.

There are no sub-brains. Containment and boundary are mutually exclusive, so a brain cannot sit inside another brain: if you can read it at will the agent has a folder, and if you cannot then it is not inside you. Whoever holds the signing key owns the refusal, and a brain you can sign for is a folder with aspirations. What looks like a hierarchy of brains is a set of peers under asymmetric agreements plus an authority graph that DEFER already governs.

## The ten layers

| # | Layer | Owns |
|---|---|---|
| 0 | Charter | Brain identity, ownership, legal entity, keys, lineage, license, purpose and refusals |
| 1 | Constitution | The one governing file, precedence, prime directives, path anchors |
| 2 | Topology | Folder taxonomy, domains, manifests, shared entity layer, artifact roots |
| 3 | Records | Frontmatter contract, controlled vocabularies, ids, filenames |
| 4 | Lifecycle | Sources versus works, stages, gates, change authority |
| 5 | Classification | Sensitivity, visibility, consent, publication guard, custody matrix |
| 6 | Ledger | Append only logs, sequencing, hash chaining, decision records, session anchors |
| 7 | Agency | Agent identities, roles, authority envelopes, delegation grants, enforcement, authorship policy |
| 8 | Boundary | Three flows in, out, and inference. Peers, agreements, utterances, receipts |
| 9 | Operations | Automation, host roles, verification, conformance self test |

## Conformance tiers

- **Tier 1, Sovereign.** Owned, structured, logged. Plain text is the source of truth. No exchange. Every inference call catalogued, every agent harness registered, one purpose statement and one enforceable refusal declared, every act classified and recorded before execution.
- **Tier 2, Governed.** Hash bound gates, enforced classification, agents draft and never approve, all inference through one broker that holds the only credentials, every session anchored and its evidence sealed, authority conferred only by signed grant with a human root, refusals evaluated at every crossing and tested on an interval. Safe to publish from.
- **Tier 3, Federated.** Signed bidirectional exchange, reconciliation, admission gate, key rotation and revocation, custody floors declared and enforced, refusal floors that travel with the record, no grant chain crossing a brain boundary. Required to participate in SPEAK.

## The custody ladder

Every inference endpoint is classified by custody, which answers one question: at the moment of inference, who holds the bytes.

| Class | Term | Hardware | Model operator |
|---|---|---|---|
| C0 | Resident | Owner owns and physically holds | Owner |
| C1 | Enclave | Owner controls, does not physically hold | Owner |
| C2 | Tenant | Vendor owns, owner controls the stack | Owner |
| C3 | Broker | Vendor owns | Vendor, under contract |
| C4 | Open | Vendor owns | Vendor, default terms |

A class describes an endpoint under a contract, never a company. Chains take the weakest class. An undeclared retention posture is C4.

## Artifact classes

Everything an agent harness leaves behind is one of six things, and each needs different handling.

| Class | Term | Examples | Rule |
|---|---|---|---|
| A0 | Directive | agent definitions, skills, rules, permission grants | authority: inside the brain, versioned, gated |
| A1 | Session | transcripts, prompt history, tool logs | evidence: anchored, sealed, protected |
| A2 | Derived | harness memory, embeddings, goal state | adopt into the brain or expire |
| A3 | Copy | file snapshots, attachments, worktrees | inherits classification, expires |
| A4 | Credential | tokens, OAuth caches, shell snapshots | excluded by construction, never sealed |
| A5 | Telemetry | usage counters, crash reports, install ids | egress: declared or disabled |

A0, A1, and A3 are protected artifacts. Deleting one is a recorded act, and an agent may not do it.

## Consequence classes

Authority routes on the consequence of an act, never on the seniority of the actor. A class is assigned by the worst true statement about the act, not the typical case.

| Class | Term | Meaning | Delegable |
|---|---|---|---|
| K0 | Reversible local | Undone by an author with no residue | Yes, freely |
| K1 | Reversible costly | Undone, but the reversal is itself work | Yes, bounded |
| K2 | Irreversible internal | Cannot be undone, stays inside the brain | Yes, narrowly |
| K3 | Irreversible external | Crosses a boundary, cannot be recalled | Yes, very narrowly |
| K4 | Constitutional | Changes the rules or who may change them | Owner only |

Any SPEAK, CONFIDE, or TRACE boundary crossing is at minimum K3, which is where the boundary documents and the authority document meet. Narrowing an envelope or revoking a grant is K2 and delegable, because a governance system should be easy to tighten and slow to loosen.

Authority is a bounded envelope on four axes, never a rank: act class, scope, magnitude, and conditions. A missing axis is malformed, not unbounded. Every chain of grants terminates in a human signature, each redelegation is a strict subset of the grant above it, a decision routes to the least authorized covering holder rather than the most senior, and a timeout may resolve as denied, as a pre authorized safe act, or as a red health check, but never as approved.

Urgency decides what happens while a decision waits. It never decides who may make it.

## What Blueprint is not

It is not an implementation. It requires only a device, a folder, and a text format. Obsidian is one editor that works. So is any other.

It is not a sync system. Two brains never share a repository, a working tree, or a mutable state root. Knowledge crosses the boundary as a copy, and the two copies legitimately diverge.

## Repository layout

```
spec/        normative specifications
schema/v1/   JSON Schema for charters, agreements, utterances, receipts,
             inference providers, authorizations, call records,
             harnesses, session anchors, artifact ledger entries,
             roles, authority envelopes, delegation grants,
             decision requests, decision records, purpose declarations,
             agent state stores, mandates
profiles/    starting configurations for individual and organization brains
design/      design notes and rationale, non normative
rfcs/        change proposals
docs/        published site
```

## License

Apache 2.0. See `LICENSE`.
