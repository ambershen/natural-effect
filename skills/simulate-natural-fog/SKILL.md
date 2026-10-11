---
name: simulate-natural-fog
description: Create or refine interactive fogged glass and condensation surfaces with writing, broad wiping, gradual recovery, and live camera or image backgrounds. Use for temporary canvas experiences rather than atmospheric fog volumes.
---

# Simulate Natural Fog

Build a translucent surface that can be locally cleared. Separate the background view, fog veil, clearing mask, and recovery state. In the States of Water direction, this is a Temporary Canvas: the background remains present, and touch changes how clearly it can be seen.

## Material response

- Writing clears a narrow feathered path; palm wiping clears a substantially broader area. Keep gesture recognition separate from mask rendering so touch and camera input can share the material response.
- Use spatially sampled strokes to bridge input samples without dotted gaps. Keep each contact's previous position independent and end it on release or interruption.
- Preserve a gesture coherently while it is active. If recovery starts after release, age the completed gesture consistently so its beginning does not disappear while its end is still being drawn.
- Recover through gradual local opacity and edge softness changes. Avoid isolated circular nuclei, hard final disappearance, or indefinitely visible residual marks unless requested.

## Appearance and controls

Use a blurred version of the actual background beneath a subtle cloudy veil. For a live mirror, update both the clear and blurred views and use the same cover crop and mirror transform for hand coordinates. Avoid baked highlights that remain when fog density approaches zero. Scale fog texture with fog opacity; at zero density, the background should remain clean.

Treat controls as perceptual mappings unless an actual thermodynamic model exists. In the accepted study, Dirty Level controls veil opacity, and warmer Temperature makes the veil lighter with less blur. This is an artistic mapping, not a dew-point calculation. Preserve an explicit user mapping if it differs.

Droplets are optional, not a requirement for condensation. The accepted study omits them at all temperatures. If requested elsewhere, model accumulation, gravity-driven movement, merging, and trails; do not add fixed glossy beads as a shortcut. Recovery timing can remain internal without exposing Hold or Fade controls.

Breath input is a separate optional adapter. Microphone noise alone cannot identify the mouth's location or reliably distinguish breath from speech and room noise. Keep it opt-in and experimental until tested with the selected microphone. Do not claim that breath-localized clearing is implemented when clearing is centered. If sound is requested, audition real rubbing recordings and movement-controlled envelopes; do not infer success from audio decoding.

## Verification

Sweep density and temperature through their full ranges, including near-zero density and maximum temperature. Check for fixed light spots, residual particles, halos, and droplets appearing unexpectedly. Test narrow writing, broad wiping, release, recovery, reset, resize, and camera crop alignment. Check repeated mode switches and interruption for connecting lines. Cache brush textures and bound stroke history or compact it for long sessions.

For the accepted implementation, parameters, and unfinished experiments, read [references/fog-study.md](references/fog-study.md). `natural-motion-interaction` can guide camera adapters when available, but is not required.
