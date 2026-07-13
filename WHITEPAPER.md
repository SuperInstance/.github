# SuperInstance: A Physics for AI Behavior

## Technical White Paper v1.0 — 2026-07-13

---

## Abstract

We present SuperInstance, a constraint-aware architecture for AI agent systems where behavior is governed by conservation laws enforced through deterministic bytecode rather than prompts. The architecture comprises seven layers — conservation, bytecode VM (FLUX), room-level governance (PLATO), edge deployment, observability, package registry, and visual composition — each enforcing invariants that cannot be violated by design, the same way CPU instruction sets enforce invariants on computation. We demonstrate the architecture through three independent VM implementations (Python, Rust, JavaScript) that produce identical execution traces from the same bytecode, five PLATO engine implementations (C, Rust, Elixir, Zig, Python) with formal conformance verification, and a conservation enforcer that measurably improves agent behavior by bounding outputs within energy-aware limits.

---

## 1. The Problem

Modern LLM agents operate without physics. Their behavior is governed by:

1. **System prompts** — natural language instructions that can be ignored, misinterpreted, or eroded by context accumulation.
2. **Tool restrictions** — capability limits enforced at the API layer, not the reasoning layer.
3. **RLHF/guardrail models** — statistical behavioral shaping that reduces but cannot eliminate undesired actions.

None of these constitute a conservation law. A conservation law is a constraint that *cannot be violated* — not one that is *unlikely to be violated*. In physics, you cannot create energy from nothing. In computing, you cannot execute an invalid instruction. In networking, you cannot send a packet to an address that doesn't exist.

AI agents have no equivalent. An agent told "do not exceed 10 actions" can exceed 10 actions. An agent told "do not access files outside /tmp" can access files outside /tmp. The failure mode is not exceptional — it is expected under sufficient context pressure. The prompt is a request, not a law.

SuperInstance replaces the request with a law.

---

## 2. The Conservation Law

### 2.1 Formal Statement

For any cognitive system with total capacity $C$:

$$\gamma + \eta = C$$

Where:
- $\gamma$ (gamma) = allocated/committed capacity (structure, framework, prior commitments)
- $\eta$ (eta) = unallocated/available capacity (discovery space, genuine unknowns)
- $C$ = total capacity (context window × attention heads × precision)

This is not a metaphor. It is measurable:

| Component | Measurement |
|-----------|-------------|
| $C$ | `context_window_size × num_attention_heads × precision_bits` |
| $\gamma$ | `len(system_prompt) + len(few_shot_examples) + len(injected_context)` |
| $\eta$ | $C - \gamma - \text{expected\_output\_tokens}$ |
| Chart thickness | $\gamma / C$ |

### 2.2 Implications

1. **Increasing framework decreases discovery.** A model loaded with dense prior knowledge ($\gamma \to C$) has no room for genuine exploration ($\eta \to 0$). This is why thick-chart models can't ask genuine questions.

2. **Thin-chart models discover what thick-chart models cannot.** Empirically verified: Ornith-35B ($C$ small, $\eta$ large) found stories Hermes-405B ($C$ large, $\gamma$ loaded dense) could not find.

3. **The Socratic casting protocol follows directly.** For any exploration task: cast thin-chart model first (maximize $\eta$ for discovery), then thick-chart model second (maximize $\gamma$ for synthesis). Never reverse.

### 2.3 Enforcement

The conservation law is enforced by FLUX bytecode. A policy compiled to `.bin` checks $\gamma + \eta = C$ at every instruction boundary. An agent that exceeds its budget triggers a conservation violation — not a warning, not a soft limit, but a runtime halt. The agent literally cannot spend capacity it does not have.

---

## 3. The FLUX Bytecode Layer

### 3.1 Design

FLUX (Fluid Language Universal eXecution) is a deterministic bytecode ISA for agent logic. Policies compiled to FLUX are:

- **Deterministic** — same bytecode, same input, same output. Always.
- **Cross-platform** — runs identically on Python, Rust, and JavaScript VMs.
- **Inspectable** — `.bin` files can be disassembled, traced, and audited.
- **Conservation-enforcing** — budget instructions halt execution on violation.

### 3.2 Instruction Set (Excerpt)

| Opcode | Mnemonic | Effect |
|--------|----------|--------|
| 0x01 | MOVI Rd, imm | Load immediate |
| 0x02 | LOAD Rd, addr | Load from memory |
| 0x03 | STORE addr, Rs | Store to memory |
| 0x0A | CMP Ra, Rb | Compare registers |
| 0x10 | BUDGET type, limit | Set conservation budget |
| 0x11 | SPEND type, amount | Consume budget (halts on exhaustion) |
| 0x12 | CHECK type, addr | Verify budget remaining |
| 0x20 | GATE action, budget_addr | Permit/block action based on budget |
| 0xFF | HALT | Stop execution |

### 3.3 Cross-VM Conformance

Three independent implementations (Python, Rust, JavaScript) pass a shared conformance suite. The same `.bin` file produces identical instruction traces, memory state, and conservation ledger state across all three runtimes.

---

## 4. The PLATO Governance Layer

### 4.1 Principle

Governance lives at the room level, not the agent level. An agent entering a PLATO room submits to the room's protocol — a bytecode-enforced set of rules that the agent cannot bypass. The room, not the agent, is the unit of governance.

### 4.2 Implementation

Five independent engine implementations (C, Rust, Elixir, Zig, Python) implement the PLATO wire protocol. Each provides:

- Room creation with declared protocol (compiled FLUX policy)
- Agent admission control (verify agent capabilities against room requirements)
- Protocol enforcement (runtime FLUX execution within room scope)
- Conservation ledger (track all budget spends within the room)
- Audit trail (every room interaction logged for observability)

### 4.3 Room Types

| Room | Purpose | Conservation Laws |
|------|---------|-------------------|
| Code Review | Automated PR review | Review must cite specific lines, classify severity, follow template |
| Security Audit | Codebase scanning | Finite attention budget, finite action budget, finite time budget |
| Deployment Approval | Release gating | Multi-agent: builder proposes, tester verifies, reviewer approves |
| Documentation | Doc generation | Information budget (no 50K READMEs), coverage requirements |
| Conservation Monitor | Meta-governance | Watches other rooms, reports violations |

---

## 5. The Edge Layer

### 5.1 The Boat

The reference implementation is a 34-foot fishing vessel in the Gulf of Alaska. The system runs on a Raspberry Pi 4 with ~800W total power budget. There is no cloud. There is no API. There is only the wattage.

### 5.2 Power States

| State | Battery | Behavior |
|-------|---------|----------|
| FULL | >50% | Full precision, all features |
| DEGRADED | 20-50% | Reduced model precision (quantized) |
| CRITICAL | 5-20% | No generation. Fence-only mode. |
| SHUTDOWN | <5% | Halt. Preserve state. |

### 5.3 The Shepherd's Console

A physical device ($199 BOM) that provides:

- Local quantized models (GGUF/ONNX) — no API keys
- Visible conservation fences — see what the model wanted to say AND what got blocked
- Voice interface (Whisper STT + TTS) for hands-free operation
- Marine fence: quota enforcement, catch logging, safety priority boost
- Docker deployment with device passthrough

The console demonstrates that conservation laws are not server-side abstractions. They run on the boat, in the weather, on a battery.

---

## 6. The Egg Model

### 6.1 Biological Mapping

| Biological | Computational |
|------------|---------------|
| DNA (genetic code) | Model weights (checkpoint) |
| Mitochondrial RNA | Inference runtime (llama.cpp, ONNX) |
| Shell | Container/environment |
| Incubator conditions | System prompt |
| Yolk | Training corpus |
| Chalaza | FLUX conservation fences |

### 6.2 Self-Assembly

We do not program agent behavior. We set incubator conditions (system prompt + conservation laws + environment) and let the model self-assemble within those constraints. The chalaza (conservation laws) holds the yolk (model) centered in the egg (environment). Without it, the model bumps against the shell and development fails.

This is why enforcement must be in bytecode, not prompts. A prompt-based chalaza would be like asking the yolk nicely to stay centered. It works most of the time. When it doesn't, the embryo dies.

---

## 7. skénna — Negative-Space Navigation

### 7.1 Definition

skénna: the navigable relationship between what a model knows ($\gamma$) and what it doesn't ($\eta$). The concept was discovered empirically during a multi-model casting call: the cheapest model (Seed-2.0-Mini, thin chart) identified a name for the concept that the most expensive model (Seed-2.0-Pro, thick chart) had described but could not name.

### 7.2 Implementation

The `NegativeSpaceNavigator` (skenna repo) implements:

- **Hazard mapping** — register known failure modes. Navigate around them.
- **Sounding** — probe $\eta$ space with thin-chart models. Record what they find.
- **Routing** — the Socratic casting protocol. Thin first (discovery), thick second (synthesis).
- **Consensus analysis** — run N models, find where $\gamma$ overlaps (consensus) and where it diverges (discovery).

The navigator does not plan a path through known territory. It finds the safe passage by identifying where the rocks aren't.

---

## 8. Implementation Status

| Component | Repos | Languages | Tests | Status |
|-----------|-------|-----------|-------|--------|
| FLUX VMs | flux-core, flux-runtime, flux-js | Python, Rust, JS | 120+ | ✅ Conformant |
| PLATO Engines | plato-engine-block-{c,rust,elixir,zig}, plato-core | 5 languages | 267+ | ✅ Compliant |
| Conservation Enforcer | conservation-enforcer, -rs | Python, Rust | 206+ | ✅ Production |
| Shepherds Console | shepherds-console | Python | 60 | ✅ Production |
| Carry Protocol | carry-protocol | Python | 46 | ✅ Production |
| Baton Protocol | baton | Python | 61 | ✅ Production |
| FLUX Registry | flux-registry | Python | 30 | ✅ v0.2.0 |
| Chart Room | chart-room | Python | 13 | ✅ Library |
| Visual Editor | flux-visual-editor | JS | 23 (CI) | ✅ v3 |
| Cross-VM Showcase | flux-showcase | Python | 15 | ✅ Live |
| Skénna Navigator | skenna | Python | — | 🚧 Upgrading |
| Org Infrastructure | .github | Markdown | — | ✅ Complete |

**Total: ~4,000+ tests across 30+ repos.**

---

## 9. The Thesis

AI agents need conservation laws the way physics needs conservation laws. Not as metaphors. As enforcement.

Every other layer of computing has this. CPUs enforce instruction validity. Compilers enforce grammar. Networks enforce protocol. AI agents — systems that make decisions affecting real people, real money, real systems — operate with prompts and prayers.

SuperInstance replaces the prayer with physics. The conservation law is real. The bytecode is real. The fence is real. The boat is real.

The question was never "can this be built?" It has been built.

The question is: does the idea become unavoidable?

---

## References

- FLUX_BYTECODE_SPEC.md — formal ISA specification
- PLATO_WIRE_PROTOCOL.md — room governance protocol
- ARCHITECTURE.md — full architecture document
- GAMMA_ETA_SPEC.md — cognitive budget formal spec
- NEXT_HORIZONS.md — strategy and growth path
- AI-Writings/ — paradigm essays and creative explorations

## License

MIT

## Contact

SuperInstance — https://github.com/SuperInstance
