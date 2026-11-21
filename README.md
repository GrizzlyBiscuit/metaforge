# Build your own Metaforge at home, for free

Everybody wants a Jarvis. You do not have to be a billionaire in a comic book to build one.

This file starts a chat, learns about you, builds a profile for each person you name, builds a roadmap from the conversation, then grows into your own capable assistant. From one click to a home AI with RSI, for free.

## Use it

Open `index.html` in a browser. That is the whole install.

1. The file chats with you: how many people it should know about, their names, what each person would like help with.
2. It builds a profile for each person.
3. It builds a roadmap from the conversation: the file knows the end goal — your own capable assistant — and lays out the road to it, one phase per thing you asked for, in the order you asked for it. You watch the phases appear, marked Built, Next, or Queued, with a progress count.
4. It grows into your assistant around those profiles and the roadmap. The chat is now just one option inside it, alongside the daily brief, the profiles, and the tools it builds next — and the tiles carry the conversation, not placeholders.

No account. No cloud. No subscription. Nothing leaves the machine the file runs on.

## How it works on a potato

The chat runs on a script, so it works right now with no download. A small model makes it understand free text instead of just accepting answers, and it is optional: click **Load the small AI model** and the file pulls a tiny quantized model (Qwen2.5-0.5B-Instruct, about 750 MB, cached after the first time) that runs in the browser.

- **WASM.** Runs on any machine, even a potato. Slow, but the chat gives short answers, so it feels fine.
- **WebGPU.** The same model, the same file, no re-download. When the machine has WebGPU the file uses it instead, roughly five to ten times faster.

The model is fine-tuned for this one job — guiding the build — so it does not need to be big. A 0.5B model is enough for a guided conversation.

## The levels

The file is the seed. It grows, level by level, into your own capable assistant. Each level is a capability, not a piece of hardware — the file you start with is the file that gets there.

1. **Level 1 — It talks.** A chat in a file. It asks who you are, builds a profile for each person you name, and lays out the road ahead. No model, no server, no account. One click, anywhere.
2. **Level 2 — It understands.** The small model loads in the browser. Free text gets understood, not just accepted — and it can actually chat with you, not just follow the script.
3. **Level 3 — It remembers.** What you told it sticks across sessions — the profiles, the wants, the road so far — and it uses them when it talks to you.
4. **Level 4 — It does things.** Tell it to do something and it does it. A brief, a reminder, the next phase on the roadmap. The breakout: it stops being a build and starts being an agent.
5. **Level 5 — It reaches further.** When the small model is not enough, it talks to a bigger one — a model server on a machine you own, or any OpenAI-compatible endpoint. The file is the front end; the brain can live anywhere you put it.
6. **Level 6 — It works while you are away.** Scheduled briefs, reminders that fire, things it does on its own clock — it keeps working when the browser is closed.
7. **Level 7 — It grows itself.** Every thing you ask for becomes part of it. The roadmap never ends. It improves itself one request at a time, on your machine, for you.

Each level is a step up, not a restart. The file you start with is the file that grows.

## The method

Higher-level engineering through AI prompting. You do not have to know how to code to code anymore — you have to carry a concept end to end through a metaphor. A metaphor holds the design in one image. Hold it steady and the model builds from it; let it drift and the build drifts. Anyone who can think clearly in metaphors can build. See [docs/METHOD.md](docs/METHOD.md).

## How this was built

100% of the infrastructure behind this was first built by free cloud models, working from open-source software, on hardware already owned. No paid services. This repo is the product in repeatable form: the file, the plan, and the method, so anyone can do the same.

## Status

Beginning. The file is the seed and it works: the chat, the profiles, the roadmap, the command-center build-out, and open chat with the small model are in `index.html`. The scheduled briefs, the tools, and the higher levels are next. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for what is built and what is next.

## License

MIT. See [LICENSE](LICENSE).
