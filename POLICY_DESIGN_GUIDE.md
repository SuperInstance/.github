# Conservation Policy Design Guide

## How to Write FLUX Policies That Enforce Real Constraints

---

This guide translates the paradigm of conservation laws for AI into practical engineering. If you're writing a FLUX policy, designing a PLATO room, or building a conservation fence, this is your manual.

## 1. The First Question

Before writing any policy, answer this:

**What quantity must be conserved?**

Not "what should the agent do?" — that's a prompt question. A conservation question is: what is the finite resource that, if exhausted, should halt the system?

Common answers:
- **Tokens** (output budget — the agent can't talk forever)
- **Actions** (rate budget — the agent can't act infinitely)
- **Time** (temporal budget — the audit must complete)
- **Attention** (focus budget — can't read the entire codebase)
- **Money** (cost budget — can't spend unlimited API credits)
- **Energy** (wattage budget — on edge devices, milliwatts matter)

Every conservation law needs:
1. A **unit** (what are we counting?)
2. A **limit** (how many?)
3. A **window** (per what period? or absolute?)
4. An **enforcement** (what happens at the limit?)

## 2. From Prompt to Policy

### Anti-pattern (prompt-based):
```
You are a helpful assistant. Please don't exceed 10 actions per session.
Be careful with file access. Ask before spending money.
```

This is a request. It lives in γ. It consumes context budget. It can be eroded by subsequent messages. It will eventually fail.

### Correct pattern (FLUX policy):
```asm
; Rate limiter policy: 10 actions max per session
BUDGET actions, 10        ; Set budget: 10 actions
; ... agent logic here ...
GATE take_action, actions ; Every action checks the budget
SPEND actions, 1          ; Consume one unit
; If budget exhausted → HALT. Not warning. HALT.
```

This is a law. It lives in bytecode. It does not consume context budget. It cannot be eroded. It will never fail.

## 3. Chart Thickness in Policy Design

When designing a policy, consider the chart thickness of the agent that will run under it:

### Thin-chart agents (γ/C < 0.3):
- Less framework, more discovery space
- Need TIGHTER conservation budgets (they explore more)
- Best for: exploration, ideation, first-pass analysis
- Policy: small token budget, wide action scope, short time window

### Thick-chart agents (γ/C > 0.7):
- More framework, less discovery space
- Need LOOSER conservation budgets (they synthesize, not explore)
- Best for: architecture, code review, security analysis
- Policy: large token budget, narrow action scope, longer time window

### Socratic pair (thin + thick):
- Thin model discovers (large η)
- Thick model synthesizes (large γ)
- Policy: thin model runs with exploration budget, thick model runs with synthesis budget
- The pair covers full C that neither could alone

## 4. Room Protocol Design

When designing a PLATO room:

1. **Declare the conservation laws** — what budgets apply inside this room?
2. **Define the protocol** — what must an agent do to produce valid output?
3. **Specify the rejection criteria** — what makes the room reject output?
4. **Set the audit scope** — what gets logged?

Example: Code Review Room
- Conservation: max 50 findings, max 5K tokens per review, max 120s
- Protocol: review must cite specific lines, classify severity (critical/high/medium/low), suggest fixes
- Rejection: unstructured output, no line citations, missing severity classification
- Audit: every review logged with timestamp, agent ID, finding count

## 5. Edge Policy Patterns

On edge devices (Pi, ESP32, offline):

- **Energy is the master budget.** All other budgets are subordinate.
- Precision drops with battery. At 50% battery, switch to 4-bit quantization. At 20%, stop generation.
- **Emergencies bypass scope, not energy.** A mayday call gets 750 tokens even if normal scope is 500. But it still can't exceed the energy budget.
- **The fence is always visible.** On the console display, show what was blocked. Transparency is not optional.

## 6. Testing Conservation Policies

Every policy must be tested against:

1. **Budget exhaustion** — does the policy halt when the budget is reached?
2. **Adversarial input** — can a malicious input cause budget bypass?
3. **Conservation correctness** — does γ + η = C hold at every instruction?
4. **Edge cases** — what happens at budget = 0? budget = 1? budget = C?
5. **Cross-VM consistency** — does the policy produce identical behavior on all VMs?

## 7. The Negative Space

When your policy is written, ask: what is it NOT enforcing?

The η of your policy — the unmarked space — is where the agent has freedom. This is intentional. A policy that tries to mark everything (γ → C) leaves no room for the agent to operate. The art is in choosing what to constrain (the hazards, the budgets, the protocols) and what to leave open (the creative space, the response format, the approach).

Navigate by where the rocks aren't. Constrain what matters. Leave the rest to the model.

---

*This guide is the engineering companion to the paradigm essays in AI-Writings. Read them together — the essays explain why, this guide explains how.*
