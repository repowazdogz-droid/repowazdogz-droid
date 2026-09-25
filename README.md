# Warren Smith

I build experiments and verification systems for the places where software passes its checks while the property the checks stand for has already failed. Bristol, UK.

The pattern I keep finding is the same across authorization layers, monitoring pipelines, LLM judges, proof tooling and hardware verification: the check ran, the check was green, and the check could not see the failure. The work below builds the instrument, runs it, and records what the green signal did and did not establish.

## What the system said, and what the evidence showed

| The system said | The evidence showed | Where |
|---|---|---|
| Authorised, tests green, replay VERIFIED | a 100,000-byte write executed under a 4,096-byte grant, because execution was not bound to the operation Cedar authorised | [mcp-authority-boundary](https://github.com/repowazdogz-droid/mcp-authority-boundary) |
| 1,026 actions prevented | all 1,026 executed; a monitor beside the path records intentions that read exactly like outcomes | [safeguards-control-plane](https://github.com/repowazdogz-droid/safeguards-control-plane) |
| Every agent within its allowance | the shared budget was breached in 60 of 60 BLIND episodes on each of three models (two cells of 30, every agent within its allowance). Counting only episodes in which every agent stayed within its allowance, for gpt-4.1-mini, gpt-5-mini and gemini-2.5-flash respectively: stating the remaining headroom (METER) left 60, 40 and 34 of 60 breaching; adding one more sentence restating the same headroom (RESTATE) left 4, 2 and 0 (Gemini also had one RESTATE breach that involved an individual overdraw, not counted here); rewording the headroom line in place instead of adding a line (REPHRASE) left 41, 14 and 1 | [commons-agent-lab](https://github.com/repowazdogz-droid/commons-agent-lab) |
| All 26 requirement-derived assertions pass the unbounded proof (PDR, collapsed-clock model, four environment assumptions; 2 vacuous, 3 needing a further stated assumption; clock-crossing checks bounded at depth 20) | two injected defects passed every specification-derived property, because the specification never stated the requirement they break | [spcu-verification](https://github.com/repowazdogz-droid/spcu-verification) |
| LLM judge: PASS, 8/10, three seeds | Z3 proved the decision violated the encoded policy; the judge passed 4 of the 6 violating decisions, the checker caught 6 of 6 | [proof-carrying-evals](https://github.com/repowazdogz-droid/proof-carrying-evals) |
| Verifier: green | the run could not have failed: a Kani assertion never reached, a loom test that instrumented nothing, and a Lean axiom audit byte-identical for a correct and a wrong model | [evidence-audit](https://github.com/repowazdogz-droid/evidence-audit) |

Each row is a number computed by a script in that repository from committed evidence, with a limitations file that says what the number does not establish.

## The six repositories

**[spcu-verification](https://github.com/repowazdogz-droid/spcu-verification)**: a small DVFS power-control IP verified with open tools (SymbiYosys, Verilator, pyuvm, bare-metal C). Formal found four unseeded RTL bugs and one requirement that no synchronous design could satisfy as written. Then mutation analysis showed two defects invisible to every property, and a 200-mutant `mcy` run showed the hand-written mutations had probed the wrong part of the design. Unbounded proofs are separated from bounded checks, and the vacuous assertions are kept and excluded from every claim.

**[mcp-authority-boundary](https://github.com/repowazdogz-droid/mcp-authority-boundary)**: a Cedar-mediated MCP tool server. Version 1 passed 66 tests and a replay verification while a 100 KB write went through a 4 KB cap. The audit is preserved, the repair binds execution to the canonical operation, and the repair is re-attacked with a falsification sweep. Mediation and binding are established; policy adequacy and effect verification are stated as not established. 182 tests, CI (182/182 on `main` at 2ea137b).

**[safeguards-control-plane](https://github.com/repowazdogz-droid/safeguards-control-plane)**: a fault-injected testbed on Redis Streams with two arms that differ only in position, one on the path and one beside it. Under injected drops, duplicates and crashes the monitor's dashboard reports 1,026 preventions and 0 hold. Two independent writers catch what single-writer telemetry cannot. Nine negative controls; CI deletes the committed results and regenerates them.

**[commons-agent-lab](https://github.com/repowazdogz-droid/commons-agent-lab)**: a pre-registered study of whether LLM agents produce the collective failure that per-agent rules permit. 2,100 model episodes across three models, 30 per cell, plus 120 scripted control episodes, scored mechanically from the environment ledger; results in RESULTS.md recompute offline from `results/_canonical`. The pre-registration commit precedes the first data; four amendments each precede their data; deviations are logged.

**[proof-carrying-evals](https://github.com/repowazdogz-droid/proof-carrying-evals)**: governance properties of agent decisions routed to the checker whose logic fits (Z3 for one decision, Lean 4 for a whole trace, TLA+ for interleavings, CryptoVerif for authorisation), with the LLM judge's score sealed beside the proof. The judge is a 14B local model and sometimes grades its own output; both caveats are on the first screen.

**[evidence-audit](https://github.com/repowazdogz-droid/evidence-audit)**: a grader for recorded verification outputs (Kani, loom, cargo test, Lean) that reports what a run explored rather than the verdict it printed. Three catches on real crates (`jsonwebtoken`, `governor`) and one on a Lean model of a kernel Rust parser. It does not run any verifier itself.

## Formal methods

[collective-bound](https://github.com/repowazdogz-droid/collective-bound) is the formal core behind the collective-bound result: six Lean 4 theorems with no axioms over closed data, eleven sealed Z3 verdicts with witnesses, a 180,000-episode learning adversary, and negative controls, all regenerating byte for byte. It is the reproduction surface for [omegaprotocol.org/collective/](https://www.omegaprotocol.org/collective/), where the same result is presented with its live-agent experiment and exact denominators.

[capctl-iris](https://github.com/repowazdogz-droid/capctl-iris) is the deepest proof development here: a Rocq 9.2 / Iris 4.5 development of a concurrent capability meter, 40 theorems closed under the global context, including a logically atomic specification and safety under arbitrary interleavings, with the `Print Assumptions` output committed and diffed in CI. DOI [10.5281/zenodo.21505165](https://doi.org/10.5281/zenodo.21505165). It also carries a TLA+ model of the check-then-commit race the proof rules out.

Related: [escrow-budget](https://github.com/repowazdogz-droid/escrow-budget) (Lean 4 aggregate-spend bound under message loss and crash recovery, two proved negative controls, and a commit log that records a pre-registered prediction scored wrong); [vsf-cjson](https://github.com/repowazdogz-droid/vsf-cjson) (cJSON re-implemented in Lean 4 with zero `sorry`, differential-tested against the C original, where the requested round-trip property turned out to be false of cJSON itself); [compositional-temporal-safety](https://github.com/repowazdogz-droid/compositional-temporal-safety) (machine-checked assume-guarantee composition with four proved negative controls).

## Defects found in other people's systems

Issues I reported that maintainers fixed and shipped. Links go to the fix, not to my report.

- [LemmaScript](https://github.com/midspiral/LemmaScript): every cross-file extern was modelled as a deterministic function, so two calls to a random source proved equal. Fixed the next day in [#207](https://github.com/midspiral/LemmaScript/pull/207) and released in v0.6.1.
- [inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai): `completed_samples` depended on scorer declaration order after scorer errors. Fixed in [#4604](https://github.com/UKGovernmentBEIS/inspect_ai/pull/4604), merged.
- [inspect-robots](https://github.com/robocurve/inspect-robots): the persisted log could not distinguish an embodiment-adopted verdict from a VLM-sampled one. Fixed in [#422](https://github.com/robocurve/inspect-robots/pull/422), merged.
- [labs-OO-Agents](https://github.com/NVIDIA-NeMo/labs-OO-Agents): generator-bodied agent methods ended their span at generator creation. Fixed in [#120](https://github.com/NVIDIA-NeMo/labs-OO-Agents/pull/120), merged.
- [SkillSpector](https://github.com/NVIDIA/SkillSpector): structured-output schemas with numeric bounds were rejected by the Anthropic provider. Fixed in [#85](https://github.com/NVIDIA/SkillSpector/pull/85), merged.

A pull request of mine that was merged: a SymbiYosys proof for the ECC encoder and decoder in [common_cells](https://github.com/pulp-platform/common_cells/pull/355) (3 September), during which the proof surfaced that `cc_ecc_decode` declared `syndrome_o` and never drove it; the same PR fixes that. Pull requests of mine that are open and unmerged: a typed-expression differential-testing target for [cedar-spec](https://github.com/cedar-policy/cedar-spec/pull/995) (a maintainer requested changes on 28 July; I addressed the review comments on 24 August, there has been no maintainer response since, and the branch now conflicts with main) and a fix for polarity caching of `sep.emp` reductions in [cvc5](https://github.com/cvc5/cvc5/pull/12937) (approved by a maintainer on 21 September; I resolved conflicts and formatting on 24 September; not yet merged).

## How claims are graded here

Every repository states its result with a tier: proven (a kernel or solver accepted it), measured (a script recomputes it from committed evidence), observed (it happened on this machine on this date), or not established. Every check is shown able to fail before its pass is counted. A PASS from any tool here means "no checked failure found", not "correct".

## Contact

warrensmith8@ymail.com; for Omega Protocol work, omegaprotocol87@gmail.com (the address on the site). Site: [omegaprotocol.org](https://omegaprotocol.org).
