# Warren Smith

Research engineer in Bristol, UK. I build small, well-tested tools for AI
evaluation and software integrity, and I machine-check the parts that need to be
provably correct. I try to keep claims exactly as wide as the evidence: each
repository states plainly what it does and does not establish.

These six are distinct pieces of work, not one integrated system.

## Formal verification

- **[capctl-iris](https://github.com/repowazdogz-droid/capctl-iris)** — a
  machine-checked proof, in Rocq/Iris, that a shared capability meter never exceeds
  its cap.
  - Result (PROVEN): safety holds across *all* thread interleavings, as a closed
    HeapLang adequacy theorem.
  - Evidence: the Rocq kernel checks every proof, and an assumptions audit reports
    each audited theorem as axiom-free ("Closed under the global context").
  - Limitation: the theorem concerns a HeapLang model of a meter, not a deployed
    runtime.

- **[escrow-budget](https://github.com/repowazdogz-droid/escrow-budget)** — a
  distributed budget protocol proved to keep aggregate authorised spend within a
  global cap under message loss and disciplined crash/recovery.
  - Result (PROVEN): the aggregate bound holds for arbitrary finite replica and
    transfer sets (Lean 4), with proved negative controls showing each discipline
    hypothesis is necessary.
  - Evidence: Lean build plus an axiom audit (headline theorems depend only on
    `[propext, Quot.sound]`); TLA+ and property tests are separate, non-authoritative
    checks.
  - Limitation: there is no machine-checked refinement linking the Lean theorem, the
    TLA+ model, and the Python model; the Lean crash model is global while the
    TLA+/property crash model is per-replica.

- **[vsf-cjson](https://github.com/repowazdogz-droid/vsf-cjson)** — an instrumented
  study of where AI-assisted formalization breaks: a real C JSON parser (cJSON)
  re-implemented in Lean 4 and proved against a formal grammar.
  - Result (PROVEN against the grammar; MEASURED for C agreement): the Lean port's
    totality, round-trip, idempotence, and canonicity are kernel-checked, and
    differential testing found four genuine cJSON bugs.
  - Evidence: an axiom gate plus a mutation suite that proves every assurance gate
    can actually fail.
  - Limitation: adequacy is against a handwritten grammar, not RFC 8259 conformance,
    and it does not prove equivalence to cJSON.

## AI evaluation integrity

- **[inspect-replay](https://github.com/repowazdogz-droid/inspect-replay)** — a
  deterministic, sample-aligned comparison of two [Inspect](https://inspect.aisi.org.uk)
  evaluation logs.
  - Result: it reports what changed across configuration, metrics, and samples,
    keeping "unchanged" separate from "cannot determine".
  - Evidence: 117 tests and CI, including a build-time guard that fails the build if
    the tool's own prose asserts causation.
  - Limitation: it compares recorded state, it does not re-run models, and it leaves
    statistical testing out of scope.

- **[inspect-audit](https://github.com/repowazdogz-droid/inspect-audit)** — a
  read-only validity auditor for a single Inspect `.eval` log.
  - Result (OBSERVED): it flags silent validity failures (samples dropped from a
    metric denominator, a grader that scored nothing, a model grading its own output,
    invalid scores) with concrete evidence paths.
  - Evidence: 58 tests and CI; the bundled broken example reproduces a FAIL verdict.
  - Limitation: PASS means "no checked failure found", not "valid"; it shares subject
    matter with inspect-replay but answers a different question (audit one run versus
    diff two).

## Security engineering

- **[mcp-boundary-audit](https://github.com/repowazdogz-droid/mcp-boundary-audit)** —
  a harness that detects one specific [MCP](https://modelcontextprotocol.io)
  authorization bug: a tool hidden from `tools/list` that is still reachable through
  `tools/call`.
  - Result (OBSERVED): against the bundled mock it returns FAIL when hidden tools
    execute and PASS when they are refused.
  - Evidence: it actively issues the real `tools/call` and records hashable evidence;
    11 tests and CI.
  - Limitation: it probes operator-named tools rather than discovering unknown tool
    names, and validation is currently against the bundled mock, not a third-party
    deployment.

## Promotion candidate

**[evaltrust](https://github.com/repowazdogz-droid/evaltrust)** — a reliability
benchmark for agent *evaluation* rather than agent capability. Its `evaltrust`
console command now works, and a CI check recomputes the committed result
byte-identically. It is a candidate to replace inspect-audit once that CI is green
on GitHub. Its numbers are small-N and single-annotator, by its own statement.

## What I work on

AI evaluation integrity, formal verification (Lean 4, Rocq/Iris), and the security
and supply-chain side of engineering. I am interested in AI safety and security
engineering roles.
