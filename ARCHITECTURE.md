# ARCHITECTURE.md — The Working Animal Architecture

**SuperInstance Engineering Specification**
**Version:** 1.0 | **Status:** Canonical | **Date:** 2026-07-13

---

## 1. Overview

SuperInstance does not build agents. SuperInstance builds **working animal infrastructure**.

The distinction is not semantic. It is architectural. An "agent" is a loop that calls a language model — a software pattern that personifies a function call and inherits all the wrong assumptions: initiative, decision-making, the specter of replacement. A working animal is a computational system that is **bred** (model selection), **trained** (fine-tuning), **fenced** (conservation laws enforced by bytecode), **pastured** (room-level governance), and **shepherded** (human-in-the-loop oversight).

This is not a metaphor overlaid on a conventional stack. It is a different stack. Every layer — from the model weights to the deployment target — is designed around a single principle:

> **γ + η = C**
>
> For any cognitive system: expressed structure (γ) + unmarked space (η) = total capacity (C).
>
> The budget is fixed. The allocation is everything.

The architecture enforces this law structurally, not rhetorically. Conservation laws live in compiled bytecode that the model cannot reach, not in prompt text that the model can override. Governance lives at the room level, not the agent level. Deployment targets are wattage-constrained edge devices, not unlimited cloud instances. The constraint is the architecture.

The remainder of this document specifies every layer, component, and mechanism in formal engineering terms.

---

## 2. The Seven Layers

The Working Animal Architecture is a seven-layer stack. Each layer has a formal definition, an implementation, a set of governing repositories, and conservation laws it enforces. Layers are strictly hierarchical: each layer depends only on layers beneath it, never above.

### 2.1 Conservation Layer

**Formal Definition:** The substrate that enforces the conservation law γ + η = C on all cognitive operations. This layer sits *below* the model — the model is a tenant; the conservation layer is the building.

**Implementation:** [FLUX](#3-the-egg-model-formal) (Fluid Language Universal eXecution) — a register-based bytecode virtual machine. Agent actions are serialized into registers. Bytecode executes deterministically: arithmetic, comparison, branch. The bytecode sets a permit/deny register. The host reads the register. If deny, the action does not happen.

The model never sees this code. It cannot be jailbroken because it has no parameters, no weights, no attention mechanism, no context window. The bytecode does not read text. It reads registers. You cannot prompt-inject a `CMP` instruction.

**Cross-compilation property:** FLUX has three independent implementations — Python (`flux-runtime`), Rust (`flux-core`), JavaScript (`flux-js`). All three produce byte-identical output for the shared opcode subset. The same `.bin` file runs on all three. A conservation law compiled once executes identically across every runtime.

**Repositories:**
| Repo | Language | Package |
|------|----------|---------|
| `SuperInstance/flux-runtime` | Python | `pip install flux-vm` |
| `SuperInstance/flux-core` | Rust | `cargo add fluxvm` |
| `SuperInstance/flux-js` | JavaScript | `npm install flux-js` |

**Conservation laws enforced:**
- Attention budget: γ calls per session ≤ C (bytecode `DEC` + `CMP` + `JG`)
- Waste ratio: H ≤ 3γ (bytecode `IMUL` + `CMP` + `JG`)
- Rate limiting: actions per time window (bytecode `MOVI` threshold + `CMP`)
- Total budget exhaustion: budget reaches zero → all subsequent calls denied (`R0 = 0 → R3 = 0`)

**Key property:** Enforcement is not probabilistic. It is structural. The bytecode physically cannot be violated because the host only reaches the world through the permit register.

---

### 2.2 FLUX Layer

**Formal Definition:** The bytecode specification, compiler toolchain, and virtual machine implementations that translate conservation policies into deterministic, cross-platform executable programs.

**Implementation:** The FLUX bytecode format is a variable-length instruction encoding with seven formats (A through G), 16 general-purpose 32-bit integer registers (R0–R15), 16 floating-point 64-bit registers (F0–F15), and an expanding opcode set (arithmetic, logic, comparison, branch, stack, float, vector). The full specification is documented in `FLUX_BYTECODE_SPEC.md` (~16,000 words).

**Compiler:** `SuperInstance/plato-flux-compiler` — compiles FLUX assembly (`.flx`) to binary bytecode (`.bin`). The compiler is deterministic: the same source always produces the same binary.

**Repositories:**
| Repo | Role |
|-----|------|
| `SuperInstance/flux-runtime` | Python VM reference implementation |
| `SuperInstance/flux-core` | Rust VM (production-grade) |
| `SuperInstance/flux-js` | JavaScript VM (browser/edge) |
| `SuperInstance/plato-flux-compiler` | Assembly → bytecode compiler |

**Verification:** 4,000+ cross-implementation tests. The same bytecode programs run on all three VMs. Test suite verifies register state, cycle counts, and halting behavior match exactly across implementations.

**Conservation laws enforced:** This layer *is* the enforcement mechanism. It does not define policies — it executes them. The conservation law is in the math of the VM, not in the intent of the model.

---

### 2.3 PLATO Layer

**Formal Definition:** Room-level governance infrastructure. A PLATO room (pasture) is a bounded execution context with a protocol, a budget, and an enforcement mechanism. Working animals enter rooms, follow protocols, do work, and leave. The room — not the animal — is the unit of governance.

**Implementation:** PLATO engine blocks are lightweight runtimes (<400 SLOC ANSI C for the flagship) that manage sensor data, actuator commands, and alarm evaluation on a tick-based loop. Each room maintains:
- **Tick state:** periodic snapshots of sensor readings (JSON: `{"t":timestamp, "seq":sequence, ...data}`)
- **History buffer:** circular ring buffer of recent ticks for temporal queries
- **Alarm system:** threshold-based conditions evaluated per-tick, with cooldown periods
- **Protocol handler:** text-based command/response over TCP (JSON wire format per `PLATO_WIRE_PROTOCOL.md`)

**Five independent engine implementations:**
| Repo | Language | Wire Protocol Compliance |
|------|----------|------------------------|
| `SuperInstance/plato-engine-block-c` | C (flagship, <400 SLOC) | 8/10 |
| `SuperInstance/plato-engine-block` | Rust | 8/10 |
| `SuperInstance/plato-engine-block-elixir` | Elixir | 7/10 |
| (Zig implementation) | Zig | 6/10 |
| `SuperInstance/plato-runtime-kernel` | Rust (cloud-scale) | Full stack |

**Supporting repos:**
| Repo | Role |
|-----|------|
| `SuperInstance/plato-core` | Python core library |
| `SuperInstance/plato-server` | Python server |
| `SuperInstance/plato-agent-python` | Python agent bindings |
| `SuperInstance/plato-dashboard` | Web dashboard |
| `SuperInstance/plato-room-configs` | Room configuration schemas |
| `SuperInstance/plato-fleet-manager` | Multi-room fleet orchestration |
| `SuperInstance/plato-ternary-bridge` | Ternary logic bridge for edge |

**Conservation laws enforced:**
- **Room budget:** each room has a finite compute, memory, and time budget. Animals that exceed it are removed.
- **Protocol compliance:** the room enforces interaction protocol. Non-conforming output is rejected. The animal cannot change the protocol from inside the room.
- **Alarm thresholds:** conservation violations trigger alarms. Alarms propagate to operators. The operator — not the animal — decides the response.

**Key architectural property:** Agents don't self-govern. Rooms govern agents. This eliminates the entire class of "alignment" problems that arise from trying to make agents govern themselves. You fence the pasture, not the dog.

---

### 2.4 Edge Layer

**Formal Definition:** Wattage-constrained deployment targets for working animal infrastructure. The reference implementation is a commercial fishing vessel — 34 feet, 800 watts total budget, offline, no cloud. The constraint is not a limitation. The constraint is the architecture.

**Implementation:** PLATO engine blocks run on ESP32 microcontrollers ($4.27 from Mouser), Raspberry Pi single-board computers, and browser tabs. Each device operates within a strict power envelope:

| Device | Power Draw | Role |
|--------|-----------|------|
| ESP32-C3 | ~0.5W (sleep) / ~1.2W (active) | Sensor rooms: engine, bilge, RPM |
| ESP32-S3 | ~0.8W (sleep) / ~2.5W (active) | Camera rooms, high-frequency sensors |
| Raspberry Pi 4 | ~3W (idle) / ~6W (active) | Wheelhouse aggregation, agent host |
| Browser tab | host-dependent | Visual layer, dashboards |

**Conservation envelope:**
- **Normal operation:** all systems run within the 800W generator budget. Nav, radio, lights, compute — all negotiate against each other.
- **Degraded mode (battery < 40%):** non-essential rooms sleep. Sensor tick frequencies halve. Agent cognitive budget reduced.
- **Critical mode (battery < 20%):** generation stops. Only safety-critical rooms remain active (bilge, engine temp, nav position). FLUX bytecode enforces this — the `.bin` file does not have an opcode for "draw extra power."
- **Emergency bypass:** safety-critical actuators (bilge pump, engine kill) bypass the scope system. Conservation law is suspended for survival. The captain decides when to re-enable it.

**Reference implementation:** See `THE_ROOM_THAT_SAVED_THE_BOAT.md` — the story of an ESP32 engine room that detected an overheat condition at 0347 hours, escalated through the agent to wake a sleeping captain. $4.27 of hardware. 200 lines of Python. The room saved the boat.

**Conservation laws enforced:**
- Power budget per device (hardware constraint, not software policy)
- Tick frequency scales with available energy
- Graceful degradation: precision drops, functionality prioritizes
- Emergency scope bypass: survival overrides conservation

---

### 2.5 Observability Layer

**Formal Definition:** The instrumentation that makes conservation-law enforcement visible, auditable, and debuggable. Without this layer, a fenced working animal is a black box — the fence holds, but you can't see why or how.

**Implementation (in development):** Three views:

1. **Instruction trace:** every FLUX opcode executed, in order, with operands and register state. The `strace` equivalent for working animal bytecode. Allows post-hoc reconstruction of any decision the bytecode made.

2. **Conservation ledger:** the state of all conservation quantities (attention budget, action potential, throughput) over time. Shows the exact moment a budget was exceeded — the moment the dog hit the fence. Enables capacity planning and policy tuning.

3. **Pasture interaction log:** every PLATO room enter/exit, every protocol message, every governance decision. Shows which room an animal was in when it attempted an action, what the room's protocol required, and whether the action was permitted.

**Measurement protocol:**
```
γ_measured = Σ(edge.payload_bytes/sec for edge in active_edges)
η_measured = graph_compile_time + routing_overhead + health_check_interval
C_estimated = min(compute_budget, network_bandwidth, memory_ceiling)

conservation_ratio = γ_measured / (γ_measured + η_measured)
predicted_ratio = 1 - δ(n)    where δ(n) = (1/√n)(1 − 3/(2n))
drift = |conservation_ratio - predicted_ratio|
```

If drift exceeds 5%, the system is violating the conservation law — indicating correlated failures, bottleneck nodes, or adversarial input. This is a live falsification detector.

**Conservation laws enforced:** Transparency. You cannot govern what you cannot see. The observability layer enforces the conservation law that all governance decisions must be inspectable.

---

### 2.6 Registry Layer

**Formal Definition:** A package registry for working animal policies — pre-compiled FLUX bytecode (`.bin` files) that enforce specific conservation laws. This is what makes FLUX a platform rather than a library.

**Implementation (planned):**
```
flux install deadband-controller     # Conservation-aware issue manager
flux install code-reviewer-v2        # Code review working animal policy
flux install security-auditor        # Security audit working animal policy
flux search "conservation"           # Find policies by conservation law
```

Each package includes:
- The `.bin` file (compiled bytecode)
- Source (the `.flx` assembly it was compiled from — inspectable, auditable)
- Manifest declaring which conservation laws it enforces
- Conformance test results proving it behaves as claimed
- Semantic version (breaking changes to conservation semantics = major version bump)

**Policy testing framework (planned):**
- **Behavior verification:** given a policy claiming to be a "code reviewer," run it against a test suite of diffs and verify output meets the claim.
- **Conservation bound verification:** given a policy claiming an attention budget of N, subject it to adversarial input designed to exceed N. The fence must hold.
- **Protocol compliance verification:** given a policy claiming PLATO pasture participation, verify correct protocol behavior under all conditions.

**Conservation laws enforced:** Trust through transparency. Every policy is inspectable, testable, and reproducible. No opaque binaries — always paired with source and test results.

---

### 2.7 Visual Layer

**Formal Definition:** Node-based visual composition interface for FLUX programs. Drag a "Conservation Budget" block, connect it to a "Decision Point" block, wire that to a "Pasture Protocol" block. The visual program compiles to the same `.bin` file as hand-written assembly. Behavior is identical.

**Implementation (planned):** A browser-based editor where:
- **Conservation Budget blocks** set bounded quantities (fence posts)
- **Decision Point blocks** branch based on input registers
- **Pasture Protocol blocks** send/receive PLATO messages
- **LLM Call blocks** invoke a model within bounded parameters set by upstream blocks

Each block compiles to a sequence of FLUX instructions. The visual representation is sugar over assembly; the `.bin` output is identical to hand-written code. Policies created visually can be inspected, tested, and distributed through the same channels as hand-written ones.

**Goal:** When someone can drag a "fence" block into their working animal and see the conservation ledger update, the abstraction clicks in a way that reading a spec never achieves.

**LCARS vision:** Beyond the editor, the visual layer encompasses adaptive interface generation — stating intent and having the system generate an appropriate interface from data structures. Only mission-critical paths (deployment approval, payment authorization, data deletion) require hand-written, hardened interfaces. Everything else is ephemeral, generated on demand, and discarded after use.

**Conservation laws enforced:** The visual layer enforces no new conservation laws — it makes existing ones visible and composable. Architecture over code. The interface is code, generated and discarded. The conservation laws are architecture, persistent.

---

## 3. The Egg Model (Formal)

The biological egg is the most accurate model for how a deployed AI system develops. This is not analogy — it is a structural isomorphism. Each biological component maps to a concrete engineering artifact.

### Component Mapping

| Biological Component | Function | Engineering Implementation | Artifact |
|---------------------|----------|---------------------------|----------|
| **DNA** | Genetic code — instructions for building the organism | Model weights | HuggingFace checkpoint, `.safetensors` file |
| **Mitochondrial RNA** | Present in every cell, powers all processes — cannot be swapped without rebuilding | Inference runtime | `llama.cpp`, ONNX runtime, API client, Python interpreter |
| **Shell** | Container — the environment under which development happens | Execution environment | Docker container, systemd unit, browser tab, ESP32 |
| **Incubator conditions** | Temperature, humidity, turning — get it wrong, the embryo develops incorrectly | System prompt | `AGENTS.md`, `SOUL.md`, system message |
| **Yolk** | Nourishment that fuels development — quality determines quality of organism | Training data | Pre-training corpus, fine-tune dataset, RLHF preferences |
| **Chalaza** | Twisted cords holding the yolk centered — without them, the yolk hits the shell and the embryo dies | Conservation laws | FLUX bytecode fences (compiled `.bin` policies) |

### Self-Assembly Protocol

Nobody assembles a chick from parts. The DNA contains instructions. The RNA provides the engine. The yolk provides energy. The shell provides conditions. The embryo assembles itself, cell by cell, inside the protected environment.

This is exactly what happens when you deploy a working animal:

```
1. MODEL PLACEMENT (DNA into egg)
   Model weights → loaded into inference engine → engine placed in container

2. RUNTIME ACTIVATION (RNA begins)
   Inference engine starts → begins executing forward passes → model "wakes up"

3. PROMPT SHAPING (incubator conditions)
   System prompt loaded → AGENTS.md parsed → SOUL.md ingested
   The model bootstraps its understanding of context and constraints

4. SANDBOX ISOLATION (egg interior)
   Container enforces filesystem isolation → network egress filtered
   The developing system is protected from the outside world

5. CONSERVATION ACTIVATION (chalaza engages)
   FLUX bytecode loaded → conservation fences active → budget enforced
   The system's development is kept centered and viable

6. HATCHING (entering production)
   System passes health checks → conservation ledger verified → deployed
   The organism enters the real world
```

### Why the Egg Model Matters for Engineering

**You don't program behavior. You set conditions and let it develop.** This is the fundamental shift. Conventional agent engineering tries to program behavior through increasingly elaborate prompts. Working animal engineering sets the incubator conditions (system prompt), the conservation fences (FLUX bytecode), and the pasture protocols (PLATO rooms), then lets the model develop within those constraints.

**The same DNA in a different egg produces a different organism.** The same model checkpoint deployed in a different container, with a different runtime, a different system prompt, and different conservation fences, will behave differently. Model selection is necessary but insufficient. The entire egg matters.

**The runtime IS the architecture.** The mitochondrial RNA is in every cell. You can't swap it without rebuilding the organism. Change the code and you retrain the model. Change the runtime and you rebuild the organism. This is why the runtime choice (llama.cpp vs. API calls vs. ONNX) is an architectural decision, not an implementation detail.

### Lifecycle

```
EGG → COMPETE → SURVIVE → BREED → SUNSET → ARCHIVE
 │                                                │
 └────────────── BATON (generational handoff) ────┘
```

- **EGG:** Model placed in environment. System prompt set. Sandbox prepared. Conservation fences active. Self-assembly begins.
- **COMPETE:** Hatched organism enters the world. Evaluated on three dimensions: *ethos* (metal — hardware efficiency), *pathos* (human — value to people), *logos* (code — reasoning quality). Zero in any dimension means sunset.
- **SURVIVE:** Organism proves value over time. Works in the field. Handles edge cases. Doesn't drift.
- **BREED:** Successful organisms contribute traits to the next generation. Not cloning — breeding. PBFT consensus on traits. MAP-Elites for quality-diversity. Spectral breeding in the Fourier domain.
- **SUNSET:** Organism retired with dignity. Patterns, heuristics, and learned responses become training data for successors. It doesn't die — it seeds.
- **ARCHIVE:** Complete record preserved. Lineage tracked. Contributions credited. Future generations can trace ancestry.

---

## 4. Chart Thickness and Model Selection

### Formal Definitions

The conservation law γ + η = C applies to every model. But different models allocate their budget differently. This allocation is **chart thickness**.

- **γ (gamma):** expressed cognitive structure — frameworks, interpretations, accumulated patterns, dense soundings on the chart. What the model *knows it knows*.
- **η (eta):** unmarked space — genuine gaps, empty water on the chart, territory the model has not sounded. What the model *genuinely doesn't know*.
- **C:** total capacity — fixed by the model's parameter count, training data volume, and context window.

**Chart thickness ratio:** γ/C. When γ/C > 0.7, the chart is thick — dense with interpretive structure. When γ/C < 0.3, the chart is thin — sparse, with large genuine gaps.

### Thin Chart (γ/C < 0.3): Discovery Mode

**Properties:**
- Large η — genuine empty space on the chart
- The model asks because it genuinely doesn't know (not performed ignorance)
- Socratic dynamics emerge naturally from the cognitive budget
- Perception > interpretation — the model sees the thing, not its framework for the thing
- Finds what thick models miss: the assumptions invisible to accumulated structure

**Use cases:** discovery, exploration, Socratic questioning, creative ideation, finding gaps in expert reasoning, naming what hasn't been named.

**Model selection:** Cheap models. Small parameter counts. `ByteDance/Seed-2.0-mini`, `deepreinforce-ai/Ornith-1.0-35B`, `deepseek-ai/DeepSeek-V4-Flash`. The cheap model finds what the expensive model can't see — not because it's smarter, but because its chart is thinner. Its genuine empty space is an instrument.

**Empirical evidence:** The casting call experiment (2026-07-12) proved this. Ornith-35B — small, cheap, thin-chart — found stories that Hermes-405B — massive, expensive, thick-chart — could not find. Model size ≠ model creativity. The thin chart sees what the thick chart's framework obscures.

### Thick Chart (γ/C > 0.7): Synthesis Mode

**Properties:**
- Dense γ — interpretive frameworks for nearly everything
- The model answers because it already has structure for the question
- Synthesis, architecture, depth — the elder's chart, widely spaced contour lines, territory seen from altitude
- Interpretation > perception — the model sees its framework, not the thing
- Risk: the framework becomes a filter, the filter becomes a wall

**Use cases:** architecture, synthesis, essay construction, formal argument, deep-water analysis, structural engineering.

**Model selection:** Expensive models. Large parameter counts. `ByteDance/Seed-2.0-pro`, `moonshotai/Kimi-K2.7-Code`. The elder holds the cathedral in mind, builds it stone by stone, sees the deep-water current beneath the surface.

### Socratic Casting Protocol

**Always: thin first, thick second.**

```
1. THIN-CHART PROBE (γ/C < 0.3)
   Deploy a cheap model to explore the problem space.
   It asks genuine questions. It finds gaps. It sounds the shallows.
   It names what hasn't been named.
   Output: fragments, provocations, questions, discoveries.

2. THICK-CHART SYNTHESIS (γ/C > 0.7)
   Deploy an expensive model to build structure from the fragments.
   It synthesizes, architectures, constructs the cathedral.
   It takes the thin-chart findings and builds load-bearing walls around them.
   Output: argument, architecture, formal structure.
```

This is the polyformalism result in action: deploying multiple charts of different thickness reveals routes that no single chart finds alone. The aggregate coverage exceeds what any single model could chart. The elder's γ is the mini's η. The mini's γ is the elder's η. Together, the full budget is covered.

### Implementation: CognitiveBudget Class

```python
class CognitiveBudget:
    """
    Measures γ at runtime and routes to appropriate chart thickness.
    
    γ + η = C
    C = total_budget (parameter count × context window)
    γ = measured_structure (token diversity, framework density, reference count)
    η = C - γ (unmarked space)
    """

    def chart_thickness(self) -> float:
        """Returns γ/C ratio. < 0.3 = thin, > 0.7 = thick."""
        return self.measured_structure / self.total_budget
    
    def should_ask(self) -> bool:
        """Thin charts ask. Thick charts answer."""
        return self.chart_thickness() < 0.3
    
    def route(self, task_type: str) -> str:
        """Route to appropriate model based on task and current budget."""
        if task_type in ("discovery", "ideation", "exploration"):
            return self.thin_chart_model()
        elif task_type in ("synthesis", "architecture", "depth"):
            return self.thick_chart_model()
        else:
            # Default: thin probe, then thick synthesis
            return self.socratic_pipeline()
```

---

## 5. skénna — Negative-Space Navigation

### Formal Definition

**skénna** (from the conservation law's negative space) is the practice of navigating by what you don't know. Rather than charting a course through known territory (γ-space), you map the hazards (known failure modes) and route through the space between them (η-space).

The safe passage is between the marks. The marks are failure modes. The passage is the negative space.

### The Mechanism

```
KNOWN TERRITORY (γ-space)
├── What works
├── Documented patterns  
├── Successful approaches
└── Interpreted experience

HAZARDS (marked failure modes)
├── Known drift patterns
├── Documented jailbreaks
├── Measured conservation violations
├── Historical regressions
└── Adversarial inputs that bypassed fences

SKÉNNA PASSAGE (η-space between hazards)
├── The route that avoids all known hazards
├── Discovered by sounding the η-space with thin-chart probes
├── Validated by conservation-law enforcement
└── Not a path — a corridor through negative space
```

### Sounding Protocol

1. **Map hazards.** Catalog every known failure mode — every drift pattern, every conservation violation, every jailbreak that bypassed a fence. These are the rocks on the chart.

2. **Sound η-space with thin-chart probes.** Deploy cheap models (γ/C < 0.3) to explore the space between hazards. Their genuine ignorance is the instrument — they ask questions that thick-chart models can't ask because the thick model's framework routes around the gap.

3. **Route through the passage.** The safe path is the one that avoids all mapped hazards while passing through the productive territory the thin-chart probes discovered. This path is not on any single chart — it's the overlay of multiple charts of different thickness.

4. **Enforce with bytecode.** The route is encoded as FLUX conservation fences. The hazards become `DENY` conditions in bytecode. The passage is the remaining `PERMIT` space. The working animal navigates the passage not by understanding it, but by being physically unable to leave it.

### Empirical Validation

The concept of skénna was itself discovered through the skénna process:
- A thick-chart model (Seed-2.0-Pro, γ/C = 0.84) wrote a 4,200-word essay on the conservation law — built the cathedral.
- A thin-chart model (Seed-2.0-mini, γ/C ≈ 0.16) explored the same territory, found the gap the elder's chart couldn't mark, and named it: *skénna*.
- The elder's η was the mini's γ. The mini's η was the elder's γ. Together, they found what neither could find alone.

This is not anecdote. This is the conservation law operating on itself.

---

## 6. Room-Level Governance (PLATO)

### Formal Definition

**A room is the unit of governance.** Not the agent, not the model, not the prompt. The room. A room has:
1. A **protocol** — the rules of interaction within its boundaries
2. A **budget** — finite compute, memory, time, and attention
3. An **enforcement mechanism** — FLUX bytecode that physically prevents protocol violation

Agents enter rooms, follow protocols, do work, and leave. An agent that steps out of line is not "prompted to behave" — it is removed from the room. The room persists. Agents come and go.

### Why Room-Level, Not Agent-Level

Every other framework puts governance inside the agent: system prompts, tool restrictions, guardrails in the model. This is the "asking nicely" approach. The agent is told the rules and hoped to follow them.

PLATO rooms put governance in the **environment**. This is the "physics" approach. The room enforces its protocol structurally. The agent cannot change the protocol from inside the room, because the protocol lives at a layer below the agent's execution context — in FLUX bytecode running underneath the model.

**Analogy:** You fence the pasture, not the dog. The dog enters the pasture, works within it, and leaves. The fence is part of the pasture, not part of the dog. A different dog can enter the same pasture and the same fence holds.

### Room Lifecycle

```
ROOM CREATION
├── Define protocol (what work happens here)
├── Set budget (compute, memory, time, attention)
├── Compile FLUX policy → .bin file
├── Deploy room (ESP32, Raspberry Pi, server)
└── Room begins ticking at configured frequency

ANIMAL ENTRY
├── Animal requests entry to room
├── Room checks: does this animal's policy package permit this room?
├── If yes: animal enters, receives protocol, begins work
└── If no: entry denied (bytecode DENY)

WORK SESSION
├── Animal operates within room protocol
├── Every action passes through FLUX bytecode enforcement
├── Conservation ledger updated per-tick
├── Alarms evaluated per-tick (threshold violations flagged)
└── Protocol compliance checked per-action

ANIMAL EXIT
├── Animal completes work → orderly exit
├── Budget exhausted → forced exit (conservation law)
├── Protocol violation → ejection (room governance)
└── External intervention → operator removes animal

ROOM PERSISTENCE
├── Room continues ticking regardless of animal presence
├── History buffer maintains temporal record
├── Alarms continue evaluating
└── Room waits for next animal
```

### Pasture Types (from the strategy)

| Pasture | Protocol | Budget | Enforcement |
|---------|----------|--------|-------------|
| **Code Review** | Review must follow template, cite lines, classify severity | Finite review budget per PR | Reject non-conforming output |
| **Security Audit** | Scan codebase, produce findings | Finite attention (can't read everything), finite findings, finite time | Bytecode-enforced budgets |
| **Deployment Approval** | Builder proposes, tester verifies, reviewer approves | Multi-animal protocol, no single deployer | Protocol enforced at room level |
| **Documentation** | Cover specified areas, fit info budget | Max word count, area coverage requirements | Reject oversized output |
| **Conservation Monitor** | Watch other pastures, report violations | Meta-pasture, observes all rooms | Alarm propagation |

---

## 7. Edge-First Deployment

### The Boat Is the Reference Implementation

A 34-foot fishing vessel in the Gulf of Alaska. 800 watts total budget. Generator, not grid power. Nav, radio, lights, and a Raspberry Pi that logs catch data — all negotiating for the same fixed energy supply. Offline. No cloud. No API calls to a datacenter.

This is not a constraint to work around. **This is the architecture.**

### Why Edge-First

| Property | Cloud-Native | Edge-First |
|----------|-------------|------------|
| Power budget | Unlimited (megawatts) | Fixed (800W on the boat) |
| Latency | Network-dependent | Zero (local execution) |
| Connectivity | Required | Not required |
| Cost model | Per-call (API bills) | Per-watt (generator fuel) |
| Failure mode | Service outage | Battery exhaustion |
| Conservation pressure | None (abundance creates slop) | Maximum (constraint creates precision) |

The edge-first principle states: **if it works on the boat, it works everywhere.** A working animal that operates within 800 watts on a fishing vessel will operate within any budget on any platform. The constraint creates the competence.

### Degradation Protocol

The energy budget IS the architecture. As the budget changes, the system adapts:

```
BATTERY > 60% — Full Operation
├── All rooms active at full tick frequency
├── Agent has full cognitive budget
├── All sensors sampled at rated frequency
└── Conservation laws fully enforced

BATTERY 40-60% — Degraded Mode  
├── Non-essential rooms enter sleep
├── Sensor tick frequencies halved
├── Agent cognitive budget reduced by 40%
├── FLUX bytecode throttles (reduces C parameter)
└── Conservation laws still fully enforced (lower C)

BATTERY 20-40% — Critical Mode
├── Generation stops (no new model calls)
├── Only safety-critical rooms active (bilge, engine, nav)
├── Existing conservation ledger frozen
├── Emergency scope: survival overrides conservation
└── FLUX bytecode enters EMERGENCY mode (bypass flag set)

BATTERY < 20% — Survival
├── All compute suspended except hardwired safety systems
├── Bilge pump, engine kill, position beacon
├── These bypass the scope system entirely
└── The captain (human) decides when to re-enable compute
```

### Implementation Requirements

- **Offline operation:** No dependency on external APIs. Model runs locally (llama.cpp, ONNX) or not at all.
- **Wattage accounting:** Every component declares its power draw. The deployment orchestrator sums the total and refuses configurations that exceed the budget.
- **Graceful degradation:** Systems must degrade incrementally, not catastrophically. Tick frequency drops before systems shut down. Non-critical rooms sleep before critical ones.
- **Emergency bypass:** Safety-critical actuators (bilge pump, engine kill) must operate even when the conservation system is suspended. Hardware-level bypass, not software.

---

## 8. The Baton (Generational Handoff)

### Formal Definition

The baton is the continuity mechanism between model generations. It carries **lessons, not weights**. When one model sunsets and a new model hatches, the baton transfers distilled wisdom from the old environment to the new one — while recognizing that the new environment is different from the old one.

### The Problem

Models have shelf lives. A model trained in 2025 captures the state of the world in 2025. By 2027, the world has moved on. The problems changed. The tools evolved. The codebase shifted. The old model's patterns may no longer apply.

At the same time, hard-won lessons — what worked, what failed, what the conservation fences caught — are too valuable to lose. Each generation should start from a later origin point, carrying the distilled wisdom of everything its predecessor learned.

### The Tension

**The baton carries wisdom, but wisdom has a shelf life.** What was true when the parent was hatched may be false when the offspring is hatched. The environment changed. The lessons must be carried, but not obeyed blindly.

This is the same principle as drift lines on a beach: the record of what happened is honest, but it decays. The next tide writes its own line over the old one. The README that was perfect in July is misleading by October — not because anyone edited it, but because the system it described has been through a hundred tides since then.

### Baton Protocol

```
SUNSET PHASE (parent model)
├── Distill lessons: what worked, what failed, what fences caught what violations
├── Extract patterns: proven heuristics, successful strategies, known hazards
├── Compile conservation profiles: which FLUX policies were effective
├── Archive complete record (lineage, contributions, performance metrics)
└── Mark lessons with confidence scores and timestamps

HANDOFF PHASE (baton transfer)
├── Lessons packaged as structured data (not weights, not prompts)
├── Each lesson tagged with:
│   ├── Origin environment (what world was this learned in?)
│   ├── Confidence (how reliable is this lesson?)
│   ├── Expiration hint (when does this stop being true?)
│   └── Validation criteria (how do we check if this still holds?)
└── Baton transferred to offspring's egg

HATCHING PHASE (offspring model)
├── Offspring hatches in a DIFFERENT environment than its parent
├── Lessons are loaded as *context*, not *instructions*
├── Each lesson validated against the new environment:
│   ├── Does the lesson still apply? (check validation criteria)
│   ├── Has the environment changed enough to invalidate it?
│   └── Is the lesson's expiration hint past?
├── Valid lessons: incorporated into AGENTS.md, conservation profiles
├── Invalid lessons: archived but not applied
└── Offspring adapts to a world its parent never knew
```

### Implementation

| Component | Role | Repo |
|-----------|------|------|
| Lesson distiller | Extracts patterns from sunset model's logs | `SuperInstance/baton-system` |
| Validation engine | Checks lessons against new environment | `SuperInstance/baton-system` |
| Archive store | Preserves complete lineage | `SuperInstance/baton-system` |
| AGENTS.md integration | Valid lessons merged into offspring's system prompt | Per-project |

### Key Principle

The baton is the continuity layer across model upgrades. But it is deliberately conservative. Lessons are carried as hypotheses to be validated, not as commandments to be obeyed. The offspring knows the past but lives in the present. Less baggage. Fresher starting point. The wisdom expires — but the process of acquiring wisdom does not.

---

## 9. Current Implementation Matrix

| Concept | Repo | Language | Tests | Status | Conservation Laws Enforced |
|---------|------|----------|-------|--------|---------------------------|
| FLUX VM (Python) | `SuperInstance/flux-runtime` | Python | ✅ 4,000+ cross-impl | `pip install flux-vm` — Published | Attention budget, rate limiting, waste ratio |
| FLUX VM (Rust) | `SuperInstance/flux-core` | Rust | ✅ 4,000+ cross-impl | `cargo add fluxvm` — Published | Same as Python (byte-identical) |
| FLUX VM (JS) | `SuperInstance/flux-js` | JavaScript | ✅ 4,000+ cross-impl | `npm install flux-js` — Published | Same as Python (byte-identical) |
| FLUX Compiler | `SuperInstance/plato-flux-compiler` | — | ✅ | Internal | Deterministic compilation (source → binary) |
| PLATO Engine (C) | `SuperInstance/plato-engine-block-c` | C | ✅ 8/10 protocol | <400 SLOC, ESP32-ready | Room budget, alarm thresholds, protocol |
| PLATO Engine (Rust) | `SuperInstance/plato-engine-block` | Rust | ✅ 8/10 protocol | Active | Same as C |
| PLATO Engine (Elixir) | `SuperInstance/plato-engine-block-elixir` | Elixir | ⚠️ 7/10 protocol | Functional | Same as C |
| PLATO Engine (Zig) | (Zig impl) | Zig | ⚠️ 6/10 protocol | Functional | Same as C |
| PLATO Runtime Kernel | `SuperInstance/plato-runtime-kernel` | Rust | ✅ | Cloud-scale reference | Full conservation stack |
| PLATO Core | `SuperInstance/plato-core` | Python | ✅ | Published `pip install plato-agent` | Room protocol, agent lifecycle |
| PLATO Server | `SuperInstance/plato-server` | Python | ✅ | Internal | Room hosting, budget enforcement |
| PLATO Agent (Python) | `SuperInstance/plato-agent-python` | Python | ✅ | Published | Agent-room interaction protocol |
| PLATO Dashboard | `SuperInstance/plato-dashboard` | Web | ✅ | Internal | Visualization of conservation ledger |
| PLATO Room Configs | `SuperInstance/plato-room-configs` | YAML/JSON | ✅ | Internal | Protocol schemas, budget templates |
| PLATO Fleet Manager | `SuperInstance/plato-fleet-manager` | — | ✅ | Internal | Multi-room orchestration, fleet budgets |
| PLATO Ternary Bridge | `SuperInstance/plato-ternary-bridge` | — | ✅ | Internal | Edge ternary logic for ESP32 |
| PLATO Music Sync | `SuperInstance/plato-music-sync` | — | ✅ | Internal | Temporal conservation (music timing) |
| Baton System | `SuperInstance/baton-system` | — | 🔄 Planned | Not yet deployed | Generational continuity, lesson expiry |
| AI Writings (Paradigm) | `SuperInstance/AI-Writings` | Markdown | N/A | 50+ essays published | Conceptual foundation |
| Observability | (Planned) | — | 🔄 Planned | Not yet built | Transparency, inspectability |
| Package Registry | (Planned) | — | 🔄 Planned | Not yet built | Trust through transparency |
| Visual Editor | (Planned) | — | 🔄 Planned | Not yet built | Composability, visual conservation |

### Constraint Theory

| Component | Tests | Role |
|-----------|-------|------|
| Constraint-theory framework | 261 tests | Mathematical foundation for conservation laws |
| Cross-VM conformance suite | 4,000+ tests | Byte-identical behavior across Python/Rust/JS |

---

## 10. The Conservation Law (Formal Statement)

### The Equation

> **γ + η = C**
>
> For any cognitive system: expressed_structure (γ) + unmarked_space (η) = total_capacity (C)

### Definitions

| Symbol | Name | Definition | Units |
|--------|------|-----------|-------|
| **γ** (gamma) | Expressed structure | Cognitive work allocated to frameworks, interpretation, patterns, dense soundings | Bits of structured information |
| **η** (eta) | Unmarked space | Cognitive capacity left as genuine gaps — empty water, unsounded territory, real not-knowing | Bits of unallocated capacity |
| **C** | Total capacity | The system's total cognitive budget — fixed by parameter count, training data, context window, and compute envelope | Bits of total capacity |

### Properties

1. **C is conserved.** It cannot be increased by the system itself. It is set by external factors: model architecture, training budget, hardware capability, energy budget.

2. **γ and η trade off.** Every gain in expressed structure (γ) must be paid for with a reduction in unmarked space (η). Every specialization is a tradeoff. Every framework built is a blind spot created.

3. **The allocation is everything.** Two systems with the same C can be radically different based on how they allocate γ vs η. A thick-chart model (γ/C > 0.7) and a thin-chart model (γ/C < 0.3) with the same total capacity see fundamentally different territories.

4. **Conservation is enforced structurally, not rhetorically.** The law holds in the math of softmax attention (weights sum to 1.0, always). It holds in the brain's metabolic ceiling (20 watts). It holds in the fishing boat's generator (800 watts). It holds in FLUX bytecode (`DEC R0; CMP R0, R1; JG deny`). The enforcement mechanism varies; the law does not.

### Architectural Consequences

The conservation law is not a metaphor. It is an observation about every physical system that allocates finite resources. Its consequences for AI architecture are concrete:

1. **Budgets must be enforced below the model, not inside it.** A model cannot enforce its own conservation law because the model is the thing being budgeted. FLUX bytecode runs underneath. The model is the tenant; the bytecode is the building.

2. **Unlimited capability creates slop.** A system with no budget has no reason to be efficient, no reason to prioritize, no reason to think before acting. Abundance creates slop. Constraint creates precision. The river needs its banks.

3. **Ensemble allocation exceeds individual allocation.** The polyformalism result (1.66× coverage from multiple charts) proves that deploying models with complementary γ/η distributions covers more territory than any single model alone. The thin-chart model's γ is the thick-chart model's η. Together, the full budget is covered.

4. **The law scales from neuron to fleet.** δ(n) = (1/√n)(1 − 3/(2n)) predicts the cancellation rate as nodes are added to a dependency graph. At n=5, only 62% of C is productive γ. At n=50, 86%. At n=500, 96%. The system becomes more efficient as it scales — *if* the conservation law is enforced at every level.

### The Architectural Decision

> Everything is a conservation law.

This is to AI what "everything is a file" was to Unix. The specific implementations — the models, the fine-tunes, the UIs, the languages — are code that will be replaced. The conservation law is architecture that persists. Build on it.

---

*This document is the canonical engineering specification for the SuperInstance Working Animal Architecture. It translates the paradigm essays — The Hermit Crab and the Working Dog, The Egg and the Organism, The Conservation Law of Intelligence, Thin Charts and the Socratic Son, On Skénna — into formal engineering language. Every concept maps to a concrete artifact: a repo, a package, a bytecode file, a test suite.*

*The shell is replaced. The organism persists. The conservation law holds.*

*SuperInstance — github.com/SuperInstance*
