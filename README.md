# 🚀 NOVA STRIKE — Galactic Defense System

> Built during **Vedam School of Technology × Amazon AI BootCamp 2** (June 28, 2026)  
> Mentored by **Tanishq Gupta** (SDE-2, Amazon)

---

## 🎮 What Is This?

**Nova Strike** is a fully browser-playable 2D space shooter game — no downloads, no installs, just open `index.html` in Chrome and play. It was built from scratch using HTML, CSS, and JavaScript as part of a live 2.5-hour AI BootCamp session where participants learned to break down complex problems into smaller components and use AI tools to ship real software fast.

---

## ✨ Features

### 🛸 Three Unique Atmospheres
| Mode | Vehicle | Enemies | Vibe |
|------|---------|---------|------|
| **Space** | Rocket ship | Alien ships | Deep cosmos, stars |
| **Earth** | Fighter jet | Enemy planes | Sky combat, clouds |
| **Fantasy** | Dragon rider | Magical creatures | Mystic realm, orbs |

Each atmosphere has its **own visual style, enemy designs, bullet colors, and background music.**

### 💀 Game Over Pop-up — 3 Exact Buttons
When your spaceship is destroyed (by enemy damage, collision, or a Boss):

- **▶ CONTINUE FROM LEVEL [X]** — Dynamically shows the exact level you died on. Restarts that level with full HP; your score checkpoint is preserved.
- **⌂ MAIN MENU** — Returns to the home screen instantly. Your name stays in the input field so you can start a new session or change your name.
- **↺ RESTART — START OVER** — Full reset: Level 1, Score 0, fresh start.

### 📊 Kill-Based Level Progression (20 Levels)
- The **level progress bar fills based on enemy kills**, not score — kills needed scale with level (`10 + level × 4`)
- Level 1 needs **14 kills**, Level 20 needs **90 kills**
- When the bar fills: **"LEVEL X COMPLETE!"** banner fires → bar resets → Level X+1 begins
- At Level 20: **Endless combat mode** — difficulty stays maxed

### ⚡ Dynamic Difficulty (Level 1 → 20)
| Mechanic | Level 1 | Level 20 |
|---|---|---|
| Enemy speed multiplier | 1.0× | 2.8× |
| Spawn interval | ~67 frames | 10 frames (minimum) |
| Armored enemy frequency | 15% | 50%+ |
| Boss HP | 23 | 175 |
| Boss fire rate | Every 84 frames | Every 10 frames |
| Boss spawn interval | 40 seconds | ~25 seconds |

### 🎵 Layered Audio System — No Overlapping
Four completely distinct BGM tracks, each with its own character:

| Track | When it plays | Style |
|---|---|---|
| `menu` | Home screen | High-energy driving synth — punchy bass, fast arpeggios, chord stabs |
| `space` | Space mode in-game | Eerie drone — sub-bass, tremolo pulse, slow cosmic arpeggios |
| `earth` | Earth mode in-game | Aerial combat — punchy bass, fast staccato lead melody |
| `fantasy` | Fantasy mode in-game | Orchestral — vibrato strings, harp cascades, orchestral bass |

**Isolation guarantee:** Entering a level always stops the menu BGM. Returning to the main menu always stops all level music and restarts the menu track cleanly. No two tracks ever overlap.

### 💥 Spaceship Destruction & Death SFX
When HP reaches 0:
1. **Ship sprite hides immediately** (no flickering ghost ship)
2. **Multi-ring burst explosion** — 4 expanding concentric rings + 50 particles burst outward
3. **White screen flash** — instant impact feedback
4. **Death SFX plays** — synthesized "ta — ta ta ta tata — taa" rhythm using sawtooth oscillators:
   - All gameplay SFX are silenced during the death sequence
   - Rhythm pattern: `ta (pause) ta ta ta ta-ta (pause) taaaa`
5. After ~1.5s, the **Game Over popup animates in**

### ⚡ Powerup System
Collect powerups by flying over them (drop every 8–12 seconds):

| Icon | Powerup | Effect |
|---|---|---|
| ⚡ | Rapid Fire | Triple bullets, double fire rate for 5s |
| 🛡 | Shield | Absorbs all damage for 5s |
| 💥 | Nuke | Instantly destroys all enemies on screen |
| ❄️ | Freeze | Slows all enemies and boss to 20% speed for 5s |

### 💬 Combo System
Kill enemies in quick succession to build combos. 3×+ combos multiply your score (up to 5×) and display a glowing **"Nx COMBO!"** banner.

### 👾 Boss Encounters
A boss spawns on a timer every ~40 seconds (shorter at higher levels). 2 seconds before it arrives, you receive automatic **Rapid Fire** as a warning gift.

Boss attack patterns scale with tier:
- **Tier 1–2:** Spread shots aimed at player
- **Tier 3:** 360° bullet ring
- **Tier 4:** Aimed spread + rotating spiral
- **Tier 5+:** Aimed spread + spiral + random burst shots

---

## 🕹️ Controls

| Action | Key |
|---|---|
| Move | `W A S D` or `↑ ↓ ← →` |
| Shoot | `Space` or `Left Click` |
| Pause / Resume | `P` |

---

## 🚀 How to Run

1. **Download** or clone this repo
2. **Open** `index.html` in any modern browser (Chrome recommended)
3. Type your commander name → choose your battlefield → launch!

No build tools. No dependencies. No server needed. Pure HTML/CSS/JS.

---

## 🏗️ Project Structure

```
nova-strike/
├── index.html      ← Entire game (single file: HTML + CSS + JS)
└── README.md       ← This file
```

The game is intentionally a **single self-contained file** — easy to share, host on GitHub Pages, or submit anywhere.

---

## 🛠️ Technical Notes

### Audio Engine
Built entirely on the **Web Audio API** using oscillators, gain nodes, and LFO modulation — no external audio files needed. The `stopBgMusic()` / `startBgMusic()` isolation guard ensures tracks never stack or overlap, even when rapidly switching screens.

### Level System
Level progression is kill-based (not score-based), using the formula:
```
killsNeeded(level) = 10 + level × 4
```
This makes early levels feel achievable and later levels feel earned.

### Death Explosion
The burst animation uses a dedicated render loop separate from the main game loop, so it plays cleanly even after `gameRunning` is set to false. All particle ring positions are computed frame-by-frame via `requestAnimationFrame`.

### Difficulty Scaling
Enemy speed uses a linear interpolation:
```
speedMultiplier = 1.0 + (level - 1) × (1.8 / 19)
```
So at Level 1, enemies move at 1× speed. At Level 20, they move at 2.8× speed. Boss HP scales as `15 + level × 8`.

---

## 🏆 BootCamp Context

This game was built live during the **Vedam School of Technology × Amazon AI BootCamp 2** on June 28, 2026. The session demonstrated **vibe coding** — using natural English prompts to drive AI-assisted development, then iterating rapidly.

The core lesson: *AI can write code, but a builder still needs to break the problem into logical components, know what to ask for, and have the creative vision to make it interesting.*

> "Engineering always starts with problem solving. Even if domains are different — ethical hacker, data scientist, frontend dev — the one common part is: they have to be problem solvers."  
> — Tanishq Gupta, SDE-2 @ Amazon

---

## 👤 Author

Built with Claude (Anthropic) as AI coding assistant.  
Game design, feature specification, and creative direction by the student.

---

## 📄 License

Free to use, modify, and share. Go build something cool.
