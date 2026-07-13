# Warren Smith

Research engineer in Bristol, UK. I build small, well-tested tools for AI
evaluation and software integrity, and I formalise the parts that need to be
provably correct. I try to keep my claims honest: my tools state plainly what
they do and do not guarantee.

## Start here

- **[inspect-audit](https://github.com/repowazdogz-droid/inspect-audit)** —
  a read-only auditor for [Inspect](https://github.com/UKGovernmentBEIS/inspect_ai)
  `.eval` evaluation logs. It flags silent validity failures that make a result
  look clean while being wrong: samples dropped from a metric's denominator, a
  grader that graded nothing, a model grading its own output. Python, tested,
  CI, with an explicit assurance boundary.

- **[semdiff](https://github.com/repowazdogz-droid/semdiff)** —
  a Rust CLI for semantic diffs of high-risk artifacts (lockfiles, API specs,
  configs). It answers "is this safe to merge?" when a line-level diff is too
  noisy or too quiet.

- **[omega-lean-proof](https://github.com/repowazdogz-droid/omega-lean-proof)** —
  a Lean 4 formalisation of governance predicates for AI decision records. A CI
  workflow re-derives the result from a clean checkout; the README accounts
  precisely for what is proven, what is assumed, and what is still open.

## What I work on

AI evaluation tooling, formal methods (Lean 4), and the integrity and
supply-chain side of engineering. I am interested in AI safety and security
engineering roles.
