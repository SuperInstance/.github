# SuperInstance Synergy Map

*How the repos connect. Every line is a real integration point.*

```
                    ┌─────────────────┐
                    │   γ + η = C     │  ← The Conservation Law
                    │  (the physics)  │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
     ┌────────────┐  ┌─────────────┐  ┌───────────┐
     │conservation│  │    FLUX     │  │   PLATO   │
     │ -enforcer  │  │  bytecode   │  │   rooms   │
     │            │  │   (laws)    │  │ (govern)  │
     └─────┬──────┘  └──────┬──────┘  └─────┬─────┘
           │                │                │
           │    ┌───────────┘                │
           │    │                            │
           ▼    ▼                            ▼
     ┌──────────────┐              ┌──────────────┐
     │   skénna     │              │  shepherds   │
     │ (navigate η) │              │  -console    │
     └──────┬───────┘              │  (the boat)  │
            │                      └──────┬───────┘
            │                             │
            ▼                             ▼
     ┌──────────────┐              ┌──────────────┐
     │  chart-room  │              │    baton     │
     │ (4 panels,   │              │ (generational│
     │  4 γ configs)│              │  handoff)    │
     └──────┬───────┘              └──────┬───────┘
            │                             │
            ▼                             ▼
     ┌──────────────┐              ┌──────────────┐
     │ chart-system │              │    carry     │
     │ (formal chart│              │  -protocol   │
     │  types)      │              │ (offline xfer│
     └──────────────┘              │  of baton)   │
                                   └──────────────┘
```

## Cross-Repo Integrations

### 1. conservation-enforcer ↔ CognitiveBudget
- `CognitiveBudget` class in `budget.py` implements γ + η = C
- FLUX bytecode BUDGET/SPEND/CHECK instructions enforce it at runtime
- Tests: 149 in conservation-enforcer

### 2. skénna ↔ conservation-enforcer
- Navigator uses `ChartThickness` to measure γ/C ratio
- Hazards are conservation violations (budget exceeded = hazard)
- Route planning respects cognitive budgets
- Tests: 147 in skénna

### 3. chart-room ↔ chart-system
- chart-room imports `ChartConfiguration`, `ChartType` from chart-system
- chart-system defines fisherman (thin γ), sailor (thick γ), tourist, native configs
- chart-room's 4 panels = 4 different γ allocations on same C
- Tests: 42 in chart-system, 13 in chart-room

### 4. baton ↔ lineage-tracker
- baton stores lessons in `./lineage/` directory (shared convention)
- `trace_lineage()` follows the chain of handoffs
- Lessons tag with model_origin for bloodline tracking
- Tests: 61 in baton

### 5. carry-protocol ↔ baton
- `carry.baton_bridge` module: pack_lessons() / unpack_lessons()
- Baton lessons survive offline transfer with checksum integrity
- Carry parcels carry baton wisdom across the Divide
- Tests: 10 in baton_bridge (56 total in carry-protocol)

### 6. shepherds-console ↔ conservation-enforcer
- Console's `speak()` calls `enforcer.enforce()` on every output
- Wattage budget maps to C (energy = cognition)
- Fences visible on display — blocked output shown to user
- Tests: 60 in shepherds-console

### 7. flux-visual-editor ↔ FLUX bytecode
- Budget nodes ARE γ/η allocators
- Compile visual graph → FLUX assembly → .bin file
- Conservation ledger preview in the editor
- Tests: 23 CI checks

### 8. flux-registry ↔ FLUX VM
- Registry policies are .bin files with manifests
- `flux run` loads .bin into FLUX VM and executes
- Manifests declare which conservation laws are enforced
- Tests: 30 in flux-registry

### 9. flux-showcase ↔ all 3 FLUX VMs
- Same .bin runs on Python, Rust, JS VMs
- Identical traces = proof the abstraction is correct
- Tests: 15 in flux-showcase

## The Paradigm Loop

```
Creative ideation (essays)
        │
        ▼  concretizes into
Formal specifications (GAMMA_ETA_SPEC, ARCHITECTURE)
        │
        ▼  implements as
Code (conservation-enforcer, skénna, chart-system)
        │
        ▼  verified by
Tests (4,000+ across the org)
        │
        ▼  demonstrated by
Products (shepherds-console, chart-room, showcase)
        │
        ▼  feeds back into
Creative ideation (what did we learn?)
```

The loop is closed. Essays become specs. Specs become code. Code becomes products. Products generate experience. Experience generates essays.

---

*Last updated: 2026-07-13*
