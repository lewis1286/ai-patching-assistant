# AI Patching Assistant

A Claude Code skill for designing and documenting Eurorack modular synthesis patches. Describes patches conversationally, generates interactive HTML signal flow diagrams, and produces documentation suitable for a static website.

## What It Does

- **Design patches** from scratch given a sound goal or technique
- **Document existing patches** from a free-form verbal description
- **Generate interactive HTML** — standalone, self-contained patch pages with:
  - Color-coded signal flow diagram (audio, CV, gate, clock, V/Oct)
  - Cable hover tooltips showing source → destination and purpose
  - Signal type filter toggles (show/hide cable types)
  - Module detail panels (click any module to see its settings)
  - Animated signal flow (moving dashes showing signal direction)
- **Save markdown documentation** alongside the HTML for reference

## Directory Structure

```
ai-patching-assistant/
├── eurorack-patcher-skill-template.md   ← Claude Code skill definition
│
├── modules/
│   └── inventory.md                    ← Module inventory (source of truth)
│
├── patches/
│   ├── sequences/
│   │   ├── basic-east-coast.md         ← Patch documentation (markdown)
│   │   ├── basic-east-coast.html       ← Interactive patch page (standalone HTML)
│   │   └── basic-east-coast.svg        ← Static signal flow diagram
│   ├── drones/
│   ├── percussion/
│   ├── effects/
│   └── experimental/
│
└── templates/
    ├── patch-template.md          ← Markdown documentation template
    ├── patch-rf-reference.html    ← Canonical interactive HTML template (React Flow + ELK)
    └── miro/symbols/SVG/          ← Patch & Tweak symbol set, kept for reference
```

## Usage

### Invoking the Skill

Use the skill in Claude Code by referencing `eurorack-patcher-skill-template.md`. The skill reads `modules/inventory.md` on every invocation — that file is the source of truth for what modules are available.

### Designing a New Patch

```
User: design a generative drone patch using MATHS and Beads
```

The skill will suggest a patch design, then automatically save:
- `patches/drones/maths-beads-drone.md`
- `patches/drones/maths-beads-drone.html`

### Documenting an Existing Patch

Describe your patch however feels natural — the skill extracts structure and asks targeted follow-up questions only when something is ambiguous:

```
User: I want to document my current patch. Pamela is clocking Bloom on out 1,
      Bloom CV goes through the buff mult into the STO. Gate out from Bloom
      splits via passive mult to Zadar channels 1 and 2...
```

The skill will confirm the cable table, then generate both files.

### Viewing Interactive HTML

Open any `.html` file in `patches/` directly in a browser. No server required — all files are fully self-contained.

## Interactive HTML Features

| Feature | How to Use |
|---------|-----------|
| Cable hover | Move cursor over any cable to see source, destination, and purpose |
| Signal filter | Click `[Audio]` `[CV]` `[Gate]` `[Clock]` `[V/Oct]` to show/hide cable types |
| Module panel | Click any module icon to see its knob settings for this patch |
| Animation | Click `▶ Animate` to enable moving dashes showing signal flow direction |

## Adding a New Module to the Inventory

Edit `modules/inventory.md` directly. The skill reads this file on every use — no other configuration needed. Add the module to the appropriate category table and update the system stats at the bottom.

## Astro Site Integration

`templates/astro-patch-page.astro` is scaffolding for integrating patch pages into an Astro site. Two options:

**Iframe embed** (simplest): Copy `.html` patch files into `public/patches/` and embed via `<iframe>`. Zero parsing, full interactivity preserved.

**Content collection** (recommended): Extract the `PATCH` data object from the HTML into a `.json` file, create a content collection, and use a client-side island component to render the interactive diagram natively within the site layout.

## Symbol License

SVG symbols in `templates/miro/symbols/SVG/` are from *Patch & Tweak* by Kim Bjørn and Chris Meyer, published by Bjooks. Licensed under [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/) — free to use with attribution, no modifications.

All generated patch HTML files include the required attribution in the footer.
