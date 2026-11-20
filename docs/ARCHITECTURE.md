# Architecture

The product is a file that builds itself. This document describes how it works now, and how it grows.

## The file

`index.html` is the whole product at tier 1. A single file, no build step, no server, no install. Open it in a browser.

It has four parts:

1. **The chat.** A state machine that walks the household through the setup: how many people, their names, what each person wants help with. The script is the backbone, so the chat works with no download at all.
2. **The profiles.** One profile per person, built from the chat. Names and wants, shown as cards, carried into the command center.
3. **The roadmap.** The plan, built from the conversation. The file knows the end goal — a command center that runs the household — and lays out the road to it: the profiles and the center marked Built, one phase per thing the household asked for (first marked Next, the rest Queued, in the order they were asked), and the full command center at the end as the goal itself. The phases appear one by one so the household watches the plan assemble, with a progress count (two of five built, the rest queued).
4. **The command center.** Once the profiles are confirmed, the file rebuilds its own page: the roadmap assembles, the chat moves inside as one panel, and the daily brief, profiles, and tools appear around it — with the tiles carrying the conversation (the brief tile names who asked for it, the tools tile lists what the household asked for) instead of placeholders. The chat was the start; now it is one option inside the thing it built.

## The model

The chat understands free text through a small in-browser model, loaded on demand:

- **Model:** Qwen2.5-0.5B-Instruct, quantized, served through Transformers.js (ONNX Runtime Web).
- **Level 1 — WASM.** The default. Runs on any machine, including a potato. A few tokens a second, which is enough because the chat gives short answers.
- **Level 2 — WebGPU.** The same model file, the same code path, a different execution provider. When `navigator.gpu` reports WebGPU, the file uses it. Roughly five to ten times faster than WASM. No re-download, no new model.
- **Fallback.** If the model cannot load (offline, unsupported browser, no WebGPU and slow WASM), the script keeps working. The model is an enhancement, never a gate.

The model is chosen for the job, not for generality: it guides a build script. A 0.5B model is enough for that. Larger models are a later tier, not a requirement.

## The tiers

Each tier is a step up from the one before, not a restart. The file you start with is the file that grows.

| Tier | What runs | Where |
|---|---|---|
| 1 — The file | Chat + profiles + command-center skeleton, model in-browser (WASM, WebGPU when available) | Any PC, in the browser |
| 2 — Local server | The same model, or a bigger one, served locally (llama.cpp) so it runs around the clock | The household PC |
| 3 — Full stack | Model router, local chat page, phone app, scheduled daily briefs, tools and plugins | The household PC + phone |
| 4 — The pool | Models split across two consumer GPUs when the household has them | The household PC |

The stack at tier 3 and 4 is the proving ground this project was built on: a home PC running local models, a model router, a local chat page, and a phone app, used daily by one household. The file is how any household gets there from one click.

## Data

Profiles live in the page. Nothing is sent anywhere: no account, no telemetry, no cloud call. The model weights download once from the model host and are cached by the browser. At tier 2 and above, the model runs on the household's own hardware.

## What is built, what is next

Built now (tier 1):

- Chat flow: household size, names, wants, confirmation.
- Profiles: built from the chat, shown as cards, carried into the command center.
- Roadmap: built from the conversation, phases marked Built / Next / Queued, assembled one by one for the household to watch, with a progress count toward the end goal.
- Command-center build-out: the chat becomes one panel; daily brief, profiles, and tools appear with the conversation in them, not placeholders.
- Model hook: Transformers.js + Qwen2.5-0.5B-Instruct, loaded on demand, WASM with WebGPU when available, script fallback when it cannot load.

Next:

- Scheduled daily briefs (the brief panel builds a real brief from the profiles).
- Tools and plugins (each one the file adds becomes part of the stack).
- A local-server tier (tier 2) so the model runs around the clock without the browser open.
- The full stack reference (tier 3/4): model router, chat page, phone app.
