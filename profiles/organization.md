# Profile: Organization Brain

A starting configuration for a company, team, or other legal entity. Non normative.

## Charter defaults

```yaml
tier: 3
layers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
owner: { kind: organization }
```

An organization brain has contributors from the first day, so it claims Tier 3 as a target from the start even though it will not exercise Layer 8 until Phase 9.

## Two differences from the individual track

**Existing material enters as sources.** An organization standing up a brain over years of existing documents has years of sources, not years of finished works. Imported material MUST NOT be admitted at a stage that implies review the organization has not performed. Material that genuinely was published keeps its published structure and is marked as such. Everything else enters at the earliest stage.

**The boundary is mounted per contributor.** Where an individual brain mounts its boundary inside the domain that names the counterparty, an organization brain mounts it under a system surface, one subtree per contributor, alongside a contributor record and a contribution ledger.

```
<brain>/System/Boundary/
  Peers/<contributor-handle>.md
  Agreements/<agreementId>.yaml
  <contributor-handle>/
    In/  ledger.jsonl  Quarantine/
    Out/ ledger.jsonl  bundles/  receipts/
```

## Contributor records

An organization brain tracks who contributed what. It does not hold a copy of any contributor's brain. It holds the records it admitted, the ledger of how they arrived, and its own knowledge about that contributor.

## Host roles

Assign exactly one host as the owner of each mutable state root. An organization brain running on a dedicated machine, separate from any contributor's personal machine, removes whole classes of race rather than coordinating them.
