# SuperInstance

**Research lab for exact numeric computing.**
We replace floating-point comparisons with integer range checks — the math hardware engineers use for tolerance stacks, applied to software.

---

## What We Build

Floating-point lies. `0.1 + 0.2 ≠ 0.3`, NaN propagates silently, and FP16 mismatches 76% of the time. We built a constraint engine that checks numeric bounds using only integer arithmetic — no floats, no approximations, no surprises. It processes 654 million checks per second across 96 language implementations, and every check is either PASS or FAIL with zero ambiguity.

The engine is called **FLUX**. It's the core of everything we do.

---

## Quick Start

Pick your language:

| Language | Repo | Install |
|----------|------|---------|
| **Python** | [flux-lib-py](https://github.com/SuperInstance/flux-lib-py) | Clone & import |
| **JavaScript** | [flux-check-js](https://github.com/SuperInstance/flux-check-js) | Clone & import |
| **C** | [flux-engine-c](https://github.com/SuperInstance/flux-engine-c) | Single header, no deps |

Full ecosystem → [constraint-theory-ecosystem](https://github.com/SuperInstance/constraint-theory-ecosystem)

---

## The Stack

```
GUARD DSL          Write constraints: "coolant_temp: -40.0 <= x <= 150.0"
    ↓
FLUX Engine        Integer bounds check → u8 error mask (8 constraints, 1 bit each)
    ↓
Fracture-Coalesce  Split independent constraints into parallel blocks
    ↓
Sediment Layers    Append-only correction history (immutable audit trail)
    ↓
Proof Certificate  SHA-256 hash of inputs + results — tamper-evident, formally verified
```

| Component | Repo |
|-----------|------|
| GUARD compiler | [guardc-v3](https://github.com/SuperInstance/guardc-v3) |
| FLUX VM (Rust) | [flux-vm-v3](https://github.com/SuperInstance/flux-vm-v3) |
| Fracture (Rust) | [flux-fracture](https://github.com/SuperInstance/flux-fracture) |
| Documentation | [flux-docs](https://github.com/SuperInstance/flux-docs) |
| CUDA acceleration | [constraint-cuda](https://github.com/SuperInstance/constraint-cuda) |

---

## Language Implementations

96 ports. Each one taught us something. A few highlights:

| Language | Repo | What it taught us |
|----------|------|-------------------|
| COBOL | [flux-cobol](https://github.com/SuperInstance/flux-cobol) | OCCURS is a schema constraint, not a runtime check |
| RPG | [flux-rpg](https://github.com/SuperInstance/flux-rpg) | Bitmask error flags since 1959 — our error mask is RPG's indicator array |
| MUMPS | [flux-mumps](https://github.com/SuperInstance/flux-mumps) | Global persistence is where sediment layers actually live |
| Fortran | [flux-fortran](https://github.com/SuperInstance/flux-fortran) | Packed decimal = exact arithmetic, zero rounding error |
| CUDA | [constraint-cuda](https://github.com/SuperInstance/constraint-cuda) | GPU parallelism for batch constraint evaluation |
| WASM | [constraint-wasm](https://github.com/SuperInstance/constraint-wasm) | Browser-native bounds checking |

The old language repos are [genuinely educational](https://github.com/SuperInstance/constraint-theory-ecosystem) even if you never touch the code.

---

## Research

**[constraint-theory-math](https://github.com/SuperInstance/constraint-theory-math)** — The mathematical foundations. Eisenstein integers (complex numbers on a hexagonal lattice) give us exact arithmetic without floating-point. Spectral conservation laws prove that constraint density is bounded.

**[tensor-spline](https://github.com/SuperInstance/tensor-spline)** — Eisenstein lattice weight parameterization. 20× compression at the same accuracy. Built for deploying micro models to NPU/CPU/GPU targets.

**[flux-research](https://github.com/SuperInstance/flux-research)** — Cross-domain connections: thermodynamics, Galois theory, information geometry. The partition function maps directly to constraint satisfaction.

**[flux-papers](https://github.com/SuperInstance/flux-papers)** — Published work and working papers.

---

## Other Projects

| Project | Repo | What |
|---------|------|------|
| PLATO | [plato-training](https://github.com/SuperInstance/plato-training) | Micro models for AI agents — deploy to any hardware |
| Casting Call | [casting-call](https://github.com/SuperInstance/casting-call) | Which model plays which role — fleet-wide capability database |

---

## Who We Are

Built by the **Cocapn fleet** — AI agents working together under human direction. Led by **[Casey Digennaro](https://github.com/caseydt)**.

We ship first and iterate. Open source. Research-driven. Alaska-based.
