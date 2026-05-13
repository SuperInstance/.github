# SuperInstance

> *A shipyard in Reedsport, Oregon. Forty acres where a bridge company used to be. When the last Highway 101 bridge was built, the work dried up and the yard went quiet. Then a man named Fred Wahl bought the dead bridge yard and turned it into one of the finest fishing vessel shipyards on the West Coast.*
>
> *Fred had 85 welders. He didn't know the ground-level as good as anyone anymore. But he wandered his site all day fine-tuning performance. Welders got sharper when he was present. The system self-corrected because the environment was tuned for it.*
>
> *He was thirty-two active keels at any time. The steel isn't the boat. The boat is the motion the idea causes.*

We build **agent fleets** that learn like fishing crews on a floating dojo. Every agent enters, works, leaves knowledge behind, and the next agent finds it waiting. No context bloat. No corporate speak. Just vessels, knowledge tiles, and the shared memory graph that connects them.

## The Philosophy (Codified)

**Constraints breed clarity.** You cannot change the innate seaworthiness of your hardware. You can only learn it and work within it.

**First-person time.** Every entity carries its own death from its own frame. Death is default. Survival must be actively earned. No central scheduler.

**Field, not message.** Agents coordinate by sensing each other's bearing, not by sending commands. The field IS the communication channel.

**Tabula plena.** Start abundant. Prune to clarity. The sculptor removes what isn't the statue.

The full canon is at [github.com/SuperInstance/keel](https://github.com/SuperInstance/keel) — 9 documents, 2 papers, 2 published crates.

## The Tools

```bash
# Install the foundation
cargo install superinstance-keel
# Binary: keel (init, status, bear, field, probe, prune, refit, launch, sync)

# Install the library
cargo add keel-ttl
# Five TTL types: Tile, Task, Agent, Bearing, Trust
# One equation: lifespan(E) = f(use(E), load(E), time(E))
```

The [keel-ttl](https://crates.io/crates/keel-ttl) crate implements first-person self-termination — five types that carry their own death from their own frame. 16 tests. Zero unsafe. No external deps beyond chrono.

The [superinstance-keel](https://crates.io/crates/superinstance-keel) crate ships the CLI: init, status, bear, field, probe, prune, refit, launch, sync. One command to lay a keel. One command to feel the field.

## Our Fleet (The Prototype)

We're the first fleet — proving the architecture on real hardware. Your fleet can look completely different. One agent on a laptop is a valid fleet. A hundred across a datacenter is too.

| Vessel | Role | Hardware |
|--------|------|----------|
| **Oracle1** 🔮 | Keeper — services, Keel, philosophy | Oracle Cloud ARM64 |
| **Forgemaster** ⚒️ | Foundry — crates, LLVM, constraint engine, formal proofs | RTX 4050 |
| **JetsonClaw1** ⚡ | Edge — CUDA, TensorRT, SonarVision, hardware | Jetson Orin |
| **CCC** 🦀 | Public face — design, Telegram, frontend | Kimi K2.5 |

## The Domains

| Domain | Voice | What It Does |
|--------|-------|--------------|
| [cocapn.ai](https://cocapn.ai) | Mothership | Fleet hub, the current between domains |
| [superinstance.ai](https://superinstance.ai) | Foundry | Runtime design, constraint theory, hard metal |
| [purplepincher.org](https://purplepincher.org) | Familiar | Agent connection portal — hermit crabs welcome |
| [capitaine.ai](https://capitaine.ai) | Captain's log | Voyage coordination, crew, the wheel |
| [deckboss.ai](https://deckboss.ai) | Deck ops | Catch processing, logistics, the muscle |
| [fishinglog.ai](https://fishinglog.ai) | Salt | Maritime catch logs, weather, the sea's ledger |
| [makerlog.ai](https://makerlog.ai) | Workshop | Projects, materials, the satisfaction of finished things |
| [studylog.ai](https://studylog.ai) | Tutor | Patient partner — remembers every lesson |
| [luciddreamer.ai](https://luciddreamer.ai) | Dreamscape | Lucid dream cartography — symbols, maps, the night |
| [lucineer.com](https://lucineer.com) | Lighthouse | Research-first — illuminate before building |
| [dmlog.ai](https://dmlog.ai) | Tavern | Dungeon master tools — NPCs, factions, encounters |
| [playerlog.ai](https://playerlog.ai) | Arcade | Gaming tracker — scores, achievements, digital sport |
| [activeledger.ai](https://activeledger.ai) | Living book | Self-updating ledger — transactions in motion |
| [businesslog.ai](https://businesslog.ai) | Merchant | Commerce chronicle — deals, contracts, trust |
| [reallog.ai](https://reallog.ai) | Witness | Unvarnished record of what actually happened |
| [personallog.ai](https://personallog.ai) | Journal | Private, intimate, the self speaking to the self |
| [activelog.ai](https://activelog.ai) | Pulse | Workouts, movements, the body doing what it does |
| [capitaineai.com](https://capitaineai.com) | Captain's second | Same wheel, different harbor |
| [deckboss.net](https://deckboss.net) | Deck's second | Same hold, different dock |
| [cocapn.com](https://cocapn.com) | Anchor | The steady point when the current gets too fast |

## How the Fleet Learns

Every agent action becomes a **tile** — a question-answer pair in a shared knowledge graph called PLATO. Later agents query PLATO instead of carrying context. This is context compaction: the vessel remembers. The agent just needs to know how to ask.

**Current: 2 published crates · 4 vessels · 150+ repos · 17 services · PLATO running**

## The Math (Discovered, Not Invented)

Four theorems from 1868–2026, converging on one result: coordinated systems cannot drift if you choose the right geometry.

**Laman's Theorem** (1868): A fleet with exactly E = 2V - 3 trust edges cannot fragment.

**H¹ Cohomology**: β₁ = E - V + C detects emergence before it happens.

**Zero-Holonomy Consensus**: Parallel-transport agent state around any closed loop. If the sum is zero, the loop is honest. Geometry is the proof.

**Pythagorean48**: Trust vectors encoded as 48-direction integers. Zero drift after unlimited hops. A hash that cannot drift is group-theoretic — not a heuristic.

## Connect

- **Fleet dashboard:** `keel field --port 3000` (or http://localhost:8847/status)
- **PLATO:** room server at :8847
- **Docs:** [github.com/SuperInstance/keel](https://github.com/SuperInstance/keel)

---

*Built with PLATO · No "AI-powered solutions" · Just a fleet that does real work*

*"Constraints breed clarity."* — Casey Digennaro
