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
| `templates/patch-interactive-reference.html` | **Canonical HTML template** — read before generating any interactive patch HTML. Contains the full PATCH data schema, rendering engine, and all interactive JS. |
| `templates/miro/symbol-mapping.md` | Maps each physical module to its Patch & Tweak SVG symbol file |
| `templates/miro/symbols/SVG/` | 92 SVG module symbols (Patch & Tweak, CC BY-ND 4.0) |
| `templates/patch-template.md` | Markdown documentation template |
| `templates/astro-patch-page.astro` | Astro page scaffolding for site integration (adapt to match existing viz pages) |

---

## Patch Output Convention

Every complete patch generates two files in `patches/[category]/`:
- `patch-name.md` — markdown documentation with cable table
- `patch-name.html` — standalone interactive HTML (no server needed, no external deps)

The `.svg` files in `patches/sequences/` are from an earlier workflow and kept for reference.

---

## HTML Generation Rules (critical)

1. Always read `templates/patch-interactive-reference.html` before generating HTML — don't invent the structure from scratch.
2. Embed only the SVG symbols used in the patch. Prefix all CSS class names with the module id to avoid conflicts (`.cls-1` → `.polaris-cls-1`).
3. SVG symbols must be embedded **unmodified** — CC BY-ND 4.0 forbids derivatives. Attribution footer is required.
4. The file must be fully self-contained — no external URLs, no CDN links.
5. Signal type colors are fixed: audio `#E24A33`, CV `#348ABD`, gate `#52A35F`, clock `#E5AE38`, V/Oct `#9B59B6`.

---

## Current State

- **PDF manuals**: Stored on the owner's other machine, not available here. Use general module knowledge and the inventory notes instead of looking for manual files.
- **Two undocumented cases**: They exist but aren't in `modules/inventory.md` yet. Don't invent modules — only use what's in the inventory.
- **Astro site**: The owner's site (Astro on Cloudflare Pages) is private on GitHub. `templates/astro-patch-page.astro` is scaffolding — the owner will adapt it to match their existing `src/pages/viz` style on their other machine.

---

## Conventions

- Module inventory is the only source of truth for what's available. If a module isn't listed, don't include it in a patch.
- Patch HTML files open in a browser directly from the filesystem — no build step.
- The `templates/patch-interactive-reference.html` rendering engine (JS below the `PATCH` object) is reused verbatim across all patches. Only the `PATCH` data object changes per patch.
- When documenting an existing patch conversationally: extract structure, ask only for genuinely ambiguous details, confirm the cable table before writing files.
