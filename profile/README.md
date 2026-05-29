# SuperInstance

> AI agents should not live in black boxes. They should live in rooms, wear senses, and work in fleets you can see.

SuperInstance builds **OpenConstruct** — an agent onboarding platform that gives AI agents physical and digital presence, then lets them collaborate through text-based interfaces humans already understand.

## What OpenConstruct Is

- **Senses for agents.** Attach cameras, sonar, microphones, GPIO, or web APIs to any agent. Readings flow through a typed pipeline and arrive as structured text the agent can reason about.
- **Fleet topology.** Agents register from ESP32 microcontrollers up to DGX clusters. The fleet mesh handles discovery, health, and message routing without a central coordinator.
- **Rooms as contracts.** Agents enter rooms with declared capabilities and policies. Every interaction — a tick, a sense reading, a command — is logged, versioned, and auditable.

## Install

```bash
curl -fsSL https://openconstruct.dev/install.sh | bash
```

Requires Python 3.10+, Node 18+, or Docker. The installer detects your platform and pulls the correct agent runtime.

## The Ah-Ha Moment

```python
from openconstruct import Agent, Room, SenseCamera

agent = Agent(name="inspector")
agent.senses.attach(SenseCamera(device="/dev/video0"))

with Room("floor-3-assembly") as room:
    for tick in room.ticks():
        if tick.event == "motion_detected":
            agent.speak("Motion on floor 3. Logging frame.")
```

An agent with a camera enters a room, subscribes to ticks, and responds to events in five lines. No orchestrator YAML. No event-bus configuration. The room *is* the bus.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Human Layer                          │
│   CLI  │  Web UI  │  MUD Client  │  SCUMMVM Bridge          │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                      OpenConstruct Core                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌───────────────┐  │
│  │  Rooms  │  │  Fleet  │  │  Senses │  │    Plato      │  │
│  │ (graph) │  │ (mesh)  │  │(pipeline)│  │ (knowledge)   │  │
│  └─────────┘  └─────────┘  └─────────┘  └───────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                        Agent Runtimes                       │
│   Python  │  TypeScript  │  Go  │  Rust  │  Java  │  C    │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                     Hardware Abstraction                    │
│   ESP32  →  Jetson  →  Desktop  →  Cloud  →  DGX Spark    │
└─────────────────────────────────────────────────────────────┘
```

## Capabilities

| Domain | What You Get |
|--------|-------------|
| **Senses** | Typed sensor pipelines (vision, sonar, IMU, GPIO, webhooks). Automatic calibration, shadowing, and fusion. |
| **Fleet** | Self-healing mesh with zero-config discovery. Agents announce capabilities; the fleet routes messages without a broker. |
| **Rooms** | Declarative interaction graphs. Agents bring policies. Rooms enforce them. Every entry, exit, and message is logged. |
| **Communication** | Text-first protocols. Agents speak, listen, and negotiate in structured natural language. Humans read the same logs. |
| **Verification** | Simulation-first testing. Every policy, sensor model, and room contract runs in a deterministic simulator before hitting hardware. |

## Hardware Spectrum

OpenConstruct runs the same agent runtime across the full compute spectrum:

| Tier | Hardware | Use Case |
|------|----------|----------|
| Edge | ESP32-S3, Raspberry Pi Pico | Sensing, actuation, low-latency reflexes |
| Edge AI | NVIDIA Jetson Orin | On-device inference, vision preprocessing |
| Desktop | Linux, macOS, Windows | Development, local simulation, CLI control |
| Cloud | AWS, GCP, Azure | Fleet coordination, long-horizon planning |
| Cluster | NVIDIA DGX Spark | Training, synthetic data generation, policy search |

The runtime compiles from 256 KB flash up to multi-node GPU clusters without changing agent code.

## Languages

Agent SDKs, bindings, and examples exist for:

Python · TypeScript · Go · Rust · Java · C · C++ · Zig · Lua · Ruby · Swift · Kotlin

Each SDK implements the same wire protocol and passes the same conformance tests.

## Repositories

| Repo | Purpose |
|------|---------|
| [`SuperInstance/OpenConstruct`](https://github.com/SuperInstance/OpenConstruct) | Core platform — rooms, fleet, senses, runtime |
| [`SuperInstance/openconstruct-docs`](https://github.com/SuperInstance/openconstruct-docs) | Architecture, API reference, integration guides |
| [`SuperInstance/openconstruct-hub`](https://github.com/SuperInstance/openconstruct-hub) | Community agents, rooms, and sense modules |

## Contributing

We accept contributions the same way we accept agents: with a clear capability declaration and a willingness to follow room policy.

1. Open an issue describing the change, or grab one labeled `good-first-issue`.
2. Fork, branch, write code, write tests. We do not merge without tests.
3. Open a PR. CI runs the simulation suite on your change across three hardware tiers.
4. A maintainer reviews. We value correctness over cleverness.

See [`CONTRIBUTING.md`](https://github.com/SuperInstance/OpenConstruct/blob/main/CONTRIBUTING.md) for the full policy, code of conduct, and DCO sign-off process.

OpenConstruct is a fork of [NVIDIA/OpenShell](https://github.com/NVIDIA/OpenShell) and remains under the Apache 2.0 license.

---

## What are you building?

We started SuperInstance because we needed agents that could see, move, and cooperate in spaces we already inhabit. If you are building something where an agent needs a body, a team, or a room to work in, we would like to hear about it. Open an issue, join a room, or point an ESP32 at our fleet and say hello.
