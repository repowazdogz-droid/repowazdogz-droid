# Warren Smith

I investigate cases where a computational system reports success without establishing the property that actually matters. I am an independent researcher and direct [OMEGA](https://omegaprotocol.org), an AI-native computational research system. AI agents do much of the work; [how that works](#how-this-work-is-done) is set out below.

People act on green results. In the cases below, a solver answered `sat` where `unsat` was expected, a battery model's lithium inventory drifted by 2.44%, and a replay verifier said VERIFIED while a 100,000-byte write ran under a 4,096-byte cap.

## Reviewed and merged by maintainers

| Pull request | What it changed |
|---|---|
| [cvc5 #12937](https://github.com/cvc5/cvc5/pull/12937) | Fixes a polarity-caching bug in separation-logic reduction behind `sat` where `unsat` was expected. The bug report, [#12870](https://github.com/cvc5/cvc5/issues/12870), came from another user. |
| [PyBaMM #5747](https://github.com/pybamm-team/PyBaMM/pull/5747) | Restores a missing flux term in the Basic electrolyte models. With a concentration-dependent transference number, `BasicDFN` lithium drift fell from about 2.44e-2 to about 2e-14. The half-cell model keeps a pre-existing floor near 1e-6. |
| [common_cells #355](https://github.com/pulp-platform/common_cells/pull/355) | Adds a SymbiYosys proof for the ECC encoder and decoder. Writing it exposed a declared `syndrome_o` output that was never driven, and the PR fixes that too. |
| [inspect-robots #425](https://github.com/robocurve/inspect-robots/pull/425) | Records the grader and its resolved configuration in evaluation logs, so two differently graded runs no longer produce identical specs. |

Approved, not yet merged: [Qcodes #8627](https://github.com/microsoft/Qcodes/pull/8627), a numpy integer overflow fix for parameter stepping.

Reported and fixed by maintainers: [inspect_ai #4602](https://github.com/UKGovernmentBEIS/inspect_ai/issues/4602) and [inspect-robots #413](https://github.com/robocurve/inspect-robots/issues/413). [LemmaScript #206](https://github.com/midspiral/LemmaScript/issues/206) led to an opt-in `impure` marker on externs; the default is unchanged.

Under review: [cedar-spec #995](https://github.com/cedar-policy/cedar-spec/pull/995) (changes requested), [Strata #1448](https://github.com/strata-org/Strata/pull/1448), [Strata-CLI #7](https://github.com/strata-org/Strata-CLI/pull/7) and [#8](https://github.com/strata-org/Strata-CLI/pull/8), [genome-nexus #881](https://github.com/genome-nexus/genome-nexus/pull/881), [chemprop #1417](https://github.com/chemprop/chemprop/pull/1417), [TorchIO #1536](https://github.com/TorchIO-project/torchio/pull/1536).

Withdrawn: [lean-kernel-arena #196](https://github.com/leanprover/lean-kernel-arena/pull/196) and [#207](https://github.com/leanprover/lean-kernel-arena/pull/207). I closed both after a maintainer's question showed they added nothing the arena did not already have.

[All merged PRs](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Amerged+-user%3Arepowazdogz-droid&type=pullrequests) · [all open PRs](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Aopen+-user%3Arepowazdogz-droid&type=pullrequests) · [all issues](https://github.com/search?q=author%3Arepowazdogz-droid+is%3Aissue+-user%3Arepowazdogz-droid&type=issues)

## Original work

Each repository has its own statement of limits. I know of no independent reproduction of these results by someone else.

- [mcp-authority-boundary](https://github.com/repowazdogz-droid/mcp-authority-boundary): the VERIFIED case above. The first version passed 66 tests and its ledger replayed cleanly, while an independent observer saw the oversized file. It covers one MCP server and one authored policy set, and the failure class (CWE-436) is not new.
- [vsf-cjson](https://github.com/repowazdogz-droid/vsf-cjson): an experiment in how far an AI agent can port a C library to Lean 4, with unmodified cJSON as the oracle. It found four cJSON bugs, such as `1e400` parsing to `null`. Round-trip theorems are proved; which inputs the parser accepts is measured, not proved.
- [inspect-replay](https://github.com/repowazdogz-droid/inspect-replay): compares two Inspect AI evaluation logs sample by sample and reports "not recorded" separately from "unchanged".
- [collective-bound](https://github.com/repowazdogz-droid/collective-bound) and [commons-agent-lab](https://github.com/repowazdogz-droid/commons-agent-lab): the formal and empirical sides of an [AMLUCS 2026 accepted poster](https://www.omegaprotocol.org/amlucs-2026-poster.pdf). With caps summing to 1.5 times the shared budget and agents unable to see the pool, every agent stayed within its own cap and the budget was still breached in 60 of 60 baseline episodes on each of three models. This is a preregistered study of a simplified environment, not a claim about deployed systems.
- [spcu-verification](https://github.com/repowazdogz-droid/spcu-verification): a small power-control IP checked with open formal tools. Two of five injected defects passed every property written from the specification, and 93 of 200 sampled netlist mutations survived and were observable.
- [silent-pass-catalogue](https://github.com/repowazdogz-droid/silent-pass-catalogue): 12 cases of a check passing after its property had failed, each with a reproducer and an upstream acknowledgement or independent oracle. They come from my own work, so no rate follows from them.

## How this work is done

OMEGA is the research system I designed and direct. I use AI heavily, including Claude, Codex and Cursor. Agents carry out implementation, test development and execution, and much of the research and drafting. I choose what to investigate, set the acceptance criteria and stopping conditions, challenge the conclusions, and decide what the evidence justifies claiming. Read my name on a commit or PR as direction and responsibility, not as hand-written code. Commit history does not show AI use reliably, so this paragraph is the disclosure.

Results that fail or narrow the original idea stay in the record.

The contributions above touch SMT solving, battery modelling, hardware verification and AI evaluation. Each is one specific result, not a demonstrated general capability in that field.

More: [omegaprotocol.org](https://omegaprotocol.org)
