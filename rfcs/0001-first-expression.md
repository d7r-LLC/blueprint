# RFC 0001: The first expression: chain of command routing, delegated hiring, agent approval by grant, budgeted spend, and SAGA canonical signing

**Status:** Draft
**Specification:** BLUEPRINT/1.0, DEFER/1.0, TRACE/1.0, SPEAK/1.0, SAGA/1.0
**Change class:** MAJOR
**Author:** drafted by an agent for Spencer Thornock; the listed authors decide
**Opened:** 2026-09-30
**Comment period ends:** 2026-10-30

## Summary

d7r.io is the first instance built against this stack. Building it found five clauses that make a normal company impossible to run under the specification and three places where the text and the schemas disagree. This RFC proposes revisions that keep each invariant the clause protects and remove the part that blocks the first expression. It also adds the two schemas BLUEPRINT names but does not ship.

## Motivation

Observed while designing the d7r.io workspace authority model on 2026-09-30:

1. DEFER 3.2 forbids resolving an approver by ascending `reports_to`, and 9.1 routes to the least authorized covering holder. A company that operates by chain of command asks the immediate supervisor. Both want the same guarantee: the approver's envelope covers the act.
2. DEFER 4.6 and 5.2 reserve every nonzero `authority-delta` to the owner, while 8.3 permits redelegation. A CEO cannot hire a seat without the owner, and the two sections disagree.
3. BLUEPRINT 12.2 and TRACE 4.1 forbid an agent identity from approving a gate, while DEFER 9.3 lets an agent resolve a decision the owner decided in advance by grant. The two cannot both hold.
4. DEFER 6.2 forbids resolving a K3 act automatically on magnitude alone, and the envelope's `boundaries` enum has no payment rail, so an agent cannot buy inside a budget the owner set.
5. SAGA 15.1 requires signing over the RFC 8785 canonical document, while the schema's `signature.message` and the reference SDK sign only `SAGA export <documentId> at <exportedAt>`. A verifier cannot check a document body, and the specification ships no verifier.
6. SAGA has no identity model for a human principal, although its purpose statement covers human and AI agents.
7. The SPEAK receipt schema allows a `quarantined` verdict that SPEAK 1.5 does not define, and the peer agreement schema has no field for the alignment declaration POLARIS 12.2 requires.
8. BLUEPRINT names a `record` schema and a `source-provenance` schema that do not exist.

## Specification

### DEFER 3.2 and 9.1: chain of command as a declared routing rule

A Charter MAY declare `routing: chain-of-command`. Under this rule the brain MUST, before any decision is routed, verify that for every role the envelope set of its `reportsTo` role strictly covers the role's own envelope set, and MUST refuse to route while that proof fails. Under this rule a decision MUST be routed to the requesting role's `reportsTo` role, and the decision record MUST carry `selectionRule: chain-of-command` and the digest of the coverage proof. The least authorized holder rule of 9.1 is satisfied by construction, because ascending the supervisor relation ascends coverage. The prohibition in 3.2 is retained for brains that do not declare the rule.

### DEFER 4.6, 5.2 and 6.3: delegated hiring inside the delegator's envelope

`authority-delta` counts widenings beyond the delegator's own envelope. A grant creation or redelegation whose envelope is a strict subset of the delegator's envelope, issued under a parent grant with `redelegation: true`, reads zero on `authority-delta`, is classified K3, and MAY be delegated. A widening beyond the chain root's envelope reads nonzero and remains K4, owner only.

### BLUEPRINT 12.2 and TRACE 4.1: agent approval by grant

Replace "A Governed brain MUST NOT permit an agent identity to approve a gate" with: "A Governed brain MUST NOT permit an agent identity to approve a gate except under a signed delegation grant whose envelope covers the gate's consequence class. An agent identity MUST NOT approve a K4 act. The decision record MUST name the grant." TRACE 4.1 is amended to match.

### DEFER 6.2 and the envelope schema: budgeted spend

Add `payment-rail` to the `boundaries` enum of `authority-envelope.schema.json`, with a `rail` string naming the rail. A spend whose per-act magnitude and windowed per-chain aggregate are both inside a signed grant that names the rail is a decision the owner decided in advance under 9.3, and MAY be resolved by the grant holder. 6.2 is unchanged: magnitude alone still resolves nothing.

### DEFER 3.3: the role set inside a governed record

A machine-readable role set held inside a governed record, whose rendered chart carries the digest of that role set, is the role set and not a hand-maintained chart file. No change to the invariant.

### BLUEPRINT 5.3: templates and minted identifiers

A template is not a brain and its issued assets are not records. A record created by copying an issued asset into a brain MUST mint its identifier at the copy, per 5.3. The issued asset MAY carry a stable slug in a separate field.

### SAGA 15.1: canonical signing and a required verifier

`signature.message` MUST be the RFC 8785 canonical serialization of the document with the `signature` member removed, or its SHA-256 digest prefixed `saga-canonical-sha256:`. A Level 1 implementation MUST ship a verifier that canonicalizes, verifies the signature against `walletAddress` or a registered Ed25519 key, and confirms the signer matches the identity layer. The two-field message form is retired.

### SAGA: human principals

An identity document with `persona.profileType: human` is valid at Level 1. It carries the same envelope, is signed by the person's wallet or an Ed25519 key registered in a compatible directory, and MAY be referenced as a `principal` by agent documents.

### SPEAK schemas

Remove `quarantined` from the receipt verdict enum. Add `alignmentDeclaration` to `peer-agreement.schema.json` as a required object carrying the signed POLARIS declaration reference of each party.

### New schemas

Add `schema/v1/record.schema.json` (required `type`, `id`, `created`, `authorship`; optional `sensitivity`, `visibility`, custody floor and gate properties) and `schema/v1/source-provenance.schema.json` per BLUEPRINT Appendix A.

## Failure mode

A brain declaring `chain-of-command` whose coverage proof fails MUST refuse to route any decision and MUST record the failing pair. A redelegation that is not a strict subset MUST be refused as K4. An agent approval without a named covering grant MUST be recorded as invalid and the gate MUST remain closed. A spend outside the per-act or per-chain ceiling MUST be refused before execution. A SAGA document whose signature does not verify over the canonical form MUST be rejected by a Level 1 implementation.

## Conformance impact

Tier 2 and Tier 3 are affected. An existing implementation that routes by least authorized holder remains conformant; the chain rule is opt-in. An implementation that let agents approve gates without a grant was never conformant. SAGA Level 1 implementations that sign the two-field message cease to be conformant and must re-sign.

## Schema impact

`authority-envelope.schema.json` (new boundary value), `decision-record.schema.json` (`selectionRule`, `coverageProofDigest`), `receipt.schema.json` (enum), `peer-agreement.schema.json` (new required field), `brain-charter.schema.json` (`routing`), two new schemas, and SAGA `saga.schema.json` (`signature.message` pattern). `contractVersion` strings move to the next minor where a field is added and to the next major for the receipt enum removal.

## Alternatives considered

- Keep least-authorized routing and model the supervisor chain only as Informed. Rejected: it does not describe how the company decides, and the first expression would carry two routing models.
- Keep grant creation K4 and pre-authorize seats in bulk. Rejected: it moves the owner's decision into a larger, earlier one and defeats delegation.
- Keep the SAGA two-field message and add a separate body digest. Rejected: two signatures where one suffices.

## Unresolved questions

- Whether `chain-of-command` should be declared per brain or per role set.
- Whether an Ed25519 key registered in a directory is sufficient for a human SAGA identity, or a wallet is required.
- Whether the `record` schema belongs in BLUEPRINT or in a separate profile.
