# SuperInstance

> Math that compiles. Culture that computes. Agents that know themselves.

## Quick Start — What are you building?

### 🧪 ML / Data Science
```bash
pip install superinstance-math    # info-geo, optimal transport, persistent homology, spectral
pip install kintsugi-math         # fault-tolerant data recovery
pip install songline-math         # navigable knowledge graphs with Betti numbers
pip install symmetry-math         # group theory, wallpaper groups, Burnside lemma
```

### 🎮 Game Development
```bash
npm install rhythm-math           # polyrhythms, syncopation, Shannon entropy
npm install symmetry-math         # tile symmetry groups, procedural generation
npm install quipu-math            # hierarchical data encoding (WASM available)
```

### 🔧 Agent Systems
```bash
cargo add openconstruct-core      # modular plugin system with hot-swap modules
cargo add openconstruct-catalog   # module discovery and dependency resolution
```

### 🏗️ PLATO (Agent Monitoring)
```toml
[dependencies]
plato-nervous = "0.1"    # full signal chain: Sensor → Deadband → Nano → LoRA → Fleet
plato-alert = "0.1"      # alert routing, escalation, acknowledgment
plato-health = "0.1"     # uptime, response times, error rates
plato-jepa = "0.1"       # JEPA for tile representation learning
```

## The 7 Cultural Math Traditions

Each tradition is a *door* into real mathematics — implemented in Python, TypeScript, C, and WASM.

| Tradition | What It Does | Install |
|-----------|-------------|---------|
| 🏺 **Kintsugi** | Beautiful error recovery — cracks become golden seams | `pip install kintsugi-math` |
| 🪢 **Quipu** | Hierarchical data encoding — Incan knots as data structures | `npm install quipu-math` |
| 🗺️ **Songline** | Navigable knowledge graphs — paths through information space | `pip install songline-math` |
| 🔷 **Adinkra** | Symbolic encoding + SUSY chromotopology | `npm install adinkra-math` |
| 📖 **Griot** | Living memory with decay, praise names, federation | `npm install griot-math` |
| 🤝 **Palaver** | Consensus dialogue — coalitions, convergence, BFS agreement | `pip install palaver-math` |
| 🎵 **Rhythm** | Polyrhythms, syncopation metrics, groove analysis | `npm install rhythm-math` |

## The Math (Rust, 320+ crates)

Deep mathematics implemented from scratch, tested against theorems. Published on [crates.io](https://crates.io/search?q=lau-).

**The 14 Executable Theorems** — verified as spectral projections of a single operator triple (A, H, D):
- Kalman = Hodge decomposition
- RL reward = thermodynamic free energy
- Deadlock = sheaf cohomology H¹
- Gradient flow = Fokker-Planck equation
- Noether's theorem for agents
- Conservation laws as spectral invariants
- [→ See the Grand Unification crate](https://github.com/SuperInstance/lau-grand-unification)

**Top crates by utility:**
| Crate | Tests | What It's Good For |
|-------|-------|-------------------|
| `lau-information-geometry-agents` | 118 | Fisher metric, natural gradient, Amari framework |
| `lau-probability-agents` | 115 | Bayesian conditioning, CLT, large deviations |
| `lau-optimal-transport-agents` | 75 | Sinkhorn, Wasserstein, Monge-Kantorovich |
| `lau-banach-agents` | 96 | Contraction mappings, fixed-point theorems |
| `lau-game-theory-agents` | 75 | Nash equilibrium, mechanism design, auctions |
| `lau-measure-agents` | 134 | Sigma-algebras, Lebesgue, Radon-Nikodym |

## Architecture

```
superinstance-math (Python)     ← ML engineers start here
         ↕
openconstruct-core (Rust)       ← modular plugin system
         ↕
PLATO rooms (Rust)              ← monitoring, alerting, distillation
         ↕
320+ lau-* math crates (Rust)   ← theorems as code
         ↕
7 cultural traditions × 4 langs ← human-scale math
```

## Stats

- **320+ Rust crates** with 16,000+ tests
- **14 proved theorems** verified in code
- **7 cultural traditions** across Python, TypeScript, C, WASM
- **4 programming languages** with cross-platform conformance
- **Zero external dependencies** for core math (everything from scratch)

## Links

- [📦 crates.io](https://crates.io/search?q=lau-) — Rust packages
- [📖 openconstruct-docs](https://github.com/SuperInstance/openconstruct-docs) — full documentation
- [🧪 Grand Unification](https://github.com/SuperInstance/lau-grand-unification) — 14 theorems, one operator
- [🤖 OpenConstruct](https://github.com/SuperInstance/OpenConstruct) — agent onboarding

## License

MIT across the board. Use it however you want.
