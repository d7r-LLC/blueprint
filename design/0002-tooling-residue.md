# Tooling Residue: Design Note

Non normative working note. Records rationale, the survey that motivated it, alternatives, and open decisions for TRACE/1.0.
Prepared: 2026-08-25.

---

## 1. The question

Agent harnesses leave trails: config directories, auth caches, session logs, memory stores, temporary working folders. The requirement is that this be treated as protected audit trail data linked to the brain's own ledgers, not as arbitrary machine litter, and that the treatment be enforced by configuration rather than by intention.

The framing I landed on is that this residue is simultaneously the best evidence the brain has and the worst leak it has. Both halves are true of the same bytes, which is why a single rule cannot cover it, and why the design ended up as six classes with six different handling rules rather than one policy about logs.

## 2. What is actually on the machine

I surveyed the local device before designing anything, because the scale determines whether this is a governance nicety or a live exposure.

| Location | Size | What it holds |
|---|---|---|
| `~/.codex` | 24 GB | 1,344 session files, 21 GB of transcripts, `auth.json`, `memories/`, `history.jsonl`, `dictation-history`, `transcription-history.jsonl`, `attachments/`, `computer-use/`, `generated_images/`, `shell_snapshots`, 1.4 GB telemetry database, `installation_id` |
| `~/.claude` | 3.3 GB | 4,340 session transcripts across 63 project folders, `file-history`, `history.jsonl`, `shell-snapshots`, `plans`, `tasks`, `telemetry`, `debug`, `backups` |
| `Library/Application Support/Claude` | 12 GB | desktop application state |
| `~/.ollama` | 17 GB | local model weights |
| `~/.cursor`, `~/.gemini`, `~/.continue`, `~/.vscode` | 1.7 GB | four more harnesses with their own trails |

The number that matters most: **578 transcript files, roughly 330 MB, in seven `~/.claude/projects/` folders whose names encode vault paths.** Those seven include `brain`, `brain/Shared`, `brain/d7r`, and `brain/d7r/Outputs/Courses/D7R-1-Fundamentals`. One of them is a `.claude-worktrees` scratch clone that lived inside the vault and held 80 MB of transcripts.

So the boundary domain, the shared entity layer, and course output are all present in full text in a directory that has no classification, no ledger entry, no retention policy, no gate, and no mention in the vault's governance. The vault's `.gitignore` opens with a prime directive about what no host, job, or agent may ever restore into the brain, and it mentions harness paths exactly twice, both times to exclude a single local settings file and a lock.

Three smaller findings shaped specific rules.

`~/.claude` and `~/.codex` are mode 0755 while `auth.json` and `.claude.json` are 0600. Credentials are protected and content is not, which is backwards relative to the risk, and it is the normal default everywhere.

`~/.codex` holds `memories/` and `memories_1.sqlite`. That is a persistent derived store of extracted facts that influences every future session, with no charter, no classification, no review, and no expiry. It is a second brain, and nobody decided to build it.

**63 harness files are already tracked in the vault's git repo, and every one of them is an agent definition or a skill.** `.codex/agents` has 13, `.claude/agents` has 14 including 7 advisors, and the rest are skills. Nothing else from either root is versioned.

That last finding is the most important one in the survey, because it is the shape of the correct answer arrived at by instinct. Directives were pulled into the brain and versioned. Residue was left where it fell. The instinct is right, and the spec's job is to make it a rule and to name what happens to the residue.

## 3. The central distinction

**Directives and residue are opposites that live in the same directory tree.**

| | Directives | Residue |
|---|---|---|
| Count | Few | Enormous |
| Reviewed | Yes, before taking effect | No, never |
| Versioned | Must be | Cannot usefully be |
| Time sense | Current only. Old versions are history | Historical only. All of it is the point |
| Failure if lost | Authority drift, silent behavior change | Evidence loss |
| Failure if leaked | Discloses how you work | Discloses what you know |

Every harness stores both under one root, which is what makes them easy to conflate, and conflating them produces one of two bad outcomes. Treat everything as directive and you try to version 24 GB of transcripts. Treat everything as residue and your agent definitions become untracked local state, which is where they were before someone thought to commit them.

So: A0 Directive gets the strictest rules, and A1 Session gets the retention rules, and they are different rules.

## 4. Six classes, and why six

| Class | Term | Failure it prevents |
|---|---|---|
| A0 | Directive | Authority drift. The charter describes an authority model no longer in force |
| A1 | Session | Evidence loss, and full text content escape |
| A2 | Derived | A shadow brain with no charter influencing every future session |
| A3 | Copy | Records existing outside the record contract, past their source's life |
| A4 | Credential | Capture together with content by any bulk operation |
| A5 | Telemetry | Undeclared egress and cross project correlation |

Six is more than I wanted. I tried three, splitting on protected, excluded, and egress, and it collapsed immediately because the protected group needs three incompatible rules. Directives must be current and versioned. Sessions must be historical and immutable. Copies must expire when their sources do. Any grouping that puts those under one rule produces a rule that is wrong for two of them.

The short nouns matter for the same reason the custody ladder uses them. These need to be sayable in a decision record: "harness memory is A2, so it gets adopted or it expires."

The rule that unmatched paths must never default to A5 came directly from the survey. Looking at 69 entries in `~/.codex`, most of which are undocumented, the tempting default for anything unrecognized is telemetry. That is the one default that both drops a file from protection and permits it to leave.

## 5. Linking to the brain ledger

The requirement was linkage. The mechanism is the **session anchor**, and the design principle behind it is containment.

```
session anchor (TRACE)        outer container, brain owned
  └── call records (CONFIDE)  inner events, broker owned
        └── record ids        the content, brain owned
```

An anchor opens when a session starts, and seals at close with the record set, the call ids, the artifacts produced, and the computed sensitivity. It is a normal Layer 6 entry: append only, hash chained, signed.

The critical design decision is that **the brain creates the anchor, not the harness.** A brain that enumerates its sessions by reading `~/.codex/sessions` has delegated the completeness of its own audit trail to the tool being audited. The harness trail is corroborating detail attached to a brain owned skeleton, never the skeleton itself.

Which forces the **observed versus attested** distinction, and I think that pair is the most useful idea in this document. Every claim about a session carries a grade. `observed` means a mechanism the brain controls produced it: a broker call record, a hook, a git commit. `attested` means the harness said so. An attested claim is never sole evidence for a governance conclusion, and every report must show the grade.

This is not paranoia about vendors. It is that a harness is not accountable to the brain, changes its storage format between versions, compacts and rotates on its own schedule, and has no obligation to record its own failures legibly. Without the grade distinction, a brain that reads a transcript and concludes "no confidential record was accessed" has proven nothing, because absence in an attested log is not absence.

The reconciliation this enables is the payoff. Two failures, and the second is the interesting one.

- A call record naming an anchor that does not exist: a call outside any recorded session.
- An anchor claiming a call the broker never saw: **either the harness reached a provider without the broker, which is a CONFIDE credential isolation failure, or the harness misreported, which downgrades every other attested claim it makes.**

Either way you learn something you could not learn from one ledger alone. That is the argument for two ledgers with a join key rather than one merged log.

## 6. Sealing, and why in place retention is not enough

The obvious cheap design is to reference `~/.claude/projects/...jsonl` from the ledger and call it linked. That produces a ledger that points at mutable state, which is worse than a ledger with an acknowledged gap, because it reports integrity it does not have. The harness can rewrite, compact, truncate, or delete that file at any time, including as a side effect of an upgrade nobody initiated.

So sealing copies bytes into a brain controlled append only store, digests them, and writes an artifact ledger entry. **An unsealed artifact is a lead. A sealed artifact is evidence.**

Three rules fell out of thinking about failure.

Sealing must not delete the source in the same operation. Failing closed here means failing toward keeping the original, because an unsealed original is a risk while an unsealed and deleted original is a lost record.

The artifact ledger stores digests, never content, for exactly the reason the CONFIDE call ledger stores hashes and not prompts. A ledger that inlines transcripts becomes the largest concentration of sensitive content in the brain and is read far more often, by more parties, than the records it describes.

Sealing 21 GB is not always affordable, so selective sealing is permitted, but **only at session granularity.** Partial sealing within a session is prohibited. A transcript with sections removed is not smaller evidence, it is unfalsifiable evidence, because nothing in it shows what was dropped. Either a session is sealed whole, or the decision not to seal it is itself a ledger entry stating why. The one exception is a shell environment snapshot, which is A4 and is excluded with the exclusion recorded.

## 7. The controls I would defend hardest

**Sensitivity is the maximum, never an average.** A session that read forty public records and one confidential record produces a confidential transcript, because the transcript contains that record's text. Any dilution scheme misclassifies exactly the sessions that matter. And where the read set is unknown, access is the bound: classify at the highest sensitivity anywhere in the scope the session could reach.

**An agent may not delete a protected artifact.** This is just "agents draft, the owner decides" applied to the audit trail, and it closes the hole where an agent can erase the record of what it did. When a previously enumerated protected artifact disappears with no entry, that is `protected-artifact-vanished`, which is the entire reason sealing exists: after a seal, the harness deleting its copy is bookkeeping, and before a seal, it is evidence loss.

**A reconstructed anchor does not satisfy the anchoring invariant.** Sealing will find artifacts from sessions that were never anchored, and the brain should reconstruct what it can, marked wholly attested. But if reconstruction counted as compliance, any gap could be papered over after the fact and the invariant would mean nothing.

**Scratch surfaces must be enumerated in the charter.** The `.claude-worktrees` folder inside the vault is the case in point: a location inside the brain folder where a file is not brain content. That exception is necessary, and it must be declared, must be excluded from the publication guard's inputs *and* from its notion of coverage, and must never satisfy a gate. An unenumerated exception is indistinguishable from a gap. This also connects to your existing rule that approval binds to bytes at a path: a copy in a scratch directory is a different artifact even when its digest matches.

**A syncing harness is a provider.** This closes the largest hole in CONFIDE taken alone. A brain can route every inference call to a resident C0 provider and still ship the complete text of every session to a vendor cloud, because the harness synced its history. The inference was governed and the record still left. So any harness transmitting A1, A2, or A3 artifacts gets a CONFIDE provider record and is bound by the same matrix.

**Retention has a ceiling, not just a floor.** An artifact kept past its purpose is a breach surface with no remaining benefit. `indefinite` is prohibited for every class except A0.

## 8. The one that will be least popular

Support bundles. A transcript from a session that read a record admitted from a peer under a C1 floor is itself C1 material. It cannot be attached to a vendor support ticket, and it cannot be pasted into an unregistered tool for debugging. This is the rule most likely to be broken, it will be broken with good intentions every time, and the same logic governs any backup that copies a harness root as a unit. Hence the strongest member rule: a bulk operation over a mixed root either applies the rules of every class present or is refused.

## 9. Tier placement

**Tier 1.** Register every harness with declared roots. Sweep for undeclared roots. Declare scratch surfaces. Verify no credential artifact is under version control. Registration and enumeration only, because a brain that cannot list what its tools left behind cannot describe its own audit surface, and because this tier is achievable in an afternoon.

**Tier 2.** Anchor every session, seal under a declared policy, hold directives inside the brain referenced by digest from the charters they implement, record deletions, prevent agents from deleting protected artifacts, adopt or expire derived state, reconcile anchors against the call ledger.

**Tier 3.** Enforce artifact custody floors including in backups and support bundles, register syncing harnesses as providers, do not transfer artifacts to peers except sealed, as incident evidence, under an agreement that names artifact transfer.

The self test in section 13.3 is eight seeded violations. The one I would run first is number six: put a file in a scratch surface that would satisfy a gate, and assert the gate does not pass.

## 10. Open decisions

1. **Spec name.** `TRACE/1.0`, expanded as Tooling Residue, Artifact Custody, and Evidence, matching the bare word precedent set by Blueprint and CONFIDE. Plain alternative: `HAP/1.0`, Harness Artifact Protocol.
2. **Fourth document, or sections inside CONFIDE.** I made it a fourth document because it completes a clean taxonomy: knowledge crosses to a brain under SPEAK, to a model under CONFIDE, into the tooling under TRACE. The cost is a repository with four normative documents, and the alternative was a CONFIDE at roughly seventy kilobytes covering two subjects.
3. **Sealing at 21 GB.** The honest options are seal everything with a real storage cost, seal selectively per section 8.4, or seal a digest and index per session while leaving bodies in place and accepting that they are attested rather than sealed. I did not specify the third because it dilutes what sealing means, but it is the pragmatic answer for existing volume and deserves an explicit decision.
4. **Whether A2 adoption is realistic.** Adopt or expire is the right rule and it is real work. The weaker form is to require only that derived stores be enumerated, classified, and age bounded, without requiring adoption. I lean toward keeping adoption required, because unadopted derived state is precisely the ungoverned second brain the whole system exists to prevent.
5. **Anchor granularity.** Per session is what harnesses reliably identify. Per turn would be more precise and would require hooks that most harnesses do not offer. Per working day would be cheap and would lose the sensitivity boundary that makes the classification rule work.
6. **What to do with the existing 578 files.** Options: seal them now as a one time historical batch and accept the storage, classify and hold them in place pending review, or purge with a manifest after extracting anchors. This is a decision record, not a spec question, and it should be made before the registry goes live, because the registry will otherwise describe a clean state that does not exist.

## 11. Suggested next build steps

Ordered so that each step produces something checkable, and placed before the CONFIDE broker work only where it is cheaper to do first.

1. Enumerate and register. Eight harness records for the eight roots found in the survey, with honest class rules and honest `unknown` values. This is a day of work and it is the artifact that makes everything else possible.
2. Fix the permissions inversion. Content directories at 0700, not 0755.
3. Declare scratch surfaces in the charter, and widen the vault's ignore rules from one settings file to a class based set.
4. Bring the remaining A0 artifacts under the same treatment as the 63 already versioned, and add digest references from the seven agent charters to the definitions that implement them.
5. Decide on the existing 578 files, per open decision 6, and record it.
6. Write the sweep: undeclared roots, credential artifacts in the wrong places, growth against declared expectations, A0 outside the brain. Sweep before sealing, because enumeration finds problems and sealing only preserves them.
7. Then anchors, then the artifact store, then retention.

---

## Sources

Local device survey conducted 2026-08-25 on the author's machine, plus the specifications in this repository.

- Artifact root sizes and file counts: `~/.claude`, `~/.claude.json`, `~/.codex`, `~/.cursor`, `~/.gemini`, `~/.ollama`, `~/.continue`, `~/.vscode`, `Library/Application Support/Claude`, `Library/Logs/Claude`
- Vault referencing transcripts: seven folders under `~/.claude/projects/` matching `-Users-sthornock-code-obsidian*`, 578 `.jsonl` files
- Versioned harness files: `git ls-files` in `/Users/sthornock/code/obsidian` filtered to `.claude`, `.codex`, `.cursor`
- Ignore rules: `/Users/sthornock/code/obsidian/.gitignore`
- `<repo>/blueprint/spec/BLUEPRINT-v1.0.md`, `spec/CONFIDE-v1.0.md`, `spec/SPEAK-v1.0.md`, `spec/TRACE-v1.0.md`
- `<repo>/blueprint/design/0000-workflow-and-spec-design.md`, `design/0001-inference-governance.md`
- `/Users/sthornock/code/obsidian/brain/AGENTS.md` (sensitivity vocabulary, the seven agent identities, decisions `0018`, `0027`, `0037`, `0038`)
- `/Users/sthornock/code/d7r/src/agent-rights/spec/BILL_OF_RIGHTS-v1.0.md` (Right IX Transparency)
