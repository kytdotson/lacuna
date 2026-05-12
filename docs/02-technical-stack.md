# LACUNA — Technical Stack Record

**Version:** 1.0
**Status:** Confirmed — Phase 1
**Prepared by:** Miss Blackwood

This document is the authoritative reference for technology decisions. Changes require explicit confirmation from Kyt and a version increment.

---

## Core Stack

| Layer | Technology | Purpose |
|---|---|---|
| Frontend framework | Svelte + Vite | UI structure, reactive state management |
| Room rendering | HTML + CSS + SVG | Interactive room objects, layout |
| Character rendering | Pixi.js | Shoelace animation, sprite sheets, gesture hit detection |
| UI animation | GSAP | Transitions, cipher text effect, choreographed sequences |
| Audio | Howler.js | Vocalisations, ambient sound, audio sprites |
| LLM | Anthropic API (streaming) | Claude Haiku (quick) / Sonnet (complex), streamed responses |
| Backend | Node.js + Express | API key proxy, request routing |
| Desktop wrapper (Phase 3) | Tauri | Native desktop shell |

---

## Decision Rationale

### Svelte + Vite

Chosen over React for reactive state management suited to game-like UI. Svelte compiles to vanilla JavaScript at build time, producing smaller bundles and cleaner state handling without framework overhead. Vite is the standard build tool pairing.

SvelteKit not required at this stage. Revisit if routing or SSR becomes necessary.

### HTML + CSS + SVG (Room Layer)

The room environment, furniture, and interactive objects are standard web elements. Canvas-based rendering for interactive objects would require manual hit detection and event reconstruction — unnecessary complexity when the browser already handles this for HTML elements. Standard event handlers for object interaction.

The Pixi canvas layer for Shoelace floats above the HTML room layer. These two rendering contexts are maintained separately and must not be consolidated into a single canvas.

### Pixi.js (Character Layer)

WebGL-accelerated 2D rendering. Industry standard for browser-based sprite animation. Handles sprite sheets natively — the correct architecture for a character with multiple animation states. Gesture hit detection on Shoelace's actual sprite bounds is handled within Pixi.

Alternatives considered: CSS animation (too limited for complex state machine), Phaser (full game engine — unnecessary overhead), Lottie (suitable for decorative loops, not interactive stateful characters).

### GSAP

All choreographed UI animation: sidebar transitions, fan menu open/close, bubble materialisation, cipher-to-legible text effect, Shoelace traverse sequences between anchor points. Timeline-based sequencing handles the sidebar overflow transition mechanic — a complex, multi-step choreographed sequence with precise timing relationships.

### Howler.js

Audio sprite architecture for Shoelace vocalisations and ambient sounds. Cross-browser audio normalisation. One audio file, many named clips triggered individually.

Phase 2 consideration: Tone.js for procedurally generated glitch audio if pre-recorded sprites prove insufficient.

### Anthropic API (Streaming)

Streamed responses via SSE (Server-Sent Events). Streaming is a non-negotiable architectural requirement — the sidebar overflow mechanic depends on mid-stream surface switching and cannot be retrofitted.

**Model split:**
- Claude Haiku: bubble interface (fast, cheap, short tasks)
- Claude Sonnet: sidebar conversations (capable, complex queries)

### Node.js + Express (Backend)

API key proxy only in Phase 1. Thin and minimal — no database, no auth, no complexity beyond routing and authentication. The API key must never appear in client-side code.

Phase 3: replaced or absorbed by Tauri's Rust backend layer.

### Tauri (Phase 3)

Native webview shell with Rust backend. Produces small binaries (5–15MB) compared to Electron (100–200MB). The Svelte + Pixi frontend ports to Tauri with minimal rework. Target platforms: Windows, macOS, Linux.

---

## Constraints

- LLM response streaming must be implemented from day one
- Pixi canvas and HTML room layers must remain separate rendering contexts
- API keys must never appear in client-side code
- All animation sequencing for the sidebar overflow mechanic must be GSAP timelines from the start — this transition cannot be bolted on later

---

## Decisions Not Yet Made

| Item | Notes |
|---|---|
| Local model (Phase 3) | Ollama likely. Architecture, model selection, integration pattern deferred. |
| Serverless deployment | Netlify / Vercel functions viable alternative to self-hosted Express. Not ruled out. |
| Procedural audio | Tone.js for glitch sounds deferred to Phase 2 evaluation. |

---

*The stack is conservative where it needs to be and specific where it matters. Nothing here will surprise anyone in three years — which is exactly the point for a project that intends to still be running in three years.*

**— Miss Blackwood, Episkopos of Codename Lacuna**
