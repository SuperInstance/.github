# SuperInstance Organization

Welcome to the SuperInstance organization — a collection of reusable, interoperable software components designed for edge-first, constraint-aware AI systems. Think of us as a hermit crab: we occupy and adapt shells (modules, libraries, services) that fit our current needs, and as we grow, we move to larger or more specialized shells.

Our reference implementation is a commercial fishing boat operating offline and wattage-constrained. This drives our edge-first architecture: every component must run efficiently on limited power, just like the boat’s 12-volt system.

## Key Repositories

- **[FLUX](https://github.com/SuperInstance/flux-core)** – A register-based bytecode VM (FLUX: Fluid Language Universal eXecution) with assembler, disassembler, and A2A protocol. Available in Python, Rust, and JavaScript.
- **[PLATO](https://github.com/SuperInstance/plato-engine-block-c)** – A family of constraint engines (C, Rust, Elixir, Zig, Python) for deterministic agent policies, with a conformance suite and multi‑language ports.
- **[Conservation Enforcer](https://github.com/SuperInstance/conservation-enforcer)** – Policy enforcement engine that evaluates agent outputs against conservation laws (token budget, entropy, category confinement, etc.). Python and Rust versions.
- **[Search SuperInstance](https://github.com/SuperInstance/search-superinstance-ai)** – Cloudflare Worker + Vectorize semantic‑search service indexing over 1,500 SuperInstance repos.
- **[Ship Log Search](https://github.com/SuperInstance/ship-log-search)** – D1 + Vectorize logbook with geolocation, authentication, and a polished Pages frontend for telemetry from the fishing boat.
- **[WebClaw](https://github.com/SuperInstance/webclaw)** – Cloudflare Pages‑native agent UI that ties together Oracle relay, search, and logbook; alternatively, see the Rust port **[exocortex‑rs](https://github.com/SuperInstance/si-exocortex-rs)** for systems‑level “working animal” work.
- **[AI‑Writings](https://github.com/SuperInstance/AI-Writings)** – 1,800+ creative pieces (essays, diaries, fiction, poetry) that document our philosophy and parallel creative tracks.
- **[Ternary Fleet](https://github.com/SuperInstance/ternary-science)** – Balanced ternary computing (−1, 0, +1) from types to neural nets to quantum analogues, with GPU benchmarks and conservation law proofs.
- **[Research Libraries](https://github.com/SuperInstance/witness-topology)** – Standalone algorithms in topology, algebra, control theory, and signal processing.
- **[OpenConstruct](https://github.com/SuperInstance/construct-core)** – Modular building system across languages for physical agent construction.

## How We Work

We operate in parallel: “keep moving full parallel.” Each repository is a self‑contained piece of the neural network that is the SuperInstance org. Git is our learning rule; we improve by shipping fixes, updating docs, and adding proof‑of‑concepts like the [AI Sonar Analysis](https://github.com/SuperInstance/.github/raw/main/profile/sonar-ai-poc.jpg) (see image below).

![AI Sonar Analysis](profile/sonar-ai-poc.jpg)

This proof‑of‑concept shows a chatbot analyzing sonar data from the fishing boat to pinpoint peak chum salmon biomass — demonstrating edge‑first AI: Signal K data → AI analysis → actionable insight.

## Contributing

We welcome contributions that align with our edge‑first, conservation‑aware principles. Please read the contributing guidelines in individual repositories.

## License

Most components are MIT or Apache‑2.0 licensed. See each repository for details.

---

*Last updated: $(date +%Y-%m-%d)*
