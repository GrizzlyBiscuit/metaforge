# Build your own Metaforge at home, for free

Everybody wants a Jarvis. You do not have to be a billionaire in a comic book to build one.

This file starts a chat, learns your household, builds a profile for each person, builds a roadmap from the conversation, then builds itself into a command center. From one click to a home AI with RSI, for free.

## Use it

Open `index.html` in a browser. That is the whole install.

1. The file chats with you: how many people live in your household, their names, what each person wants help with.
2. It builds a profile for each person.
3. It builds a roadmap from the conversation: the file knows the end goal — a command center that runs your household — and lays out the road to it, one phase per thing you asked for, in the order you asked for it. You watch the phases appear, marked Built, Next, or Queued, with a progress count.
4. It builds itself into a command center around those profiles and the roadmap. The chat is now just one option inside it, alongside the daily brief, the profiles, and the tools it builds next — and the tiles carry the conversation, not placeholders.

No account. No cloud. No subscription. Nothing leaves the machine the file runs on.

## How it works on a potato

The chat runs on a script, so it works right now with no download. A small model makes it understand free text instead of just accepting answers, and it is optional: click **Load the small AI model** and the file pulls a tiny quantized model (Qwen2.5-0.5B-Instruct, about 300 MB, cached after the first time) that runs in the browser.

- **Level 1 — WASM.** Runs on any machine, even a potato. Slow, but the chat gives short answers, so it feels fine.
- **Level 2 — WebGPU.** The same model, the same file, no re-download. When the machine has WebGPU the file uses it instead, roughly five to ten times faster.

The model is fine-tuned for this one job — guiding the build — so it does not need to be big. A 0.5B model is enough for a guided conversation.

## The tiers

The file is the seed. The tiered plan grows it, step by step, into the full stack:

1. **The file.** A chat in the browser, profiles for the household, a command-center skeleton.
2. **A local model server.** The same small model, or a bigger one, on the household PC. Faster, and it runs around the clock.
3. **The full stack.** A model router, a local chat page, a phone app, scheduled daily briefs, tools and plugins becoming part of the household's own stack.
4. **The pool.** A household with two consumer GPUs splits models across them. The stack itself runs on one.

Each tier is a step up, not a restart. The file you start with is the file that grows.

## The method

Higher-level engineering through AI prompting. You do not have to know how to code to code anymore — you have to carry a concept end to end through a metaphor. A metaphor holds the design in one image. Hold it steady and the model builds from it; let it drift and the build drifts. Anyone who can think clearly in metaphors can build. See [docs/METHOD.md](docs/METHOD.md).

## How this was built

100% of the infrastructure behind this was first built by free cloud models, working from open-source software, on hardware the household already owned. No paid services. This repo is the product in repeatable form: the file, the plan, and the method, so any household can do the same.

## Status

Beginning. The file is the seed and it works: the chat, the profiles, the roadmap, and the command-center build-out are live in `index.html`. The model integration, the scheduled briefs, and the tools are the next tiers. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for what is built and what is next.

## License

MIT. See [LICENSE](LICENSE).
