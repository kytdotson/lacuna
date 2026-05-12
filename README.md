# Lacuna

> *An agentic productivity environment — a living, animated room on your screen where a void-spirit assistant helps you find files, launch apps, and talk to AI, wrapped in a slightly gothic cartoon skin.*

Lacuna reimagines the desktop as an inhabited space: a modernist apartment, subtly wrong, with something watching from the corner. Your assistant — **Shoelace**, a chthonic mollusc-jellyfish-kitsune who has decided to look like a fox — moves through the room, perches on window edges, and acts as the primary interface between you and your tools.

It is Microsoft Bob if Bob had been designed by someone who read too much Borges.

*This project is currently a thought and design experiment. It is in semi-active development with feedback from beta users*

---

## Current Status

**Phase 0 — Foundations.** Repository scaffolded. Documentation in progress. Nothing on screen yet that would alarm you.

See the [Phase Roadmap](docs/04-phase-roadmap.md) for current progress.

---

## Documentation

| Document | Description |
|---|---|
| [Room & Interface Requirements](docs/01-room-interface-requirements.md) | Layout, objects, chat system, gesture vocabulary |
| [Technical Stack](docs/02-technical-stack.md) | Framework decisions and rationale |
| [Shoelace Character Spec](docs/03-shoelace-character-spec.md) | Visual design, animation states, personality — *in progress* |
| [Phase Roadmap](docs/04-phase-roadmap.md) | Milestones across all phases |

---

## Architecture Overview

```
lacuna/
├── src/                        # Svelte frontend
│   ├── App.svelte              # Root component — composes all layers
│   ├── main.js                 # Entry point
│   ├── lib/
│   │   ├── room/               # Room environment components
│   │   ├── shoelace/           # Character rendering, state machine, gestures
│   │   ├── chat/               # Conversation store, bubble + sidebar logic
│   │   ├── audio/              # Howler.js audio manager
│   │   └── llm/                # Anthropic API streaming client
│   ├── components/             # Shared UI components
│   ├── stores/                 # Global Svelte stores
│   └── assets/                 # Sprites, backgrounds, audio, icons
├── server/                     # Node.js + Express API proxy
│   ├── index.js                # Server entry point
│   └── .env.example            # Environment variable template
└── docs/                       # Project documentation
```

### Rendering Layers (bottom to top)

1. **Room background** — HTML/CSS/SVG illustration
2. **Room objects** — Interactive furniture (HTML elements, standard event handlers)
3. **Shoelace** — Pixi.js canvas (WebGL sprite animation, gesture detection)
4. **Bubble layer** — HTML overlay (cipher text animation via GSAP)
5. **Sidebar** — HTML overlay, right edge (slides in via GSAP)
6. **Hamburger menu** — HTML overlay, top-left (persistent, floating)

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | Svelte + Vite |
| Room rendering | HTML + CSS + SVG |
| Character animation | Pixi.js |
| UI animation | GSAP |
| Audio | Howler.js |
| LLM | Anthropic API (streaming) |
| Backend | Node.js + Express |
| Desktop (Phase 3) | Tauri |

---

## Getting Started

> Phase 0 — nothing runs end-to-end yet. Setup instructions will appear here when Phase 1 is underway.

### Prerequisites

- Node.js 20+
- An Anthropic API key

### Development setup (when ready)

```bash
# Install frontend dependencies
npm install

# Install server dependencies
cd server && npm install && cd ..

# Copy and fill in environment variables
cp server/.env.example server/.env

# Run the dev server and API proxy concurrently
# (run in separate terminals for now)
npm run dev
node server/index.js
```

---

## Design Principles

- **The room is not a grid.** Objects are placed spatially and interacted with directly.
- **Shoelace is the interface.** Not a widget. Not an assistant panel. The primary control.
- **Subtly wrong.** The aesthetic is modernist-gothic technoir — warm interiors, slightly off atmosphere. The uncanny is subtext, never the lead.
- **Everything streams.** LLM responses are streamed from the first character. This is an architectural constraint, not a feature.

---

## Contributing

This is a personal project. It is not currently open to external contributions. That may change.

---

## License

TBD.

---

*She is a void-spirit who has decided to look like a fox. We are not going to question this.*
