# House Room

**Category**: Experimental
**Complexity**: Complex
**Voices**: 3 melodic (STO, Plaits, Beads) + 4-channel drum kit

## Concept

A house-music groove that slowly dissolves into a degraded room resonance — inspired by William Basinski's *Disintegration Loops* and Alvin Lucier's *I Am Sitting in a Room*. A four-on-the-floor kick/snare/hat pattern from Squid Salmple grounds the patch, while three melodic voices (STO through Polaris, Plaits, and Beads) are driven by Bloom's fractal sequencer. The signal runs into an MFX reverb, then Beads granular processor, and splits: one path goes directly to the Listen IO output, the other feeds a Daisy Patch buffer-swap loop (triggered by Pams) that re-records and replays audio through a Disting EX convolver. That convolved signal re-enters the main Quad VCA mix, creating an accumulating room resonance that gradually transforms and degrades the original signal over time.

## Signal Flow

```
PAMS ──out1──► BLOOM ──note1──► STO ──complex──► POLARIS LP ──► QUAD VCA ch1
  │              ├──note2────────────────────────────────────────► BEADS pitch
  │              ├──note3──► PLAITS ─────────────────────────────► MEGA MILTON mixer
  │              └──gate3──► PLAITS trig
  │
  ├──out2 (stack)──► MFX clock
  ├──out2 (stack)──► BEADS seed
  ├──out3──► DAISY PATCH gate in 1
  ├──out5..8──► SQUID SALMPLE trig 1..4 (kick / snare / closed hat / open hat)
  └──out1──► BLOOM clock

ZADAR A──► SQUID CV in 1 (snare pitch)
ZADAR C──► POLARIS FM2
ZADAR D──► MFX CV in 1

SQUID 1+2 out (stack) ──► MEGA MILTON mixer in
                      └──► MATHS ch1 signal in ──► QUAD VCA CV in 1 (sidechain)
SQUID mix out ──► MEGA MILTON mixer in (hats only)
STO sub ──► QUAD VCA ch2

MEGA MILTON mixer out ──► QUAD VCA ch3
DISTING EX out ──────────► QUAD VCA ch4

QUAD VCA mix out ──► MEGA MILTON buff mult in
                     ├──out2──► MFX L in
                     └──out3──► MFX R in

MFX out L/R ──► BEADS L/R in

BEADS L out ──► ARCUS BUFF MULT in 1 ──1a──► LISTEN IO L
                                      └──1b──► DAISY PATCH in 1 ──► DISTING EX in 1
                                                                       └──► QUAD VCA ch4 (feedback loop)
BEADS R out ──► ARCUS BUFF MULT in 2 ──2a──► LISTEN IO R
```

## Module Settings

### Pamela's PRO Workout
- Out 1: Master clock, 120–128 BPM, ÷1 (to Bloom)
- Out 2: Clock for MFX sync + Beads freeze/seed — try ÷4 or ÷8
- Out 3: Gate pattern for Daisy buffer swap — try Euclidean 3/8 or ÷16
- Out 5: Kick trigger — ÷1 (four-on-the-floor)
- Out 6: Snare trigger — ÷2 offset (on the 2 and 4)
- Out 7: Closed hat — ÷2 or ÷4
- Out 8: Open hat — Euclidean or ÷8

### Bloom V2
- Note 1: Drives STO (main melodic bass/lead voice)
- Note 2: Drives Beads pitch (granular voice)
- Note 3: Drives Plaits (harmonic engine)
- Gate 3: Triggers Plaits internal LPG
- Scale: Minor or Dorian recommended for house
- Mutation: Start at 0; increase slowly for evolving variations
- Branches: 1–2

### STO
- Frequency: C2–C3 range
- Complex output used (to Polaris): richer waveform
- Sub output used (to Quad VCA ch2): low sub voice, unfiltered

### Polaris
- Mode: LP (Lowpass)
- Cutoff: ~40–50% — main performance control
- Resonance: ~15–25%
- FM2 attenuator: ~40–60% (Zadar C modulates cutoff)

### Zadar
- Out A: Envelope for snare pitch CV — short AD, medium decay
- Out B: Unused
- Out C: Filter FM envelope for Polaris — medium AD
- Out D: MFX parameter CV — slow LFO-like or triggered shape
- All: Triggered mode (not cycling) unless using D for LFO effect

### Plaits (Pleiades)
- Engine: Harmonic oscillator (model knob position ~7 o'clock from default)
- Harmonics: ~50% for chord-like texture
- V/Oct from Bloom note 3, Gate/Trig from Bloom gate 3

### Maths
- Ch1: Receives Squid 1+2 (kick+snare) as input signal
- Rise: Fast (~9 o'clock)
- Fall: Medium-slow (~2 o'clock) — controls sidechain pump length
- Ch1 output: Quad VCA CV in 1 — duck the filtered STO on every kick+snare hit

### Squid Salmple
- Ch1: Kick drum (4-on-the-floor from Pams out 5)
- Ch2: Snare (Pams out 6, pitch CV from Zadar A)
- Ch3: Closed hat (Pams out 7)
- Ch4: Open hat (Pams out 8)
- Ch5–8: Unused in this patch
- 1+2 out patched out (removes kick+snare from main mix; separate pre-fader send)

### Quad VCA
- Ch1 (Polaris LP): Exponential, level ~80%, CV from Maths ch1 (sidechain)
- Ch2 (STO sub): Linear, level ~50%
- Ch3 (Mega Milton mix): Linear, level ~70%
- Ch4 (Disting EX convolver): Linear, start at 0 — fade in slowly for room effect
- Mix out: Full summed output to Mega Milton buff mult in

### Mega Milton
- Mixer section inputs: Plaits, Squid 1+2, Squid mix (hats) — set relative levels by ear
- Mixer out: Quad VCA ch3
- Buff mult in: Quad VCA mix out (final bus)
- Buff mult outs 2 & 3: To MFX L and R (stereo send)
- Buff mult out 1: Unused

### MFX
- Algorithm: Reverb (or hall)
- Clock in: Pams out 2 (synced delay/reverb time)
- CV in 1: Zadar D (modulates reverb depth/time)
- Stereo in/out used

### Beads
- Seed in: Pams out 2 (periodic freeze of the buffer)
- Pitch in: Bloom note 2 (pitched granular voice)
- Density, Texture, Size: Set by ear — start sparse, increase over time
- Quality: High mode recommended

### Daisy Patch
- Firmware: Looping buffer swap — records audio for N cycles, then plays back and re-records
- Gate in 1: Pams out 3 (triggers buffer swap)
- Audio in 1: Arcus buff mult 1b (left channel of granular output)
- Audio out 1: Disting EX in 1

### Disting EX
- Algorithm: Convolver
- Input 1: Daisy Patch out 1 (degraded/re-recorded audio)
- IR loaded: Room or hall impulse response
- Output: Quad VCA ch4 (feedback into main mix)

### Arcus Buff Mult
- In 1 (Beads L): out 1a → Listen IO L, out 1b → Daisy Patch in 1
- In 2 (Beads R): out 2a → Listen IO R
- Attenuators: All at unity

### Listen IO
- L in: Arcus buff mult 1a
- R in: Arcus buff mult 2a
- Output: To monitors / DAW

## Modulation Routing

| Source | Destination | Amount | Notes |
|--------|-------------|--------|-------|
| Zadar A | Squid CV in 1 (snare pitch) | Short AD | Subtle pitch variation on snare |
| Zadar C | Polaris FM2 | Med AD | Filter cutoff envelope (synth voice) |
| Zadar D | MFX CV in 1 | Slow/looping | Reverb parameter sweep |
| Maths ch1 | Quad VCA CV in 1 | Full range | Sidechain duck on kick+snare hits |
| Pams out 2 | Beads seed + MFX clock | Gate/clock | Periodic texture freeze + effect sync |

## Patch Cable Table

### Clock

| Cable | Output Module | Output Jack | Input Module | Input Jack | Type | Notes |
|-------|--------------|------------|-------------|-----------|------|-------|
| 1 | Pams | Out 1 | Bloom V2 | Clock in | Clock | Master tempo |
| 2 | Pams | Out 2 | MFX | Clock in | Clock | Effect sync (stacked) |
| 3 | Pams | Out 2 | Beads | Seed in | Gate | Granular freeze (stacked) |

### V/Oct

| Cable | Output Module | Output Jack | Input Module | Input Jack | Type | Notes |
|-------|--------------|------------|-------------|-----------|------|-------|
| 4 | Bloom V2 | Note 1 | STO | 1V/Oct | V/Oct | Sequenced pitch to main osc |
| 5 | Bloom V2 | Note 2 | Beads | Pitch | V/Oct | Sequenced pitch to granular voice |
| 6 | Bloom V2 | Note 3 | Plaits | 1V/Oct | V/Oct | Sequenced pitch to harmonic engine |

### Gate / Trigger

| Cable | Output Module | Output Jack | Input Module | Input Jack | Type | Notes |
|-------|--------------|------------|-------------|-----------|------|-------|
| 7 | Bloom V2 | Gate 3 | Plaits | Trig | Gate | Triggers Plaits internal LPG |
| 8 | Pams | Out 3 | Daisy Patch | Gate in 1 | Gate | Triggers buffer swap |
| 9 | Pams | Out 5 | Squid Salmple | Trig 1 | Gate | Kick trigger |
| 10 | Pams | Out 6 | Squid Salmple | Trig 2 | Gate | Snare trigger |
| 11 | Pams | Out 7 | Squid Salmple | Trig 3 | Gate | Closed hat trigger |
| 12 | Pams | Out 8 | Squid Salmple | Trig 4 | Gate | Open hat trigger |

### Modulation CV

| Cable | Output Module | Output Jack | Input Module | Input Jack | Type | Notes |
|-------|--------------|------------|-------------|-----------|------|-------|
| 13 | Zadar | Out A | Squid Salmple | CV in 1 | CV | Snare pitch modulation |
| 14 | Zadar | Out C | Polaris | FM2 in | CV | Filter cutoff modulation |
| 15 | Zadar | Out D | MFX | CV in 1 | CV | Effect parameter sweep |
| 16 | Maths | Ch1 out | Quad VCA | CV in 1 | CV | Sidechain compression |

### Audio Signal Path

| Cable | Output Module | Output Jack | Input Module | Input Jack | Type | Notes |
|-------|--------------|------------|-------------|-----------|------|-------|
| 17 | STO | Complex out | Polaris | In | Audio | Main osc voice into filter |
| 18 | STO | Sub out | Quad VCA | In 2 | Audio | Sub voice, unfiltered |
| 19 | Polaris | LP out | Quad VCA | In 1 | Audio | Filtered STO voice |
| 20 | Plaits | Out | Mega Milton | Mixer in | Audio | Harmonic voice into drum mix |
| 21 | Squid Salmple | 1+2 out | Mega Milton | Mixer in | Audio | Kick+snare (stacked, pre-fader) |
| 22 | Squid Salmple | 1+2 out | Maths | Ch1 signal in | Audio | Kick+snare to sidechain env (stacked) |
| 23 | Squid Salmple | Mix out | Mega Milton | Mixer in | Audio | Hats only (ch1+2 removed from mix) |
| 24 | Mega Milton | Mixer out | Quad VCA | In 3 | Audio | Pre-effects mix bus |
| 25 | Disting EX | Out 1 | Quad VCA | In 4 | Audio | Convolved room signal (feedback) |
| 26 | Quad VCA | Mix out | Mega Milton | Buff mult in | Audio | Final bus to distribution |
| 27 | Mega Milton | Buff mult out 2 | MFX | In L | Audio | Left send to reverb |
| 28 | Mega Milton | Buff mult out 3 | MFX | In R | Audio | Right send to reverb |
| 29 | MFX | Out L | Beads | In L | Audio | Effected signal into granular |
| 30 | MFX | Out R | Beads | In R | Audio | Effected signal into granular |
| 31 | Beads | L out | Arcus buff mult | In 1 | Audio | Left granular to output split |
| 32 | Beads | R out | Arcus buff mult | In 2 | Audio | Right granular to output split |
| 33 | Arcus buff mult | 1a out | Listen IO | L in | Audio | Left output to monitors |
| 34 | Arcus buff mult | 1b out | Daisy Patch | In 1 | Audio | Left channel into degradation loop |
| 35 | Daisy Patch | Out 1 | Disting EX | In 1 | Audio | Re-recorded buffer into convolver |
| 36 | Arcus buff mult | 2a out | Listen IO | R in | Audio | Right output to monitors |

### Cable Summary

| Location | Cable Count |
|----------|------------|
| Mantis | 36 |
| **Total** | **36** |

## Performance Tips

- **Start Quad VCA ch4 at zero.** Fade Disting EX level in slowly after the groove is established — the room degradation is most striking when heard entering an existing texture rather than from the start.
- **Daisy buffer swap rate** is the key to the Lucier effect. A slow Pams out 3 rate (long between swaps) produces gradual, subtle degradation. A fast rate creates stuttering artifacts. Try ÷32 to start, then experiment.
- **Sidechain pump:** Maths fall time controls how long the Quad VCA ch1 ducks after each kick/snare hit. A medium-slow fall (~2 o'clock) gives classic house pumping. Shorter fall = tighter, drier feel.
- **Bloom mutation** for variation: Start mutation at 0 for a steady groove, then slowly increase to introduce melodic variation. The fractal algorithm keeps all three voices harmonically related even as they evolve.
- **Polaris as a performance control:** Sweep cutoff manually during playback. The Zadar C envelope adds attack to the filter — raising the cutoff base frequency shifts the character from dark/filtered to open/bright.
- **Beads seed rate** (Pams out 2) determines how often the granular buffer freezes. A slow rate lets the granular texture evolve naturally. Stopping it (or unpatching) freezes Beads permanently for a drone-like pad.
- **Zadar B** is unused — patch it to Beads density or position for an additional modulation layer as the patch evolves.

---
*Generated by Claude Code with eurorack-patcher skill*
*Date: 2026-04-29*
