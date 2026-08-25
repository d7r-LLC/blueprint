# Contributing to Blueprint

## House rules

1. **Never use the em dash character.** Use periods, commas, colons, or parentheses.
2. **No machine absolute paths in committed text.** Use the anchors `<brain>`, `<repo>`, and `<vault>`.
3. **RFC 2119 keywords are load bearing.** MUST, MUST NOT, SHOULD, SHOULD NOT, MAY. If a requirement cannot be tested, it is prose and belongs in `design/`.
4. **Clean room.** No section of a specification may be produced by copying and scrubbing a private vault. Read a reference implementation, then write the general rule.
5. **Every normative requirement needs a failure mode.** State what an implementation does when the requirement is violated. Fail closed is the default.

## Change process

Substantive changes to a specification go through an RFC.

1. Copy `rfcs/0000-template.md` to `rfcs/NNNN-short-title.md`.
2. Open a pull request. The RFC gets a 30 day comment period.
3. MAJOR changes require a two thirds supermajority of listed authors. MINOR and PATCH changes require one approving author review.

Editorial changes (typos, formatting, broken links, clarifications that do not alter a requirement) go straight to a pull request with no RFC.

## Versioning

Semantic versioning on the specification, not the repository.

- **MAJOR:** a conformant implementation of the previous version is no longer conformant.
- **MINOR:** new optional capability, backward compatible.
- **PATCH:** clarification with no change to conformance.

## Schema changes

Any change to a wire format in `schema/v1/` is at minimum MINOR, and any removal or retyping of an existing field is MAJOR. Wire formats carry a `contractVersion` string, and that string changes when the shape changes.
