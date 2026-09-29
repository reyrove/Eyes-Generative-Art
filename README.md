# Eyes

**A seed-based generative system for anatomical eye compositions.**

A catalogue of computational textile compositions for fashion, textile and surface design — algorithmically drawn, seed-documented, and ready for production.

---

## Overview

Eyes is a generative design system rather than a single artwork. Each composition is built from a single eye — an outer sclera ring, a gradient-filled iris base, three concentric iris layers of increasing detail, a black pupil, and a highlight reflection. The result is a single portrait — a small, quiet face, drawn entirely by algorithm.

The system is designed for:

- **Fashion houses** adapting anatomical ornament for apparel and accessories
- **Textile studios** developing repeat patterns and yardage
- **Surface designers** working across print, wallpaper, and interior applications

Every composition can be licensed, adapted, or commissioned to a brief.

---

## Concept

An eye, when it is *generated* rather than drawn, becomes a portrait — anatomical, precise, quietly yours.

The eye — layered, radial, endlessly varied — has always carried the structure of a mandala. From the mosaics of ancient temples to the concentric rings of a columbarium, the eye is one of the oldest systems of ornamental computation we have. Eyes translates that structure into code. Each composition begins with a sclera tone and an iris palette, and unfolds through three concentric layers of increasing detail — a fractal bloom at the centre of the frame.

The sclera tone, the iris palette, the iris layer density, and the highlight position are all derived from a single numeric seed.

Like the other still volumes in this series (Girih, Arachne, Celestial Grove, ChaotiColor, Citrus Mosaic, Crazy Knight Curve, Crazy Knight Line, Crazy Letter, cyPollock, Digital Pollen, Draconic Fractals, Dreamscape Watercolors, Elliott Waves, Ellipses, Enigma Sudoku, Ephemeral Whirls), **Eyes is a static composition.** The plate, the framed plate, the surfaces, and the archive are all static frames. A portrait is something you read; its character is stillness, not motion.

---

## Features

- **Seed-based generation** — every composition is defined by a numeric seed and can be regenerated exactly
- **Deterministic output** — the same seed always produces the same composition
- **Three-layer iris** — a gradient base, a first layer of ~200–300 points, and two dense layers of ~1,000–3,000 points each
- **Bezier-closed layers** — every iris layer is drawn as a smooth closed Bézier curve, giving each layer a soft, organic edge
- **Gradient fills** — the iris base and each layer are filled with a linear gradient, producing depth and colour flow
- **Highlight reflection** — a small white highlight is placed near the pupil, in one of two shapes (square or circle)
- **27 sclera tones** — from white smoke, through pale azure and gulf blue, to soft linen and ivory
- **11 iris palettes** — Blue, Dull Blue, Ocean, Baggy, Deep Blue, Bright Hazel, Brown, Hazel, Green, Azure, and Steel
- **Adaptive surfaces** — one seed applied across print, scarf, textile, and wall formats
- **Archive** — eight curated seeds available for immediate loading
- **Download** — export the composition as a high-resolution PNG
- **Keyboard shortcuts** — `R` for new seed, `S` to save

---

## Project Structure

```
.
├── index.html          # Main catalogue page
├── images/
│   ├── fav.svg         # Favicon
│   ├── tote.png        # Mockup: tote bag
│   ├── tee.png         # Mockup: t-shirt
│   └── cushion.png     # Mockup: cushion
└── README.md
```

---

## How It Works

### The Seed

A numeric seed (a large integer) initializes a deterministic pseudo-random generator. From this seed, the system derives:

- Sclera tone (from a palette of 27 light tones)
- Iris palette (from a set of 11 named iris colours)
- The rotation angle of the gradient axis
- The three iris layer densities
- The position, size, and shape of the highlight reflection

Because the generator is deterministic, the same seed always produces the same composition — on any device, at any time.

### The Iris

Each composition builds the iris in four stages:

**Stage 1 — Iris base.** A filled circle with a linear gradient, running from `Color1[0]` to `Color1[1]` along a randomly-rotated axis.

**Stage 2 — First layer.** A smooth closed Bézier curve through ~200 to ~300 points, each at a radius between 50% and 100% of the iris. Filled with a gradient from `Color1[1]` to `Color1[2]`.

**Stage 3 — Second layer.** A denser Bézier curve through ~1,000 to ~3,000 points, at radii between 25% and 100%. Filled with `Color1[3]`.

**Stage 4 — Third layer.** Another dense Bézier curve through ~1,000 to ~3,000 points, at radii between 20% and 100%. Filled with `Color1[4]`.

Where the layers overlap, colour deepens and the iris reads as a fractal — each layer adding detail, each layer tightening toward the centre.

### The Bézier Layers

Each iris layer is drawn by `drawSmoothClosedBezierCurve` — a small helper that:

1. Moves to the midpoint between the last and first points.
2. For each point, draws a quadratic Bézier curve to the midpoint between it and the next point.
3. Closes the path and strokes/fills it.

This produces a smooth, closed curve that passes near every point — a soft, continuous edge instead of a jagged polygon. The layer is filled with a gradient, not a solid colour, so the depth is layered across the composition.

### The Pupil and Highlight

At the centre, a filled circle in pure black forms the pupil, with a soft shadow that gives it weight. The highlight reflection is then drawn near the pupil — either as a small square of four rects, or as a filled circle — in translucent white, at a random position and size within the upper-left region of the frame.

### The Colour Palettes

The composition uses two independent palettes:

- **Sclera tones** — 27 pale tones, from pure white to gulf blue and soft linen. These form the background of the composition, and they read as the white of the eye.
- **Iris palettes** — 11 named colour sets, each containing 5 tones that step from dark to light. For example, "Ocean Eyes" runs from a deep navy to a bright electric blue and finally to a light aqua.

Where the two meet, the composition reads as a portrait — a small, floating face.

### The Surfaces

The same seed is rendered across four surface formats. These are static frames — they represent the print-ready composition.

| Surface  | Aspect | Material          |
|----------|--------|-------------------|
| Print    | 1 : 1  | Cotton rag        |
| Scarf    | 3 : 1  | Twill silk        |
| Textile  | 4 : 3  | Fabric yardage    |
| Wall     | 2 : 3  | Wallpaper         |

Each surface uses the same underlying seed and structural logic — only the repeat, orientation, and scale change.

### Stillness

Like the rest of the still volumes, Eyes does not animate. The plate is a single frozen frame — the composition is complete the moment it is generated.

This is a deliberate design choice. A portrait is not a swarm. It is not a rotation. It is a figure, laid down once and left. Its stillness is what makes it print-ready in the strictest sense: what you see is what you get.

---

## Usage

### In the browser

1. Open `index.html` in any modern browser.
2. Click **New Seed** to generate a new composition.
3. Click **Download** to save the composition as a PNG.
4. Scroll to the **Archive** section and click any plate to load it into Plate 001.

### Keyboard shortcuts

| Key | Action          |
|-----|-----------------|
| `R` | New seed        |
| `S` | Save as PNG     |

### Reproducing a composition

Each composition is identified by an 8-digit seed label displayed in the metadata panel. To reproduce a specific composition, note the seed and regenerate it programmatically:

```js
const rng = new RandomGenerator(seed);
const features = buildFeatures(rng);
renderComposition(canvas, features, rng);
```

Because the generator is deterministic, this will produce the identical composition on any device.

---

## Technical Notes

- **No build step.** The system is a single HTML file with inline CSS and JavaScript.
- **No dependencies.** All drawing is done with the native Canvas 2D API.
- **Deterministic.** The `RandomGenerator` class uses a xorshift-based PRNG seeded by an integer, so identical seeds produce identical outputs.
- **Static rendering.** Every canvas renders a single frame. There is no animation loop.
- **Feature isolation.** Cover, framed plate, surfaces, and archive thumbnails each derive their own feature set from their own local RNG, without disturbing the main plate's state.
- **Integer layer counts.** The iris layer point counts are wrapped in `Math.floor`, so no fractional loops. This ensures deterministic output across every render.
- **Bezier-closed layers.** Each iris layer is drawn as a closed path using the `drawSmoothClosedBezierCurve` helper, producing soft organic edges rather than jagged polygons.
- **Clean shadow exit.** Every `renderComposition` resets `shadowBlur` and `shadowColor` at the end, so the pupil's glow never bleeds into subsequent drawing.
- **Responsive.** The layout adapts from large desktop down to very small mobile devices (tested at 360px viewport width).
- **Accessible.** Supports `prefers-reduced-motion`. Pinch-zoom is enabled.

### Browser support

Tested in current versions of:

- Chrome / Edge
- Firefox
- Safari (desktop and iOS)

---

## Licensing

All Eyes compositions are **seed-documented** and available for licensing across textile, surface, and print applications.

- **Standard licenses** cover single-product production runs.
- **Commercial use, custom editions, or exclusive rights** are available on request.

Each license is issued against a specific seed ID. Regeneration of the same seed produces the identical composition — ensuring reproducibility between artist, studio, and manufacturer.

For licensing enquiries: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Commission

Eyes is a generative design system, not a fixed artwork. It can be adapted for specific briefs:

| Service     | Description                                                       |
|-------------|-------------------------------------------------------------------|
| Licensing   | Existing seeds from the archive, licensed for production use      |
| Commission  | New compositions designed to your palette, repeat, and product    |
| Systems     | A private generative tool built for your studio's ongoing use     |

To begin a conversation: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Series

Eyes is part of a computational textile series. Each volume approaches ornament from a different structural angle:

| Volume                     | Structure                    | Motion                     |
|----------------------------|------------------------------|----------------------------|
| Girih 1                    | Islamic geometric            | Static                     |
| Arachne                    | Rotating rings               | Static                     |
| Baroque Me Baby            | Baroque frames               | Static                     |
| Bezier 1                   | Concentric curves            | Static                     |
| Bezier 2                   | Single rotating curve        | Animated (plate)           |
| Brownian Graphe            | Graph networks               | Animated + interactive     |
| Celestial Grove            | Recursive branch trees       | Static                     |
| ChaotiColor                | Cellular automata            | Static                     |
| Citrus Mosaic              | Arc-and-triangle tiles       | Static                     |
| Crazy Knight Curve         | Knight's-tour smooth path    | Static                     |
| Crazy Knight Line          | Knight's-tour gradient       | Static                     |
| Crazy Letter               | Framed wavy lines            | Static                     |
| cyPollock                  | Scattered branch field       | Static                     |
| Digital Pollen             | Noise-driven texture         | Static                     |
| Draconic Fractals          | Tiled dragon curve           | Static                     |
| Dreamscape Watercolors     | Layered watercolor blooms    | Static                     |
| Elliott Waves              | Financial chart              | Static                     |
| Ellipses                   | Concentric elliptical rings  | Static                     |
| Enigma Sudoku              | Playable 9×9 puzzle          | Interactive (plate)        |
| Ephemeral Whirls           | Wandering looper field       | Static                     |
| **Eyes**                   | **Layered iris portrait**    | **Static**                 |

The series is designed as a coherent whole — same page structure, same seed logic, same licensing and commission terms — so that each volume can be presented individually or as part of a larger body of work.

---

## Credits

- **Design & Generative System** — Reyhaneh Daneshdoost
- **Typefaces** — Cormorant Garamond · DM Mono
- **Platform** — Reyrove Studio
- **Edition** — Eyes, Autumn 2026

### On AI tools

Where technical obstacles were encountered, AI tools were used for debugging and code optimization. Every structural, aesthetic, and conceptual decision remained the artist's own.

---

## Links

- Website — [reyrove.github.io](https://reyrove.github.io/)
- Instagram — [@rey._.rove](https://www.instagram.com/rey._.rove/)
- LinkedIn — [Reyhaneh Daneshdoost](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- X — [@reyrove](https://x.com/reyrove)

---

© Eyes · All compositions reproducible by seed · Computational Textile Design