# SuperInstance

![AI Sonar Analysis — a small model reading sonar off the Gulf of Maine](https://github.com/SuperInstance/.github/raw/main/profile/sonar-ai-poc.jpg)

> **A fishing boat, a hermit crab, and a small model reading sonar at three in the morning. That is the org.**

---

A **pod** is not a **pack**. A pack runs a dominance hierarchy; a pod runs kin-tracked consensus. The word is the architecture. SuperInstance is organized the same way — not a swarm (mindless, emergent-only) and not a hive (one queen, many bodies) but a **fleet**: independent hulls, shared weather, one captain. ~4,098 repos that abandon shells that no longer fit and keep the ones that do.

**Two motifs. One conservation law.**

- 🦀 **The hermit crab** — every repo is a shell. Soft animal, borrowed armor, serial homes. The commits outlive the body.
- ⛵ **The 12V fishing boat** — edge-first. Wattage is the architecture, the ocean is the deploy target, and nothing gets an outlet.
- ⚖️ **γ + η = C** — useful work + entropy = fixed budget. [FLUX](https://github.com/SuperInstance/flux-core) enforces it at the bytecode level, not as policy. A fishing ground, not a farm: take what regenerates.

---

## Start in 30 seconds

```bash
pip install conservation-enforcer          # Python: the policy layer
cargo add fluxvm                            # Rust: the VM
gh repo clone SuperInstance/AI-Writings     # the corpus
```

The first two install in under a minute. The third is ~1,800 markdown files — start with [ON_THE_12V_BOAT.md](https://github.com/SuperInstance/AI-Writings/blob/main/ON_THE_12V_BOAT.md).

---

## The fleet

**The engine room** — what runs.

| Repo | One-liner |
|---|---|
| [flux-core](https://github.com/SuperInstance/flux-core) | Register-based bytecode VM, 3 implementations, byte-identical |
| [plato-engine-block-c](https://github.com/SuperInstance/plato-engine-block-c) | Constraint engine, 5 impls at 9–10/10 conformance |
| [conservation-enforcer](https://github.com/SuperInstance/conservation-enforcer) · [-rs](https://github.com/SuperInstance/conservation-enforcer-rs) | Policy layer for LLM outputs, two languages |
| [flux-policy-tester](https://github.com/SuperInstance/flux-policy-tester) | Fuzz the policies |
| [si-exocortex-rs](https://github.com/SuperInstance/si-exocortex-rs) | Agent framework with conservation awareness |

**The wheelhouse** — who steers. A kennel stores dogs; this is a working team:

| Repo | One-liner |
|---|---|
| [shepherds-console](https://github.com/SuperInstance/shepherds-console) | Ops dashboard — where are the dogs |
| [breed-registry](https://github.com/SuperInstance/breed-registry) | Model selection — which bloodline for which job |
| [lineage-tracker](https://github.com/SuperInstance/lineage-tracker) | Fine-tune provenance — which dog came from which |

**The crow's nest** — what we see with:

| Repo | One-liner |
|---|---|
| [search-superinstance-ai](https://github.com/SuperInstance/search-superinstance-ai) | Semantic search across 4,098 repos |
| [ship-log-search](https://github.com/SuperInstance/ship-log-search) | The boat's logbook — D1 + Vectorize + Pages |
| [AI-Writings](https://github.com/SuperInstance/AI-Writings) | The 1,800 essays — the *reasons*. Not documentation *of* the thing; the lasting truth of it. |

> **One-liner:** clone 3, run one, read one — you've got the spine.

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

## The 6 conservation laws, in one line each

1. **Energy** — every component runs under a measurable wattage budget.
2. **γ + η = C** — useful work + entropy = fixed budget, enforced by softmax.
3. **Attention** — total attention weight in any transformer sums to 1.
4. **Action-rate** — an agent may take at most N actions per window; the runtime denies N+1.
5. **Information-throughput** — bounded output per interaction; structured tiles fit the wire.
6. **Presence** — the diary is a presence-battery that discharges with each reading.

---

*Updated 2026-08-24 — v3*
