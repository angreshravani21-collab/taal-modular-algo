# Taal Explorer

**Every Taal is a Circle.** An interactive, beginner-friendly web app that explores Indian classical rhythm (Taal) through modular arithmetic 
🔗 **Live demo:** 

![status](https://img.shields.io/badge/status-active-brightgreen) ![license](https://img.shields.io/badge/license-MIT-blue)

---

## ✨ What is this?

Indian Taals (rhythm cycles) are, mathematically, cyclic groups — `ℤ_n`. Every cycle (Avartana) loops back to beat 1 (Sam) exactly the way a clock loops back to 12. This project visualizes that idea as an interactive wheel, lets people tap through beats, and reveals the math *only if they're curious* — so it's just as approachable for a commerce student as it is for an engineer.

### Core features
- 🎡 **Interactive cycle wheel** — tap any beat, watch it highlight on a rotating SVG/Canvas wheel
- 🥁 **Tabla bols ↔ 💃 Kathak tatkar toggle** — switch between musical bols (Dha, Dhin, Na...) and dance footwork syllables (Ta, Thei, Tat, Aa...)
- 🏠 **Plain-language insights** — tapping a beat explains it in everyday words first (e.g. "You found home base!"), with the formal math term (Sam, Khali, Vibhag) hidden behind an optional "Curious?" reveal
- ▶️ **Auto-play loop** + **Next Beat** step-through navigation
- 🔢 **Beat calculator** — enter any beat number (even 100+) and see exactly where it lands in the cycle
- 🌀 **Tihai solver** — calculates the starting beat for a 3x-repeated phrase to land exactly on Sam
- 🚀 **Lay (speed) mapper** — visualizes how beats remap when tempo doubles/triples
- 6 taals included: Teentaal, Jhaptaal, Ektaal, Rupak, Keherwa, Dadra

---

## 🧮 The algorithm

All the math lives in a handful of small, pure functions:

```js
// 1. Cycle wraparound (modular arithmetic)
position = (beatNumber - 1) % totalBeats

// 2. Beat type classifier — Sam / Tali / Khali
function getBeatType(taal, position) {
  if (position === 0) return "Sam";
  // walks cumulative vibhag lengths to find which chunk `position` falls in
}

// 3. Tihai solver — start + 3L ≡ 0 (mod n)
function solveTihai(phraseLength, totalBeats) {
  const total = 3 * phraseLength;
  const remainder = total % totalBeats;
  return remainder === 0 ? 0 : totalBeats - remainder;
}

// 4. Lay (speed) homomorphism — φ: ℤ_n → ℤ_Ln, k ↦ Lk
function speedMap(beatPosition, multiplier, totalBeats) {
  return { newPosition: beatPosition * multiplier, newTotalBeats: totalBeats * multiplier };
}
```

See [`index.html`](./index.html) for the full implementation (vanilla JS, no build step).

---

## 🗂️ Project structure

```
taal-explorer/
├── index.html          # main app — single-file, no dependencies
├── legacy/
│   └── taal_explorer_desktop.py   # original Python/tkinter prototype
├── docs/                # design notes / reference material
└── README.md
```

This is intentionally a **single-file app** — no npm, no build step. Open `index.html` in any browser and it just works. Good for quick demos, kiosk displays, and offline event setups.

---

## 🚀 Running locally

```bash
git clone https://github.com/<your-username>/taal-explorer.git
cd taal-explorer
open index.html   # or just double-click it
```

No server, no install required.

## 🌐 Deploying to GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, root folder
4. Your live link will be `https://<your-username>.github.io/taal-explorer/`

---

## 🎯 Roadmap / ideas

- [ ] Add audio playback of actual tabla bols per beat
- [ ] Add more taals (Deepchandi, Sooltaal, etc.)
- [ ] Mobile-first touch gestures for the wheel
- [ ] Printable cheat-sheet export (beat → type table)
- [ ] Sync with TechNrityam's live Taal Chakra widget

---

## 🙏 Credits

Built by **Shravani Angre** 



