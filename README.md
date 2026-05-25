# OMEGA Lab

Research engineering for **accountable, replayable, provenance-bound** machine systems.

This profile hosts the public trunk of that work: formal predicates, shared record schemas, pre-runtime assurance, hash-chained decision traces, and authority/materiality boundary records. It is not a chatbot product or a generic AI startup surface.

**Site:** [omegaprotocol.org](https://omegaprotocol.org)

---

## Start here

| If you want to… | Repository |
| --- | --- |
| Check spec drift before runtime | [specgap](https://github.com/repowazdogz-droid/specgap) |
| Reproduce the formal `Governed` model | [omega-lean-proof](https://github.com/repowazdogz-droid/omega-lean-proof) |
| Integrate governed evidence records | [omega-contracts](https://github.com/repowazdogz-droid/omega-contracts) |
| Inspect replayable agent decision traces | [clearpath](https://github.com/repowazdogz-droid/clearpath) |
| Compare authorization vs execution | [consent-ledger](https://github.com/repowazdogz-droid/consent-ledger) |
| Surface load-bearing assumptions | [assumption-registry](https://github.com/repowazdogz-droid/assumption-registry) |

---

## Lab layers (public trunk)

| Layer | Role | Entry |
| --- | --- | --- |
| **Assurance** | Evidence before runtime — spec implication checks, triangulation | [specgap](https://github.com/repowazdogz-droid/specgap) |
| **Doctrine** | Lean 4 predicates for governed systems (shipped roots, zero `sorry`) | [omega-lean-proof](https://github.com/repowazdogz-droid/omega-lean-proof) |
| **Substrate** | `OmegaRecord` schemas and conformance for cross-library evidence | [omega-contracts](https://github.com/repowazdogz-droid/omega-contracts) |
| **Replay** | Tamper-evident traces with faithfulness states | [clearpath](https://github.com/repowazdogz-droid/clearpath) |
| **Authority** | Authorisation vs action boundary records | [consent-ledger](https://github.com/repowazdogz-droid/consent-ledger) |
| **Materiality** | Load-bearing assumptions and pre-action review reports | [assumption-registry](https://github.com/repowazdogz-droid/assumption-registry) |

Stack map: [omega-contracts TRUST_STACK](https://github.com/repowazdogz-droid/omega-contracts/blob/main/docs/TRUST_STACK.md)

---

## Terminology (public stack)

| Term | Meaning in this stack |
| --- | --- |
| **Replay** | Re-export / re-verify recorded structure, not re-prove world truth |
| **Verification** | Chain, schema, or conformance check unless explicitly tied to an external verification workflow |
| **HELD / HOLD** | Record encoding or operator-review recommendation — not an autonomous stop |
| **Faithfulness** | Annotated label on trace nodes, not verified cognition |
| **Governance** | Record shape and integrator claims, not organizational approval |

---

## Operating principles

- Bounded claims over bold claims
- Evidence before runtime evaluation
- HELD evaluations are first-class records, not silent failures
- Disagreement preserved where independent evaluators diverge

---

## Integrate

```bash
npm install @omega-protocol/contracts
```

Formal reproduction:

```bash
git clone https://github.com/repowazdogz-droid/omega-lean-proof.git
cd omega-lean-proof && lake build
```

Spec assurance quickstart:

```bash
git clone https://github.com/repowazdogz-droid/specgap.git
cd specgap && python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m specgap.cli examples/sandbox_no_network.json --out reports/demo_report.md
```

---

## What this is not

- A collection of unrelated hackathon demos
- An autonomous agent product
- A substitute for domain-specific professional judgment

Questions on specification, proof reproduction, or schema PRs: see [omegaprotocol.org](https://omegaprotocol.org).
