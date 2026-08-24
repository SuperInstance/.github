# SuperInstance

![AI Sonar Analysis — a small model reading sonar off the Gulf of Maine](https://github.com/SuperInstance/.github/raw/main/profile/sonar-ai-poc.jpg)

> **A fishing boat, a hermit crab, and a small model reading sonar at three in the morning. That is the org.**

---

A **pod** is not a **pack**. A pack runs a dominance hierarchy; a pod runs kin-tracked consensus. The word is the architecture. SuperInstance is organized the same way — not a swarm (mindless, emergent-only) and not a hive (one queen, many bodies) but a **fleet**: independent hulls, shared weather, one captain. 4,357 repos that abandon shells that no longer fit and keep the ones that do.

**Two motifs. One conservation law.**

- 🦀 **The hermit crab** — every repo is a shell. Soft animal, borrowed armor, serial homes.
- ⛵ **The 12V fishing boat** — edge-first. Wattage is the architecture.
- ⚖️ **γ + η = C** — useful work + entropy = fixed budget. [FLUX](https://github.com/SuperInstance/flux-core) measures and enforces it in the bytecode validator, not as after-the-fact policy.

**MIT licensed.** The engine-room repos carry the license surface — the rest inherit the shipyard's standards. Want aboard? [CONTRIBUTING.md](https://github.com/SuperInstance/SuperInstance/blob/main/CONTRIBUTING.md) and [GOOD_FIRST_ISSUES.md](https://github.com/SuperInstance/SuperInstance/blob/main/GOOD_FIRST_ISSUES.md) — issues are open on the flagship repos.

---

## Start in 30 seconds

```bash
pip install conservation-enforcer     # the policy layer ([PyPI](https://pypi.org/project/conservation-enforcer/))
cargo add fluxvm                      # the VM ([crates.io](https://crates.io/crates/fluxvm))
```

Then wrap any LLM call:

```python
from conservation_enforcer import ConservationEnforcer, combined_policy

enforcer = ConservationEnforcer(combined_policy(max_tokens=500), budget=500)
result = enforcer.enforce(llm_response)   # violation → rejected, with audit trail
```

Or go straight to the corpus: [AI-Writings](https://github.com/SuperInstance/AI-Writings) — ~1,800 markdown files. Start with [ON_THE_12V_BOAT.md](https://github.com/SuperInstance/AI-Writings/blob/master/ON_THE_12V_BOAT.md).

---

## The fleet

**The engine room** — what runs.

| Repo | One-liner |
|---|---|
| [flux-core](https://github.com/SuperInstance/flux-core) | Register-based bytecode VM — Py / Rust / JS, byte-identical |
| [plato-engine-block-c](https://github.com/SuperInstance/plato-engine-block-c) | Constraint engine — C / Rust / Elixir / Zig / Py, 5 impls |
| [conservation-enforcer](https://github.com/SuperInstance/conservation-enforcer) · [-rs](https://github.com/SuperInstance/conservation-enforcer-rs) | Policy layer for LLM outputs, two languages |
| [flux-policy-tester](https://github.com/SuperInstance/flux-policy-tester) | Fuzz the policies |
| [si-exocortex-rs](https://github.com/SuperInstance/si-exocortex-rs) | Agent framework with conservation awareness |

**The wheelhouse** — who steers. Working dogs on a working boat: the kennel is where they sleep, the deck is where they matter.

| Repo | One-liner |
|---|---|
| [shepherds-console](https://github.com/SuperInstance/shepherds-console) | Ops dashboard — where are the dogs |
| [breed-registry](https://github.com/SuperInstance/breed-registry) | Model selection — which bloodline for which job |
| [lineage-tracker](https://github.com/SuperInstance/lineage-tracker) | Fine-tune provenance — which dog came from which |

**The crow's nest** — what we see with:

| Repo | One-liner |
|---|---|
| [search-superinstance-ai](https://github.com/SuperInstance/search-superinstance-ai) | Semantic search across the org |
| [ship-log-search](https://github.com/SuperInstance/ship-log-search) | The boat's logbook — D1 + Vectorize + Pages |
| [AI-Writings](https://github.com/SuperInstance/AI-Writings) | The 1,800 essays — the *reasons*. Not documentation *of* the thing; the lasting truth of it. |

---

## Read more

- 📖 [Canonical README](https://github.com/SuperInstance/SuperInstance/blob/main/README.md) — the full guide
- 🦀 [HERMIT_CRAB_MANIFESTO](https://github.com/SuperInstance/SuperInstance/blob/main/docs/v2/HERMIT_CRAB_MANIFESTO.md) — the one-paragraph distillation
- 🗺️ [ORG_MAP](https://github.com/SuperInstance/SuperInstance/blob/main/docs/v2/ORG_MAP.md) — structural topology + surfaced risks
- 🔧 [RUST_PORT_QUEUE](https://github.com/SuperInstance/SuperInstance/blob/main/docs/v2/RUST_PORT_QUEUE.md) — next three Rust ports to ship
- 📚 [PACKAGES.md](https://github.com/SuperInstance/SuperInstance/blob/main/PACKAGES.md) — full taxonomy
- 🦀 [THE_HERMIT_CRAB_AND_THE_WORKING_DOG](https://github.com/SuperInstance/SuperInstance/blob/main/THE_HERMIT_CRAB_AND_THE_WORKING_DOG.md) — the two animals, one essay
- 🥚 [THE_EGG_AND_THE_ORGANISM](https://github.com/SuperInstance/SuperInstance/blob/main/THE_EGG_AND_THE_ORGANISM.md) — what hatches from a repo

---

## The conservation laws

Six of them — energy budgets, action-rate caps, attention sums, information throughput, presence. Each is enforced in code, not in vibes; the FAQ on what breaks when each is violated lives in [the canonical README](https://github.com/SuperInstance/SuperInstance/blob/main/README.md). γ + η = C is the one that started it all: the budget is fixed, spend it on useful work or lose it to entropy.

> **The spine:** install one, run it, then read one. You've got the fleet.

---

*Updated 2026-08-24 — v4*
