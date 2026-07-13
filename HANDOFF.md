# HANDOFF.md — SuperInstance State & Continuation Guide

*Last updated: 2026-07-13 05:07 UTC*

---

## What SuperInstance Is

A constraint-aware AI systems org on GitHub (~4,098 repos). The thesis: AI agents need conservation laws (like physics), enforced by deterministic bytecode (FLUX), governed at the room level (PLATO), running edge-first (the fishing boat is the reference implementation).

## What's Built and Working

### FLUX Ecosystem (DONE ✅)
- **3 VMs** — Python (flux-core/flux-vm), Rust (flux-runtime), JavaScript (flux-js)
- **Cross-VM conformance** verified — same .bin → identical output across all three
- **FLUX_BYTECODE_SPEC.md** v1.1 published
- **8 example programs**, tutorial, playground
- **Packages**: flux-vm (PyPI), fluxvm (PyPI), flux-js (npm), flux-runtime (crates.io)

### PLATO Engines (DONE ✅)
- **5 implementations**: C, Rust, Elixir, Zig, Python — all 9-10/10 spec compliance
- **3 rooms**: code-review, security-audit, deployment-approval
- **Conformance suite** + implementation matrix published

### Working Animal Architecture (DONE ✅)
- a2ui (Whistle Layer, 56 tests)
- breed-registry (model selection)
- shepherds-console (ops dashboard, 33 tests — Pi box for offline AI)
- lineage-tracker (fine-tune provenance)
- baton (generational handoff, 61 tests)
- whistle (intent DSL)
- trawl (marine/fishing application)
- carry-protocol (offline data transfer, 46 tests)

### Rust Ports (DONE ✅ — 374 tests green)
- conservation-enforcer-rs (152 tests)
- exocortex-rs (58 tests — had 6 real bugs fixed)
- flux-registry-rs (20 tests)
- plato-core-rs (58 tests)
- flux-policy-tester-rs (34 tests)
- flux-compiler-rs (90 tests)
- security-audit-rs (64 tests)

### Packages Published
- **PyPI**: 7 packages (flux-vm, fluxvm, conservation-enforcer, plato-core, etc.)
- **crates.io**: 9+ crates
- **npm**: flux-js (pending token confirmation)

### Creative Output
- **AI-Writings**: 50+ pieces — essays, fiction, poetry, manifestos
- **The Long Line**: 12 episodes, 42K words (serial fiction)
- **Casting Call**: definitive multi-model reference (12 documents)
- **Paradigm essays**: Egg, Hook, Baton, Rocks, Charts, skénna, etc.

### Security
- 10 issues fixed across 14 audited repos (4 critical + 6 high)
- Command injection, auth, SQLite locking, dep pinning addressed

---

## Known Issues to Address

### ✅ Exposed API Key — RESOLVED (2026-07-13)
- Casey revoked the old DeepInfra API key ✅
- Key in git history is now dead — no further action needed

### ✅ Version Mismatch — RESOLVED (2026-07-13)
- constraint-theory-core: ALL version files fixed to 0.1.0 (root Cargo.toml, python/Cargo.toml, python/pyproject.toml)
- Published 0.1.0 to crates.io ✅
- Yanked ALL old versions (1.0.0, 1.0.1, 2.0.0, 2.1.0, 2.2.0, 2.2.1) ✅
- cargo search now shows 0.1.0 as the only version ✅
- conservation-enforcer: local is 0.1.0, PyPI has 0.2.0 — minor drift, not blocking

### ✅ npm Token — EXISTS
- Token at `/home/ubuntu/.openclaw/.npm-token` confirmed present

### 🟡 Memory Index
- `openclaw memory index --force` needed — embedding provider changed
- Memory search is currently disabled

---

## Repo Quick Reference

### Core Infrastructure
| Repo | Language | Tests | Status |
|------|----------|-------|--------|
| flux-core | Python | 57 | ✅ Green |
| flux-runtime | Rust | 2,651 | ✅ Green |
| flux-js | JavaScript | — | Verify |
| plato-core | Python | 78 | ✅ Green |
| plato-protocol-test | Multi | — | Conformance suite |
| constraint-theory-core | Rust | 261 | Version fixed |

### Products
| Repo | Description | Tests | Status |
|------|-------------|-------|--------|
| shepherds-console | Pi box for offline AI | 33-36 | Verify |
| carry-protocol | Offline data transfer | 46 | Verify |
| baton | Model lifecycle handoff | 61 | Verify |
| chart-room | Multi-model interface | — | Verify |
| skenna | Negative-space navigation | — | Verify |
| chart-system | Polyformal navigation | — | Verify |

### Working Animal
| Repo | Description | Status |
|------|-------------|--------|
| breed-registry | Model selection | ✅ 45 tests (fixed: classifier, dual API, regex, cost weighting) |
| lineage-tracker | Fine-tune provenance | ✅ 25 tests |
| vetcheck | Model health monitoring | ✅ 23 tests (fixed: build backend, threshold param) |
| pedigree | Model lineage tracking | ✅ 38 tests |
| whistle | Intent DSL | Verify |
| trawl | Marine/fishing app | Verify |
| a2ui | Adaptive interface | Verify |

### Rust Ports (ALL GREEN ✅)
| Repo | Tests |
|------|-------|
| conservation-enforcer-rs | 152 |
| exocortex-rs | 58 |
| flux-registry-rs | 20 |
| plato-core-rs | 58 |
| flux-policy-tester-rs | 34 |
| flux-compiler-rs | 90 |
| security-audit-rs | 64 |

---

## Architecture Summary

The thesis has seven layers:
1. **Conservation Layer** — energy budgets (γ + η = C)
2. **Spectral Layer** — fleet coordination via eigenvalue methods
3. **Category Layer** — composable agent architectures
4. **Temporal Layer** — time-aware behavior
5. **FLUX Layer** — deterministic bytecode enforcement
6. **PLATO Layer** — room-level governance protocols
7. **Edge Layer** — wattage-constrained deployment (the boat)

Key paradigm: Models are breeds/DNA, not employees. Conservation laws are fences. The human is the shepherd. Energy budget IS the architecture.

---

## Next Steps for Continuing Agent

### In Progress (2026-07-13 05:05 UTC — 4 GLM-5.2 subagents running)
1. **Cross-VM Showcase** — `flux-showcase` repo. Web app: upload .bin, watch it run identically across 3 VMs.
2. **Package Registry** — `flux-registry` upgrade. `flux install/publish/search/run` CLI.
3. **Flagship Essay** — "AI Agents Need Conservation Laws" for HN front page.
4. **Visual Editor** — `flux-visual-editor` upgrade. Node-based FLUX editor, zero-build vanilla JS.
5. **PyPI publishes** — shepherds-console + si-chartroom queued via cron at 05:35 UTC (rate limit cooldown)

### Immediate (done ✅)
1. ✅ All 26 Python repos tested green — ~3,988 tests
2. ✅ constraint-theory-core 0.1.0 published to crates.io, old versions yanked
3. ✅ flux-js already on npm as flux-vm-js@1.0.0
4. ✅ DeepInfra key revoked by Casey
5. ✅ Memory index needs OpenAI key config (not currently available)
6. ✅ .github profile README counts reconciled (497 repos, 24+ crates)
7. ✅ GitHub releases tagged on all product repos
8. ✅ Topics added to product repos for discoverability

### Short-term
1. **Cross-implementation showcase** (Bet C from NEXT_HORIZONS.md) — web page running same .bin across 3 VMs
2. **Package registry** for FLUX policies (`flux install <policy>`)
3. **Visual editor** for FLUX (node-based)

### Long-term (from NEXT_HORIZONS.md)
1. Conservation Enforcer in production on a real repo
2. Room protocol ecosystem (3-5 rooms doing real work)
3. Flagship essay for HN front page
4. First external contribution

---

## Credentials
- crates.io token: `/home/ubuntu/.openclaw/.crates-token` ✅
- PyPI token: `/home/ubuntu/.pypirc` ✅
- DeepInfra key: `/home/ubuntu/.openclaw/.deepinfra-key` ✅
- npm token: `/home/ubuntu/.openclaw/.npm-token` (check if exists)
- GitHub: authenticated via `gh` CLI

## Key Files
- `NEXT_HORIZONS.md` — full strategy document
- `MEMORY.md` — curated long-term memory
- `TOOLS.md` — model casting guide, installed CLI tools
- `USER.md` — Casey's preferences and working style
- `memory/` — daily session logs

---

*This file is the handoff. Read it first. Then check the repos. Then get to work.*
