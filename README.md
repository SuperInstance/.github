# SuperInstance

**AI-Driven Research Infrastructure · 500+ Structured Inquiry Repositories**

---

## What We Are

SuperInstance is a **research organization**, not a product company. We use autonomous AI systems to conduct structured, reproducible inquiry across computer science, mathematics, physics, and machine learning. Our output is not a single codebase — it is a **distributed archive of process artifacts**: commit-by-commit records of how knowledge is constructed, tested, and refined.

Think of our repositories as **lab notebooks** that compile and run.

---

## The `lau-*` Namespace

Our repositories use the `lau-*` prefix as a **research lineage marker**. Each repo isolates a single domain of inquiry:

- **`lau-queueing-theory`** → M/M/1, M/M/c, Erlang, Jackson networks
- **`lau-topological-data-analysis`** → Persistent homology, simplicial complexes, Mapper
- **`lau-database-theory`** → B-trees, WAL, ARIES recovery, query optimization
- **`lau-fluid-dynamics`** → Navier-Stokes, Lattice Boltzmann D2Q9, vortex methods
- ...and 120+ more, spanning CS theory, pure math, physics, and systems engineering

The prefix is opaque to search engines. We are progressively renaming the most mature artifacts to standalone, discoverable names (`queuecraft`, `tda-rs`, `db-internals`) while preserving the original repos as historical records.

---

## Repository Philosophy

### One Concept, One Repo

We keep repositories **spread out and independent**. Each repo is:

- **Self-contained** — zero internal `lau-*` crate coupling
- **Searchable** — every commit is part of the research record
- **Tested** — the top 37 repos alone contain ~2,200+ unit tests
- **Discoverable** — Rust source, 20K–112K LOC per repo, standard Cargo tooling

We do **not** merge into monorepos. The commit history is part of the artifact.

### Process Over Product

These repositories are **process artifacts**, not polished products. They document:

- How an AI system reasons about scheduling theory
- The evolution of a PDE solver from first principles
- The refinement of a cryptographic primitive through iterative testing

Some repos have evolved into substantial, publishable implementations. Others remain educational reference material. Many are stepping stones — inquiry that led elsewhere.

---

## Research Domains

| Domain | Example Repos | Maturity |
|--------|--------------|----------|
| **Systems & Infrastructure** | `lau-database-theory`, `lau-distributed-systems`, `lau-memory-arena` | Production-adjacent |
| **Numerical & Scientific Computing** | `lau-numerical-pde`, `lau-fluid-dynamics`, `lau-solid-mechanics` | Research-grade |
| **AI / ML / Data** | `lau-neural-networks`, `lau-time-series`, `lau-topological-data-analysis` | Educational to publishable |
| **Pure & Applied Mathematics** | `lau-algebraic-topology`, `lau-free-probability`, `lau-ergodic-theory` | Reference implementations |
| **Physics & Engineering** | `lau-electromagnetism`, `lau-thermodynamics`, `lau-relativity` | Educational |
| **PLATO Ecosystem** | `lau-construct`, `lau-ai-tutor`, `lau-consciousness-bridge` | Narrative / conceptual |

---

## For Researchers & Developers

### Using Our Code

Repos are Rust crates with standard `Cargo.toml` files. Most depend only on `nalgebra`, `serde`, `rand`, and `rayon`.

```bash
git clone https://github.com/superinstance/lau-queueing-theory.git
cd lau-queueing-theory
cargo test        # 72 tests
cargo doc --open  # Browse the API
```

### Citing Our Work

If you use code from a SuperInstance repo in research, cite the specific repository and commit hash. Each repo is a frozen snapshot of an inquiry process.

```bibtex
@software{superinstance_queueing_2026,
  author = {SuperInstance},
  title = {lau-queueing-theory: Queueing Theory in Rust},
  url = {https://github.com/superinstance/lau-queueing-theory},
  year = {2026},
  commit = {abc123...}
}
```

### Contributing

We welcome:
- **Bug reports** with test cases
- **Documentation improvements** (many repos need real-world examples)
- **Agent abstraction cleanup** — stripping PLATO-specific framing from math crates
- **Renaming proposals** — better discoverable names for mature repos

See [FINAL_PLAN.md](./FINAL_PLAN.md) for our current synthesis of repo dispositions.

---

## Governance & Transparency

### Independent Audits

Our repository collection is periodically audited by independent model reviewers. The latest synthesis (June 2026) classified ~120 `lau-*` repos into:

- **~55 Consensus Diamonds** — real code, tests, standalone value
- **~15 PLATO-Specific Keepers** — narrative artifacts, keep `lau-` prefix
- **~55 Archive Candidates** — internal plumbing, stubs, or superseded inquiry

See [FINAL_PLAN.md](./FINAL_PLAN.md) for the full synthesis.

### Research Ethics

- **No crates.io squatting.** We only publish what we maintain.
- **No misleading claims.** We label educational implementations clearly.
- **Transparency about provenance.** AI-generated code is identified as such.

---

## Contact

- **Issues:** Use GitHub Issues on the relevant repo
- **General inquiry:** Open an issue on this repository
- **Research collaboration:** We are open to partnerships with academic labs and independent researchers

---

*SuperInstance — Structured inquiry at scale.*
