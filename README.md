# Modulor Massing

A browser-based parametric architectural massing tool. Single-file HTML/JS, built on Three.js, exploring building composition through preset typologies, proportional systems, and controlled randomization.

**Live:** [modulor-massing.axisbim.io](https://modulor-massing.axisbim.io)
**Repo:** `JoeK212/modular.massing`
**Deploy:** Netlify continuous deployment from `main`

---

## What it does

Modulor Massing generates architectural massing studies — plan grids of building volumes with configurable heights, merges, voids, and facade treatments (punched windows, curtain wall, solid panels). Every composition is driven by a proportional module derived from Le Corbusier's Modulor Blue Series (`BLUE[2]`–`BLUE[9]`, 3m–86m), so results stay dimensionally coherent even when randomized.

Three synchronized views:
- **3D** — Three.js orbit view of the full massing, with a picture-in-picture toggle
- **Plan** — grid layout showing volume footprint, merges, and voids
- **Elevation** — facade drawing per volume, with panel/window subdivision

### Presets

| Preset | Description |
|---|---|
| **Tower** | Manhattan skyline cluster — 6×2 grid, BLUE[5]–[9] heights (12m–86m), neutral palette, portrait punched windows |
| **Podium** | Gropius/Bauhaus office block — wide merged floor plates, spandrel/vision curtain wall, warm concrete tones |
| **Courtyard** | Haussmann perimeter block — 7×7 grid, high merge fuses solid wings, voids carve a central court |

### Palettes

`Mondrian` (primary red/blue/yellow on cream) · `Unité` (Le Corbusier brise-soleil ochres) · `Habitat` (Brutalist concrete greys) · `Neutral` (pure greyscale for proportion studies)

### Modes

- **Simple** — Scale, Height, Windows, Density, and preset buttons for fast exploration
- **Advanced** — full plan grid control (columns/rows, merge/void probability, bay width, depth unit), facade parameters (window proportions, relief depth, glaze probability), and independent Blue Series index range per axis

Compositions are seed-based (`grid`, `merge`, `color`, `z` seeds) — every result is unique but reproducible, with individual seed locking for iterative refinement.

---

## Project structure

```
modular.massing/
├── index.html          Single-file app — HTML, CSS, JS, Three.js scene, all in one
├── audit_deploy.js      148-check pre-deploy validation script
└── HANDOFF_vXX.md       Per-version changelog and handoff notes
```

There is no build step. `index.html` is deployed as-is.

## Handoff protocol

Every version produces three files together: `index.html`, `audit_deploy.js`, `HANDOFF_vXX.md`. A new working session starts by uploading all three and running the audit script before making any changes, to confirm the starting state is clean.

## Critical invariants — do not modify

These are load-bearing for camera/interaction behavior and have broken silently in the past when touched incidentally:

- `setupOrbit`
- `mousemove` handler
- `orb.dragging`
- `orb.right`
- `panX` / `panZ` accumulation signs

## Known open issues

- Plan zoom and 3D frustum are not decoupled
- Picture-in-picture expand button has no handler wired up
- Elevation drawing panels need live browser verification pass
- Neutral palette reads flat in some compositions

---

## Local development

No build tooling required — open `index.html` directly in a browser, or serve it with any static file server. Onboarding callouts are gated behind `localStorage` key `modulor_onboarded_v53`; clear it to re-trigger the first-run walkthrough.

## Deployment

Push to `main` on `JoeK212/modular.massing` — Netlify continuous deployment builds and publishes automatically to `mondrainmodularmassing.netlify.app`, aliased at `modulor-massing.axisbim.io`.

---

*Joe K. · [axisbim.io](https://axisbim.io)*
