# LACUNA — Phase Roadmap

**Version:** 1.0
**Status:** Working reference
**Prepared by:** Miss Blackwood

---

## Phase 0 — Foundations (Current)

**Goal:** Lock decisions, stand up the skeleton, establish documentation.

- [x] Project codename confirmed: Lacuna
- [x] Character name confirmed: Shoelace (Lacey)
- [x] Room and interface requirements drafted (v0.3)
- [x] Technical stack confirmed
- [x] Repository structure established
- [ ] Shoelace character spec written
- [ ] Room layout wireframe produced (Figma or equivalent)
- [ ] First working build: static room placeholder + Shoelace sprite placeholder + chat box hitting Anthropic API

---

## Phase 1 — Proof of Concept (Browser, Single Room)

**Goal:** A running, interactive room with Shoelace present and one real tool working.

### Environment
- [ ] Room background illustration (one art style pass)
- [ ] Window layer with three weather states and passive animation
- [ ] Computer (Tier 1) — fan menu with 5–8 configurable slots
- [ ] Desk (Tier 2) — manually assigned objects
- [ ] Shelf (Tier 3) — manually pinned items
- [ ] Entertainment center — fan menu with media app slots
- [ ] Couch — Shoelace idle anchor, click to wake

### Shoelace
- [ ] Sprite sheet produced (idle_float, idle_couch, idle_window, traverse, react_poke, react_pet, fanmenu_open, sidebar_pull)
- [ ] Pixi.js integration — sprite loaded and animating
- [ ] State machine implemented
- [ ] Anchor point movement with GSAP traversal
- [ ] Idle timer (180s) → couch or window ledge
- [ ] Mouse proximity reaction
- [ ] Gesture system: single click (fan), drag right (sidebar), double-click, pet

### Chat System
- [ ] Bubble interface — cipher text animation, duration formula, audio
- [ ] Fan menu — four Phase 1 options
- [ ] Chat sidebar — slide-in, pull tab, conversation history
- [ ] Sidebar overflow mechanic — mid-stream surface switch with Shoelace animation
- [ ] Streaming LLM integration (Haiku / Sonnet split)

### Audio
- [ ] Shoelace voice sprite sheet produced
- [ ] Howler integration — all trigger events wired
- [ ] Global toggle in hamburger menu

### Navigation
- [ ] Hamburger menu — top-left, weather toggle, sound toggle, slot config, about

---

## Phase 2 — Environment Depth

- [ ] File system hooks (Google Drive or local)
- [ ] Tier auto-population by usage frequency
- [ ] Tier drag-and-drop migration
- [ ] Metadata pull-in from Google Docs
- [ ] Shoelace idle commentary driven by user activity
- [ ] Hypatia's distortion bubbles on loading/transfer states
- [ ] Auto weather state (system clock or time-of-day)
- [ ] Second weather state (scheduled or behavioural)
- [ ] Granular audio controls
- [ ] Reading-speed accessibility preference

---

## Phase 3 — Desktop Port

- [ ] Tauri wrapper (Windows, macOS, Linux)
- [ ] Local model integration (Ollama)
- [ ] System-level file access
- [ ] App launching (native, not browser tabs)
- [ ] Fullscreen mode / hamburger auto-hide

---

## Phase 4 — Multi-Room / Multi-Workspace

- [ ] Additional rooms as workspace metaphor
- [ ] Room transition animations
- [ ] Exterior detail (tentacle cityscape)
- [ ] Begin 3D/VR extension planning

---

*Milestones are kept small. The point is to always have something running.*

**— Miss Blackwood, Episkopos of Codename Lacuna**
