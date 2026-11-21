# Architecture

The product is a file that builds itself. This document describes how it works now, and how it grows.

## The file

`index.html` is the whole product at level 1. A single file, no build step, no server, no install. Open it in a browser.

It has four parts:

1. **The chat.** A state machine that walks you through the setup: how many people it should know about, their names, what each person would like help with. The script is the backbone, so the chat works with no download at all.
2. **The profiles.** One profile per person, built from the chat. Names and wants, shown as cards, carried into the command center.
3. **The roadmap.** The plan, built from the conversation. The file knows the end goal — your own capable assistant — and lays out the road to it: the profiles and the center marked Built, one phase per thing you asked for (first marked Next, the rest Queued, in the order they were asked), and the full command center at the end as the goal itself. The phases appear one by one so you watch the plan assemble, with a progress count (two of five built, the rest queued).
4. **The command center.** Once the profiles are confirmed, the file rebuilds its own page: the roadmap assembles, the chat moves inside as one panel, and the daily brief, profiles, and tools appear around it — with the tiles carrying the conversation (the brief tile names who asked for it, the tools tile lists what you asked for) instead of placeholders. The chat was the start; now it is one option inside the thing it built.

## The model

The chat understands free text through a small in-browser model, loaded on demand:

- **Model:** Qwen2.5-0.5B-Instruct, quantized, served through Transformers.js (ONNX Runtime Web).
- **WASM.** The default. Runs on any machine, including a potato. A few tokens a second, which is enough because the chat gives short answers.
- **WebGPU.** The same model file, the same code path, a different execution provider. When `navigator.gpu` reports WebGPU, the file uses it. Roughly five to ten times faster than WASM. No re-download, no new model.
- **Fallback.** If the model cannot load (offline, unsupported browser, no WebGPU and slow WASM), the script keeps working. The model is an enhancement, never a gate.

The model is chosen for the job, not for generality: it guides a build script. A 0.5B model is enough for that. Larger models are a later level, not a requirement.

## The levels

Each level is a capability, not a piece of hardware. The file you start with is the file that grows.

1. **Level 1 — It talks.** Chat + profiles + command-center skeleton, script only. Any PC, in the browser.
2. **Level 2 — It understands.** The small model loads in the browser and the file can actually chat — free text understood, not just accepted.
3. **Level 3 — It remembers.** Profiles, wants, and the road so far persist across sessions and shape what it says.
4. **Level 4 — It does things.** Breakout: tell it to do something and it does it. Briefs, reminders, the next phase on the roadmap.
5. **Level 5 — It reaches further.** A bigger model, anywhere you put it — a model server on a machine you own, or any OpenAI-compatible endpoint. The file is the front end.
6. **Level 6 — It works while you are away.** Scheduled briefs and reminders that fire on their own clock, without the browser open.
7. **Level 7 — It grows itself.** Every thing you ask for becomes part of it. The roadmap never ends; the file improves itself one request at a time.

A home PC running local models, a model router, a local chat page, and a phone app is one way to live at the higher levels — it is the proving ground this project was built on, used daily. But it is not the levels. The levels are what the companion can do, on whatever the person already has. The file is how anyone gets there from one click.

## Data

Profiles live in the page. Nothing is sent anywhere: no account, no telemetry, no cloud call. The model weights download once from the model host and are cached by the browser. At level 5 and above, the model runs on hardware you own.

## What is built, what is next

Built now (level 1, with level 2 and 4 in the file):

- Chat flow: how many people, names, wants, confirmation.
- Profiles: built from the chat, shown as cards, carried into the command center.
- Roadmap: built from the conversation, phases marked Built / Next / Queued, assembled one by one for you to watch, with a progress count toward the end goal.
- Command-center build-out: the chat becomes one panel; daily brief, profiles, and tools appear with the conversation in them, not placeholders.
- Model hook: Transformers.js + Qwen2.5-0.5B-Instruct, loaded on demand, WASM with WebGPU when available, script fallback when it cannot load.
- Open chat with the small model (level 2) and the breakout that lets it do things (level 4): free text that is not a command goes to the model as a real conversation, with the people it knows in the prompt.

Next:

- Scheduled daily briefs (the brief panel builds a real brief from the profiles).
- Tools and plugins (each one the file adds becomes part of the stack).
- Memory across sessions (level 3): profiles, wants, and the road so far persist and shape what it says.
- Reaching further (level 5) and working while you are away (level 6): a bigger model anywhere you put it, and scheduled work on its own clock.
