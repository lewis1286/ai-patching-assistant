---
title: Module Symbol Mapping
last_updated: 2026-04-04
---

# Symbol Mapping

Maps each module to its Patch & Tweak SVG symbol.
Symbols are in `templates/miro/symbols/SVG/`.
License: CC BY-ND 4.0 — Patch & Tweak by Kim Bjørn and Chris Meyer, published by Bjooks.

## Mantis Case Modules

| Module | Manufacturer | SVG Symbol File | Notes |
|--------|--------------|-----------------|-------|
| STO | Make Noise | `sawtooth-wave-oscillator.svg` | Primary waveform is triangle, but sawtooth symbol is closest VCO |
| Polaris | Intellijel | `low-pass-filter-resonant.svg` | Multimode filter, LP is most common use |
| Zadar | Xaoc Devices | `eg-adsr.svg` | Quad envelope generator |
| MATHS | Make Noise | `looping-eg-ar.svg` | Function generator — looping AR best represents its dual role |
| Beads | Mutable Instruments | `granular-synthesis.svg` | Granular texture synthesizer |
| Squid Salmple | ALM Busy Circuits | `sample-player.svg` | 8-channel sample player |
| MFX | ALM Busy Circuits | `reverb.svg` | Multi-effects; reverb chosen as representative |
| Daisy Patch | Electrosmith | `custom-module.svg` | Programmable DSP — no fixed function |
| Bloom V2 | Qu-Bit Electronix | `cv-gate-sequencer.svg` | Fractal sequencer with CV + gate outputs |
| Pleiades | CalSynth | `physical-modelling-generic.svg` | Plaits clone macro-oscillator; physical modeling symbol represents its multi-engine nature |
| Pamela's PRO Workout | ALM Busy Circuits | `source-clock.svg` | Master clock + euclidean/LFO outputs |
| Quad VCA | Intellijel | `amplifier-vca.svg` | 4-channel VCA with mix output |
| Mega Milton | ALM Busy Circuits | `mixer-audio.svg` | 4-channel audio mixer |
| DATA | Mordax | `custom-module.svg` | Monitoring/analysis only — no processing function |
| Buff Mult with Attenuators | Arcus Audio | `buffered-multiple.svg` | Buffered multiple with per-output attenuation |
| Listen IO | 4ms Company | `custom-module.svg` | I/O interface to external gear |
| Passive Multiple | 4ms Company | `custom-module.svg` | Passive passive mult — no dedicated symbol |
| disting EX | Expert Sleepers | `custom-module.svg` | Multi-algorithm; use custom-module, annotate algorithm |

## Signal Type Color Reference (for SVG diagrams)

| Signal Type | Color | Hex | SVG Stroke |
|-------------|-------|-----|------------|
| Audio | Red | #E24A33 | `stroke="#E24A33"` |
| CV / Modulation | Blue | #348ABD | `stroke="#348ABD"` |
| Gate / Trigger | Green | #52A35F | `stroke="#52A35F"` |
| Clock | Yellow | #E5AE38 | `stroke="#E5AE38"` |
| V/Oct Pitch | Purple | #9B59B6 | `stroke="#9B59B6"` |
