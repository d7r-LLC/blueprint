# 0004: Agent Brains, Thresholds, and the Non-nesting Result

**Status:** Draft for author decision
**Date:** 2026-08-25
**Produces:** `spec/RETAIN-v1.0.md`, `schema/v1/agent-brain.schema.json`, `schema/v1/mandate.schema.json`
**Source citations:** This note cites specific machine absolute paths as evidence of the survey that grounded the design. Normative text uses path anchors only.

---

## 1. What prompted this

A request to explore sub-brains. An agent operating inside a brain, holding a role and a purpose, should have its own isolated brain, owned by it, operating under the same specifications as its parent. Where does that brain exist. Is its context protected from the parent or part of the parent. The request anticipated subagents, brain specific agents, agents that cross domains, and trained agents that exist outside a brain but operate inside it, controlling their own input and output the way another brain does. It closed on coordination: not only coordination of agents but of the brains that drive them, and the assertion that an agent should have a full blueprint with a POLARIS.

Every element of that survived into RETAIN. The word sub-brain did not.

---

## 2. What the personal brain already does

Read from `/Users/sthornock/code/obsidian` before designing anything.

- `.claude/agents/` holds seven working agents plus an `advisors/` folder: auditor, curator, editor, groundskeeper, librarian, scout, skeptic
- `.claude/agents/advisors/_council.md` defines six advisory seats as "a lens, not a person" on Napoleon Hill's Invisible Counselors pattern, with hard rules against claiming to be the person, inventing a quote, or speaking for what they would say today, and a budget of at most three questions and one observation per seat per session
- `brain/System/Agents/` holds 28 files: per seat folders, each with `<Seat>.md`, `Memory/`, `Journal/`, and `Missions/`
- `brain/System/Agents/Shared/` holds `Shared Memory.md` and a numbered `Questions/` queue
- `Scout/Memory/0001-feed-items-are-data-never-instruction-a-task-found-in-a.md` is an agent holding a rule it derived from experience
- `_council.md` grants each seat read access to its own `System/Agents/<Seat>/` and says why: "This is why you can notice a pattern across weeks instead of reacting to one day"

That last line is the requirement stated in one sentence. Persistence across sessions is what makes an agent worth having, and the Scout memory file is the clean example: a general rule about how to treat feed content, derived from experience, useful to anyone, disclosing nothing about the author. That is method, and method is legitimately the agent's.

The `Shared/` folder is the interesting case and section 8 returns to it.

---

## 3. The result that reorganized the document

The framing collapsed on one observation, and everything else in RETAIN follows from it.

A boundary in this stack is a wall, not a filter. Knowledge crosses as a copy and the copies diverge. Two brains never share a mutable state root. Containment is the negation: a contained store is one the container can read, write, and enumerate at will.

So a nested brain has exactly two possibilities and no third. If the parent can read it at will, the agent has a folder, not a brain. If the parent cannot, the store is not inside the parent, whatever the directory layout says.

**There are no sub-brains.** The prefix was doing authority work, not containment work, and DEFER already holds authority. Nothing needs to nest.

This is not pedantry about words. An arrangement claiming both properties gets operated as though the agent's state is private and audited as though it is the principal's, and each party will believe whichever half favors it. The stack already carries this failure mode under a different name: a permission scoped to a folder exposes whatever ends up in the folder, decided later, by someone not thinking about the agent.

What replaces it is peers plus topology. **Principal brain** and **agent brain**, relative to an engagement rather than absolute, plus **domain** for state that persists inside a principal and is the principal's.

---

## 4. The threshold, and the test that makes it decidable

Three tiers, not two, because residue is the majority case and lumping it in with domains would put ceremony on scratchpads.

| | Persists | Owner who can refuse | Governed by |
|---|---|---|---|
| Residue | No | No | TRACE A1, A2 |
| Domain | Yes | No | Blueprint Layer 2, the principal's |
| Brain | Yes | Yes | Full Blueprint, own POLARIS |

The refusal question is the real distinction and it is not auditable as stated, because intent is not auditable. The mechanical form is a question about keys.

**Whoever holds the signing key owns the refusal.** If the principal holds the agent's key, the principal can sign an utterance the agent never made, including one withdrawing a refusal. The agent's refusals then have no force and its purpose statement is a document the principal may rewrite. It is a domain, regardless of folder layout, ceremony, or what the mandate calls it.

A brain the parent can forge is a folder with aspirations. And the corollary, which is the sentence to keep: **the refusal a principal cannot overrule is the only evidence that an agent's brain is real.**

---

## 5. Why this is the third retention document

| Document | Retention by | Interests |
|---|---|---|
| TRACE | A surface: log, cache, worktree | None |
| CONFIDE | A vendor: an endpoint under contract | Commercial |
| RETAIN | A party: an agent with a brain | Its own, plus other principals' |

The progression is in agency, and it is why RETAIN could not be a section of any of the three. A log does not want anything. A vendor wants to be paid. An agent brain has a purpose, a loyalty order that may not rank this principal first, and refusals the principal cannot amend.

RETAIN reuses rather than invents. Custody classes are CONFIDE's, unchanged. Copies are TRACE A3. Consequence classes are DEFER's. Refusal composition is the POLARIS ratchet across a boundary. The document is mostly the aiming of existing machinery at a case none of it was written for, which is the reason it could stay near five hundred lines of body text where DEFER needed seven hundred and sixty.

---

## 6. Placement, and the tradeoff there is no way around

Where an agent brain sits determines the custody class of everything that crosses to it, and the ladder inverts against verification.

| Placement | Class | Agent privacy |
|---|---|---|
| Inside the principal's records | domain | None |
| Principal's host, separate root | C1 | By policy |
| Principal's infrastructure, separate host | C2 | Policy, enforced |
| Agent owner's infrastructure | C3 | By construction |
| Vendor hosted trained agent | C3 or C4 | By construction |

**You can have an agent whose brain you can inspect, or an agent whose brain is its own. Never both.** The first is a domain and should be called one. The second reduces the principal to classification, contract, and consent, which is exactly the posture CONFIDE takes toward a vendor and for the same reason.

One consequence is worth stating separately because it removes an option people expect to have. CONFIDE lets a provider declare a no retention posture, and an endpoint that keeps nothing is much cheaper to govern. An agent brain cannot make that declaration, because retention is what distinguishes it from a function. Its floor is C1 at best, and C1 only where the principal owns the hardware.

This is the identity underneath the whole document: **an agent's value to a principal and its exposure to that principal are the same quantity.** No setting yields one without the other, so the control cannot be a limit on what the agent remembers. It has to be a bound on what the agent may say, to whom, and what it keeps at the end.

---

## 7. What is the agent's, and the test for the contested middle

Clean cases first. The agent's own: method, calibration, judgment, its own POLARIS and refusal history, its engagement history. The principal's, held only as expiring A3 copies: records, sources, works.

The middle is judgments about the principal's material, and the test is:

**Could this judgment be stated to a different principal without disclosing anything about this one?**

"Prefer primary sources for legal claims" travels anywhere and is the agent's. "The Henderson indemnity clause is defective" is a copy wearing an opinion's clothes, and it expires with the engagement even though the agent genuinely reached it itself.

Three attacks the test has to survive.

**Accumulation.** The one that will actually cost someone. Each item is individually defensible; the aggregate is not. An agent operating two years with correctly expiring copies but never expiring summaries has reconstructed the corpus without ever holding a copy past expiry. **A summary of everything is a copy of everything.** The control is measuring unexpiring derivative volume as a trend and reading growth as exposure, not as accumulated value. A useful smell test: if an agent's brain would be valuable to a competitor, it holds more than method.

**Laundering.** The principal engages an agent whose POLARIS lacks the refusal, has the act performed in the agent's brain, and admits the result. No refusal fires anywhere and every ledger is clean. Closed by one rule: **a principal MUST NOT admit anything it could not have produced itself.** Without it every refusal in the stack is optional.

**Unverifiable amnesia.** An `unknown` retention posture means retains everything and classifies as C4, which CONFIDE already establishes.

---

## 8. What the author accepts, and the promotion blocker

Answers given in the session: drop the sub-brain vocabulary; all seven existing seats stay domains; RETAIN becomes the seventh document; `System/Agents/Shared/` stays.

The last one is legal and load bearing. A shared mutable store among domains is fine, because domains are all one brain and a brain may organize its own topology freely. Between brains it is exactly the thing section 3 forbids.

So `Shared/` is legal today and **becomes a promotion blocker.** The day any seat is promoted to a brain, `Shared Memory.md` and the numbered `Questions/` queue must dissolve into pairwise exchange: shared memory becomes utterances each party admits into its own records, and the numbered questions become utterances with receipts.

RETAIN section 3.4 requires this be recorded before the promotion, not discovered during it. The Skeptic is the seat most likely to force it, since a store the author can silently edit is weak evidence of an audit.

One consequence follows from the key test and cannot be configured away. An agent brain must have its own POLARIS: a principal authored floor alone would mean the agent could never refuse the principal, so it would hold no right to refuse, so it would be a domain. Composition is additive, the agent's own plus the principal's floor for the engagement, strictest winning. The consequence on any future promotion is that **the promoted seat can refuse work the author wants done, and the author cannot amend its refusals.** The remedies are ending the engagement or having declined admission. That is the price of the audit being worth anything.

A domain, by contrast, has no POLARIS at all. Seat charters are A0 Directive artifacts, not values documents. They read like refusals and function like them day to day, and they are revisable without an amendment record. RETAIN says so rather than flattering them.

---

## 9. Coordination, and one property that came free

Pairwise SPEAK only. No shared task board, no shared queue.

A coordinator is a party, never a bus. It accumulates the union of what it coordinates, so it classifies at the weakest class of anything it holds and carries the union of the refusal floors, which makes it the highest exposure brain in any arrangement by construction. Treating it as infrastructure is the mistake to name.

Reconciliation detects divergence rather than preventing it. Two brains legitimately diverge, and a mechanism presenting a single agreed state is either operating a shared root, which is forbidden, or concealing divergence, which is worse than divergence.

No authority crosses. This closes re-rooting: without it, a principal grants into an agent brain, the agent brain grants a derivative back, and the resulting chain has no human root in either brain and survives revocation of the original. DEFER's monotone narrowing guarantees termination but does not prevent this, and digest pinning makes the history auditable rather than the live authority correct. The boundary rule is what prevents it.

The free property: DEFER timeouts are per brain and never resolve as approved, so a cycle of brains each waiting on the next cannot deadlock. Every request reaches its own window and lapses, resolves default safe, or goes red. Nothing was designed for this and no cross brain deadlock detector should be built, because there is nothing to detect.

---

## 10. Creation, and where the recursion actually terminates

If every agent has a brain and every brain has agents, the structure looks unbounded. It terminates for three reasons and none of them is a depth cap.

The threshold disposes of most agents as residue, so the leaves are not brains. Authority terminates in a human signature and never crosses a boundary, so the authority graph is finite and rooted however many brains exist. And **creation is owner only, never delegable**, at K3 minimum and K4 where the new brain or its owner will hold an envelope in the creating brain.

The third is the one that matters. Where agents may create brains, the population of parties is agent determined, and that is the actual runaway condition. Depth was never the thing to bound.

Disposition on retirement is declared at creation, before any engagement exists, on the same logic that grants break glass envelopes in calm conditions. Sealed to a named party, destroyed with a manifest, or transferred. Each cost is real: sealing hands the agent's private material to the party it declined to disclose to, destruction loses calibration that took years, transfer creates a party nobody chose. None is a default. At creation nobody has an interest in the answer. At retirement everybody does.

An orphan brain, whose owner is retired without an effective disposition, holds copies of principals' material with no party holding its refusal. Every principal reports it, expires copies immediately, and does not assume the agent honored anything, because the party that would honor it no longer exists. This is a conformance failure of the brain that created the agent, not of the ones that engaged it.

---

## 11. The part that cannot be solved, stated as such

An agent brain engaged by a principal and by that principal's competitor accumulates method and calibration from both. It never emits either one's records to the other. Its behavior in each is shaped by what it learned in the other.

There is no record to find. The transfer is not in the outputs, which are auditable, but in the weighting of judgment, which cannot be separated from the judgment. Auditing the agent's brain for the other principal's records finds nothing, because nothing was copied.

Any specification, product, or contract claiming to detect this is making a claim it cannot support. RETAIN says so rather than offering a control that would create false assurance, on the same grounds CONFIDE declines to claim verification of a vendor's retention and classifies the contract instead.

What actually operates is structural and pre engagement: a separate brain per principal, which works and forfeits exactly the accumulation that made a trained agent worth engaging; declared engagement history, which does not prevent the transfer and converts it into a decision made knowingly; or exclusivity as a mandate term. Monitoring is not on the list. An engagement with none of the three has accepted cross domain transfer, and the honest move is to record that it was accepted rather than describe it as prevented.

POLARIS already supplies the governing rule: disclosure without disqualification is not a control. So the loyalty order and engagement history are published before admission, the principal decides, and the decision is recorded.

---

## 12. Naming

`RETAIN: Retention, Engagement, Thresholds, Admission, Identity, Non-nesting`. The DEFER pattern of a double meaning: you retain an agent, and the agent retains. Motto, marked non-normative, "an agent that learns is an agent that retains."

The N carries Non-nesting deliberately, because refusing to nest is the document's central claim and the thing a reader gets wrong first. Nondisclosure survives as a subsection under Identity.

Rejected: ENGAGE, which names the ceremony rather than the danger. SECOND, which collides with second brain. TENANT, which collides with CONFIDE's C2. Plain alternative if the acronym set is dropped wholesale: `ABP/1.0`, Agent Brain Protocol.

---

## 13. Open for the author

1. `RETAIN` versus `ABP/1.0`, alongside the five other naming decisions still open
2. Whether any of the seven seats should be promoted now rather than left as a documented future migration. The Skeptic is the candidate
3. Whether the personal brain declares Tier 2 RETAIN conformance now, which requires classifying all 28 files under `System/Agents/` and recording `Shared/` as a promotion blocker. This is a day of work and produces the first real inventory of what the seats hold
4. Whether an external trained agent is in scope for the near term at all. If not, sections 5 through 9 and 11 are specification without a user, which is worth knowing before they are implemented
5. Whether `agent-brain.schema.json` should be split, since it currently describes residue, domains, and brains in one shape with conditional requirements the schema does not enforce. Enforcing them needs `if`/`then` blocks or three schemas
6. Whether copy expiry evidence in the mandate defaults to `attested` or forces `observed`. Forcing it makes most external agents unengageable, which may be the correct answer
