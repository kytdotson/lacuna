# LACUNA — Room & Interface Requirements

**Version:** 0.3
**Status:** Near-complete draft — Phase 1 scope
**Scope:** Phase 1 — Single Room, Browser Environment
**Prepared by:** Miss Blackwood

---

## 1. Environment Overview

The primary interface is a single 2D cartoon room rendered in a modernist-gothic technoir style. The room reads as a high-floor apartment in a contemporary skyscraper — warm interior, slightly wrong atmosphere. It functions as the user's primary desktop metaphor: navigating the room navigates their tools and files.

The room is not a grid. Objects are placed spatially and interacted with directly. No traditional desktop icons or taskbars appear in the default view.

---

## 2. Room Layout — Objects & Functions

### 2.1 Window (Background / Atmosphere Layer)

**Purpose:** Scale, ambiance, passive animation.

**Specs:**
- Full cityscape visible — tall buildings, urban density
- Exterior tentacle detail deferred to visual design phase
- Three animated states at launch:
  - **Overcast day** — grey-blue sky, muted exterior
  - **Night, clear** — dark sky, city lights, star shimmer
  - **Night, rain** — rain streaks on glass, wet city reflections
- State manually toggled (Phase 1); auto/scheduled (Phase 2)
- No visible sun — hard design constraint
- Shoelace may idle at window ledge as an anchor point (cat behaviour)

**Interaction:** Passive environmental layer. Shoelace destination only.

---

### 2.2 Accessibility Tiers — Computer / Desk / Shelf

A single spatial metaphor for distance from active work. Not three separate launchers — one layered system.

#### 2.2.1 Computer (Tier 1 — Active Work)

- Computer screen is the focal point for pinned, actively-used apps
- Click → fan/radial pop-out of 5–8 user-pinned app slots
- Phase 2: OS suggests slots based on usage frequency
- Opens apps in new browser tab

#### 2.2.2 Desk (Tier 2 — Frequent Periphery)

- Desk surface objects represent frequently-used-but-not-pinned apps and files
- Phase 1: manually assigned
- Phase 2: auto-populated by access recency below Tier 1 threshold
- Individual object clicks — no fan mechanic

#### 2.2.3 Shelf (Tier 3 — Reference & Waiting)

- Bookshelf objects represent parked, reference, or recently-touched-but-not-active items
- Phase 1: manually pinned
- Phase 2: surfaced from file system or Google Drive recents
- Click → opens file or app in new tab

**Tier migration:** Objects are draggable between tiers. This spatial rearrangement *is* the file management paradigm. Phase 2 implementation; architecture anticipates it.

---

### 2.3 Entertainment Center

- Television unit / entertainment wall
- Click → fan of media app icons (YouTube, TikTok, TBD)
- Opens in new browser tab

---

### 2.4 Couch

- Shoelace idle anchor — one of two (see Section 4.1)
- No direct user function in Phase 1
- Clicking couch or Shoelace-on-couch wakes Shoelace

---

## 3. Navigation & Menu System

### 3.1 Hamburger Menu

- **Position:** Top-left, floating, persistent
- **Purpose:** Configuration and settings — not primary interaction
- **Contents:** Weather toggle, sound toggle, app slot configuration, about/credits
- **Phase 2:** Auto-hides in fullscreen if native top bar present; workspace navigation added
- Styled to match room aesthetic — not a browser default element

---

### 3.2 Chat System — Dual Surface Architecture

Two surfaces, one shared conversation context and one LLM stream. Shoelace is the access point for both.

#### 3.2.1 Bubble Interface (Quick Interaction Layer)

- Input and short responses happen in bubbles near Shoelace's current position
- Accessed via gesture (see Section 5)
- Bubbles stack upward, fade on duration timer
- Text materialises via cipher-to-legible animation (random glyphs resolve to text)
- Audio: Simlish-adjacent kitten-digital-glitch vocalisation during generation

**Bubble duration formula:**
`duration = 3 + (word_count / 3) seconds`
Minimum 3 seconds. Maximum approximately 10 seconds.
Fade out over 0.5–0.8 seconds.
Global reading-speed preference (slow/normal/fast) accessible via hamburger menu.

#### 3.2.2 Chat Sidebar (Deep Interaction Layer)

- Slides in from right edge; room remains visible and active to the left
- Scrollable conversation history, text input at bottom
- Shoelace remains animated in room while sidebar is open
- **Pull tab:** Persistent small tab on right screen edge — user can grab and drag to open manually
- **Gesture access:** Click-and-drag-right on Shoelace opens sidebar directly

#### 3.2.3 Sidebar Transition Mechanic (Overflow Behaviour)

**Trigger:** Response exceeds approximately 280 characters (Phase 1 heuristic).

**Sequence:**
1. Bubble begins populating — cipher animation, audio plays
2. At threshold, generation pauses mid-cipher
3. Shoelace registers a beat of hesitation — looks toward sidebar edge
4. She traverses to right edge and performs a pull/yank animation on the sidebar tab
5. Sidebar slides open
6. Partial response flows directly into sidebar without restarting — stream continues uninterrupted
7. Bubble dissolves; full response populates in sidebar

**Technical requirement:** LLM response must be streamed; output surface must be hot-swappable mid-stream. This must be architected from day one.

---

## 4. Shoelace — In-Room Behaviour

*Full character spec: `docs/03-shoelace-character-spec.md`*

### 4.1 Idle Anchor Points & Threshold

- **Idle threshold:** 180 seconds of no user interaction
- At threshold, Shoelace navigates to one of two idle anchors: **couch** or **window ledge** (chosen at random or weighted by prior behaviour)
- Window ledge idle reflects cat-like behaviour — she watches the exterior

### 4.2 Movement

- Defined anchor points: couch, window ledge, desk/computer area, shelf area, screen edges
- Traversal is animated — she moves through the room, does not cut
- She can adhere to edges, perch on corners, drape across furniture

### 4.3 Poke / Click Reactions

- Governed by gesture system (see Section 5)
- Reaction animations tied to gesture type

### 4.4 Thought Bubbles (Unprompted)

- Low-frequency idle commentary on random timer
- Same cipher-to-legible animation and duration formula as response bubbles
- Phase 2: driven by user activity awareness

---

## 5. Shoelace Gesture System

Shoelace is the primary UI control. The hamburger menu handles configuration; Shoelace handles action.

| Gesture | Input | Result |
|---|---|---|
| Single click | Click Shoelace | Fan menu appears |
| Fan — bubble | Mouse up over bubble option | Bubble input activates |
| Fan — option | Mouse up over other option | Executes that option |
| Click + drag right | Hold and swipe toward right edge | Sidebar opens directly |
| Double-click | Double-click Shoelace | Reaction animation (TBD specific behaviour) |
| Hover + lateral stroke | Mouse back-and-forth over Shoelace | Pet reaction |

**Fan menu contents (Phase 1):**
- Chat (opens bubble input)
- Find a file
- Launch an app
- Surprise me (idle commentary or random observation)

---

## 6. Audio Design

**Default state:** On.

**Shoelace voice:** Simlish-adjacent — short, synthetic, kitten-digital-glitch hybrid. Suggests dialogue without forming words. Scales with text length.

**Trigger events:**
- Bubble text generation (primary)
- Poke/gesture reactions
- Pet reaction (sustained while stroking)
- Sidebar open (ambient — TBD)
- Room state transitions (ambient layer — TBD)

**Toggle:** Global on/off via hamburger menu. Phase 2: per-type granular control.

---

## 7. Open Items

| Item | Status |
|---|---|
| Shoelace character spec | Not yet written — see `docs/03-shoelace-character-spec.md` |
| Double-click specific behaviour | TBD |
| Idle anchor weighting (random vs behavioural) | TBD |
| Fan menu icon/visual treatment | TBD |
| Sidebar visual style (response rendering) | TBD |

---

## 8. Deferred to Phase 2+

- Exterior tentacle detail on cityscape
- Auto weather state (clock-based)
- File system and Google Drive integration
- Tier auto-population by usage frequency
- Tier drag-and-drop migration UI
- Shoelace activity awareness
- Second-monitor living mode
- Fullscreen hamburger auto-hide
- Directional drag gesture expansion
- Granular audio controls
- Reading-speed accessibility preference

---

*The gesture vocabulary turns Shoelace from a character into an instrument. The room is the stage; she is the interface. Everything else is furniture.*

**— Miss Blackwood, Episkopos of Codename Lacuna**
