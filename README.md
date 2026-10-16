# Warren Smith

I investigate cases where a computational check says everything is fine, but
the property it is supposed to establish has already failed.

In [mcp-authority-boundary](https://github.com/repowazdogz-droid/mcp-authority-boundary),
every test passed and the replay verifier said VERIFIED while a 100,000-byte write ran
under a 4,096-byte cap.

## Flagships

- [inspect-replay](https://github.com/repowazdogz-droid/inspect-replay): sample-aligned comparison of two Inspect AI evaluation logs that reports "cannot tell" separately from "unchanged" and exits non-zero when anything moved.
- [vsf-cjson](https://github.com/repowazdogz-droid/vsf-cjson): cJSON re-implemented in Lean 4 and proved adequate against a formal grammar; differential testing found four inputs cJSON silently alters or wrongly accepts, such as `1e400` parsing to `null`.

More cases, each with a public reproducer: [silent-pass-catalogue](https://github.com/repowazdogz-droid/silent-pass-catalogue).

## AI assistance

I use AI heavily in this work, including Claude, Codex and Cursor for code, research
and drafting; the commit history makes that visible. I choose what to
investigate, set the tests and stopping conditions, and decide what the
evidence justifies claiming. Results that fail or narrow the original idea
stay in the record.

## Reviewed upstream

Merged, mine: common_cells #355 (a SymbiYosys proof for the ECC encoder and decoder,
which found an undriven `syndrome_o`), PyBaMM #5747 (a lithium-conservation fix in the
Basic electrolyte model), inspect-robots #425 (records the effective grader configuration),
cvc5 #12937 (a polarity-caching fix in separation-logic reduction that produced `sat`
where `unsat` was expected).

Reported here, fixed upstream: inspect_ai #4602, inspect-robots #413, LemmaScript #206.

Open: cedar-spec #995, Strata #1448, genome-nexus #881, METR task-standard #42,
and two in Strata-CLI.

[All merged PRs](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Amerged+-user%3Arepowazdogz-droid&type=pullrequests) · [all open PRs](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Aopen+-user%3Arepowazdogz-droid&type=pullrequests) · [all issues](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Aissue+-user%3Arepowazdogz-droid&type=issues)
