# Gaussophone

A prime number detector that turns math into sound and motion. Every odd integer gets tested using a triangular number (Gaussian) decomposition — primes and composites produce distinct audio signatures, and a fleet of emoji turtles choreograph the results in real time.

**[Live demo →](https://jayzon.github.io/gaussophone/gaussophone.html)**

---

## What it does

The engine walks odd integers from 3 upward. For each N, it searches for a value called **magic** — the smallest offset that makes a triangular-number residue collapse to zero. When it finds it, two things happen:

- If `factor == N`, the number is **prime** — turtles panic, a sharp FM tone fires, the log marks it red
- Otherwise it's **composite** — turtles glide, an additive harmonic chord plays, the log shows the factor pair

The audio, motion, and log all read from the same three values: **N**, **magic**, and **turtle%** (magic / N × 100).

---

## The algorithm

```
rightPos  = next triangular index ≥ N
rightSum  = triangular(rightPos + magic)
rightDiff = rightSum − N
leftPos   = next triangular index ≥ rightDiff
leftSum   = triangular(leftPos)
fz        = rightDiff − leftSum          ← zero when magic is found
factor    = magic + rightPos + leftPos + 1
```

`fz == 0` is the detection condition. `factor == N` means prime.

---

## Sound design

The Sound Lab panel (collapsible) gives full control over the audio engine:

| Section | What it controls |
|---|---|
| **Master** | Volume, reverb wet mix, root tuning frequency, musical scale |
| **Prime** | FM synthesis — carrier freq, modulation index, chaos, LFO, noise, dissonance, decay |
| **Composite** | Additive synthesis — partials, brightness, harmonic drift, pan spread, attack/decay |
| **Drone / Spatial** | Continuous undertone — base freq, pitch range, detune, stereo width, filter floor/ceiling/Q, waveform |

Built-in presets: `default`, `alien radio`, `glass bells`, `deep space`, `chaos engine`, `minimal`, `ritual drone`, `jazz voicing`

The oscilloscope in the Sound Lab shows a live waveform read from the Web Audio analyser node.

---

## Controls

| Control | Description |
|---|---|
| **speed** slider | Step interval from ~290ms (1) down to ~18ms (10) |
| **turtles** slider | 1–12 simultaneous turtles on the stage |
| **trails** checkbox | Fading dot trail behind each turtle |
| **panic on prime** checkbox | Turtles move faster and more chaotically on prime hits |
| **audio toggle** | Enables Web Audio (must be clicked once to satisfy browser autoplay policy) |

---

## Running it

**Option 1 — just open it**
Download `gaussophone.html` and open it in any modern browser. No install, no server needed.

**Option 2 — GitHub Pages**
1. Create a repo and push the file
2. Go to Settings → Pages → Source → Deploy from branch (`main`, `/root`)
3. If you rename the file to `index.html`, the root URL serves it directly

The app has zero external dependencies and no network requests at runtime, so it works offline after the first load.

---

## Browser compatibility

Requires Web Audio API support. Works in Chrome, Firefox, Safari, and Edge (all current versions). Mobile browsers work but the Sound Lab layout is optimized for desktop width.

---

## Project

Built by **Jason Ausborn** / [Nerd Toolbox Research](https://nerdtoolbox.com)  
Part of past independent research into triangular number factorization and quantum-adjacent number theory.

---

## License

MIT — do whatever you want with it, attribution appreciated.
