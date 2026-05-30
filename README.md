# Simplex Noise Art

An interactive generative-art studio that runs entirely in the browser. Thousands of particles flow through an animated [simplex-noise](https://en.wikipedia.org/wiki/Simplex_noise) field, painting organic, ever-changing artwork in real time. Tweak the field, pick a palette, push the particles around with your mouse, and export the result as a PNG.

**Zero dependencies. Zero build step. One file.**

> Tip: press `S` in the app to export a frame, save it as `preview.png` next to this README, then uncomment the line below for a portfolio hero image.
> `<!-- ![Simplex Noise Art](preview.png) -->`

## Run it

Just open `index.html` in any modern browser:

```bash
open index.html        # macOS
# or simply double-click the file
```

Or serve it locally (recommended so fullscreen / save behave consistently):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Controls

| Control | What it does |
| --- | --- |
| **Palette** | Six curated color schemes (each sets its own background). |
| **Particles** | How many agents trace the field (200–6000). |
| **Flow scale** | Zoom of the noise field — small = tight swirls, large = sweeping currents. |
| **Speed** | How fast particles travel and how quickly the field evolves. |
| **Curl** | Rotates the whole field, twisting the flow. |
| **Line width / Trail fade** | The look of the strokes and how long trails persist. |
| **Blend** | *Glow* (additive) or *Ink* (opaque). |
| **Mouse** | Off / Attract / Repel — drag on the canvas to interact. |

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Space` | Pause / resume |
| `R` | Randomize a new composition |
| `S` | Save as PNG |
| `C` | Clear the canvas |
| `F` | Fullscreen |
| `H` | Hide / show the control panel |

## How it works

- A **seeded simplex-noise** generator (implemented from scratch, no libraries) produces a smooth 2D field. Each point's noise value becomes a flow angle.
- Every frame, each particle samples the field at its position and steps along the resulting vector, drawing a short line from its previous spot — the accumulation of these strokes forms the artwork.
- A slowly advancing `z` offset animates the field over time, and a translucent fill each frame creates the trailing fade.
- Mouse forces are added on top of the field vector for attract/repel interaction.
- Because the noise is **seeded**, every artwork has a reproducible seed (it's even baked into the exported PNG's filename).

## Tech

Plain HTML, CSS, and vanilla JavaScript with the Canvas 2D API. No frameworks, no bundler, no dependencies.
