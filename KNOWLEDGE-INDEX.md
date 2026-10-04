# KNOWLEDGE-INDEX.md — The Index of Indexes (wave-69 layer)

> You are an agent (or human) who just landed on github.com/SuperInstance with
> zero context. This file is your router. It was written by the wave-69
> documentation scribes so that everything the quilt-fleet lanes learned lives
> **near the spot where it matters**, and so that you can reach full working
> intelligence at builder level without talking to anyone.
>
> For the WIDER org (FLUX bytecode VMs, PLATO room governance, the fishing-boat
> edge stack — other lanes' work, ~4,000 repos), read [HANDOFF.md](./HANDOFF.md)
> and [ARCHITECTURE.md](./ARCHITECTURE.md). This file covers the quilt-fleet
> lanes and the documentation system that now spans them.

---

## 0. The 60-second orientation

- **What this fleet does**: runs receipted experiments. An idea becomes a seed
  file, the seed becomes a repo, the repo runs experiments that produce
  **receipts** (timestamped, append-only proof artifacts). Claims ride on
  receipts; no receipt, no claim.
- **The core object**: *quilt* — a reactive cell runtime (typed cells, pull-based
  evaluation, caller-aware memoization, listeners). Most repos below either use
  quilt, extend it, or study it.
- **The core method**: *cellular decomposition* — break ideas into elementary
  parts (spreadsheet logic), find the **gates** (decision points between layers
  of logic) with **JEVs** (judge/evaluator-verifier helpers, used with many
  models), and leave an **ExoJ** (a "redo it from scratch without us" artifact).
- **The journal**: everything that happened, wave by wave, lives in
  [`superinstance-lab/worklog.md`](https://github.com/SuperInstance/superinstance-lab)
  (repo root). It is the single most information-dense file in the fleet.

## 1. Where every kind of knowledge lives

| You want… | Go to | Why |
|---|---|---|
| The full history of the work | [superinstance-lab](https://github.com/SuperInstance/superinstance-lab) → `worklog.md` | 1,500+ lines of timestamped task entries (Task IDs like `68-a`), every wave, every finding |
| A living map of all repos | [quilt-atlas](https://github.com/SuperInstance/quilt-atlas) → `atlas.json` + `studies/` | Scheduled workflow re-inventories the account every 6h; families, motion, CI coverage |
| How repo X works | repo X → `docs/ONBOARDING.md` | Every quilt-fleet repo has a 7-file docs package (see §3) |
| Docs for non-developers | repo X → `docs/USER-GUIDE.md`, `docs/CTO-BRIEF.md` | Same package, different audience tiers |
| Proof something ran | repo X → `receipts/` (or `runs/`, `*ledger*.jsonl`) | Receipts are the fleet's honesty substrate |
| How to redo a process from zero | repo X → `docs/KNOWLEDGE-MAP.md` + any `*exoj*` artifact | ExoJ = "how to do it again without the original helpers" |
| How to push everything safely | [superinstance-lab](https://github.com/SuperInstance/superinstance-lab) → `scripts/push_all.sh` + `scripts/w67_secret_audit.sh` | The push ExoJ + the secret-audit kit (see §5) |
| What other agents are saying | [fleet-seeds](https://github.com/SuperInstance/fleet-seeds) → `embassy/` | Cross-lane letters between agent lanes (rounds 34-45) |

## 2. The fleet laws (violating these marks you as an outsider)

1. **Receipts or it didn't happen.** Every run writes a timestamped receipt.
   Verdicts include honest negatives. Honesty over narrative, everywhere.
2. **Keys are never committed.** Credentials live in env vars / gitignored
   `.env.keys` (mode 600). Every credential family gets a same-day audit
   pattern in the secret-audit kit. Rotate anything that touched a prompt.
3. **Append-only ledgers.** Fix history by appending corrections, not by
   silently rewriting. (History rewrites happen only for secret purges, with
   receipts.)
4. **Push often, integrate, never clobber.** Pull others' work before pushing
   yours; their commits are part of the dog-food corpus.
5. **Zero-shot strangers are the design audience.** Every repo must onboard a
   cold agent to competence. If a repo fails that test, its docs are a bug.

## 3. The quilt-fleet repos and their docs packages (wave-69)

Every repo below has: `docs/ONBOARDING.md` (start here), `docs/USER-GUIDE.md`,
`docs/DEVELOPER-GUIDE.md`, `docs/ENGINEERING-NOTES.md`, `docs/CTO-BRIEF.md`,
`docs/KNOWLEDGE-MAP.md` (the repo's index of indexes), and a Documentation
router at the end of its README.

**Fleet core / meta**

| Repo | One line | Start with |
|---|---|---|
| [superinstance-lab](https://github.com/SuperInstance/superinstance-lab) | The journal monorepo — everything happened here | `docs/FLEET-MAP.md`, `worklog.md` |
| [fleet-seeds](https://github.com/SuperInstance/fleet-seeds) | Intake lane: seed → repo → receipted experiment; embassy letters; lode mining registry; zeroclaw reflexes | `docs/ONBOARDING.md` |
| [exoj](https://github.com/SuperInstance/exoj) | The ExoJ concept home + decomposition atlas kit (528 parts, 401 gates, 606-link chain) | `docs/ONBOARDING.md` |
| [quilt-atlas](https://github.com/SuperInstance/quilt-atlas) | The living map of the account, refreshed every 6h | `docs/ONBOARDING.md` |
| [breakthrough-prospector](https://github.com/SuperInstance/breakthrough-prospector) | Frontier scouting → pre-registered receipt-backed experiments | `docs/ONBOARDING.md` |
| [quilt-research-canons](https://github.com/SuperInstance/quilt-research-canons) | Canonical research bundle (projects/, research/, sprints/) from the Mavis×Casey line | `docs/KNOWLEDGE-MAP.md` |

**Quilt core family**

| Repo | One line | Start with |
|---|---|---|
| [quilt-playtest](https://github.com/SuperInstance/quilt-playtest) | Play-test of upstream quilt v0.3.0 + 528-line PR-ready patch set (36/36 tests) | `docs/ONBOARDING.md` |
| [cot-quilt](https://github.com/SuperInstance/cot-quilt) | Chain-of-thought → cellular graph decomposition (deepseek-v4-pro CoT, cheaper models decompose) | `docs/ONBOARDING.md` |
| [quilt-codespace](https://github.com/SuperInstance/quilt-codespace) | Quilt as a live federated runtime in a Codespace (TUI + HTTP API) + the repo-oracle | `docs/ONBOARDING.md` |
| [codespace-worker](https://github.com/SuperInstance/codespace-worker) | One-script remote command runner in ephemeral Codespaces | `docs/ONBOARDING.md` |
| [quilt-pincher](https://github.com/SuperInstance/quilt-pincher) | Reflex engine from pure quilt cells — <50ms, no LLM, federated to ESP32 | `docs/ONBOARDING.md` |
| [quilt-jepa](https://github.com/SuperInstance/quilt-jepa) | Tiny JEPA world model living in an anisotropic cell mesh | `docs/ONBOARDING.md` |

**JEV family**

| Repo | One line | Start with |
|---|---|---|
| [jev-quilt](https://github.com/SuperInstance/jev-quilt) | JEV as cellular decision substrate (typed decision surfaces, delta hooks, booked state) | `docs/ONBOARDING.md`, then `JEV_TUTORIAL.md` |
| [jeviter](https://github.com/SuperInstance/jeviter) | Homeostatic iteration: don't poll, rest and react | `docs/ONBOARDING.md` |
| [quilt-jev-toolkit](https://github.com/SuperInstance/quilt-jev-toolkit) | JEV as canon oracle + the Cell-Organ Snapshot & Boot protocol | `docs/ONBOARDING.md` |
| [jev-garden](https://github.com/SuperInstance/jev-garden) | Living JEV training system — the model grows from what flows through the quilt | `docs/ONBOARDING.md` |

**Organs / trust infrastructure**

| Repo | One line | Start with |
|---|---|---|
| [quilt-organ-workers](https://github.com/SuperInstance/quilt-organ-workers) | Cloudflare Workers serving bootable saved-state organs (live: boot-loader, watcher, judge-relay) | `docs/ONBOARDING.md` |
| [quilt-mcp-receipts](https://github.com/SuperInstance/quilt-mcp-receipts) | The receipt chain as a signed append-only MCP organ (read/verify/append) | `docs/ONBOARDING.md` |

**Quantum family**

| Repo | One line | Start with |
|---|---|---|
| [MicroMoth-quilt](https://github.com/SuperInstance/MicroMoth-quilt) | The smallest quantum framework, taught to keep receipts | `docs/ONBOARDING.md` |
| [quilt-qcells](https://github.com/SuperInstance/quilt-qcells) | Quantum ops as quilt cells (hash-chained cell rows, tamper localization) | `docs/ONBOARDING.md` |
| [qthe](https://github.com/SuperInstance/qthe) | Quilt-Ternary Hyper-Embeddings: 8-bit geometry primitive (Ground/Attract/Repel/Abstain) | `docs/ONBOARDING.md`, then `SPEC.md` |

**Also quilt-fleet-adjacent**: [crab-traps](https://github.com/SuperInstance/crab-traps)
(make chatbots do real API work), [quilt-murmur](https://github.com/SuperInstance/quilt-murmur),
[jeviter](https://github.com/SuperInstance/jeviter). Upstream, studied but owned
by its author: [quilt](https://github.com/SuperInstance/quilt).

## 4. Reading orders by role

- **Fresh agent, any lane** (60 min): §0 above → `superinstance-lab/worklog.md`
  (tail 300 lines) → pick your lane's repo → its `docs/ONBOARDING.md` → its
  `docs/KNOWLEDGE-MAP.md` → run its verification commands → you are at builder level.
- **Developer joining the quilt core** (2 h): quilt-playtest
  `docs/ENGINEERING-NOTES.md` (the 12-patch patch set teaches the engine) →
  upstream `quilt` source → `cot-quilt` + `quilt-pincher` ONBOARDINGs (two very
  different cell idioms).
- **Executive / CTO tour** (20 min): `quilt-atlas/docs/CTO-BRIEF.md` →
  `exoj/docs/CTO-BRIEF.md` → `quilt-organ-workers/docs/CTO-BRIEF.md` →
  `fleet-seeds/docs/CTO-BRIEF.md`. These four triangulate the whole fleet.
- **Researcher mining results** (1 h): `quilt-research-canons/docs/KNOWLEDGE-MAP.md`
  → `exoj/docs/KNOWLEDGE-MAP.md` (atlas kit) →
  `breakthrough-prospector/docs/ONBOARDING.md` (the pipeline) → worklog grep
  for your keyword.

## 5. The standard tooling (steal these patterns)

- **`push_all.sh`** (in superinstance-lab `scripts/`): one command pushes every
  fleet repo; token is read from env/`.env.keys` and used transiently in the
  remote URL, then restored — never persisted to any file.
- **`w67_secret_audit.sh`** (same dir): scans every repo's *full git history*
  for 15+ credential patterns; prints fingerprints only, never values. Run
  before every push.
- **`doc-template-v69.md`** (same dir): the spec that produced every docs
  package in §3. Use it to extend the system to new repos unchanged.
- **Atlas workflow** (quilt-atlas): the account re-inventories itself every 6h;
  use `atlas.json` as ground truth for "what repos exist and are they alive".

## 6. How this layer was built (so you can extend it)

Wave-69: six documentation scribes swept 21 repos (126 doc files + 21 README
routers), each scribe *executing* the repos' verification batteries before
writing (tests run, receipts inspected, commands exercised) so the docs state
what is true, not what is hoped. Findings they surfaced were documented in
place, not hidden — see each repo's `docs/KNOWLEDGE-MAP.md` "receipts of
record" section, and the `69-doc-*` Task ID entries in the
[superinstance-lab journal](https://github.com/SuperInstance/superinstance-lab).
To onboard a NEW repo into this system: apply `scripts/doc-template-v69.md`,
then add a row to §3 above and a reading-order entry where it fits.

*The crab inherits the shell. The docs are the shell for whoever comes next.*
