# Warren Smith

I investigate cases where a computational check says everything is fine, but
the property it is supposed to establish has already failed.

One experiment replayed as VERIFIED while executing a 100,000-byte write under a 4,096-byte cap.

That has taken me from agent authorization and formal verification to
scientific software and hardware verification. I tend to build the smallest
experiment I can that could prove my idea wrong, then keep the result even
when it does.

## AI assistance

I use AI heavily in this work, including Claude, Codex and Cursor for code, research
and drafting; the commit history makes that visible. I choose what to
investigate, set the tests and stopping conditions, and decide what the
evidence justifies claiming. Results that fail or narrow the original idea
stay in the record.

## Selected work

Pinned below. If you read one, start with mcp-authority-boundary.

Also public, each with its limits stated in its own README:

**Formal verification**

- [escrow-budget](https://github.com/repowazdogz-droid/escrow-budget): Lean 4 proof that a distributed budget protocol keeps aggregate spend within a global cap under message loss and crash/recovery. [escrow-budget-mpst](https://github.com/repowazdogz-droid/escrow-budget-mpst) checks the transfer sub-protocol a second way, with session types in Rust, and says where the two methods do not overlap.
- [vsf-cjson](https://github.com/repowazdogz-droid/vsf-cjson): cJSON re-implemented in Lean 4 and proved adequate against a formal grammar. Differential testing against the unmodified C found four inputs that cJSON silently alters or wrongly accepts, such as `1e400` parsing to `null`.
- [collective-bound](https://github.com/repowazdogz-droid/collective-bound): the Lean 4 and Z3 core of work accepted at AMLUCS 2026. Agents that each stay inside their own cap can together exceed a smaller shared pool; [commons-agent-lab](https://github.com/repowazdogz-droid/commons-agent-lab) tests whether LLM agents actually do.
- [compositional-temporal-safety](https://github.com/repowazdogz-droid/compositional-temporal-safety): assume-guarantee composition of per-agent proofs into a system-wide spending bound, in Lean 4 and TLA+.
- [omega-lean-proof](https://github.com/repowazdogz-droid/omega-lean-proof): Lean 4 proof that a tamper which still verifies in a canonical-encoding hash chain yields a hash collision.
- [verify-mcp](https://github.com/repowazdogz-droid/verify-mcp): Lean, TLA+/TLC and Rocq proof checks as MCP tools, with a three-valued result.

**Evaluation**

- [proof-carrying-evals](https://github.com/repowazdogz-droid/proof-carrying-evals): on six violating agent decisions, a local 14B LLM judge passed 4 and the formal checker proved all 6 violated.
- [apart-defensive-workflow-2026](https://github.com/repowazdogz-droid/apart-defensive-workflow-2026): all 16 Claude refusals on a synthetic incident-response battery arrived as HTTP 200 with no text, and a text-only detector labelled every one AMBIGUOUS.
- [inspect-audit](https://github.com/repowazdogz-droid/inspect-audit) and [inspect-replay](https://github.com/repowazdogz-droid/inspect-replay): a validity audit for a single Inspect log, and a sample-aligned comparison of two.
- [secret-loyalties-matched-base-audit](https://github.com/repowazdogz-droid/secret-loyalties-matched-base-audit): without subtracting the base model, two blind interpreters named the wrong model as fine-tuned.

**Security**

- [mcp-boundary-audit](https://github.com/repowazdogz-droid/mcp-boundary-audit): finds MCP tools hidden from `tools/list` that still answer `tools/call`.
- [omega-n1-permit-membership](https://github.com/repowazdogz-droid/omega-n1-permit-membership): a permission record that was never issued was accepted, and the effect ran. Standard-library reproduction.
- [nanogpt-provenance](https://github.com/repowazdogz-droid/nanogpt-provenance): a verifier that recomputes a training run's claimed loss instead of trusting the log, and reports cross-hardware re-derivation as UNKNOWN.
- [ai-research-security-plane](https://github.com/repowazdogz-droid/ai-research-security-plane): in-series controls for a model artifact from build to serving, with negative-control tests that assert the insecure behaviour when each control is removed.

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

## Contact

warren@omegaprotocol.org · [omegaprotocol.org](https://omegaprotocol.org)
