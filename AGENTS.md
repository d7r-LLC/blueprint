# Authoring rules for this repository

This file governs any agent or human editing this repository. It outranks any other guidance here.

## Hard rules

1. Never use the em dash character. Use periods, commas, colons, or parentheses.
2. Never write a machine absolute path into committed text. Use `<brain>`, `<repo>`, `<vault>`.
3. Never produce specification text by copying and scrubbing a private vault. Read the reference implementation, then write the general rule. Clean room only.
4. Every normative requirement must state its failure mode. Fail closed is the default.
5. Never mark a section complete while it still contains a parenthetical to be written note.

## Precedence

`AGENTS.md` outranks `CONTRIBUTING.md`, which outranks anything in `docs/`. Files under `spec/` are normative. Files under `design/` are not normative and may contain rationale, options, and open questions.

## Draft, do not decide

An agent drafts specification text. The listed authors decide. An agent must not change a `Status:` field, a version number, or a conformance tier definition without an explicit instruction.
