# Warren Smith

Research engineer in Bristol, UK. I build small, well-tested tools for AI
evaluation and software integrity, and I formalise the parts that need to be
provably correct. I try to keep my claims honest: my tools state plainly what
they do and do not guarantee.

## Start here

**Evaluation integrity** — tools and evals that check whether an evaluation result
means what it claims.

- **[inspect-replay](https://github.com/repowazdogz-droid/inspect-replay)** —
  deterministic, sample-aligned comparison of two [Inspect](https://inspect.aisi.org.uk)
  `.eval` logs. It reports what changed in configuration, metrics, samples, and
  errors between two runs, and is careful about the difference between "unchanged"
  and "we cannot tell". Typed, 117 tests, CI, explicit assurance boundary.

- **[inspect-audit](https://github.com/repowazdogz-droid/inspect-audit)** —
  a read-only auditor for a single Inspect `.eval` log. It flags silent validity
  failures that make a result look clean while being wrong: samples dropped from a
  metric's denominator, a grader that graded nothing, a model grading its own output.

- **[case-notes-eval](https://github.com/repowazdogz-droid/case-notes-eval)** —
  an Inspect evaluation with a deterministic grader and a rubric committed before
  the first model call. An adversarial condition tests the validator itself, not
  only the model: whether a note can pass a lexical safeguarding checker while still
  carrying the judgement to a human reader. A study of construct validity.

**Security and formal verification.**

- **[mcp-boundary-audit](https://github.com/repowazdogz-droid/mcp-boundary-audit)** —
  a harness that detects one specific authorization bug in
  [MCP](https://modelcontextprotocol.io) servers: a tool hidden from `tools/list`
  that is still reachable through `tools/call`. Ships a bundled mock server so a
  fresh clone reproduces the finding with no network.

- **[omega-lean-proof](https://github.com/repowazdogz-droid/omega-lean-proof)** —
  a machine-checked Lean 4 proof that a canonical-encoding, hash-linked record chain
  is tamper-evident, using only Lean's standard axioms and no Mathlib. A CI workflow
  re-derives the result from a clean checkout on a pinned toolchain.

- **[semdiff](https://github.com/repowazdogz-droid/semdiff)** —
  a Rust CLI for semantic diffs of high-risk artifacts (lockfiles, API specs,
  configs). It answers "is this safe to merge?" when a line-level diff is too noisy
  or too quiet.

## What I work on

AI evaluation integrity, formal verification (Lean 4), and the security and
supply-chain side of engineering. I am interested in AI safety and security
engineering roles.
