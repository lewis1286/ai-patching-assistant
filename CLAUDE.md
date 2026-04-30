# AI Patching Assistant — Claude Context

## What This Is

A Claude Code skill for designing and documenting Eurorack modular synthesis patches. Produces interactive, self-contained HTML pages suitable for a static website, alongside markdown documentation.

The owner patches a single Tiptop Audio Mantis case (104HP × 2 rows, 19 modules documented). Two additional cases exist but aren't inventoried yet.

---

## Key Files

| File | Role |
|------|------|
| `eurorack-patcher-skill-template.md` | The Claude Code skill definition — invoke this when working on patches |
| `modules/inventory.md` | **Source of truth** for all available modules. Read this first before any patch work. Never guess what modules exist. |
| `templates/patch-rf-reference.html` | **Canonical HTML template** (React Flow + ELK auto-layout). Copy this for every new patch and replace only the header metadata + `PATCH = {...}` data object. Schema is documented in the comment at the top of the file. |
| `patches/experimental/house-room-rf.html` | Working complex example using the same template (16 modules, 36 cables) — reference when designing richer patches. |
| `templates/patch-template.md` | Markdown documentation template |
| `templates/astro-patch-page.astro` | Astro page scaffolding for site integration (adapt to match existing viz pages) |
| `templates/miro/symbols/SVG/` | 92 Patch & Tweak SVG symbols (CC BY-ND 4.0) — left over from the retired SVG-illustration approach. Not used by the current React Flow template; kept in case needed for other diagrams. |

---

## Patch Output Convention

Every complete patch generates two files in `patches/[category]/`:
- `patch-name.md` — markdown documentation with cable table
- `patch-name.html` — interactive HTML built from `patch-rf-reference.html`

The `.svg` files in `patches/sequences/` are from an earlier workflow and kept for reference.

---

## HTML Generation Rules (critical)

1. Always read `templates/patch-rf-reference.html` before generating HTML — copy that file rather than inventing structure from scratch.
2. Edit only two regions per patch: the header HTML (`<title>`, `<h1 id="ph-title">`, the four `.patch-meta` spans) and the `PATCH = {...}` object. Leave the rest of the file untouched.
3. Layout, edge routing, back-edge handling, and badge placement are all automatic — do **not** write `x/y` positions, bezier paths, or SVG symbols.
4. Module ids in `cables[]` must exactly match a module in `modules[]`, and `fromPort`/`toPort` must exactly match a string in that module's `outputs[]`/`inputs[]`. Typos cause dangling edges.
5. The file uses CDN imports for React, React Flow, htm, and elkjs — internet required at first load. Acceptable since these patches end up as Astro pages on the owner's site.
6. Signal type colors are fixed: audio `#E24A33`, CV `#348ABD`, gate `#52A35F`, clock `#E5AE38`, V/Oct `#9B59B6`.

---

## Current State

- **PDF manuals**: Stored on the owner's other machine, not available here. Use general module knowledge and the inventory notes instead of looking for manual files.
- **Two undocumented cases**: They exist but aren't in `modules/inventory.md` yet. Don't invent modules — only use what's in the inventory.
- **Astro site**: The owner's site (Astro on Cloudflare Pages) is private on GitHub. `templates/astro-patch-page.astro` is scaffolding — the owner will adapt it to match their existing `src/pages/viz` style on their other machine.

---

## Conventions

- Module inventory is the only source of truth for what's available. If a module isn't listed, don't include it in a patch.
- Patch HTML files open in a browser directly from the filesystem — no build step.
- The `templates/patch-rf-reference.html` rendering engine (everything outside the `PATCH = {...}` object and the header metadata) is reused verbatim across all patches.
- When documenting an existing patch conversationally: extract structure, ask only for genuinely ambiguous details, confirm the cable table before writing files.
